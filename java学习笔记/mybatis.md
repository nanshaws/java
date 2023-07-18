# xml文件的符号禁区

在 XML 中有 5 个预定义的实体引用：
&lt;        <       小于
&gt;        >       大于
&amp;       &       和号
&apos;      '       省略号
&quot;      "       引号

<![CDATA[2特殊符号3]]>

注释：严格地讲，在 XML 中仅有字符 “<”和”&” 是非法的。省略号、引号和大于号是合法的，但是把它们替换为实体引用是个好的习惯。

```java
&lt;        <       小于
&gt;        >       大于
&amp;       &       和号
&apos;      '       省略号
&quot;      "       引号
```

# 核心文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="mysql">

        <environment id="mysql">
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/itheima?useSSL=false&amp;allowPublicKeyRetrieval=true&amp;serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <!--资源配置-->
        <mapper resource="Student-mapp.xml"/>

    </mappers>
</configuration>
```

# 资源文件，可以说是操作文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">        <!--使用操作就是namespace.id-->       
<mapper namespace="Student-mapp">
     <select id="selectAll" resultType="org.example.Student"> <!--resultType输出的对象放在=的右边-->
         SELECT * from student                                <!--同时等号右边那个类要配置mysql相应属性-->
     </select>
</mapper>
```

# mybatis连接数据库

```
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.example.Student;
import org.junit.Test;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class StudentTest {
    @Test
    public void selectAll(){
        try {
            //加载核心配置文件
            InputStream resource = Resources.getResourceAsStream("MyBatisConfig.xml");
            //获取SqlSession工厂对象
            SqlSessionFactory sqlSessionFactory=new SqlSessionFactoryBuilder().build(resource);
            //通过工厂对象获取SqlSession
            SqlSession sqlSession= sqlSessionFactory.openSession();
            List<Student> list = sqlSession.selectList("Student-mapp.selectAll");
            //处理结果
            for (Student stu:list){
                System.out.println(stu);

            }
            sqlSession.close();
            resource.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
}
```

# Student的属性类

```java
package org.example;

import dao.StudentTest;

import java.io.Serializable;
import java.util.Date;

public class Student implements Serializable {
    private String Sno;
    private String Sname;
    private String Ssex;
    private Date Sbirthday;           //一般来说只需要配置这些属性即可，那些方法都不重要
    private String Class;

    public Student() {
    }

    public void setSno(String sno) {
        Sno = sno;
    }

    public void setSname(String sname) {
        Sname = sname;
    }

    public void setSsex(String ssex) {
        Ssex = ssex;
    }

    public void setSbirthday(Date sbirthday) {
        Sbirthday = sbirthday;
    }

    public void setClass(String aClass) {
        Class = aClass;
    }

    public String getSno() {
        return Sno;
    }

    public String getSname() {
        return Sname;
    }

    public String getSsex() {
        return Ssex;
    }

    public Date getSbirthday() {
        return Sbirthday;
    }

    @Override
    public String toString() {
        return "Student{" +
                "Sno='" + Sno + '\'' +
                ", Sname='" + Sname + '\'' +
                ", Ssex='" + Ssex + '\'' +
                ", Sbirthday=" + Sbirthday +
                ", Class='" + Class + '\'' +
                '}';
    }
}
```

![image-20230208124232136](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230208124232136.png)



# 1.2、Map 封装的一个参数多个值：

这个是最常见的，不多说了。

**示例1：**

数据对象：

```java
HashMap <String, Object> params = new HashMap<String, Object>();
params.put("id", "1234");
params.put("code ", "ABCD");
123
```

Mapper 接口：

```java
public interface UserMapper{
	public List<SysUser>  getUserList(Map  params);
}
123
```

mapper.xml ：

```xml
<select id="getUserList" parameterType="map" resultType="SysUser">
　　select t.* from sys_user t where  id=#{id}  and  code = #{code}
</select>
```

![image-20230208222829015](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230208222829015.png)

# 一对多，注解开发

## User实体类

```java
package com.powernode.pojo;

import java.util.List;

public class User {
   private   Integer id;
   private   String  name;
   private   Integer password;
   private   Integer salary;

   private List<Dept> dept;

    public List<Dept> getDept() {
        return dept;
    }

    public void setDept(List<Dept> dept) {
        this.dept = dept;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getPassword() {
        return password;
    }

    public void setPassword(Integer password) {
        this.password = password;
    }

    public Integer getSalary() {
        return salary;
    }

    public void setSalary(Integer salary) {
        this.salary = salary;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", password=" + password +
                ", salary=" + salary +
                ", dept=" + dept +
                '}';
    }
}

```

## Dept实体类

```java
package com.powernode.pojo;

public class Dept {
    private Integer deptid;
    private String  deprname;
    private String  deptaddr;

    public Integer getDeptid() {
        return deptid;
    }

    public void setDeptid(Integer deptid) {
        this.deptid = deptid;
    }

    public String getDeprname() {
        return deprname;
    }

    public void setDeprname(String deprname) {
        this.deprname = deprname;
    }

    public String getDeptaddr() {
        return deptaddr;
    }

    public void setDeptaddr(String deptaddr) {
        this.deptaddr = deptaddr;
    }

    @Override
    public String toString() {
        return "Dept{" +
                "deptid=" + deptid +
                ", deprname='" + deprname + '\'' +
                ", deptaddr='" + deptaddr + '\'' +
                '}';
    }
}

```

## Userdao接口

```java
package com.powernode.dao;

import com.powernode.pojo.Dept;
import com.powernode.pojo.User;
import org.apache.ibatis.annotations.Many;
import org.apache.ibatis.annotations.Result;
import org.apache.ibatis.annotations.Results;
import org.apache.ibatis.annotations.Select;
import org.apache.ibatis.mapping.FetchType;

import java.util.List;

public interface Userdao {

    @Select("select * from user")
    @Results( id = "DeptMap",value = {
            @Result(property = "id",column = "id"),//

            @Result(property = "dept",column = "id",many = @Many(select = "com.powernode.dao.Deptdao.selectOne"         //property实体类对象,column传过来的参数
                    ,fetchType = FetchType.LAZY))
    })
    List<User> selectUD();
}

```

## DeptDao接口

```java
package com.powernode.dao;

import com.powernode.pojo.Dept;
import org.apache.ibatis.annotations.Select;

import java.util.List;

public interface Deptdao {

    @Select("select * from dept")
    List<Dept> selectAll();

    @Select("select * from dept where deptid=#{id}")
    List<Dept> selectOne(Integer id);
}

```

## Test测试

```java
package MybatisTest;

import com.powernode.dao.Deptdao;
import com.powernode.dao.Userdao;
import com.powernode.pojo.Dept;
import com.powernode.pojo.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import java.io.InputStream;
import java.util.List;

public class Test002 {
    private SqlSessionFactoryBuilder sessionFactoryBuilder;
    private SqlSessionFactory sqlSessionFactory;
    private SqlSession sqlSession;
    private InputStream in;
    private User user;
    private Userdao userdao;
    @Before
    public void init() throws Exception {
        in = Resources.getResourceAsStream("MybatisConfig.xml");
        sessionFactoryBuilder=new SqlSessionFactoryBuilder();
        sqlSessionFactory=sessionFactoryBuilder.build(in);
        sqlSession=sqlSessionFactory.openSession();
        userdao = sqlSession.getMapper(Userdao.class);
    }

    @After
    public void complete() throws Exception {
        sqlSession.commit();
        sqlSession.close();
        in.close();
    }

    @Test
    public void testSelectAll(){
        List<User> users =userdao.selectUD();

        for (User user1:users){
            System.out.println(user1);
        }
    }

}
```

# log4j

```properties
### 配置根 ###
log4j.rootLogger = debug,console ,fileAppender,dailyRollingFile,ROLLING_FILE,MAIL,DATABASE

### 设置输出sql的级别，其中logger后面的内容全部为jar包中所包含的包名 ###
log4j.logger.org.apache=dubug
log4j.logger.java.sql.Connection=dubug
log4j.logger.java.sql.Statement=dubug
log4j.logger.java.sql.PreparedStatement=dubug
log4j.logger.java.sql.ResultSet=dubug

### 配置输出到控制台 ###
log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern =  %d{ABSOLUTE} %5p %c{ 1 }:%L - %m%n

### 配置输出到文件 ###
log4j.appender.fileAppender = org.apache.log4j.FileAppender
log4j.appender.fileAppender.File = logs/log.log
log4j.appender.fileAppender.Append = true
log4j.appender.fileAppender.Threshold = DEBUG
log4j.appender.fileAppender.layout = org.apache.log4j.PatternLayout
log4j.appender.fileAppender.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n

### 配置输出到文件，并且每天都创建一个文件 ###
log4j.appender.dailyRollingFile = org.apache.log4j.DailyRollingFileAppender
log4j.appender.dailyRollingFile.File = logs/log.log
log4j.appender.dailyRollingFile.Append = true
log4j.appender.dailyRollingFile.Threshold = DEBUG
log4j.appender.dailyRollingFile.layout = org.apache.log4j.PatternLayout
log4j.appender.dailyRollingFile.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n

### 配置输出到文件，且大小到达指定尺寸的时候产生一个新的文件 ###
log4j.appender.ROLLING_FILE=org.apache.log4j.RollingFileAppender 
log4j.appender.ROLLING_FILE.Threshold=ERROR 
log4j.appender.ROLLING_FILE.File=rolling.log 
log4j.appender.ROLLING_FILE.Append=true 
log4j.appender.ROLLING_FILE.MaxFileSize=10KB 
log4j.appender.ROLLING_FILE.MaxBackupIndex=1 
log4j.appender.ROLLING_FILE.layout=org.apache.log4j.PatternLayout 
log4j.appender.ROLLING_FILE.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n

### 配置输出到邮件 ###
log4j.appender.MAIL=org.apache.log4j.net.SMTPAppender
log4j.appender.MAIL.Threshold=FATAL
log4j.appender.MAIL.BufferSize=10
log4j.appender.MAIL.From=chenyl@yeqiangwei.com
log4j.appender.MAIL.SMTPHost=mail.hollycrm.com
log4j.appender.MAIL.Subject=Log4J Message
log4j.appender.MAIL.To=chenyl@yeqiangwei.com
log4j.appender.MAIL.layout=org.apache.log4j.PatternLayout
log4j.appender.MAIL.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n

### 配置输出到数据库 ###
log4j.appender.DATABASE=org.apache.log4j.jdbc.JDBCAppender
log4j.appender.DATABASE.URL=jdbc:mysql://localhost:3306/test
log4j.appender.DATABASE.driver=com.mysql.jdbc.Driver
log4j.appender.DATABASE.user=root
log4j.appender.DATABASE.password=
log4j.appender.DATABASE.sql=INSERT INTO LOG4J (Message) VALUES ('[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n')
log4j.appender.DATABASE.layout=org.apache.log4j.PatternLayout
log4j.appender.DATABASE.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n
log4j.appender.A1=org.apache.log4j.DailyRollingFileAppender
log4j.appender.A1.File=SampleMessages.log4j
log4j.appender.A1.DatePattern=yyyyMMdd-HH'.log4j'
log4j.appender.A1.layout=org.apache.log4j.xml.XMLLayout
```

# MybatisXml

## user

```java
package com.powernode.pojo;

public class User {
    private Integer id;
    private String name;
    private Integer password;
    private Integer salary;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getPassword() {
        return password;
    }

    public void setPassword(Integer password) {
        this.password = password;
    }

    public Integer getSalary() {
        return salary;
    }

    public void setSalary(Integer salary) {
        this.salary = salary;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", password=" + password +
                ", salary=" + salary +
                '}';
    }
}

```

## Test001

```java
package XmlTest;

import com.powernode.pojo.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class Test001 {
    private SqlSessionFactoryBuilder sessionFactoryBuilder;
    private SqlSessionFactory sqlSessionFactory;
    private SqlSession sqlSession;
    private User user=new User();
    @Before
    public void init() throws Exception {
        InputStream in = Resources.getResourceAsStream("MybatisConfig.xml");
        sessionFactoryBuilder=new SqlSessionFactoryBuilder();
        SqlSessionFactory build = sessionFactoryBuilder.build(in);
        sqlSession = build.openSession();
    }

    @After
    public void complete(){
        sqlSession.commit();
        sqlSession.close();
    }

    @Test
    public void test001(){
        List<User> list = sqlSession.selectList("selectAll", user);
       for (User user1:list){
           System.out.println(user1);
       }
    }

}

```

```
Student-mapp.xml
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">        <!--使用操作就是namespace.id-->
<mapper namespace="Student-mapp">
    <select id="selectAll" resultType="com.powernode.pojo.User"> <!--resultType输出的对象放在=的右边-->
        SELECT * from user                              <!--同时等号右边那个类要配置mysql相应属性-->
    </select>
</mapper>
```

# #{}和${}

## 1.#{}与${}的区别

#{}的执行结果:

```java
17:47:21,167 DEBUG com.powernode.impl.UserDao.selectByid:143 - ==>  Preparing: select * from user where id=? 
17:47:21,201 DEBUG com.powernode.impl.UserDao.selectByid:143 - ==> Parameters: 1(Integer)
17:47:21,221 DEBUG com.powernode.impl.UserDao.selectByid:143 - <==      Total: 1
```

${}的执行结果，它这个是字符串拼接，数字还好，一旦是字符串就没有双引号:

```java
报错
```

#{}和${}的区别：

​       #{}：底层使用PreparedStatement，特点:先进行SQL语句的编译，然后给SQL语句的占位符号？传值,可以避免sql语句注入的风险

​       ${}:   底层使用Statement，先进行sql语句的拼接，然后再对sql语句进行编译.

​       优先使用#{},这是原则，避免sql注入的风险

​       #{}是以值的形式传递

​       ${}是以字段的形式传递

如果需要SQL语句的关键字放到sql语句中，只能使用${}

## 2.向Sql语句当中拼接表名，就需要使用${}

​      现实业务当中，可能存在分表存储数据的情况，因为一张表存的话数据量太大，查询效率比较低，

​      可以将这些数据有规律的分表存储，这样在查询的时候，效率就比较高，因为扫描的数据量变少了

​      日志表：专门存储日志信息的。

​       怎么解决？

​               可以每天生成一个新表，每张表以当天日期作为名称，例如：

​                       t_log_20230104

​      



