# WaterproofViz3D 项目结构概述

## 项目组织

WaterproofViz3D 项目采用模块化的结构组织，清晰地分离了不同类型的模型和文档。项目的主要组成部分包括：

1. **入口页面**：`index.html` 作为项目的主入口，提供模型库和导航功能
2. **模型文件**：按类型组织在 `models` 目录下的各个子目录中
3. **文档文件**：按类型组织在 `docs` 目录下的各个子目录中

## 目录结构

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
    │   ├── project_overview.md        # 项目总体概述
    │   ├── project_structure.md       # 项目结构概述
    │   ├── house_overview.md          # 房屋模型概述
    │   ├── roof_overview.md           # 屋顶模型概述
    │   └── bathroom_overview.md       # 卫生间模型概述
    ├── design/               # 设计文档
    │   └── design_principles.md       # 设计原则
    ├── implementation/       # 实现文档
    │   └── house_implementation.md    # 房屋模型实现
    └── plans/                # 规划文档
        ├── future_plans.md            # 总体未来规划
        ├── product_roadmap.md         # 产品化规划
        └── bathroom_development_plan.md # 卫生间开发计划
```

## 文件关系

### 入口页面与模型文件

`index.html` 作为项目的主入口，提供了一个模型库界面，用户可以在这里浏览和访问所有可用的3D模型。主要特点包括：

1. **模型预览**：每个模型卡片包含一个简化版的3D预览，使用Three.js渲染
2. **分类筛选**：用户可以按房屋、屋顶、卫生间等类别筛选模型
3. **模态窗口**：点击"查看模型"按钮会在当前页面打开一个模态窗口，加载完整的模型页面

当用户点击某个模型的"查看模型"按钮时，对应的模型HTML文件会在模态窗口中加载，例如：
- 点击"基础房屋模型"会加载 `models/house/house_basic.html`
- 点击"屋顶维修模型"会加载 `models/roof/roof_repair.html`

### 模型文件之间的关系

各个模型文件虽然独立存在，但在概念上有一定的层次关系：

1. **房屋模型**是最基础的模型，提供了完整的房屋外形结构
2. **屋顶模型**专注于房屋的屋顶部分，提供更详细的结构和维修步骤
3. **卫生间模型**专注于房屋内部的卫生间，展示漏水问题和维修过程

这些模型可以独立使用，也可以作为整体防水维修解决方案的不同方面。

### 文档文件的组织

文档文件按照其内容和用途组织在不同的子目录中：

1. **overview/**：包含各个模型和项目整体的概述文档
2. **design/**：包含设计原则和设计决策的文档
3. **implementation/**：包含技术实现细节的文档
4. **plans/**：包含未来规划和发展路线的文档

## 技术实现

### 共享技术栈

所有模型页面共享相同的基础技术栈：

1. **Three.js**：用于3D渲染和场景管理
2. **HTML/CSS**：用于用户界面和布局
3. **JavaScript**：用于交互逻辑和动画

### 模块化设计

项目采用模块化设计，主要体现在：

1. **模型组件化**：每个模型都由多个组(Group)和网格(Mesh)组成，便于管理和交互
2. **功能分离**：渲染逻辑、交互逻辑和UI逻辑分离，提高代码可维护性
3. **资源复用**：共享材质、几何体和交互控制代码，减少重复

## 开发与部署流程

### 开发流程

1. **本地开发**：在本地环境中开发和测试新功能
2. **文档更新**：同步更新相关文档，确保文档与代码一致
3. **版本控制**：使用Git进行版本控制，保持清晰的提交历史

### 部署流程

项目使用GitHub Pages进行部署：

1. **代码推送**：将更改推送到GitHub仓库的main分支
2. **自动部署**：GitHub Pages自动从main分支构建和部署网站
3. **访问地址**：部署后的网站可通过 https://franksunye.github.io/WaterproofViz3D/ 访问

## 未来发展

随着项目的发展，项目结构可能会有以下变化：

1. **更多模型类型**：添加更多类型的模型，如窗户、地下室等
2. **共享组件库**：提取常用组件，创建可复用的组件库
3. **构建工具集成**：引入构建工具，优化资源加载和性能
4. **测试框架**：添加自动化测试，确保功能稳定性

## 结论

WaterproofViz3D项目采用清晰、模块化的结构组织，便于维护和扩展。通过入口页面的模型库和独立的模型文件，用户可以方便地浏览和使用各种3D防水维修模型。项目的文档体系全面覆盖了概述、设计、实现和规划等方面，为开发者和用户提供了充分的参考资料。
