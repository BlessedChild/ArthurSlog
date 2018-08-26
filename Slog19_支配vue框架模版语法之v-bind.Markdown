* ArthurSlog
* SLog-19
* Year·1

* Guangzhou·China
* July 21th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

不管你接不接受 意外总会发生 人生就是由各种各样的意外组成 重要的是 你的那颗炙热的心是否还在燃烧

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* 本文的所有[源码地址](https://github.com/BlessedChild/node_vue_directive_learningload)

* vue.js 的[模版指令（directive）](https://vuejs.org/v2/api/index.html#v-text)，当前（2018/7/17）一共有 13 个，分别是：

1. v-text

2. v-html

3. v-show

4. v-if

5. v-else

6. v-else-if

7. v-for

8. v-on

9. v-bind

10. v-model

11. v-pre

12. v-cload

13. v-once

* vue.js 的模版指令，与编程语言的 “关键字” 或者 “保留字” 有点相似，例如 if（判断语句关键字）、for（循环语句关键字）

### 开始编码

* 首先，搭起静态服务器，先切换至桌面路径

> cd ~/Desktop

* 创建一个文件夹node_vue_directive_learningload

> mkdir node_vue_directive_learningload

* 切换路径到新建的文件夹下

> cd node_vue_directive_learningload

* 使用npm初始化node环境，一路enter键完成初始化

> npm init

* 使用npm安装koa和koa-static

> sudo npm install koa koa-static

* 参考[Koa-static说明手册](https://github.com/koajs/static)，我们在当前路径下编写index.js和index.html两份文件

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
    <title>ArthurSlog</title>
</head>

<body>

    <h1>The static web server by ArthurSlog</h1>

</body>

</html>
```

* 接下来，我们来根据使用场景，来编写 vue.js 模版指令代码

v-bind.html
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
        <button v-bind:disabled="Output">Hello ArthurSlog</button>
        </div>

        <script>
        new Vue({
            el: '#app',
            data: {
                Output: true
            }
        })
        </script>
    </body>
</html>
```

* 现在你可以打开浏览器，在地址栏输入 127.0.0.1:3000/v-bind.html，正常执行会出来一个button，但是这个button无法接受点击

* 关键点在：

v-bind.html
``` html
<button v-bind:disabled="Output">Hello ArthurSlog</button>

<script>
new Vue({
    el: '#app',
    data: {
        Output: true
    }
})
</script>
```

* 看到 button 的 Attributes--“disabled”，“disabled” 与 “Output” 相关联了

v-bind.html
``` html
<button v-bind:disabled="Output">Hello ArthurSlog</button>
```

* 这下我们可以通过 javascript，控制 “Output” 的值，进而控制 button 的 Attributes--“disabled”，“disabled” 的值，进而影响了 button 是否接受点击

v-bind.html
``` html
<script>
new Vue({
    el: '#app',
    data: {
        Output: true
    }
})
</script>
```

* 关键的地方在于，在 HTML 中，elements（元素，指< button >，< textarea >，< input > 等等）的 Attribute，具体参考[HTML Attribute Reference](https://www.w3schools.com/tags/ref_attributes.asp)

* 现在，把 script 里，"Output" 的值改为 false：

v-bind.html
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
            <button v-bind:disabled="Output">Hello ArthurSlog</button>
        </div>

        <script>
        new Vue({
            el: '#app',
            data: {
                Output: false
            }
        })
        </script>
    </body>
</html>
```

* 打开浏览器，地址栏输入 127.0.0.1:3000/v-bind.html， 回车，正常执行会出来一个button，但是这个button已经可以接受点击了

* 至此，我们把 vue模版指令 v-bind 介绍了一遍，更多使用方法和信息，请参考 [vue官方手册](https://vuejs.org/v2/api/index.html#v-text)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
