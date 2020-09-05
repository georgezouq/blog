# 从NPM大数据看前端的发展趋势

本文来自JSConf 的一篇演讲整理

原始演讲: [npm and the future of JavaScript - Laurie Voss - JSConf US 2018](https://www.youtube.com/watch?v=mSQh0gcDXkc&list=PL37ZVnwpeshGGVeMxXxCxjQZBJq5bqM7b&index=10)

本文数据来自 NPM，结合历史历届 JSConf 的演讲主题，为大家梳理 JS 发展脉络

## JS 发展规模

* Github 上最多的仓库数

![image](http://note.youdao.com/yws/res/21751/WEBRESOURCE8f045c7d0857a57ff1a2939366419b2e)

* StackOverflow 上最多的问题数

![image](http://note.youdao.com/yws/res/21753/WEBRESOURCE27fe41b2b4a0e07663216e91ea5d015b)

* 最大的软件镜像库

![image](http://note.youdao.com/yws/res/21755/WEBRESOURCE5fe521bef4226ef0f42be99317cf0980)

* JS是最受欢迎的变成语言

![image](http://note.youdao.com/yws/res/21757/WEBRESOURCEc06e8e782c69cf176e9e082e2de3b044)

## 开发者

* 有经验的开发者越来越多

![image](http://note.youdao.com/yws/res/21759/WEBRESOURCEec75f6e7f14283fa53bb71ba3e45c4f7)

* 99% 的 JS 开发者使用 NPM

![image](http://note.youdao.com/yws/res/21761/WEBRESOURCE06f3d9ecc000c782b32fd096ffaa2c22)

* 29%的开发者没使用开源协议

![image](http://note.youdao.com/yws/res/21763/WEBRESOURCE16f5b9744ea8eecd6eb74a3d945a9b27)

* JS开发者使用的其他语言

![image](http://note.youdao.com/yws/res/21765/WEBRESOURCE7962963ba9e891135d971727751df6f7)

* JSConf 演讲主题中的 前端 or 后端项目

![image](http://note.youdao.com/yws/res/21767/WEBRESOURCE852bd92c93b64602485df27c29f0c15c)

* 97%的 JS 开发者为开发浏览器应用

![image](http://note.youdao.com/yws/res/21769/WEBRESOURCE215a6b27ff57f67c37bd59267dac3bdc)

* JS 应用的部署方式

PS：这里惊讶到我的是K8S似乎还是一个昨天才开始使用的很新的应用，这里居然占了 56% （当然，容器化应该包括 Docker）

![image](http://note.youdao.com/yws/res/21771/WEBRESOURCEbea3ac951eb62228745f5eef3414ca11)

## Serverless 微服务 和 Docker 的热度

![image](http://note.youdao.com/yws/res/21773/WEBRESOURCEe871c9dabdd9803fd29b97670ea9bd75)

## 前端框架库的增长

值得注意的是，这里对比的是下载数的增长率，所以曲线尽管可能比较平滑，但是也是在增长的

这里我研究了一下 preact 蛮有意思的一个框架

![image](http://note.youdao.com/yws/res/21775/WEBRESOURCEf59d8efb6c69e3c72513cf974d56b712)

## 框架对比

* 服务端渲染

现在服务端渲染非常流行，但是如果我没记错的，PHP好像就是这么做的

![image](http://note.youdao.com/yws/res/21777/WEBRESOURCE062616f5482182ee00b6d1331f31f346)

* JS 服务端框架 Express依旧是主宰

![image](http://note.youdao.com/yws/res/21779/WEBRESOURCEe36d3be9a27bba382e0cc94f9e85d160)

* Gatsby 盖茨比居然是最受欢迎的服务端框架 8%的JS开发者在使用

虽说反复强调紧致套娃，但是 React Vue Angular 的SSR框架分别为 Next Nuxt Nest 还是惊讶了我。看我们前端开发者多团结

![image](http://note.youdao.com/yws/res/21781/WEBRESOURCE7f0481023c7b212904e0aa84849c7a86)

* JS 领域最热的讨论就是 “不要写JS！”

Anyway 我还是认为JS（& TS）是世界上最好的语言

![image](http://note.youdao.com/yws/res/21786/WEBRESOURCEb5e66b723e0d52f60f8a5fefadde67b2)

## 63% 的 JS 开发者使用 TS

这个一点不惊讶，Angular 带过去一波，马上 Vue3 也要用 TS 写了。不知道为什么JS新的标准为什么出得那么慢 -。-！

![image](http://note.youdao.com/yws/res/21788/WEBRESOURCEa11b2ef78f229a5c4dea8f1bddda4402)

## 对未来 JS 端的畅想

未来的前端发展更应该朝着面向组件开发，大家把现成的组件不断进行集成，快速的组装出一个一个应用，就像 VB/C\# 之前的那样

![image](http://note.youdao.com/yws/res/21812/WEBRESOURCE7ea66231d4e80c3c7ba0235330d009d3)

