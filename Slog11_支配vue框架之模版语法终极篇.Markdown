* ArthurSlog
* SLog-11
* Year·1

* Guangzhou·China
* July 17th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

一个瘦小的男孩 从小失去父母 但一只小鸟每天在他窗前说 你是世上最高大威猛的男人 男孩长大后 真的成了小鸟所说的高大威猛的人 当上将军拯救了国家

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

* 在当前路径下，编写 v-text.html 文件 ：

v-text.html
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
        <span v-text="message"></span>

        <!-- v-text="message" 等同于 {{message}} -->
        <span>{{message}}</span>
    </div>

    <script>
        new Vue({
            el: '#app',
            data: {
                message: 'Hello ArthurSlog! \n' //噢～这里换行符 “\n” 无效
            }
        })
    </script>

</body>

</html>
```
* 此时，在此路径下执行

> node index.js

* 记得，现在开始不要终止 index.js 程序，因为后面会一直需要这个到这个 静态web服务器

* 现在你可以打开浏览器，在地址栏输入 127.0.0.1:3000/v-text.html，你会看到没有换行，这是因为，message 的值被执行为 txt格式了，也就是无格式的字符串

* Ok，下一个，在当前路径下，编写 v-html.html 文件 ：

v-html.html
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

* 之前的 静态web服务器 已经启动了，所以这里就不用再启动一次了

* 现在你可以打开浏览器，在地址栏输入 127.0.0.1:3000/v-html.html，你会看到：使用了v-html 的，会把rawHtml的值进行 html 格式解析

* Ok，下一个，在当前路径下，编写 v-show.html 文件 ：

v-show.html
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
            <h1 v-show="ok">Hello ArthurSlog, "ok" is true and "no" is false</h1>
            <h1 v-show="no">Hello ArthurSlog, "no" is false</h1>
        </div>
        <script>
        new Vue({
            el: '#app',
            data: {
                ok: true,
                no: false
            }
        })
        </script>
    </body>
</html>
```

* 现在你可以打开浏览器，在地址栏输入 127.0.0.1:3000/v-show.html，你会看到：“ok” 的值与 “show” 相关联，当 “ok”的值 等于 “true” 时，“show” 的值也就等于 “true”，所以文字会显示出来；当 “no” 的值与 “show” 相关联，当 “no”的值 等于 “false” 时，“show” 的值也就等于 “false”，所以文字不会显示出来

* Ok，下一个，在当前路径下，编写 v-if.html 文件 ：

v-if.html
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
            <h1 v-if="state1 === state2">Hello ArthurSlog, "state1" === "state2"</h1>
            <h1 v-if="state2 !== state2">Hello ArthurSlog, "state1" !== "state2"</h1>
        </div>
        <script>
        new Vue({
            el: '#app',
            data: {
                state1: 'ok',
                state2: 'ok'
            }
        })
        </script>
    </body>
</html>
```

* 现在你可以打开浏览器，在地址栏输入 127.0.0.1:3000/v-if.html，你会看到：Hello ArthurSlog, "state1" === "state2"，因为此时 state1 的值与 state2 的值相等，判断为 true，所以会显示出第一条字符串

* Ok，下一个，在当前路径下，编写 v-else.html 文件 ：

v-else.html
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
            <h1 v-if="state1 === state2">Hello ArthurSlog, "state1" === "state2"</h1>
            <h1 v-else>Hello ArthurSlog, "state1" !== "state2"</h1>
        </div>
        <script>
        new Vue({
            el: '#app',
            data: {
                state1: 'ok',
                state2: 'no'
            }
        })
        </script>
    </body>
</html>
```

* 现在你可以打开浏览器，在地址栏输入 127.0.0.1:3000/v-else.html，你会看到：Hello ArthurSlog, "state1" !== "state2"，因为此时 state1 的值与 state2 的值不相等，判断为 false，所以会显示出第二条字符串

* Ok，下一个，在当前路径下，编写 v-else-if.html 文件 ：

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

* Ok，下一个，在当前路径下，编写 v-for.html 文件 ：

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

* Ok，下一个，在当前路径下，编写 v-on.html 文件 ：

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

* Ok，下一个，在当前路径下，编写 v-bind.html 文件 ：

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

* Ok，下一个，在当前路径下，编写 v-model.html 文件 ：

v-model.html
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
            <input v-model="message" placeholder="edit me">
            <p>Message is: {{ message }}</p>
            <br>
            
            <span>Multiline message is:</span>
            <p style="white-space: pre-line;">{{ msg }}</p>
            <br>
            <textarea v-model="msg" placeholder="add multiple lines"></textarea>
        </div>

        <script>
        new Vue({
            el: '#app',
            data: {
                message: '',
                msg: ''
            }
        })
        </script>
    </body>
</html>
```

* 打开浏览器，地址栏输入 127.0.0.1:3000/v-model.html， v-model 指令在 表单输入 和 textarea元素 上创建双向数据绑定。它会根据输入类型自动选择更新元素的正确方法。虽然有点神奇，但v-model实质上是用于更新用户输入事件数据的 语法糖(就是把多个操作连接成一个操作)，更多信息参考 [vue官方手册](https://vuejs.org/v2/guide/forms.html#Basic-Usage)

* Ok，下一个，在当前路径下，编写 v-pre.html 文件 ：

v-pre.html
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
            <span v-pre>{{msg}}</span>
        </div>

        <script>
        new Vue({
            el: '#app',
            data: {
                msg: 'this will not be compiled'
            }
        })
        </script>
    </body>
</html>
```

* 打开浏览器，地址栏输入 127.0.0.1:3000/v-pre.html，显示

```txt
{{msg}}
```

* v-pre 指令会跳过此元素及其所有子元素的编译，把标签里的数据都按普通文本解析

* Ok，下一个，在当前路径下，编写 v-cloak.html 文件 ：

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

* Ok，最后一个，在当前路径下，编写 v-once.html 文件 ：

v-once.html
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
            <p v-once>The button above has been clicked {{ counter }} times.</p>
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

* 我们引用上面的代码，在标签 < p > 里使用 v-once 指令，打开浏览器，地址栏输入 127.0.0.1:3000/v-once.html，然后你点击 “Add 1” 按钮，你会发现文本不会再变化了，这是因为 once 仅渲染元素和组件一次。在随后的重新渲染中，元素/组件及其所有子元素将被视为静态内容并被跳过，这是用来用于优化更新性能的

* 至此，我们把当前的13个 vue模版指令 介绍了一遍，更多使用方法和信息，请参考 [vue官方手册](https://vuejs.org/v2/api/index.html#v-text)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
