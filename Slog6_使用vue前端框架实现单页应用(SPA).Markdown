* ArthurSlog
* SLog-6
* Year·1

* Guangzhou·China
* July 13th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

时间 时间 时间 每一份有限的时间里 都饱含无限的价值 需要非常珍惜

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息：

* [brew官方手册](https://brew.sh)，一款MacOS工具，具体内容请移步官方手册

* [npm官方手册](https://docs.npmjs.com/)，一刻nodejs代码包管理工具，具体内容请移步官方手册

* [vue官方安装手册](https://cn.vuejs.org/v2/guide/installation.html)，前端框架

* [chrome浏览器devtools扩展](https://github.com/vuejs/vue-devtools#vue-devtools)，用于调试Vue.js应用程序，下一篇进行详细介绍和应用，本篇先自己花一分钟做个了解

* [vue快速使用手册](https://scrimba.com/playlist/pXKqta)，可以先花20分钟的时间写一写感受一下vue的写法

##### 执行方案

* 切换至桌面路径

> cd ~/Desktop

* 创建一个新文件夹

> mkdir node_vue_learningload

* 切换至新建的文件夹路径下

> cd node_vue_learningload

* 使用npm指令初始化nodejs项目环境，一路回车，完成初始化

> npm init

* 安装 koa 和 kao-static

> sudo npm install koa koa-static

* 需要管理员权限，输入密码

* 在当前路径下创建 index.js 和 index.html 这两个文件

index.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();

// $ GET /package.json
app.use(serve('.'));

app.listen(3000);

console.log('listening on port 3000');
```

index.html
``` html
<!DOCTYPE html>
<html>
    <head>
    <meta charset="utf-8">
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <title>ArthurSlog</title>
    </head>

    <body>
        <div id="app">{{ message }}</div>

        <script>
        new Vue({
            el: '#app',
            data: {
                message: 'Hello ArthurSlog!'
            }
        })
        </script>
    </body>
</html>
```

##### 分析一下上面的两份文件代码：

1. 在 index.js 里，引入 koa 框架和 koa-static 中间件实现了一个 静态web服务器，静态路由至当前路径下的 index.html
2. 在 index.html 里，引入 vue框架：

index.html
``` html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

3. 在 index.html 里，vue.js 使用简洁的模板语法来声明式地将数据渲染进DOM的系统：

index.html
``` html
    <body>
        <div id="app">{{ message }}</div>

        <script>
        new Vue({
            el: '#app',
            data: {
                message: 'Hello ArthurSlog!'
            }
        })
        </script>
    </body>
```

index.html
``` html
<div id="app">{{ message }}</div>
```

index.js
``` js
new Vue({
    el: '#app',
    data: {
        message: 'Hello ArthurSlog!'
    }
})
```

4. Vue 在背后做了大量工作。现在数据和 DOM 已经被建立了关联，所有东西都是响应式的

* 现在启动由 koa框架 和 koa-static中间件 搭建的静态web服务器

> node index.js

* 现在打开浏览器，在地址栏输入静态web服务器的地址 127.0.0.1:3000 ，可以看到页面显示

```
Hello ArthurSlog!
```

* 至此，我们使用 vue框架 实现了一个单页应用

* 下一节，会介绍 后端框架koa 搭配 前端框架vue，实现前后端的衔接

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
