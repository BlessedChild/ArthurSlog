# Slog54_lua_表、模块和包

* ArthurSlog
* SLog-54
* Year·1

* Guangzhou·China
* Aug 30 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

三观拼不过五官 以前五官是无法提升的 但三观可以动 所以我们宣扬三观 现在五官也可以动了 而且提升的效益比三观来的直接和明显 所以那些坚守三观的人更要宣扬三观了 因为他们当他们无法提升五官的时候 唯一能做的 就是高举三观打压五官了 

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [github 完整代码](https://github.com/BlessedChild/lua_learningload)

* [require](http://www.lua.org/pil/8.1.html)

* [package](http://www.lua.org/pil/15.html)

* [package Basic Approach](http://www.lua.org/pil/15.1.html)

* [package Privacy](http://www.lua.org/pil/15.2.html)

* [Packages and Files](http://www.lua.org/pil/15.3.html)

* [Using the Global Table](http://www.lua.org/pil/15.4.html)

* [Other Facilities](http://www.lua.org/pil/15.5.html)

* [Programming in Lua](http://www.lua.org/pil/contents.html)

### 开始编码

* lua的表是一种数据结构，同时还可以作为模块和包，其他的程序可以引用这些写好的模块和包，以提高效率

* 完整代码：

～/Desktop/lua_learningload/lua_table/table_1.lua
``` lua
-- 文件名为 table_1.lua
-- 定义一个名为 table_1 的模块
table_1 = {}
 
-- 定义一个常量
table_1.constant = "This is a constant value"
 
-- 定义一个函数
function table_1.f1()
    io.write("This is a public function！\n")
end
 
local function f2()
    print("This is a privacy function！")
end
 
function table_1.f3()
    f2()
end
 
return table_1
```

～/Desktop/lua_learningload/lua_table/run.lua
``` lua
-- run.lua 文件
-- table_1 模块为上文提到到 table_1.lua
-- 别名变量 m
local t = require("table_1")
 
print(t.constant)
 
t.f1()
t.f3()
```

* 切换之当前文件路径下

> cd ～/Desktop/lua_learningload/lua_table/

* 执行程序

> lua ./run.lua

* 执行结果：

``` txt
This is a constant value
This is a public function！
This is a privacy function！
```

* 至此，我们编写了一个lua模块，也叫做lua包（其实就是一个lua表），掌握了对lua包导入的操作。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
