# Slogxx_xxxxxx

* ArthurSlog
* SLog-XX
* Year·1

* Guangzhou·China
* Aug XXth 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [ArthurSlog Page](http://www.arthurslog.com)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)



---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

### 开始编码

* vue框架的单文件组件分为三部分，栗子如下：

Hello.vue
``` vue
<template>
</template>

<script>
</script>

<style>
</style>
```

* 以上

1. < template > 称为“模版文件”，可以是普通的 html 或者是 JSX、jade 等语法，例如：

``` 
<template lang="jade">
</template>
```

2. < script > 就是脚本 javascript 文件了

3. < style > 是页面样式文件，可以是普通的css 或者是 scss、sass、less 等语法，例如

``` 
<style lang="scss">
</style>
```

* 其中，style 标签中有 scoped 属性时，根据官网说明：

``` txt
当 <style> 标签有 scoped 属性时，它的 CSS 只作用于当前组件中的元素。这类似于 Shadow DOM 中的样式封装。它有一些注意事项，但不需要任何 polyfill。它通过使用 PostCSS 来实现以下转换：
```

* 例如：

``` vue
<style scoped>
.example {
  color: red;
}
</style>

<template>
  <div class="example">hi</div>
</template>
```

* 转换结果：

``` vue
<style>
.example[data-v-f3f3eg9] {
  color: red;
}
</style>

<template>
  <div class="example" data-v-f3f3eg9>hi</div>
</template>
```

* 这样的一个 vue单文件组件，需要用一个编译器（或者说是转化程序）来对vue单文件组件里的三个部分，分别进行编译

* 例如：

1. 对于template，如果是JSX语法，可以使用 Babel 进行编译，[官方地址](https://babeljs.io/docs/en/babel-plugin-syntax-jsx)

2. 对于script， 即js文件，可以使用 Babel 进行编译, [官方地址](https://babeljs.io/docs/en/babel-cli)

3. 对于style， 如果是scss语法，可以使用 sass 进行编译, [官方地址](https://sass-lang.com/install)

* 为了方便进行上述操作，我们可以使用构建或者说是打包工具来帮忙完成，比如，可以使用 webpackage 

* 

* 至此，XXX。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
