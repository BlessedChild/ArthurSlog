* ArthurSlog
* SLog-22
* Year·1

* Guangzhou·China
* July 21th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

公平是弱者的安慰剂 竞争是强者的试金石

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

v-cloak.html
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
            <div v-cloak>{{ msg }}</div>
        </div>
        <br>
        <button onclick="loadmsg()">Load msg</button>

        <script>
            function loadmsg () {
                new Vue({
                    el: '#app',
                    data: {
                        msg: 'Hello ArthurSlog'
                    }
                })
            }
        </script>

        <style>
            [v-cloak]{ display:none; }
        </style>
    </body>
</html>
```

* 打开浏览器，地址栏输入 127.0.0.1:3000/v-cloak.html，文本 “Hello ArthurSlog” 没有显示，只有显示一个 按钮 “load msg”，按钮的 “click” 事件 和 "loadmsg()" 方法相关联，而 “loadmsg()” 方法里包含了 “vue对象的实例化”，

``` js
function loadmsg () {
    new Vue({
        el: '#app',
        data: {
            msg: 'Hello ArthurSlog'
        }
    })
}
```

* 另一方面，在样式文件里，添加了：

``` css
[v-cloak]{ display:none; }
```

* 现在点击按钮，文本 “Hello ArthurSlog” 显示出来，此时按钮 “load msg” 响应了 “click” 事件，“click” 事件调用了 “loadmsg()” 方法，“loadmsg” 方法 执行了 “vue对象的实例化”，关键点在于：v-cloak 指令让指定的 元素 和 元素的子元素 在“vue对象的实例化” 之前处于隐藏状态，当 “vue对象的实例化” 完成后，才会显示出来 

* 至此，我们把 vue模版指令 v-cloak 介绍了一遍，更多使用方法和信息，请参考 [vue官方手册](https://vuejs.org/v2/api/index.html#v-text)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
