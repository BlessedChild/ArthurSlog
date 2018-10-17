# Slog98_项目上线之ArthurSlog个人网站上线5
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-98
* Year·1

* Guangzhou·China
* September 17th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

摆脱点对点的方式 实现点对多的方式 让你的收益成倍放大

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* [阿里云免费SSL证书申请](https://yundun.console.aliyun.com)

* [https部署](https://help.aliyun.com/knowledge_detail/44596.html?spm=a2c4g.11186623.2.17.34bb4593rYckAu)

### 开始编码

* 登陆阿里云控制台 点击左侧的 ‘云盾控制台概述’ 

* 点击 ‘证书服务’ 

* 点击 ‘购买证书’

* 点击 ‘symantec’ 然后随便点一下证书类型里的任意选项

* 这个时候才会出现 ‘免费型DV SSL’

* OK 可以购买了

* 接着绑定自己的域名 例如 ‘www.arthurslog.com’

* 如果你的服务器和域名都在阿里云 那么 那你可以选择DNS验证 并勾选下面的‘勾勾’ 阿里云的后台系统会自动验证

* 接着 选择 nginx服务器类型的证书下载

* 之前我是直接用express框架裸写了一个 web服务器

* 现在换nginx

* 我的服务器系统是CentOS 7+

* So 

* 登陆服务器 安装nginx

> yum install nginx

> yum install openssl

> yum install pcre

> yum install zlib

* 虽然Centos 7+ 已经有安装过上述依赖了

* 不过还是再来一次 确保一切正常

* 安装完了之后

* 切换至nginx安装路径下

> cd etc/nginx/

* 新建一个文件夹 cert

> mkdir cert

* 上传刚刚下载的ssl证书文件至 cert路径下

> scp -r 本地证书路径 root@服务器地址：/etc/nginx/cert

* 成功上传之后 需要更新nginx配置文件

* 参考 阿里云官方文档 [https://yundun.console.aliyun.com/?spm=5176.2020520110.all.12.3d5856a1xvsKvM&p=cas#/cas/download/215075710400981?regionId=](https://yundun.console.aliyun.com/?spm=5176.2020520110.all.12.3d5856a1xvsKvM&p=cas#/cas/download/215075710400981?regionId=)

``` txt
server {
    listen 443;
    server_name localhost;
    ssl on;
    root html;
    index index.html index.htm;
    ssl_certificate   cert/215075710400981.pem;
    ssl_certificate_key  cert/215075710400981.key;
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    location / {
        root html;
        index index.html index.htm;
    }
}
```

* 关键就这两个

``` txt
ssl_certificate   cert/215075710400981.pem;
ssl_certificate_key  cert/215075710400981.key;
```

* 接着

> service nginx start

* 上面直接启动nginx 然后

* 打开浏览器 输入域名 arthurslog.com 

* 你会发现 地址栏并没有发生变化.. 依旧是 http开头

* 调整nginx配置文件nginx.conf

* 在配置文件里添加一行

``` txt
server {
  ...
  server_name localhost;

  rewrite ^(.*)$ https://$host$1 permanent; 

  ...
```

* 重新打开浏览器 输入域名 arthurslog.com 

* 现在地址栏已经变成 https开头了

* 现在显示的 nginx的默认页面 

* 修改nginx配置文件 把主页路径指向我自己的主页

``` text
server {
  ...
  server_name localhost;

  root  自己网站主页的路径

  ...
```

* 记得 80端口和443端口都需要配置root参数

* Ok 重启nginx

> service nginx restart

* ok，现在用自己的电脑打开浏览器，输入域名 www.arthurslog.com

* 正常情况下，可以看到自己的网站主页了

* 同时 地址栏也成功变成了 https 开头的了

![https://www.arthurslog.com](https://github.com/BlessedChild/LogofAxu/blob/master/images/Slog98/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202018-10-17%20%E4%B8%8A%E5%8D%887.35.45.png?raw=true)

* 至此，我的个人网站 [http://www.ArthurSlog.com](www.ArthurSlog.com) 成功更新为 [https://www.ArthurSlog.com](https://www.ArthurSlog.com)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
