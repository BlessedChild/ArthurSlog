* ArthurSlog
* SLog-28
* Year·1

* Guangzhou·China
* Aug 1th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

当你头脑发热的时候 手足无措的时候 记得 先面对遇到的事情和问题 先看清自己 认清问题 然后把解决方法一个一个记下来 最后选择一个合适的方法去解决

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* Slog1_如何使用nodejs与mysql进行数据交互
* Slog4_使用后端框架KOA实现静态web服务器
* Slog6_使用vue前端框架实现单页应用(SPA)
* Slog24
* Slog25
* Slog26

##### 前端部分：

* 统计页面-计算属性和侦听器、https://cn.vuejs.org/v2/guide/computed.html 主页：index.html

* 注册界面-条件渲染、https://cn.vuejs.org/v2/guide/conditional.html :signup.html

* 登陆界面 :signin.html

* 后台用户管理的界面-列表渲染、https://cn.vuejs.org/v2/guide/list.html 用户界面: account.hmtl

* 调查问卷-文本、多行文本、复选框、单选按钮、选择框、https://cn.vuejs.org/v2/guide/forms.html : form.html

* 离开页面提醒-事件处理、https://cn.vuejs.org/v2/guide/events.html 

* 移动端样式兼容-Class与Style绑定、https://cn.vuejs.org/v2/guide/class-and-style.html

##### 后端部分：

* 数据库数据交互模块-部署、配置

* 静态web服务器

* 用户注册模块

* 用户登陆模块

* 统计分析模块

* 用户状态模块-超时、无效、非法

##### 关键思路

* vue框架属于前端的js，需要与后端koa框架的nodejs进行交互，这是怎么做到的？

* 直接能想到的，就是nodejs直接通过io去动态修改前端的vue文件的js代码，这样当浏览器打开html文件的时候，html文件会去加载vue的js文件，这样看起来就实现了前后端js数据的交互

* 如果按照上面的思路，需要先等待koa后端js执行完之后，vue的js文件修改完成了之后，koa的js文件再执行重定向，调用浏览器打开修改好的html文件

* 这样就完成了一个操作流程

* 这里有个点？！

* 后端框架koa使用nodejs，在操作系统纸上运行各种服务；而前端vue框架使用js，在浏览器上执行路由等各种功能，浏览器js的边界在哪里？；

* 这就意味着，vue框架的使用范围在被限制在浏览器里了，而koa实际上是nodejs的代码集合，可以操作到vue框架也就是浏览器里的js代码；那么，可以把vue代码直接放进koa代码里，让vue的代码成为koa代码的数据的一部分（这里指的是“指令与数据”里面的数据），把vue的代码作为数据交给koa操作

* 这里可能有两种情况：

1. 当在浏览器点击按钮的时候，浏览器里的js向后端发去一条信息，后端的nodejs写的服务接收到这条信息之后，对这条信息进行解析和响应或执行，把执行完的结果返回给前端浏览器的js，前端浏览器的js一直在等待着返回的信息，现在收到信息后，对信息进行解析和重组，渲染成我们最终看到的页面

2. 当在浏览器点击按钮的时候，浏览器里的js向后端发去一条信息，后端的nodejs写的服务接收到这条信息之后，对这条信息进行解析和响应或执行，把执行完的结果进行重组，最后保存为一份js文件或者html文件，然后返回一条信息给前端浏览器的js，提醒前端浏览器的js去信息里的地址里下载对应的文件，前端浏览器的js一直在等待着返回的信息，现在收到信息以及信息里的提醒后，会下载对应的文件，再把下载好的文件渲染成我们最终看到的页面

* 有什么区别吗！？

* 额，有的，因为这些区别，导致后面搞出来复杂的东西：

* vue框架的诞生，就是第一种情况孕育出来的畸形产物，而vue框架实际上就是一堆js代码的集合，这些代码做了什么事情呢？这些代码把后端返回的信息进行解析和重组，生成新的html或者js或者css文件，这些文件再重新渲染浏览器界面；后来，所谓的vue服务端渲染，也就是使用后端的nodejs代码写一些服务，在服务器上把原来要直接返回前端的信息截下来，然后进行解析和重组，在服务器上生成新的html或者js或者css文件，然后提醒前端浏览器下载这些文件，浏览器下载好了，再重新加载这些文件，对浏览器界面重新进行渲染，这样前端不用再去解析和重组信息了，但。。。。事实往往是更复杂的，前端的解析和重组部分还是会继续存在，后端增加了解析和重组模块，现在，模块更多了，可以把工作分的更细了，呵呵

* 为了实现上面的操作，需要是用nodejs写出更多的代码来支撑，这些代码就是 [Vue.js 服务器端渲染指南](https://ssr.vuejs.org/zh/#%E4%BB%80%E4%B9%88%E6%98%AF%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E6%B8%B2%E6%9F%93-ssr-%EF%BC%9F)

* 你需要用npm安装下面这些中间件，这些中间件也就是nodejs代码的集合，用来解析和重组处理过的信息，生成html或者js或者css或者所谓的“模版”文件，在提醒前端浏览器下载，最后在浏览器中渲染出我们所看到的页面：

1. vue & vue-server-renderer 2.3.0+
2. vue-router 2.5.0+
3. vue-loader 12.0.0+ & vue-style-loader 3.0.0+

* 说到这里，上面 vue这个体系的操作使用方式 已经与入门学习脱离太远了 呵呵

* 回到目前的项目教程，我们回归单机开发的思路，就是完全编写浏览器的js代码作为前端，编写nodejs代码作为服务器后端服务

* 我们现在在设计一个用户管理模块，设计到用户管理前端页面 和 用户管理后端服务模块

* 前端页面使用vue，使用js编写，这样，就很明了了，我们创建两个层次，一个层次放好服务端的js代码和其他服务端的资源和文件，另一个层次放前端代码，供客户端浏览器下载，渲染

* 创建 server文件夹 和 client文件夹，作用就是上面所说的

* 安排好文件结构，当前的文件结构如下

> cd server

> ls

``` txt
server client README.md
```

* server 中的文件结构是：

> cd ..

> cd client

> ls

``` txt
index.js node_modules package-lock.json package.json
```

* client 中的文件结构是：

> cd ..

> cd client

> ls

``` txt
index.html signin.html signup.html form.html account.html css
```

* 文件结构重新调整好后，需要检查和调整各个文件的引用路径

* 从 server 开始检查：

* 调整 index.js 代码

index.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();
const Router = require('koa-router');
const router = new Router();

// $ GET /package.json
app.use(serve('../client'));

//
router.get('/signin', async (ctx) => {

    var mysql = require('mysql');
    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '88888888',
        database: 'my_db'
    });

    
    connection.connect(function (err) {
        if (err) {
            console.error('error connecting: ' + err.stack);
            return;
        }
        console.log('connected as id ' + connection.threadId);
    });
    

    var response = {
        "name": ctx.query.name,
        "password": ctx.query.password
    };

    var addSql = 'SELECT * FROM ArthurSlogAccount WHERE AccountName=?';
    var addSqlParams = [response.name];

    var datas = await new Promise((resolve, reject) => {

        connection.query(addSql, addSqlParams, function (err, result) {
            if (err) {
                reject(err);
                console.log('[SELECT ERROR] - ', err.message);
                return;
            }
            if (result[0].Password == response.password) {
                resolve(result[0]);
                console.log('Welcome~ SingIn Successul ^_^' + '\\' + 'Level: ' + result[0].Level + ' Houses: ' + result[0].Houses);
            }
            if (result[0].Password != response.password) {
                reject('SingIn Fault ^_^!');
                console.log('SingIn Fault ^_^!');
            }
        });
    });

    
    if(datas){
        ctx.redirect('account.html');
    }
    
    connection.end();  
});

//
router.get('/signup', async (ctx) => {

    var mysql = require('mysql');
    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '88888888',
        database: 'my_db'
    });

    
    connection.connect(function (err) {
        if (err) {
            console.error('error connecting: ' + err.stack);
            return;
        }
        console.log('connected as id ' + connection.threadId);
    });

    var response = {
        "name": ctx.query.name,
        "password": ctx.query.password,
        "firstname": ctx.query.firstname,
        "lastname": ctx.query.lastname,
        "birthday": ctx.query.birthday,
        "sex": ctx.query.sex,
        "age": ctx.query.age,
        "wechart": ctx.query.wechart,
        "qq": ctx.query.qq,
        "email": ctx.query.email,
        "contury": ctx.query.contury,
        "address": ctx.query.address,
        "phone": ctx.query.phone,
        "websize": ctx.query.websize,
        "github": ctx.query.github,
        "bio": ctx.query.bio
    };

    var  addSql = 'INSERT INTO ArthurSlogAccount(AccountName, Password, Firstname, Lastname, Birthday, Sex, Age, Wechart, Qq, Email, Contury, Address, Phone, Websize, Github, Bio) VALUES(?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?)';
    var  addSqlParams = [response.name, response.password, response.firstname, response.lastname, response.birthday, response.sex, response.age, response.wechart, response.qq, response.email, response.contury, response.address, response.phone, response.websize, response.github, response.bio];



    ctx.body = await new Promise((resolve, reject) => {

        connection.query(addSql,addSqlParams,function (err, result) {
            if(err){
                reject(err);
                console.log('[INSERT ERROR] - ',err.message);
                return;
            }
            resolve('Singup Successful!');
        });
    });
    
    connection.end();
});

app.use(router.routes());

app.listen(3000);

console.log('listening on port 3000');

```

* 调整部分

index.js
``` js
// $ GET /package.json
app.use(serve('../client'));
```

* 切换至 server 路径下，启动静态web服务器

> node index.js

* 打开浏览器，输入 127.0.0.1:3000，测试一下网站各个功能是否正常

### 开始编码


* 至此，我们重新对文件结构进行调整。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
