# Slog96_使用React框架进行前端开发8
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-96
* Year·1

* Guangzhou·China
* October 14th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

自古逢秋悲寂寥 天气凉了 记得适时进补一些温补的食材 约上小伙伴吃吃火锅 撸撸串 除了填饱饥肠辘辘的肚子 更重要的是填满繁忙城市里孤独空洞的灵魂 踏在梦想的道路上 枫叶漫地 加油朋友 任何时候都不要放弃 当你迷茫的时候 可以来看看我的博客（不一定有什么卵用） 只是 你会知道 有一个人 一直在前进的路上

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* 各大线上运营的商城

### 开始编码

* 过去这几天 研究了几款上线的产品的设计

* 同时调查了解了一下一些主流的开发方案

* 结合做几天收集的信息 我先杂糅在一起 然后提取出最本质的东西

* 还是以项目为导向

* 本次完成了‘个人中心’页面的功能设计 和 页面布局的设计 以及 前后端接口的设计

* 本篇来完成‘个人中心’页面的功能设计 和 页面布局的设计

* 前后端的接口设计另起一篇来写

* 市面上的微信h5商城非常繁多

* 但一些必须的业务是高度统一的 例如‘订单系统、个人信息系统、支付系统’

* 根据分析 为‘个人中心’产品页面设计了以下业务功能：

``` txt
余额、积分、卡、券
我的订单、待付款、待接单、待发货、已发货、已完成
性别、生日、收获地址
手机号、微信绑定
店铺主页、推广中心、关注我们、店铺信息
```

* 上面几个 都是是基础必要的业务（店铺主页只是简单路由到主页）

* 代码比较多 就不一个一个列出来了 没什么意思

* 可以直接到Github上看一看源码 顺便点个star 支持一下谢谢（笑）

* 在文件结构的安排上 目前还没有完全固定 

* 主要是样式文件的解耦和业务之间的权衡一直在变化 所以有一些文件命名和代码还未全部更新完

* 下面上一下当前mobile端 ‘个人中心’页面的产品图

![个人中心1](https://github.com/BlessedChild/LogofAxu/blob/master/images/96/%E4%B8%AA%E4%BA%BA%E4%B8%AD%E5%BF%831.png?raw=true)

![个人中心2](https://github.com/BlessedChild/LogofAxu/blob/master/images/96/%E4%B8%AA%E4%BA%BA%E4%B8%AD%E5%BF%832.png?raw=true)

* 接下来 使用ajax来获取页面信息内容了

* 考虑到产品上线之后的运营 还需要在web端开发一个运营平台

* 这个运营平台可以来更新 产品里面产品的数据内容 例如图片、产品介绍、价格等一些日常高频率使用的功能

* 其他比较大的功能 解耦出来 进行深度开发

* 上一次提到了 页面上的字体采用 css3 的 rem单位特性（随着根节点font-size的大小变化而变化）

* 这次‘个人中心’页面 也全面采用了 rem特性和百分比来处理页面样式 

* 更新README，增加 产品的 ‘个人中心’ 页面的设计

* Github上工程的名称更新了

* 工程文件已经上传至[Github：https://github.com/BlessedChild/ArthurSlogStore](https://github.com/BlessedChild/ArthurSlogStore)

* 至此，实现了mobile端 ‘个人中心’ 页面的功能设计 和 布局设计。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
