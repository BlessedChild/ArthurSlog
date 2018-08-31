# Slog56_React框架_React使用说明书

* ArthurSlog
* SLog-56
* Year·1

* Guangzhou·China
* Sep 1th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

有人前进 就有人后退 还有些人保持在中间 或许大家其实都是在前进 只是大家的前进的速度不一样罢了

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [React CDN Links](https://reactjs.org/docs/cdn-links.html)

* [babel](https://babeljs.io/)

* [react](https://reactjs.org/)

* [react-dom](https://reactjs.org/docs/react-dom.html)

* [Github](https://github.com/BlessedChild/React_learningload)

### 开始编码

* 这篇文章使用的是直接在[浏览器引入的方法](https://reactjs.org/docs/cdn-links.html)，

* 所以需要先下载三个文件：
1. [babel.min.js]() -- 一个转换器
2. [react-dom.development.js]() -- ReactDOM是React和DOM之间的粘合剂
3. [react.development.js]() -- 可以使用React来定义和创建元素，生命周期钩子等，即React应用程序的内核

* 关于react和react-dom，[官方的解释](https://reactjs.org/blog/2015/10/07/react-v0.14.html)如下：

``` txt
Two Packages: React and React DOM
As we look at packages like react-native, react-art, react-canvas, and react-three, it has become clear that the beauty and essence of React has nothing to do with browsers or the DOM.

To make this more clear and to make it easier to build more environments that React can render to, we’re splitting the main react package into two: react and react-dom. This paves the way to writing components that can be shared between the web version of React and React Native. We don’t expect all the code in an app to be shared, but we want to be able to share the components that do behave the same across platforms.

The react package contains React.createElement, .createClass, .Component, .PropTypes, .Children, and the other helpers related to elements and component classes. We think of these as the isomorphic or universal helpers that you need to build components.

The react-dom package has ReactDOM.render, .unmountComponentAtNode, and .findDOMNode. In react-dom/server we have server-side rendering support with ReactDOMServer.renderToString and .renderToStaticMarkup.
```

* 大概的意思就是

``` txt
以前react框架体系里里面有react-native，react-art，react-canvas和react-three这样
的包，浏览器和DOM用不到这些包，那为什么会这样呢？
因为react想要多平台发布，一次代码就可以导出各种平台的程序，例如ios、android、pc...
从v0.14版本开始，react包拆分为两个：react和react-dom，这样，就为编写可以在
React和React Native的Web版本之间共享的组件铺平了道路。
他不希望共享应用程序中的所有代码，但希望能够共享跨平台执行相同操作的组件。
所述react包中包含React.createElement，.createClass，.Component，.PropTypes
.Children，和与元件和组件类的其它辅助函数。我们将这些视为构建组件所需的同构或通用助手。
该react-dom包有ReactDOM.render，.unmountComponentAtNode和.findDOMNode。在
react-dom/server我们的服务器端渲染支持ReactDOMServer.renderToString和.renderToStaticMarkup
```

* 了解完了相关信息之后，还需要知道运行babel需要开启一个web服务器

* 切换至当前文件路径下：

> cd ~/Desktop/React_learningload/

* 使用npm指令安装 koa 和 koa-static

> sudo npm install koa koa-static

* 编写静态web服务器

~/Desktop/React_learningload/server.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();

// $ GET /package.json
app.use(serve('.'));

app.listen(3000);

console.log('listening on port 3000');
```

* 使用koa开启一个静态web服务器

> nodejs server.js

* 接着编写 html文件

~/Desktop/React_learningload/index.html
``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Oh~ React!</title>
   	<script src="./react.development.js"></script>
    <script src="./react-dom.development.js"></script>
    <script src="./babel.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
  <script type="text/babel" src="./react_compent_HelloWorld.js"></script>
  </body>
</html>
```

* 根据react框架编写 js文件

~/Desktop/React_learningload/react_compent_HelloWorld.js
```js
ReactDOM.render(
  <h1>Hello, React!</h1>,
  document.getElementById('example')
);
```

* 至此，我们简单了解了react的使用。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
