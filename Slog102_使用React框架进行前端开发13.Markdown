# Slog102_使用React框架进行前端开发13
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-102
* Year·1

* Guangzhou·China
* October 26th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

曲则全 枉则直 洼则盈 敝则新 少则多 多则惑

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* [require: https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_require](https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_require)

* [module: https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_module](https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_module)

* [export: https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_exports](https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_exports)

* [path: https://www.npmjs.com/package/path](https://www.npmjs.com/package/path)

### 开始编码

* 本次为后端服务添加了 基础的数据库操作

* 实现基本的CRUD函数

* 代码如下：

server/main.js
``` js
// 数据操作函数区
// 数据库和集合： https://docs.mongodb.com/manual/core/databases-and-collections/

// Create database
// 创建数据库
// 在 MongoDB 中创建一个数据库 需要创建一个 MongoClient 对象
// 不指定数据库名 默认打开 test 数据库
// 然后指定数据库的 URL 和 端口
// 当数据库不存在时 MongoDB 会根据你给的 数据库名 创建新的数据库并建立连接
function create_MongodbDatabase(config) {
    MongoClient.connect(config.databaseBaseUrl)
        .then(connection => {
            // Connect specified database
            // 连接指定的数据库
            return connection.db(config.databaseName)
        })
        .then(db => {
            // Returns the name of the current database
            // 返回当前数据库的名称
            console.log('数据库' + db.getName() + '创建成功')
            console.log('--------------------')
            return db
        })
        .then(db => {
            db.close()
        })
        .catch(err => {
            console.log('Error: ' + err)
            console.log('--------------------')
        })
}

// Create collection
// 创建集合（如果数据库和集合都不存在 那么会根据指定的数据库名和集合名创建新的数据库和集合）
// 有三种方式创建集合，例如：
// db.myNewCollection2.insertOne( { x: 1 } )
// db.myNewCollection3.createIndex( { y: 1 } )
// db.createCollection(name, options)
// options 的约定 请参考：https://docs.mongodb.com/manual/reference/method/db.createCollection/#db.createCollection
// 在 MongoDB 的数据库中创建一个集合 需要创建一个 MongoClient 对象
// 然后指定数据库的 URL 和 端口
// 然后使用 createCollection() 方法来创建集合
function create_MongodbCollection(config) {
    MongoClient.connect(config.databaseBaseUrl)
        .then(connection => {
            // Connect specified database
            // 连接指定的数据库
            return connection.db(config.databaseName)
        })
        .then(db => {
            console.log('成功连接到' + '数据库' + db.getName())
            return db
        })
        .then(db => {
            db.createCollection('Slog')
            return db
        })
        .then(db => {
            console.log('集合创建成功')
            console.log('--------------------')
            db.close()
        })
        .catch(err => {
            console.log('Error: ' + err)
            console.log('--------------------')
        })
}

// Document operate
// 文档操作
// 与 MySQL 不同的是 MongoDB 会自动创建数据库和集合
// 所以使用前我们不需要手动去创建
// 向集合插入文档（document）
// 例如：
// document = { name: "ArthurSlog", url: "https://www.arthurslog.com" }
function create_MongodbDocument(collection, document) {
    MongoClient.connect(config.databaseBaseUrl)
        .then(() => {
            // Connect specified database
            // 连接指定的数据库
            return connection.db(config.databaseName)
        })
        .then(db => {
            console.log('成功连接到' + '数据库' + db.getName())
            return db
        })
        .then(db => {
            console.log('正在向集合 ' + collection + ' 插入文档...')
            db.collection(collection).insertOne(document)
                .then(result => {
                    console.log('文档插入成功')
                    console.log('插入结果 => ')
                    console.log(result)
                    console.log('--------------------')
                })
        })
}

// 查询数据
// 查询条件： condition
// 例如：condition = {name:'ArthurSlog'}
function read_MongodbDocument(collection, condition) {
    MongoClient.connect(config.databaseBaseUrl)
        .then(() => {
            // Connect specified database
            // 连接指定的数据库
            return connection.db(config.databaseName)
        })
        .then(db => {
            console.log('成功连接到' + '数据库' + db.getName())
            return db
        })
        .then(db => {
            console.log('正在集合查询 ' + collection + ' 里的文档...')
            db.collection(collection).find(condition).toArray()
                .then(result => {
                    console.log('查询成功')
                    console.log('查询结果 => ')
                    console.log(result)
                    console.log('--------------------')
                })
        })
}

// 更新数据
// 查询条件： condition
// 例如：condition = {name:'ArthurSlog'}
// 更新动作： updateAction
// 例如：updateAction = {$set: { url : "https://www.arthurslog.com" }}
function upade_MongodbDocument(collection, condition, updateAction) {
    MongoClient.connect(config.databaseBaseUrl)
        .then(() => {
            // Connect specified database
            // 连接指定的数据库
            return connection.db(config.databaseName)
        })
        .then(db => {
            console.log('成功连接到' + '数据库' + db.getName())
            return db
        })
        .then(db => {
            console.log('正在更新集合 ' + collection + ' 中的文档')
            db.collection(collection).updateOne(condition, updateAction)
                .then(result => {
                    console.log('文档更新成功')
                    console.log('更新结果 => ')
                    console.log(result)
                    console.log('--------------------')
                })
        })
}

// 移除数据
// 查询条件： condition
// 例如：condition = {name:'ArthurSlog'}
function delete_MongodbDocument(collection, condition) {
    MongoClient.connect(config.databaseBaseUrl)
        .then(() => {
            // Connect specified database
            // 连接指定的数据库
            return connection.db(config.databaseName)
        })
        .then(db => {
            console.log('成功连接到' + '数据库' + db.getName())
            return db
        })
        .then(db => {
            console.log('正在集合 ' + collection + ' 中移除文档')
            db.collection(collection).deleteOne(condition)
                .then(result => {
                    console.log('文档移除成功')
                    console.log('移除结果 => ')
                    console.log(result)
                    console.log('--------------------')
                })
        })
}

// 排序： 
// 按 type 字段升序
// sort_Mongodb = { type: 1 }  
// 按 type 字段降序
// sort_Mongodb = { type: -1 } 
// 例如：
// db.collection(collection).find().sort(sort_Mongodb).toArray()
// 对查询到的结果进行排序：

// 查询数据
// 查询条件： condition
// 例如：condition = {name:'ArthurSlog'}
function read_MongodbDocument(collection, condition, sort_Mongodb) {
    MongoClient.connect(config.databaseBaseUrl)
        .then(() => {
            // Connect specified database
            // 连接指定的数据库
            return connection.db(config.databaseName)
        })
        .then(db => {
            console.log('成功连接到' + '数据库' + db.getName())
            return db
        })
        .then(db => {
            console.log('正在集合查询 ' + collection + ' 里的文档...')
            db.collection(collection).find(condition).sort(sort_Mongodb).toArray()
                .then(result => {
                    console.log('排序成功')
                    console.log('排序结果' + '(' + ((sort_Mongodb == 1) ? '升序' : '降序') + ')' +  ' => ')
                    console.log(result)
                    console.log('--------------------')
                })
        })
}

// 分页： 
// 查询的返回条数：limit_Mongodb

// 查询数据
// 查询条件： condition
// 例如：condition = {name:'ArthurSlog'}
function read_MongodbDocument(collection, condition, limit_Mongodb) {
    MongoClient.connect(config.databaseBaseUrl)
        .then(() => {
            // Connect specified database
            // 连接指定的数据库
            return connection.db(config.databaseName)
        })
        .then(db => {
            console.log('成功连接到' + '数据库' + db.getName())
            return db
        })
        .then(db => {
            console.log('正在集合查询 ' + collection + ' 里的文档...')
            db.collection(collection).find(condition).limit(limit_Mongodb).toArray()
                .then(result => {
                    console.log('查询成功')
                    console.log('查询结果 => ')
                    console.log(result)
                    console.log('--------------------')
                })
        })
}
```

* 同时对程序的入口点进行了更新

server/main.js
``` js
// Enter point
// 程序的入口点
// Connect database base Url
// 连接数据库的基地址（连接成功后才连接指定的数据库）
MongoClient.connect(config.databaseBaseUrl, { useNewUrlParser: true })
    .then(connection => {
        // Connect specified database
        // 连接指定的数据库
        db = connection.db(config.databaseName)
    })
    .then(() => {
        // Start server 
        // 启动服务
        app.listen(config.serverPort, () => {
            console.log('Server start on port: ' + config.serverPort)
        })
    })
    .catch(err => {
        // Print error informations on console
        // 打印出错信息
        console.log('Error: ', err)
    })
```

* 前端页面进行测试 之前的功能保持正常

* 不过新增的函数还没有经过测试 下篇进行测试报告

* 目前 全局配置是放在main.js的一个对象里

server/main.js
``` js
// 引入路径方案解决第三方包
// path.join()方法path使用特定于平台的分隔符作为分隔符将所有给定的段连接在一起 然后规范化生成的路径
// 零长度path段会被忽略 如果连接的路径字符串是零长度字符串 则返回'.' 表示当前工作目录
const path = require('path')

// 这里config作为一个object 所以使用{}
const config = {
    jsUrl: path.join(__dirname, "/src/js"),
    imgUrl: path.join(__dirname, "/src/public/img"),
    // 公告栏显示的信息
    BulletinBoardMsg: '[欢迎来到ArthurSlogStore]_当前时间是： ',
    serverPort: 3000,
    databaseBaseUrl: 'mongodb://localhost:27017',
    databaseName: 'issuetracker'
}
// 导出工程的配置文件
module.exports = config
```

* 一些详细的解释和参考 包含在代码注释里面

* 工程文件已经上传至[Github：https://github.com/BlessedChild/ArthurSlogStore](https://github.com/BlessedChild/ArthurSlogStore)

* 至此，开始了后端数据库CURD基础函数的持续构建。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
