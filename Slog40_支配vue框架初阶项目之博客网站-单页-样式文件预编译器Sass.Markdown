* ArthurSlog
* SLog-40
* Year·1

* Guangzhou·China
* Aug 17th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

劳心者治人 劳力者治于人

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [样式文件预编译器Sass的安装和使用](https://sass-lang.com/install)

* [样式文件预编译器Sass指导手册](https://sass-lang.com/guide)

* [HTTP概述](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_is_a_web_server)

* [HTTP](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)

* [互联网是如何工作的](https://developer.mozilla.org/zh-CN/docs/learn/How_the_Internet_works)

* [万维网是如何工作的](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/How_the_Web_works)

* [统一资源定位符(URL)](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_is_a_URL)

* [什么是超链接](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_are_hyperlinks)

* [创建超链接](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks)

* [AJAX是异步的JavaScript和XML（Asynchronous JavaScript And XML）](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started)

* [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)

* [Using files from web applications](https://developer.mozilla.org/zh-CN/docs/Web/API/File/Using_files_from_web_applications)

### 开始编码

* 我们在这里使用 npm 指令的方式安装 Sass，根据 [Sass官网](https://sass-lang.com/install) 的说明，我们全局安装 Sass

> sudo npm install -g sass

* 我们切换到 css 文件夹路径下，创建一个 sass文件，sass 文件分两种语法 sass 和 scss，在这里我们使用 scss 语法，这种语法更接近原生的 css语法

> cd clinet/css

* 根据 [Sass官网的使用手册](https://sass-lang.com/guide)

client/css/style.scss
``` scss
$font-stack:    Helvetica, sans-serif;
$primary-color: #ff0000;

body {
  font: 100% $font-stack;
  color: $primary-color;
}

#signup-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
```

* Sass使用 $ 符号来实现变量的功能，也就是说，在一个字符串前面加上 $ 符号，就能使这个字符串代表一个变量：

``` scss
$front-stack: Helvetica, sans-serif;
```

* 上面变量为 front-stack，他的值是 Helvetica, sans-serif

* 现在，切换到 css 文件夹路径下

> cd client/css/

* 现在，我们要使用 Sass预编译器（其实就是一段代码，一个程序），来把 sass 文件转换为 css 文件

* 根据 [Sass官网的使用说明](https://sass-lang.com/install),"sass sass文件名 css文件名"

> sass style.scss style.

* 现在，scss 文件就转换为 css 文件了，转换的结果如下：

client/css/style.css
``` css
body {
  font: 100% Helvetica, sans-serif;
  color: #ff0000;
}

#signup-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

/*# sourceMappingURL=style.css.map */
```

* 现在，打开浏览器，输入 127.0.0.1:3000/app.html，文字现在应该是红色的了

* 至此，我们成功使用 Sass预编译器 来生成我们需要的 css 文件。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
