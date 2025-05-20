# 3D房屋模型应用实现细节

## 技术实现概述

本文档详细记录了3D房屋模型应用的实现细节，包括HTML结构、CSS样式、JavaScript代码和Three.js实现。

## HTML结构

应用的HTML结构主要分为两部分：

1. **Canvas容器**：用于渲染3D场景
2. **菜单区域**：用于显示可选择的房屋部分和控制按钮

```html
<div id="container">
  <div id="canvas-container">
    <canvas id="house-canvas"></canvas>
    <div id="info">使用鼠标拖动旋转视图，滚轮缩放，右键拖动平移</div>
  </div>
  <div id="menu">
    <div class="menu-header">...</div>
    <div class="menu-item" data-part="roof">...</div>
    <div class="menu-item" data-part="walls">...</div>
    <div class="menu-item" data-part="windows">...</div>
    <div class="menu-item" data-part="doors">...</div>
    <div class="controls">
      <button id="reset-view">重置视图</button>
    </div>
  </div>
</div>
```

每个菜单项使用`data-part`属性存储对应的部件名称，便于JavaScript代码获取。

## CSS样式

CSS样式主要实现以下功能：

1. **布局样式**：使用Flexbox实现左右双栏布局
2. **菜单样式**：美化菜单项和控制按钮
3. **交互状态**：定义菜单项的悬停和选中状态

关键CSS样式：

```css
#container {
  display: flex;
  width: 100vw;
  height: 100vh;
}

#canvas-container {
  flex: 1;
  position: relative;
}

#menu {
  width: 250px;
  background-color: #f8f8f8;
  border-left: 1px solid #ddd;
}

.menu-item {
  padding: 15px 20px;
  border-bottom: 1px solid #eee;
  cursor: pointer;
  display: flex;
  align-items: center;
}

.menu-item.active {
  background-color: #e6f7ff;
  border-left: 3px solid #1890ff;
}
```

## Three.js实现

### 初始化

```javascript
// 场景初始化
const scene = new THREE.Scene();
scene.background = new THREE.Color(0xf0f0f0);

// 设置渲染器
const renderer = new THREE.WebGLRenderer({ 
  canvas: canvas,
  antialias: true 
});
renderer.setSize(canvas.parentElement.clientWidth, canvas.parentElement.clientHeight);
renderer.shadowMap.enabled = true;

// 设置相机
const camera = new THREE.PerspectiveCamera(
  45, 
  canvas.parentElement.clientWidth / canvas.parentElement.clientHeight, 
  0.1, 
  1000
);
camera.position.set(10, 8, 15);
camera.lookAt(0, 0, 0);

// 添加轨道控制器
const controls = new OrbitControls(camera, renderer.domElement);
controls.enableDamping = true;
controls.dampingFactor = 0.05;
```

### 光照设置

```javascript
// 环境光
const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
scene.add(ambientLight);

// 平行光（模拟太阳光）
const directionalLight = new THREE.DirectionalLight(0xffffff, 0.8);
directionalLight.position.set(10, 20, 15);
directionalLight.castShadow = true;
directionalLight.shadow.mapSize.width = 2048;
directionalLight.shadow.mapSize.height = 2048;
scene.add(directionalLight);
```

### 模型创建

房屋模型使用组(Group)组织，便于管理和选择：

```javascript
// 创建房屋组
const house = new THREE.Group();
scene.add(house);

// 创建房屋基础（地基）
const foundationGeometry = new THREE.BoxGeometry(10, 0.5, 8);
const foundationMaterial = new THREE.MeshStandardMaterial({ color: 0x808080 });
const foundation = new THREE.Mesh(foundationGeometry, foundationMaterial);
foundation.position.y = 0.25;
foundation.receiveShadow = true;
house.add(foundation);

// 创建墙壁组
const walls = new THREE.Group();
walls.name = "walls";
house.add(walls);

// 创建主体墙壁
const mainWallsGeometry = new THREE.BoxGeometry(9, 3, 7);
const mainWalls = new THREE.Mesh(mainWallsGeometry, wallMaterial);
mainWalls.position.y = 2;
mainWalls.castShadow = true;
mainWalls.receiveShadow = true;
walls.add(mainWalls);

// 创建屋顶组
const roof = new THREE.Group();
roof.name = "roof";
house.add(roof);

// 创建主屋顶
const mainRoofGeometry = new THREE.ConeGeometry(7, 3, 4);
mainRoofGeometry.rotateY(Math.PI / 4);
const mainRoof = new THREE.Mesh(mainRoofGeometry, roofMaterial);
mainRoof.position.y = 5;
mainRoof.castShadow = true;
roof.add(mainRoof);
```

### 窗户创建

窗户使用函数创建，便于在不同位置添加相同样式的窗户：

```javascript
// 添加窗户函数
function addWindow(x, y, z, rotationY = 0) {
  const windowGroup = new THREE.Group();
  
  // 窗框
  const frameGeometry = new THREE.BoxGeometry(1.2, 1.2, 0.1);
  const frame = new THREE.Mesh(frameGeometry, windowFrameMaterial);
  frame.castShadow = true;
  windowGroup.add(frame);
  
  // 窗玻璃
  const glassGeometry = new THREE.BoxGeometry(1, 1, 0.05);
  const glass = new THREE.Mesh(glassGeometry, windowMaterial);
  glass.position.z = 0.05;
  windowGroup.add(glass);
  
  windowGroup.position.set(x, y, z);
  windowGroup.rotation.y = rotationY;
  windows.add(windowGroup);
}

// 添加窗户
addWindow(-4.5, 2, 0, Math.PI / 2); // 左侧窗户
addWindow(4.5, 2, 0, -Math.PI / 2); // 右侧窗户
addWindow(0, 2, 3.5); // 前面窗户
addWindow(0, 2, -3.5, Math.PI); // 后面窗户
```

### 高亮功能实现

高亮功能通过替换材质实现：

```javascript
// 高亮显示选中的部分
let highlightedPart = null;
const originalMaterials = new Map();
const highlightMaterial = new THREE.MeshStandardMaterial({ 
  color: 0xffff00,
  emissive: 0xffff00,
  emissiveIntensity: 0.2,
  transparent: true,
  opacity: 0.8
});

function highlightPart(partName) {
  // 如果有之前高亮的部分，恢复其原始材质
  if (highlightedPart) {
    resetHighlight();
  }
  
  // 获取要高亮的部分
  const part = house.getObjectByName(partName);
  if (part) {
    highlightedPart = part;
    
    // 保存原始材质并应用高亮材质
    part.traverse(child => {
      if (child.isMesh) {
        originalMaterials.set(child, child.material);
        child.material = highlightMaterial;
      }
    });
  }
}

function resetHighlight() {
  if (highlightedPart) {
    highlightedPart.traverse(child => {
      if (child.isMesh && originalMaterials.has(child)) {
        child.material = originalMaterials.get(child);
      }
    });
    originalMaterials.clear();
    highlightedPart = null;
  }
}
```

### 交互实现

菜单交互通过事件监听器实现：

```javascript
// 添加菜单交互
document.querySelectorAll('.menu-item').forEach(item => {
  item.addEventListener('click', () => {
    // 移除所有活动状态
    document.querySelectorAll('.menu-item').forEach(i => i.classList.remove('active'));
    
    // 添加活动状态到当前项
    item.classList.add('active');
    
    // 高亮显示对应部分
    const partName = item.getAttribute('data-part');
    highlightPart(partName);
  });
});

// 重置视图按钮
document.getElementById('reset-view').addEventListener('click', () => {
  // 重置相机位置
  camera.position.set(10, 8, 15);
  camera.lookAt(0, 0, 0);
  controls.reset();
  
  // 移除高亮
  resetHighlight();
  
  // 移除菜单活动状态
  document.querySelectorAll('.menu-item').forEach(i => i.classList.remove('active'));
});
```

### 动画循环

使用requestAnimationFrame实现动画循环：

```javascript
// 动画循环
function animate() {
  requestAnimationFrame(animate);
  
  controls.update();
  
  renderer.render(scene, camera);
}

animate();
```

### 响应式设计

通过监听窗口大小变化事件实现响应式设计：

```javascript
// 处理窗口大小变化
window.addEventListener('resize', () => {
  const width = canvas.parentElement.clientWidth;
  const height = canvas.parentElement.clientHeight;
  
  camera.aspect = width / height;
  camera.updateProjectionMatrix();
  
  renderer.setSize(width, height);
});
```

## 性能优化

当前实现已采取以下性能优化措施：

1. **材质共享**：相同类型的部件共享材质实例
2. **几何体简化**：使用低多边形模型减少渲染负担
3. **按需渲染**：只在相机或场景变化时渲染

## 已知问题

1. 在某些低性能设备上，阴影渲染可能导致性能下降
2. 当前未实现移动设备的触摸控制优化
3. 高亮效果在某些角度可能不够明显

## 后续优化方向

1. 添加模型加载进度指示器
2. 实现模型的LOD (Level of Detail)
3. 优化移动设备的触摸控制
4. 增强高亮效果的可见性
