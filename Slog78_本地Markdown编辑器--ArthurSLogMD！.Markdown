# Slog78_本地Markdown编辑器--ArthurSLogMD！

* ArthurSlog
* SLog-78
* Year·1

* Guangzhou·China
* September 19th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog.com](http://www.arthurslog.com)

* [MSDN: ArthurSlog](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub: BlessedChild](https://github.com/BlessedChild/ArthurSlog)

* [NPMJS.com: arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

不尚贤 使民不争 不贵难得之货 使民不为盗 不见可欲 使民心不乱 是以圣人之治 虚其心 实其腹 弱其志 强其骨 常使民无知无欲 使夫智者不敢为也 为无为 则无不治

---

### 开发环境MacOS(High Sierra 10.13.6 (17G65))

#### 需要的信息和信息源：

* [Electron](https://electronjs.org/docs)

* [本篇源文件Github地址](https://github.com/BlessedChild/ArthurSlogMarkdownEditor)

### 开始编码

* 本篇是把ArthurSlog.com网站上的Markdown编辑器本地化了

* 使用的是Electron，用HTML，CSS和JavaScript来构建跨平台桌面应用程序的一个开源库

* 目前已经完成基本功能

* 完整源码已上传至 Github： [https://github.com/BlessedChild/ArthurSlogMarkdownEditor](https://github.com/BlessedChild/ArthurSlogMarkdownEditor)

> git clone https://github.com/BlessedChild/ArthurSlogMarkdownEditor.git

> cd ArthurSlogMarkdownEditor

> sudo npm i --unsafe-perm=true

> sudo npm run start

* 启动rthurSlogMarkdownEditor

* 使用Markdown语法书写，测试成功！

* 对于electron来说，他主要是负责两件事情：

1. 使用nodejs负责操作系统与界面之间的交互，称为主函数

2. 调用浏览器渲染（例如V8、webkit、等）引擎负责界面的交互，成为渲染函数

* 顾名思义，主函数是一切的开始：

~/Desktop/ArthurSlogMarkdownEditor/main.js
``` js
const { app, BrowserWindow } = require('electron')

let win

function createWindow() {
    win = new BrowserWindow({
        width: 800,
        height: 600,

    })
    win.loadFile('index.html')

    //win.webContents.openDevTools()

    win.on('closed', () => {
        win = null
    })
}

app.on('ready', createWindow)

app.on('window-all-closed', () => {
    if (process.platform == 'darwin') {
        qpp.quit()
    }
})

app.on('activate', () => {
    if (win == null) {
        createWindow()
    }
})
```

* 具体函数的作用，下次再补充了，因为我现在还有更重要的事要去做

* 再来看一下配置文件 package.json:

~/Desktop/ArthurSlogMarkdownEditor/package.json
``` json
{
  "name": "ArthurSlogBrowser_Nodejs",
  "version": "0.0.1",
  "description": "This is a Browser by Nodejs",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "electron  ."
  },
  "keywords": [],
  "author": "ArthurSlog",
  "license": "ISC",
  "devDependencies": {
    "electron": "^2.0.9"
  },
  "dependencies": {
    "markdown-it": "^8.4.2"
  }
}
```

* 当然，界面文件index.html也需要更新一下：

``` html
<!DOCTYPE html>
<html lang="en">

<head>
    <title>ArthurSlogMD</title>
    <meta charset="UTF-8">
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
        require('markdown-it')
        const md = require('markdown-it')();

        document.getElementById("sourceCode_Markdown").addEventListener('input', function () {
            document.getElementById("resultCode_HTML").innerHTML = md.render(document.getElementById("sourceCode_Markdown").innerText)
        }, false);
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
        //document.getElementById("sourceCode_Markdown").addEventListener('input', function () { document.getElementById("resultCode_HTML").innerHTML = window.markdownit().render(document.getElementById("sourceCode_Markdown").innerText) }, false);
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

* ok，文件结构比较简单，后面在来构建指定平台的可执行文件

* 至此，ArthurSLogMarkdownEditor编辑器本地化第一阶段 GET！。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
