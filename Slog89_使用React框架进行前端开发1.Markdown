# Slog89_使用React框架进行前端开发1
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-89
* Year·1

* Guangzhou·China
* October 2th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog.com](http://www.arthurslog.com)

* [MSDN: ArthurSlog](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub: BlessedChild](https://github.com/BlessedChild/ArthurSlog)

* [NPMJS.com: arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

上善若水 水善利万物而不争 处众人之所恶 故几于道

---

### 开发环境MacOS(Mojave 10.14 (18A391))

#### 需要的信息和信息源：

* [React： https://reactjs.org/](https://reactjs.org/)


* [REST: https://en.wikipedia.org/wiki/Representational_state_transfer](https://en.wikipedia.org/wiki/Representational_state_transfer)

### 开始编码

* 新建一个文件夹ArthurSlogStore

> cd ~/Desktop && mkdir ArthurSlogStore

> cd ArthurSlogStore

* 使用npx创建一个工程文件

> npx create-react-app client

> cd client

* 删除不需要的文件，最终的文件目录如下：

``` txt
 - ArthurSlogStore
   - public
     - index.html
   - src
     - App.js
     - index.css
     - index.js
     - Header.jsx
   - package.json
   - package-lock.json
```

* 完整代码如下：

src/Hander.jsx
``` jsx
import React, { Component } from 'react'

class Header extends Component {
    render() {
        return (
            <div>This is a Header</div>
        )
    }
}

export default Header
```

src/App.js
``` js
import React, { Component } from 'react';

import Header from './Header'

class App extends Component {
  render() {
    return (
        <Header />
    )
  }
}

export default App;
```

src/index.js
``` js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

public/index.html
``` html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8"/>
        <title>ArthurSlogStore</title>
    </head>

    <body>
        <div id="root">
            
        </div>
    </body>
</html>
```

* 切换至当前目录下

> sudo npm start

* 浏览器会被调起并显示

* 至此，使用React框架实现了一个简单的前端页面。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢