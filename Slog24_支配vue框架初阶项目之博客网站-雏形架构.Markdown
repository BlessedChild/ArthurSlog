* ArthurSlog
* SLog-24
* Year·1

* Guangzhou·China
* July 25th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

潮水退去后 所有没能回到大海的鱼 都会死 除了那只提前上岸的

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* Slog1_如何使用nodejs与mysql进行数据交互
* Slog4_使用后端框架KOA实现静态web服务器
* Slog6_使用vue前端框架实现单页应用(SPA)

##### 前端部分：

* 统计页面-计算属性和侦听器、https://cn.vuejs.org/v2/guide/computed.html 主页：index.html

* 注册界面-条件渲染、https://cn.vuejs.org/v2/guide/conditional.html :signup.html

* 登陆界面 :signin.html

* 登陆后的界面-列表渲染、https://cn.vuejs.org/v2/guide/list.html 用户界面: account.hmtl

* 调查问卷-文本、多行文本、复选框、单选按钮、选择框、https://cn.vuejs.org/v2/guide/forms.html : form.html

* 离开页面提醒-事件处理、https://cn.vuejs.org/v2/guide/events.html 

* 移动端样式兼容-Class与Style绑定、https://cn.vuejs.org/v2/guide/class-and-style.html

##### 后端部分：

* 数据库数据交互模块-部署、配置

* 静态web服务器

* 用户注册模块

* 用户登陆模块

* 统计分析模块

* 用户状态模块-超时、无效、非法

### 开始编码

* 首先，搭起静态服务器，先切换至桌面路径

> cd ~/Desktop

* 创建一个文件夹node_vue_directive_learningload (前面文章已经创建过的就直接使用就行了)

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
    <title>index_ArthurSlog</title>
</head>

<body>

    <div>This is index's page by ArthurSlog</div>

</body>

</html>
```

* 除此之外，继续创建另外的四个页面文件 signup.html、signin.html、account.html、form.html，加上上面的 index.html 主页，我们现在一共把所有的页面文件都安排好了，一共是五个页面：

signup.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>signup_ArthurSlog</title>
</head>

<body>

    <div>This is signup's page by ArthurSlog</div>

</body>

</html>
```

signin.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>signin_ArthurSlog</title>
</head>

<body>

    <div>This is signin's page by ArthurSlog</div>

</body>

</html>
```

account.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>account_ArthurSlog</title>
</head>

<body>

    <div>This is account's page by ArthurSlog</div>

</body>

</html>
```

form.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>form_ArthurSlog</title>
</head>

<body>

    <div>This is form's page by ArthurSlog</div>

</body>

</html>
```

* 现在，把这五个页面的业务逻辑连接起来

* 首先是主页 index.html，主页与登陆和注册页面有业务关联，并且是双向的，可以从主页连接到登陆页面，也可以从登陆页面返回主页

index.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>index_ArthurSlog</title>
</head>

<body>

    <div>This is index's page by ArthurSlog</div>

</body>

</html>
```

* 加入连接的逻辑

index.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>index_ArthurSlog</title>
</head>

<body>

    <div>This is index's page by ArthurSlog</div>
    <a href="./signin.html">Signin</a>
    <br>
    <a href="./signup.html">Signup</a>

</body>

</html>
```

* 因为是双向的，对应的 signin.html 和 signin.html 文件要添加返回主页的逻辑

signup.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>signup_ArthurSlog</title>
</head>

<body>

    <div>This is signup's page by ArthurSlog</div>
    <a href="./index.html">Return index's page</a>

</body>

</html>
```

signin.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>signin_ArthurSlog</title>
</head>

<body>

    <div>This is signin's page by ArthurSlog</div>
    <a href="./index.html">Return index's page</a>

</body>

</html>
```

* 这么做的目的就是先把这个网站的业务逻辑先连接好，或者说是，先把前端路由设计好

* account.html 是登陆后的页面，因此与 signin.html 有业务逻辑的联系

signin.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>signin_ArthurSlog</title>
</head>

<body>

    <div>This is signin's page by ArthurSlog</div>
    <a href="./account.html">Signin</a>
    <br>
    <a href="./index.html">Return index's page</a>

</body>

</html>
```

account.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>account_ArthurSlog</title>
</head>

<body>

    <div>This is account's page by ArthurSlog</div>
    <a href="./signin.html">Exit Signin</a>

</body>

</html>
```

* form.html 是填写个人的注册信息的页面，因此与 signup.html 有业务逻辑的联系

signup.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>signup_ArthurSlog</title>
</head>

<body>

    <div>This is signup's page by ArthurSlog</div>
    <a href="./form.html">Signup</a>
    <br>
    <a href="./index.html">Return index's page</a>

</body>

</html>
```

form.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>form_ArthurSlog</title>
</head>

<body>

    <div>This is form's page by ArthurSlog</div>
    <a href="./signup.html">Exit Signup</a>

</body>

</html>
```

* 在当前路径下，启动静态web服务器

> node index.js

* 打开浏览器，在地址栏输入 127.0.0.1:3000，然后测试各个页面的跳转逻辑

* 至此，完成了前端页面的基础路由，一个网站的简单架构初具雏形

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
