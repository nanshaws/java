## 对象  instanceof   类   判断a是不是B类的对象

```java
public class instanceOF {
    public static void main(String[] args) {
        A a=new B();           //a表面是A的对象，实际是B类的对象，但是只能调用A类里面的方法的名字。
        B b = new B();         //强制转换就是向下转型
        if (a instanceof B){   //new 子类就是向上转型
            ((B) a).add();
        }
    }
}

class A {
    void mov(){
        System.out.println("数据的流动");
    }
}

class B extends A{
    @Override
    void mov() {
        System.out.println("地址的流动");
    }
    void add(){
        System.out.println("地址的偏移量加");
    }
}

class C extends A{
    @Override
    void mov() {
        System.out.println("数据的流动");
    }
}
```

![image-20230122094142076](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230122094142076.png)

## 向下转型

![image-20230122094859710](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230122094859710.png)

## 向上转型

![image-20230122094926249](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230122094926249.png)

## String类

```java
public class Stringjjj {
   public static String s="cao";
  public static   void show(){
      byte[] bytes=s.getBytes();
      String s1 = new String(bytes);
      for (byte b:bytes){
          System.out.println(b);
      }
      System.out.println(s1);
    }
   public static void show1(){
      char c = s.charAt(1);
       System.out.println(c);
       String qq="3347004610@qq.com";
       String[] split =qq.split("@");
       for(String f:split){
           System.out.println(f);
       }
       boolean a = s.contains("a");
   }
    public static void main(String[] args) {
       // show();
         show1();
    }
}

```

```java
try {
                        //字符读入流
                        FileReader reader = new FileReader(file);  //以后就只用FileReader类和FileWriter类了
                        //读入缓冲区
                        char[] buffer = new char[1024];           //缓存区
                        //读入结果
                        StringBuffer result = new StringBuffer(); //累加对象
                        //每次读入缓冲区的长度
                        int len;
                        //从读入流中读取文件内容并形成结果
                        while((len = reader.read(buffer)) != -1) {     
                            result.append(buffer,0,len);       //不段的累加
                        }
                        //关闭读入流
                        reader.close();
                        //更新文本显示区内容
                        jTextArea.setText(result.toString());    //显示累加对象
                        System.out.println("读档成功");
                    } catch (FileNotFoundException e1) {
                        // TODO Auto-generated catch block
                        e1.printStackTrace();
                    } catch (IOException e1) {
                        // TODO Auto-generated catch block
                        e1.printStackTrace();
                    }
```

## java线程

```java
new Thread(() -> {
	System.out.println(Thread.currentThread().getName() + "\t上完自习，离开教室");
}, "MyThread").start();
```

java的转换流

InputStreamReader 就是将Stream字节流转换为Reader字符流，OutputStreamWriter

![image-20230125191414414](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230125191414414.png)

## java序列化

就是将对象存到文件中

```java
import java.io.*;
 
public class SerializeDemo
{
   public static void main(String [] args)
   {
      Employee e = new Employee();
      e.name = "Reyan Ali";
      e.address = "Phokka Kuan, Ambehta Peer";
      e.SSN = 11122333;
      e.number = 101;
      try
      {
         FileOutputStream fileOut =
         new FileOutputStream("/tmp/employee.ser");
         ObjectOutputStream out = new ObjectOutputStream(fileOut);
         out.writeObject(e);
         out.close();
         fileOut.close();
         System.out.printf("Serialized data is saved in /tmp/employee.ser");
      }catch(IOException i)
      {
          i.printStackTrace();
      }
   }
}
```

```java
import java.io.*;
 
public class DeserializeDemo
{
   public static void main(String [] args)
   {
      Employee e = null;
      try
      {
         FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
         ObjectInputStream in = new ObjectInputStream(fileIn);
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
      }catch(IOException i)
      {
         i.printStackTrace();
         return;
      }catch(ClassNotFoundException c)
      {
         System.out.println("Employee class not found");
         c.printStackTrace();
         return;
      }
      System.out.println("Deserialized Employee...");
      System.out.println("Name: " + e.name);
      System.out.println("Address: " + e.address);
      System.out.println("SSN: " + e.SSN);
      System.out.println("Number: " + e.number);
    }
}
```

## java反序列化

就是将文件对象读取出来

```java
import java.io.Serializable;

public class Student implements Serializable {
    private int id;
    private String name;
    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
}
```

```java
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;

public class hu {
    public static void main(String[] args) throws Exception{
        Student s=new Student(1,"cao");
        ObjectOutputStream stream=new ObjectOutputStream(new FileOutputStream("t1"));
        stream.writeObject(s);
        stream.flush();
        stream.close();

    }
}
```

## transient关键字表示不参加序列号版本号，不管赋多少都是所显示为null

序列化版本号的作用（接口Serializable可以自动生成序列号版本号，强烈建议自己定义）

`private static final long serialVersionUID=1L;`

![image-20230125231301862](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230125231301862.png)

## java线程

一个进程就相当于一个软件。

线程就是进程的组成部分

![image-20230126104638003](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230126104638003.png)

一个线程一个栈。

![image-20230126105401518](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230126105401518.png)

![image-20230126110921367](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230126110921367.png)

就只有一个主线程，这些方法都在主线程的栈里面

## java线程的start方法就是开辟另一段栈空间

主栈空间for循环和另一段空间的for循环是同时进行的。

## java传参的参数是接口类型，这个可以使用new 接口的实现类

```java
public class 内部类 {
    public static void main(String[] args) {
        A a =new A();
        System.out.println(a.add(new A(),1,4));
        
    }
}

interface sum{
    int add(sum c,int a,int b);
}

class A implements sum{

    @Override
    public int add(sum c,int a,int b) {
        return a+b;
    }
}
```

不用实现类带的话，就可以使用接口然后实现接口里面的方法

```java
public class Thread001 {
    public static void main(String[] args) {
      new Thread(new Runnable() {
          @Override
          public void run() {
              System.out.println("sb");
              System.out.println(Thread.currentThread());
          }
      },"mythread").start();
    }

}
```

```java
       new B().play();
    }

}

class B{
  public   void play(){
      System.out.println("play");
    }
}
```

![image-20230126200849528](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230126200849528.png)

## java线程锁

Java锁null时，会报空指针异常

没有线程，锁就没有意义

单线程的工作不要用多线程来干，否则要么出错要么只有一个线程工作





## System类的方法

```java
import java.io.PrintStream;

public class printLiu {
    public static void main(String[] args) {
        PrintStream ps=System.out;
        ps.println("sv");
        ps.println("wangwu");
        System.out.println(System.currentTimeMillis());//该整数表示当前时间与1970年1月1日零点整之间的时间差，以毫秒为单位，又称时间戳。
        System.gc();//强制垃圾回收器来释放这些对象的内存
        ps.println(123);
        //System.arraycopy();//复制数组
        System.exit(0);//退出java虚拟机jvm,这段代码后面的程序不执行
        ps.println(123);
    }
}
```

## 日志的实现

```java
import java.io.FileOutputStream;
import java.io.PrintStream;
public class printLiu {
    public static void main(String[] args) throws Exception{
        PrintStream ps=new PrintStream(new FileOutputStream("log",true));
        ps.println("sb");
        ps.flush();
    }
}
```

## Date类的方法

```java
public class Data日期 {
    public static void main(String[] args) {
        Date date=new Date();
        System.out.println(date);
        SimpleDateFormat simpleDateFormat=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        String s = simpleDateFormat.format(date);
        System.out.println(s);
    }
}
```

## date转化为字符串，字符串转化为date

```java
import java.text.SimpleDateFormat;
import java.util.Date;

public class Data日期 {
    public static void main(String[] args) throws Exception{
        Date date=new Date();       //1000毫秒是1秒
        System.out.println(date);   //yyyy年 MM月 dd 天 HH//24小时 mm分钟 ss秒 SSS毫秒
        SimpleDateFormat simpleDateFormat=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        String s = simpleDateFormat.format(date);
        String datee="2003-07-29 12:27:34 333";
        SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        Date date1 = sdf.parse(datee);
        System.out.println(date1);
        System.out.println(s);
    }
}
```

## 分割符使用特殊符号需要转义

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
        String s="dsa&%&*?db";
        String[] split = s.split("\\?");  //使用\\转义
        for(String s1:split){
            System.out.println(s1);
        }
    }
}
```

## java左移和右移

- `<<` :左移运算符，向左移若干位，高位丢弃，低位补零。`x << 1`,相当于 x 乘以 2(不溢出的情况下)。
- `>>` :带符号右移，向右移若干位，高位补符号位，低位丢弃。正数高位补 0,负数高位补 1。`x >> 1`,相当于 x 除以 2。
- `>>>` :无符号右移，忽略符号位，空位都以 0 补齐。

由于 `double`，`float` 在二进制中的表现比较特殊，因此不能来进行移位操作。

移位操作符实际上支持的类型只有`int`和`long`，编译器在对`short`、`byte`、`char`类型进行移位前，都会将其转换为`int`类型再操作。

<<=为左移

```java
>>=为右移
int i = -1;
    System.out.println("初始数据： " + i);
    System.out.println("初始数据对应的二进制字符串： " + Integer.toBinaryString(i));
    i <<= 10;
    System.out.println("左移 10 位后的数据 " + i);
    System.out.println("左移 10 位后的数据对应的二进制字符 " + Integer.toBinaryString(i)); 
```

![image-20230205215124421](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230205215124421.png)

由于左移位数大于等于 32 位操作时，会先求余（%）后再进行左移操作，所以下面的代码左移 42 位相当于左移 10 位（42%32=10），输出结果和前面的代码一样。

```java
int i = -1;
System.out.println("初始数据： " + i);
System.out.println("初始数据对应的二进制字符串： " + Integer.toBinaryString(i));
i <<= 42;
System.out.println("左移 10 位后的数据 " + i);
System.out.println("左移 10 位后的数据对应的二进制字符 " + Integer.toBinaryString(i));
```

![image-20230205215506198](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230205215506198.png)



## java的return

return可以在任意位置结束这个方法

## java的可变长参数

从 Java5 开始，Java 支持定义可变长参数，所谓可变长参数就是允许在调用方法时传入不定长度的参数。就比如下面的这个 `printVariable` 方法就可以接受 0 个或者多个参数。

```java
public static void method1(String... args) {
   //......
}
```

另外，可变参数只能作为函数的最后一个参数，但其前面可以有也可以没有任何其他参数。

```java
public static void method2(String arg1, String... args) {
   //......
}
```

**遇到方法重载的情况怎么办呢？会优先匹配固定参数还是可变参数的方法呢？**

答案是会优先匹配固定参数的方法，因为固定参数的方法匹配度更高。

我们通过下面这个例子来证明一下。

```java
/**
 * 微信搜 JavaGuide 回复"面试突击"即可免费领取个人原创的 Java 面试手册
 *
 * @author Guide哥
 * @date 2021/12/13 16:52
 **/
public class VariableLengthArgument {

    public static void printVariable(String... args) {
        for (String s : args) {
            System.out.println(s);
        }
    }

    public static void printVariable(String arg1, String arg2) {
        System.out.println(arg1 + arg2);
    }

    public static void main(String[] args) {
        printVariable("a", "b");
        printVariable("a", "b", "c", "d");
    }
}
```

输出：

```text
ab
a
b
c
d
```

另外，Java 的可变参数编译后实际会被转换成一个数组，我们看编译后生成的 `class`文件就可以看出来了。

```java
public class VariableLengthArgument {

    public static void printVariable(String... args) {
        String[] var1 = args;
        int var2 = args.length;

        for(int var3 = 0; var3 < var2; ++var3) {
            String s = var1[var3];
            System.out.println(s);
        }

    }
    // ......
}
```

## java的String[] args

我们可以通过以下方式来进行验证：

- 1、先编写一个Hello.java文件，文件内容如下：

```java
public class Hello{
	public static void main(String[] args) {
		System.out.println("==============args start============");
		for(int i = 0; i < args.length; i++) {
			System.out.println(args[i]);
		}
		System.out.println("==============args end============");
	}
}
```

- 2、在Hello.java文件的路径下打开cmd命令提示符，运行javac Hello.java命令编译该文件，这将会在对应的文件路径下，得到一个Hello.class字节码文件。
- 3、使用java Hello命令运行Hello.class文件，我们将会得到如下的运行结果：
  ![-](https://img-blog.csdnimg.cn/20210110215255723.png)
- 4、我们这次在java命令后面添加一些参数，这些参数我们可以自己定义。例如：java Hello a b c d ，我们将会得到如下的运行结果：
- ![image-20230206101259941](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230206101259941.png)

> 正是因为Java main()方法的这个扩展性，使得每一个开发者，可以通过自己定义一些Java命令的参数，实现一些不同的功能。

## java的基本数据类型

![image-20230206113159026](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230206113159026.png)



1. Java 里使用 `long` 类型的数据一定要在数值后面加上 **L**，否则将作为整型解析。

## java包装类的缓存机制

### 包装类型的缓存机制了解么？

Java 基本数据类型的包装类型的大部分都用到了缓存机制来提升性能。

`Byte`,`Short`,`Integer`,`Long` 这 4 种包装类默认创建了数值 **[-128，127]** 的相应类型的缓存数据，`Character` 创建了数值在 **[0,127]** 范围的缓存数据，`Boolean` 直接返回 `True` or `False`。

**Integer 缓存源码：**



```java
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
private static class IntegerCache {
    static final int low = -128;
    static final int high;
    static {
        // high value may be configured by property
        int h = 127;
    }
}
```

**`Character` 缓存源码:**



```java
public static Character valueOf(char c) {
    if (c <= 127) { // must cache
      return CharacterCache.cache[(int)c];
    }
    return new Character(c);
}

private static class CharacterCache {
    private CharacterCache(){}
    static final Character cache[] = new Character[127 + 1];
    static {
        for (int i = 0; i < cache.length; i++)
            cache[i] = new Character((char)i);
    }

}
```

**`Boolean` 缓存源码：**



```java
public static Boolean valueOf(boolean b) {
    return (b ? TRUE : FALSE);
}
```

如果超出对应范围仍然会去创建新的对象，缓存的范围区间的大小只是在性能和资源之间的权衡。

两种浮点数类型的包装类 `Float`,`Double` 并没有实现缓存机制。



```java
Integer i1 = 33;
Integer i2 = 33;
System.out.println(i1 == i2);// 输出 true

Float i11 = 333f;
Float i22 = 333f;
System.out.println(i11 == i22);// 输出 false

Double i3 = 1.2;
Double i4 = 1.2;
System.out.println(i3 == i4);// 输出 false
```

下面我们来看一下问题。下面的代码的输出结果是 `true` 还是 `false` 呢？



```java
Integer i1 = 40;
Integer i2 = new Integer(40);
System.out.println(i1==i2);
```

`Integer i1=40` 这一行代码会发生装箱，也就是说这行代码等价于 `Integer i1=Integer.valueOf(40)` 。因此，`i1` 直接使用的是缓存中的对象。而`Integer i2 = new Integer(40)` 会直接创建新的对象。

因此，答案是 `false` 。你答对了吗？

记住：**所有整型包装类对象之间值的比较，全部使用 equals 方法比较**。

![img](https://img-blog.csdnimg.cn/20210422164544846.png)

# java的自动装箱和拆箱

## 自动装箱与拆箱了解吗？原理是什么？

**什么是自动拆装箱？**

- **装箱**：将基本类型用它们对应的引用类型包装起来；
- **拆箱**：将包装类型转换为基本数据类型；

举例：

```java
Integer i = 10;  //装箱
int n = i;   //拆箱
```

## java的拷贝

**浅拷贝**  就是拷贝的对象里面有其他的对象，这个其他的对象就是使用的是同一个

浅拷贝的示例代码如下，我们这里实现了 `Cloneable` 接口，并重写了 `clone()` 方法。

`clone()` 方法的实现很简单，直接调用的是父类 `Object` 的 `clone()` 方法。

```java
public class Address implements Cloneable{
    private String name;
    // 省略构造函数、Getter&Setter方法
    @Override
    public Address clone() {
        try {
            return (Address) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
}

public class Person implements Cloneable {
    private Address address;
    // 省略构造函数、Getter&Setter方法
    @Override
    public Person clone() {
        try {
            Person person = (Person) super.clone();
            return person;
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
}
```

测试 ：

```java
Person person1 = new Person(new Address("武汉"));
Person person1Copy = person1.clone();
// true
System.out.println(person1.getAddress() == person1Copy.getAddress());
```

从输出结构就可以看出， `person1` 的克隆对象和 `person1` 使用的仍然是同一个 `Address` 对象。

**深拷贝**  

这里我们简单对 `Person` 类的 `clone()` 方法进行修改，连带着要把 `Person` 对象内部的 `Address` 对象一起复制。



```java
@Override
public Person clone() {
    try {
        Person person = (Person) super.clone();
        person.setAddress(person.getAddress().clone());
        return person;
    } catch (CloneNotSupportedException e) {
        throw new AssertionError();
    }
}
```

测试 ：



```java
Person person1 = new Person(new Address("武汉"));
Person person1Copy = person1.clone();
// false
System.out.println(person1.getAddress() == person1Copy.getAddress());
```

从输出结构就可以看出，虽然 `person1` 的克隆对象和 `person1` 包含的 `Address` 对象已经是不同的了。

**那什么是引用拷贝呢？** 简单来说，引用拷贝就是两个不同的引用指向同一个对象。

我专门画了一张图来描述浅拷贝、深拷贝、引用拷贝：

![浅拷贝、深拷贝、引用拷贝示意图](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/basis/shallow&deep-copy.png)

java的复制对象的属性（简单拷贝，并没有涉及对象里面的对象那种情况）也可以认为是浅拷贝

```java
package org.example;

public class Main  {
    public static void main(String[] args) throws CloneNotSupportedException {
        A a=new A(1,"cao","add");
        A b=new A(2,"li","sum");
        b= (A) a.clone();
        System.out.println(b.id +" " +b.name);
        System.out.println(a==b);
        System.out.println(a.hashCode());
        System.out.println(b.hashCode());
    }


}
class A implements Cloneable{
    public  int id;
    public  String name;
    public  String address;

    public A(int id, String name, String address) {
        this.id = id;
        this.name = name;
        this.address = address;
    }
    public Object clone() throws CloneNotSupportedException {
        return  super.clone();
    }
}

```

![image-20230206194454673](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230206194454673.png)

java的引用拷贝

```java
package org.example;

public class Main  {
    public static void main(String[] args) throws CloneNotSupportedException {
        A a=new A(1,"cao","add");
        A b=a;
        //b= (A) a.clone();
        System.out.println(b.id +" " +b.name);
        System.out.println(a==b);
        System.out.println(a.hashCode());
        System.out.println(b.hashCode());
    }


}
class A implements Cloneable{
    public  int id;
    public  String name;
    public  String address;

    public A(int id, String name, String address) {
        this.id = id;
        this.name = name;
        this.address = address;
    }
    public Object clone() throws CloneNotSupportedException {
        return  super.clone();
    }
}

```

![image-20230206195238653](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230206195238653.png)

# hashCode() 有什么用？

`hashCode()` 的作用是获取哈希码（`int` 整数），也称为散列码。这个哈希码的作用是确定该对象在哈希表中的索引位置。

总结下来就是 ：

- 如果两个对象的`hashCode` 值相等，那这两个对象不一定相等（哈希碰撞）。
- 如果两个对象的`hashCode` 值相等并且`equals()`方法也返回 `true`，我们才认为这两个对象相等。
- 如果两个对象的`hashCode` 值不相等，我们就可以直接认为这两个对象不相等。

#### 为什么重写 equals() 时必须重写 hashCode() 方法？

因为两个相等的对象的 `hashCode` 值必须是相等。也就是说如果 `equals` 方法判断两个对象是相等的，那这两个对象的 `hashCode` 值也要相等。

如果重写 `equals()` 时没有重写 `hashCode()` 方法的话就可能会导致 `equals` 方法判断是相等的两个对象，`hashCode` 值却不相等。

**思考** ：重写 `equals()` 时没有重写 `hashCode()` 方法的话，使用 `HashMap` 可能会出现什么问题。

## String

`String` 中的对象是不可变的，也就可以理解为常量，线程安全。`AbstractStringBuilder` 是 `StringBuilder` 与 `StringBuffer` 的公共父类，定义了一些字符串的基本操作，如 `expandCapacity`、`append`、`insert`、`indexOf` 等公共方法。`StringBuffer` 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。`StringBuilder` 并没有对方法进行加同步锁，所以是非线程安全的。

**性能**

每次对 `String` 类型进行改变的时候，都会生成一个新的 `String` 对象，然后将指针指向新的 `String` 对象。`StringBuffer` 每次都会对 `StringBuffer` 对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用 `StringBuilder` 相比使用 `StringBuffer` 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

**对于三者使用的总结：**

1. 操作少量的数据: 适用 `String`
2. 单线程操作字符串缓冲区下操作大量数据: 适用 `StringBuilder`
3. 多线程操作字符串缓冲区下操作大量数据: 适用 `StringBuffer`

`String` 真正不可变有下面几点原因：

1. 保存字符串的数组被 `final` 修饰且为私有的，并且`String` 类没有提供/暴露修改这个字符串的方法。
2. `String` 类被 `final` 修饰导致其不能被继承，进而避免了子类破坏 `String` 不可变。

#### intern 方法有什么作用?

`String.intern()` 是一个 native（本地）方法，其作用是将指定的字符串对象的引用保存在字符串常量池中，可以简单分为两种情况：

- 如果字符串常量池中保存了对应的字符串对象的引用，就直接返回该引用。
- 如果字符串常量池中没有保存了对应的字符串对象的引用，那就在常量池中创建一个指向该字符串对象的引用并返回。

示例代码（JDK 1.8） :

```java
// 在堆中创建字符串对象”Java“
// 将字符串对象”Java“的引用保存在字符串常量池中
String s1 = "Java";
// 直接返回字符串常量池中字符串对象”Java“对应的引用
String s2 = s1.intern();
// 会在堆中在单独创建一个字符串对象
String s3 = new String("Java");
// 直接返回字符串常量池中字符串对象”Java“对应的引用
String s4 = s3.intern();
// s1 和 s2 指向的是堆中的同一个对象
System.out.println(s1 == s2); // true
// s3 和 s4 指向的是堆中不同的对象
System.out.println(s3 == s4); // false
// s1 和 s4 指向的是堆中的同一个对象
System.out.println(s1 == s4); //true
```

对于 `String str3 = "str" + "ing";` 编译器会给你优化成 `String str3 = "string";` 。

并不是所有的常量都会进行折叠，只有编译器在程序编译期就可以确定值的常量才可以：

- 基本数据类型( `byte`、`boolean`、`short`、`char`、`int`、`float`、`long`、`double`)以及字符串常量。
- `final` 修饰的基本数据类型和字符串变量
- 字符串通过 “+”拼接得到的字符串、基本数据类型之间算数运算（加减乘除）、基本数据类型的位运算（<<、>>、>>> ）

**引用的值在程序编译期是无法确定的，编译器无法对其进行优化。**

对象引用和“+”的字符串拼接方式，实际上是通过 `StringBuilder` 调用 `append()` 方法实现的，拼接完成之后调用 `toString()` 得到一个 `String` 对象 。



```java
String str4 = new StringBuilder().append(str1).append(str2).toString();
```

我们在平时写代码的时候，尽量避免多个字符串对象拼接，因为这样会重新创建对象。如果需要改变字符串的话，可以使用 `StringBuilder` 或者 `StringBuffer`。

不过，字符串使用 `final` 关键字声明之后，可以让编译器当做常量来处理。

示例代码：



```java
final String str1 = "str";
final String str2 = "ing";
// 下面两个表达式其实是等价的
String c = "str" + "ing";// 常量池中的对象
String d = str1 + str2; // 常量池中的对象
System.out.println(c == d);// true
```

被 `final` 关键字修改之后的 `String` 会被编译器当做常量来处理，编译器在程序编译期就可以确定它的值，其效果就相当于访问常量。

如果 ，编译器在运行时才能知道其确切值的话，就无法对其优化。

示例代码（`str2` 在运行时才能确定其值）：



```java
final String str1 = "str";
final String str2 = getStr();
String c = "str" + "ing";// 常量池中的对象
String d = str1 + str2; // 在堆上创建的新的对象
System.out.println(c == d);// false
public static String getStr() {
      return "ing";
}
```

# try-catch-finally 如何使用？

- `try`块 ： 用于捕获异常。其后可接零个或多个 `catch` 块，如果没有 `catch` 块，则必须跟一个 `finally` 块。

- `catch`块 ： 用于处理 try 捕获到的异常。

- `finally` 块 ： 无论是否捕获或处理异常，`finally` 块里的语句都会被执行。当在 `try` 块或 `catch` 块中遇到 `return` 语句时，`finally` 语句块将在方法返回之前被执行。

- **注意：不要在 finally 语句块中使用 return!** 当 try 语句和 finally 语句中都有 return 语句时，try 语句块中的 return 语句会被忽略。这是因为 try 语句中的 return 返回值会先被暂存在一个本地变量中，当执行到 finally 语句中的 return 之后，这个本地变量的值就变为了 finally 语句中的 return 返回值。

  # 异常

**Unchecked Exception** 即 **不受检查异常** ，Java 代码在编译过程中 ，我们即使不处理不受检查异常也可以正常通过编译。

`RuntimeException` 及其子类都统称为非受检查异常，常见的有（建议记下来，日常开发中会经常用到）：

- `NullPointerException`(空指针错误)
- `IllegalArgumentException`(参数错误比如方法入参类型错误)
- `NumberFormatException`（字符串转换为数字格式错误，`IllegalArgumentException`的子类）
- `ArrayIndexOutOfBoundsException`（数组越界错误）
- `ClassCastException`（类型转换错误）
- `ArithmeticException`（算术错误）
- `SecurityException` （安全错误比如权限不够）
- `UnsupportedOperationException`(不支持的操作错误比如重复创建同一用户)

# Throwable 类常用方法有哪些？

- `String getMessage()`: 返回异常发生时的简要描述
- `String toString()`: 返回异常发生时的详细信息
- `String getLocalizedMessage()`: 返回异常对象的本地化信息。使用 `Throwable` 的子类覆盖这个方法，可以生成本地化信息。如果子类没有覆盖该方法，则该方法返回的信息与 `getMessage()`返回的结果相同
- `void printStackTrace()`: 在控制台上打印 `Throwable` 对象封装的异常信息

# BufferedInputStream类(缓存)

```java
import java.io.*;
class 左移右移
{
	
	public static void main(String[] args) {
       try (BufferedInputStream bin = new BufferedInputStream(new FileInputStream(new File("javaNope.jar")));
            BufferedOutputStream bout = new BufferedOutputStream(new FileOutputStream(new File("1.jar")))) {
          int b;
        while ((b = bin.read()) != -1) {
         bout.write(b);
    }
  }
      catch (IOException e) {
      e.printStackTrace();
    }
    }
}
```

![img](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/basis/spi/1ebd1df862c34880bc26b9d494535b3dtplv-k3u1fbpfcp-watermark.png)

# jvm的内存形式

jdk1.8之前的

![Java 运行时数据区域（JDK1.8 之前）](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/jvm/java-runtime-data-areas-jdk1.7.png)

jdk1.8之后的

![Java 运行时数据区域（JDK1.8 之后）](https://guide-blog-images.oss-cn-shenzhen.aliyuncs.com/github/javaguide/java/jvm/java-runtime-data-areas-jdk1.8.png)



# Stream流（针对于集合来说）

![image-20230210165852576](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230210165852576.png)

# 函数式接口编程

用接口函数的方法，并且传值，和重写，并运行

```java
if (new Function<String, Boolean>() {
            @Override
            public Boolean apply(String s) {
                System.out.println(s);
                return false;
            }
        }.apply("A")){
            System.out.println("A");
        }else {
            System.out.println("B");
        }
```

# Java 并发工具箱之concurrent包

![img](https://img-blog.csdn.net/20170301212847989?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2J3ang=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

概述
java.util.concurrent 包是专为 Java并发编程而设计的包。包下的所有类可以分为如下几大类：

locks部分：显式锁(互斥锁和速写锁)相关；
atomic部分：原子变量类相关，是构建非阻塞算法的基础；
executor部分：线程池相关；
collections部分：并发容器相关；
tools部分：同步工具相关，如信号量、闭锁、栅栏等功能；

## Lock

```java
package threadLearnPool;

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class SuoID implements Runnable{
   static int id=0;
   Lock lock=new ReentrantLock();
    @Override
    public  void run() {    //线程加锁
        lock.lock();
        for (int i=0;i<10000;i++){      //线程不同步
            id++;
        }
        lock.unlock();
    }

    public int getId() {
        return id;
    }
}

```

## BlockingQueue接口以及实现类

此接口是一个线程安全的 存取实例的队列。

使用场景
BlockingQueue通常用于一个线程生产对象，而另外一个线程消费这些对象的场景。

![img](https://img-blog.csdn.net/20170227071415737?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2J3ang=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

注意事项：
此队列是有限的,如果队列到达临界点，Thread1就会阻塞，直到Thread2从队列中拿走一个对象。
若果队列是空的，Thread2会阻塞，直到Thread1把一个对象丢进队列。
相关方法
BlockingQueue中包含了如下操作方法：

![image-20230217225235501](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230217225235501.png)
名词解释：
Throws Exception: 如果试图的操作无法立即执行，抛一个异常。
Special Value: 如果试图的操作无法立即执行，返回一个特定的值(常常是 true / false)。
Blocks: 如果试图的操作无法立即执行，该方法调用将会发生阻塞，直到能够执行。
Times Out: 如果试图的操作无法立即执行，该方法调用将会发生阻塞，直到能够执行，但等待时间不会超过给定值。返回一个特定值以告知该操作是否成功(典型的是 true / false)。
注意事项：
无法插入 null，否则会抛出一个 NullPointerException。
队列这种数据结构，导致除了获取开始和结尾位置的其他对象的效率都不高，虽然可通过remove(o)来移除任一对象。
实现类
因为是一个接口，所以我们必须使用一个实现类来使用它，有如下实现类：

ArrayBlockingQueue： 数组阻塞队列
DelayQueue： 延迟队列
LinkedBlockingQueue： 链阻塞队列
PriorityBlockingQueue： 具有优先级的阻塞队列
SynchronousQueue： 同步队列

## CountDownLatch

CountDownLatch 是一个并发构造，它允许一个或多个线程等待一系列指定操作的完成。

CountDownLatch 以一个给定的数量初始化。countDown() 每被调用一次，这一数量就减一。
通过调用 await() 方法之一，线程可以阻塞等待这一数量到达零。
CyclicBarrier
CyclicBarrier 类是一种同步机制，它能够对处理一些算法的线程实现同步。

更多实例参考： CyclicBarrier

## Exchanger

Exchanger 类表示一种两个线程可以进行互相交换对象的会和点。

更多实例参考： Exchanger

## Semaphore

Semaphore 类是一个计数信号量。具备两个主要方法：

acquire()
release()
每调用一次 acquire()，一个许可会被调用线程取走。
每调用一次 release()，一个许可会被返还给信号量。
Semaphore 用法
保护一个重要(代码)部分防止一次超过 N 个线程进入。
在两个线程之间发送信号。
保护重要部分
如果你将信号量用于保护一个重要部分，试图进入这一部分的代码通常会首先尝试获得一个许可，然后才能进入重要部分(代码块)，执行完之后，再把许可释放掉。

Semaphore semaphore = new Semaphore(1);  
//critical section  
semaphore.acquire();  
...  
semaphore.release();

在线程之间发送信号
如果你将一个信号量用于在两个线程之间传送信号，通常你应该用一个线程调用 acquire() 方法，而另一个线程调用 release() 方法。

如果没有可用的许可，acquire() 调用将会阻塞，直到一个许可被另一个线程释放出来。
如果无法往信号量释放更多许可时，一个 release() 调用也会阻塞。
公平性
无法担保掉第一个调用 acquire() 的线程会是第一个获得一个许可的线程。

可以通过如下来强制公平：

Semaphore semaphore = new Semaphore(1, true); 
1
需要注意，强制公平会影响到并发性能，建议不使用。

## ExecutorService

这里之前有过简单的总结： Java 中几种常用的线程池

存在于 java.util.concurrent 包里的 ExecutorService 实现就是一个线程池实现。

实现类
此接口实现类包括：

ScheduledThreadPoolExecutor ： 通过 Executors.newScheduledThreadPool(10)创建的
ThreadPoolExecutor: 除了第一种的其他三种方式创建的
相关方法
execute(Runnable)：
无法得知被执行的 Runnable 的执行结果
submit(Runnable)：
返回一个 Future 对象，可以知道Runnable 是否执行完毕。
submit(Callable)：
Callable 实例除了它的 call() 方法能够返回一个结果，通过Future可以获取。
invokeAny(…)：
传入一系列的 Callable 或者其子接口的实例对象，无法保证返回的是哪个 Callable 的结果 ，只能表明其中一个已执行结束。
如果其中一个任务执行结束(或者抛了一个异常)，其他 Callable 将被取消。
invokeAll(…)：
返回一系列的 Future 对象，通过它们你可以获取每个 Callable 的执行结果。
关闭ExecutorService
shutdown() ： 不会立即关闭，但它将不再接受新的任务
shutdownNow()： 立即关闭
ThreadPoolExecutor
ThreadPoolExecutor 使用其内部池中的线程执行给定任务(Callable 或者 Runnable)。
ScheduledExecutorService（接口，其实现类为ScheduledThreadPoolExecutor）
ScheduledExecutorService能够将任务延后执行，或者间隔固定时间多次执行。
ScheduledExecutorService中的 任务由一个工作者线程异步执行，而不是由提交任务给 ScheduledExecutorService 的那个线程执行。
相关方法
schedule (Callable task, long delay, TimeUnit timeunit)：
Callable 在给定的延迟之后执行，并返回结果。
schedule (Runnable task, long delay, TimeUnit timeunit)
除了 Runnable 无法返回一个结果之外，和第一个方法类似。
scheduleAtFixedRate (Runnable, long initialDelay, long period, TimeUnit timeunit)
这一方法规划一个任务将被定期执行。该任务将会在首个 initialDelay 之后得到执行，然后每个 period 时间之后重复执行。
period 被解释为前一个执行的开始和下一个执行的开始之间的间隔时间。
scheduleWithFixedDelay (Runnable, long initialDelay, long period, TimeUnit timeunit)
和上一个方法类似，只是period 则被解释为前一个执行的结束和下一个执行的结束之间的间隔。

## ForkJoinPool

ForkJoinPool 在 Java 7 中被引入。它和 ExecutorService 很相似，除了一点不同。ForkJoinPool 让我们可以很方便地把任务分裂成几个更小的任务，这些分裂出来的任务也将会提交给 ForkJoinPool。

用法参考：Java Fork and Join using ForkJoinPool

Lock
Lock 是一个类似于 synchronized 块的线程同步机制。但是 Lock 比 synchronized 块更加灵活、精细。

实现类
Lock是一个接口，其实现类包括：

ReentrantLock
示例
Lock lock = new ReentrantLock();  
lock.lock();  
//critical section  
lock.unlock();
调用lock() 方法之后，这个 lock 实例就被锁住啦。
当lock示例被锁后，任何其他再过来调用 lock() 方法的线程将会被阻塞住，直到调用了unlock() 方法。
unlock() 被调用了，lock 对象解锁了，其他线程可以对它进行锁定了。
Lock 和 synchronized区别
synchronized 代码块不能够保证进入访问等待的线程的先后顺序。
你不能够传递任何参数给一个 synchronized 代码块的入口。因此，对于 synchronized 代码块的访问等待设置超时时间是不可能的事情。
synchronized 块必须被完整地包含在单个方法里。而一个 Lock 对象可以把它的 lock() 和 unlock() 方法的调用放在不同的方法里。

## ReadWriteLock

读写锁一种先进的线程锁机制。

允许多个线程在同一时间对某特定资源进行读取，
但同一时间内只能有一个线程对其进行写入。
实现类
ReentrantReadWriteLock
规则
如果没有任何写操作锁定，那么可以有多个读操作锁定该锁
如果没有任何读操作或者写操作，只能有一个写线程对该锁进行锁定。
示例：

ReadWriteLock readWriteLock = new ReentrantReadWriteLock();  
readWriteLock.readLock().lock();  
    // multiple readers can enter this section  
    // if not locked for writing, and not writers waiting  
    // to lock for writing.  
readWriteLock.readLock().unlock();  
readWriteLock.writeLock().lock();  
    // only one writer can enter this section,  
    // and only if no threads are currently reading.  
readWriteLock.writeLock().unlock();

更多原子性包装类
位于 atomic包下，包含一系列原子性变量。

AtomicBoolean
AtomicInteger
AtomicLong
AtomicReference
…

# java反射创建对象并调用方法

```java
package org.example;

import java.lang.reflect.Field;
import java.lang.reflect.Method;

public class ClassforNew {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("org.example.People");
        Object o = clazz.newInstance();
        //无论那种方式来使用都是一个套路
        //0.类加载   (class.forName())
        //1.创建对象 (通过类来创建对象newInstance())
        //2.得到方法 (方法名字，参数的class)
        //3.方法调用(对象,参数，参数)
        Method dosome = clazz.getMethod("dosome");
        Method dosome1 = clazz.getMethod("dosome",String.class);
        Method dosome2 = clazz.getMethod("dosome",int.class,String.class);
        dosome2.invoke(o,1,"王五");
        dosome1.invoke(o,"张三");
        dosome.invoke(o);
    }
}

```

# jvm垃圾回收机制（GC）

1.GC只针对于堆内存，Java语言中不存在指针说法，而是叫引用，**在堆内存中没有被任何栈内存引用的对象应该被回收**。

## 引用计数算法（肯定不采用）

​    引用计数算法是判断对象是否存活的算法之一：**它给每一个对象加一个引用计数器，每当有一个地方引用它时，计数器值就加1；当引用失效时，计数器值就减1；任何时刻计数器为0的对象就是不可能被使用的，即将被垃圾回收器回收。**

**缺点：无法解决对象减互相循环引用的问题。即当两个对象循环引用时，引用计数器都为1，当对象周期结束后应该被回收却无法回收，造成内存泄漏**。

## 可达性分析算法

​    目前主流使用的都是可达性分析算法来判断对象是否存活。算法基本思路：**以“GC Roots”作为对象的起点,从此节点开始向下搜索，搜索所走过的路径成为引用链（Reference Chain），当一个对象到GC Roots没有任何引用链相连时，则证明此对象是不可用的。**

![img](https://ask.qcloudimg.com/http-save/yehe-5522483/wm8k2bt3uj.jpeg?imageView2/2/w/1620)

**哪些对象可作为GC Roots？**

- 虚拟机栈（栈帧中的本地变量表）中引用的对象；
- 方法区中类静态属性引用的对象；
- 方法区中常量引用的对象；
- 本地方法栈中JNI（Native方法）引用的对象；
- 活跃线程的引用对象。

# java的xml文件在resources里面的读取

```java
package org.example;

import org.dom4j.Document;
import org.dom4j.Element;
import org.dom4j.Node;
import org.dom4j.io.SAXReader;
import sun.nio.cs.Surrogate;

import java.io.FileInputStream;
import java.io.InputStream;
import java.util.List;
import java.util.PropertyResourceBundle;
import java.util.ResourceBundle;
import java.util.function.Consumer;

public class Main {
    public static void main(String[] args) throws Exception{
        SAXReader reader = new SAXReader();
        //获取一个输入流，指向配置文件
        Document document = reader.read(Main.class.getClassLoader().getResource("test.xml"));
        //读文件
        System.out.println(document);
        Element rootElement = document.getRootElement();//该文件的根标签
        System.out.println(rootElement.getName());
        List<Element> elements = rootElement.elements("property");//根目录下的标签
        elements.forEach(element->{
            Element elt=(Element) element;
            String id = elt.attributeValue("id");              //根标签里面的属性
            System.out.println(id);
        });
       // List<Node> nodes = document.selectNodes("//id");这个方法一定要安装jaxen的jar包

        //System.out.println(element.getName());

//        List<Node> nodes1 = element.selectNodes("//id");
//        nodes1.stream()
//                .forEach(new Consumer<Node>() {
//                    @Override
//                    public void accept(Node node) {
//                        System.out.println(node);
//                    }
//                });

     //   List<Node> nodes = document.selectNodes("//property");
    /**    nodes.forEach(node -> {
                    Element beanElt = (Element) nodes;
                    String id = beanElt.attributeValue("id");
                    System.out.println(id);
                });
        System.out.println("Hello world!");**/
    }
}
```

# java对URL进行编码和解码

## 代码

- 引入

```java
import java.net.URLEncoder;
import java.net.URLDecoder;
```

- 编码

```cobol
URLEncoder.encode( URL, "UTF-8" )
```

- 解码

```cobol
URLDecoder.decode( URL, "UTF-8" )
```

```java
String packageName1="工作区";
        String packagePath1 = packageName1.replaceAll("\\.", "/");//.正则表达式是可以匹配任何值，替代/,所以现在bean可以有四个/
        URL url1 = ClassLoader.getSystemClassLoader().getResource(packageName1);
        try {
            String decode = URLDecoder.decode(url1.toString(), "UTF-8");
            System.out.println(decode);
        } catch (UnsupportedEncodingException e) {
            throw new RuntimeException(e);
        }

```

# 2、无边界通配符：？

而无边界通配符？则只能用于填充泛型变量T，表示通配任何类型！！！！再重复一遍：？只能用于填充泛型变量T。它是用来填充T的！！！！只是填充方式的一种！！！

```java
package 工作区;

public class BEl1 {
    public static void main(String[] args) {
        BEI <?> yu=new BEI<>();//<T extends 贝贝>
        yu.setId(34);
        System.out.println(yu.getId());
    }
}                                                 //都是用来约束泛型
```

```java
package com.powernode.client;

import com.powernode.service.OrderService;
import com.powernode.service.OrderServicelmpl;
import com.powernode.service.TimerInvocationHandler;

import java.lang.reflect.Proxy;

public class Client {
    //客户端程序
    public static void main(String[] args) {

        //创建目标对象
        OrderService target=new OrderServicelmpl();
        //创建代理对象
        /**
         * 1.newProxyInstance 翻译为：新建代理对象
         * 也就是说通过调用这个方法可以创建代理对象：
         * 本质上 Proxy.newProxyInstance()方法的执行做了两件事，
         * 第一件事：在内存中动态的生成了一个代理类的字节码class，
         * 第二件事：new对象了，通过内存中生成的代理类这个代码，实例化了代理对象，
         * 2.关于newProxyInstance()方法的三个重要参数，每一个什么含义，有什么用？
         * 第一个参数：ClassLoader loader  程序传入jvm中需要类加载器
         * 类加载器，这个类加载器有什么用呢？
         * 第二个参数：Class<?>[] interfaces  创建对象需要对应的接口
         * 第三个参数： InvocationHandler h  被翻译为：调用处理器，是一个接口，
         *            在调用处理器接口中编写的就是：增强代码，
         *            因为具体要增强什么代码，jdk动态代理技术它是猜不到的，没有那么神
         *            既然是接口就要写接口的实现类。
         * 注意：代理对象和目标对象实现的接口一样，所以可以向下转型
         */
        OrderService o =(OrderService) Proxy.newProxyInstance(target.getClass().getClassLoader(),
                                                        target.getClass().getInterfaces(),
                                                         new TimerInvocationHandler(target));
        //调用代理对象的代理方法
        o.generate();
        //客户端每调用一次方法，jvm都会执行一次invoke
        o.modify();
        o.detail();
    }
}

```

```java
package com.powernode.service;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

/**
 * 专门负责记时的一个调用处理器对象
 * 在这个调用处理器当中编写记时相关的增强代码，
 * 这个调用处理器只需要写一个就行了。
 */
/**
 1.为什么强行要求你必须实现 InvocationHandler接口？
 因为一个类实现接口就必须实现接口中的方法。
 以下这个方法必须是invoke（），因为jdk在底层调用invoke（）方法的程序已经写好了
 注意：invoke（）方法是jdk负责调用的
 2.invoke方法什么时候被调用呢？
 当代理对象调用代理方法的时候，注册在InvocationHandler调用处理器当中的invoke()方法被调用。

 3.invoke方法的三个参数：
 invoke方法是jdk负责调用的，所以jdk调用这个方法的时候会自动给我们传过来这三个参数，
 我们可以在main括号里面直接使用
 第一个参数，Object proxy 代理对象的引用，这个参数使用较小
 第二个参数：Method method 目标对象上的目标方法，（要执行的目标方法就是它，）
 第三个参数: Object[] args 目标方法上的实参,

 invoke方法执行过程中，使用method来调用目标对象的目标方法。
 */
public class TimerInvocationHandler implements InvocationHandler {
    //目标对象
    private Object target;
    public TimerInvocationHandler(Object target) {
        //赋值给成员变量，
        this.target=target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //调用目标对象上的目标方法
        //
        long begin=System.currentTimeMillis();
       // System.out.println("增强1");
       // method.invoke(target,args);

       // System.out.println("增强2");
       long end=System.currentTimeMillis();
        System.out.println("耗时"+(end-begin)+"毫秒");
        return null;
    }
}

```

## method方法的getName和get返回类型，可以确定唯一方法

# CGLIB

```java

```

# 泛型

```java
public  static  <AnyType extends Comparable< AnyType>>
    int binarySearch(AnyType[] a,AnyType x)
    {
        int low=0,high=a.length-1;
        while (low<=high){
            int mid =(low+high)/2;
            if (a[mid].compareTo(x)<0)
                low=mid+1;
            else if(a[mid].compareTo(x)>0)
                high=mid-1;
            else return mid;
        }
        return -1;
    }

    public static  <AnyType> void sayHello(AnyType k){   //属性<AnyType> 
        AnyType i=k;
        System.out.println(i);
    }


    public static void main(String[] args) {
        Integer[] a=new Integer[34];
        int i=0;
        for (Integer c:a){
            a[i]=i;
            i++;
        }
        Integer b=23;
        System.out.println(binarySearch(a, b));
        sayHello(b);

    }
```











