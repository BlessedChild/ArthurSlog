# Slog55_lua面向对象之lua类

* ArthurSlog
* SLog-55
* Year·1

* Guangzhou·China
* Aug 30th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

现实中的事情不是根据人的喜好而定的 比如长在你嘴里的智齿 大部分情况下 你会因为自己（的牙）而痛苦 直到忍痛拔掉 鲜血淋漓 也许痛过之后 才能回归正途 

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [github 完整代码](https://github.com/BlessedChild/lua_learningload)

* [Object-Oriented Programming](http://www.lua.org/pil/16.html)

* [Classes](http://www.lua.org/pil/16.1.html)

* [Classes Inheritance](http://www.lua.org/pil/16.2.html)

* [Classes Multiple Inheritance](http://www.lua.org/pil/16.3.html)

* [Classes Privacy](http://www.lua.org/pil/16.4.html)

* [Classes The Single-Method Approach](http://www.lua.org/pil/16.5.html)

* [require](http://www.lua.org/pil/8.1.html)

* [package](http://www.lua.org/pil/15.html)

* [package Basic Approach](http://www.lua.org/pil/15.1.html)

* [package Privacy](http://www.lua.org/pil/15.2.html)

* [Packages and Files](http://www.lua.org/pil/15.3.html)

* [Using the Global Table](http://www.lua.org/pil/15.4.html)

* [Other Facilities](http://www.lua.org/pil/15.5.html)

* [Programming in Lua](http://www.lua.org/pil/contents.html)

### 开始编码

* 完整代码：

~/Desktop/lua_learningload/lua_class/Employee.lua
``` lua
-- 文件名为 EmployeePackage.lua
-- 定义一个名为 EmployeePackage 的模块
-- Meta class
EmployeePackage = {empCount = 0, name = '0', salary = 0}

-- 派生类的方法 new
function EmployeePackage:new (o,name,salary)
  e = e or {}
  setmetatable(e, self)
  self.__index = self
  self.empCount = self.empCount + 1
  self.name = name
  self.salary = salary
  return e
end

-- 派生类的方法 printArea
function EmployeePackage:info ()
  print("Total Employee ", self.empCount)
  print("Name : " , self.name)  
  print("Salary: " , self.salary)
end

emp = Employee:new(nil,'xiaoming',1024)

emp:info()
```

* 其中，Employee类如下：

~/Desktop/lua_learningload/lua_class/Employee/lua
``` lua
-- 文件名为 EmployeePackage.lua
-- 定义一个名为 EmployeePackage 的模块
-- Meta class
EmployeePackage = {empCount = 0, name = '0', salary = 0}

-- 派生类的方法 new
function EmployeePackage:new (o,name,salary)
  e = e or {}
  setmetatable(e, self)
  self.__index = self
  self.empCount = self.empCount + 1
  self.name = name
  self.salary = salary
  return e
end

-- 派生类的方法 printArea
function EmployeePackage:info ()
  print("Total Employee ", self.empCount)
  print("Name : " , self.name)  
  print("Salary: " , self.salary)
end
```

* 现在，切换至文件路径下

> cd ~/Desktop/lua_learningload/lua_class/Employee.lua

* 执行lua文件

> lua ./Employee.lua

* 执行结果：

``` txt
Total Employee 	1
Name : 	xiaoming
Salary: 	1024
```

* 另一方面，根据上一篇文章所讲，上面的这个lua类也可以作为一个lua包，在新的程序里导入

~/Desktop/lua_learningload/lua_class/
``` lua
-- Meta class
EmployeePackage = {empCount = 0, name = '0', salary = 0}

-- 派生类的方法 new
function EmployeePackage:new (o,name,salary)
  e = e or {}
  setmetatable(e, self)
  self.__index = self
  self.empCount = self.empCount + 1
  self.name = name
  self.salary = salary
  return e
end

-- 派生类的方法 printArea
function EmployeePackage:info ()
  print("Total Employee ", self.empCount)
  print("Name : " , self.name)  
  print("Salary: " , self.salary)
end

return EmployeePackage
```

~/Desktop/lua_learningload/lua_class/EmployeePackage.lua
``` lua
-- run.lua 文件
-- EmployeePackage 模块为上文提到到 EmployeePackage.lua
-- 别名变量 p
local p = require("EmployeePackage")
 
emp = p:new(nil,'xiaoming',1024)
 
emp:info()
```

* 现在，切换至文件路径下

> cd ~/Desktop/lua_learningload/lua_class/

* 执行lua文件

> lua ./run.lua

* 执行结果：

``` txt
Total Employee 	1
Name : 	xiaoming
Salary: 	1024
```

* 至此，我们实现了一个lua类，并把这个lua类打包供其他lua程序使用。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
