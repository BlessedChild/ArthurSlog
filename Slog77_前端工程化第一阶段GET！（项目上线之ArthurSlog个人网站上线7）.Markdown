# Slog77_前端工程化第一阶段GET！（项目上线之ArthurSlog个人网站上线7）

* ArthurSlog
* SLog-77
* Year·1

* Guangzhou·China
* September 18th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog.com](http://www.arthurslog.com)

* [GitHub: BlessedChild](https://github.com/BlessedChild/ArthurSlog)

* [NPMJS.com: arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

企者不立 跨者不行 自见者不明 自是者不彰 自伐者无功 自矜者不长

---

### 开发环境MacOS(High Sierra 10.13.6 (17G65))

#### 需要的信息和信息源：

* [Webpack](https://webpack.js.org/)

* [Sass](https://sass-lang.com/)

* [Translation](https://en.wikipedia.org/wiki/Translation)

* [Compiler](https://zh.wikipedia.org/wiki/%E7%B7%A8%E8%AD%AF%E5%99%A8)

### 开始编码

* 上一次对页面做了布局，但是编码起来比较“硬”

* 不够严谨和简洁

* 可以采用css预编译（preprocessor）的方式来解决

* 这里需要到两个东西：

1. 文件打包工具，简单点说，有点像Makefile/make 的作用一样，指导文件如何去组合

2. css预编译器（preprocessor），用在打包的过程中

* 关于css预编译器的承担的角色，举个栗子：

``` txt
1. 提高代码可读性，帮你添加css浏览器条件前缀
比如，你写了如下的代码

你写的代码：
:fullscreen{

}

经过css预编译器（preprocessor）编译之后的代码：
:-webkit-:full-screen {
}
:-moz-:full-screen {
}
:full-screen {
}
   
2. 使用最新的标准语法，或者其他语法，把向下兼容的问题交给css预编译器（preprocessor）解决
   比如可以用函数，对象的语法来编辑设计你的布局
   简单点说，就是不去管协议的变化或者浏览器间的不同，你就只管写（你就只管学习），css预编译器（preprocessor）（你的爸妈）
   会用现有的方法去达到新标准的要求（会想办法给你提供一个要啥有啥的学习环境）

3. 自动帮你命名标签（id或者class的值）

4. 一些实用的 “语法糖”（语法糖可以理解为高级的封装，比如你想和咖啡的时候，只要向服务员传递一个你想要的口味，然后
   等服务员帮你把咖啡递过来就行了；而不用你自己去采摘咖啡豆，烘烤咖啡豆，研磨咖啡豆，冲调，装盘，运送等）
```

* 目前比较主流的css预编译器（preprocessor）有 Sass、Less、PostCSS、Stylus 等....

* 而打包工具有 webpack、Parcel、Gulp、Grunt、Babel（一些既能编译、又能打包）

* 废话一下，Babel使用比较广泛，主要是可以使用他来对js版本进行转换

* 还有再废话一下，以上这些“工具”都有js（nodejs）实现

* 我选择预编译器Sass和打包工具webpack来构造我的网站 [ArthurSlog.com](http://www.arthurslog.com)

* 一开始使用，可能会比较繁琐

* 无所谓

* 继续

* 使用Sass的文章，在我之前的一篇文章中有所提及

* 简单点说，就是你要使用新的语法写一个样式文件，然后使用Sass去处理这个文件，转换成标准的css文件

* 而 webpack，我应该也是有写过一篇文章介绍过的

* 简单点说，就是帮你去调用Sass去处理你的那个新的样式文件，然后把转换而成的标准的css文件和

* html文件等所有资源打包成你想要的样子（一般是会打包成 一个html文件 + 资源文件）

* css预编译器（preprocessor）如果自动帮你命名的时候，html文件里的id和class也必须同步更新，以相互关联起来

* 这部分是webpack来做的，我们需要写一个配置文件，来指导webpack如何去做

* 这里是Sass官方使用手册，https://sass-lang.com/guide

* 这里是webpack官方使用手册，https://webpack.js.org/guides/

* 参考着来

* 先来进入我的网站源码路径下

> cd ~/Desktop/ArthurSlogWebsize

* 先来安装 webpack打包工具

> sudo npm i webpack webpack-cli --save-dev

* 现在，webpack就被安装到 当前路径/node_modules/.bin/webpack下了

* 现在查询webpack的版本

> ./node_modules/.bin/webpack -v

* 结果如下：

``` txt
4.19.0
```

* 每次都要./node_modules/.bin/webpack比较麻烦，我们来配置一下package.json文件（也就是npm环境配置文件）

> sudo vim package.json

* 更新代码：

~/Desktop/ArthurSlogWebsize/package.json
``` json
{                                                                                         
    "name": "nodeserver",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "dependencies": {
    "koa": "^2.5.2",
    "koa-static": "^5.0.0"
    },
    "devDependencies": {
        "webpack": "^4.19.0",
        "webpack-cli": "^3.1.0"
    },
    "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "./node_modules/.bin/webpack -v"
    },
    "repository": {
    "type": "git",
    "url": "git+https://github.com/BlessedChild/ArthurSlog.com.git"
    },
    "author": "ArthurSlog",
    "license": "ISC",
    "bugs": {
    "url": "https://github.com/BlessedChild/ArthurSlog.com/issues"
    },
    "homepage": "https://github.com/BlessedChild/ArthurSlog.com#readme"
}
```

* 更新了 15、16行

* 保存文件，退出vim编辑器

> :wq

* 尝试一下npm命令

> npm run start

* 你会得到

``` txt
> nodeserver@1.0.0 start /Users/kingarthur/Desktop/ArthurSlogWebsize
> webpack -v

4.19.0
```

* 漂亮，差不多了，现在，我希望webpack能按照我的指示去做事，所以要给webpack一个配置文件（指导文件）

* 在当前路径下：

~/Desktop/ArthurSlogWebsize/webpack.config.js
``` js
const path = require('path');                                                             

    module.exports = {
    // 入口点：准备进行转换的源代码的路径
    entry: './src/index.js',

    // 输出点：用来存放转换好的文件的路径
    output: {
        filename: 'main.js',
        path: path.resolve(__dirname, 'dist')
    }
};
```

* 对 webpack进行配置，指导webpack去获取./src/index.js 进行转换

* 然后转换好的文件命名为main.js，并存放在 当前路径/dist 下

* So，调整一下文件结构，该新建文件夹的新建，该移动的移动

> mkdir src dist server client

> mv index.js /server

> mv *.js *.html *.css *.json *.md *.jpg /client

> sudo mv src/ dist/ /client

> sudo rm -rf node_modules

> cd client

> sudo rm -rf package.json package-lock.json

> sudo npm init -y

> sudo npm i --save-dev webpack webpack-cli

> sudo vim package.json

* 更新 package.json文件 如下：

~/Desktop/ArthurSlogWebsize/client/package.json
``` json
{
  "name": "client",
  "version": "1.0.0",
  "description": "## OS Environment: Cent OS 7.0+",
  "private": true,
  "scripts": {
    "build": "./node_modules/.bin/webpack --config webpack.config.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^4.19.0",
    "webpack-cli": "^3.1.0"
  }
}
```

> mv Markdown_Editor.html index.html style.css background.jpg markdown-it.js dist

> cd ../server

> sudo npm init -y

> sudo npm i koa koa-static

> sudo vim index.js

* 更新一下 index.js文件：

~/Desktop/ArthurSlogWebsize/server/index.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();

// $ GET /package.json
app.use(serve('../client/dist'));

app.listen(80);

console.log('listening on port 80');
```

* ok，文件结构的调整告一段落了

* 在本机上测试服务器通过，记得需要修改一下端口号，不要是80

* 提交服务器的时候需要改成80端口

* 因为主页没有js脚本，所以直接使用webpack会打包一个奇怪的文件出来

* 我来写一个简单的脚本好了

~/Desktop/ArthurSlogWebsize/client/src/index.js
``` js
document.getElementById("myheand").addEventListener('click', function(){document.getElementById("myheand").innerText = "V0.0.1"})    
```

* ok，为了测试，现在需要更新一下主页文件 dist/index.html

~/Desktop/ArthurSlogWebsize/client/dist/index.html
``` html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>ArthurSlog</title>
        <link rel="stylesheet" type="text/css" href="style.css" >

    </head>
    <body>
        <p id="myheand">个人技术分享</p>
        <div>
            <a href="./Markdown_Editor.html">ArthurSlog_MarkdownEditor</a>
        </div>
        <footer>
            <a href="http://www.miitbeian.gov.cn">粤ICP备18088522号-1</a>
        </footer>
    </body>
    <script src="main.js"></script>
</html>
```

* 给标签 p 加了个id属性，以便在js里操控他

* 现在回到 ~/Desktop/ArthurSlogWebsize/client/ 路径下

> sudo npm run build

* 直接用浏览器打开index.html文件

* 点击“技术分享”，“技术分享“会变成”v0.0.1“

* ok，现在webpack可以正常打包js源码了，接下来就是调用Sass去转换scss文件

* 先 根据[webpack官方文档](https://webpack.js.org/loaders/sass-loader/)，配置webpack配置文件，指导webpack去调用Sass

> sudo npm i style.css css-loader --save-dev

* 这里呢，解释一下 css-loader会把css里面的媒体查询和url替换成import/require这样的形式的css文件，然后再交给style-loader

* style-loader 会把css文件插进html文件里

* 讲到这里，发现本篇的内通已经过多了

* 剩下的先直接上代码，下篇继续说

~/Desktop/ArthurSlogWebsize/client/dist/index.html
``` html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>ArthurSlog</title>
    </head>
    <body>
        <p id="myheand">点击显示版本</p>
        <div>
            <a href="./Markdown_Editor.html">ArthurSlog_MarkdownEditor</a>
        </div>
        <footer>
            <a href="http://www.miitbeian.gov.cn">粤ICP备18088522号-1</a>
        </footer>
    </body>
    <script src="main.js"></script>
</html>
```

* 调整文件结构

> mv /dist/style.css /dist/background.jpg /scr

* 添加文件加载器

> sudo npm i file-loader --save-dev

~/Desktop/ArthurSlogWebsize/client/src/index.js
``` js
import './background.jpg'
import './style.css'

document.getElementById("myheand").addEventListener('click', function(){document.getElementById("myheand").innerText = "V0.0.1"})    
```

* 更新 webpack配置文：

~/Desktop/ArthurSlogWebsize/client/src/index.js
``` json
const path = require('path');

module.exports = {
  // 入口点：准备进行转换的源代码的路径
  entry: './src/index.js',

  // 输出点：用来存放转换好的文件的路径
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  },

  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      },
      {
        test: /\.(png|svg|jpg|gif)$/,
        use: [
          'file-loader'
        ]
      }
    ]
  }
};   
```

* ok，现在切换至 ~/Desktop/ArthurSlogWebsize/client/ 路径下

> sudo npm run build

* 结果：

``` txt

Hash: 8c8382595145524a04c7
Version: webpack 4.19.0
Time: 525ms
Built at: 2018-09-18 03:52:56
                               Asset      Size  Chunks             Chunk Names
a8638038b88457d3a383437190030288.jpg    77 KiB          [emitted]  
                             main.js  7.72 KiB       0  [emitted]  main
Entrypoint main = main.js
[0] ./src/background.jpg 82 bytes {0} [built]
[1] ./src/index.js 182 bytes {0} [built]
[2] ./src/style.css 1.05 KiB {0} [built]
[3] ./node_modules/css-loader!./src/style.css 885 bytes {0} [built]
    + 4 hidden modules

WARNING in configuration
The 'mode' option has not been set, webpack will fallback to 'production' for this value. Set 'mode' option to 'development' or 'production' to enable defaults for each environment.
You can also set it to 'none' to disable any default behavior. Learn more: https://webpack.js.org/concepts/mode/
```

* 双击打开主页，测试一下，布局引用正常

* 点击“点击显示版本”，显示“V0.0.1”

* 我的网站已经同步更新，传送门：[ArthurSlog.com](http://www.arthurslog.com)

* 网站的源码已同步至 [Github](https://github.com/BlessedChild/ArthurSlog.com)

* 下一步，在继续完善前端开发的工程化，并采用css预编译器（preprocessor）

* 至此，ArthurSlog.com ---- ArthurSlog_Markdown前端工程化第一阶段 Get！。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢