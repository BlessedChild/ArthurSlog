# Slog82_ArthurSlong个人网站后台管理页面GET！
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-82
* Year·1

* Guangzhou·China
* September 24th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog.com](http://www.arthurslog.com)

* [MSDN: ArthurSlog](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub: BlessedChild](https://github.com/BlessedChild/ArthurSlog)

* [NPMJS.com: arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

慎终如始 终无败事

---

### 开发环境MacOS(High Sierra 10.13.6 (17G65))

#### 需要的信息和信息源：

### 开始编码

* 本篇对ArthurSlog.com 后台管理页面登陆界面进行设计

* 暂时先把样式和html写在一起

* 完整的页面代码如下：

~/Desktop/ArthurSlogWebsize/client/dist/manager.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>ArthurSlogManagerPathfrom</title>
</head>

<body>
    <div class="header">
        <a href="http://www.arthurslog.com">
            <img src="./ArthurSlog_Logo.png">
        </a>
    </div>
    <div class="container">

        <form action="demo_form.asp" method="POST" id="logininfo">
            <input type="text" name="userName" placeholder="UserName" required="required">
            <br>
            <br>
            <input type="password" name="password" placeholder="Password" required="required">
            <br>
            <br>
            <input class="loginButton" type="submit" form="logininfo" value="Login">
        </form>
    </div>

    <footer>
        <a href="http://www.miitbeian.gov.cn">粤ICP备18088522号-1</a>
    </footer>
</body>

<style>
    html,
    body {
        position: relative;
        margin: 0%;
        padding: 0%;
        height: 100%;
        display: block;
        overflow: hidden;
        background-color: #797e85;
    }

    .header {
        width: 256px;
        height: 95px;
        position: relative;
        left: calc(50% - 104.5px);
        margin: 1px;
        padding: 1px;
    }


    .container {
        display: block;
        width: 350px;
        height: 150px;
        background-color: #d3d3d3;
        position: relative;
        left: calc(50% - 175px);
        padding: 24px;
        border: 1px solid #bbb;
        box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1);
        margin: 0%;
        border-radius: 4px;
    }

    input {
        width: 300px;
        height: 38px;
        font-size: 100%;
        border: 0;
        padding: 0 25px 0 25px;
        margin: 0;
        border-radius: 4px;
        box-shadow: inset 0 1px 2px rgba(0, 0, 0, .4);
    }

    .loginButton {
        width: 350px;
        background-color: #2593de;
        color: white;
        font-size: 100%;
        margin: 0%;
        border-radius: 4px;
        border: 1px solid #aaa;
        padding: 0 80px 0 80px;
    }

    .spreaLine {
        height: 10px;
    }

    footer {
    font-size: .8rem;
    position: absolute;
    height: 5vh;
    bottom: 1vh;
    left: calc(50% - 80px);
}
</style>

</html>
```

* 实际效果请移步 [www.ArthurSlog.com/manager.html](http://www.ArthurSlog.com/manager.html)

* 至此，完成了 ArthurSlog网站的后台登陆界面。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
