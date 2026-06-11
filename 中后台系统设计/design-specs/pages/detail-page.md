# 广发中后台系统设计规范 — 典型页面：详情页

详情页用于展示单条业务记录的完整信息，通常由列表页或流程页跳转进入。

## 页面结构

标准详情页由以下区域自上而下组成：

1. 顶部导航栏（Top Header）
2. 侧边栏导航（Navigation Menu）
3. 面包屑（Breadcrumb）
4. 页头（PageHeader）
5. 信息展示区（Description / Card）
6. 流程/日志区（Timeline，可选）
7. 关联数据区（Table / List，可选）

## 布局规范

- 页面背景：#F7F8FA (N1)
- 内容区内边距：24px
- 信息卡片背景：#FFFFFF
- 信息卡片内边距：24px
- 信息卡片圆角：4px
- 卡片间距：16px

## 各区域规范

### 顶部导航栏

遵循 [顶部导航](../components/navigation.md#5-顶部导航-top-header) 组件规范。

### 侧边栏

遵循 [导航菜单](../components/navigation.md#1-导航菜单) 组件规范。

### 面包屑

遵循 [面包屑](../components/navigation.md#2-面包屑-breadcrumb) 组件规范。

### 页头

遵循 [页头](../components/navigation.md#4-页头-pageheader) 组件规范。

**详情页扩展规则：**
- 页头标题：业务对象名称 + 编号，如"合同详情 - HT20240001"
- 右侧操作区：编辑（主要按钮）、删除（危险按钮）、导出/打印（次要按钮）

### 信息展示区

#### 基础信息卡片

- 卡片标题：16px / 500 / #13161B
- 使用 [描述列表](../components/data-display.md#12-描述列表-description) 组件展示字段
- 字段排列：2列或3列网格
- 重要状态字段使用 [标签](../components/data-display.md#3-标签-tag) 高亮

#### 扩展信息卡片

- 金额类数据使用 [统计数值](../components/data-display.md#13-统计数值-statistic) 组件
- 长文本内容使用正文 14px 展示，行高 1.5em

### 流程/日志区

- 卡片标题：16px / 500
- 使用 [时间轴](../components/data-display.md#6-时间轴-timeline) 组件展示审批流程或操作日志
- 最新节点置顶

### 关联数据区

- 卡片标题：16px / 500
- 使用 [表格](../components/data-display.md#1-表格-table) 或 [列表](../components/data-display.md#2-列表-list) 展示关联记录
- 支持分页

## 交互规范

- 点击"编辑"进入表单页，携带当前数据
- 点击"删除"弹出确认框
- 标签页切换（如"基本信息"/"操作日志"/"关联记录"）使用 [标签页](../components/navigation.md#7-标签页-tabs) 组件
