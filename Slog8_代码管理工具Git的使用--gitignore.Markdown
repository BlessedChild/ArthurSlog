* ArthurSlog
* SLog-8
* Year·1

* Guangzhou·China
* July 15th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

因为害怕 所以要继续前进

---

### 开发环境MacOS(High Sierra 10.13.5)

* 我们需要到的信息 [git官方手册](https://git-scm.com/docs/gitignore)

* .gitignore 文件：当你使用git 或 github 工具的时候，如果你项目里有一些文件只想留在本地而不上传至仓库，此时你就需要到.gitignore 文件

* 切换至项目路径下，创建一个 .gitignore 文件

> touch .gitignore

#### 下面是 .gitignore 的配置

* 如果你要忽略路径，请在 .gitignore 文件里写入：

.gitignore
```
dir/
```

* 如果你要忽略所有后缀为 .txt 的文件，请在 .gitignore 文件里写入

.gitignore
``` 
dir/
*.txt
```

#### 使用技巧： 要忽略已存在的文件或路径时，如果此时代码仓库已存在该路径或文件，需要先移除本地的路径或文件，然后执行如下代码，最后再push到仓库：

##### 如果要移除路径 dir

> git rm --cached -r dir/

##### 如果要移除文件 doc.txt

> git rm --cached -r doc.txt

* 至此，介绍完 gitignore 的基本使用方法，更多信息，请查看 [git官网](https://git-scm.com/docs/gitignore)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
