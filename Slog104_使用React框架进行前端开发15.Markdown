# Slog104_使用React框架进行前端开发15
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-104
* Year·1

* Guangzhou·China
* October 29th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [Medium：https://medium.com/@ArthurSlog](https://medium.com/@ArthurSlog)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)



贵以贱为本 高以下为基

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

### 开始编码

* 本次来设计 ‘开发前端’ 的功能界面

* 暂时先支持PC端

* 这里我们使用React框架来搭建

* 同时引入less编译器 使用less语法来提供样式解决方案

* 整个界面主要由四个部分组成

1. 一个下拉选择栏： 用于选择测试接口（就是在开发阶段 我们选择把数据传给后端的指定接口）

2. input输入框：根据上面的选择 这里输入的是准备发给后端的数据

3. 测试按钮：当点击测试按钮的时候 会调用我们上面选中的函数 和 数据 向后端发起请求

4. 结果显示框：显示后端返回的所有数据

* 这里是开发前端的界面

![开发前端界面](https://github.com/BlessedChild/LogofAxu/blob/master/images/Slog104/%E5%BC%80%E5%8F%91%E5%89%8D%E7%AB%AF%E7%95%8C%E9%9D%A2.png?raw=true)

* 使用方式是这样的

* 首先选择下拉选择栏 选中用于后端接收数据的接口

* 然后在输入框里 输入要传给后端的数据

* 接着点击测试按钮

* 后端接受到数据之后 会反馈数据回来

* 所以 结果显示框 就会显示得到的测试结果了

![开发前端界面](https://github.com/BlessedChild/LogofAxu/blob/master/images/Slog104/%E5%BC%80%E5%8F%91%E5%89%8D%E7%AB%AF%E7%95%8C%E9%9D%A2.png?raw=true)

* 开发前端 在项目前期开发 到 项目上线之后的持续集成和功能、业务的拓展 起到了一个持续更新迭代的作用

* 将不再影响已有的功能和业务

* 在界面样式的处理上

``` less
html{
    margin: 0%;
    padding: 0%;
    width: 100%;
    font-size: 16px;
}

body{
    margin: 0%;
    padding: 0%;
    width: 100%;
}
```

* 将root节点的字体大小固定为16px

* 样式采用rem单位

* 主要的逻辑代码如下：

``` js
import React, { Component } from "react";
import { Config } from "./App";
import '../styles/Button.less';

class Button extends Component {
    constructor(props) {
        super(props)
        this.state = {
            Datas: '',
            ResponseDatas: '',
            value: '1'
        }

        this.sendDatas = this.sendDatas.bind(this);
        this.handleChange_select = this.handleChange_select.bind(this);
        this.handleChange_input = this.handleChange_input.bind(this);
    }

    // 官方对<select>的使用手册： https://reactjs.org/docs/forms.html#the-select-tag
    /*
    <select>
    <option value="grapefruit">Grapefruit</option>
    <option value="lime">Lime</option>
    <option selected value="coconut">Coconut</option>
    <option value="mango">Mango</option>
    </select>

    class FlavorForm extends React.Component {
        constructor(props) {
            super(props);
            this.state = {value: 'coconut'};

            this.handleChange = this.handleChange.bind(this);
            this.handleSubmit = this.handleSubmit.bind(this);
        }

        handleChange(event) {
            this.setState({value: event.target.value});
        }

        handleSubmit(event) {
            alert('Your favorite flavor is: ' + this.state.value);
            event.preventDefault();
        }

        render() {
            return (
            <form onSubmit={this.handleSubmit}>
                <label>
                Pick your favorite flavor:
                <select value={this.state.value} onChange={this.handleChange}>
                    <option value="grapefruit">Grapefruit</option>
                    <option value="lime">Lime</option>
                    <option value="coconut">Coconut</option>
                    <option value="mango">Mango</option>
                </select>
                </label>
                <input type="submit" value="Submit" />
            </form>
            );
        }
    }
    */
    render() {
        return (
            <div className="container">
                <div className="operateBar">
                    <div className="selectBar">
                        <div>
                            选择接口：
                    </div>
                        <div>
                            <select value={this.state.value} onChange={this.handleChange_select}>
                                <option value="0">func0</option>
                                <option value="1">func1</option>
                                <option value="2">func2</option>
                                <option value="3">func3</option>
                            </select>
                        </div>
                    </div>
                    <div className="inputBar">
                        <input className="ClientDatas" type="text" value={this.state.Datas} onChange={this.handleChange_input} placeholder="输入测试数据" />
                        <button onClick={this.sendDatas}>测试</button>
                    </div>
                </div>
                <div className="ShowBar">
                    <div className="ShowResponseDatas">
                        {this.state.ResponseDatas}
                    </div>
                </div>
            </div>
        );
    }

    handleChange_select(event) {
        this.setState({
            value: event.target.value
        });
    }

    handleChange_input(event) {
        this.setState({
            Datas: event.target.value
        });
    }

    sendDatas() {
        // let Datas = document.getElementsByClassName("ClientDatas").value

        /*
        转换函数：parseInt()和parseFloat()分别将值转换成整数和浮点数
        强制类型转换：Boolean(value)、Number(value)、String(value)将给定的值分别转换成逻辑值、数字（整数或浮点数）及字符串
        弱类型自动转换：字符串与数字进行数学操作符运算时，字符串会自动转为数字
        */
        const myObj = { func: parseInt(this.state.value), object: this.state.Datas }
        fetch(Config.serverAddress + 'api/client', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(myObj),
        })
            .then(response => {
                console.log('Add data to message successfuly')
                // 这里获取到了服务端返回的‘公告栏’的数据 resmsg
                const resmsg = response.json()
                console.log('Response1: ', resmsg)
                console.log('Response2: ', response)
                return resmsg
            })
            .then(resmsg => {
                // 然后 传值给‘公告栏’
                // 接着 重新渲染（局部渲染）页面
                // 语法 查一下setState里怎么使用对象
                this.setState({
                    ResponseDatas: resmsg
                })
            })
            .catch(err => {
                alert("Error in sending data to server: " + err.message)
            })
    }
}

export default Button;
```

* 这里使用的请求函数 与 ‘客户端前端’ 里的请求函数是一样的

* 后面把这些频繁使用的功能函数打包起来 降低开发成本

* 工程文件已经上传至[Github：https://github.com/BlessedChild/ArthurSlogStore](https://github.com/BlessedChild/ArthurSlogStore)

* 至此，完成了‘开发前端’的界面和功能的开发。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
