# 数据库的连接用Java

## 第一步注册驱动

```java
Class.forName("com.mysql.cj.jdbc.Driver");
```

## 第二步创建用户密码，和具体的url

```java
static String name = "root";
static String password = "123456";
```

```java
static final String DB_URL = "jdbc:mysql://localhost:3306/itheima?     //3306的后面接着自己创建的数据库 //useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC";
```

## 注意如果禅道开启的，请关闭禅道服务。

![image-20230112095855472](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230112095855472.png)

## 第三步 设置连接器和接收器

```Java
Connection conn = null;
Statement stmt = null;
```

## 第四部 直接连接

```java
System.out.println("连接数据库...");
conn = DriverManager.getConnection(DB_URL, name, password);
```

连接结果成功

![image-20230112100048363](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230112100048363.png)

# 完整代码

```java
package dao;
import com.mysql.cj.jdbc.Driver;

import java.sql.*;

public class userdao {

    static String name = "root";
    static String password = "123456";
    static final String JDBC_DRIVER = "com.mysql.cj.jdbc.Driver";
    static final String DB_URL = "jdbc:mysql://localhost:3306/itheima?     useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC";
    public static void main(String[] args) {
        Connection conn = null;
        Statement stmt = null;
        try {
            // 注册 JDBC 驱动
            Class.forName(JDBC_DRIVER);

            // 打开链接
            System.out.println("连接数据库...");
            conn = DriverManager.getConnection(DB_URL, name, password);


        }catch (Exception e){
            e.printStackTrace();
        }
    }
}
```

## 如果不关禅道的话，结果如下

![image-20230112100355577](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230112100355577.png)

![image-20230112100437024](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230112100437024.png)

## 这个禅道直接就抢了mysql的端口号

```Java
conn = DriverManager.getConnection(DB_URL, name, password);
//数据库查询语句
String sql = "select * from user";//要执行的SQL   
stmt  = conn.createStatement();//创建一个Statement对象   ;表对象
/*在询数据表时，需要用到ResultSet接口，它类似于一个数据表，通过该接口的实例可以获得检索结果集，以及对应数据表的接口信息。*/
ResultSet rs = stmt.executeQuery(sql);//创建数据对象    ;根据查询的字符串来提取数据

System.out.println("编 号"+"\t"+"姓 名"+"\t"+"密 码"+"\t"+"工资");
while (rs.next()) {
    System.out.print(rs.getInt(1)+"\t");
    System.out.print(rs.getString(2)+"\t");
    System.out.print(rs.getInt(3)+"\t");
    System.out.print(rs.getInt(4)+"\t");
    System.out.println();
}
```

# 预处理，？占位符

```java
import org.junit.Test;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class Test003 {
    @Test
    public void test003(){
        String sql="name=?";
        try {
            Connection con= DriverManager.getConnection("jdbc:127.0.0.1:3306&itheima");
            PreparedStatement statement=con.prepareStatement(sql);
            statement.setString(1,"caoyanglin");
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }

    }
}
```

# JDBC代码解释

```java
import org.junit.Test;

import java.sql.*;

public class Test003 {
    @Test
    public void test003(){
        String sql="name=?";    
        try {
            Connection con= DriverManager.getConnection("jdbc:127.0.0.1:3306&itheima");   //获取连接
            PreparedStatement preparedStatementstatement=con.prepareStatement(sql);      //预处理
            Statement statement = con.createStatement();                                 //获得执行对象
            statement.execute(sql);                                                      //执行对象执行sql语句
            con.setAutoCommit(false);                                                    //关闭事务
            con.commit();                                                                //提交事务
            preparedStatementstatement.setString(1,"caoyanglin");                        //预处理处理占位符
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }

    }
}

```





























