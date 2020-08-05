# Vue 编码规范

### 基本约束

##### 能使用 Lodash 的方法不要自己写

Good ✅

```
const newValue = cloneDeep(oldValue)
```

Bad ❌

```
const newValue = { ...oldValue }
```

##### 只添加必要注释

Good ✅

```
// Check if an incoming prop key is a declared emit event listener.
// e.g. With `emits: { click: null }`, props named `onClick` and `onclick` are
// both considered matched listeners.
export function isEmitListener(comp: Component, key: string): boolean { ... }
```

Bad ❌

```
// 通过id获取字段列表
function getFieldListById() {}
```


##### 单个JS / Vue 文章代码不能超过 `800行`
##### 禁止提交非必要 console.log
##### ESLint 不通过禁止提交

### 命名规范

##### class / type 名需要大写开头

Good ✅

```
class FieldItem {}
const FieldItem = {
  id: null,
  name: null
}
```

Bad ❌

```
class fieldItem {}
const Fielditem = {}
```

##### 方法/对象 要采用驼峰命名

Good ✅

```
const styleConfig = {}
function styleConfig () {}
```

Bad ❌

```
const StyleConfig = {}
function Styleconfig () {}
```

##### 如对应关系未获得广泛认可，禁止使用缩写

关于对应关系不确定的词，禁止使用缩写

Good ✅

```
const dataSource = {}
function mathJs () {}
const newValue = {}
```

Bad ❌

```
const ds = {}
function mathJavaScript () {}
const newVal = {}
```

##### 数值/字符型等基础数据类型常量，使用全大写

Good ✅

```
const BAR_CHART_LENGTH = 70;
const BAR_CHART_TYPE_CHART = "bar";
const BAR_CHART_TYPE_CHART = symbol("bar");
```

Bad ❌

```
const barChartLength = 70;
const Bar_chart_CHART = "bar";
const BAR_chart_type_Symbol = symbol("bar");
```

##### 注意对象层级结构，不要重复描述

Good ✅

```
const options = {
  field: {
    id: "",
    name: ""
  }
}
```

Bad ❌

```
const options = {
  field: {
    fieldId: "",
    fieldName: ""
  }
}
```


## Vue

#### Prop 定义应该尽量详细

Good ✅

```
props: {
  status: {
    type: String,
    required: true
  }
}
```

Bad ❌

```
props: ['status']
```

## Vuex

#### 禁止在页面中使用 $store API

1. 读取 store 数据，需要通过 `getter`

Good ✅

```
import { mapGetters } from "vuex"

export default {
  computed: mapGetters("xList")
}
```

bad ❌

```
{
  methods: {
    computeXList() {
      return this.$store.xList;
    }
  }
}
```

2. 分发Action 需要使用 mapActions


Good ✅

```
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

```
this.$store.dispatch("queryFields", window.innerHeight);
```

3. 不可以直接commit 调用 mutation

Good ✅

```
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

```javascript
this.$store.commit("queryFields", window.innerHeight);
```

or

```vue
{
  methods: {
    mapMutations([ "queryFields" ]),
    init() {
      this.queryFields()
    }
  }
}
```
