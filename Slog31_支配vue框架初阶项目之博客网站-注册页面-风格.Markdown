* ArthurSlog
* SLog-31
* Year·1

* Guangzhou·China
* Aug 6th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

迟到太久 就不必到了

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

* 后台用户管理的界面-列表渲染、https://cn.vuejs.org/v2/guide/list.html 用户界面: account.hmtl

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

##### 关键思路

### 开始编码

* 切换至 client 文件夹路径下

> cd client

* 修改和调整 signup.html 文件

signup.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="./css/style.css">
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <title>signup_ArthurSlog</title>
</head>

<body>

    <div id="signup-container">
        <div>This is signup's page by ArthurSlog</div>
        <p>Singup</p>

        <form action="http://127.0.0.1:3000/signup" method="GET">

            <br>
            <div>
                Account:
                <br>
                <input type="text" name="name">
            </div>
            <br>

            <br>
            <div>
                Password:
                <br>
                <input type="text" name="password">
            </div>
            <br>

            <br>
            <div>
                Again Password:
                <br>
                <input type="text" name="repassword">
            </div>
            <br>


            <br>
            <div>
                First Name:
                <br>
                <input type="text" name="firstname">
            </div>
            <br>

            <br>
            <div>
                Last Name:
                <br>
                <input type="text" name="lastname">
            </div>
            <br>

            <br>
            <div>
                Birthday:
                <br>
                <input type="text" name="birthday">
            </div>
            <br>

            <br>
            <div>
                <span>Sex: {{ sex }}</span>
                <br>
                <input type="radio" id="one" value="Male" v-model="sex">
                <label for="one">Male</label>
                <br>
                <input type="radio" id="two" value="Female" v-model="sex">
                <label for="two">Female</label>
            </div>
            <br>

            <br>
            <div>
                <span>Age: {{ age }}</span>
                <br>
                <select v-model="age" name="age">
                    <option disabled value="">Select</option>
                    <option>1</option>
                    <option>2</option>
                    <option>3</option>
                    <option>4</option>
                    <option>5</option>
                    <option>6</option>
                    <option>7</option>
                    <option>8</option>
                    <option>9</option>
                    <option>10</option>
                    <option>11</option>
                    <option>12</option>
                    <option>13</option>
                    <option>14</option>
                    <option>15</option>
                    <option>16</option>
                    <option>17</option>
                    <option>18</option>
                    <option>19</option>
                </select>
            </div>
            <br>

            <br>
            <div>
                Wechart:
                <br>
                <input type="text" name="wechart">
            </div>
            <br>

            <br>
            <div>
                QQ:
                <br>
                <input type="text" name="qq">
            </div>
            <br>

            <br>
            <div>
                Email:
                <br>
                <input type="text" name="email">
            </div>
            <br>

            <br>
            <div>
                Contury:
                <br>
                <input type="text" name="contury">
            </div>
            <br>

            <br>
            <div>
                Address:
                <br>
                <input type="text" name="address">
            </div>
            <br>

            <br>
            <div>
                Phone:
                <br>
                <input type="text" name="phone">
            </div>
            <br>

            <br>
            <div>
                Websize:
                <br>
                <input type="text" name="websize">
            </div>
            <br>

            <br>
            <div>
                Github:
                <br>
                <input type="text" name="github">
            </div>
            <br>

            <br>
            <div>
                Bio:
                <br>
                <input type="text" name="bio">
            </div>
            <br>

            <br>
            <input type="submit" value="完成注册">
        </form>

        <a href="./index.html">Return index's page</a>
        <br>
        <br>
    </div>

    <script src="./js/signup.js"></script>
</body>

</html>
```

* 切换至server文件夹路径下

> cd server

* 现在，启动静态web服务器

> node index.js

* 现在打开浏览器，在地址栏输入 127.0.0.1:3000，正常显示主页后，点击 signup 链接，正常情况下，signup.html 页面会显得更加的简洁，同时撤掉了多余的跳转链接

* 至此，我们更新了 signup.html 的页面风格。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
