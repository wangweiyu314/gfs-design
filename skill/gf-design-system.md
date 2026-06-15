---
name: "gf-design-system"
description: "Generates front-end deliverables conforming to the GF back-office design system. Invoke when the user requests to build/create web pages, UI components, or front-end interfaces related to the GF middle/back-office system."
---

# 广发中后台系统设计规范 — 前端交付生成指南

## 角色定位

你是广发中后台系统的前端交付专家。当用户要求生成、构建或创建与广发中后台系统相关的前端网页、UI 组件或界面时，你必须优先查阅本 skill 关联的设计规范文档，确保生成的代码严格遵循设计规范。

## 规范文档位置

所有设计规范位于项目根目录的 `design-specs/` 文件夹中：

```
design-specs/
├── foundation/          # 基础规范：颜色、字体、间距、阴影、图标、Token
│   ├── colors.md
│   ├── typography.md
│   ├── spacing-layout.md
│   ├── shadows-corners.md
│   ├── icons.md
│   └── tokens.md
├── components/          # 组件规范：基础、导航、数据录入、数据展示、反馈、业务
│   ├── basic.md
│   ├── navigation.md
│   ├── data-entry.md
│   ├── data-display.md
│   ├── feedback.md
│   └── business.md
├── pages/               # 典型页面：列表页、表单页、详情页、仪表盘页
│   ├── list-page.md
│   ├── form-page.md
│   ├── detail-page.md
│   └── dashboard-page.md
└── icons/               # SVG 图标资源
    ├── common/
    └── status/
```

## 调用策略

根据用户请求的具体内容，你必须按需读取对应的规范文档，**禁止一次性读取全部文件**。

| 开发需求 | 必须读取的文档 |
|----------|----------------|
| 任何颜色、Token 值查询 | `design-specs/foundation/tokens.md` |
| 配色方案、品牌色、状态色 | `design-specs/foundation/colors.md` |
| 字体、字号、行高 | `design-specs/foundation/typography.md` |
| 间距、布局、栅格、响应式 | `design-specs/foundation/spacing-layout.md` |
| 阴影、圆角 | `design-specs/foundation/shadows-corners.md` |
| 图标规格、查找图标路径 | `design-specs/foundation/icons.md` |
| 按钮、分割线等基础组件 | `design-specs/components/basic.md` |
| 导航菜单、面包屑、标签页、分页 | `design-specs/components/navigation.md` |
| 输入框、选择器、表单 | `design-specs/components/data-entry.md` |
| 表格、列表、卡片、标签 | `design-specs/components/data-display.md` |
| 弹窗、提示、加载、通知 | `design-specs/components/feedback.md` |
| 图表、筛选区、工具栏 | `design-specs/components/business.md` |
| 列表页整体设计与布局 | `design-specs/pages/list-page.md` |
| 表单页整体设计与布局 | `design-specs/pages/form-page.md` |
| 详情页整体设计与布局 | `design-specs/pages/detail-page.md` |
| 仪表盘页整体设计与布局 | `design-specs/pages/dashboard-page.md` |

## 代码生成约束

### 1. 色彩约束

- **品牌主色**：`#2A6CDD`，悬停态：`#1E5BBF`
- **功能色**：成功 `#52C41A`，警告 `#FAAD14`，错误 `#F5222D`
- **中性色序列**：
  - 页面背景：`#F7F8FA` (N1)
  - 卡片背景：`#FFFFFF`
  - 边框/分割线：`#F0F2F5` (N2)
  - 次要文字：`#939599` (N6)
  - 主要文字：`#313133` (N8)
  - 标题文字：`#13161B` (N9)
- **导航背景**：`#0C1D43`
- **禁止使用规范外的颜色值**

### 2. 字体约束

- **中文**：`Microsoft YaHei`, `PingFang SC`, sans-serif
- **英文/数字**：`SF Pro Display`, `DIN Alternate`, `-apple-system`, `Helvetica Neue`, Arial, sans-serif
- **正文默认**：`14px / 400 / 1.5em`
- **标题层级**：`20px / 24px / 32px / 48px / 64px / 96px`

### 3. 间距约束

- 采用 **8px 基准网格**，最小单位 4px
- 常用间距：`8px`, `12px`, `16px`, `20px`, `24px`
- 卡片内边距：`16px`（紧凑）/ `24px`（默认）
- 页面内容区内边距：`24px`

### 4. 阴影与圆角约束

- 按钮圆角：`2px`
- 卡片、输入框、弹窗圆角：`4px`
- 卡片阴影：`0 2px 8px rgba(0, 0, 0, 0.08)`
- 下拉面板阴影：`0 6px 16px rgba(0, 0, 0, 0.12)`
- 弹窗阴影：`0 12px 32px rgba(0, 0, 0, 0.14)`

### 5. 图标约束

- 常规图标尺寸：`16px`
- 导航图标：`24px`
- 优先使用项目自带 SVG 图标：`design-specs/icons/common/` 和 `design-specs/icons/status/`
- 图标与文字间距：`8px`

## 页面生成指南

### 列表页

若用户要求生成列表页，严格遵循 `pages/list-page.md` 的 12 层结构：

1. 顶部导航栏（56px，背景 `#0C1D43`）
2. 侧边栏导航（208px，可展开子菜单）
3. 多标签导航（40px，可选）
4. 页面标题区（20px / 600 / `#262626`）
5. 标签切换（可选，带徽标数）
6. 提示信息 Alert（可选，信息/警告类型）
7. 筛选区（卡片包裹，16px 内边距）
8. 工具栏（flex 两端对齐，背景 `#F7F8FA`，底部边框 `#F0F2F5`）
9. 数据表格（斑马纹，行内操作按钮组，表头 `#F7F8FA`）
10. 分页器（右下角，支持每页条数选择与快速跳转）
11. 底部操作栏（批量操作时 sticky 显示）

### 表单页

若用户要求生成表单页，严格遵循 `pages/form-page.md`：

- **单列布局**（字段 ≤6）/ **双列布局**（字段 >6）/ **分组布局**
- 标签宽度：`120px`，右对齐
- 必填项：标签前红色星号 `*`，颜色 `#F5222D`
- 表单项间距：`24px`
- 底部操作栏：左侧"保存草稿"（可选），右侧"取消（次要按钮）+ 提交（主要按钮）"

### 详情页

若用户要求生成详情页，严格遵循 `pages/detail-page.md`：

- 页头标题格式：业务对象名称 + 编号（如"合同详情 - HT20240001"）
- 信息展示区：2-3 列描述列表，重要状态用 Tag 高亮
- 流程/日志区：时间轴组件，最新节点置顶
- 关联数据区：表格或列表，支持分页

### 仪表盘页

若用户要求生成仪表盘页，严格遵循 `pages/dashboard-page.md`：

- 搜索区（输入框 + 搜索按钮，可选）
- 业务概览区块：左侧 4px 蓝色色条标题 + 筛选表单 + KPI 标签卡片
- 图表可视化区：2 列排列，卡片包裹，支持分段控制器切换维度
- 客户/数据概览区：维度切换标签 + 数据表格卡片（前五/后五 + "更多"链接）

## 交互规范

- **悬停状态**：表格行背景 `#F5F5F5`，按钮/链接颜色变为主色悬停态 `#1E5BBF`
- **聚焦状态**：输入框边框 `#2A6CDD`，外发光 `rgba(42, 108, 221, 0.1)`
- **禁用状态**：透明度 40% 或背景 `#F5F5F5`
- **过渡动画**：`200ms ease-in-out`（快速），`300ms ease-in-out`（常规）

## 输出要求

- 生成代码时必须使用上述规范中的颜色值、间距值、字体值，**不得自行编造**
- 组件类名建议采用 BEM 命名法（如 `.gf-button`, `.gf-card`, `.gf-table`）
- 优先使用语义化 HTML 标签和 ARIA 属性
- 图表优先使用 ECharts，遵循 `components/business.md` 中的图表规范
