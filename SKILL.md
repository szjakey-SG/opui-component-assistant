---
name: opui-component-assistant
description: "Query Oceanpayment UI (OPUI) component docs, search components, retrieve Props/demos, and build Vue 3 pages. Supports screenshot-to-code: analyze uploaded UI screenshots, map visual elements to OPUI components, generate static HTML preview for confirmation, then produce OPUI-compliant Vue code. Use when the user asks about OPUI components, uploads a design screenshot, wants to replicate a UI, or needs help building pages with oceanpayment-ui."
---

# OPUI Component Assistant

Helps you efficiently query and use the Oceanpayment UI component library (based on Ant Design Vue) via the OPUI-MCP server. Supports two workflows:

- **Query workflow**: Search components → get docs → build pages
- **Screenshot-to-Code workflow**: Upload screenshot → analyze UI → HTML preview → confirm → Vue code

## Prerequisites

The OPUI-MCP server must be connected. Available MCP tools:

| Tool | Internal Name |
|------|---------------|
| list-components | `mcp__OPUI-MCP__list-components` |
| search-components | `mcp__OPUI-MCP__search-components` |
| query-component | `mcp__OPUI-MCP__query-component` |
| get-component-props | `mcp__OPUI-MCP__get-component-props` |
| get-component-demo | `mcp__OPUI-MCP__get-component-demo` |
| get-info | `mcp__OPUI-MCP__get-info` |

Call via `qw_mcp_call` with the internal tool name. Always call `qw_mcp_get` first to confirm schema.

## Tool Reference

### 1. search-components — Find components by keyword

```json
{ "keyword": "表格" }
```
Supports Chinese/English keywords: "卡片", "select", "上传", "反馈", "chart", "form", etc.
Returns: matching component names, descriptions, and associated hooks.
**Use when**: user doesn't know the exact component name.

### 2. list-components — Browse all components by category

```json
{ "category": "数据展示", "offset": 0 }
```
Categories: `通用`, `布局`, `导航`, `数据展示`, `数据录入`, `反馈`, `其他`
Omit `category` to list all. Supports `offset` for pagination.
**Use when**: user wants to browse available components in a category.

### 3. query-component — Full documentation (recommended)

```json
{ "name": "OPTable", "offset": 0 }
```
Returns: docs + Props table + events + methods + FAQ + example code.
Component name accepts with or without `OP` prefix (e.g., `Table` = `OPTable`).
**Use when**: user needs comprehensive understanding of a component.

### 4. get-component-props — Props/API only (token-efficient)

```json
{ "name": "OPButton", "offset": 0 }
```
Returns: import statement + Props table + events + methods + FAQ only.
**Use when**: user already knows the component and just needs the API.

### 5. get-component-demo — Example code only (token-efficient)

```json
{ "name": "OPBasicForm", "offset": 0 }
```
Returns: complete Vue SFC example only.
**Use when**: user needs code reference for implementation.

### 6. get-info — Library metadata

```json
{}
```
Returns: version, component count (151 total), icon count (789), etc.

## Pagination

All tools returning long content support pagination:
- Response includes `truncated: true` and `nextOffset` value
- Pass `nextOffset` as `offset` parameter in subsequent call
- Repeat until `truncated` is `false`

## Core Workflow

### Step 1: Find the component

**User says**: "I need a date picker" / "有没有日期选择组件"
**Action**: `search-components` with `keyword: "日期"` or `"date"`
**If unsure of category**: `list-components` with relevant `category`

### Step 2: Get documentation

**User says**: "Show me how OPTable works" / "查一下 OPTable 文档"
**Action**: `query-component` with `name: "OPTable"`
**If only need API**: `get-component-props` with `name: "OPTable"`
**If only need examples**: `get-component-demo` with `name: "OPTable"`

### Step 3: Build the page

After gathering component info, generate Vue 3 code following these conventions:

```vue
<script setup>
import { ref, reactive, computed } from 'vue'
import {
  // Layout
  OPRow, OPCol, OPSpace, OPDivider,
  // Data Display
  OPCard, OPTable, OPStatistic, OPCharts, OPBadge, OPTag,
  // Data Entry
  OPBasicForm, OPSelect, OPInput, OPDatePicker,
  // Feedback
  OPButton, OPModal, OPMessage,
  // Icons (from @ant-design/icons-vue, re-exported by oceanpayment-ui)
  SearchOutlined, PlusOutlined, DollarOutlined,
} from 'oceanpayment-ui'
</script>
```

## Import Pattern

```javascript
// All components import from 'oceanpayment-ui'
import { OPTable, OPCard, OPButton } from 'oceanpayment-ui'

// Icons also from 'oceanpayment-ui' (789 icons from @ant-design/icons-vue)
import { SearchOutlined, PlusOutlined } from 'oceanpayment-ui'

// Hooks
import { useTable, useForm, useDescription, useModalSelect, useLoading } from 'oceanpayment-ui'
```

## Component Categories Quick Reference

| Category | Key Components | Typical Use |
|----------|---------------|-------------|
| **布局** | OPRow, OPCol, OPLayout, OPSpace | Grid layout, page structure |
| **数据展示** | OPTable, OPCard, OPStatistic, OPCharts, OPBadge, OPTabs | Lists, cards, charts, stats |
| **数据录入** | OPBasicForm, OPSelect, OPInput, OPDatePicker, OPUpload | Forms, inputs, file upload |
| **反馈** | OPModal, OPDrawer, OPMessage, OPNotification | Dialogs, toasts, drawers |
| **导航** | OPMenu, OPBreadcrumb, OPPagination | Menus, navigation |
| **通用** | OPButton, OPTypography, OPDropdown | Buttons, text, menus |

For full component list, see [component-reference.md](component-reference.md).

## Page Building Patterns

### Data List Page
Components: `OPBasicForm` (filter) + `OPTable` (with `useTable` hook) + `OPModal` (detail/edit)

### Form Page
Components: `OPBasicForm` (with `useForm` hook) + `OPCard` (section wrapper) + `OPButton` (submit/cancel)

### Dashboard
Components: `OPRow/OPCol` (grid) + `OPCard` + `OPStatistic` + `OPCharts` + `OPTable`

### Detail Page
Components: `OPCustomDescriptions` (with `useDescription`) + `OPCard` + `OPDivider` + `OPTabs`

## Token Efficiency Tips

1. **Prefer `get-component-props` over `query-component`** when you only need the API — saves ~60% tokens
2. **Use `search-components` first** to confirm the exact component name before querying full docs
3. **Use `get-component-demo` separately** when you know the API and just need code patterns
4. **Handle pagination proactively** — check `truncated` flag and fetch remaining content with `offset`
5. **Batch queries** — query multiple components in parallel when building a page with several components

## Custom Components vs Ant Design Vue

OPUI has 38 custom-wrapped components and 113 direct Ant Design Vue re-exports.

**Custom-wrapped** (enhanced with extra features):
`OPTable` (useTable), `OPBasicForm` (useForm), `OPCustomDescriptions` (useDescription), `OPModalSelect` (useModalSelect), `OPCharts`, `OPVirtualList`, `OPLayout`

**Direct re-exports**: Same API as Ant Design Vue, just prefixed with `OP`. E.g., `Button` → `OPButton`, `Select` → `OPSelect`.

When building pages, prefer custom-wrapped components with their companion hooks for the best OPUI experience.

---

## Screenshot-to-Code Workflow

When the user uploads a UI screenshot or design image and wants to recreate it using OPUI components, follow this 5-step workflow strictly:

### Step 1: Analyze the Screenshot

Read the uploaded image and identify all UI elements:

**Layout structure**:
- Overall page layout (single column, sidebar+content, header+content+footer)
- Grid patterns (how many columns, proportional widths)
- Spacing and grouping between sections

**Visual elements → OPUI component mapping**:

| Visual Pattern | OPUI Component | Notes |
|---------------|---------------|-------|
| Card with shadow/border | `OPCard` | Wrap content blocks |
| Key metrics with large numbers | `OPStatistic` | Inside OPCard |
| Bar/line/pie chart | `OPCharts` | ECharts-based |
| Data grid with headers | `OPTable` | Use `useTable` hook |
| Form fields (input, select, date) | `OPBasicForm` + `useForm` | Check component-reference.md |
| Navigation tabs | `OPTabs` + `OPTabPane` | |
| Status dots/labels | `OPBadge` | success/error/processing |
| Pill-shaped tags | `OPTag` | With color variants |
| Buttons (primary/outline/link) | `OPButton` | type="primary" / default |
| Dropdown menus | `OPDropdown` | |
| Breadcrumb trail | `OPBreadcrumb` | |
| Page numbers | `OPPagination` | |
| Modal/dialog overlay | `OPModal` | |
| Side drawer panel | `OPDrawer` | |
| Toast/notification popup | `OPMessage` / `OPNotification` | |
| Step indicators | `OPSteps` | |
| Timeline with dots | `OPTimeline` | |
| Key-value description list | `OPCustomDescriptions` | With `useDescription` |
| File upload area | `OPUpload` | |
| Search bar | `OPInput` / `OPInputSearch` | |
| Toggle switch | `OPSwitch` | |
| Slider control | `OPSlider` | |
| Tree/hierarchy | `OPTree` | |
| Empty state placeholder | `OPEmpty` | |
| Loading spinner | `OPSpin` | |
| Section dividers | `OPDivider` | |

**After mapping, output a component plan** to the user:

```
分析结果：
- 页面结构：顶部导航 + 内容区（左右布局）
- 顶部：OPLayout > OPBreadcrumb + 用户头像
- 左侧：3 张 OPCard + OPStatistic（统计卡片）
- 右侧：OPTable（数据表格）+ OPPagination
- 操作栏：OPSelect（筛选）+ OPButton（查询/导出）
```

### Step 2: Query Key Components via MCP

For components identified in Step 1 that you're unsure about:

1. Use `search-components` if the component name is unclear
2. Use `get-component-demo` for the most relevant components to get real code patterns
3. Use `get-component-props` when you need specific API details

**Prioritize querying**: custom-wrapped components (`OPTable`, `OPBasicForm`, `OPCharts`, `OPCustomDescriptions`) over simple re-exports.

### Step 3: Generate Static HTML Preview

Create a single-file `.html` page that visually replicates the screenshot using plain HTML/CSS/JS:

**Rules**:
- Single file: all CSS in `<style>`, all JS in `<script>`
- Use ECharts CDN for charts: `https://cdnjs.cloudflare.com/ajax/libs/echarts/5.5.0/echarts.min.js`
- Use Google Fonts or system fonts for typography
- Use CSS variables for the color palette
- Include realistic mock data (not lorem ipsum)
- Make it interactive: hover effects, clickable tabs, chart period switching
- Responsive: support desktop and tablet breakpoints

**HTML template structure**:
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <title>Page Preview</title>
  <!-- ECharts CDN if charts needed -->
  <!-- Google Fonts if needed -->
  <style>
    :root { /* color variables matching screenshot */ }
    /* layout + component styles matching screenshot */
  </style>
</head>
<body>
  <!-- Page structure matching screenshot -->
  <script>
    // ECharts init + mock data + interactions
  </script>
</body>
</html>
```

**Save to outputs folder** and provide a `file://` link for the user to preview.

### Step 4: Wait for User Confirmation

Present the preview and explicitly ask for confirmation:

```
预览已生成，请查看效果：
[查看预览](file://path/to/preview.html)

请确认布局和视觉风格是否满意，或提出需要调整的地方：
- 调整布局 / 间距
- 更换配色方案
- 增删模块
- 修改交互行为
```

**If user requests changes** → modify HTML preview → re-present.
**If user confirms** → proceed to Step 5.

**DO NOT skip this step. Always wait for explicit user confirmation before generating Vue code.**

### Step 5: Convert to OPUI Vue Code

Transform the confirmed HTML into a Vue 3 SFC using OPUI components:

**Conversion rules**:

1. **Layout**: HTML flexbox/grid → `OPRow` + `OPCol` with `:span` (24-grid) or `:flex`
2. **Cards**: `.card` divs → `OPCard` with `title`, `#extra` slots
3. **Tables**: `<table>` → `OPTable` with `columns` config + `useTable` hook
4. **Forms**: `<form>` → `OPBasicForm` with `useForm` hook
5. **Charts**: ECharts option objects → `OPCharts` with `:option` prop
6. **Buttons**: `.btn` → `OPButton` with `type="primary"` / `type="default"`
7. **Select**: `<select>` → `OPSelect` with `:options` + `v-model:value`
8. **Tags**: `.tag` → `OPTag` with `color` prop
9. **Badges**: `.badge` → `OPBadge` with `:status`
10. **Icons**: SVG inline → import from `'oceanpayment-ui'` (e.g., `SearchOutlined`)

**Vue SFC structure**:
```vue
<template>
  <!-- OPUI components replacing HTML equivalents -->
</template>

<script setup>
import { ref, reactive, computed } from 'vue'
import {
  // Only import components actually used in the page
  OPRow, OPCol, OPCard, OPTable, OPButton,
  SearchOutlined, PlusOutlined,
} from 'oceanpayment-ui'

// Mock data (replace with API calls in production)
// ECharts options (same config passed to OPCharts)
</script>

<style scoped>
/* Only custom styles OPUI components can't handle natively */
</style>
```

**Output both files**: the Vue SFC (`.vue`) and keep the HTML preview as reference.

### HTML → OPUI Tag Mapping (Quick Reference)

| HTML Element | OPUI Component |
|-------------|---------------|
| `<div class="card">` | `<OPCard>` |
| `<table>` | `<OPTable>` |
| `<form>` | `<OPBasicForm>` |
| `<input>` | `<OPInput>` |
| `<select>` | `<OPSelect>` |
| `<button>` | `<OPButton>` |
| `<div class="row">` | `<OPRow>` |
| `<div class="col-N">` | `<OPCol :span="N">` |
| `<span class="badge">` | `<OPBadge>` |
| `<span class="tag">` | `<OPTag>` |
| `<div class="stat">` | `<OPStatistic>` |
| `<div id="chart">` | `<OPCharts :option="...">` |
| `<nav class="tabs">` | `<OPTabs>` |
| `<nav class="breadcrumb">` | `<OPBreadcrumb>` |
| `<div class="pagination">` | `<OPPagination>` |
| `<div class="modal">` | `<OPModal>` |
| `<div class="drawer">` | `<OPDrawer>` |
| `<div class="steps">` | `<OPSteps>` |
| `<hr>` / divider | `<OPDivider>` |
| `<div class="empty">` | `<OPEmpty>` |
| `<div class="upload">` | `<OPUpload>` |
