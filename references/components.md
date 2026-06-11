# OceanPayment UI Component Reference

## Package

- Package name: `oceanpayment-ui`
- Observed version: `1.0.0`
- Common alias from users: `opopui`
- Framework: Vue 3
- Base library: `ant-design-vue`
- Browser support: modern browsers; Vue 3 does not support IE11.
- Direct browser script import: not supported by the bundled docs.

## Installation

In internal projects, install from the configured Git repository and branch:

```json
{
    "dependencies": {
        "oceanpayment-ui": "git+https://<credential>@opgitlab.oceanpayment.com/oceanpayment-odp-vue/odp-components-ui.git#prod"
    }
}
```

Then run:

```bash
npm install
```

If peer dependency resolution fails, this project uses `.npmrc`:

```text
legacy-peer-deps=true
```

## Vite / Vue 3 Setup

```ts
import { createApp } from 'vue'
import Antd from 'ant-design-vue/es'
import { opGlobalConfig, message } from 'oceanpayment-ui'
import App from './App.vue'

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

createApp(App).use(Antd).mount('#app')
```

## Component Usage

```vue
<template>
    <OPCard title="订阅状态">
        <OPButton type="primary">刷新</OPButton>
        <OPTag color="green">正常</OPTag>
    </OPCard>
</template>

<script setup lang="ts">
import { OPButton, OPCard, OPTag } from 'oceanpayment-ui'
</script>
```

## Global Helpers

- `opGlobalConfig.tableConfig(...)`: configure table behavior, including list-setting visibility and optional save/load APIs.
- `opGlobalConfig.searchFormConfig(...)`: configure search form behavior, including search cache.
- `message`: notification/message helper from the component library.
- `notification`: notification helper from the component library.

## Component Groups

### Basic Display

`OPAlert`, `OPAvatar`, `OPAvatarGroup`, `OPBadge`, `OPBadgeRibbon`, `OPCalendar`, `OPCard`, `OPCardGrid`, `OPCardMeta`, `OPCarousel`, `OPCollapse`, `OPCollapsePanel`, `OPComment`, `OPDescriptions`, `OPDescriptionsItem`, `OPEmpty`, `OPImage`, `OPImagePreviewGroup`, `OPList`, `OPListItem`, `OPListItemMeta`, `OPPopover`, `OPProgress`, `OPResult`, `OPSkeleton`, `OPSkeletonAvatar`, `OPSkeletonButton`, `OPSkeletonImage`, `OPSkeletonInput`, `OPSkeletonTitle`, `OPSpin`, `OPStatistic`, `OPStatisticCountdown`, `OPTag`, `OPCheckableTag`, `OPTimeline`, `OPTimelineItem`, `OPTooltip`, `OPTypography`, `OPTypographyLink`, `OPTypographyParagraph`, `OPTypographyText`, `OPTypographyTitle`

### Layout And Navigation

`OPAffix`, `OPAnchor`, `OPAnchorLink`, `OPBackTop`, `OPBreadcrumb`, `OPBreadcrumbItem`, `OPBreadcrumbSeparator`, `OPDivider`, `OPDrawer`, `OPGrid`, `OPLayout`, `OPLayoutContent`, `OPLayoutFooter`, `OPLayoutHeader`, `OPLayoutSider`, `OPMenu`, `OPMenuDivider`, `OPMenuItem`, `OPMenuItemGroup`, `OPSubMenu`, `OPPageHeader`, `OPPagination`, `OPRow`, `OPCol`, `OPSpace`, `OPSteps`, `OPStep`, `OPTabs`, `OPTabPane`

### Form And Input

`OPButton`, `OPButtonGroup`, `OPForm`, `OPFormItem`, `OPFormItemRest`, `OPInput`, `OPTextarea`, `OPInputGroup`, `OPInputPassword`, `OPInputSearch`, `OPInputNumber`, `OPInputNumberPro`, `OPAutoComplete`, `OPAutoCompleteOptGroup`, `OPAutoCompleteOption`, `OPCheckbox`, `OPCheckboxGroup`, `OPRadio`, `OPRadioButton`, `OPRadioGroup`, `OPRate`, `OPSelectPlus`, `OPSelectPro`, `OPSelectOption`, `OPSelectOptGroup`, `OPSwitch`, `OPSlider`, `OPTreeSelect`, `OPTreeSelectNode`, `OPCascader`, `OPDatePicker`, `OPMonthPicker`, `OPQuarterPicker`, `OPWeekPicker`, `OPRangePicker`, `OPTimePicker`, `OPTimeRangePicker`, `OPCustomRangePicker`, `OPNaiveDatePicker`, `OPIntlTelInput`

### Data And Business Components

`OPTable`, `useTable`, `OPTableColumn`, `OPTableColumnGroup`, `OPTableSummary`, `OPTableSummaryCell`, `OPTableSummaryRow`, `OPBasicForm`, `useForm`, `OPSearchContainer`, `OPApiSelect`, `OPCharts`, `OPBasicMenu`, `OPBasicHeader`, `OPCustomDescriptions`, `useDescription`, `OPModalSelect`, `useModalSelect`, `OPLoading`, `useLoading`, `createLoading`

### Feedback, Modal, And Security

`OPCustomModal`, `Modal`, `OPPopconfirm`, `message`, `notification`, `OPMfaVerificationModal`, `OPEmailVerificationModal`, `OPSecurityVerificationModal`, `useSecurityVerificationModal`

### Other Enhanced Components

`IconPark`, `OPUpload`, `OPUploadDragger`, `OPEditor`, `OPWatermark`, `OPVirtualList`, `OPDropdown`, `OPDropdownButton`, `OPTour`, `OPFooterBar`, `OPCustomBreadcrumb`, `OPTransfer`, `OPTree`, `OPTreeNode`, `OPDirectoryTree`, `OPMentions`, `OPMentionsOption`, `OPConfigProvider`, `OPLocaleProvider`

## Theme

OceanPayment UI uses Less variables. In Vite, configure Less in `vite.config.ts`:

```ts
css: {
    preprocessorOptions: {
        less: {
            javascriptEnabled: true,
            modifyVars: {
                'primary-color': '#28A745',
                'link-color': '#28A745',
                'border-radius-base': '4px'
            }
        }
    }
}
```

Common variables:

- `primary-color`
- `link-color`
- `success-color`
- `warning-color`
- `error-color`
- `font-size-base`
- `border-radius-base`
- `border-color-base`
- `box-shadow-base`

If theme changes do not apply, check that Less styles are imported instead of CSS-only styles.

## Internationalization

Use `OPConfigProvider` or Ant Design Vue config provider with locale data. Time components also require the date library locale, such as `dayjs`.

```vue
<template>
    <OPConfigProvider :locale="locale">
        <App />
    </OPConfigProvider>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OPConfigProvider, zhCN } from 'oceanpayment-ui'
import dayjs from 'dayjs'
import 'dayjs/locale/zh-cn'

dayjs.locale('zh-cn')

const locale = ref(zhCN)
</script>
```

Available locales observed in docs:

- `enUS`
- `zhCN`

## Notes And Pitfalls

- The package is ESM-style and designed for build tools such as Vite or webpack.
- It depends on Vue 3, Ant Design Vue, Less, Day.js, and related ecosystem packages.
- Some exports are direct aliases from `ant-design-vue`; others are custom OceanPayment wrappers.
- Prefer custom wrappers such as `OPButton`, `OPInput`, `OPSelectPlus`, `OPTable`, `OPBasicForm`, `OPDropdown`, and `OPCascader` when available.
- Always check the target project's existing import style before changing conventions.
