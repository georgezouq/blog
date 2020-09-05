# Vuex 工作原理

### Vue 双向绑定

1. 数据劫持
2. 添加观察者

数据劫持 实现：

```js
Object.defineProperty(obj, key, {
    enumerable: true,
    configurable: true,
    get: function reactiveGetter() {
      const value = getter ? getter.call(obj) : val
      if (Dep.target) {
        dep.depend()
        if (childOb) {
          childOb.dep.depend()
        }
        if (Array.isArray(value)) {
          dependArray(value)
        }
      } 
      return value
    },
    set: function reactiveSetter(newVal) {
      const value = getter ?  getter.call() : val
      if (newVal === value || (newVal !== newVal && value !== value)) {
        return
      }
      if (setter) {
        setter.call(obj, newVal)
      } else {
        val = newVal
      }   
      childOb = !shallow && observe(newVal)
      dep.notify()
    } 
  }
)
```

劫持了对象的 `getter` 和 `setter` 方法。在所代理的属性的get方法中，当 `dep.Target` 存在的时候会 调用 `dep.depend()`

- Object.defineProperty
- dep.depend()

观察者模式实现

```js
class Dep {
  constructor(props) {
   super(props);
   this.subs = []
  }

  addSub(sub) {
    this.subs.push(sub)
  }
  
  depend() {
    if (Dep.target) {
      this.subs.addDep(this)
    }
  } 
  
  notify() {
    this.subs.forEach(sub => sub.update())
  } 
}

class Watcher {
  constructor(props) {
    super(props);
    this.vm = vm
    this.getter = expOrFn
    this.value
  }
  
  get() {
    Dep.target = this
    var vm = this.vm
    var value = this.getter.call(vm, vm)
    return value
  }

  evaluate() {
    this.value = this.get()
  }

  addDep(dep) {
    dep.addSub(this)
  }

  update() {
    console.log('更新')
  }

}

// 观察者
var dep = new Dep()

// 被观察者
var watcher = new Watcher({x: 1}, (val) => val)
watcher.evaluate()

// 观察者监听被观察对象
dep.depend()

dep.notify()
```

### Vuex 插件

1. Vuex 注入代码调用 `applyMixin` (新版本 `Vue.mixin`)，在所有的组件的 `beforeCreate` 生命周期注入了 `this.$store` 对象

总结

Vuex的双向绑定通过调用 new Vue实现，然后通过 Vue.mixin 注入到Vue组件的生命周期中，再通过劫持state.get将数据放入组件中
