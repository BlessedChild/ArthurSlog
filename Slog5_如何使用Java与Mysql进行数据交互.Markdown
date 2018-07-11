* ArthurSlog
* SLog-5
* Year·1

* Guangzhou·China
* July 11th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

做到每个敲下的按键、每次鼠标的点击、每次手机屏幕的触碰，都能产生价值

### 开发环境MacOS(High Sierra 10.13.5)

Java为了开发应用级的程序，整个开发链比较繁琐复杂，所以会需要更多的时间来掌握。

* 老规则，让我们明确一下需要的信息[Mysql官方手册](https://dev.mysql.com/doc/connector-j/8.0/en/connector-j-usagenotes-connect-drivermanager.html)

* 打开命令行，测试一下java，如果提示没有安装JDK，移步[JavaJDK下载](https://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)

* 安装完JDK，测试一下安装是否完整

> java -version

``` bash
java version "10.0.1" 2018-04-17
Java(TM) SE Runtime Environment 18.3 (build 10.0.1+10)
Java HotSpot(TM) 64-Bit Server VM 18.3 (build 10.0.1+10, mixed mode)
```

> javac -version

``` bash
javac 10.0.1
```

1. 在macOS中，JDK安装路径是/Library/Java/JavaVirtualMachines/jdk-10.jdk/Contents/Home
2. 在macOS中，JRE安装路径是/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home


* [下载Connector / J](https://dev.mysql.com/downloads/connector/j/)，选择platform Independent，选择Platform Independent (Architecture Independent), ZIP Archive下载

* 下载好Connector / J后解压文件得到文件夹，[配置 CLASSPATH](https://dev.mysql.com/doc/connector-j/8.0/en/connector-j-installing-classpath.html)

> export CLASSPATH=~/Downloads/mysql-connector-java-8.0.11.jar:$CLASSPATH

* 下面是完整代码

LoadDriver.java
``` java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;

// assume that conn is an already created JDBC connection (see previous examples)
public class LoadDriver {
    public static void main(String[] args) {
        try {
            // The newInstance() call is a work around for some
            // broken Java implementations

            Class.forName("com.mysql.cj.jdbc.Driver").newInstance();
            Connection conn = null;
            try {
                conn =
                DriverManager.getConnection("jdbc:mysql://localhost/my_db?" +
                "user=root&password=88888888");

                // Do something with the Connection

                Statement stmt = null;
                ResultSet rs = null;

                try {
                    stmt = conn.createStatement();
                    rs = stmt.executeQuery("SELECT * FROM Account");

                    // or alternatively, if you don't know ahead of time that
                    // the query will be a SELECT...

                    if (stmt.execute("SELECT * FROM Account")) {
                        rs = stmt.getResultSet();
                    }

                    // Now do something with the ResultSet ....

                    ResultSetMetaData rsmd = rs.getMetaData();
                    int columnsNumber = rsmd.getColumnCount();
                    while (rs.next()) {
                        for (int i = 1; i <= columnsNumber; i++) {
                            if (i > 1) System.out.print(",  ");
                            String columnValue = rs.getString(i);
                            System.out.print(columnValue + " " + rsmd.getColumnName(i));
                        }
                        System.out.println("");
                    }
                }
                catch (SQLException ex){
                    // handle any errors
                    System.out.println("SQLException: " + ex.getMessage());
                    System.out.println("SQLState: " + ex.getSQLState());
                    System.out.println("VendorError: " + ex.getErrorCode());
                }
                finally {
                    // it is a good idea to release
                    // resources in a finally{} block
                    // in reverse-order of their creation
                    // if they are no-longer needed

                    if (rs != null) {
                        try {
                            rs.close();
                        } catch (SQLException sqlEx) { } // ignore

                        rs = null;
                    }

                    if (stmt != null) {
                        try {
                            stmt.close();
                        } catch (SQLException sqlEx) { } // ignore

                        stmt = null;
                    }
                }

            } catch (SQLException ex) {
                // handle any errors
                System.out.println("SQLException: " + ex.getMessage());
                System.out.println("SQLState: " + ex.getSQLState());
                System.out.println("VendorError: " + ex.getErrorCode());
            }
        } catch (Exception ex) {
            // handle the error
            System.out.println("Exception: " + ex.getMessage());
        }
    }
}
```

### 执行流程如下：

1. 用java应用程序注册你的mysql jdbc驱动程序，参考[Mysql/JDBC执行SQL手册](https://dev.mysql.com/doc/connector-j/8.0/en/connector-j-usagenotes-statements.html)

``` java
Class.forName("com.mysql.cj.jdbc.Driver").newInstance()
```

2. 连接数据库

``` java
conn =DriverManager.getConnection("jdbc:mysql://localhost/my_db?" + "user=root&password=88888888")
```

3. 获得连接对象，并执行SQL指令

``` java
Statement stmt = null;
ResultSet rs = null;

stmt = conn.createStatement();
rs = stmt.executeQuery("SELECT * FROM Account");
```

4. 获得SQL执行结果，对结果进行打印

``` java
ResultSetMetaData rsmd = rs.getMetaData();
int columnsNumber = rsmd.getColumnCount();
while (rs.next()) {
                    for (int i = 1; i <= columnsNumber; i++) {
                    if (i > 1) System.out.print(",  ");
                    String columnValue = rs.getString(i);
                    System.out.print(columnValue + " " + rsmd.getColumnName(i));
                    }
                    System.out.println("");
                    }
```

* 打印SQL结果

``` java
ResultSet resultSet = statement.executeQuery("SELECT * from foo");
ResultSetMetaData rsmd = resultSet.getMetaData();
int columnsNumber = rsmd.getColumnCount();
while (resultSet.next()) {
    for (int i = 1; i <= columnsNumber; i++) {
        if (i > 1) System.out.print(",  ");
        String columnValue = resultSet.getString(i);
        System.out.print(columnValue + " " + rsmd.getColumnName(i));
    }
    System.out.println("");
}
```

* 切换到LoadDriver.java文件路径下，编译LoadDriver.java文件

> javac LoadDriver.java

* 编译生成LoadDriver.class,编译提示

``` bash
注: LoadDriver.java使用或覆盖了已过时的 API。
注: 有关详细信息, 请使用 -Xlint:deprecation 重新编译。
```

* 执行LoadDriver.class文件

> java LoadDriver

* 执行结果，打印Account表信息如下：

```
1 ID,  ArthurSlog AccountName,  ArthurSlog Password
```


* 至此，Java与MySQL成功实现了数据交互。

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢