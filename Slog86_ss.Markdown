# Slog86_使用Sketch 设计ArthurSlog网站主页原型
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-86
* Year·1

* Guangzhou·China
* September 28th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog.com](http://www.arthurslog.com)

* [MSDN: ArthurSlog](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub: BlessedChild](https://github.com/BlessedChild/ArthurSlog)

* [NPMJS.com: arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

理想 是用实际行动去实现的 而不是藏在心里！

---

### 开发环境MacOS(Mojave 10.14 (18A391))

#### 需要的信息和信息源：

* [Sketch](https://www.sketchapp.com/)

### 开始编码

* Sketch 是一个专业的矢量图形编辑器，特定于 MaoOS

* 使用过程中，与Axure Rp8 做对比

* Sketch 目前更偏向于 UI设计 和 界面精细化设计

* 而 Axure RP8 目前更偏向与 产品设计

* 一般来说，开发的流程如下：

``` txt
Product Manager -> Designer -> Enginner



Product Manager: 产品经理根据用户调查表生成规格列表

Designer: 设计师们根据这些要求探索出低精确度的原型 最终创造出高保真的模型

Enginner: 工程师将这些设计应用到代码中 最终将产品交给用户
```

* 下次可以尝试这样的开发流程：

``` txt
Axure -> Sketch -> Fonted Coding、 Backed Coding
```

* 这次先使用Sketch 来设计ArthurSlog 的主页

* 由于Sketch 需要通过一些第三方插件来实现 HTML文件的输出

* 为了节约时间 这里我就自己Coding了，完整的代码如下：

``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>ArthurSlog</title>
    <style type="text/css">
        body,
        html {
            position: relative;
            margin: 0%;
            padding: 0%;
            display: block;
        }

        div {
            position: relative;
            left: calc(50% - 720px);
            padding: 0;
            margin: 0;
        }

        img {
            padding: 0;
            margin: 0;
        }
    </style>
</head>

<body>
    <div>
        <img src="./nav_header.jpg">
        <img src="./hero.jpg">
        <img src="./text-left-image-right1.jpg">
        <img src="./gap.jpg">
        <img src="./text-left-image-right2.jpg">
    </div>
</body>

</html>
```

* 从Sketch导出所有设计好的图片文件之后，需要与上面的 HTML文件存放在同一路径下

* 效果展示：[http://www.arthurslog.com/000100/index.html](http://www.arthurslog.com/000100/index.html)

* 这次为页面使用了 1440px 的宽度，把整个基本的页面确定了下来

* 源码已更新至 Github： [https://github.com/BlessedChild/ArthurSlog.com](https://github.com/BlessedChild/ArthurSlog.com)

* 至此，使用Sketch 重新设计了ArthurSlog 的主页界面。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢