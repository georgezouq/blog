# Vue 编码规范

### 基本约束

#### 单个JS / Vue 文章代码不能超过 `800行`

#### 禁止提交非必要 `console.log`

#### `ESLint` 规则必须通过才能提交

#### 变量 / 方法名有拼写错误需修改

#### 能使用 Lodash 的方法不要自己写

Good ✅

```text
const newValue = cloneDeep(oldValue)
```

Bad ❌

```text
const newValue = { ...oldValue }
```

#### 只添加必要注释

如无必要，不要加注释，如有必要，必须加注释。

Good ✅

```text
// Check if an incoming prop key is a declared emit event listener.
// e.g. With `emits: { click: null }`, props named `onClick` and `onclick` are
// both considered matched listeners.
export function isEmitListener(comp: Component, key: string): boolean { ... }
```

Bad ❌

```text
// 通过id获取字段列表
function getFieldListById() {}
```

### 命名规范

#### class / type 名需要大写开头

Good ✅

```text
class FieldItem {}
const FieldItem = {
    id: null,
    name: null
}
```

Bad ❌

```text
class fieldItem {}
const Fielditem = {}
```

#### 方法 / 对象 要采用驼峰命名

Good ✅

```text
const styleConfig = {}
function styleConfig () {}
```

Bad ❌

```text
const StyleConfig = {}
function Styleconfig () {}
```

#### 如对应关系未获得广泛认可，禁止使用缩写

关于对应关系不确定的词，禁止使用缩写

Good ✅

```text
const dataSource = {}
function mathJs () {}
const newValue = {}
```

Bad ❌

```text
const ds = {}
function mathJavaScript () {}
const newVal = {}
```

#### 数值 / 字符等基础数据类型常量，使用全大写

Good ✅

```text
const BAR_CHART_LENGTH = 70;
const BAR_CHART_TYPE_CHART = "bar";
const BAR_CHART_TYPE_CHART = symbol("bar");
```

Bad ❌

```text
const barChartLength = 70;
const Bar_chart_CHART = "bar";
const BAR_chart_type_Symbol = symbol("bar");
```

#### 注意对象层级结构，不要重复描述

Good ✅

```text
const options = {
    field: {
        id: "",
        name: ""
    }
}
```

Bad ❌

```text
const options = {
    field: {
        fieldId: "",
        fieldName: ""
    }
}
```

## Vue

### Prop

#### 非必填需提供默认值

#### 定义应该尽量详细

Good ✅

```text
props: {
  status: {
    type: String,
    required: true
  }
}
```

Bad ❌

```text
props: ['status']
```

### Composition API

#### 目录结构

组件中使用到的 hook 函数统一放到同级目录下 `hook.js` 文件中

```text
- src
    - components
        - Table
            - hooks.js // Table 组件使用的所有 hook 函数放到这里
            - index.vue
    - hooks // 有可能全局使用的 hook 函数放到这里
    - views
```

#### 所有的 hook 函数必须使用 `use` 开头

Good ✅

```javascript
const useTask = () => {
  const $hasJob = ref(false);
  return { $hasJob }
}
```

Bad ❌

```javascript
const getTask = () => {
  const hasJob = ref(false);
  return { hasJob }
}
```

#### 使用 CompositionAPI ref 开头的变量要使用 $ 开头

为了提醒使用变量中的 `value` 属性获取元素，请使用 `ref` 包装的响应式变量使用 `$` 开头.

Good ✅

```javascript
const useTask = () => {
  const $hasJob = ref(false);
  return { $hasJob }
}
```

Bad ❌

```javascript
const useTask = () => {
  const hasJob = ref(false);
  return { hasJob }
}
```

#### ref 变量返回时需要去掉 $ 开头

由于在组件中使用 `ref` 变量不需要使用 `value`，所以在 `setup` 方法返回到外部时需要去掉 `$`.

Good ✅

```javascript
export default {
    setup() {
        const { $hasJob } = useTask();
        return {
          hasJob: $hasJob
        }
    }
}
```

Bad ❌

```javascript
export default {
    setup() {
        const { $hasJob } = useTask();
        return {
          $hasJob
        }
    }
}
```

## Vuex

#### 禁止在页面中使用 $store API

如需要，需使用 mapActions / mapGetters 显示声明

#### 读取 store 数据，需要通过 `getter`

Good ✅

```text
import { mapGetters } from "vuex"

export default {
    computed: mapGetters("xList")
}
```

bad ❌

```text
{
    methods: {
        computeXList() {
            return this.$store.xList;
        }
    }
}
```

#### 分发Action 需要使用 mapActions

Good ✅

```text
{
    methods: {
        mapActions([ "queryFields" ]),
        init() {
            this.queryFields()
        }
    }
}
```

Bad ❌

```text
  this.$store.dispatch("queryFields", window.innerHeight);
```

1. 不可以直接commit 调用 mutation

Good ✅

```text
{
    methods: {
        mapActions([ "queryFields" ]),
        init() {
            this.queryFields()
        }
    }
}
```

Bad ❌

```text
  this.$store.commit("queryFields", window.innerHeight);
```

or

```text
{
    methods: {
        mapMutations([ "queryFields" ]),
        init() {
            this.queryFields()
        }
    }
}
```

#### 页面中禁止直接调用 Mutation

Mutation 需在 Action 中 commit，页面只能 dispatch action

#### 禁止在 Getters 中操作 Store 数据、dispatch & commit

Good ✅

```text
{
    getters: {
        currentId(state) {
            return state.id
        }
    }
}
```

Bad ❌

```text
{
    getters: {
        currentId(state) {
            state.type = state.list[state.id]
            return state.id
        }
    }
}
```

