# Slog73_ArthurSlog_Markdown编辑器！（项目上线之ArthurSlog个人网站上线5）

* ArthurSlog
* SLog-73
* Year·1

* Guangzhou·China
* September 15th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

一尺之棰 日取其半 万世不竭

---

### 开发环境MacOS(High Sierra 10.13.6 (17G65))

#### 需要的信息和信息源：

* [Markdown语法](https://en.wikipedia.org/wiki/Markdown)

* [Translation](https://en.wikipedia.org/wiki/Translation)

* [Compiler](https://zh.wikipedia.org/wiki/%E7%B7%A8%E8%AD%AF%E5%99%A8)

* [Markdown-it](https://www.npmjs.com/package/markdown-it)

* [contenteditable 属性](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Editable_content)

### 开始编码

* 本次来给[自己的网站 ArthurSlog.com](http://www.arthurslog.com)，增加一点新功能

* 这个功能就是 Markdown编辑器模块

* 简单点说，Markdwon文件 使用易读易写的纯文本格式编写文档，然后转换成有效的XHTML（或者HTML）文档

* 这个换装的过程就需要一个转换器，这里我们使用 Markdown-it，具体介绍 [在此](https://www.npmjs.com/package/markdown-it)

* 在这里选择下载markdown-it.js文件，在 html文件里直接引用

* 这里把html、css、js都一起写在一个文档里，简单直接一点

ClientFile: ArthurSlog.com/Markdown_Editor.html
``` html
<!DOCTYPE html>
<html lang="en">

<head>
    <title>ArthurSlog_MarkdownEditor</title>
    <meta charset="UTF-8">
    <script src="./markdown-it.js"></script>
</head>

<body>
    <div id="container">
        <!-- ArthurSlog_Manual_Area -->
        <div id="editorManual">
            <div id="editorManual_Title">ArthurSlog 创作中心</div>
            <div id="editorManual_Tool">工具栏（建设中...）</div>
        </div>
        <div id="editorContent">
            <!-- ArthurSlog_MarkdownEditor_Area -->
            <div id="sourceCode_Markdown" contenteditable="true"></div>

            <div id="middleLine"></div>
            <!-- ArthurSlog_MarkdownToHTML_AREA -->
            <div id="resultCode_HTML"></div>
        </div>
    </div>

    <script>
        // target.addEventListener(type, listener, options);
        // target.addEventListener(type, listener ,{capture: Boolean, passive: Boolean, once: Boolean});
        // target.addEventListener(type, listener, useCapture);
        // target.addEventListener(type, listener[, useCapture, wantsUntrusted  ]); 
        // ---
        // 1. target = document.getElementById("basic")
        // 2. type = 'input'
        // 3. listener = document.getElementById("resultHTML").innerHTML = window.markdownit().render(document.getElementById("basic").value)
        // 4. options = false
        // =>
        // 5. target.addEventListener(type, listener, options)
        document.getElementById("sourceCode_Markdown").addEventListener('input', function () { document.getElementById("resultCode_HTML").innerHTML = window.markdownit().render(document.getElementById("sourceCode_Markdown").innerText) }, false);
        //document.getElementById("sourceCode_Markdown").addEventListener('paste', function () { document.getElementById("sourceCode_Markdown").innerText = document.getElementById("sourceCode_Markdown").innerText.toString()}, false);
        document.getElementById("sourceCode_Markdown").style.boxShadow = "none";
        document.getElementById("sourceCode_Markdown").style.textShadow = "none";
        document.getElementById("sourceCode_Markdown").style.outlineColor = "none";
        document.getElementById("sourceCode_Markdown").style.outlineStyle = "none";
        document.getElementById("sourceCode_Markdown").style.outline = "none";
        document.getElementById("sourceCode_Markdown").style.borderColor = "none";
    </script>

    <style>
        html,
        body {
            height: 100%;
            display: block;
            overflow: hidden;
        }

        body {
            margin: 0;
            padding: 0;
        }

        #container {
            display: flex;
            flex-direction: column;
            position: absolute;
            margin: 0;
            padding: 0;
        }

        #EditorManual {
            display: flex;
            flex-direction: column;
            position: relative;
            margin-left: 0%;
            margin-right: 0%;
            height: 15vh;
        }

        #editorManual_Title {
            margin-left: 0%;
            margin-right: 0%;
            height: 10vh;
            background-color: ghostwhite;
        }

        #editorManual_Tool {
            margin-left: 0%;
            margin-right: 0%;
            height: 5vh;
            background-color: rgb(211, 250, 255);
        }

        #editorContent {
            display: flex;
            flex-direction: row;
            position: relative;
            margin: 0;
            padding: 0;
        }

        #sourceCode_Markdown {
            width: 47.5vw;
            height: 85vh;
            margin-left: 0%;
            margin-right: 0%;
            overflow: scroll;
            background-color: aliceblue;
            text-decoration:none;
        }

        #middleLine {
            width: 5vw;
            height: 85vh;
            overflow: hidden;
            background-color: ghostwhite;
        }

        #resultCode_HTML {
            width: 47.5vw;
            height: 85vh;
            margin-left: 0%;
            margin-right: 0%;
            overflow: scroll;
            background-color: ghostwhite;
        }
    </style>
</body>

</html>
```

* 这里有几个需要关键的地方：

1. 当div标签出现 contenteditable属性，且这个属性为“true”的时候，这个div 会变成可编辑状态，点击这里详细了解[contenteditable 属性](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Editable_content)

2. 根据Markdown-it的官方说明，使用 window.markdownit().render(document.getElementById("sourceCode_Markdown").innerText)把输入的文本转换为Html

3. 关闭输入div标签区域的边框效果：

ClientFile: ArthurSlog.com/Markdown_Editor.html(script)
``` js
document.getElementById("sourceCode_Markdown").style.boxShadow = "none";
document.getElementById("sourceCode_Markdown").style.textShadow = "none";
document.getElementById("sourceCode_Markdown").style.outlineColor = "none";
document.getElementById("sourceCode_Markdown").style.outlineStyle = "none";
document.getElementById("sourceCode_Markdown").style.outline = "none";
document.getElementById("sourceCode_Markdown").style.borderColor = "none";
```

4. 使用flex对页面进行布局

5. 调整html和body的样式，以达到覆盖整个页面的效果：

ClientFile: ArthurSlog.com/Markdown_Editor.html(style)
``` css
html,
body {
    height: 100%;
    display: block;
    overflow: hidden;
}

body {
    margin: 0;
    padding: 0;
}
```

* 完成了编辑，现在给首页加个链接先，直接跳转过去

ClientFile: ArthurSlog.com/index.html
``` html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>ArthurSlog</title>
        <link rel="stylesheet" type="text/css" href="style.css" >
    </head>
    <body>
        <p>个人技术分享</p>
        <div>
            <a href="./Markdown_Editor.html">ArthurSlog_MarkdownEditor</a>
        </div>
        <footer>
            <a href="http://www.miitbeian.gov.cn">粤ICP备18088522号-1</a>
        </footer>
    </body>
</html>
```

* 其中更新的部分是：

ClientFile: ArthurSlog.com/index.html
``` html
<div>
    <a href="./Markdown_Editor.html">ArthurSlog_MarkdownEditor</a>
</div>
```

* 编辑器还有一些问题，后续再继续更新优化

* 至此，ArthurSlog的网站又添加新模块----ArthurSlog_Markdown编辑器！。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢