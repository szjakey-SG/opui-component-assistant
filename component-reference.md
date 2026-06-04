# OPUI Component Reference

Complete component catalog for Oceanpayment UI (151 components + 789 icons).

> **Note**: This reference was compiled from OPUI-MCP v1.0.8. For the latest list, use `list-components` tool.

## 布局 (Layout) — 10 components

| Component | Description | Custom |
|-----------|-------------|--------|
| OPCol | 列 (Column) | |
| OPDivider | 分割线 (Divider) | |
| OPGrid | 栅格 (Grid) | |
| OPLayout | 布局 (Layout) | |
| OPLayoutContent | 布局内容 (Layout Content) | |
| OPLayoutFooter | 布局底部 (Layout Footer) | |
| OPLayoutHeader | 布局头部 (Layout Header) | |
| OPLayoutSider | 布局侧边栏 (Layout Sider) | |
| OPRow | 行 (Row) | |
| OPSpace | 间距 (Space) | |

Import: `import { OPRow, OPCol, OPSpace, OPDivider } from 'oceanpayment-ui'`

## 数据展示 (Data Display) — 43 components

| Component | Description | Custom | Hook |
|-----------|-------------|--------|------|
| OPTable | 高级表格 (Advanced Table) | Yes | `useTable` |
| OPCustomDescriptions | 描述列表 (Descriptions) | Yes | `useDescription` |
| OPCharts | 图表 (Charts, ECharts-based) | Yes | |
| OPVirtualList | 虚拟列表 (Virtual List) | Yes | |
| OPAvatar | 头像 (Avatar) | | |
| OPAvatarGroup | 头像组 (Avatar Group) | | |
| OPBadge | 徽标数 (Badge) | | |
| OPBadgeRibbon | 缎带徽标 (Badge Ribbon) | | |
| OPCalendar | 日历 (Calendar) | | |
| OPCard | 卡片 (Card) | | |
| OPCardGrid | 卡片网格 (Card Grid) | | |
| OPCardMeta | 卡片元信息 (Card Meta) | | |
| OPCarousel | 走马灯 (Carousel) | | |
| OPCheckableTag | 可选标签 (Checkable Tag) | | |
| OPCollapse | 折叠面板 (Collapse) | | |
| OPCollapsePanel | 折叠面板项 (Collapse Panel) | | |
| OPComment | 评论 (Comment) | | |
| OPDescriptions | 描述列表 (Descriptions) | | |
| OPDescriptionsItem | 描述列表项 (Descriptions Item) | | |
| OPDirectoryTree | 目录树 (Directory Tree) | | |
| OPEmpty | 空状态 (Empty) | | |
| OPImage | 图片 (Image) | | |
| OPImagePreviewGroup | 图片预览组 (Image Preview Group) | | |
| OPList | 列表 (List) | | |
| OPListItem | 列表项 (List Item) | | |
| OPListItemMeta | 列表项元信息 (List Item Meta) | | |
| OPPopover | 气泡卡片 (Popover) | | |
| OPStatistic | 统计数值 (Statistic) | | |
| OPStatisticCountdown | 倒计时 (Statistic Countdown) | | |
| OPTabPane | 标签面板 (Tab Pane) | | |
| OPTableColumn | 表格列 (Table Column) | | |
| OPTableColumnGroup | 表格列组 (Table Column Group) | | |
| OPTableSummary | 表格汇总 (Table Summary) | | |
| OPTableSummaryCell | 表格汇总单元格 | | |
| OPTableSummaryRow | 表格汇总行 | | |
| OPTabs | 标签页 (Tabs) | | |
| OPTag | 标签 (Tag) | | |
| OPTimeline | 时间轴 (Timeline) | | |
| OPTimelineItem | 时间轴项 (Timeline Item) | | |
| OPTooltip | 文字提示 (Tooltip) | | |
| OPTree | 树形控件 (Tree) | | |
| OPTreeNode | 树节点 (Tree Node) | | |

Import: `import { OPTable, OPCard, OPStatistic, OPBadge } from 'oceanpayment-ui'`

## 通用 (General)

| Component | Description |
|-----------|-------------|
| OPButton | 按钮 (Button) |
| OPButtonGroup | 按钮组 (Button Group) |
| OPConfigProvider | 全局化配置 (Config Provider) |
| OPFloatButton | 悬浮按钮 (Float Button) |
| OPFloatButtonGroup | 悬浮按钮组 |
| OPIcon | 图标 (Icon) |
| OPTypography | 排版 (Typography) |
| OPTypographyLink | 排版链接 |
| OPTypographyParagraph | 排版段落 |
| OPTypographyText | 排版文本 |
| OPTypographyTitle | 排版标题 |

Import: `import { OPButton, OPTypography } from 'oceanpayment-ui'`

## 数据录入 (Data Entry)

| Component | Description | Custom | Hook |
|-----------|-------------|--------|------|
| OPBasicForm | 基础表单 | Yes | `useForm` |
| OPCascader | 级联选择 | | |
| OPCheckbox | 多选框 | | |
| OPCheckboxGroup | 多选框组 | | |
| OPColorPicker | 颜色选择器 | | |
| OPDatePicker | 日期选择 | | |
| OPForm | 表单 (Form) | | |
| OPFormItem | 表单项 (Form Item) | | |
| OPInput | 输入框 (Input) | | |
| OPInputGroup | 输入框组 | | |
| OPInputNumber | 数字输入框 | | |
| OPInputPassword | 密码输入框 | | |
| OPInputSearch | 搜索输入框 | | |
| OPMentions | 提及 | | |
| OPMentionSelect | 弹窗选择器 | Yes | `useModalSelect` |
| OPRadio | 单选框 | | |
| OPRadioGroup | 单选框组 | | |
| OPRate | 评分 | | |
| OPSelect | 选择器 (Select) | | |
| OPSlider | 滑动输入条 | | |
| OPSwitch | 开关 | | |
| OPTextarea | 文本域 | | |
| OPTimePicker | 时间选择 | | |
| OPTransfer | 穿梭框 | | |
| OPTreeSelect | 树选择 | | |
| OPUpload | 上传 (Upload) | | |

Import: `import { OPBasicForm, OPSelect, OPInput, OPDatePicker } from 'oceanpayment-ui'`

## 反馈 (Feedback)

| Component | Description |
|-----------|-------------|
| OPAlert | 警告提示 |
| OPDrawer | 抽屉 |
| OPMessage | 全局提示 |
| OPModal | 对话框 |
| OPNotification | 通知提醒框 |
| OPPopconfirm | 气泡确认框 |
| OPProgress | 进度条 |
| OPResult | 结果 |
| OPSkeleton | 骨架屏 |
| OPSkeletonAvatar | 骨架屏头像 |
| OPSkeletonButton | 骨架屏按钮 |
| OPSkeletonInput | 骨架屏输入框 |
| OPSpin | 加载中 |
| OPSpinNested | 嵌套加载 |
| OPWatermark | 水印 |

Import: `import { OPModal, OPDrawer, OPMessage, OPNotification } from 'oceanpayment-ui'`

## 导航 (Navigation)

| Component | Description |
|-----------|-------------|
| OPAnchor | 锚点 |
| OPAnchorLink | 锚点链接 |
| OPBreadcrumb | 面包屑 |
| OPBreadcrumbItem | 面包屑项 |
| OPBreadcrumbSeparator | 面包屑分隔 |
| OPDropdown | 下拉菜单 |
| OPMenu | 导航菜单 |
| OPMenuDivider | 菜单分割线 |
| OPMenuItem | 菜单项 |
| OPMenuItemGroup | 菜单项组 |
| OPPagination | 分页 |
| OPSteps | 步骤条 |
| OPStep | 步骤 |
| OPSubMenu | 子菜单 |

Import: `import { OPMenu, OPBreadcrumb, OPPagination, OPSteps } from 'oceanpayment-ui'`

## Hooks

| Hook | Component | Import |
|------|-----------|--------|
| `useTable` | OPTable | `import { useTable } from 'oceanpayment-ui'` |
| `useForm` | OPBasicForm | `import { useForm } from 'oceanpayment-ui'` |
| `useDescription` | OPCustomDescriptions | `import { useDescription } from 'oceanpayment-ui'` |
| `useModalSelect` | OPMentionSelect | `import { useModalSelect } from 'oceanpayment-ui'` |
| `useLoading` | Global | `import { useLoading, createLoading } from 'oceanpayment-ui'` |

## Icons

789 icons from `@ant-design/icons-vue`, re-exported by `oceanpayment-ui`:

- **Outlined** (线框风格): 421 icons — e.g., `SearchOutlined`, `PlusOutlined`
- **Filled** (实底风格): 218 icons — e.g., `HomeFilled`, `UserFilled`
- **TwoTone** (双色风格): 150 icons — e.g., `CheckCircleTwoTone`

```javascript
import { SearchOutlined, HomeFilled, CheckCircleTwoTone } from 'oceanpayment-ui'
```

Icon utilities: `createFromIconfontCN`, `getTwoToneColor`, `setTwoToneColor`

## Language Packs

```javascript
import { enUS, zhCN } from 'oceanpayment-ui'
```
