# Slog66_自动化工具之make和Makefile1

* ArthurSlog
* SLog-66
* Year·1

* Guangzhou·China
* Sep 10th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

天之道 损有余而补不足 人之道则不然 损不足以奉有余

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [make工具](https://zh.wikipedia.org/wiki/Make)

* [集成开发环境](https://zh.wikipedia.org/wiki/%E9%9B%86%E6%88%90%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83)

* [make工具的指导文件Makefile](https://seisman.github.io/how-to-write-makefile/index.html)

### 开始编码

* 切换至桌面，创建一个文件夹 makefile_demo

> cd ~/Desktop/ && mkdir makefile_demo

* 切换至makefile_demo路径下

> cd makefile_demo

* 编写一份Makefile文件

Makefile
``` mk
say_hello:
        echo "Hello Malefile"
```

* 然后，打开命令行，在当前路径下输入一下指令

> make

* 结果是：

``` txt
echo "Hello Malefile"
Hello Malefile
```

* 上面的代码中；

1. say_hello 是一个方法，这个方法会被命令行执行，

2. echo "Hello Malefile" 是方法say_hello的主体，echo是系统指令，指令的结果 是在控制台打印“Hello Malefile”这行字

3. echo "Hello Malefile" 这一行不是我们要的，所以在前面加上@，取消命令本身的输出

Makefile
``` mk
say_hello:
        @echo "Hello Malefile"
```

* 重新试试，打开命令行，在当前路径下输入一下指令

> make

* 结果是：

``` txt
Hello Malefile
```

* 现在来写一个常用的Makefile文件，这里面有三个方法

Makefile
``` mk
say_hello:
	@echo "Hello Malefile"

generate:
	@echo "Create some text file..."
	touch file-{1..10}.txt

clean:
	@echo "Cleaning up..."
	rm *.txt
```

* 重新试试，打开命令行，在当前路径下输入一下指令

> make

* 结果仍旧是：

``` txt
Hello Malefile
```

* 下面的两个函数并没有执行

* 我们需要搞点额外的东西，默认执行的方法换一下

* 我们需要设置一个对象，把要执行的函数填入这个对象里，举个栗子：“.DEFAULT_GOAL := generate”

* 完整的代码如下：

Makefile
``` mk
.DEFAULT_GOAL := generate

say_hello:
	@echo "Hello Malefile"

generate:
	@echo "Create some text files..."
	touch file-{1..10}.txt

clean:
	@echo "Cleaning up..."
	rm *.txt
```

* 然后，打开命令行，在当前路径下输入一下指令

> make

* 结果是：

``` txt
Create some text files...
touch file-{1..10}.txt
```

* 现在默认执行的方法就是generate了

* 但是设置.DEFAULT_GOAL对象一次只能运行一个方法

* 如果要调用多个方法，就需要设置all对象，栗子如下：

Makefile
``` txt
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

* 先把刚刚生成的.txt文件都删掉

> rm -rf *.txt

* 然后，打开命令行，在当前路径下输入一下指令

> make

* 结果是：

``` txt
Hello Malefile
Create some files...
touch file-{1..10}.txt
```

* ok，现在已经两个方法都执行了

* 现在，在说一个 “强制所有文件更新” 的方法

Markfile
``` mk
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

* 看到上面的栗子，”.PHONY“里有四个“强制所有文件更新”的方法：

1. all       // all里面的方法是say_hello + generate

2. say_hello

3. generate

4. clean

* 当你的make不起作用的时候，尝试一下设置“.PHONY”对象的值

* 至此，完成了一个基础的Makefile的了解和编写。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
