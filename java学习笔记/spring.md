# IOC

## 之前的Set注入，P注入，构造方法注入，C注入，还有对象里面的对象的注入，这些我不讲了。

## 设计模式

### 简单工厂设计模式

![](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230216181113637.png)

![image-20230216175509252](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230216175509252.png)

客户

```java
package sheJiMoShi;

public class Test {
    public static void main(String[] args) {
        //客户端只需要访问工厂，并不需要去了解细节
        //需要坦克
        Weapon tank = WeaponFactory.get("TANK");
        tank.attack();
        //需要飞机
        Weapon fighter = WeaponFactory.get("FIGHTER");
        fighter.attack();
        //需要砍刀
        Weapon dagger = WeaponFactory.get("DAGGER");
        dagger.attack();

    }
}
```

工厂

```java
package sheJiMoShi;

public class WeaponFactory {
    public static Weapon get(String weaponType){
        if ("TANK".equals(weaponType)){
            return new Tank();
        }else if ("DAGGER".equals(weaponType)){
            return new Dagger();
        }else if("FIGHTER".equals(weaponType)){
            return new Fighter();
        }else {
            throw new RuntimeException("不支持该武器的生产");
        }
    }
}
```

### 工厂方法设计模式

![](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230216183425078.png)

客户端

```java
package sheJiMoShi002;

public class Test {
    public static void main(String[] args) {
        WeaponFactory weaponFactory=new DaggerFactory();
        Weapon dagger = weaponFactory.get();
        dagger.attack();

        WeaponFactory weaponFactory1=new GunFactory();
        Weapon gun = weaponFactory1.get();
        gun.attack();

    }
}

```

抽像工厂

```java
package sheJiMoShi002;

abstract public class WeaponFactory {
    public abstract Weapon get();
}
```

每个武器类都要有一个工厂

枪工厂

```java
package sheJiMoShi002;

public class GunFactory extends WeaponFactory{
    @Override
    public Weapon get() {
        return new Gun();
    }
}
```

## Bean的实例化

![image-20230216183902605](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230216183902605.png)

### 第一种，构造方法实例化

![image-20230216184032136](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230216184032136.png)

### 第二种

通过自定义工厂来实现实例化，在xml文件中告诉spring框架，去调用工厂的静态方法

工厂

```java
package org.example;

public class StarFactory {
    public static Star get(){
        return new Star();
    }
}
```

Star类

```java
package org.example;

public class Star {
    public Star() {
        System.out.println("构造方法执行");
    }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--      简单工厂模式,属性是静态方法，让告诉spring框架-->
    <bean id="starBean" class="org.example.StarFactory" factory-method="get"/>
</beans>
```

### 第三种

![image-20230216194831369](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230216194831369.png)

不用static方法修饰的话，调用那个方法就要创建对象，所以这里先创建了一个工厂对象，然后用factory-bean注入，同时使用factory-method来调用方法

![image-20230216195122586](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230216195122586.png)

### 第四种，通过FactoryBean接口实例化

![image-20230217092306767](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217092306767.png)

## Bean的生命周期，（五步）

![是58](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217101943835.png)

在配置文件中，写`init-method=""`和`destroy-method=""`后面接方法，方法的名字根据类里面的方法确定

赋值是Set注入，使用bean

![image-20230217102437946](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217102437946.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--      简单工厂模式,属性是静态方法，让告诉spring框架-->
    <bean id="starBean" class="org.example.StarFactory" factory-method="get" init-method="initStar" destroy-method="destoryStar"/>
</beans>
```

## Bean的生命周期，（七步）

![image-20230217103021092](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217103021092.png)

![image-20230217103419513](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217103419513.png)

![image-20230217104124561](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217104124561.png)

```

```

![image-20230217104342354](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217104342354.png)

## Bean的生命周期，（十步）

![image-20230217112514182](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217112514182.png)

![image-20230217112622563](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217112622563.png)

Bean后处理器before方法之前

![image-20230217211823316](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217211823316.png)

Bean后处理器before方法之后

![image-20230217212058124](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217212058124.png)

销毁Bean之前执行

![image-20230217212222272](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217212222272.png)

## 自己new的对象纳入spring

![image-20230217213415216](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217213415216.png)

```java
@Test
    public void test002(){
        Star star=new Star();
        System.out.println(star);

        DefaultListableBeanFactory factory=new DefaultListableBeanFactory();
        factory.registerSingleton("StarBean",star);
        Object starBean = factory.getBean("StarBean");
        System.out.println(starBean);
    }
```

## Bean循环依赖之单例和set模式

![image-20230217214816492](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217214816492.png)

# 注解IOC

```java
package IOCTest;

import com.powernode.LocNOxml;
import com.powernode.SpringCofig;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Test001 {
    @Test
    public void testIOC(){
        ApplicationContext applicationContext=new AnnotationConfigApplicationContext(SpringCofig.class);
        LocNOxml locNOxml = applicationContext.getBean("locNOxml", LocNOxml.class);
        System.out.println(locNOxml.getAge());
        System.out.println(locNOxml.getMain());
    }
}

```



## 注解Config

```java
package com.powernode;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.stereotype.Component;

@Configuration
@ComponentScan("com.powernode")
public class SpringCofig {

}

```



## 目标类

```java
package com.powernode;

import jakarta.annotation.Resource;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;

@Service("locNOxml")
public class LocNOxml {
    @Value("23")
    private int age;
    @Value("张三")
    private String name;

    @Resource(name = "main")
    Main main;

    public Main getMain() {
        return main;
    }

    public int getAge() {
        return age;
    }
    public String getName() {
        return name;
    }

    public LocNOxml() {

    }
}

```



## Main目标类

```java
package com.powernode;

import org.springframework.stereotype.Service;

@Service
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```



# AOP

## 目标类

```java
package com.powernode.Aop;

import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Pointcut;
import org.springframework.stereotype.Service;

@Service
public class MainSHIxian implements HELLO{
    @Override
    public void printhi() {
        System.out.println("hi");
    }
}

```

## 增强类

```java
package com.powernode.Aop;

import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.EnableAspectJAutoProxy;
import org.springframework.stereotype.Service;

@Service
@Aspect       //增强标注
public class AddHi {
    @Before("execution(* com.powernode..*(..))")
    public void sb(){
        System.out.println("sb");
    }

}

```

## Test

```java
@Test
    public void testAOP1(){
        ApplicationContext applicationContext=new AnnotationConfigApplicationContext(SpringCofig.class);
        MainSHIxian addHi = applicationContext.getBean("mainSHIxian", MainSHIxian.class);
        addHi.printhi();
    }
```

## 配置类

```java
package com.powernode;

import org.aspectj.lang.annotation.Aspect;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.EnableAspectJAutoProxy;
import org.springframework.stereotype.Component;

@Configuration   //动态代理
@ComponentScan("com.powernode")  //组件扫描
@EnableAspectJAutoProxy(proxyTargetClass = true) //aop
public class SpringCofig {

}

```

# 注解大全

```java
@Configuration     //标明配置类
@ComponentScan("com.powernode.pojo")  //扫描 @Component @Service @Controller @Repository  的配置类，后面就只用那个类就可以创建以上四个注解所在的包的类对象
@Bean  //注入，第三方包
@PropertySource("T1.properties")  //加载配置文件 和@Value("${name}")联用,用来赋值这里的配置文件里面要有name=什么的



@Configuration
@ComponentScan(value = "com.powernode.pojo",excludeFilters = {
        @ComponentScan.Filter(type = FilterType.ANNOTATION,classes = {Controller.class})
},useDefaultFilters=false)  将自动扫描全部关掉                                                                 //不包含Controller.class

//  Filter[] includeFilters() default {};  只包含
//
//    Filter[] excludeFilters() default {}; 不包含

//FilterType.ANNOTATION ，按照注解
//

@Scope("") //prototype 多例的 //singleton 单例的
@Lazy    //懒加载是单例情况下，容器启动时不创建对象，第一次使用获取Bean创建对象，并且初始化

    
组件注册-@Conditional -按照条件注册

    
给容器中注册组件就三种方式
    第一种@ComponentScan("com.powernode.pojo")  //扫描 @Component @Service @Controller @Repository  的配置类，后面就只用那个类就可以创建以上四个注解所在的包的类对象   只能加在类上
    第二种@Bean  //注入，第三方包  只能加在方法和注解上
    第三种@import(要导入的组件.class)[快速给容器中导入一个组件，id默认是全类名] 只能加在类上
         @ImportSelector:导入的选择器,返回需要导入组件的全类名的数组，加在import的组件内,可以扫描可选择的组件，不过要先                              implements ImportSelector
         @         
    第四种，使用Spring提供的FactoryBean(工厂Bean)  工厂bean获取的是调用getObject创建的对象
             默认是获取工厂bean创建的对象，是用getObject方法创建的对象
             要获取工厂bean本身，我们需要给id前面加一个&
                &colorFactoryBean
             
             
             
使用 @Value赋值
             1.基本数值
             2.可以写SpEL，#{} //里面是运算符
             3.可以写${};取出配置文件的值（在运行环境变量里面的值）在xml文件下配置<context:property-placeholder location="classpath:" />
             4.使用@PropertySource()读取外部配置文件中的k/v保存到运行的环境变量中
             还可以使用环境来读取
             
自动装配
                 spring利用依赖注入(DI),完成对IOC容器中各个组件的依赖关系赋值
             1.@Autowired，自动注入：      位置:构造器，参数，方法，属性；
                 1.会默认优先按照类型去容器中找对应的组件
                 2.如果找到多个相同类型的组件，再将属性的名称作为组件的id去容器中查找
                 3.@Qualifier("bookDao"):使用@Qualifier指定需要装配的组件id，而不是使用属性名
                 4.自动装配默认一定要将属性赋值好，没有就会报错
             2.@Resource
               @Inject (导依赖javax.inject包)
             3.Autowired //标注在方法上，Spring容器创建当前对象，就会调用方法，完成赋值
                         方法使用的参数，自定义类型的值从IOC容器中获取
               
@Profile：指定组件在哪个环境的情况下才能被注册到容器中，不指定，任何环境下都能注册这个组件
           1.加了环境标识的bean，只有这个环境被激活的时候才能注册到容器中。默认是default环境
           怎么切换到test环境呢
           1.使用命令行动态参数：在虚拟机参数位置上加载 -Dspring.profiles.active=test
           2.使用代码的方式                     
                         1.创建一个applicationContext
                         2.设置需要激活的环境
                         applicationContext.getEnvironment().setActiveProfiles("test","dev");
                         3.注册主配置类
                         applicationContext.register(AppCl.class);
                         4.刷新容器
                         applicationContext.refresh();
          位置：放在方法上，只有是这个环境的，方法才能运行                   
               放在配置类上，只有是指定的环境的时候，整个配置类里面的所有配置类才会生效
          3.没有标注环境的bean在任何环境下都是加载的; 
                             
```

## 获取当前的操作系统类型

```java
@Test
    public void test001(){
       ApplicationContext applicationContext=new AnnotationConfigApplicationContext(MainConfig2.class);
       Environment environment = applicationContext.getEnvironment();
       String property = environment.getProperty("os.name");
       System.out.println(property);
    }

package com.powernode.pojo;

import org.springframework.beans.factory.config.ConfigurableListableBeanFactory;
import org.springframework.beans.factory.support.BeanDefinitionRegistry;
import org.springframework.context.annotation.Condition;
import org.springframework.context.annotation.ConditionContext;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.env.Environment;
import org.springframework.core.type.AnnotatedTypeMetadata;

public class LinuxCondition implements Condition {
    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        //能获取到ioc使用的beanFactory
        ConfigurableListableBeanFactory beanFactory=context.getBeanFactory();
        //获取类加载器
        ClassLoader classLoader = context.getClassLoader();
        //获取当前的环境信息
        Environment environment = context.getEnvironment();
        //获取bean定义的注册类
        BeanDefinitionRegistry registry = context.getRegistry();
        boolean app = registry.containsBeanDefinition("app");
        System.out.println(app);
        //可以判断容器中的bean注册情况,也可以给容器中注册bean
        //registry.registerBeanDefinition();

        return true;
    }
}

```

## Bean的生命周期

```java
//1.用bean 先通过构造方法创建对象然后 来   创建 对象的初始化和销毁
@Service
public class Color {
    @Bean(initMethod = "getObject")//初始化方法一定是返回的类型的类里面所有的方法,销毁也是
    public ColorFactoryBean colorFactoryBean(){
        return new ColorFactoryBean();
    }
}

//2.通过让Bean实现InitializingBean(定义初始化逻辑),DisposableBean(定义销毁逻辑)  //Bean实现类的类
public class ColorFactoryBean implements FactoryBean<Color>, InitializingBean {
}

//3.可以使用JSR250
     @PostConstruct:在bean创建完成并且属性赋值完成，来执行初始化
     @PreDestroy:在容器销毁bean之前通知我们进行清理工作

         
         
//4.BeanPostProcessor,bean的后置处理器，
         在bean初始化前后进行一些处理工作 
         postProcessBeforeInitialization:初始化之前
         postProcessAfterInitialization:初始化之后
```











































































