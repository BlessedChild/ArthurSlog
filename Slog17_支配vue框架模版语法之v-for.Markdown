* ArthurSlog
* SLog-17
* Year·1

* Guangzhou·China
* July 19th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

实际上 结果是最重要的 根本没有人在乎你的过程 甚至根本就没有人在乎你 

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

v-for.html
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
            <div v-for="item in items">
            {{ item.text }}
            </div>
        </div>
        <script>
        new Vue({
            el: '#app',
            data: {
                items: [
                    {id: 0, text: 'Hello ArthurSlog~ id: 0' + '\n'},
                    {id: 1, text: 'Hello ArthurSlog~ id: 1' + '\n'},
                    {id: 2, text: 'Hello ArthurSlog~ id: 2' + '\n'}
                ]
            }
        })
        </script>
    </body>
</html>
```

* 现在你可以打开浏览器，在地址栏输入 127.0.0.1:3000/v-for.html，你会看到：

``` txt
Hello ArthurSlog~ id: 0
Hello ArthurSlog~ id: 1
Hello ArthurSlog~ id: 2
```

* 这里注意到，我们创建了一个对象 “items”，他是一个数组，里面存放了三个对象，每个对象拥有两个属性 “id” 和 “text”，他们的值都不一样：

``` js
items: [
    {id: 0, text: 'Hello ArthurSlog~ id: 0' + '\n'},
    {id: 1, text: 'Hello ArthurSlog~ id: 1' + '\n'},
    {id: 2, text: 'Hello ArthurSlog~ id: 2' + '\n'}
]
```

* 看到模版语法里， “item” 是一个临时的对象，这个名字随便定，只是临时使用的，“item in items” 这样的语法，意思就是在 “items” 这个对象中，按顺序一个一个取出里面的对象，然后，每一次取出对象的时候，打印出对象的 “text” 属性的值：

``` html
<div v-for="item in items">
{{ item.text }}
</div>
```

* 至此，我们把 vue模版指令 v-for 介绍了一遍，更多使用方法和信息，请参考 [vue官方手册](https://vuejs.org/v2/api/index.html#v-text)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
