# java网络编程

## socket和httpANDwebSocket之间的联系与区别

![image-20230315190806699](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230315190806699.png)

![img](http://5b0988e595225.cdn.sohucs.com/images/20190622/9dbde0322cc1482fa17b38a4e3bfe664.jpeg)

![img](http://5b0988e595225.cdn.sohucs.com/images/20190622/8e591c52af744ad2abe762469ea5283b.jpeg)

如图1

HTTP 协议:超文本传输协议，对应于应用层，用于如何封装数据.

TCP/UDP 协议:传输控制协议，对应于传输层，主要解决数据在网络中的传输。

IP 协议:对应于网络层，同样解决数据在网络中的传输。

传输数据的时候只使用 TCP/IP 协议(传输层)，如果没有应用层来识别数据内容，传输后的协议都是无用的。

应用层协议很多 FTP,HTTP,TELNET等，可以自己定义应用层协议。

web 使用 HTTP 作传输层协议，以封装 HTTP 文本信息，然后使用 TCP/IP 做传输层协议，将数据发送到网络上。

 

## **一、HTTP 协议**

**http 为短连接：**客户端发送请求都需要服务器端回送响应.请求结束后，主动释放链接，因此为短连接。通常的做法是，不需要任何数据，也要保持每隔一段时间向服务器发送"保持连接"的请求。这样可以保证客户端在服务器端是"上线"状态。

HTTP连接使用的是"请求-响应"方式，不仅在请求时建立连接，而且客户端向服务器端请求后，服务器才返回数据。

 

**二、Socket 连接**

要想明白 Socket，必须要理解 TCP 连接。

TCP 三次握手：握手过程中并不传输数据，在握手后服务器与客户端才开始传输数据，理想状态下，TCP 连接一旦建立，在通讯双方中的任何一方主动断开连接之前 TCP 连接会一直保持下去。

Socket 是对 TCP/IP 协议的封装，Socket 只是个接口不是协议，通过 Socket 我们才能使用 TCP/IP 协议，除了 TCP，也可以使用 UDP 协议来传递数据。

创建 Socket 连接的时候，可以指定传输层协议，可以是 TCP 或者 UDP，当用 TCP 连接，该Socket就是个TCP连接，反之。

**Socket 原理**

Socket 连接,至少需要一对套接字，分为 clientSocket，serverSocket 连接分为3个步骤:

(1) 服务器监听:服务器并不定位具体客户端的套接字，而是时刻处于监听状态；

(2) 客户端请求:客户端的套接字要描述它要连接的服务器的套接字，提供地址和端口号，然后向服务器套接字提出连接请求；

(3) 连接确认:当服务器套接字收到客户端套接字发来的请求后，就响应客户端套接字的请求,并建立一个新的线程,把服务器端的套接字的描述发给客户端。一旦客户端确认了此描述，就正式建立连接。而服务器套接字继续处于监听状态，继续接收其他客户端套接字的连接请求.

**Socket为长连接：**通常情况下Socket 连接就是 TCP 连接，因此 Socket 连接一旦建立,通讯双方开始互发数据内容，直到双方断开连接。在实际应用中，由于网络节点过多，在传输过程中，会被节点断开连接，因此要通过轮询高速网络，该节点处于活跃状态。

 

很多情况下，都是需要服务器端向客户端主动推送数据，保持客户端与服务端的实时同步。

若双方是 Socket 连接，可以由服务器直接向客户端发送数据。

若双方是 HTTP 连接，则服务器需要等客户端发送请求后，才能将数据回传给客户端。

因此，客户端定时向服务器端发送请求，不仅可以保持在线，同时也询问服务器是否有新数据，如果有就将数据传给客户端。



























# URL  and  HttpURLConnotion

```java
package com.powernode.web;

import java.io.IOException;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;

public class HttpTest {
    public static void main(String[] args) throws IOException {
        String html="https://blog.csdn.net/qq_40377973/article/details/127323108";
        URL url=new URL(html);    //URL具体的网络资源
        HttpURLConnection httpURLConnection=(HttpURLConnection) url.openConnection();//通过URL来建立网络连接
        InputStream inputStream = httpURLConnection.getInputStream();//网络连接一旦建立就可以读取数据
        int n=0;
        byte[] bytes=new byte[1024];
        while ((n=inputStream.read(bytes))!=-1){
            System.out.println(new String(bytes));   //将数据输出到控制台
        }
    }
}
```

# URL类的详细分析

```
the contents of the URL:
      http://www.example.com/index.html

contained within it the relative URL:
      FAQ.html

it would be a shorthand for:
      http://www.example.com/FAQ.html
```

# URL的方法

```java
 url.openConnection()    //这个是创建HttpURLConnection对象的
```













# HttpURLConnotion的详细分析

```
A URLConnection with support for HTTP-specific features. See the spec for details.
Each HttpURLConnection instance is used to make a single request but the underlying network connection to the HTTP server may be transparently shared by other instances. Calling the close() methods on the InputStream or OutputStream of an HttpURLConnection after a request may free network resources associated with this instance but has no effect on any shared persistent connection. Calling the disconnect() method may close the underlying socket if a persistent connection is otherwise idle at that time.
```

- HttpURLConnection对象不能直接构造，需要通过URL类中的openConnection()方法来获得。
- 对HttpURLConnection对象的配置都需要在connect()方法执行之前完成，因为connect()会根据HttpURLConnection对象的配置值生成HTTP头部信息。
- HttpURLConnection的**connect()函数，实际上只是建立了一个与服务器的TCP连接，并没有实际发送HTTP请求。****HTTP请求实际上直到我们获取服务器响应数据（如调用getInputStream()、getResponseCode()等方法）时才正式发送出去**。
- HttpURLConnection是基于HTTP协议的，其**底层通过socket通信实现。如果不设置超时（timeout），在网络异常的情况下，可能会导致程序僵死而不继续往下执行**。
- HTTP**正文的内容是通过OutputStream流写入的， 向流中写入的数据不会立即发送到网络，而是存在于内存缓冲区中，待流关闭时，根据写入的内容生成HTTP正文**。
- 调用getInputStream()方法时，返回一个输入流，用于从中读取服务器对于HTTP请求的返回信息。
- 我们可以使用HttpURLConnection.connect()方法手动的发送一个HTTP请求，但是如果要**获取HTTP响应的时候，请求就会自动的发起**，比如我们使用HttpURLConnection.getInputStream()方法的时候，所以完全没有必要调用connect()方法。





# HttpURLConnotion的方法

```java
int getResponseCode(); // 获取服务器的响应代码。
String getResponseMessage(); // 获取服务器的响应消息。
String getResponseMethod(); // 获取发送请求的方法。
void setRequestMethod(String method); // 设置发送请求的方法
对象.getContentLength();      //获得对象内容大小(固定是可以下载的资源,不是网页)

```











# 服务器

```java
package TCP;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.ServerSocket;
import java.net.Socket;

public class TCPtestServer {
    //这个代码要服务器开机就启动（连接部分是这样的）
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = null;
        Socket accept = null;
        InputStream stream = null;
        OutputStream outputStream=new FileOutputStream("C:\\Users\\cao'yang'lin\\Desktop\\java学习md\\TCPtest.txt");//gui可以实现位置的替换
        try {
            //服务器就只需要开个端口就行了
            serverSocket = new ServerSocket(9999);
            //等待客户端连接
            accept = serverSocket.accept();
            //读取客户段的消息
            stream = accept.getInputStream();
            byte[] bytes = new byte[1024];
            int n=0;
//            while((n=stream.read(bytes))!=-1){
//                String s = new String(bytes,0,n);
//                System.out.println(s);
//            }
            while ((n=stream.read(bytes))!=-1){
                outputStream.write(bytes);
            }
                outputStream.flush();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }finally {
            serverSocket.close();
            accept.close();
            stream.close();
        }

    }
}
```

# 客户端

```java
package TCP;

import java.io.*;
import java.net.InetAddress;
import java.net.Socket;
import java.net.UnknownHostException;

public class TCPtestClient {
    public static void main(String[] args) {
        InetAddress serverip;
        Socket socket = null;
        OutputStream outputStream = null;
        InputStream inputStream=null;
        File file=new File("D:\\HBuilderX.3.5.3.20220729\\HBuilderX\\readme\\ThirdPartyNotices(macosx).txt");//gui
        try {
            //要知道服务器的地址
            serverip = InetAddress.getByName("127.0.0.1");
            //要知道端口号
            int port=9999;
            //创建socket连接
            socket = new Socket(serverip,port);
            //发送消息
            outputStream = socket.getOutputStream();
            inputStream =new  FileInputStream(file);
            byte[] bytes=new byte[1024];
            int len;
            while ((len=inputStream.read(bytes))!=-1){
                outputStream.write(bytes);
            }
            outputStream.flush();
        } catch (UnknownHostException e) {
            throw new RuntimeException(e);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }finally {
            try {
                socket.close();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
            try {
                outputStream.close();
                inputStream.close();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }
    }
}
```

# udp短信































# 加密的理解

都可以拿来加密文件夹，密码反正是自己设置的。

但是按照信息传输的角度，就不一样了，不能解密的根本不能信息传输

# 从网络上下载资源

```java
import javax.swing.*;
import java.awt.*;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;

import static javax.swing.JFrame.EXIT_ON_CLOSE;

public class ie {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://d1.music.126.net/dmusic/cloudmusicsetup2.7.1.198242.exe");//gui
            HttpURLConnection urlConnection=(HttpURLConnection) url.openConnection();
            InputStream inputStream =urlConnection.getInputStream();
            //就上面三行代码关键
            
            FileOutputStream outputStream=new FileOutputStream("D:\\asm1\\1.exe");//gui
            byte[] bytes=new byte[1024];
            int len;
            while((len=inputStream.read(bytes))!=-1){
                outputStream.write(bytes,0,len);
            }
            outputStream.close();
            inputStream.close();
            urlConnection.disconnect();

        } catch (MalformedURLException e) {
            throw new RuntimeException(e);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }

    }
}
```

# 从网络上下载资源之多线程下载

```java
package douThread;
import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;

public class ben001 {

    public static void main(String[] args) throws IOException {
    URL url=new URL("https://d1.music.126.net/dmusic/NeteaseCloudMusic_Music_official_2.10.6.200601.exe");
        HttpURLConnection httpURLConnection=(HttpURLConnection) url.openConnection();
        InputStream inputStream=httpURLConnection.getInputStream();
        int totalLen = httpURLConnection.getContentLength();           // 获取文件长度
        int threadLen;                                      // 每个线程下载多少
        final int THREAD_AMOUNT = 8;                        // 线程数
        threadLen = (totalLen + THREAD_AMOUNT - 1) / THREAD_AMOUNT;
        for (int i = 0; i < THREAD_AMOUNT; i++)
            new fenbu(threadLen*i,threadLen).start();
    }
}

class fenbu extends Thread{
    int skip=0;
    int end=0;
    public fenbu(int skip,int threadLen) {
        this.skip=skip;
        this.end=skip + threadLen - 1;
    }
    @Override
    public void run() {
        RandomAccessFile raf;
        OutputStream out;
        HttpURLConnection httpURLConnection;
        InputStream inputStream;
        try {
            URL url=new URL("https://d1.music.126.net/dmusic/NeteaseCloudMusic_Music_official_2.10.6.200601.exe");
             httpURLConnection=(HttpURLConnection) url.openConnection();
            httpURLConnection.setConnectTimeout(5000);
            httpURLConnection.setRequestProperty("Range", "bytes=" + skip + "-" + end);     // 设置当前线程下载的范围
            inputStream=httpURLConnection.getInputStream();
            raf = new RandomAccessFile("D://asm//1.exe", "rw");
            raf.seek(skip);
            byte[] buffer = new byte[1024];
            int len;
            while ((len = inputStream.read(buffer)) != -1)
                raf.write(buffer, 0, len);
                raf.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        try {
            raf.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        try {
            inputStream.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        httpURLConnection.disconnect();
    }
}
```







































# 稍等片刻