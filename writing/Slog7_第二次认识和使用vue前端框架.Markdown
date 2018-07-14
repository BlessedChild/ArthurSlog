* ArthurSlog
* SLog-7
* Year·1

* Guangzhou·China
* July 13th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

不管你是喜欢或者讨厌现在的生活 那都是因为你自己造成的

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息：

* 这里是我第二次为vue框架写文章，如果你没有看过第一次的文章，请先移步至[使用vue前端框架实现单页应用(SPA)](https://juejin.im/post/5b4799435188251aca1e23d0)，从第一次开始了解

* [brew官方手册](https://brew.sh)，一款MacOS工具，具体内容请移步官方手册

* [npm官方手册](https://docs.npmjs.com/)，一款nodejs代码包管理工具，具体内容请移步官方手册

* [vue官方安装手册](https://cn.vuejs.org/v2/guide/installation.html)，前端框架

* [chrome浏览器扩展 vue-devtools](https://github.com/vuejs/vue-devtools#vue-devtools)，用于调试Vue.js应用程序

* [webpack：vue框架必备](https://webpack.js.org/)，中文网站：[webpack：vue框架必备](https://www.webpackjs.com/)，Github：[webpack：vue框架必备](http://webpack.github.io/)

* [babel：vue框架必备](https://babeljs.io/)，中文网站：[vue框架必备：babel](https://www.babeljs.cn/)

### vue框架是一些 nodejs 和 javascript 代码的集合，这里指的是 [vue.js](https://cn.vuejs.org/v2/guide/installation.html#%E7%9B%B4%E6%8E%A5%E7%94%A8-lt-script-gt-%E5%BC%95%E5%85%A5) 和 他的 [Ecosystem(生态系统)](https://github.com/vuejs/vue) 

#### vue.js是vue框架的开始，他是一份js文件，就像这样[vue.js](https://cn.vuejs.org/v2/guide/installation.html#%E7%9B%B4%E6%8E%A5%E7%94%A8-lt-script-gt-%E5%BC%95%E5%85%A5)，可以嵌进html标签里，例如：

``` html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

* 为了对vue有一个主观的认识，对，是主观，下面 来操作一下：

1. 切换至桌面路径：

> cd ~/Desktop

2. 创建一个新文件夹

> mkdir testvue

3. 切换至新建的文件夹路径下

> cd testvue

4. 使用npm指令初始化nodejs项目环境，一路回车，完成初始化

> npm init

5. 使用npm指令，安装我们本次的主角 vue框架

> sudo npm install vue

6. 切换至 当前路径下的 node_modules ，存放node中间件的专用文件夹，也就是依赖

> cd node_modules

7. 查看当前路径下的文件，会看到有一个 vue文件夹

> ls

```
vue
```

8. 切换至 vue文件夹

> cd vue

9. 查看当前路径下的文件，会看到如下所示：

> ls

```
LICENSE		dist		src
README.md	package.json	types
```

#### 这里面有两个重要的文件夹 dist 和 src
#### dist 里面放着的是 javascript代码 ，运行在浏览器里，也就是运行在客户端上
#### src  里面放着的是 nodejs 代码，运行在操作系统上，也就是运行在开发者的机器上
#### src 里的源码生成 dist 里的 javascript代码 ，这份代码运行在客户端上
#### dist 里的每一份代码都是独立的，也就是说你只要选择其中一份使用就可以了，具体怎么选择，需要看使用场景，参考[对不同构建版本的解释](https://cn.vuejs.org/v2/guide/installation.html#%E5%AF%B9%E4%B8%8D%E5%90%8C%E6%9E%84%E5%BB%BA%E7%89%88%E6%9C%AC%E7%9A%84%E8%A7%A3%E9%87%8A)
#### 一个关键的地方是，dist里面的文件如下：

||UMD	|CommonJS	|ES Module
- | - | - | -
完整版	|vue.js	|vue.common.js	|vue.esm.js
只包含运行时版	|vue.runtime.js	|vue.runtime.common.js	|vue.runtime.esm.js
完整版 (生产环境)	|vue.min.js | - | -
只包含运行时版 (生产环境)	|vue.runtime.min.js | - | -

#### 一般我们会用到 vue.js(开发环境) 和 vue.min.js(生产环境)，就像下面这样： /npm/vue/dist/vue.js

``` html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

#### 这也就是说明了，客户端--比如你的手机浏览器，会下载 vue.js 或者 vue.main.js 这份文件，由这份 js 文件来指导页面的渲染功能，这就是所谓的 前端框架vue.js

![](https://github.com/BlessedChild/LogofAxu/blob/master/images/Slog7/IMG_0124.jpg?raw=true)
![](https://github.com/BlessedChild/LogofAxu/blob/master/images/Slog7/IMG_0125.jpg?raw=true)
![](https://github.com/BlessedChild/LogofAxu/blob/master/images/Slog7/IMG_0126.jpg?raw=true)

## 上面是 vue框架 的核心文件 vue.js 的一些介绍，下面是 vue框架 的另一重要组成部分 -- vue-Ecosystem（vue-生态系统）

## Introduction

Vue (pronounced `/vjuː/`, like view) is a **progressive framework** for building user interfaces. It is designed from the ground up to be incrementally adoptable, and can easily scale between a library and a framework depending on different use cases. It consists of an approachable core library that focuses on the view layer only, and an ecosystem of supporting libraries that helps you tackle complexity in large Single-Page Applications.

#### Browser Compatibility

Vue.js supports all browsers that are [ES5-compliant](http://kangax.github.io/compat-table/es5/) (IE8 and below are not supported).

## Ecosystem

| Project | Status | Description |
|---------|--------|-------------|
| [vue-router]          | [![vue-router-status]][vue-router-package] | Single-page application routing |
| [vuex]                | [![vuex-status]][vuex-package] | Large-scale state management |
| [vue-cli]             | [![vue-cli-status]][vue-cli-package] | Project scaffolding |
| [vue-loader]          | [![vue-loader-status]][vue-loader-package] | Single File Component (`*.vue` file) loader for webpack |
| [vue-server-renderer] | [![vue-server-renderer-status]][vue-server-renderer-package] | Server-side rendering support |
| [vue-class-component] | [![vue-class-component-status]][vue-class-component-package] | TypeScript decorator for a class-based API |
| [vue-rx]              | [![vue-rx-status]][vue-rx-package] | RxJS integration |
| [vue-devtools]        | [![vue-devtools-status]][vue-devtools-package] | Browser DevTools extension |

[vue-router]: https://github.com/vuejs/vue-router
[vuex]: https://github.com/vuejs/vuex
[vue-cli]: https://github.com/vuejs/vue-cli
[vue-loader]: https://github.com/vuejs/vue-loader
[vue-server-renderer]: https://github.com/vuejs/vue/tree/dev/packages/vue-server-renderer
[vue-class-component]: https://github.com/vuejs/vue-class-component
[vue-rx]: https://github.com/vuejs/vue-rx
[vue-devtools]:  https://github.com/vuejs/vue-devtools

[vue-router-status]: https://img.shields.io/npm/v/vue-router.svg
[vuex-status]: https://img.shields.io/npm/v/vuex.svg
[vue-cli-status]: https://img.shields.io/npm/v/vue-cli.svg
[vue-loader-status]: https://img.shields.io/npm/v/vue-loader.svg
[vue-server-renderer-status]: https://img.shields.io/npm/v/vue-server-renderer.svg
[vue-class-component-status]: https://img.shields.io/npm/v/vue-class-component.svg
[vue-rx-status]: https://img.shields.io/npm/v/vue-rx.svg
[vue-devtools-status]: https://img.shields.io/chrome-web-store/v/nhdogjmejiglipccpnnnanhbledajbpd.svg

[vue-router-package]: https://npmjs.com/package/vue-router
[vuex-package]: https://npmjs.com/package/vuex
[vue-cli-package]: https://npmjs.com/package/vue-cli
[vue-loader-package]: https://npmjs.com/package/vue-loader
[vue-server-renderer-package]: https://npmjs.com/package/vue-server-renderer
[vue-class-component-package]: https://npmjs.com/package/vue-class-component
[vue-rx-package]: https://npmjs.com/package/vue-rx
[vue-devtools-package]: https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd

#### 目前 生态系统里主要成员有八位，其中 vue-develops vue调试工具 早在一开始就有提到，对，这就是一款  [？调试工具](https://github.com/vuejs/vue-devtools)
#### 然后，我们从第一个开始开启，大概了解一下这几个生态系统成员的作用，第一个是 [vue-router](https://github.com/vuejs/vue-router)，

#### 这么文件介绍太没意思 我打算后面分成8篇文章 来编写一下代码 在应用场景中去了解他们

#### 本篇我们来了解一下第一个成员 [vue-router](https://github.com/vuejs/vue-router)

#### 执行方案

* 切换至桌面路径

> cd ~/Desktop

* 创建一个新文件夹

> mkdir node_koa_vue_vue-router_learningload

* 切换至新建的文件夹路径下

> cd node_koa_vue_vue-router_learningload

* 使用npm指令初始化nodejs项目环境，一路回车，完成初始化

> npm init

* 使用npm指令安装 koa 和 中间件koa-static

> sudo npm install koa koa-static

* 编写 index.js 和 index.html 两份文件

index.js 实现一个静态的 web服务器

``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();

// $ GET /package.json
app.use(serve('.'));

app.listen(3000);

console.log('listening on port 3000');
```

index.html 使用 vue.js + vue-router.js 创建单页应用

``` html
<!DOCTYPE html>
<html>
    <head>
    <meta charset="utf-8">
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
    <title>ArthurSlog</title>
    </head>

    <body>
        <div id="app">
        <h1>Hello App!</h1>
        <p>
            <!-- 使用 router-link 组件来导航. -->
            <!-- 通过传入 `to` 属性指定链接. -->
            <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
            <router-link to="/foo">Go to Foo</router-link>
            <router-link to="/bar">Go to Bar</router-link>
        </p>
        <!-- 路由出口 -->
        <!-- 路由匹配到的组件将渲染在这里 -->
        <router-view></router-view>
        </div>

        <script>
        // 0. 如果使用模块化机制编程，导入Vue和VueRouter，要调用 Vue.use(VueRouter)

        // 1. 定义 (路由) 组件。
        // 可以从其他文件 import 进来
        const Foo = { template: '<div>foo</div>' }
        const Bar = { template: '<div>bar</div>' }

        // 2. 定义路由
        // 每个路由应该映射一个组件。 其中"component" 可以是
        // 通过 Vue.extend() 创建的组件构造器，
        // 或者，只是一个组件配置对象。
        // 我们晚点再讨论嵌套路由。
        const routes = [
        { path: '/foo', component: Foo },
        { path: '/bar', component: Bar }
        ]

        // 3. 创建 router 实例，然后传 `routes` 配置
        // 你还可以传别的配置参数, 不过先这么简单着吧。
        const router = new VueRouter({
        routes // (缩写) 相当于 routes: routes
        })

        // 4. 创建和挂载根实例。
        // 记得要通过 router 配置参数注入路由，
        // 从而让整个应用都有路由功能
        const app = new Vue({
        router
        }).$mount('#app')

        // 现在，应用已经启动了！
        </script>
    </body>
</html>
```

home.vue
``` vue
// Home.vue
export default {
  computed: {
    username () {
      // 我们很快就会看到 `params` 是什么
      return this.$route.params.username
    }
  },
  methods: {
    goBack () {
      window.history.length > 1
        ? this.$router.go(-1)
        : this.$router.push('/')
    }
  }
}
```

* 至此，XXX。

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
