* ArthurSlog
* SLog-7
* Year·1

* Guangzhou·China
* July 13th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

不管你是喜欢或者讨厌现在的生活 那都是因为你自己造成的

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息：

* [brew官方手册](https://brew.sh)，一款MacOS工具，具体内容请移步官方手册

* [npm官方手册](https://docs.npmjs.com/)，一刻nodejs代码包管理工具，具体内容请移步官方手册

* [vue官方安装手册](https://cn.vuejs.org/v2/guide/installation.html)，前端框架

* [chrome浏览器devtools扩展](https://github.com/vuejs/vue-devtools#vue-devtools)，用于调试Vue.js应用程序，下一篇进行详细介绍和应用，本篇先自己花一分钟做个了解

* [vue快速使用手册](https://scrimba.com/playlist/pXKqta)，可以先花20分钟的时间写一写感受一下vue的写法

* [koa官方安装和使用手册](https://koajs.cn/)，后端框架

##### 执行方案

* 切换至桌面路径

> cd ~/Desktop

* 创建一个新文件夹

> mkdir node_koa_vue_learningload

* 切换至新建的文件夹路径下

> cd node_koa_vue_learningload

* 使用npm指令初始化nodejs项目环境，一路回车，完成初始化

> npm init

* 安装我们本次的主角，koa、vue、还有中间件koa-static

> sudo npm install koa vue koa-static

10. 打开 package.json 查看里面的配置内容，查看 vue框架 的工具依赖选项 “devDependencies” 如下

> vim package.json

```
    "@types/node": "^8.0.33",
    "@types/webpack": "^3.0.13",
    "acorn": "^5.2.1",
    "babel-core": "^6.25.0",
    "babel-eslint": "^8.0.3",
    "babel-helper-vue-jsx-merge-props": "^2.0.2",
    "babel-loader": "^7.0.0",
    "babel-plugin-istanbul": "^4.1.4",
    "babel-plugin-syntax-dynamic-import": "^6.18.0",
    "babel-plugin-syntax-jsx": "^6.18.0",
    "babel-plugin-transform-vue-jsx": "^3.4.3",
    "babel-preset-es2015": "^6.24.1",
    "babel-preset-flow-vue": "^1.0.0",
    "buble": "^0.19.3",
    "chalk": "^2.3.0",
    "chromedriver": "^2.30.1",
    "codecov": "^3.0.0",
    "commitizen": "^2.9.6",
    "conventional-changelog": "^1.1.3",
    "cross-spawn": "^5.1.0",
    "cz-conventional-changelog": "^2.0.0",
    "de-indent": "^1.0.2",
    "es6-promise": "^4.1.0",
    "escodegen": "^1.8.1",
    "eslint": "^4.13.1",
    "eslint-loader": "^1.7.1",
    "eslint-plugin-flowtype": "^2.34.0",
    "eslint-plugin-jasmine": "^2.8.4",
    "eslint-plugin-vue-libs": "^2.0.1",
    "file-loader": "^1.1.5",
    "flow-bin": "^0.61.0",
    "hash-sum": "^1.0.2",
    "he": "^1.1.1",
    "http-server": "^0.11.1",
    "jasmine": "^2.99.0",
    "jasmine-core": "^2.99.0",
    "karma": "^2.0.0",
    "karma-chrome-launcher": "^2.1.1",
    "karma-coverage": "^1.1.1",
    "karma-firefox-launcher": "^1.0.1",
    "karma-jasmine": "^1.1.0",
    "karma-mocha-reporter": "^2.2.3",
    "karma-phantomjs-launcher": "^1.0.4",
    "karma-safari-launcher": "^1.0.0",
    "karma-sauce-launcher": "^1.1.0",
    "karma-sourcemap-loader": "^0.3.7",
    "karma-webpack": "^2.0.3",
    "lint-staged": "^7.0.0",
    "lodash": "^4.17.4",
    "lodash.template": "^4.4.0",
    "lodash.uniq": "^4.5.0",
    "lru-cache": "^4.1.1",
    "nightwatch": "^0.9.16",
    "nightwatch-helpers": "^1.2.0",
    "phantomjs-prebuilt": "^2.1.14",
    "resolve": "^1.3.3",
    "rollup": "^0.54.1",
    "rollup-plugin-alias": "^1.3.1",
    "rollup-plugin-babel": "^3.0.2",
    "rollup-plugin-buble": "^0.19.2",
    "rollup-plugin-commonjs": "^8.0.0",
    "rollup-plugin-flow-no-whitespace": "^1.0.0",
    "rollup-plugin-node-resolve": "^3.0.0",
    "rollup-plugin-replace": "^2.0.0",
    "rollup-watch": "^4.0.0",
    "selenium-server": "^2.53.1",
    "serialize-javascript": "^1.3.0",
    "shelljs": "^0.8.1",
    "typescript": "^2.7.1",
    "uglify-js": "^3.0.15",
    "webpack": "^3.11.0",
    "weex-js-runtime": "^0.23.6",
    "weex-styler": "^0.3.0",
    "yorkie": "^1.0.1"
```

* 有些模块和软件包只是开发所必需的，在生产中不需要，这些就记录在 “devDependencies”

* vue框架 分为开发环境下和生产环境下，开发环境指的是你在写代码的时候，生产环境指的是你的代码在上线的服务器上运行的时候

* vue框架 的使用和发展，现在趋向于全栈，所以 会有下面这样的架构（使用流程），其中 webpack 这个工具是必须的：

![vue框架 的使用架构](https://github.com/BlessedChild/LogofAxu/blob/master/images/Slog7/Stream.png?raw=true)

* 至此，XXX。

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
