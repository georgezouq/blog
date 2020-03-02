# 在框架设计时寻求平衡

Front-end framework design

Compare not github star and npm download,and need to care about more internal technical decision

There isn't a single good vs bad spectrum for framework

Software ---> trade-offs

### Scope

how much framework try to do for you

Libraries vs. Framework
Primitives VS Abstractions
Bazaar vs. Cathedral

React Angular

##### Small Scope Props

- Fewer concepts to get started with
- More flexibility and more user land opportunities -> active ecosystem
- Smaller maintenance surface -> team can focus on exploring new ideas

##### Small Scope Cons

- More plumbing work needed when solving inherent complex problems with simple concepts
- Patterns naturally emerge over time and become semi-required knowledge, but often not officially documented
- Ecosystem moving too fast can lead to fragmentation and constant churn

##### 大作用域 的优点

- Most common problems can be solved with built-in abstractions
- 中心化设计流程确保了持续、连贯的生态系统

##### 大作用域 的缺点

- 更高的学习成本
- 对于官方解决方案不能很好的满足用户需求时，很不灵活
- 诸多功能的维护，使得新的idea的实现变得非常困难

##### 进步 作用域

- 分层设计允许组件以渐进的方式选择特征
- 更低的学习成本
- 有官方文档支持的实践方案

##### 进步 作用域 缺点 

- 生态不会像小作用域一样多种多样
- 跟大作用一样会有很多的层面维护

### 渲染机制

i.e. How a framework allows you to express your UI structure and how it renders stuff

JSX vs. Templates
Expressiveness vs. Raw Perf
Runtime Scheduling vs. AOT

##### JSX / Virtual DOM 优点

- Full expressiveness of JavaScript
- Treats the view as data
    - Userland possibility of custom usage of view data, e.g. testing & rendering to alternative targets
    
##### JSX / Virtual DOM 缺点

- 天生的大量消耗资源
- 动态渲染方法使得它很难优化
- 运行时调度优化感知性能，但是需要一个很重的运行时

##### 模版编译 优点

- 可以生成更直接的渲染指令，具有更好的原始性能
- Depends on strategy, may lead to much lighter runtime baseline size

##### 模版编译 缺点

- 模版标准限制了用户的灵活性
- 每个模版运行时更轻，来自于更多、冗长的输出
- 运行时编译导致对构建步骤的强依赖

##### Vue ->  VDOM + Template

- Performance: Compilation step produces specially optimized V-DOM render function
- Expressiveness: Option to skip template and drop down to manually written render functions for full flexibility

#### Block Tree

Separate the template into nested blocks, using structural directives as boundaries. Within each block the node structure is static, and dynamic nodes are tracked in a flat array

36ms --> 5.44ms
6x faster vue2 -> vue3

### State Mechanism

- Mutable vs. Immutable
- Dependency tracking vs. Dirty Checking
- Reactivity vs. Simulated Reactivity

### Where is the  perfect balance point?

The framework landscape is like a multi-dimensional space with multiple ever-moving entities, each seeking its own balance point.


