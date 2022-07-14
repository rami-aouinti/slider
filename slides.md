---
theme: default
layout: cover
background: /cover.jpg 
# https://sli.dev/custom/highlighters.html
highlighter: shiki
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Vitify Admin
  Presentation for Vitify Admin and new features in Online Monitor.
# persist drawings in exports and build
drawings:
  persist: false
---

# Welcome to Vitify Admin

Presentation for Vitify Admin and new features in Online Monitor

<div class="uppercase text-sm tracking-widest">
Yue JIN
</div>

<div class="abs-bl mx-12 my-12 flex">
  <img src="/logo-dark.png" class="h-11">
</div>

---

# 啥是 Vitify Admin?

Vitify 是用于快速创建web后台应用的起始模板。Vite + Vuetify = Vitify

- ⚡️ **Vite 3, pnpm, ESBuild** - 快得一逼
- 🗂️ **Pages** - 基于文件的路由
- 📑 **布局系统** - 零配置布局
- 🦾 **TypeScript** - 支持 Vuetify2 模板 intelisense, Powerer by Volar
- 🔥 **`<script setup>`** - 使用 Vue3 语法
- 🍍 **状态管理** - Pinia
- 🧪 **测试** - Vitest 单元/组件测试 + Cypress E2E 测试
- 🌍 **I18n** - 国际化开箱即用
- 📦 **自动import** - 组件自动化加载，API自动导入
- 😃 **Icons** - SVG图标自动注册
- 📉 **数据可视化** - Vue-Echarts

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: image-right
image: https://d33wubrfki0l68.cloudfront.net/b4b145110098a2c031d3ba49551c504aef62b321/b38fa/img/benchmarks/alotta-files.svg
---

# pnpm

- 安装速度大幅提升
- 大量减少磁盘占用空间
- patch package: 允许直接修改`node_modules`中的文件
- Vue团队的所有项目及多数社区知名项目已经迁移到了pnpm
- `pnpm prune`

---

# Vite

- 更快的冷启动
- 超快的热重载
- 通过环境变量更改后端api地址，不再需要请求`config.json`

<img src="/vite-restart.jpg" class="rounded-md mt-2">

---

# `vite-plugin-pages`

<div class="grid grid-cols-2 gap-x-4 mt-4">
<div>

- 基于文件系统生成路由
- 静态路由，支持debug
- 配合`vite-plugin-vue-layouts`自动在路由设置中添加layout组件

<div v-click class="mt-3">

```
src/pages/
  ├── users/
  │  ├── [id].vue
  │  └── index.vue
  └── users.vue
```

</div>
</div>
<v-click>
```ts
[
  {
    path: "/users",
    component: "/src/pages/users.vue",
    children: [
      {
        path: "",
        component: "/src/pages/users/index.vue",
        name: "users"
      },
      {
        path: ":id",
        component: "/src/pages/users/[id].vue",
        name: "users-id"
      }
    ]
  }
]
```
</v-click>

</div>

---

# Auto Import

不用再写一大堆`import`啦

- `unplugin-vue-components` 取代 `vuetify-loader` 自动导入 Vuetify 组件
- `unplugin-auto-import` 自动`import` API

<div v-click class="grid grid-cols-2 gap-x-4 mt-4">

## without

## with

```ts
import { computed, ref } from 'vue'
const count = ref(0)
const doubled = computed(() => count.value * 2)

```

```ts
const count = ref(0)
const doubled = computed(() => count.value * 2)

```

</div>

---

# TypeScript Project Reference

- 为不同环境提供正确的类型(app vs test)
- VSCode中获得正确的intellisense
- 防止意外引入不必要的源文件

<v-click>
<img src="/volar-status-bar-1.jpg">
<img src="/volar-status-bar-2.jpg">
</v-click>

---

# Volar

<v-clicks>

- 模板TypeScript检查
- `.vue`单组件文件类型
- 单组件窗格分离
- 通过[`@volar-plugins/vetur`](https://github.com/johnsoncodehk/volar-plugins/tree/master/packages/vetur)获得`vetur`的功能，迁移旧项目及js项目
- 项目已内置 Vuetify 2 type支持
</v-clicks>

<img v-click src="/volar-vuetify-1.jpg" class="h-25">
<img v-click src="/volar-vuetify-2.jpg" class="h-25">

---

# 🍍Pinia

<v-clicks>

- 支持 options api 和 composition api
- 不再需要写`mutation`
- 配合`vue devtools` debug 全局状态

</v-clicks>

<!-- 数据结构一目了然；直接测试响应性和动画；message直接新建，不用再window里暴露一个测试函数 -->

---

# 自动导入注册svg icons

把svg格式的图标放在相应文件夹下，即可在`<v-icon>`中使用

- `import.meta.glob`一次性导入所有svg
- `vite-plugin-vue2-svg`将导入的svg编译成vue component
- 根据文件名在`vuetify`中注册同名图标

```ts
const svgIcons = Object.fromEntries(
  Object.entries(import.meta.globEager('@/assets/icons/*.svg')).map(
    ([k, v]) => [
      k
        .split(/(\\|\/)/g)
        .pop()!
        .replace(/\.[^/.]+$/, ''),
      { component: v.default },
    ]
  )
)
new Vuetify({icon:{values:{...svgIcons}}})
```

---
layout: section
---

# 使用 Vue3 的新特性

更简洁的代码，更好的 ECMAScript 和 TypeScript 支持

---

<div class="grid grid-cols-2 gap-x-4"><div>

# Before

```vue {all|3-6,11-16|all}
<script lang="ts">
import { reactive, defineComponent } from 'vue'
import BtnCount from './BtnCount.vue'
export default defineComponent({
  components: { BtnCount },
  setup() {
    const state = reactive({ count: 0 })
    function increment() {
      state.count++
    }
    return {
      state,
      increment
    }
  }
})
</script>
<template>
  <BtnCount @click="increment">
    {{ state.count }}
  </BtnCount>
</template>
```
</div>
<div v-after>

# With `<setup script>`

```vue {2-6}
<script setup lang="ts">
import BtnCount from './BtnCount.vue'
const state = reactive({ count: 0 })
function increment() {
  state.count++
}
</script>
<template>
  <BtnCount @click="increment">
    {{ state.count }}
  </BtnCount>
</template>
```

</div>
</div>

<!-- 建议script写在template前面 -->
---

<div class="grid grid-cols-2 gap-x-4">
<div>

# Before

```ts {all|5,10,14|all}
import type { PropType } from 'vue'
export default defineComponent({
  props: {
    dataset: {
      type: Array as PropType<number[][]>,
      required: false,
      default: () => [],
    },
    sym: {
      type: Boolean,
      default: false,
    },
    valueFormatter: {
      type: Function as PropType<(val: number) => string>,
      required: false,
      default: (val: number) => val.toFixed(3),
    },
  }
})
```
</div>
<div v-after>

# With `<setup script>`

```ts {2-6}
const props = withDefaults(
  defineProps<{
    dataset?: number[][]
    sym?: boolean
    valueFormatter?: (val: number) => string
  }>(),
  {
    dataset: () => [],
    sym: false,
    valueFormatter: (val: number) => val.toFixed(3),
  }
)
```

</div>
</div>

---

# 在模板里写ES6

<div class="grid grid-cols-2 gap-x-4">
<div>

## Before

```vue-html
<template>
  <span> {{ power && power.toFixed(1) }} </span>
</template>
```

</div>
<div v-after>

## vue-template-babel-compiler

```vue-html
<template>
  <span> {{ power?.toFixed(1) }} </span>
</template>
```

</div>
</div>

---
layout: two-cols
---

# Portal-Vue
在 Vue2 中使用 Vue3 内置的`<Teleport>`

- 避免同页面组件间的数据交换
  - header
  - footer
- 避免`z-index`地狱
  - dialog
  - notification

::right::

<Portal class="h-1/2 mt-24"/>

---

# Vue-Echarts

Apache ECharts component for Vue.js

<div class="grid grid-cols-2 gap-x-4">

<v-clicks :every='2'>

- Auto resize

```vue-html
<v-chart autoresize />
```

- Provide/Inject

```ts
const vuetify = useVuetify()
const { locale } = useI18n()
provide(
  THEME_KEY,
  computed(() => (vuetify?.theme.dark ? 'dark' : undefined))
)
provide(
  INIT_OPTIONS_KEY,
  computed(() => ({ locale: locale.value.toUpperCase() }))
)
```

- `echarts.on` ➡️ Component Event listener

```vue-html
<v-chart
  @mousemove="onMousemove"
  @mouseout="onMouseout"
  @selectchanged="onSelectChanged"
/>
```

</v-clicks>

</div>

<!-- 比如用热力图写的组件分布图，代码量更少了，问题更少了，功能更多了 -->

---
layout: section
---

# Testing

## —— 应测尽测，每天一次大筛

---
layout: two-cols
---

# Vitest

- 与 Vite 共享设置
- 快如闪电的 watch mode
- Jest expect compatible APIs

::right::

<logos-vitest class="text-8xl ml-48"/>

<!-- 不再需要vue-jest等额外的设置和编译 -->

---

# Testing Library

---

# Cypress(WIP)

E2E测试，模拟真实的生产环境

---

# I18n

`vue-i18n v8` + `vue-i18n-bridge` + `unplugin-vue-i18n` + `i18n-Ally`
- Messages 预编译
- SFC Custom block

<div v-click class="grid grid-cols-2 gap-x-4 mt-4">

```json
// zh.json
{
  "viewLevel": {
    "private": "自己",
    "group": "组内",
    "public": "公开",
    "disabledInfo": "不能改变该对象可见级别，请确认你具有权限。"
  }
}
```

```vue
<!-- ViewLevel.vue -->
<i18n lang="json" locale="zh">
{
  "private": "自己",
  "group": "组内",
  "public": "公开",
  "disabledInfo": "不能改变该对象可见级别，请确认你具有权限。"
}
</i18n>
```

</div>

<!-- 全网第一个实现这个组合，经历了i18n-composable到bridge, vite-plugin到unplugin -->
<!-- i18n-Ally 可以inline显示翻译结果，快速提取及添加翻译，提示翻译完成度... -->

---

# Why not Vue 2.7?

<div v-click-hide>

- 还不够稳定
  - 和 Pinia 一起使用会报错
- 社区还没跟上
  - vue-i18n-bridge 不支持 Vue 2.7
  - vue-test-util 不能正常更新dom

</div>

<div v-after v-motion :enter="{ y: -140 }">

- ~~还不够稳定~~
- ~~社区还没跟上~~

Coming Soon!

</div>

<div v-click v-motion :enter="{ y: -100 }">

## 优点

- 很多依赖已不再需要
- 未来一年多官方会持续维护 2.7
- 更严格的 type 检查
- css-bind 等新功能，sfc语法、API与 [Vue3](https://vuejs.org/) [几乎完全相同](https://blog.vuejs.org/posts/vue-2-7-naruto.html)

</div>

---

# 建议
- Do one thing, and do it well
- 思考更优的交互体验
- 注意数组的性能

<v-click>

```diff
const weightedDist = computed(() => {
+ const mesh = burnupMesh.value!
  return dist.value
    ? dist.value.map((layer, j) =>
-       layer.map((val, i) => (val * burnupMesh.value[j][i]) / activeHeight.value!)
+       layer.map((val, i) => (val * mesh[j][i]) / activeHeight.value!)
      )
    : undefined
})
```

</v-click>

<!-- 主题保存在本地，开关放在了状态栏上等等提升用户体验的细节改动 -->

---

# 命名
- physical experiment ➡ physics test
- tripleAO ➡ AO3
- ladder ➡ trapezoid
- ...

<img v-click src="/trapezoid.jpg" class="h-1/2 rounded-md">

---

# Recap
- 新的 Vitiy Admin 模板
- Vite 生态
- Vue3 新语法
- 单元、组件、E2E测试
- 在线监测的一些改动
<v-click>

- 前端技术栈及项目架构已达到企业级

</v-click>

---
layout: center
class: 'text-center pb-5 :'
---

# Thank You!

Slides can be found on [docs.nustarnuclear.com](https://docs.nustarnuclear.com/vitify-slide)