* ArthurSlog
* SLog-18
* Year·1

* Guangzhou·China
* July 19th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

为什么要在一线城市，因为一切的舒适终将会被打破，因为新一代的人最不怕的就是学习和接受新的事物，旧的事物将会成为历史，也必将被新的所取代

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

v-on.html
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
            <button v-on:click="counter += 1">Add 1</button>
            <p>The button above has been clicked {{ counter }} times.</p>
        </div>
        <script>
        new Vue({
            el: '#app',
            data: {
                counter: 0
            }
        })
        </script>
    </body>
</html>
```

* 现在你可以打开浏览器，在地址栏输入 127.0.0.1:3000/v-on.html，你会看到，按钮“Add 1”，和文本 “The button above has been clicked 0 times.”：

``` txt
Add 1

The button above has been clicked 0 times.
```

* 当你点击按钮的时候，每点击以下，文本的 “0 time” 的 “0” 值就会增加1

* 在这里，我们创建了一个对象 “counter”，给了初始值为 “0”，可以看到 v-on 指令与 “click” 按钮的点击事件，注意这里是“按钮”的“事件”，而 “counter + 1” 被当作了javascript解析执行了！所以，每点击一次，就触发一次 “click” 事件，就会执行一次 “counter + 1”，所以 文本 “The button above has been clicked {{ counter }} times.” 里的 “{{ counter }}” 的值页跟着发生改变

* 至此，我们把 vue模版指令 v-on 介绍了一遍，更多使用方法和信息，请参考 [vue官方手册](https://vuejs.org/v2/api/index.html#v-text)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
