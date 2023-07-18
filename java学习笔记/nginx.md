# nignx的学习

nignx的安装，无论是用Linux宿主机安装还是docker安装都行，宿主机要么yum要么apt

## 一、Nginx配置入门

**1. 配置文件**

在Nginx的安装目录下有一个conf文件夹，打开其中的nginx.conf文件

#### 第一部分 全局块

从配置文件开始到events块之间的内容，主要会设置一些影响nginx服务器整体运行的配置指令，主要包括配置运行Nginx服务器的用户组，允许生成的worker process数，进程PID存放路径，日志存放路径和类型以及配置文件的引入等

```shell
worker_processes  1;
```

这是nginx服务器并发处理服务的关键配置，worker_processes越大，可以支持的并发处理数量也越多，但是会受到硬件，软件等设备的制约

#### 第二部分 events块

```shell
events {
    worker_connections  1024; # 表示每个work process支持的最大连接数为1024
}

```

events块涉及的指令主要影响Nginx服务器与用户的网络连接，这部分的配置对Nginx的性能影响较大，在实际中应该灵活配置

#### 第三部分 http块（ubuntu系统include引入了）

Nginx服务器配置中最频繁的部分，http块也可以包括http全局块、server块

http全局块
http全局块配置的指令包括文件引入、MIME-TYPE定义，日志自定义，连接超时时间、单链接请求数上限等

server块
这块和虚拟主机有密切关系，虚拟主机从用户角度看，和一台独立的硬件主机是完全一样的，该技术的产生是为了节省互联网服务器硬件成本

每个http块可以包括多个srever块，而每个server块就相当于一个虚拟主机，而每个server也分为全局server块以及可以同时包含多个location块

全局server块
最常见的配置时本虚拟机主机的监听配置和本虚拟机主机的名称或IP配置

location块
一个server块可以配置多个location块，这块的作用是基于nginx服务器接收到的请求字符串，对虚拟注解名称之外的字符串进行匹配，对特定的请求进行处理，地址定向、数据缓存和应答控制等功能，还有许多第三方模块的配置也在这里进行

![image-20230316224343625](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230316224343625.png)

## **2. 反向代理单个服务器**

那么，如何使用Nginx进行反向代理？

在location参数中添加proxy_pass字段，并填写需要反向代理的服务器地址与端口号：

注意：每一行的配置都需要以封号结尾！！

![img](https://pic4.zhimg.com/v2-f0afd9d0bd68e4fdfedc144abc288a4b_r.jpg)

## **3. 反向代理多台服务器**

如果有多台服务器怎么办？除了不断地添加proxy_pass参数，更好的解决方案是配置upstream服务器组！

**在配置文件的http块中添加upstream属性：**

![img](https://pic1.zhimg.com/v2-a0153e74362793d8cd18d066367f3434_r.jpg)

## 四、运行测试

**1. 启动服务**

配置完成后，进入Nginx安装目录下的sbin文件夹，运行nginx程序即可：

我这里是环境变量所在的地方，所以只需要使用命令就行了，不用进目录

如果之前已经启动，无需关闭nginx服务，只需要让nginx重新加载配置文件即可：

![img](https://pic3.zhimg.com/v2-9087198149f573e45b532fdf95b3b56a_r.jpg)

刷新浏览器，若反向代理成功，访问的路径会自动映射到配置文件中的服务器地址！

将来，随着用户量的增长，可能需要添加新的服务器；这时只需要修改配置文件，使用 nginx -s reload 命令即可，无需关闭nginx服务器！

**2. 关闭服务**

**关闭nginx服务的方式一般分为两种：**

![img](https://pic4.zhimg.com/v2-4d567b19e5f29db01a9200709394962f_r.jpg)







