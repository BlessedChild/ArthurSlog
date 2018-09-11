# Slog70_自动化工具之make和Makefile2

* ArthurSlog
* SLog-70
* Year·1

* Guangzhou·China
* Sep 11th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

圣人不积 既以为人己愈有既已为人己愈多

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* 提示：Makefile中使用Tab键作为两个block之间的分割标志

* [完整代码-Github传送门]()

* [make工具](https://zh.wikipedia.org/wiki/Make)

* [集成开发环境](https://zh.wikipedia.org/wiki/%E9%9B%86%E6%88%90%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83)

* [make工具的指导文件Makefile](https://seisman.github.io/how-to-write-makefile/index.html)

### 开始编码

* 之前的文章编写了一个基础的 Makefile文件

~/Desktop/makefile_demo/Makefile
``` makefile
.PHONY: all say_hello generate clean

all: say_hello generate

say_hello:
        @echo "Hello Malefile"

generate:
        @echo "Creating some files..."
        touch file-{1..10}.txt

clean:
        @echo "Cleaning up..."
        rm *.txt
```

* 先整理一下当前路径 ~/Desktop/makefile_demo/ 下的文件

> cd ~/Desktop/makefile_demo/

> make clean

> mkdir demo1 demo2

> mv Makefile demo1/

> cd demo2

* 在当前路径下（~/Desktop/makefile_demo/demo2/）创建一个新文件 Makefile

* 现在的目录结构如下：

``` txt
makefile_demo
      | - demo1
            | - Makefile
      | - demo2
            | - Makefile
```

* 这次，来介绍一下 Makefile中的 “判断” 语法

* 举个栗子，上代码：

~/Desktop/makefile_demo/demo2/Makefile
``` makefile
.PHONY: all warning generate clean

all: warning generate

# fun: warning
# if(./README.md)
# do
# @echo "README.md is an existing file，you just covered it"
warning : README.md
	@echo "README.md is an existing file，you just covered it"

generate: 
	@echo "Creating a file named README.md ..."
	touch README.md

clean: 
	@echo "Cleaning up..."
	rm *.md
```

* 上面的代码中；

``` makefile
# fun: warning
# if(./README.md)
# do
# @echo "README.md is an existing file，you just covered it"
warning : README.md
	@echo "README.md is an existing file，you just covered it"
```

* 这里分成了三个部分：

// 方法名
1. warning

// 判断模块，在这里是判断当前路径下是否有 README.md 这个文件
2. README.md

// 方法体，是具体的执行方法，这里是在控制台输出“README.md is an existing file，you just covered it”这一行字符串
3. @echo "README.md is an existing file，you just covered it"

* 现在，打开命令行，在当前路径执行Makefile文件里的 generate方法

> make generate

``` txt
Creating a file named README.md ...
touch README.md
```

* 现在在当前路径下，生成了一个README.md文件

> ls

``` txt
Makefile	README.md
```

* 现在，执行Makefile文件里的 all 方法，make 默认执行all方法，所以all可以省略

> make

``` txt
Creating a file named README.md ...
touch README.md
```

* 上面的 all方法里面晗有两个方法 warning 和 generate

* 其中warning会先执行 “判断模块”，然后再执行 方法体

* “判断模块总是优先执行”

* 现在执行clean方法，清理当前路径

> make clean

``` txt
Cleaning up...
rm *.md
```

* 查看当前路径

> ls

``` txt
Makefile
```

* 上面说了这么多，都是再描述Makefile的 “规则” 的使用

* 官方称之为 “rules”

a rules
```
target … : prerequisites …
        recipe
        …
        …
```

* 至此，完成了一个基础的Makefile的“rules”的了解和编写。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
