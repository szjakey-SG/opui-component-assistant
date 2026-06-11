---
name: oceanpayment-ui
description: Use when the user asks about opopui, OceanPayment UI, or oceanpayment-ui components; when building Vue 3 pages with OceanPayment UI; or when explaining setup, imports, styles, theme, i18n, tables, forms, and component choices for this library.
---

# OceanPayment UI

Use this skill for `opopui`, `OceanPayment UI`, and `oceanpayment-ui` work in Vue 3 projects.

## Workflow

1. Identify whether the user needs setup guidance, component selection, implementation help, or troubleshooting.
2. Prefer OceanPayment UI exports over raw `ant-design-vue` components when an `OP*` component exists.
3. For component inventory, examples, setup snippets, theme, or i18n details, read `references/components.md`.
4. Use Vue 3 + Vite patterns by default unless the target project clearly uses Vue CLI or webpack.
5. Include required style imports when showing setup. Missing styles are a common failure mode.
6. If the target project already has local patterns, follow those imports and style conventions first.

## Default Setup Pattern

In `main.ts`, import Ant Design Vue, OceanPayment UI global helpers, and the OceanPayment UI style files:

```ts
import Antd from 'ant-design-vue/es'
import { opGlobalConfig, message } from 'oceanpayment-ui'

import 'ant-design-vue/dist/antd.less'
import 'oceanpayment-ui/src/assets/style/global.less'
import 'oceanpayment-ui/src/assets/style/variables.less'
import 'oceanpayment-ui/src/assets/style/opCommon.less'

opGlobalConfig.tableConfig({
    showListSetting: true
})

opGlobalConfig.searchFormConfig({
    openSearchCache: 1
})

message.config({
    duration: 2,
    maxCount: 1
})
```

In Vue components, import only what is used:

```vue
<script setup lang="ts">
import { OPButton, OPCard, OPTag } from 'oceanpayment-ui'
</script>
```

## Component Reference

Read `references/components.md` when the user asks:

- What components exist in opopui/oceanpayment-ui.
- How to use the library in another project.
- Which component to choose for a Vue 3 page.
- How to configure global styles, table/form defaults, theme, or i18n.
