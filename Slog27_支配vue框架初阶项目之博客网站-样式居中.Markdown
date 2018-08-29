* ArthurSlog
* SLog-27
* Year·1

* Guangzhou·China
* July 30th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

没有写够足够的代码量，想成为高手是不可能的，只能纸上谈兵，但写够了代码量，纸上谈兵的也是大有人在

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* Slog1_如何使用nodejs与mysql进行数据交互
* Slog4_使用后端框架KOA实现静态web服务器
* Slog6_使用vue前端框架实现单页应用(SPA)
* Slog24
* Slog25
* Slog26

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

* ctx.redirect()，参考 [webapi官方手册](https://developer.mozilla.org/en-US/docs/Web/API/Response)，获取到原始webpai中的api，koa框架中的ctx和原始webapi中的api一一对应，或者说是和原始webapi的request和response中的api一一对应

### 开始编码

* 目前基本的注册登陆注册功能已经做出来了，但是页面比码农的脸还难看，接下来简单妆点一下，我们来写一下层叠样式表css（到目前为止，都是用比较原始的方法，菜鸟嘛，总得来一遍的）

* 先看一下之前的主页的 html 文件：

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

* 我们在这里外链一下样式表 style.css

index.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="./style.css" >
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

* 为了显得专业一点，我们在当前路径下建个新的文件夹“css”来放置样式表文件吧

> mkdir css

* 重新修改一下主页 html 文件

index.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="./css/style.css" >
    <title>index_ArthurSlog</title>
</head>

<body>

    <div class="container">
    <div>This is index's page by ArthurSlog</div>
    <br>
    <a href="./signin.html">Signin</a>
    <br>
    <a href="./signup.html">Signup</a>
    </div>

</body>

</html>
```

* 嗯，这样显得专业点了，分类管理，呵呵

* 接下来切换到 css 文件夹路径下

> cd css

* 新建一个样式表文件 style.css，上面主页 index.html 引用的，就是这个文件，我们上面增加的，就是样式表文件相对于主页文件的路径，“./” 表示当前路径，所以正确路径的写法就是 “./css/style.css”

* 好了，解释完，开始编码样式文件 style.css 了

styel.css
``` css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    height: 300px;
  }
```

* 启动静态web服务器

> node index.js

* 打开浏览器，输入 127.0.0.1:3000，看一下，主页是否发生了变化，正常的话，内容已经居中了，这里给出 [层叠样式表css官方手册](https://www.w3schools.com/css/css3_flexbox.asp)，以后如果需要什么样式，就去这里找

* 同样的，我们来为 signin.html 和 signup.html 添加一下样式，打开样式文件 style.css

style.css
``` css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    height: 300px;
  }

  .signin-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  } 

  .signup-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
```

* 然后，调整一下 signin.html 和 signup.html 这两个文件

signin.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="./css/style.css" >
    <title>signin_ArthurSlog</title>
</head>

<body>

    <div class="signin-container">
        <div>This is signin's page by ArthurSlog</div>
        <p>Singin</p>
        <form action="http://127.0.0.1:3000/signin" method="GET">
            Name: <br>
            <input type="text" name="name"> 
            <br>
            Password: <br>
            <input type="text" name="password">
            <br><br>
            <input type="submit" value="登陆">
        </form>
        <a href="./account.html">Signin</a>
        <br>
        <a href="./index.html">Return index's page</a>
    </div>

</body>

</html>
```

signup.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="./css/style.css" >
    <title>signup_ArthurSlog</title>
</head>

<body>

    <div class="signup-container">
        <div>This is signup's page by ArthurSlog</div>
        <p>Singup</p>
        <form action="http://127.0.0.1:3000/signup" method="GET">
            Account: <br>
            <input type="text" name="name"> 
            <br>
            Password: <br>
            <input type="text" name="password">
            <br>
            Again Password: <br>
            <input type="text" name="repassword">
            <br>
            First Name: <br>
            <input type="text" name="firstname">
            <br>
            Last Name: <br>
            <input type="text" name="lastname">
            <br>
            Birthday: <br>
            <input type="text" name="birthday">
            <br>
            Sex: <br>
            <input type="text" name="sex">
            <br>
            Age: <br>
            <input type="text" name="age">
            <br>
            Wechart: <br>
            <input type="text" name="wechart">
            <br>
            QQ: <br>
            <input type="text" name="qq">
            <br>
            Email: <br>
            <input type="text" name="email">
            <br>
            Contury: <br>
            <input type="text" name="contury">
            <br>
            Address: <br>
            <input type="text" name="address">
            <br>
            Phone: <br>
            <input type="text" name="phone">
            <br>
            Websize: <br>
            <input type="text" name="websize">
            <br>
            Github: <br>
            <input type="text" name="github">
            <br>
            Bio: <br>
            <input type="text" name="bio">
            <br><br>
            <input type="submit" value="完成注册">
        </form>
        <a href="./form.html">Signup</a>
        <br>
        <a href="./index.html">Return index's page</a>
        <br><br>
    </div>  

</body>

</html>
```

* 打开浏览器，输入 127.0.0.1:3000，看一下，主页是否发生了变化，点击 signin 和 signup，正常的话，他们的内容已经居中了

* 至此，我们完成了主页、登陆页面、注册页面的样式居中。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢




根据 [mysql官方手册](https://dev.mysql.com/doc/refman/8.0/en/assigning-passwords.html) 修改数据库密码，先登陆mysql数据库，进入mysql命令行界面，输入

> ALTER USER USER() IDENTIFIED BY '88888888';
