* ArthurSlog
* SLog-2
* Year·1

* Guangzhou·China
* July 8th 2018
![关注微信公众号“环游的球”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

想让别人拉你一把，你的手在哪？别想着拉别人一把，否则你也会被拖垮。

### 开发环境MacOS
Mac自带的编译器，可以直接编译C语言的代码。所以现在，打开你的手机，计时5分钟，[编译器](https://zh.wikipedia.org/wiki/編譯器)了解一下

有点常识 最原始的信息一般都是最有效的信息

如果面向百度或者QQ编程，那趁早转行

在Mysql的官网获取C与Mysql的交互手册[Mysql官方手册](https://dev.mysql.com/doc/refman/8.0/en/c-api.html)

* 下面这段话是智商的分水岭

The MySQL C API is a C-based API that client applications written in C can use to communicate with MySQL Server.Client programs refer to C API header files at compile time and link to a C API library file, libmysqlclient, at link time.

* 这段话就是实现C与Mysql数据交互的关键 如果你看不懂 说明你想的太多 做的太少

### 提醒：当你想进步的时候，第一时间打开官方手册
官方文档一般都不会考虑菜鸟们的阅读感受 所以 作为一只🙃菜鸟 要有点灵性

下面是在MySQL官网找到的一个具体的调用流程：

* step1 初始化MySQL客户端库，mysql_library_init()。

* step2 初始化MySQL对象，mysql_init()；并连接到服务器， mysql_real_connect()。

* step3 发出SQL语句并处理其结果，mysql_eqery()。

* step4 关闭与MySQL服务器的连接，mysql_close()。

* step5 结束使用MySQL客户端库，mysql_library_end()。

下面main.c是完整的C代码（1分钟浏览一下）， 关键是上面提到的五个步骤，函数的用法参考[Mysql官方手册](https://dev.mysql.com/doc/refman/8.0/en/c-api-function-overview.html)

main.c
``` c
#include <stdio.h>
#include <mysql.h>
#include <stdlib.h>

MYSQL mysql;
MYSQL_RES *result;
MYSQL_ROW row;
unsigned int num_fields;
unsigned int i;
const char host_name[] = "localhost";
const char user_name[] = "root";
const char password[] = "888888";
const char db_name[] = "my_db";
unsigned int port_num = 0;
unsigned long CLIENT_MULTI_STATMENTS = 0;

int main(void)
{
    /* step1 int mysql_library_init(int argc, char **argv, char **groups) */
    if (mysql_library_init(0, NULL, NULL))
    {
        fprintf(stderr, "could not initialize MySQL client library\n");
        exit(1);
    }

    /* step2 MYSQL *mysql_init(MYSQL *mysql) */
    mysql_init(&mysql);

    /* step2 MYSQL *mysql_real_connect(MYSQL *mysql, const char *host, const char *user, const char *passwd, const char *db, unsigned int port, const char *unix_socket, unsigned long client_flag) */
    if (mysql_real_connect(&mysql, host_name, user_name, password,
                           db_name, port_num, NULL, CLIENT_MULTI_STATEMENTS) == NULL)
    {
        printf("mysql_real_connect() failed\n");
        fprintf(stderr, "Failed to connect to database: Error: %s\n", mysql_error(&mysql));
        mysql_close(&mysql);
        exit(1);
    }

    /* step3 int mysql_query(MYSQL *mysql, const char *stmt_str) */
    int status = mysql_query(&mysql, "SELECT * FROM Account"); /* int mysql_query(MYSQL *mysql, const char *stmt_str) */

    if (status)
    {
        printf("Could not execute statement(s)");
        mysql_close(&mysql);
        exit(0);
    }

    /* process each statement result */
    do
    {
        /* did current statement return data? */
        /* MYSQL_RES *mysql_store_result(MYSQL *mysql) */
        result = mysql_store_result(&mysql);
        if (result)
        {
            /* unsigned int mysql_num_fields(MYSQL_RES *result) */
            num_fields = mysql_num_fields(result);
            /* MYSQL_ROW mysql_fetch_row(MYSQL_RES *result) */
            while ((row = mysql_fetch_row(result)))
            {
                unsigned long *lengths;
                lengths = mysql_fetch_lengths(result);
                for (i = 0; i < num_fields; i++)
                {
                    printf("[%.*s] ", (int)lengths[i],
                           row[i] ? row[i] : "NULL");
                }
                printf("\n");
            }
            /* yes; process rows and free the result set */
            /* process_result_set(mysql, result); */
            mysql_free_result(result) /* void mysql_free_result(MYSQL_RES *result) */;
        }
        else /* no result set or error*/
        {
            /* unsigned int mysql_field_count(MYSQL *mysql) */
            if (mysql_field_count(&mysql) == 0)
            {
                printf("lld rows affected\n");
                break;
            }
        }
        /* more results? -1 = no, >0 = error, 0 = yes (keep looping) */
        if ((status = mysql_next_result(&mysql)) > 0) /* int mysql_next_result(MYSQL *mysql) */
        {
            printf("Counld not execute statement\n");
        }
    } while (status == 0);

    /* step4 void mysql_close(MYSQL *mysql) */
    mysql_close(&mysql);

    /* step5 void mysql_library_end(void) */
    mysql_library_end();

    return EXIT_SUCCESS;
}
```

* 英文看不懂? 
* [google翻译](https://translate.google.cn)， [chrome](https://www.google.com/chrome/) ，[字典](https://item.jd.com/12987669974.html) 了解一下

* 流程代码分5个step

main.c
``` c
    /* step1 int mysql_library_init(int argc, char **argv, char **groups) */
    if (mysql_library_init(0, NULL, NULL))
    {
        fprintf(stderr, "could not initialize MySQL client library\n");
        exit(1);
    }

    /* step2 MYSQL *mysql_init(MYSQL *mysql) */
    mysql_init(&mysql);
    /* step2 MYSQL *mysql_real_connect(MYSQL *mysql, const char *host, const char *user, const char *passwd, const char *db, unsigned int port, const char *unix_socket, unsigned long client_flag) */
    if (mysql_real_connect(&mysql, host_name, user_name, password,
                           db_name, port_num, NULL, CLIENT_MULTI_STATEMENTS) == NULL)
    {
        printf("mysql_real_connect() failed\n");
        fprintf(stderr, "Failed to connect to database: Error: %s\n", mysql_error(&mysql));
        mysql_close(&mysql);
        exit(1);
    }

    /* step3 int mysql_query(MYSQL *mysql, const char *stmt_str) */
    int status = mysql_query(&mysql, "SELECT * FROM Account"); /* int mysql_query(MYSQL *mysql, const char *stmt_str) */
    if (status)
    {
        printf("Could not execute statement(s)");
        mysql_close(&mysql);
        exit(0);
    }

    /* step4 void mysql_close(MYSQL *mysql) */
    mysql_close(&mysql);

    /* step5 void mysql_library_end(void) */
    mysql_library_end();
```

* 这里面涉及到的C语法，google了解一下

* 上面的代码走完一个流程就算完了，但实际情况是需要‘增删改查’
* So

main.c
``` c
    /* process each statement result */
    do
    {
        /* did current statement return data? */
        /* MYSQL_RES *mysql_store_result(MYSQL *mysql) */
        result = mysql_store_result(&mysql);
        if (result)
        {
            /* unsigned int mysql_num_fields(MYSQL_RES *result) */
            num_fields = mysql_num_fields(result);
            /* MYSQL_ROW mysql_fetch_row(MYSQL_RES *result) */
            while ((row = mysql_fetch_row(result)))
            {
                unsigned long *lengths;
                lengths = mysql_fetch_lengths(result);
                for (i = 0; i < num_fields; i++)
                {
                    printf("[%.*s] ", (int)lengths[i],
                           row[i] ? row[i] : "NULL");
                }
                printf("\n");
            }
            /* yes; process rows and free the result set */
            /* process_result_set(mysql, result); */
            mysql_free_result(result) /* void mysql_free_result(MYSQL_RES *result) */;
        }
        else /* no result set or error*/
        {
            /* unsigned int mysql_field_count(MYSQL *mysql) */
            if (mysql_field_count(&mysql) == 0)
            {
                printf("lld rows affected\n");
                break;
            }
        }
        /* more results? -1 = no, >0 = error, 0 = yes (keep looping) */
        if ((status = mysql_next_result(&mysql)) > 0) /* int mysql_next_result(MYSQL *mysql) */
        {
            printf("Counld not execute statement\n");
        }
    } while (status == 0);
```
* 根据Mysql官方手册
* 在代码间，当一个函数执行后会返回一个结果，这个结果的数据结构各不相同，参考[Mysql官方手册](https://dev.mysql.com/doc/refman/8.0/en/c-api-function-overview.html)
* 举个例子栗子：

main.c
``` c
mysql_library_init()
```
* 完整的写法

main.c
``` c
int mysql_library_init(int argc, char **argv, char **groups)
```
* 第一个 int，代表的就是返回值的数据结构
* 如果要储存这个函数执行完返回的值，需要声明一个相同的数据结构的对象来保存这个值
* 举个栗子：

main.c
``` c
int return_mli = null; //声明一个数据结构为int的对象，并让reture_mli的值为空
```
* 然后你就可以

main.c
``` c
int return_mli = null;
return_mli = mysql_library_init(0, NULL, NULL);
```
* 此时你就可以判断函数的返回值，以确定接下来要执行的操作
* C 语言把任何非零和非空的值假定为 true，把零或 null 假定为 false。

main.c
``` c
int return_mli = 0;
return_mli = mysql_library_init(0, NULL, NULL);

if(return_mli)
{
    do something
}
```

* 明白了这些，再次看一下完整的代码

main.c
``` c
#include <stdio.h>
#include <mysql.h>
#include <stdlib.h>

MYSQL mysql;
MYSQL_RES *result;
MYSQL_ROW row;
unsigned int num_fields;
unsigned int i;
const char host_name[] = "localhost";
const char user_name[] = "root";
const char password[] = "888888";
const char db_name[] = "my_db";
unsigned int port_num = 0;
unsigned long CLIENT_MULTI_STATMENTS = 0;

int main(void)
{
    /* step1 int mysql_library_init(int argc, char **argv, char **groups) */
    if (mysql_library_init(0, NULL, NULL))
    {
        fprintf(stderr, "could not initialize MySQL client library\n");
        exit(1);
    }

    /* step2 MYSQL *mysql_init(MYSQL *mysql) */
    mysql_init(&mysql);

    /* step2 MYSQL *mysql_real_connect(MYSQL *mysql, const char *host, const char *user, const char *passwd, const char *db, unsigned int port, const char *unix_socket, unsigned long client_flag) */
    if (mysql_real_connect(&mysql, host_name, user_name, password,
                           db_name, port_num, NULL, CLIENT_MULTI_STATEMENTS) == NULL)
    {
        printf("mysql_real_connect() failed\n");
        fprintf(stderr, "Failed to connect to database: Error: %s\n", mysql_error(&mysql));
        mysql_close(&mysql);
        exit(1);
    }

    /* step3 int mysql_query(MYSQL *mysql, const char *stmt_str) */
    int status = mysql_query(&mysql, "SELECT * FROM Account"); /* int mysql_query(MYSQL *mysql, const char *stmt_str) */

    if (status)
    {
        printf("Could not execute statement(s)");
        mysql_close(&mysql);
        exit(0);
    }

    /* process each statement result */
    do
    {
        /* did current statement return data? */
        /* MYSQL_RES *mysql_store_result(MYSQL *mysql) */
        result = mysql_store_result(&mysql);
        if (result)
        {
            /* unsigned int mysql_num_fields(MYSQL_RES *result) */
            num_fields = mysql_num_fields(result);
            /* MYSQL_ROW mysql_fetch_row(MYSQL_RES *result) */
            while ((row = mysql_fetch_row(result)))
            {
                unsigned long *lengths;
                lengths = mysql_fetch_lengths(result);
                for (i = 0; i < num_fields; i++)
                {
                    printf("[%.*s] ", (int)lengths[i],
                           row[i] ? row[i] : "NULL");
                }
                printf("\n");
            }
            /* yes; process rows and free the result set */
            /* process_result_set(mysql, result); */
            mysql_free_result(result) /* void mysql_free_result(MYSQL_RES *result) */;
        }
        else /* no result set or error*/
        {
            /* unsigned int mysql_field_count(MYSQL *mysql) */
            if (mysql_field_count(&mysql) == 0)
            {
                printf("lld rows affected\n");
                break;
            }
        }
        /* more results? -1 = no, >0 = error, 0 = yes (keep looping) */
        if ((status = mysql_next_result(&mysql)) > 0) /* int mysql_next_result(MYSQL *mysql) */
        {
            printf("Counld not execute statement\n");
        }
    } while (status == 0);

    /* step4 void mysql_close(MYSQL *mysql) */
    mysql_close(&mysql);

    /* step5 void mysql_library_end(void) */
    mysql_library_end();

    return EXIT_SUCCESS;
}
```

* 接下来切换至代码路径下
* 执行编译指令
> gcc -c main.c -I /usr/local/mysql/include
* 执行链接指令，得到执行文件main
> gcc main.o -o main -L /usr/local/mysql/lib -lmysqlclient
* 此时当前路径下有这三个文件

``` c
main.c main.o main
```

* 启动可执行文件main
> ./main

* 此时会提示出错，解决办法第一时间应该想到的是[Mysql官方手册](https://dev.mysql.com/doc/refman/8.0/en/c-api-running-clients.html)
* 根据官方提供的信息，可以推断是系统链接的问题。google可得，由于MacOS系统的保护机制，解决方式如下：
> ln -s /usr/local/mysql/lib/libmysqlclient.21.dylib /usr/local/lib/libmysqlclient.21.dylib

* 最后，启动可执行文件main
> ./main

* 前提是你配置好了数据库参数，下面是我自己配置的数据库信息

``` c
const char host_name[] = "localhost";
const char user_name[] = "root";
const char password[] = "888888";
const char db_name[] = "my_db";

int status = mysql_query(&mysql, "SELECT * FROM Account"); /* int mysql_query(MYSQL *mysql, const char *stmt_str) */
```

* SQL语法不懂？[SQL手册](https://www.w3schools.com/sql/)了解一下

``` c
SELECT * FROM Account
```

* 至此，我们使用C语言与MySQL数据库成功实现了数据交互。

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢