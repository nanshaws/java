# 在jsp里面写任何代码都是在out.write里面的，都是普通字符，如果写Java代码则加特殊符号

![image-20230205141751122](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230205141751122.png)

jsp就是一个Servlet，但是他是可以由tomcat来自动转换前端操作的。他的class文件不与其他class放在一起。

jsp是一个翻译引擎

# jsp里面写中文配置

```jsp
<%@page contentType="text/html;charset=UTF-8"%>
```

# 各个web容器里面的jsp同一一个规范，就是jsp规范

<%%>方法块

<%%>相当于servcie方法体里写代码

<%！%>相当于servcie方法体外面写代码

jsp顺序是不同符号时只认符号，同符号时，自上而下

# jsp的注释

```jsp
<%--
    @page contentType="text/html;charset=UTF-8"
--%>
```

![image-20230205143430235](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230205143430235.png)

所以调试jsp的时候，是直接调试tomcat生成的java代码，而不是jsp代码

可以在<%out.write("sb")%> 虽然在idea里面报红，但是按照原理是可以用的

```jsp
<%out.write("sb")%>
```

![image-20230205145920069](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230205145920069.png)



![image-20230205164438614](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230205164438614.png)

![image-20230205164754802](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230205164754802.png)



























