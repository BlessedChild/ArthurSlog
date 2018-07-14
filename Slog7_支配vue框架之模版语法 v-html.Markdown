* ArthurSlog
* SLog-7
* Year·1

* Guangzhou·China
* July 14th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

去往目的地的列车可能会晚点 但绝不会缺席

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息：

* [vue模板语法官方手册](https://cn.vuejs.org/v2/guide/syntax.html)

* 我的上一篇文章：[使用vue前端框架实现单页应用（SPA）](https://juejin.im/post/5b4799435188251aca1e23d0)

#### 开始编码：

* 切换至桌面路径

> cd ~/Desktop

* 创建一个新文件夹

> mkdir node_vue_TemplateSyntax_learningload

* 切换至新建的文件夹路径下

> cd node_vue_TemplateSyntax_learningload

* 使用npm指令初始化nodejs项目环境，一路回车，完成初始化

> npm init

* 安装 koa 和 kao-static

> sudo npm install koa koa-static

* 需要管理员权限，输入密码

* 在当前路径下创建 index.js 和 index.html 这两个文件，其中 index.js 实现了一个静态web服务器：

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
        <div id="app">
        <p>Hello  {{ rawHtml }}                  </p>
        <p>Hello  <span v-html="rawHtml"></span> </p>
        </div>
        <script>
        new Vue({
            el: '#app',
            data: {
                rawHtml: '<span style="color:red">ArthurSlog</span>'
            }
        })
        </script>
    </body>
</html>
```

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

* 现在，切换至 ~/Desktop/node_vue_TemplateSyntax_learningload 路径下

> cd ~/Desktop/node_vue_TemplateSyntax_learningload

* 启动静态web服务器

> node index.js

* 打开浏览器，地址栏输入 127.0.0.1:3000， 回车，正常执行会有以下结果：

``` 
Hello <span style="color:red">ArthurSlog</span>

Hello ArthurSlog
```

##### 请注意到 

index.html
``` html
<p>Hello  {{ rawHtml }}                  </p>
<p>Hello  <span v-html="rawHtml"></span> </p>
```

index.js
``` js
        <script>
        new Vue({
            el: '#app',
            data: {
                rawHtml: '<span style="color:red">ArthurSlog</span>'
            }
        })
        </script>
```

##### index.html 里使用了 v-html 指令，把 index.js 里的 rawHtml 作为 html 格式

index.html
``` html
<p>Hello  <span v-html="rawHtml"></span> </p>
```

index.js
``` js
data: {
    rawHtml: '<span style="color:red">ArthurSlog</span>'
}
```

##### 另一个没有使用 v-html 指令，而用 {{}}（无逻辑模板） 的，会解释为给定的值

index.html
``` html
<p>Hello  {{ rawHtml }}                  </p>
```

index.js
``` js
data: {
    rawHtml: '<span style="color:red">ArthurSlog</span>'
}
```

* 上面要说的，就是，当你使用 v-html 指令的时候，可以把给定的值按照 html格式 解析，使用方法是：

##### 首先，先把你想执行的 html格式的内容 赋予变量 rawhtml：

``` html
rwahtml: '<span style="color:red">ArthurSlog</span>'
```

##### 其次，把你的 html标签 提取出来，这里的 html标签 指的是 \<span>\</span>：

``` html
<span></span>
```

##### 然后，给标签上 解析指令 v-html：

``` html
<span v-html></span>
```

##### 最后，把变量 rawhtml 赋值给 v-html 指令，rawhtml 要加上双引号 “rawhtml”：

``` html
<span v-html="rawHtml"></span>
```

* 至此，我们了解了 vue框架 的模版语法中 v-html 指令的使用。

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
