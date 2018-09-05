# Slog60_浏览器之ArthurSlog浏览器-ArthurSlogBrowser-一个个人浏览器的诞生

* ArthurSlog
* SLog-60
* Year·1

* Guangzhou·China
* Sep 5th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [ArthurSlog Page](http://www.arthurslog.com)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

道生一 一生二 二生三 三生万物

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [Python官方手册](https://docs.python.org/2/library/index.html)

* [GuiProgramming toolkit for Python](https://wiki.python.org/moin/TkInter()

* [Graphical User Interfaces with Tk](https://docs.python.org/2/library/tk.html)

* [HTML解析器对比](https://zh.wikipedia.org/wiki/HTML%E8%A7%A3%E6%9E%90%E5%99%A8%E5%AF%B9%E6%AF%94)

* [Python file-objects](https://docs.python.org/2/library/stdtypes.html#file-objects)

* [Python string-methods](https://docs.python.org/2/library/stdtypes.html#string-methods)

### 开始编码

* python 2.7.10

* 开始一个简单的浏览器

~/Desktop/ArthurSlogBrowser/parser.py
``` py
#!/usr/bin/python
# -*- coding: UTF-8 -*-

f = open("index.html", "rt") # 搜索并打开当前路径下的 index.html 文件

fr = f.read() # 读取 index.html 文件

restr = fr.split('<div>', 2 ) # 解析 index.html 文件，这里把 <div> 给去掉

print restr[1]
```

* 以为上面的解析程序会读取当前路径下的一个名为 index.html 的文件

~/Desktop/ArthurSlogBrowser/index.html
``` html
<div>This is ArthurSlogBrowser~<div>
```

* 切换至当前路径下，执行解析程序

> cd ~/Desktop/ArthurSlogBrowser/

> python parser.py

* 上面的代码，将会搜索当前路径下的 index.html 文件，然后进行解析，打印出解析好的数据

* 执行结果： 

``` txt
This is ArthurSlogBrowser~
```

* 现在我们来写一个 GUI 程序，也就是 ArthurSlogBrowers（ArthurSlog浏览器）

~/Desktop/ArthurSlogBrowser/ArthurSlogBrowser.py
``` py
#!/usr/bin/python
# -*- coding: UTF-8 -*-
# ArthurSlog
# v0.0.1
 
import Tkinter as tk
master = tk.Tk()

arthurslogbrower_file = open("index.html", "rt") # 搜索并打开当前路径下的 index.html 文件

arthurslogbrower_file_f = arthurslogbrower_file.read() # 读取 html文件

rendering_file = arthurslogbrower_file_f.split('<div>', 2 ) # HTML解析器，解析html文件并分析数据结构, 这里把 <div> 给去掉

msg = tk.Message(master, text = rendering_file[1]) # 像素、图形渲染器，把解析好的数据显示在屏幕上

msg.pack()

tk.mainloop()
```

* 切换至当前路径下，执行解析程序

> cd ~/Desktop/ArthurSlogBrowser/

> python ArthurSlogBrowers.py

* 正常执行的话，会开启一个图形界面，界面上显示 “This is ArthurSlogBrowser~” 字符串

* 至此，我们完成了一个初始版的浏览器ArthurSlogBrowser。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
