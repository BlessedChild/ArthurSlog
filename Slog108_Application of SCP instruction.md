![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

[Arthurslog.com](http://www.arthurslog.com)/[@Medium](https://medium.com/@ArthurSlog)/[@GitHub](https://github.com/BlessedChild/ArthurSlog)

Slog108｜Year·5

Guangzhou China
May 13th 2023

# Application of SCP instruction（技能：SCP指令的应用、向服务器上传数据）

远程拷贝文件或文件夹
在 Mac 上的“终端” App  中，使用 scp 命令在电脑间远程拷贝文件或文件夹。

scp 使用同 ssh 一样的底层协议。

例如，若要从您的个人文件夹将压缩文件拷贝到远程服务器上另一个用户的个人文件夹：

% scp -E ~/ImportantPapers.tgz username@remoteserver.com:/Users/username/Desktop/ImportantPapers.tgz

您会收到输入用户密码的提示。

-E 旗标保留扩展属性、资源分支和 ACL 信息。

-r 旗标（未在本示例中使用）使 scp 拷贝文件夹及其内容。

**Refrence**
https://support.apple.com/zh-cn/guide/terminal/apddfb31307-3e90-432f-8aa7-7cbc05db27f7/2.11/mac/11.0

---

> Sometimes it’s hard and it sucks, but there’s always a way…

Thanks to the friends who provided valuable information