# Slog75_升级ArthurSlog_Markdown编辑器！（项目上线之ArthurSlog个人网站上线6）

* ArthurSlog
* SLog-75
* Year·1

* Guangzhou·China
* September 16th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

将欲取之 必先与之 是谓微明 柔弱胜刚强

---

### 开发环境MacOS(High Sierra 10.13.6 (17G65))

#### 需要的信息和信息源：

* [Markdown语法](https://en.wikipedia.org/wiki/Markdown)

* [Translation](https://en.wikipedia.org/wiki/Translation)

* [Compiler](https://zh.wikipedia.org/wiki/%E7%B7%A8%E8%AD%AF%E5%99%A8)

* [Markdown-it](https://www.npmjs.com/package/markdown-it)

* [contenteditable 属性](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Editable_content)

### 开始编码

* 本次来给[自己的网站 ArthurSlog.com](http://www.arthurslog.com)的 Markdown编辑器进行一次更新

* 更新内容：

1. UI和布局

2. 编辑内容缩进

3. 调整背景色

* 下面上代码：

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
            <div id="editorManual_Title">
                <p id="editorManual_Title_Arthur">Arthur</p>
                <p id="editorManual_Title_Slog">Slog</p>
                <p id="editorManual_Title_createCenter">创作中心</p>
            </div>
            <div id="editorManual_middleLine"></div>
            <div id="editorManual_Tool">
                <p>building...</p>
            </div>
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
            position: absolute;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
            margin: auto;

            max-width: 100%;
            max-height: 100%;
            overflow: hidden;
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
            position: absolute;
            margin: 0;
            height: 15vh;
        }

        #editorManual_Title {
            margin-left: 0%;
            margin-right: 0%;
            height: 9.5vh;
            display: flex;
            flex-direction: row;
        }

        #editorManual_Title_Arthur {
            font-size: 28px;
            font-style: italic;
            color: rgb(255, 0, 0);
            font-weight: 800;
            position: absolute;
            margin: 0;
            top: calc(4%);
            padding-left: 56px;
        }

        #editorManual_Title_Slog {
            font-size: 28px;
            font-style: italic;
            color: rgb(17, 1, 1);
            font-weight: 800;
            position: absolute;
            margin: 0;
            top: calc(4%);
            padding-left: 138px;
        }

        #editorManual_Title_createCenter {
            font-size: 22px;
            font-style: normal;
            font-weight: 300;
            color: rgb(114, 123, 128);
            position: absolute;
            margin: 0;
            top: calc(4% + 6px);
            padding-left: 208px;
        }

        #editorManual_middleLine {
            margin: 0;
            padding: 0;
            height: 0.5vh;
            background-color: rgba(241, 248, 255, 0.966);
        }

        #editorManual_Tool {
            margin-left: 0%;
            margin-right: 0%;
            height: 5vh;
        }

        #editorManual_Tool>p {
            font-size: 16px;
            font-style: italic;
            position: relative;
            top: calc(100% - 20px);
            margin: 0;
            padding-left: 56px;
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
            background-color: rgba(199, 206, 212, 0.678);
            text-decoration: none;
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

* 我的网站已经同步更新，传送门：[ArthurSlog.com](http://www.arthurslog.com)

* 网站的源码已同步至 [Github](https://github.com/BlessedChild/ArthurSlog.com)

* 思考了一下，首先是网站的受众会采用哪些设备？

* 考虑了一下，用手机打开浏览器还要搜索，步骤太多了，不符合大部分人的使用习惯

* 那么就暂时先只考虑适配pc端，不考虑移动端的

* 下一步，移动端的考虑微信小程序或者app吧

* 至此，ArthurSlog.com ---- ArthurSlog_Markdown编辑器更新 Get！。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢