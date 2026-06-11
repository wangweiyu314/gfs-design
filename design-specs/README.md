# Skill: 广发中后台系统设计规范

## 1. 项目概述

本项目采用分层拆分策略，将设计规范拆分为 18 个独立文档。你的任务是根据用户查询精准定位到**1 个最相关的子文档**并读取，实现 token 最小化消耗。

- **适用查询**：UI 设计规范、组件参数、页面布局、Token 值、图标路径
- **技术栈**：纯 Markdown + SVG 图标
- **核心原则**：专业、稳重、高效，基于 8px 基准网格

---

## 2. 目录结构

```
design-specs/
├── README.md                          ← 本索引文档（你正在阅读）
│
├── foundation/                        # 基础规范层 — 全局 Token 与底层规则
│   ├── overview.md                    # 设计原则、目标、Figma 8 大分区结构
│   ├── colors.md                      # 品牌色、功能色、中性色 N1-N9、背景色规则
│   ├── typography.md                  # 字体、字号、字重、行高
│   ├── spacing-layout.md              # 间距 Token、24 列栅格、响应式断点
│   ├── shadows-corners.md             # 三层阴影（各 3 方向）、2px/4px 圆角
│   ├── icons.md                       # 48 个通用图标 + 13 个状态图标清单及 SVG 路径
│   └── tokens.md                      # CSS 变量汇总表
│
├── components/                        # 组件规范层 — 按类型分类的 UI 组件
│   ├── basic.md                       # 按钮(7类型/3尺寸)、复制、语音输入、分割线
│   ├── navigation.md                  # 菜单、面包屑、步骤条、页头、标签页、分页器等
│   ├── data-entry.md                  # 输入框、选择器、单选复选、开关、日期、表单等
│   ├── data-display.md                # 表格、列表、标签、卡片、统计数值、骨架屏等
│   ├── feedback.md                    # 弹窗、抽屉、提示、加载、通知、进度条等
│   └── business.md                    # 图表可视化、筛选区、工具栏、底部操作栏等
│
├── pages/                             # 典型页面层 — 完整页面模板
│   ├── list-page.md                   # 列表页：12 层结构，含筛选/表格/分页/批量操作
│   ├── form-page.md                   # 表单页：单列/双列/分组布局、校验规则
│   ├── detail-page.md                 # 详情页：信息卡片、时间轴、关联数据
│   └── dashboard-page.md              # 仪表盘页：KPI 卡片、图表、数据表格卡片
│
└── icons/                             # 图标资源层 — SVG 文件
    ├── common/                        # 45 个通用图标
    └── status/                        # 13 个状态图标
```

---

## 3. 调用映射表（必读）

### 3.1 规则：根据用户查询关键词 → 直接调用对应文件

| 用户查询关键词/意图 | 你必须调用的文件 | 备选文件 |
|---------------------|------------------|----------|
| 设计原则、设计目标、Figma 文件结构 | `foundation/overview.md` | — |
| 任何颜色值、品牌色、功能色、中性色、背景色规则 | `foundation/colors.md` | `foundation/tokens.md` |
| 字体、字号、字重、行高 | `foundation/typography.md` | `foundation/tokens.md` |
| 间距、布局、栅格、响应式断点 | `foundation/spacing-layout.md` | `foundation/tokens.md` |
| 阴影、圆角 | `foundation/shadows-corners.md` | `foundation/tokens.md` |
| 图标规格、查找特定图标文件路径 | `foundation/icons.md` | `icons/` 目录 |
| 完整的 Token 变量表、开发对接 | `foundation/tokens.md` | — |
| 按钮、复制、语音输入、分割线 | `components/basic.md` | — |
| 导航菜单、面包屑、步骤条、页头、标签页、分页器 | `components/navigation.md` | — |
| 输入框、选择器、单选复选、开关、日期、表单 | `components/data-entry.md` | — |
| 表格、列表、标签、卡片、统计数值、骨架屏、时间轴 | `components/data-display.md` | — |
| 弹窗、抽屉、Tooltip、加载、通知、消息、进度条 | `components/feedback.md` | — |
| 图表规范、筛选区、工具栏、底部操作栏、操作按钮组 | `components/business.md` | — |
| 列表页、数据管理页、查询页面设计 | `pages/list-page.md` | `components/business.md` |
| 表单页、新增/编辑页面设计 | `pages/form-page.md` | `components/data-entry.md` |
| 详情页、信息展示页面设计 | `pages/detail-page.md` | `components/data-display.md` |
| 仪表盘页、首页、驾驶舱、数据可视化页面设计 | `pages/dashboard-page.md` | `components/business.md` |

### 3.2 调用约束

1. **单一文件原则**：每个查询只允许读取 **1 个**最相关的子文档。禁止连锁读取多个文件。
2. **页面优先于组件**：若用户询问"某页面怎么设计"，直接调用 `pages/` 下的对应文件，不要分散查询组件文件。
3. **Token 溯源优先**：若需查询基础 Token 值，优先调用 `foundation/tokens.md`（单文件汇总），而非分散读取 colors/typography/spacing 等多个文件。
4. **图标直达**：若用户明确询问某个图标文件位置，直接引用 `icons/common/xxx.svg` 或 `icons/status/xxx.svg`，无需读取 icons.md。

---

## 4. 层级依赖关系

```
foundation/          ← 底层依赖，被所有上层文档引用
    │
    ├── colors.md ←──────┐
    ├── typography.md     │
    ├── spacing-layout.md │
    ├── shadows-corners.md├─→ components/ 所有组件文档
    ├── icons.md          │   └── pages/ 所有页面文档
    └── tokens.md ────────┘

components/          ← 中层依赖，被 pages/ 文档引用
    │
    ├── basic.md
    ├── navigation.md ──→ list-page.md / form-page.md / detail-page.md / dashboard-page.md
    ├── data-entry.md ──→ form-page.md / list-page.md
    ├── data-display.md ─→ list-page.md / detail-page.md / dashboard-page.md
    ├── feedback.md
    └── business.md ────→ list-page.md / dashboard-page.md

pages/               ← 顶层聚合，直接面向页面设计场景
    │
    ├── list-page.md     → 引用 navigation.md / data-entry.md / data-display.md / business.md
    ├── form-page.md     → 引用 navigation.md / data-entry.md
    ├── detail-page.md   → 引用 navigation.md / data-display.md
    └── dashboard-page.md → 引用 navigation.md / data-display.md / business.md

icons/               ← 独立资源层
    ├── common/        → 被 icons.md 索引
    └── status/        → 被 icons.md 索引
```

---

## 5. 文件内容摘要

为辅助你快速判断调用目标，以下是各文件的内容摘要：

### foundation/

- **`overview.md`** — 4 条设计原则、3 个设计目标、Figma 文件 8 大分区结构表
- **`colors.md`** — 品牌主色 #2A6CDD、红/橙 7 级序列、中性色 N1-N9、功能色、数据可视化色、背景色规则、导航色
- **`typography.md`** — 中/英/数字字体族、H1-H6 标题规格（96px~20px）、正文 3 级（16/14/12px）、5 级字重、4 种行高
- **`spacing-layout.md`** — space-0~16（0~64px，步长 4/8px）、24 列栅格、6 档响应式断点
- **`shadows-corners.md`** — Low/Medium/High 三层阴影（各含下/左/右 3 方向）、2px（按钮）/ 4px（卡片输入框）圆角
- **`icons.md`** — 5 级图标尺寸（12/16/20/24/32px）、48 个通用图标 + 13 个状态图标名称及 SVG 相对路径
- **`tokens.md`** — CSS 变量汇总：颜色 11 个、间距 11 个、圆角 2 个、阴影 3 个、字体 10 个、行高 3 个、过渡 3 个、布局 6 个

### components/

- **`basic.md`** — 按钮 7 类型（主要/次要/描边/虚框/链接/危险/危险-边框）× 3 尺寸（40/32/24px）、复制、语音输入、分割线
- **`navigation.md`** — 导航菜单（一级/二级 5 状态色值）、面包屑、步骤条、页头、顶部导航（64px/#0C1D43）、多标签导航（40px）、标签页（大/中/小）、锚点、回到顶部、分页器
- **`data-entry.md`** — 输入框（大/中/小）、选择器、单选/复选/开关（大/中/小）、日期/时间选择器、数字输入框、滑块、上传、级联选择、标签输入、表单（标签宽 120px）
- **`data-display.md`** — 表格（行高 48/40/32）、列表、标签（5 类型色值）、树、分段控制器、时间轴、折叠面板、头像、空状态、徽标数、卡片、描述列表、统计数值、图片预览、水印、二维码、代码展示、穿梭框、评分、骨架屏
- **`feedback.md`** — 弹窗（480/640/800px）、抽屉（480/640px）、Tooltip、加载（全局/局部/按钮）、通知（右上/4.5s）、消息（4 类型）、警告提示、进度条、气泡确认框、结果页
- **`business.md`** — 图表规范（标题/说明/轴网格/图例/环图中心/柱形/折线/双轴）、筛选区（flex/gap16/标签13px）、工具栏（flex/两端/背景#F7F8FA）、底部操作栏（sticky/底部）、操作按钮组（表格行内/透明背景/12px）

### pages/

- **`list-page.md`** — 12 层页面结构。新增：多标签导航、标签切换（徽标数）、提示信息（Alert）、筛选区卡片包裹、表格斑马纹+复选框、分页快速跳转、底部操作栏业务按钮配置
- **`form-page.md`** — 6 层页面结构。单列（≤6 字段）/ 双列（>6 字段）/ 分组布局、字段排列顺序（基础→业务→关联→扩展）、必填红色星号、实时+提交校验、底部取消+提交按钮
- **`detail-page.md`** — 7 层页面结构。页头标题格式（对象+编号）、信息卡片（2-3 列描述列表+标签高亮）、扩展金额统计数值、流程时间轴（最新置顶）、关联数据表格+分页
- **`dashboard-page.md`** — 6 层页面结构。搜索区（输入+按钮）、业务概览区块标题（4px 蓝色色条）、筛选表单（时间+下拉+查询/重置）、KPI 标签卡片（激活/非激活态）、图表区（折柱混合/环形/柱形/组合）、客户维度切换标签、数据表格卡片（前五/后五+更多链接）

---

## 6. 维护规则

- **新增组件**：在 `components/` 下选择最接近的分类追加；若新增分类则新建文件并更新本索引第 3、5 节
- **新增页面**：在 `pages/` 下新建文件，基于现有组件组合推断补全，并更新本索引第 3、5 节
- **修改 Token**：优先修改 `foundation/tokens.md`，同步检查 `colors.md` / `typography.md`
- **新增图标**：SVG 放入 `icons/common/` 或 `icons/status/`，在 `icons.md` 添加路径，无需修改本索引

---

*Skill 版本：v1.0*
*更新日期：2026-06-05*
