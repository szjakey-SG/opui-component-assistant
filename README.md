# OPUI Component Assistant — 团队使用说明

## 这是什么

一个跨平台的 Agent Skill，让 AI 助手具备 Oceanpayment UI（`oceanpayment-ui` / 别名 `opopui`）组件库的专业知识。安装后，AI 在对话中会自动遵循 OPUI 的工程规范：优先使用 `OP*` 组件而非裸 ant-design-vue、输出标准的 Vue 3 + Vite 初始化模板、正确引入样式文件、按速查手册选择合适的组件。

核心价值：不再需要翻阅文档网站，对话即开发。

> 当前版本是**纯文档型 Skill**（无 MCP 依赖、无需联网），开箱即用。MCP 实时文档查询和截图转代码工作流见文末 [Roadmap](#roadmap)。

## 仓库结构

```
opui-component-assistant/
├── SKILL.md                    # Skill 主文件（约 60 行）
│   ├── 触发条件（frontmatter description）
│   ├── 工作流：识别需求 → 优先 OP* 组件 → 查 references → 输出规范代码
│   └── 默认初始化模板（main.ts 样式导入 + opGlobalConfig + message.config）
│
├── references/
│   └── components.md           # 组件速查手册（约 180 行）
│       ├── 安装方式（内部 GitLab 私有源 + legacy-peer-deps）
│       ├── Vite / Vue 3 接入模板
│       ├── 组件分组（基础展示 / 布局导航 / 表单录入 / 数据业务 / 反馈弹窗 / 增强组件）
│       ├── 主题定制与国际化（i18n）
│       └── 常见坑（Notes And Pitfalls）
│
├── component-reference.md      # 同 references/components.md（兼容 QoderWork 的扁平目录约定）
│
├── agents/
│   └── openai.yaml             # Codex / OpenAI Agent 元数据（其他平台可忽略）
│
├── oceanpayment-ui/            # 组件库入口源码快照（components.ts / types.ts 等，供检索参考）
│
└── oceanpayment-ui-skill-and-package-20260611.tar.gz
                                # Codex 一键安装包（.codex/skills + node_modules 组件库副本）
```

## 安装步骤

Skill 本体只需要两个文件：`SKILL.md` 和 `references/components.md`。按你使用的平台选择对应方式：

### QoderWork

将文件复制到技能目录（注意保留 `references/` 子目录）：

| 系统 | 路径 |
|------|------|
| Windows | `%USERPROFILE%\.qoderwork\skills\oceanpayment-ui\` |
| macOS | `~/.qoderwork/skills/oceanpayment-ui/` |

放置后无需重启，QoderWork 会自动识别。

### Claude（claude.ai / Claude Code）

- **claude.ai**：将 `SKILL.md` + `references/` 打包为 zip（顶层目录名 `oceanpayment-ui`），在 设置 → Capabilities → Skills 中上传。
- **Claude Code**：解压到 `~/.claude/skills/oceanpayment-ui/`（个人级）或项目内 `.claude/skills/oceanpayment-ui/`（项目级），无需重启。

### Codex

解压仓库内的 `oceanpayment-ui-skill-and-package-20260611.tar.gz` 到用户目录，Skill 会落在 `~/.codex/skills/oceanpayment-ui/`，同时附带组件库 `node_modules` 副本供本地检索。

> 注意：Skill 目录名统一为 `oceanpayment-ui`（与 SKILL.md frontmatter 中的 `name` 字段一致），全小写、连字符分隔。

## 使用方式

直接在对话中提问，以下场景会自动触发 Skill：

- 提到 OPUI、opopui、oceanpayment-ui 或 OP 开头的组件名
- 用 OPUI 搭建 Vue 3 页面
- 询问组件选型、用法、导入方式
- 询问项目接入、样式配置、主题、i18n

示例：

| 你说 | AI 做什么 |
|------|----------|
| "新项目怎么接入 OPUI" | 输出 main.ts 标准模板（含 less 样式导入与全局配置） |
| "做一个带搜索的列表页，该用什么组件" | 查 `references/components.md`，给出 OP* 组件选型与示例 |
| "OPUI 怎么改主题色" | 返回主题定制章节的配置方式 |
| "表格默认配置怎么统一设置" | 给出 `opGlobalConfig.tableConfig` 用法 |

AI 输出的代码遵循 OPUI 规范（`import { OPxxx } from 'oceanpayment-ui'`、按需导入、必需样式文件），可直接放入项目运行。

## 团队协作建议

**统一安装**：建议团队管理员将本仓库地址同步给所有成员，或在团队共享的项目模板中内置 `.claude/skills/` / `.qoderwork/skills/` 目录。

**持续更新**：如果 OPUI 组件库有重大更新（新增组件、API 变更），需要同步更新 `references/components.md`。可以让 AI 基于最新的 `oceanpayment-ui/components.ts` 导出列表重新生成。

## 常见问题

**Q: Skill 安装后没有自动触发？**
确认目录名为 `oceanpayment-ui`，且 `SKILL.md` 在该目录根部、`references/components.md` 路径完整。对话中显式提到 "OPUI" 或 "oceanpayment-ui" 可强制触发。

**Q: 组件库本身怎么安装到项目？**
见 `references/components.md` 的 Installation 章节：通过内部 GitLab 私有源安装（需要仓库访问凭证），peer 依赖冲突时配置 `legacy-peer-deps=true`。

**Q: 能否用于非 OPUI 项目？**
可以参考本仓库结构为其他组件库制作同类 Skill：替换 `references/components.md` 为目标组件库的速查手册即可。

## Roadmap

以下能力规划中，**当前版本尚未包含**：

- **OPUI-MCP 实时文档查询**：接入 `https://mcp.oceanpayment.com/mcp` MCP 服务器（Streamable HTTP），提供 `search-components` / `query-component` / `get-component-props` / `get-component-demo` / `list-components` 等工具，实时获取最新 Props 与示例。
- **截图转代码工作流**：上传 UI 设计稿 → 组件映射方案 → MCP 查询 Props → HTML 可交互预览 → 确认后生成 OPUI 规范的 Vue 3 SFC 的 5 步闭环。

如需上述能力，欢迎提 Issue 或 PR。
