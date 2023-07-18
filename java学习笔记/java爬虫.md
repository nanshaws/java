# 一、Jsoup概述

jsoup 是一款Java 的HTML解析器，可直接解析某个URL地址、HTML文本内容。它提供了一套非常省力的API，可通过DOM，CSS以及类似于jQuery的操作方法来取出和操作数据。

关键信息：jsoup可以解析html文档。

那么，解析html文档和爬虫有什么关系呢？

网页要在浏览器显示，离不开html，要是我们能够解析它的html，那么我们就能获取其中的数据。

# 二、Jsoup使用

使用jsoup不需要繁琐的配置，直接导包就可以开始干。

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.13.1</version>
</dependency>
```


Joup中有很多类和方法，但实际上常用的就几个，我们来敲个代码试试。

```java
package vip.yangsf;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

import java.io.IOException;

public class ForBaidu {
    public static void main(String[] args) throws IOException {
        Document document = Jsoup.connect("https://www.baidu.com").get();
        System.out.println(document.getElementsByTag("title"));
    }
}
```


然后我们就获得了这个标签，操作和js一毛一样。

# 三、为什么老是被和谐，老子爬个公开的信息怎么了

我们来做一个爬取商品信息的案例：

访问它的网址（哎不敢说名字啊被和谐三次了），搜索Java

会发现地址栏是这样的：

https://search.jd.com/Search?keyword=java&enc=utf-8&wq=java&pvid=f9e0a8114fdc4692bc75096d4fff6a75

简单读一读，发现是一个get请求，“ ? ” 后面是参数，那么精简一下：

https://search.jd.com/Search?keyword=java&enc=utf-8

## 得到了url，我们就可以解析它的html，先获得dom：

```java
Document document = Jsoup.connect("https://search.jd.com/Search?keyword=java&enc=utf-8").get();//获取dom
```


按f12观察网页，检查一下商品名在哪个标签里面



观察发现，在一个id为J_goodsList的div下面的一个类名为p-namediv下，然后我们还可以看出，每一个商品就是一个li。



于是：

```java
Elements elements = document.getElementById("J_goodsList").getElementsByTag("li");//dom文件根据id下面的所有位置，.getElementsByTag("li")方法就是查找这个li属性里面的值
```



# 获取J_goodsList下的所有li。

遍历每一个li，获取里面的数据，并输出（例如获取商品名）

```java
for (Element e : elements) {
    System.out.println(e.getElementsByClass("p-name").get(0).getElementsByTag("em").text());
}//foreach循环打印输出
```

同样，我们可以通过同样的方法获取它的价格以及图片地址。

# 完整代码：

商品类：

```java
package vip.yangsf.pojo;

public class Goods {
    private String img;
    private String name;
    private String price;
public Goods() {
}

public Goods(String img, String name, String price) {
    this.img = img;
    this.name = name;
    this.price = price;
}

public String getImg() {
    return img;
}

public void setImg(String img) {
    this.img = img;
}

public String getName() {
    return name;
}

public void setName(String name) {
    this.name = name;
}

public String getPrice() {
    return price;
}

public void setPrice(String price) {
    this.price = price;
}

@Override
public String toString() {
    return "Goods{" +
            "img='" + img + '\'' +
            ", name='" + name + '\'' +
            ", price='" + price + '\'' +
            '}';
 }
}
```


爬取商品信息：

```java
package vip.yangsf;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;
import vip.yangsf.pojo.Goods;

import java.io.IOException;
import java.util.ArrayList;
import java.util.Collection;

public class JsoupTest {
    public static void main(String[] args) throws IOException {
        // 查询java第二页的商品信息
        Collection<Goods> goods = paseJD("java", 2);
        // 输出每一个商品的信息
        goods.forEach(System.out::println);
    }
// 我们可以让搜索的关键字和页数传进来，更灵活
public static Collection<Goods> paseJD(String keyword, int page) throws IOException {
    // 待会儿每爬到一个商品就把它加进来
    Collection<Goods> goods = new ArrayList<>();
    // 把url拼接出来
    String url = "https://search.jd.com/Search?keyword=" + keyword + "&enc=utf-8&page=" + page;
    // 拿到DOM就可以开始操作
    Document document = Jsoup.connect(url).get();
    String img = null;
    String name = null;
    String price = null;
    Elements elements = document.getElementById("J_goodsList").getElementsByTag("li");
    for (Element e : elements) {
        // 这里商品图片是懒加载，直接获取src获取不到
        img = e.getElementsByTag("img").attr("data-lazy-img");
        name = e.getElementsByClass("p-name").get(0).getElementsByTag("em").text();
        price = e.getElementsByClass("p-price").text();
        goods.add(new Goods(img, name, price));
    }
    return goods;
  }
}
```

# 实操

```java
package org.example;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException {
        Document document = Jsoup.connect("https://www.bilibili.com/video/BV1S8411T7Wj/?spm_id_from=333.1007.tianma.1-1-1.click").get();
       // Element app = document.getElementById("app");//id下面的所有
        //System.out.println(app.getElementsByTag("span"));//id下面的所有并且符号条件的
        Elements elementsByClass = document.getElementsByClass("mini-header__title");//class那个范围
        System.out.println(elementsByClass);
       // System.out.println(document);

    }
}
```

![image-20230218202224202](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230218202224202.png)

























