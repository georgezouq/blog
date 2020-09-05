# IM客户端设计常见问题

不知不觉做了六年的程序员，主做前端也已经三年时间，在这六年的时间里做了不少项目。虽然对基础层面、算法、JS运行原理去深究一些底层的运行机制还是一知半解。但这三年的项目中遇到的问题及做的优化点也有很多，深入JS底层的问题、深入逻辑底层的算法也遇到不少，但总是缺乏系统的梳理。在这里，率先对两年前我所做一个IM项目所遇到的问题作出整，方便知识后序查阅。

项目背景：工程师端是为实现线上客服在线通过IM的形式，发送/接受：文本、图片、标签、语音 及 在线视频直播。 等方式解决各个通路（公众号、APP）接入用户的问题。项目以 Electron 作为壳子，使用 vue 实现窗口界面。整个界面风格非常像Mac版QQ

![image](http://note.youdao.com/yws/res/21043/WEBRESOURCE70409b1016e26593a435ce5428542c77)

### IM消息发送顺序问题

不知道大家有没有观察过桌面版QQ发送框的输入逻辑，我们在输入框中同时输入的内容类型可以是：文字、表情、图片、链接... 其中，文字、表情和链接可以被单独发送出去，图片需要做拆分，比如我输入下列内容

```
今天天气真好[图片] 太阳火热 [图片] [图片]
```

点击发送按钮，该内容会被拆分为:

```
[
    { type: 'text', content: '今天天气真好' },
    { type: 'image', url: [file] }, 
    { type: 'text', content: '太阳火热' },
    { type: 'image', url: [file] }, 
    { type: 'image', url: [file] }, 
]
```

在发送的时候，我们需要调用多次发布接口，发布文字消息、图片、文字、图片、图片。由于是多消息发送，保证消息的发布顺序直观重要。关于这种情况，我们参考了一个 经典的 Promise 红绿灯问题：

解决方案：https://www.w3ctech.com/topic/916

### 多消息通路整合

我们当时遇到的业务问题在于复杂的后端服务设计，整个应用由于用户接入的通路不同，导致需要对接多套IM
消息机制，接入 APP端用户IM 使用 长轮询链接，接入 微信端用户IM使用Websocket。两套机制在客户端的业务业务场景基本一致，但是所调用的系统和服务各不相同。所以我们在action 层做了分离，action的实例使用适配器模式进行初始化，action 的适配方法通过参数判断该用户是由 APP通路接入 还是 微信通路。调用不同的 action 实现

```
class ActionBase {
  getUserInfo() {}
}

class ActionAdapter extends ActionBase {
  constructor () {
    super()

    this.apiWX = new WXApi()
    this.apiApp = new AppApi()
  }

  getUserInfo(userId, phone, from) {
    if (from === 'wx')
      return this.apiWX.getUserInfo(userId, phone)

    this.apiApp.getUserInfo(userId)
  }
}

class WXApi extends ActionBase {
  getUserInfo(userId, phone) {
    console.log('Get user info from wx')
  }
}

class AppApi extends ActionBase {
  getUserInfo(userId) {
    console.log('Get user info from APP')
  }
}

const adapter = new ActionAdapter()
adapter.getUserInfo('1', '18668888888', 'wx')
```

MVC 和 MVVM 设计模式的精髓就在于View 层与 Model
 层的解耦，通过View组件调用适配器，我们可以实现在最小化View层修改的前提下，适配新的业务体系。

### 输入框的复制与覆盖

### Electron 的跨进程通讯 

Electron 有两个进程 Main 及 Renderer，两个进程通过IPC进行实时通讯。在业务触发一个较底层的功能时，我们通过 渲染进行调用 ipcMain，与主进程进行通讯，在 MainProcess主进程 中对对应的系统级 Electron 的API进行调用。

同时，在一些底层事件中，比如 关闭程序、触发快捷键、点击菜单栏等，主进程会率先收到消息，通过 ipcRenderer 调用渲染进程，通知页面对事件作出响应。

### 保证消息必达

- 监听错误并提示感叹号
- 刷新聊天记录
- Websocket链接监听
- 客户端心跳保活
- 服务器轮询监测网络抖动

### Electron 的多窗口管理

维护窗口

### 复杂跨多系统长链路调用，前端如何独善其身

随着项目业务的逐渐增多，我们调用后台的系统服务也变得越来越多，一度达到十几套系统的复杂程度。单一一个请求的前端业务动作，比如登陆，就要调用三套系统的五个接口实现。有些业务接口的饿调用顺序还是强依赖的，比如你必须先拿到 SessionId 才能请求登陆用户基本信息。后端系统相当复杂，并且从系统稳定性的角度看，几乎不能做大的调整。那么我们只有从前端的角度入手解决问题，开始的时候我们使用Promise 的回调链去处理这种长链路请求情况。比如登陆操作：

```js
login(username, password) {
    const data = {}
    apiWX.auth({ username, password }).then(res => {
        return apiWX.getUserInfo({ res.userId })
    }).then(res => {
        return apiApp.auth({ username, password })
    }).then(res => {
        return apiApp.getUserInfo({ userId: res.userId })
    }).then(res => {
        return apiWX.getWorkState({ userId: res.userId })
    }).then(res => {
        return apiWX.startSocketListener({ userId: res.userId })
    }).then(res => {
        return apiApp.startSocketListener({ userId: res.userId })
    })
}
```

有一些很明显的一个问题：

1. 一些系统之间可能前后并没有依赖关系，如果单纯是顺序调用的话，加载时间会非常长


    对不同的调用链路进行拆分，不把没有依赖关系的promise放到一条链路当中

2. 单一接口调用出错会导致余下接口都调用不成功，那怕是不那么重要的服务。针对上述问题我们做了两点优化

```js
/**
 * finally方法用于指定不管Promise对象最后状态如何，都会执行的操作。
 * 它与done方法的最大区别，它接受一个普通的回调函数作为参数，该函数不管怎样都必须执行。
 * @param callback
 * @returns {Promise.<Promise.<*>>}
 */
Promise.prototype.finally = function (callback) {
    const P = this.constructor
    return this.then(
        value => P.resolve(callback()).then(() => value),
        reason => P.resolve(callback()).then(() => {
            throw reason
        })
    )
}
```

3. Promise对象的回调链，不管以then方法或catch方法结尾，要是最后一个方法抛出错误，都有可能无法捕捉到（因为Promise内部的错误不会冒泡到全局）

```js
Promise.prototype.done = function (onFulfilled, onRejected) {
    this.then(onFulfilled, onRejected)
        .catch((reason) => {
            setTimeout(() => {
                throw reason
            }, 0)
        })
}
```

### 对抗复杂链路调用的堡垒：中台构建

我们可以看到，大型企业内部管理系统的复杂程度令人咋舌，而我们期待服务端去做出一些改变，基于其系统的历史情况，尤其很多系统属于跨部门协同，是不现实的。而每一个系统基于其自身的定位，只是在几个业务线之间，而我们的应用有需要跨越多个系统进行调用，取数据、实现业务能力。所以最好的方案是我们在中间搭建一层中台，一方面针对后端，通过内网对单一业务动作集成不同的系统，这样对于一些跨系统的请求更快。前端只需要跟中台通讯，保证客户端调用的单一性，适度的与复杂调用链路解偶，降低客户端内部的复杂度。另外，中台实现了一种新的业务能力，这种能力可以被其他的前端应用调用，实现业务的快速拓展。

