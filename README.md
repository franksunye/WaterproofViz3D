# WaterproofViz3D

一个综合性的3D可视化项目，旨在展示房屋不同部位的防水问题和维修过程。该项目包含多个交互式3D模型，包括房屋外观模型、屋顶维修模型和卫生间漏水维修模型，为用户提供直观的防水维修可视化体验。

## 在线演示

访问 [GitHub Pages 演示](https://franksunye.github.io/WaterproofViz3D/) 查看在线演示。

> 注意：GitHub Pages 部署可能需要几分钟时间，如果链接暂时不可用，请稍后再试。

## 功能特点

### 房屋模型
- **交互式3D房屋模型**：完整的房屋外形结构，包括墙壁、屋顶、窗户和门
- **部件选择**：通过右侧菜单选择房屋的主要部分
- **高亮显示**：在3D模型中突出显示用户选择的部分

### 屋顶维修模型
- **层次结构**：展示屋顶的结构层、保温层和防水层
- **维修步骤**：演示屋顶防水维修的各个步骤
- **交互控制**：允许用户逐步查看维修过程

### 卫生间漏水维修模型
- **漏水路径**：展示水如何从卫生间漏到其他区域
- **多视角**：提供上层、下层和剖面等多种视角
- **维修步骤**：详细展示卫生间防水维修的六个步骤
- **动态效果**：水滴动画和材质变化等动态效果

### 通用功能
- **视图控制**：旋转、缩放和平移视图
- **自动演示**：一键演示完整维修流程
- **重置功能**：随时重置到初始状态
- **响应式设计**：适应不同屏幕尺寸

## 快速开始

1. 克隆仓库：
   ```
   git clone https://github.com/franksunye/WaterproofViz3D.git
   ```

2. 打开项目：
   - 使用现代浏览器（Chrome、Firefox、Edge等）打开 `index.html` 文件
   - 或者通过本地服务器访问项目目录
   - 确保启用JavaScript和WebGL

3. 使用说明：
   - 在主页上浏览不同类别的模型
   - 点击任意模型卡片上的"查看模型"按钮打开完整模型
   - 使用鼠标左键拖动旋转视图
   - 使用鼠标滚轮缩放视图
   - 使用鼠标右键拖动平移视图
   - 根据模型不同，使用界面上的按钮控制视角和功能
   - 点击"重置视图"按钮恢复初始视角

## 技术栈

- **前端**：HTML5, CSS3, JavaScript
- **3D渲染**：Three.js
- **动画库**：GSAP (GreenSock Animation Platform)
- **交互控制**：OrbitControls (Three.js addon)

## 项目结构

```
WaterproofViz3D/
├── index.html                # 主页面，模型库入口
├── models/                   # 所有3D模型文件
│   ├── house/                # 房屋相关模型
│   │   └── house_basic.html  # 基础房屋模型
│   ├── roof/                 # 屋顶相关模型
│   │   └── roof_repair.html  # 屋顶维修模型
│   └── bathroom/             # 卫生间相关模型
│       ├── bathroom_basic.html        # 基础卫生间模型
│       ├── bathroom_leakage_basic.html      # 卫生间漏水基础模型
│       ├── bathroom_leakage_external.html   # 卫生间漏水外部视图
│       ├── bathroom_leakage_livingroom.html # 卫生间漏水到客厅模型
│       ├── bathroom_high_fidelity.html      # 高保真卫生间模型
│       └── bathroom_repair.html             # 卫生间维修模型
└── docs/                     # 项目文档
    ├── overview/             # 项目概述文档
    ├── design/               # 设计文档
    ├── implementation/       # 实现文档
    └── plans/                # 规划文档
```

## 文档

### 概述文档
- [项目总体概述](docs/overview/project_overview.md)：项目的基本信息和目标
- [房屋模型概述](docs/overview/house_overview.md)：房屋模型的功能和特点
- [屋顶模型概述](docs/overview/roof_overview.md)：屋顶模型的功能和特点
- [卫生间模型概述](docs/overview/bathroom_overview.md)：卫生间模型的功能和特点

### 设计文档
- [设计原则](docs/design/design_principles.md)：项目的设计理念和规范

### 实现文档
- [房屋模型实现](docs/implementation/house_implementation.md)：房屋模型的技术实现细节

### 规划文档
- [未来规划](docs/plans/future_plans.md)：项目的总体发展方向和计划
- [产品化规划](docs/plans/product_roadmap.md)：产品化的路线图和规划
- [卫生间开发计划](docs/plans/bathroom_development_plan.md)：卫生间模型的开发计划

## 模型预览

### 房屋模型
![房屋模型预览](https://placeholder-for-screenshot.com/house-model-screenshot.png)

### 屋顶维修模型
![屋顶维修模型预览](https://placeholder-for-screenshot.com/roof-repair-screenshot.png)

### 卫生间漏水模型
![卫生间漏水模型预览](https://placeholder-for-screenshot.com/bathroom-leakage-screenshot.png)

### 卫生间维修模型
![卫生间维修模型预览](https://placeholder-for-screenshot.com/bathroom-repair-screenshot.png)

## 浏览器兼容性

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## 贡献指南

1. Fork 项目
2. 创建特性分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 创建Pull Request

## 许可证

[MIT](LICENSE)

## 联系方式

项目维护者：Ye Sun - franksunye@hotmail.com

项目链接：[https://github.com/franksunye/WaterproofViz3D](https://github.com/franksunye/WaterproofViz3D)
