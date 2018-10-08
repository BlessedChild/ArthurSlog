# Slog93_使用React框架进行前端开发5
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-93
* Year·1

* Guangzhou·China
* October 8th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

善为士者 不武 善战者 不怒 善胜敌者 不与 善用人者 为之下 是谓不争之德 是谓用人之力 是谓配天古之极

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* [Less](http://lesscss.org/)

* [Webpack](https://webpack.js.org)

* [jakoblind](https://webpack.jakoblind.no/)

### 开始编码

* 之前的页面样式 是直接手写的

* 文件代码一旦多起来 开发维护就不方便了

* 本篇来引入less样式预编译器 来升级一下开发工具

* 之前采用react官方的快速开发脚手架工具

* 现在升级为使用 webpack项目构建工具

* [简洁的使用方法 https://webpack.jakoblind.no/](https://webpack.jakoblind.no/)

* 勾选 ‘React‘、 ‘Less’、 ‘React hot loader’，之后 点击‘Get your project as a zip!’ 下载配置好的工程文件

* 解压之后，切换至文件路径下，执行：

> sudo npm i

* 等待node模块下载完成，接着

> sudo npm install --save-dev less

* 接着把之前的工程源码转移到 新的开发工程中

* 中间进行了一些代码的更新 工程地址[https://github.com/BlessedChild/ArthurSlogStore_1](https://github.com/BlessedChild/ArthurSlogStore_1)

* 你可以下载我的工程文件进行测试

> git clone https://github.com/BlessedChild/ArthurSlogStore_1.git

> cd ArthurSlogStore_1

> sudo npm i

> sudo npm start

* 查看页面 会看到header的样式发生了改变

* 这次修改了一下headerBar的样式

* 在工程根目录新建一个less文件

./index.less
``` less
@width: 600px;
@height: @width + 10px;

#app {
    width: @width;
    height: @height;
    background-color: black;
}
```

* 随后，在Header.jsx文件里添加

./Header.jsx
```js
import './index.less'
```

* 查看页面效果 已经生效

* 剩下的 找时间参照less文档 把已存在的样式转移到less文件里

* 至此，暂时完成了less预编译器的引入 和 使用。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
