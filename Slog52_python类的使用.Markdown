# Slog52_python类的使用

* ArthurSlog
* SLog-52
* Year·1

* Guangzhou·China
* Aug 29th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

现实就是现实 要理解现状并且分析 在那其中一定会有导致现状的原因 对原因有了充分认识之后再根据词付诸行动就好 连现状都不懂得判断的人 再我看来就是白痴

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

### 开始编码

* 更新后的完整代码：

~/Desktop/python_learningload/python_class/Employee.py
``` py
#!/usr/bin/python
# -*- coding: UTF-8 -*-
# v2.7
# macOS10.13.6
 
class Employee:
   empCount = 0
 
   def __init__(self, name, salary):
      self.name = name
      self.salary = salary
      Employee.empCount += 1
   
   def displayCount(self):
     print "Total Employee %d" % Employee.empCount
 
   def displayEmployee(self):
      print "Name : ", self.name,  ", Salary: ", self.salary

xiaomi = Employee('xiaomi',8000)

xiaomi.displayEmployee()
```

* 其中，Employee类如下：

~/Desktop/python_learningload/python_class/Employee.py
``` py
class Employee:
   empCount = 0
 
   def __init__(self, name, salary):
      self.name = name
      self.salary = salary
      Employee.empCount += 1
   
   def displayCount(self):
     print "Total Employee %d" % Employee.empCount
 
   def displayEmployee(self):
      print "Name : ", self.name,  ", Salary: ", self.salary
```

* def __init__(self, xx1, xx2, ...):，这个是类初始化方法，当你实例化类的时候，类就会执行这里面的逻辑，self代表的是Employee自己，这个参数是必须的，后面是实例化类的时候，代入的参数

* 所以，现在Employee类有 empCount、name、salary 三个属性，displayCount（self）、displayEmployee（self）两个方法

* 当你实例化Employee类的时候：

~/Desktop/python_learningload/python_class/Employee.py
``` py
xiaomi = Employee('xiaomi',8000)
```

* 'xiaomin'代入'name','8000'代入'salary'，然后类会执行初始化函数：

~/Desktop/python_learningload/python_class/Employee.py
``` py
def __init__(self, name, salary):
    self.name = name
    self.salary = salary
    Employee.empCount += 1
```

* 在初始化函数里，'xiaomi'代入Employee类的'name'属性，'8000'代入Employee类的'salary'属性，然后Employee类的'empCount'属性自增1

* 现在切换之文件路径下，执行python文件

> cd ~Desktop/python_learningload/python_class/

> python Employee.py

* 正常执行，会输出

``` txt
Name :  xiaomi , Salary:  8000
```

* 现在，我们要把类单独作为一个python文件，通过导入来使用类

~/Desktop/python_learningload/python_class/class_Employee.py
``` py
#!/usr/bin/python
# -*- coding: UTF-8 -*-
# v2.7
# macOS10.13.6

class Employee:
   empCount = 0
 
   def __init__(self, name, salary):
      self.name = name
      self.salary = salary
      Employee.empCount += 1
   
   def displayCount(self):
     print "Total Employee %d" % Employee.empCount
 
   def displayEmployee(self):
      print "Name : ", self.name,  ", Salary: ", self.salary
```

~/Desktop/python_learningload/python_class/show_Employee.py
``` py
#!/usr/bin/python
# -*- coding: UTF-8 -*-
# v2.7
# macOS10.13.6

from class_Employee import Employee

xiaomi = Employee('xiaomi',8000)

xiaomi.displayEmployee()
```

* ok，现在把 Employee类 单独写为一个文件，在另一个文件里倒入并使用

* 切换至文件路径下，执行 show_Employee.py 文件

> cd ~Desktop/python_learningload/python_class/

> python show_Employee.py

* 至此，我们了解了python类的使用。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
