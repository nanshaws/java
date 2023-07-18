```
11.常见JVM调优参数
配置参数	功能
-Xms	初始堆大小。如：-Xms256m
-Xmx	最大堆大小。如：-Xmx512m
-Xmn	新生代大小。通常为 Xmx 的 1/3 或 1/4。新生代 = Eden + 2 个 Survivor 空间。实际可用空间为 = Eden + 1 个 Survivor，即 90%
-XX:NewRatio	新生代与老年代的比例，如 –XX:NewRatio=2，则新生代占整个堆空间的1/3，老年代占2/3
-XX:SurvivorRatio	新生代中 Eden 与 Survivor 的比值。默认值为 8。即 Eden 占新生代空间的 8/10，另外两个 Survivor 各占 1/10
-XX:+PrintGCDetails	打印 GC 信息
-XX:+HeapDumpOnOutOfMemoryError	让虚拟机在发生内存溢出时 Dump 出当前的内存堆转储快照，以便分析用
```

## 一、idea设置全局的JVM参数

一共三步，**第一步**在菜单栏Help下选择Edit Customer VM Options.......

![image-20230304210355529](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304210355529.png)

![image-20230304210439674](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304210439674.png)

![image-20230304210749686](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304210749686.png)

## 二、针对应用配置JVM参数（maven项目的）

![image-20230304211203837](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304211203837.png)

![image-20230304211541298](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304211541298.png)

## 二、针对应用配置JVM参数（普通项目的）

![image-20230304211807263](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304211807263.png)

![image-20230304211932848](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304211932848.png)

## 1、Java堆验证

```java
import java.util.ArrayList;
import java.util.List;

public class PP {
    public static void main(String[] args) {

        List <Object>  list=new ArrayList<>();
        while (true){
            list.add(new Object());
        }
    }
}

```

![image-20230304212321752](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230304212321752.png)

二、启动JVisualVM
启动方法：

1.进入jdk安装目录的bin目录，双击打开这个程序

2.菜单键+R，输入cmd进入命令行模式，输入命令jvisualvm 启动程序。注：要是使用命令行启动的软件，命令框可不能关闭哦，关闭了的话JVisualVM也会被关闭，切记切记！！！

![image-20230315110443170](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230315110443170.png)

## GC：垃圾回收

436095saifHHhsa@@@835629

GGuuii@qq.com

# **命令行**工具

## jps

作用：列出正在运行的虚拟机进程，并显示虚拟机执行的主类

-q:    显示进程id

-m：显示进程id，主类名称，以及传入main方法的参数

-l：显示进程id，主类全名

-v: 显示进程id，主类名称，以及传入jvm的参数

-V：显示进程ID，主类名称

## jstat

-class : 显示有关类加载器行为的统计信息





这个 Nginx 配置中，`location /` 对于所有的请求都会使用代理 `proxy_pass http://easybuybackup;`，将请求转发给 upstream 中的两个 Tomcat 服务器。在 Tomcat 的多节点集群环境下，使用 Nginx 这样的反向代理服务器可以负载均衡，提高系统的性能和可用性。

现象描述：“这样配置好像，tomcat的静态资源加载不了。”如果是指静态资源文件不能被正确地加载，可能是由于 Nginx 的文件读取属性问题导致。

尝试如下操作：

1.检查 nginx 用户组和权限

首先检查 nginx 和后端 Tomcat 运行所在的目录，看看权限是否设置合理。可以通过命令 `ls -al` 来查看，例如：

```
复制代码ls -al /usr/share/nginx/html
drwxr-xr-x. 2 root root 6 Nov 18 07:29 .
drwxr-xr-x. 3 root root 22 Nov 18 07:27 ..
-rw-r--r--. 1 root root 45 Nov 18 06:57 .noindex.html
```

2.检查 Nginx 配置

检查 Nginx 配置文件中的 static 路径，一般需要加上别名 alias 或者 root，例如：

```
复制代码location /static/ {
    alias /var/www/site/static/;
}
```

或者

```
复制代码location /static/ {
    root /var/www/site/;
}
```

以上两种方式都可以让 Nginx 设置正确的文件路径。

3.使用 Nginx 静态资源缓存

如果静态资源经常被访问，可以考虑在 Nginx 中使用缓存，这样能够提高 Nginx 的读取速度，减轻后端 Tomcat 的负担。

```
复制代码location /static/ {
    root /var/www/site/;
    expires 1d;
}
```

4.检查 Tomcat 配置

如果以上方案都没有



















