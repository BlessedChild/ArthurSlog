* ArthurSlog
* SLog-10
* Year·1

* Guangzhou·China
* July 15th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

生活在99%以上的信息不是真实的世界 生活中99%以上的信息指向了剩下的信息不是真实的 

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 课前预习

* 本篇是 《支配vue框架系列》的第二篇

* 这里提醒一下大家，请一定要参考官方文档，官方的母语版本！！！看中文翻译容易被误导，为什么呢？人的水平参差不齐，比如 attributes 这个单词，有的翻译成属性？有的翻译成特性？人为的制造混乱。所以坚决坚持，只看原版的官方文档！除非作者就是中文的大家！

* 时间是有限的，技术更新是快速的，请迈开脚步 一昧的等待，等来的是被淘汰

* 上一篇，讲到了 v-html，vue的模版语法，用来干什么的？就是让他 vue 实例的数据可以和 DOM(Document Object Model) 进行数据绑定。什么是 DOM ？在比较靠谱的[w3cschool](https://www.w3schools.com/js/js_htmldom.asp)里，是这么解释 DOM 的:

``` txt
“HTML DOM” is a standard. 

With the "HTML DOM", JavaScript can access and change all the elements of an HTML document.
```

##### 本篇讲的是 “HTML DOM”， 而 ”DOM“ 指代的范围就比较广了，更多信息请参考[w3cschool](https://www.w3schools.com/js/js_htmldom.asp)

* 上面简单扼要的说了 ”HTML DOM“ 能做什么：有了 ”HTML DOM“， javascript 可以访问和改变 HTML文件 的 elements(elements指的就是 \<body> \<html> 对象) ，当然了，对象就会有 attributes 和 values 等，举个栗子：

``` txt
<body id="b1"></body> //这里 id 就是 <body> 的 attributes

<div> Hello ArthurSlog</div>  //这里 "Hello ArthurSlog" 就是 <div> 的 values，String格式的值
```

* 还要注意的地方是，“HTML DOM” 里的 elements 的值是我们可以控制的，这也就是 javascript 和 vue（vue也是javacript）的本职工作！而 attributes 是标准，是要查询标准文档的，[HTML Attributes](https://www.w3schools.com/tags/ref_attributes.asp) 与 elements相关联，举个栗子：

Attribute| Belongs to| Description
- | - | - 
accept|	\<input>|	Specifies the types of files that the server accepts (only for type="file")
accept-charset|	\<form>|	Specifies the character encodings that are to be used for the form submission
...| ...| ...

* 其中，包含有 [全局的Attribute](https://www.w3schools.com/tags/ref_standardattributes.asp)（可以直接访问到的 Attribute）:

Attribute| Description
- | -
accesskey| Specifies a shortcut key to activate/focus an element
class| Specifies one or more classnames for an element (refers to a class in a style sheet)

* 小结一下：”HTML DOM“ 如下所说的：

``` txt
In other words: The "HTML DOM" is a standard for how to get, change, add, or delete HTML elements.
```

##### 学会用英文去理解，触碰最本质的信息

#### 需要的信息和信息源：

* [vue框架模版语法](https://cn.vuejs.org/v2/guide/syntax.html#%E7%89%B9%E6%80%A7)(Template Syntax)

* [vue.js API](https://vuejs.org/v2/guide/syntax.html)(https://vuejs.org/v2/api/index.html)

* [W3CSchool HTML DOM手册](https://www.w3schools.com/js/js_htmldom.asp)

* [W3CSchool HTML Attributes Reference手册](https://www.w3schools.com/tags/ref_attributes.asp)

* [W3CSchool HTML Tags](https://www.w3schools.com/tags/tag_comment.asp)

* [Koa官方手册](https://koajs.cn/)

* [Koa-static](https://github.com/koajs/static)



### 开始编码：

* 切换至桌面路径

> cd ~/Desktop

* 创建一个新文件夹

> mkdir node_vue_TemplateSyntax_v-bind_learningload

* 切换至新建的文件夹路径下

> cd node_vue_TemplateSyntax_v-bind_learningload

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

* 现在，切换至 ~/Desktop/node_vue_TemplateSyntax_v-bind_learningload 路径下

> cd ~/Desktop/node_vue_TemplateSyntax_v-bind_learningload

* 启动静态web服务器

> node index.js

* 打开浏览器，地址栏输入 127.0.0.1:3000， 回车，正常执行会出来一个button，但是这个button无法接受点击

* 因为，在 index.html 里我们使用 vue.js模版语法，其中用到了 v-bind：

index.html
``` html
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
```

* 关键点在：

index.html
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

index.html
``` html
<button v-bind:disabled="Output">Hello ArthurSlog</button>
```

* 这下我们可以通过 javascript，控制 “Output” 的值，进而控制 button 的 Attributes--“disabled”，“disabled” 的值，进而影响了 button 是否接受点击

index.html
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

* 关键的地方在于，在 HTML 中，elements（元素，指\<button>，\<textarea>，\<input> 等等）的 Attribute，具体参考[HTML Attribute Reference](https://www.w3schools.com/tags/ref_attributes.asp)

* 现在，把 script 里，"Output" 的值改为 false：

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

* 现在，切换至 ~/Desktop/node_vue_TemplateSyntax_v-bind_learningload 路径下

> cd ~/Desktop/node_vue_TemplateSyntax_v-bind_learningload

* 启动静态web服务器

> node index.js

* 打开浏览器，地址栏输入 127.0.0.1:3000， 回车，正常执行会出来一个button，但是这个button已经可以接受点击了

* 至此，我们了解了 vue框架 的模版语法中 v-bind 指令的使用，v-bind的其他用法参考 [vue官方API文档](https://vuejs.org/v2/api/index.html#v-bind)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
