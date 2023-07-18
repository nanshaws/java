![image-20230114143435220](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230114143435220.png)

![image-20230114143552885](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230114143552885.png)

![image-20230114143740535](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230114143740535.png)



# 模拟servlet

## servlet接口

```java
public interface servlet {
    void self();
}

```

```java
//tomcat
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.io.Reader;
import java.util.Properties;
import java.util.ResourceBundle;
import java.util.Scanner;

public class tomcat {

    public static void main(String[] args) throws IOException, ClassNotFoundException, InstantiationException, IllegalAccessException {
        System.out.println("正在启动tomcat服务器");
        Scanner sc=new Scanner(System.in);
        String s1=sc.nextLine();
        FileReader r1=new FileReader("D:\\ASM\\idea工作区\\spring6\\moniservlet\\src\\use.properties");
        Properties p1=new Properties();
        p1.load(r1);
        String s2 =  p1.getProperty(s1);
        Class cl=Class.forName(s2);
        Object o= cl.newInstance();
        servlet servlet=(servlet) o;
        servlet.self();
    }

}

```

```java
//实体userlist
public class userlist implements servlet{

    @Override
    public void self() {
        System.out.println("userlist");
    }
}

```

```java
//实体银行
public class banklist implements servlet{

    @Override
    public void self() {
        System.out.println("banklist");
    }
}
```

![image-20230119115431180](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230119115431180.png)

**一个快速入门的案例：** 

我们创建Servlet1和Servlet2，分别用于在ServletContext中创建和读取属性： 



Servlet1的doGet方法为：

```
public void doGet(HttpServletRequest request, HttpServletResponse response)
        throws ServletException, IOException {
    response.setContentType("text/html;charset=utf-8");
    PrintWriter out = response.getWriter();
    // 获取ServletContext对象的引用
    // 第一种方法

    ServletContext servletContext = this.getServletContext();
    // 第二种方法
    // ServletContext servletContext2 = this.getServletConfig().getServletContext();
    servletContext.setAttribute("name", "小明");
    out.println("将 name=小明  写入了ServletContext");
}
```

Servlet2的doGet方法为：

```
public void doGet(HttpServletRequest request, HttpServletResponse response)
        throws ServletException, IOException {
    response.setContentType("text/html;charset=utf-8");
    PrintWriter out = response.getWriter();
    // 取出ServletContext的某个属性
    //1.首先获取到ServletContext
    ServletContext servletContext = this.getServletContext();
    //2.取出属性
    String name = (String)servletContext.getAttribute("name");
    out.println("name="+name);
}
```

以此访问Servlet1和Servlet2，我们可以分别看到输出如下：



![Servletcontext 对象](https://atts.w3cschool.cn/attachments/image/20180428/1524881525320646.png)



![Servletcontext 对象](https://atts.w3cschool.cn/attachments/image/20180428/1524881532405113.png)



粗看之下，这个运行结果和Session，Cookie的应用似乎没什么区别，但事实上则完全不一样的。只要不关闭Tomcat或者reload该应用，当我们关闭当前的浏览器，或者是换一个浏览器，比如从360浏览器换到了IE浏览器再次访问Servlet2，我们依然可以看到这个结果！这就是和和Session，Cookie最大的不同了。之所以会造成这种不同，是因为ServletContext存在于服务器内存中的一个公共空间，它可以供所有的用户客户端访问。

![image-20230119200646118](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230119200646118.png)

## 两个servlet的配合。

```java
import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class Main extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setAttribute("name","sun");
        RequestDispatcher dispatcher = request.getRequestDispatcher("/a");//这两行代码是跳转
        dispatcher.forward(request,response);//两个servlet可以通信，使用同一次服务，等于new了一个可以由tomcat服务器来掌控的对象
    }
}
```

```java
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class Main1 extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String name =(String) request.getAttribute("name");
        System.out.println(name);
    }
}

```

![image-20230119210713422](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230119210713422.png)

# session

1、session会话是由服务器创建的，session的断开是超时断开，并不是客户端关闭浏览器，session就没了？并不是这样的。

2、而是等时间，这段时间内没有数据的流动就会自动断开连接

3、一次会话包含多次请求

4、一个session对应一个会话

5、session怎么获取呢？

```java
HttpSession session =request.getSession();
//从服务器中获取session对象。
//如果没有获取当前session对象就新建
HttpSession session =request.getSession(false);
//从服务器中获取session对象。
//如果没有获取当前session对象就返回一个null
```

# 在tomcat服务器中显示提交，然后打开pdf观看

```java
 File file = new File("D:/ASM/books/tomcat.pdf");
            if (file.exists()){
                byte[] data = null;
                try {
                    FileInputStream input = new FileInputStream(file);
                    data = new byte[input.available()];
                    input.read(data);
                    response.getOutputStream().write(data);
                    input.close();
                } catch (Exception e) {
                    System.out.println(e);
                }

            }else{
                return;
            }
```

# 一个普通的maven项目去搭建Tomcat服务器

第一步：先控制out目录，就是输出的class文件和html，和资源文件的目录   具体操作：

![image-20230302194458024](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230302194458024.png)

![image-20230302194642170](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230302194642170.png)

![image-20230302194724931](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230302194724931.png)

















































