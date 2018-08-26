* ArthurSlog
* SLog-16
* Year·1

* Guangzhou·China
* July 19th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

你选择自己喜欢的 可能会在经济上一开始更艰难 你可以选择平坦的路 一开始走着很舒心 你也可以在在途中 选择一条崎岖的路 感受下生命的另一种色彩 这条崎岖的路可能让你看不到尽头 而且越走越泥泞 但我敢保证一点的是 当你真的坚持走下去看到路开始平坦的时候 你会无比的幸福 并且有成就感

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

v-else-if.html
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
            <div v-if="type === 'A'">
            Hello ArthurSlog, the type is A
            </div>
            <div v-else-if="type === 'B'">
            Hello ArthurSlog, the type is B
            </div>
            <div v-else-if="type === 'C'">
            Hello ArthurSlog, the type is C
            </div>
            <div v-else>
            Hello ArthurSlog, the type is Not A/B/C
            </div>
        </div>
        <script>
        new Vue({
            el: '#app',
            data: {
                type: 'B'
            }
        })
        </script>
    </body>
</html>
```

* 现在你可以打开浏览器，在地址栏输入 127.0.0.1:3000/v-else-if.html，你会看到：Hello ArthurSlog, the type is B，因为此时 type 的值等于 B，判断的流程：一开始 if 判断 type 的值是否为A，不是，所以继续往下执行，来到 else-if，判断 tyoe 的值是否为 B，是，所以显示出 Hello ArthurSlog, the type is B

* 至此，我们把 vue模版指令 v-else-if 介绍了一遍，更多使用方法和信息，请参考 [vue官方手册](https://vuejs.org/v2/api/index.html#v-text)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
