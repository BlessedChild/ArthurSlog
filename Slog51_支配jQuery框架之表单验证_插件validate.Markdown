# Slog51_支配jQuery框架之表单验证_插件validate

* ArthurSlog
* SLog-51
* Year·1

* Guangzhou·China
* Aug 28th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

现实就是答案 就算抱怨生不逢时 社会不公 也不会有任何改变

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [jQuery官网](https://jquery.com/)

* [jquery.validate](https://jqueryvalidation.org/)

### 开始编码

* jQuery说白了就是一堆js代码，运行在浏览器环境下的js代码

* 首先理一下思路：

1. 引入js插件（jQuery插件）

2. 在script里，也就是 js文件里调用插件，或者换种说法就是调用插件里写好的方法

3. 查看 js插件的说明手册，让 html文件里的元素和 js文件相关联，这样就可以在 js文件里去操控 html文件了

* 我们需要准备 三份插件 一份 html文件（js、css、html写在一份文件里）

``` txt
1.主页： index.html
2.插件： jQuery.js
3.插件： jquery.validate.js
4.jquery.validate.js的配置文件：messages.js
```

* 其中 插件： jQuery.js 和 插件： jquery.validate.js 去官网下载

* 插件： jquery.validate.js 的配置文件 message.js 如下：

message.js
``` js
(function( factory ) {
    if ( typeof define === "function" && define.amd ) {
        define( ["jquery", "../jquery.validate"], factory );
    } else {
        factory( jQuery );
    }
}(function( $ ) {

/*
 * Translated default messages for the jQuery validation plugin.
 * Locale: ZH (Chinese, 中文 (Zhōngwén), 汉语, 漢語)
 */
$.extend($.validator.messages, {
    required: "这是必填字段",
    remote: "请修正此字段",
    email: "请输入有效的电子邮件地址",
    url: "请输入有效的网址",
    date: "请输入有效的日期",
    dateISO: "请输入有效的日期 (YYYY-MM-DD)",
    number: "请输入有效的数字",
    digits: "只能输入数字",
    creditcard: "请输入有效的信用卡号码",
    equalTo: "你的输入不相同",
    extension: "请输入有效的后缀",
    maxlength: $.validator.format("最多可以输入 {0} 个字符"),
    minlength: $.validator.format("最少要输入 {0} 个字符"),
    rangelength: $.validator.format("请输入长度在 {0} 到 {1} 之间的字符串"),
    range: $.validator.format("请输入范围在 {0} 到 {1} 之间的数值"),
    max: $.validator.format("请输入不大于 {0} 的数值"),
    min: $.validator.format("请输入不小于 {0} 的数值")
});

}));
```

* 主页 html文件如下：

index.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>ArthurSlog</title>
    <script src="jquery.js"></script>
    <script src="jquery.validate.js"></script>
    <script src="messages.js"></script>
    <script>
        $.validator.setDefaults({
            submitHandler: function () {
                alert("提交事件!");
            }
        });
        $().ready(function () {
            $("#Form").validate();
        });
    </script>
    <style>
        .error {
            color: red;
        }
    </style>
</head>

<body>
    <form id="Form" method="get" action="">
        <fieldset>
            <legend>输入您的名字，邮箱，URL，备注。</legend>
            <p>
                <label for="cname">Name (必需, 最少3个字母)</label>
                <input id="cname" name="name" minlength="3" type="text" required>
            </p>
            <p>
                <label for="cemail">E-Mail (必需)</label>
                <input id="cemail" type="email" name="email" required>
            </p>
            <p>
                <label for="curl">URL (可选)</label>
                <input id="curl" type="url" name="url">
            </p>
            <p>
                <label for="ccomment">备注 (必需)</label>
                <textarea id="ccomment" name="comment" required></textarea>
            </p>
            <p>
                <input class="submit" type="submit" value="Submit">
            </p>
        </fieldset>
    </form>
</body>

</html>
```

* 用浏览器打开 index.html 文件，操作一下，正常情况下，表单已经具有了校验功能

* 至此，我们实现了表单校验功能。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
