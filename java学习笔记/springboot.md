![Spring](https://img-blog.csdnimg.cn/img_convert/968cbe83f69a3edfea91d2fe20131bd0.png)

# SpringBoot简介

## 回顾什么是Spring

Spring是一个开源框架，2003 年兴起的一个轻量级的Java 开发框架，作者：Rod Johnson 。

**Spring是为了解决企业级应用开发的复杂性而创建的，简化开发。**

## Spring是如何简化Java开发的

为了降低Java开发的复杂性，Spring采用了以下4种关键策略：

1、基于POJO的轻量级和最小侵入性编程，所有东西都是bean；

2、通过IOC，依赖注入（DI）和面向接口实现松耦合；

3、基于切面（AOP）和惯例进行声明式编程；

4、通过切面和模版减少样式代码，RedisTemplate，xxxTemplate；

## 什么是SpringBoot

学过javaweb的同学就知道，开发一个web应用，从最初开始接触Servlet结合Tomcat, 跑出一个Hello Wolrld程序，是要经历特别多的步骤；后来就用了框架Struts，再后来是SpringMVC，到了现在的SpringBoot，过一两年又会有其他web框架出现；你们有经历过框架不断的演进，然后自己开发项目所有的技术也在不断的变化、改造吗？建议都可以去经历一遍；

言归正传，什么是SpringBoot呢，就是一个javaweb的开发框架，和SpringMVC类似，对比其他javaweb框架的好处，官方说是简化开发，约定大于配置， you can “just run”，能迅速的开发web应用，几行代码开发一个http接口。

所有的技术框架的发展似乎都遵循了一条主线规律：从一个复杂应用场景 衍生 一种规范框架，人们只需要进行各种配置而不需要自己去实现它，这时候强大的配置功能成了优点；发展到一定程度之后，人们根据实际生产应用情况，选取其中实用功能和设计精华，重构出一些轻量级的框架；之后为了提高开发效率，嫌弃原先的各类配置过于麻烦，于是开始提倡“约定大于配置”，进而衍生出一些一站式的解决方案。

是的这就是Java企业级应用->J2EE->spring->springboot的过程。

随着 Spring 不断的发展，涉及的领域越来越多，项目整合开发需要配合各种各样的文件，慢慢变得不那么易用简单，违背了最初的理念，甚至人称配置地狱。Spring Boot 正是在这样的一个背景下被抽象出来的开发框架，目的为了让大家更容易的使用 Spring 、更容易的集成各种常用的中间件、开源软件；

Spring Boot 基于 Spring 开发，Spirng Boot 本身并不提供 Spring 框架的核心特性以及扩展功能，只是用于快速、敏捷地开发新一代基于 Spring 框架的应用程序。也就是说，它并不是用来替代 Spring 的解决方案，而是和 Spring 框架紧密结合用于提升 Spring 开发者体验的工具。Spring Boot 以约定大于配置的核心思想，默认帮我们进行了很多设置，多数 Spring Boot 应用只需要很少的 Spring 配置。同时它集成了大量常用的第三方库配置（例如 Redis、MongoDB、Jpa、RabbitMQ、Quartz 等等），Spring Boot 应用中这些第三方库几乎可以零配置的开箱即用。

简单来说就是SpringBoot其实不是什么新的框架，它默认配置了很多框架的使用方式，就像maven整合了所有的jar包，spring boot整合了所有的框架 。

Spring Boot 出生名门，从一开始就站在一个比较高的起点，又经过这几年的发展，生态足够完善，Spring Boot 已经当之无愧成为 Java 领域最热门的技术。
**Spring Boot的主要优点：**

- 为所有Spring开发者更快的入门
- **开箱即用**，提供各种默认配置来简化项目配置
- 内嵌式容器简化Web项目
- 没有冗余代码生成和XML配置的要求

# Spring开发-HelloWord

准备工作
我们将学习如何快速的创建一个Spring Boot应用，并且实现一个简单的Http请求处理。通过这个例子对Spring Boot有一个初步的了解，并体验其结构简单、开发快速的特性。

我的环境准备：

java version “1.8.0_181”
Maven-3.6.1
SpringBoot 2.x 最新版
开发工具：

IDEA

# 出现的问题

之前下载没有完全的插件，会一直堵塞创建springboot项目

解决方案：

删除所有maven项目的依赖包

## 成功

# springboot原理初探

自动配置:

pom.xml

- Spring-boot-dependencies:核心依赖在父工程中
- 我们在写或者引入springboot依赖的时候，不需要指定版本，因为有这些版本仓库

**启动器**

```xml
<!--启动器-->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter</artifactId>
</dependency>

```

- 启动器：说白了就是Springboot的启动场景
- 比如spring-boot-starter-web，他就会帮我们自动导入web环境所有的依赖
- springboot会将所有的功能场景，都变成一个个的启动器
- 我们要使用什么功能，就值需要找到对应的启动器`starter`

## 3.2主程序

```java
//标注这个类是一个springboot的应用
@SpringBootApplication
public class Springboot01HelloworldApplication {
    public static void main(String[] args) {
         //将springboot应用启动
        SpringApplication.run(Springboot01HelloworldApplication.class, args);
    }

}
```

在这个里面最重要的就是@SpringBootApplication这个注解了让我们点进去看看，发现他是一个派生注

![img](https://img-blog.csdnimg.cn/20210424204652788.png)

```
而这个注解也是一个派生注解，其中的关键功能由@Import提供，其导入的AutoConfigurationImportSelector的selectImports()方法通过SpringFactoriesLoader.loadFactoryNames()扫描所有具有META-INF/spring.factories的jar包。spring-boot-autoconfigure-x.x.x.x.jar里就有一个这样的spring.factories文件。

```

**注解**

```java
//springboot的配置
@SpringBootConfiguration

	//spring配置类
  @Configuration 

	//说明这也是一个spring的组件
  @Component	

//自动配置
@EnableAutoConfiguration

	//自动配置包
	@AutoConfigurationPackage 

	//自动配置	
		@Import(AutoConfigurationPackages.Registrar.class)

	//自动配置导入选择
	@Import(AutoConfigurationImportSelector.class)

//获取所有的配置
List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);


```











































# Springboot整合数据库



## 1. JPA拥有哪些注解呢？

| 注解               | 解释                                                         |
| ------------------ | ------------------------------------------------------------ |
| @Entity            | 声明类为实体或表。                                           |
| @Table             | 声明表名。                                                   |
| @Basic             | 指定非约束明确的各个字段。                                   |
| @Embedded          | 指定类或它的值是一个可嵌入的类的实例的实体的属性。           |
| @Id                | 指定的类的属性，用于识别（一个表中的主键）。                 |
| @GeneratedValue    | 指定如何标识属性可以被初始化，例如自动、手动、或从序列表中获得的值。 |
| @Transient         | 指定的属性，它是不持久的，即：该值永远不会存储在数据库中。   |
| @Column            | 指定持久属性栏属性。                                         |
| @SequenceGenerator | 指定在@GeneratedValue注解中指定的属性的值。它创建了一个序列。 |
| @TableGenerator    | 指定在@GeneratedValue批注指定属性的值发生器。它创造了的值生成的表。 |
| @AccessType        | 这种类型的注释用于设置访问类型。如果设置@AccessType（FIELD），则可以直接访问变量并且不需要getter和setter，但必须为public。如果设置@AccessType（PROPERTY），通过getter和setter方法访问Entity的变量。 |
| @JoinColumn        | 指定一个实体组织或实体的集合。这是用在多对一和一对多关联。   |
| @UniqueConstraint  | 指定的字段和用于主要或辅助表的唯一约束。                     |
| @ColumnResult      | 参考使用select子句的SQL查询中的列名。                        |
| @ManyToMany        | 定义了连接表之间的多对多一对多的关系。                       |
| @ManyToOne         | 定义了连接表之间的多对一的关系。                             |
| @OneToMany         | 定义了连接表之间存在一个一对多的关系。                       |
| @OneToOne          | 定义了连接表之间有一个一对一的关系。                         |
| @NamedQueries      | 指定命名查询的列表。                                         |
| @NamedQuery        | 指定使用静态名称的查询。                                     |

## 2.创建实体类并与数据库表映射

@Entity//声明实体类
@Data//相当于get/set方法
@Table(name=“user”)//实体类和表的映射关系

```shell
@Id//主键声明
//@GeneratedValue(strategy = GenerationType.AUTO)主键生成策略//identity自增式增长需数据库底层支持/sequence 序列，需底层数据库支持（）如果是自己设置的话建议不写这句
@Column(name="id_user")//表中字段与类属性的映射关系
private String id;
@Column(name="username")
private String name;
@Column(name="password")
private String password;
```

# Aop要加入注解和依赖

![image-20230421170318758](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230421170318758.png)

![image-20230421170331931](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230421170331931.png)

```
@Before("execution(public * com.example.springbootmain.controller.Controller .doTest(..))")
```

## 正确配置完成之后

![image-20230421170407711](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230421170407711.png)

# springboot热部署

可能有以下几个原因导致使用spring-boot-devtools未能生效：

1. 未正确添加依赖：确保在项目中正确地添加了`spring-boot-devtools`的依赖。在`pom.xml`（Maven）或`build.gradle`（Gradle）文件中检查依赖，确保其与其他Spring Boot依赖项具有相同的版本。

2. IDE缓存：有时候IDE会缓存应用程序类，这可能会妨碍某些更改的实时反映。可以尝试完全停止应用程序和重新启动IDE来解决此问题。也可以尝试清除IDE的缓存。

3. 热交换：在运行`mvn spring-boot:run`或`gradle bootRun`命令启动应用程序时，确保已启用热交换。如果没有启用该功能，则必须重新构建和部署应用程序以查看每个更改的效果。

4. 版本兼容性：确保在使用的Spring Boot版本中，`spring-boot-devtools`与其他依赖项兼容，否则可能会出现冲突，导致`devtools`无法正常工作。可以在官方文档中查找各种版本之间的兼容性列表。

5. 自动重启关闭： 如果关闭了自动重启功能，那么即使修改了代码，应用程序也不会重新启动。确认在`application.properties`或`application.yml`文件中该项配置是启用的，如下所示：

   ```
   复制代码# application.properties
   spring.devtools.restart.enabled=true
   
   # application.yml
   spring:
     devtools:
       restart:
         enabled: true
   ```

如果仍然无法解决问题，可以查看程序日志，尝试找到潜在的错误消息，这有助于定位并解决问题。

## 注意不能使用idea，因为idea自带缓存，必须使用mvn spring-boot:run命令这样热部署才能运行
