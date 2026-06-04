## OPUI Component Assistant — 团队使用说明

### 这是什么

一个 QoderWork Agent Skill，让 AI 助手具备 Oceanpayment UI 组件库的专业知识。安装后，你可以在对话中直接用自然语言查询组件文档、按截图还原页面、生成符合 OPUI 规范的 Vue 3 代码。

核心价值：不再需要翻阅文档网站，对话即开发。

### 安装步骤

**第一步：放置 Skill 文件**

将 `opui-component-assistant` 文件夹（含 `SKILL.md` 和 `component-reference.md`）复制到你的 QoderWork 技能目录：

| 系统 | 路径 |
|------|------|
| Windows | `%USERPROFILE%\.qoderwork\skills\opui-component-assistant\` |
| macOS | `~/.qoderwork/skills/opui-component-assistant/` |

放置后无需重启，QoderWork 会自动识别。

**第二步：配置 OPUI-MCP 服务器**

Skill 的组件文档查询功能依赖 OPUI-MCP 服务器。打开 QoderWork 的 MCP 设置，添加一个新的 MCP 服务器：

| 配置项 | 值 |
|--------|-----|
| 名称 | OPUI-MCP |
| 端点 | `https://mcp.oceanpayment.com/mcp` |
| 协议版本 | MCP 2024-11-05 |
| 传输方式 | Streamable HTTP |

保存后等待连接成功，你会在工具列表中看到 `mcp__OPUI-MCP__*` 系列工具（共 6 个），说明配置完成。

如果暂时不配置 MCP，Skill 仍然可以工作 —— 截图分析、HTML 预览生成、页面搭建指导等功能不依赖 MCP。只是无法实时查询最新的组件 Props 和示例代码。

### 两种使用模式

#### 模式一：组件查询

直接在对话中提问，Skill 会自动触发：

| 你说 | AI 做什么 |
|------|----------|
| "有没有日期选择组件" | 调用 `search-components` 按关键词搜索 |
| "查一下 OPTable 的文档" | 调用 `query-component` 返回完整文档 + 示例 |
| "OPButton 有哪些 Props" | 调用 `get-component-props` 只返回 API 定义 |
| "给我一个 OPBasicForm 的示例" | 调用 `get-component-demo` 只返回代码 |
| "列出所有数据录入类组件" | 调用 `list-components` 按分类浏览 |

#### 模式二：截图转代码

上传一张 UI 设计稿截图，然后说"按这个设计用 OPUI 实现"。AI 会按照 5 步工作流执行：

1. **分析截图** — 识别页面结构，将每个 UI 元素映射到对应的 OPUI 组件，输出组件方案
2. **查询组件** — 对关键组件通过 MCP 获取真实的 Props 和示例代码
3. **生成 HTML 预览** — 用纯 HTML/CSS/JS 还原设计稿，生成可交互的单文件预览
4. **等待你确认** — 你可以反复提出修改意见（调间距、换配色、增删模块），直到满意
5. **生成 Vue 代码** — 确认后转换为 OPUI 规范的 Vue 3 SFC，输出 `.vue` 文件

### 触发关键词

以下场景会自动触发 Skill，无需手动指定：

- 提到 OPUI、oceanpayment-ui、OP 开头的组件名
- 上传 UI 截图并要求实现页面
- 询问组件用法、Props、示例代码
- 要求用 OPUI 搭建某种页面

### 文件结构

```
opui-component-assistant/
├── SKILL.md                  # 主文件（~370 行）
│   ├── MCP 工具参考（6 个工具的参数和用法）
│   ├── 核心工作流（搜索 → 查文档 → 写页面）
│   ├── 导入规范（组件、图标、Hooks 的标准 import）
│   ├── 页面搭建模式（列表页、表单页、Dashboard、详情页）
│   ├── 截图转代码工作流（5 步闭环 + 组件映射表）
│   └── Token 效率技巧
│
└── component-reference.md    # 组件速查手册（~195 行）
    ├── 布局（10 个）
    ├── 数据展示（43 个）
    ├── 通用（11 个）
    ├── 数据录入（26 个）
    ├── 反馈（15 个）
    ├── 导航（14 个）
    ├── Hooks（5 个）
    └── 图标（789 个）
```

### 团队协作建议

**统一 MCP 配置**：建议团队管理员在 QoderWork 团队设置中统一配置 OPUI-MCP 服务器，避免每个人单独配置。

**配合项目模板使用**：Skill 输出的 Vue 代码遵循 OPUI 规范（`import from 'oceanpayment-ui'`、`useTable`/`useForm` Hooks），可以直接放入项目中运行。

**持续更新**：如果 OPUI 组件库有重大更新（新增组件、API 变更），需要重新生成 `component-reference.md`。可以让我通过 MCP 的 `list-components` 工具拉取最新列表后更新。

### 常见问题

**Q: Skill 安装后没有自动触发？**
确认文件夹名称是 `opui-component-assistant`（全小写，连字符分隔），且 `SKILL.md` 在文件夹根目录下。

**Q: MCP 工具调用失败？**
检查 QoderWork 中 OPUI-MCP 的连接状态。如果显示断开，尝试在 MCP 设置中重新连接。部分公司网络可能需要配置代理。

**Q: 截图转代码的还原度不高？**
截图越清晰、UI 元素越规范，还原度越高。复杂页面建议分模块截图，逐块实现后拼装。

**Q: 能否用于非 OPUI 项目？**
可以。Skill 的核心方法论（截图分析 → HTML 预览 → 确认 → 代码）适用于任何组件库。只需替换 MCP 工具为对应组件库的文档源即可。
