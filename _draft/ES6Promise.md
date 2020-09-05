# ES6 Promise 源码解析

最近看到好多面试题中都有关于 Promise 的考察，而网上各个版本的文章对Promise的实现大相径庭，差距很多。本着想要理解官方实现方式的想到在GitHub上搜到了库 
-  [es6-promise](https://github.com/stefanpenner/es6-promise)

其中还是有很多与国内文章大有不同，或者关键地方被国内文章简化的地方，在这里做一个梳理。

很多文章中都尝试应几百行实现一个Promise，其实问题会非常多，看到官方对Promise的实现分为近十个文件超几千行代码。

国内文章通常用在 Resolve 的时候使用 `setTimeout` 保证 `then` 方法传入的参数，在 `then` 方法被调用的那一轮事件循环之后的新执行栈中执行


```js
let scheduleFlush;
// Decide what async method to use to triggering processing of queued callbacks:
if (isNode) {
  scheduleFlush = useNextTick();
} else if (BrowserMutationObserver) {
  scheduleFlush = useMutationObserver();
} else if (isWorker) {
  scheduleFlush = useMessageChannel();
} else if (browserWindow === undefined && typeof require === 'function') {
  scheduleFlush = attemptVertx();
} else {
  scheduleFlush = useSetTimeout();
}
```
