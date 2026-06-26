# 广发中后台系统设计规范 — 导航组件

## 1. 侧边栏导航 (Sidebar)

### 整体结构
```html
<div class="gf-sidebar__menu">
  <div class="gf-sidebar__section">分组标题</div>
  <div class="gf-sidebar__item">
    <div class="gf-sidebar__item-content">
      <svg class="icon">...</svg>
      <span>菜单文字</span>
    </div>
    <svg class="gf-sidebar__item-arrow">...</svg>
  </div>
  <div class="gf-sidebar__submenu">
    <div class="gf-sidebar__submenu-item">子菜单</div>
  </div>
</div>
```

### 容器样式
- 宽度：208px（展开）/ 64px（折叠）
- 背景：#FFFFFF
- 边框：右侧 1px solid #E8E8E8 (N2)
- 位置：固定，顶部偏移 header-height
- 主菜单容器 `.gf-sidebar__menu`：`padding: 8px 0`

### 分组区块
- 类名：`.gf-sidebar__section`
- **用途**：仅在 `.gf-sidebar__submenu` 容器内使用，用于**二级内容分类标题**（如"睿享融通""私享会"）
- **不用于一级导航分组**：一级导航直接排列菜单项，不需要分组标题
- padding：`12px 16px 8px` (space-3 space-4 space-2)
- 文字：`color: #8C8C8C` (N5)，`font-size: 12px`
- `text-transform: uppercase`，`letter-spacing: 0.5px`
- 不需要箭头、不需要点击展开，仅作为视觉分类标识

### 一级菜单项
- 类名：`.gf-sidebar__item`
- 布局：`display: flex; align-items: center; justify-content: space-between; gap: 12px`
- 内边距：`padding: 12px 16px` (space-3 space-4)
- 外边距：`margin: 0 8px` (0 space-2)
- 圆角：`border-radius: 2px` (radius-sm)
- 字号：14px
- 默认文字色：#595959 (N6)
- 默认字重：500
- 过渡动画：`transition: all 0.2s`

### 一级菜单状态
| 状态 | 文字色 | 背景 | 字重 |
|------|--------|------|------|
| 默认 | #595959 | 透明 | 500 |
| 悬停 | #595959 | #E8E8E8 (N2) | 500 |
| 点击 | #595959 | #D9D9D9 (N3) | 500 |
| **选中** | **#2A6CDD** | **transparent** | **600** |

### 图标规范
- 图标容器：`.icon`，`width: 18px; height: 18px; display: inline-flex; align-items: center; justify-content: center; color: currentColor; flex-shrink: 0`
- SVG 图标：`width: 100%; height: 100%`，`stroke-width: 2`
- 箭头图标：`.gf-sidebar__item-arrow`，`width: 12px; height: 12px; flex-shrink: 0`，默认颜色 `#595959`
- 选中态箭头：`.gf-sidebar__item--active .gf-sidebar__item-arrow` → `color: #2A6CDD`
- 展开状态：`.gf-sidebar__item--expanded .gf-sidebar__item-arrow` → `transform: rotate(180deg)`
- 过渡动画：`transition: transform 300ms ease-in-out`

### 子菜单容器
- 类名：`.gf-sidebar__submenu`
- 背景：`rgba(247, 248, 250, 0.4)`（浅灰半透明）
- 外边距：`margin: 0 8px` (0 space-2)
- 圆角：`border-radius: 2px` (radius-sm)
- 默认状态：`max-height: 0; overflow: hidden`
- 展开状态：`.gf-sidebar__submenu--expanded` → `max-height: 500px`
- 过渡动画：`transition: max-height 300ms ease-in-out`

### 二级子菜单项
- 类名：`.gf-sidebar__submenu-item`
- 布局：`display: flex; align-items: center`
- 内边距：`padding: 8px 16px` (space-2 space-4)
- 外边距：`margin: 4px 8px` (space-1 space-2)
- 圆角：`border-radius: 2px` (radius-sm)
- 字号：13px
- 默认文字色：#595959 (N6)
- 默认字重：500
- 过渡动画：`transition: all 0.2s`

### 二级子菜单项状态
| 状态 | 文字色 | 背景 | 字重 |
|------|--------|------|------|
| 默认 | #595959 | 透明 | 500 |
| 悬停 | #595959 | rgba(247,248,250,0.6) | 500 |
| **选中** | **#2A6CDD** | **#EAF0FC** | **600** |

### 嵌套子菜单（二级分类）
当子菜单内包含多个功能模块时，使用 `gf-sidebar__section` 作为**二级分类标题**（如"睿享融通""私享会"），与一级分组标题共用同一样式：
- 类名：`.gf-sidebar__section`
- 样式：复用一级分组区块样式（`padding: 12px 16px 8px; color: #8C8C8C; font-size: 12px; text-transform: uppercase; letter-spacing: 0.5px`）
- 用途：在 `.gf-sidebar__submenu` 容器内对子菜单项进行内容分类
- 不需要箭头、不需要点击展开，仅作为视觉分类标识

### 正确的嵌套结构示例
```
gf-sidebar__menu
├── gf-sidebar__item "营销专区"         ← 一级菜单（直接排列，无分组标题）
│   └── gf-sidebar__submenu            ← 子菜单容器
│       ├── gf-sidebar__section "睿享融通"   ← 二级分类
│       │   ├── gf-sidebar__submenu-item    ← 页面项
│       │   └── gf-sidebar__submenu-item
│       └── gf-sidebar__section "私享会"     ← 二级分类
│           └── gf-sidebar__submenu-item
├── gf-sidebar__item "数据统计"         ← 一级菜单
└── gf-sidebar__item "系统管理"         ← 一级菜单
```

### 展开/收起箭头规范
- 类名：`gf-sidebar__item-arrow`
- 图标：ChevronDown (`<path d="M6 9l6 6 6-6"/>`)
- 容器尺寸：12px × 12px（直接设置，非容器+内部SVG结构）
- 默认颜色：#595959 (N6)
- 选中颜色：#2A6CDD (Primary)
- 展开旋转：`transform: rotate(180deg)`
- 过渡动画：transform 300ms ease-in-out

## 2. 面包屑 (Breadcrumb)

- 分隔符：/
- 链接颜色：#2A6CDD
- 当前页面：#13161B

## 3. 步骤条 (Steps)

- 圆形序号：32px 直径
- 已完成：广发蓝背景 + 白色数字
- 进行中：广发蓝背景 + 白色数字
- 未完成：灰色背景 + 灰色数字
- 连接线：1px 实线

## 4. 页头 (PageHeader)

- 返回按钮：左侧箭头
- 面包屑：页面顶部
- 标题：20px / 500
- 描述：14px / #999
- 操作按钮：右侧对齐

## 5. 顶部导航 (Top Header)

系统级顶部导航栏，位于页面最顶部。

### 布局规范

- 高度：64px
- 背景：#0C1D43 (Nav)
- 阴影：0px 4px 12px rgba(0, 0, 0, 0.12)
- 位置：fixed，顶部
- 内边距：0 24px
- 结构：左侧（Logo + 主导航）/ 右侧（操作图标 + 用户信息）

### 导航项规范

- 内边距：8px 16px
- 默认文字色：rgba(255, 255, 255, 0.85)
- 悬停背景：rgba(255, 255, 255, 0.1)
- 选中背景：rgba(255, 255, 255, 0.2)
- 选中字重：600
- 圆角：2px

### 右侧操作区

- 图标按钮尺寸：36px × 36px
- 图标颜色：rgba(255, 255, 255, 0.85)
- 头像尺寸：28px 圆形
- 用户名：14px，白色

## 6. 多标签导航 (MultiTab)

### 容器样式
- 高度：40px，背景 #FFFFFF
- 底部边框：`border-bottom: 1px solid #E8E8E8`（统一分割线）
- 对齐方式：`align-items: flex-end`（标签底部对齐容器底部，确保与分割线完全贴合）
- 标签项间距：`gap: 4px`（需定义 `--space-1: 4px`）

### 标签项样式
- 内边距：`7px 16px 8px`（上方边框距离文字少1px，整体下移1px）
- 字号：13px，字重 500
- 最大宽度：160px（过长显示省略号）
- 所有标签统一 `margin-bottom: -1px`（向上偏移 1px，使标签底部边缘与分割线完全贴合）
- 标签项之间不使用分隔线，通过 `gap` 自然间隔

### 标签项状态
| 状态 | 背景 | 文字色 | 字重 | border-bottom |
|------|------|--------|------|---------------|
| 非激活 | #F5F5F5 | #595959 | 500 | `1px solid transparent`（透明占位，与激活态高度一致） |
| 激活 | #FFFFFF | #2A6CDD | 600 | `1px solid #FFFFFF`（白色边框覆盖容器灰色分割线，实现与内容区无缝融合） |

### 边框融合设计（关键）
1. 容器底部有 `border-bottom: 1px solid #E8E8E8` 作为统一分割线
2. 非激活标签：`border-bottom: 1px solid transparent`（透明占位边框，与激活态高度完全一致）
3. 激活标签：`border-bottom: 1px solid #FFFFFF`（白色边框遮挡容器灰色边框，实现无缝融合）
4. 所有标签统一 `margin-bottom: -1px`（向上偏移 1px，使标签底部边缘与分割线完全贴合）
5. 结果：激活/非激活标签高度完全一致、下方无任何间隙、与分割线完全贴合

### 过渡动画
- 仅过渡 `color` 和 `background`
- **禁止 `transition: all`**（会导致 `margin-bottom`/`border` 属性变化产生动画，造成切换时标签跳动或闪线）

### 关闭按钮
- 尺寸：14px × 14px，圆形（`border-radius: 50%`），`margin-left: 4px`
- hover 背景：#E8E8E8
- 图标：X 图标 `<path d="M6 6l12 12M6 18L18 6"/>`
- SVG 尺寸：`width="10" height="10"`，`stroke-width="3"`，`viewBox="0 0 24 24"`
- **每个标签项都必须有关闭按钮**（包括默认首页标签）

### 标签激活逻辑（关键）
- 点击侧边栏菜单项时，**必须先创建/注册标签 DOM 元素，再调用 `activateTab`**，否则新标签的激活状态无法正确设置
- 标签页切换时同步更新 `tabs` Map 中的 `active` 标记和 DOM 中的 `gf-multitab__item--active` 类

### 新建标签按钮（可选）
- 仅在需要用户手动新建标签页的场景使用
- 尺寸：28px × 28px，边框 1px solid #E8E8E8
- 如果标签页由系统根据导航自动创建，**不显示新建标签按钮**

## 7. 标签页 (Tabs)

| 尺寸 | 高度 | 内边距 | 字号 |
|------|------|--------|------|
| 大 | 48px | 12px 24px | 16px |
| 中 | 40px | 10px 20px | 14px |
| 小 | 32px | 8px 16px | 13px |

## 8. 锚点 (Anchor)

- 容器：160px 宽度
- 左侧边框：2px
- 当前项：左侧 2px 蓝色边框 + 蓝色文字

## 9. 回到顶部 (BackTop)

- 按钮尺寸：40px × 40px
- 圆形按钮
- 阴影：0 2px 8px rgba(0,0,0,0.15)
- 位置：右下角 24px

## 10. 分页器 (Pagination)

- 类型：常规 / 简约 / 迷你
- 尺寸：大 / 小
- 功能：页码导航、上一页/下一页、首页/末页、快速跳转、每页条数选择
- 样式：无边框或细边框（1px solid #E8E8E8）
- 与内容区上下间距：`padding: 16px 0`（上下各 16px）
