# Slog103_使用React框架进行前端开发14
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-103
* Year·1

* Guangzhou·China
* October 29th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

知常曰明 不知常 妄作 凶

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

### 开始编码

* 整个工程更新为 四大前端-大后端 的结构

* 四大前端分为：客户端前端 -> 运营前端 -> 管理前端 -> 开发前端 (实现业务解耦)

* 大后端则承接了上述所有前端的后台交互

* 本次来开荒 ‘开发前端’

* 作为首尾的‘客户端前端’和‘开发前端’是 项目的必要选项

* 中间部分根据业务可以进行无限的解耦

* ok 现在来配置‘开发前端’的环境

# 开发前端界面

* 一个下拉选择栏： 用于选择测试接口（就是在开发阶段 我们选择把数据传给后端的指定接口）

* input输入框：根据上面的选择 这里输入的是准备发给后端的数据

* 测试按钮：当点击测试按钮的时候 会调用我们上面选中的函数 和 数据 向后端发起请求

* 结果显示框：显示后端返回的所有数据

# Contract

``` txt
开发模式，应该以降低开发成本为原则

一个网页的基础是由 HTML，CSS 和 JS 构成的
这些网页前端代码通过浏览器打开后能够直接运行

当时为了降低开发成本
现在我们写的大部分代码并不是原生的 HTML，CSS 和 JS
而是基于它们扩展出来的更上层的语法

所以在开发的过程中
我们需要一个编译的过程 把上层代码编译为原生的 HTML，CSS 和 JS

编译上层代码的工具有很多 
比如
使用babel工具 把ES6+的代码 编译为 ES5的代码
使用Less工具 把less代码 编译为 css代码

这些编译工具 成为了前端研发体系的一部分
在工具的更上一层 渐渐出现了统一管理这些工具的超级工具
比如 webpack
通过 webpack工具 可以让所有工具协同工作 进一步降低开发的成本

除了编译工具之外
超级工具webpack 还一直处于发展之中
在这个期间 出现了帮助开发人员 自动刷新浏览器的工具、压缩代码的工具
、代码风格检测的工具、代码单元测试的工具、...

发展到当前的时间点 
类似webpack的超级工具渐渐的把所有工具集成在自己身上
更进一步的降低开发的成本

在发展的过程中 就是在经历着从不成熟到成熟
所以纷乱、繁杂 始终相伴

坚守 一切为降低成本 为原则
大家一同共勉 前进
```

``` txt
注释并不是冷冰冰的文字

注释应该是一个充满温暖的地方 记载着无数不甘寂寞的灵魂

所以 在我的注释里 不限制内容和格式 可以尽情的记录下任何信息

最后 在构建生产环境代码的时候 再把注释信息进行屏蔽
```

> sudo npm init -y

* add webpack and webpack-cli as a dev dependency to our project

* We installed webpack-cli so that we can use webpack in the command line

> sudo npm install webpack webpack-cli --save-dev

> sudo npm install react react-dom --save

* In order for React to work, we need to install Babel alongside with it

* We need Babel to transpile ES6 and JSX to ES5

* So:

> sudo npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev

* babel-core: Transforms ES6 code to ES5

* babel-loader: Webpack helper to transpile code, given the the preset

* babel-preset-env: Preset which helps babel to convert ES6, ES7 and ES8 code to ES5

* babel-preset-react: Preset which Transforms JSX to JavaScript


* The less-loader requires less as peerDependency

* Thus you are able to control the versions accurately.

* Use the css-loader or the raw-loader to turn it into a JS module and 

* the ExtractTextPlugin to extract it into a separate file

> npm install less-loader less css-loader style-loader --save-dev

* Chain the less-loader with the css-loader and the style-loader to immediately apply all styles to the DOM

webpack.config.js
``` js
module.exports = {
    ...
    module: {
        rules: [{
            test: /\.less$/,
            use: [{
                loader: "style-loader" // creates style nodes from JS strings
            }, {
                loader: "css-loader" // translates CSS into CommonJS
            }, {
                loader: "less-loader" // compiles Less to CSS
            }]
        }]
    }
};
```

* Create an index.js file inside root of the /src folder

* for now add the following line code inside it

* This file will be the entry point to our app

./src/index.js
``` js
console.log("Hello Arthur")
```

* Create an index.html file inside root of the /src folder and add following code inside it

./src/index.html
``` html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>React Boilerplate</title>
</head>

<body>
    <div id="root">

    </div>
</body>

</html>
```

* Create a webpack.config.js in the root directory of the project

* so that we can define rules for our loaders

* Define the entry point and output directory of our app inside the webpack.config.js

./webpack.config.js
``` js
const path = require("path");

const config = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "/dist"),
    filename: "bundle.js"
  }
};

module.exports = config;
```

* In the above code

* Webpack will bundle all of our JavaScript files into bundle.js file inside the /dist directory

* Add some loaders inside this file, which will be responsible for loading and bundling the source files

./webpcak.config.js
``` js
const path = require("path");

const config = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "/dist"),
    filename: "bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        },
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader", "less-loader"]
      }
    ]
  }
};

module.exports = config;
```

* Here babel-loader is used to load our JSX/JavaScript files and

* less-loader is used to load all of the Less files to CSS files

* css-loader is used to load and bundle all of the CSS files into one file and 

* style-loader will add all of the styles inside the style tag of the document

* Create a .babelrc file inside root of the project directory with the following contents inside of it

./.babelrc
``` js
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

* This file will tell babel which presets to use for transpiling the code

* Here we are using two presets:

* env: This preset is used to transpile the ES6/ES7/ES8 code to ES5

* react: This preset is used to transpile JSX code to ES5

* Add the following lines of code inside the script object of the package.json file as below:


``` txt
"start": "webpack --mode development --watch",
"build": "webpack --mode production"
```

* Here i have used watch flag

* So whenever there is a change in source files

* Webpack will automatically compile all the source files

* There are two modes in webpack 4

* the production mode which produces optimized files ready for use in production

* and development mode which produces easy to read code

* and gives you best development experience

* Html-webpack-plugin：

* Now we also need to install html-webpack-plugin

* this plugin generates an HTML file

* injects the script inside the HTML file and writes this file to dist/index.html

> sudo npm install html-webpack-plugin --save-dev

* Now we need to configure this plugin inside the webpack.config.js file

./webpcak.config.js
``` js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

const config = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "/dist"),
    filename: "index-bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: ["babel-loader"]
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html"
    })
  ]
};

module.exports = config;
```

* Here the value of template key is the file index.html

* that we created earlier and it uses this file as a template

* and generates new file named index.html inside the /dist folder

* with the script injected

* But this approach has a downside that you have to manually refresh the webpage

* in order to see the changes you have made

* To have webpack watch our changes and refresh webpage whenever any change

* is made to our components, we can install webpack-dev-server

* Webpack-dev-server:

> npm install webpack-dev-server --save-dev

* And change the package.json start script like below:

```
"start": "webpack-dev-server --mode development --open --hot"
```

* 因为 有一些比较细节的地方 使用英文来理解比较准确

* 以上就是对开发环境的一个配置

* 这里是配置好的工程目录结构

![工程目录结构](https://github.com/BlessedChild/LogofAxu/blob/master/images/Slog103/%E5%B7%A5%E7%A8%8B%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84.png?raw=true)

* 工程文件已经上传至[Github：https://github.com/BlessedChild/ArthurSlogStore](https://github.com/BlessedChild/ArthurSlogStore)

* 至此，完成了‘开发前端’的开发环境的初始化配置。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
