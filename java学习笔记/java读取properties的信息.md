```java
public void test8() {
        
        ResourceBundle rb2 = ResourceBundle.getBundle("jdbc");//读取resources/jdbc
        String u2=  rb2.getString("user");
        String password= rb2.getString("password");
        String url= rb2.getString("url");
        String JDBC_DRIVER= rb2.getString("JDBC_DRIVER");
        System.out.println(u2+password+url+JDBC_DRIVER);
    }
```

```java
public void test9(){
        try {

            FileReader fileReader=new FileReader("D:\\ASM\\idea工作区\\spring6\\spring6-001-revelation\\src\\main\\resources\\jdbc.properties");//这个方法只能搞绝对路径
            Properties p1=new Properties();
            p1.load(fileReader);
            fileReader.close();
            String className=p1.getProperty("user");
            System.out.println(className);

        } catch (FileNotFoundException e) {
            throw new RuntimeException(e);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
```

# java获取 /resources 目录资源文件的 6 种方法

发布于2022-10-30 15:02:34阅读 1.7K0

# 公用的打印文件方法



```javascript
/**
 * 根据文件路径读取文件内容
 *
 * @param fileInPath
 * @throws IOException
 */
public static void getFileContent(Object fileInPath) throws IOException {
    BufferedReader br = null;
    if (fileInPath == null) {
        return;
    }
    if (fileInPath instanceof String) {
        br = new BufferedReader(new FileReader(new File((String) fileInPath)));
    } else if (fileInPath instanceof InputStream) {
        br = new BufferedReader(new InputStreamReader((InputStream) fileInPath));
    }
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
    br.close();
}
```

复制

>   方式一：主要核心方法是使用getResource和getPath方法，这里的getResource("")里面是空字符串

```javascript
public void function1(String fileName) throws IOException {
    String path = this.getClass().getClassLoader().getResource("").getPath();//注意getResource("")里面是空字符串
    System.out.println(path);
    String filePath = path + fileName;
    System.out.println(filePath);
    getFileContent(filePath);
}
```

复制

>   方式二：主要核心方法是使用getResource和getPath方法，直接通过getResource(fileName)方法获取文件路径，注意如果是路径中带有中文一定要使用URLDecoder.decode解码。

```javascript
/**
 * 直接通过文件名getPath来获取路径
 *
 * @param fileName
 * @throws IOException
 */
public void function2(String fileName) throws IOException {
    String path = this.getClass().getClassLoader().getResource(fileName).getPath();//注意getResource("")里面是空字符串
    System.out.println(path);
    String filePath = URLDecoder.decode(path, "UTF-8");//如果路径中带有中文会被URLEncoder,因此这里需要解码
    System.out.println(filePath);
    getFileContent(filePath);
}
```

复制

>   方式三：直接通过文件名+getFile()来获取文件。如果是文件路径的话getFile和getPath效果是一样的，如果是URL路径的话getPath是带有参数的路径。

```javascript
/**
 * 直接通过文件名+getFile()来获取
 *
 * @param fileName
 * @throws IOException
 */
public void function3(String fileName) throws IOException {
    String path = this.getClass().getClassLoader().getResource(fileName).getFile();//注意getResource("")里面是空字符串
    System.out.println(path);
    String filePath = URLDecoder.decode(path, "UTF-8");//如果路径中带有中文会被URLEncoder,因此这里需要解码
    System.out.println(filePath);
    getFileContent(filePath);
}
```

复制

>   方式四（重要）：直接使用getResourceAsStream方法获取流，上面的几种方式都需要获取文件路径，但是在SpringBoot中所有文件都在jar包中，没有一个实际的路径，因此可以使用以下方式。

```javascript
/**
 * 直接使用getResourceAsStream方法获取流
 * springboot项目中需要使用此种方法，因为jar包中没有一个实际的路径存放文件
 *
 * @param fileName
 * @throws IOException
 */
public void function4(String fileName) throws IOException {
    InputStream in = this.getClass().getClassLoader().getResourceAsStream(fileName);
    getFileContent(in);
}
```

复制

>   方式五（重要）：主要也是使用getResourceAsStream方法获取流，不使用getClassLoader可以使用getResourceAsStream("/配置测试.txt")直接从resources根路径下获取，SpringBoot中所有文件都在jar包中，没有一个实际的路径，因此可以使用以下方式。

```javascript
/**
 * 直接使用getResourceAsStream方法获取流
 * 如果不使用getClassLoader，可以使用getResourceAsStream("/配置测试.txt")直接从resources根路径下获取
 *
 * @param fileName
 * @throws IOException
 */
public void function5(String fileName) throws IOException {
    InputStream in = this.getClass().getResourceAsStream("/" + fileName);
    getFileContent(in);
}
```

复制

>   方式六（重要）：通过ClassPathResource类获取文件流，SpringBoot中所有文件都在jar包中，没有一个实际的路径，因此可以使用以下方式。

```javascript
/**
 * 通过ClassPathResource类获取，建议SpringBoot中使用
 * springboot项目中需要使用此种方法，因为jar包中没有一个实际的路径存放文件
 *
 * @param fileName
 * @throws IOException
 */
public void function6(String fileName) throws IOException {
    ClassPathResource classPathResource = new ClassPathResource(fileName);
    InputStream inputStream = classPathResource.getInputStream();
    getFileContent(inputStream);
}
```

```java
  SAXReader reader=new SAXReader();

            //获取一个输入流，指向配置文件
            InputStream in = ClassLoader.getSystemClassLoader().getResourceAsStream(configLocation);
            //读文件
            Document document = reader.read(in);
            List<Node> nodes = document.selectNodes("//bean");
```

