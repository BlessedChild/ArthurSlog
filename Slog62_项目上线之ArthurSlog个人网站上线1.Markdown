# Slog62_项目上线之ArthurSlog个人网站上线1

* ArthurSlog
* SLog-62
* Year·1

* Guangzhou·China
* September 9th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [ArthurSlog Page](http://www.arthurslog.com)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

ArthurSlog个人网站上线了～

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

### 开始编码

* 继之前的域名购买、服务器购买、域名解析、域名备案完成之后，现在把第一版的网站正式上线

* 网站地址 www.arthurslog.com

* 第一版网站，以最少的代码实现：

1. 网站标题是“个人技术分享”

2. 背景图一张

3. 底部根据管局要求，附上了备案号并链接至管局

4. 前端布局使用到了 [calc方法](https://developer.mozilla.org/zh-CN/docs/Web/CSS/calc)

5. 后端使用 koa框架 + koa-static 实现了一个简单的web服务器

* 前后端所有代码已经上传至 v1.0.0[Github](https://github.com/BlessedChild/ArthurSlog.com)

* 当前的文件结构：

ArthurSlog
    |
    |
     -- index.html
     -- index.js
     -- style.css
     -- background.jpg
     -- node_modules
     -- package.json
     -- package-lock.json
     --README.md

* 当前的前端代码index.html、style.css如下：

index.html
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
        <footer>
            <a href="http://www.miitbeian.gov.cn">粤ICP备18088522号-1</a>
        </footer>
    </body>
</html>
```

style.css
``` css
body{ 
    background-image:url('background.jpg');
    background-repeat:no-repeat;
    background-position:50% -10%;
}

p{
    font-size: 48px;
    position: relative;
    left: calc(50% - 144px);
}

footer {
    font-size: .8rem;
    position: absolute;
    bottom: 10px;
    left: calc(50% - 80px);
}
```

* 后端服务器代码index.js如下：

index.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();

// $ GET /package.json
app.use(serve('.'));

app.listen(80);

console.log('listening on port 80');
```

* 配置文件 package.json如下：

package.json
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
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/BlessedChild/ArthurSlog.com.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/BlessedChild/ArthurSlog.com/issues"
  },
  "homepage": "https://github.com/BlessedChild/ArthurSlog.com#readme"
}
```

* 自述文件 README.md如下：

README.md
``` md
# This is ArthurSlog.com
```

* 另外，其他的文件无需手动修改，不管

* 至此，完成了第一版网站源码的编写。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
