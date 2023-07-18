# js学习笔记

## 嵌入Javascript代码的三种方式

### 第二种方式

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<!-- css样式块 -->
		<style type="text/css">
			
		</style>
	</head>
	<body>
		<!-- 嵌入脚本块 -->
		<script type="text/javascript">
			/**
			 * 暴露在代码块的代码执行起来是一加载就开始执行
			 * 并且是逐行执行，自上而下的执行
			 */放在任何位置都是可以的
			window.alert("Hello World");
			window.alert("javascript");  //alert函数会阻塞整个HTML文件的加载
		</script>
		<input type="button" value="我是一个按钮对象" />
	</body>
</html>
```

### 第一种方式

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<input type="button" value="hello" onclick="window.alert('傻逼')
		window.alert('250')
		window.alert('傻逼')
		window.alert('傻逼')
		window.alert('傻逼')"
		/>
		<input type="button" value="hello" onclick="alert('傻逼')
		alert('250')
		alert('傻逼')
		alert('傻逼')
		alert('傻逼')"
		/>
	</body>
</html>
```

### 第三种方式

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>                                               
		<!-- 在需要的位置引入js脚本文件 -->
		<script type="text/javascript" src="真js/001.js">
			//这里写代码没有用
			//window.alert("sb");
            //JavaScript的注释就跟Java一样
		</script>
		

	</body>
</html>
```

## javaScript的标识符和关键字

### 跟Java一样

## 变量

### 变量的定义和规则

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			var i=100;
			i="sb";
			i=123.45
			//undefined在js中是个值
			alert("i="+ i);
			//在js中变量没有初始化时，系统会默认赋值，undefined
			var a;
			alert("a=" + a);
			alert(ku);  //语法错误
		</script>
	</body>
</html>
```

![image-20230106085845814](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230106085845814.png)

## js函数

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			/**
			 * js的函数
			 */
			function sum(a,b){
				//a,b都是局部变量都是形参
				alert(a+b);              //js不能重载，就是后面一个函数覆盖前一个函数
			}
			//函数必须调用才能执行
			// sum(10,20);
			
			function sayhello(){
				alert("hello");
			}
			// sayhello();
		</script>
		<input type="button" value="hello" onclick="sayhello();" />
	</body>
</html>
```

![image-20230106110803605](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230106110803605.png)

![image-20230106111517982](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230106111517982.png)

## js的数据类型

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			function sum(a,b){
				if(typeof a=="number" && typeof b=="number"){
					return a+b
				}
				//typeof的运算结果是六个字符串之一，全是字符串
				//"undefined number string object boolean null" 类型
				//typeof等于"undefined number string object boolean function"
				//null类型的typeof运算结果是object
			}
		var u=	sum("a","b");
		alert(u);
	    u=sum(1,2);
		alert(u);
		</script>
	</body>
</html>
```

### Number

![image-20230106164551601](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230106164551601.png)

### string的方法

substr（startIndex,length）

substring  (startIndex,endindex)

## js里面的类和类里面的函数

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			function mysum(a,b){
				this.a=a;//类，类似于java里面的构造方法
				this.b=b;
			}
			var a=new mysum(1,3);
			alert(a.a+a.b);
			mysum.prototype.sum=function(){
				alert("hello");         //js里面的方法，好像只能用这个来写类里面的方法
			}
			a.sum();
		</script>
	</body>
</html>
```

## 事件

- onclick：单击事件
- ondblclick：双击事件

2）焦点事件

- onblur：失去焦点
- onfocus:元素获得焦点。

3）加载事件：

- onload：一张页面或一幅图像完成加载。

4）鼠标事件：

- onmousedown 鼠标按钮被按下。
- onmouseup 鼠标按键被松开。
- onmousemove 鼠标被移动。
- onmouseover 鼠标移到某元素之上。
- onmouseout 鼠标从某元素移开。

5）键盘事件：

- onkeydown 某个键盘按键被按下。
- onkeyup 某个键盘按键被松开。
- onkeypress 某个键盘按键被按下并松开。

6）选择和改变事件

- onchange 域的内容被改变。
- onselect 文本被选中。

7）表单事件：

- onsubmit 确认按钮被点击。
- onreset 重置按钮被点击。

把on去掉就是事件，加on是事件句柄

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			window.onload=function(){
				document.getElementById("t1").onclick=function(){
					alert("hello");
				}
			}
		</script>
		<input type="button" id="t1" value="hello">
	</body>
</html>
```

如果不加window.load的话，那个就必须要求相对应的html文件要放到事件的前面

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<input type="button" id="t2" value="hello1"/>        //比如说这个事件
		<script type="text/javascript">
			window.onload=function(){
				document.getElementById("t1").onclick=function(){
					alert("hello");
				}
			}
			function c (){
				alert("hello1");
			}
			var b=document.getElementById("t2");
			b.onclick=c;
			
			// window.onload= read();
			
			// function read(){
			// 	document.getElementById("t2").onclick=c(); 
			// }
			window.onload= read;
			function read(){                              //window.onload可以有两个吗？
				var b=document.getElementById("t2");
				b.onclick=c;
			}
//有一个
//    我们都知道在javascript中window.onload 只能有一个如果有多个的话后面的会覆盖前面的，
    
		</script>
		<input type="button" id="t1" value="hello">
	</body>
</html>
```

### js代码回车键事件

回车键的键值是13

esc的键值是27

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<input type="text" placeholder="登录">
		<br />
		<input type="text" placeholder="密码"  id="t3"/>
		<script type="text/javascript">
			window.onload=function(){
		   var b	=	document.getElementById("t3")
		   b.onkeydown=function(event){
			   if(event.keyCode==13){
				   alert("登录成功");
			   }
		   }
			}
		</script>
		
	</body>
</html>
```

### 事件点击改变html属性

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		
		<script type="text/javascript"> 
			window.onload=function(){
			var b=	document.getElementById("t4");
			b.onclick=function(){
			var c=	document.getElementById("t5");
			c.type="checkbox";
			}
			}
		</script>
		<input type="text" id="t5">
		<input type="button" id="t4" value="hello">
	</body>
</html>
```

### javascript: void(0)

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<p>tou</p>
		<br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
		<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
		<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
		<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
		<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
		<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />
		<br /><br /><br /><br /><br /><br /><br /><br />
		<br /><br /><br /><br /><br />
		<script type="text/javascript">
			window.onload=function(){
				document.getElementById("t6").onclick=function(){
					alert("sb");
				}
			}
		</script>
		<a href="javascript:void(0)" id="t6">sbsbbsbsbbsbsbbsb</a>
	</body>
</html>
```

## js的控制语句

除开Java本身的

![image-20230108081752629](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230108081752629.png)



for in遍历下标。

![image-20230108081942741](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230108081942741.png)



![image-20230108082948656](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230108082948656.png)

## dom

![image-20230108083821522](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230108083821522.png)

![image-20230108083950836](C:\Users\cao'yang'lin\AppData\Roaming\Typora\typora-user-images\image-20230108083950836.png)



```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
		   window.onload=function(){
			 var b=   document.getElementById("t8")
			 b.onclick=function(){
			// // var c=	document.getElementById("t7");
			// // alert(c.value);

			//alert(document.getElementById("t7").value);
			document.getElementById("t9").value=document.getElementById("t7").value
			}
		}	
		</script>
		
		<input type="text" id="t7">
		<input type="text" id="t9"/>
		<input type="button" id="t8" value="获取文本框的value">
	</body>
</html>
```

## dom控制div

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			div{
				width: 300px;
				height: 300px;
				border: 1px solid red;
				background-color: antiquewhite;
				
			}
		</style>
	</head>
	<body>
		<script type="text/javascript">
			window.onload=function(){
			var t=	document.getElementById("div1");
			t.innerHTML="<font>saidlsakj</font>"
			t.innerText="<font>saidlsakj</font>"
			}
		</script>
		<div id="div1">
			
		</div>
	</body>
</html>
```

## bom001跳转和跳回去

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<script type="text/javascript">
			
			window.onload=function(){
				document.getElementById("baidu").onclick=function(){
					window.open("bom002.html");
				}
			}
		</script>
		<input type="button" value="baidu" id="baidu">
	</body>
</html>
```

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<p>这里是bom002</p>
		<input type="button" value="跳回去" id="13"/>
		<script type="text/javascript">
			document.getElementById("13").onclick= function(){
				window.close();
			}
         window.location.assign("http://127.0.0.1:8848/Project/js/bom/bom001.html")//加载另一个页面
		</script>
	</body>
</html>
```

### window.location

```javascript
document.write(location.href); //路径，显示当前页面的路径
```

window.location.assign(url) ： 加载 URL 指定的新的 HTML 文档。 就相当于一个链接，跳转到指定的url，当前页面会转为新页面内容，可以点击后退返回上一个页面。

window.location.replace(url) ： 通过加载 URL 指定的文档来替换当前文档 ，这个方法是替换当前窗口页面，前后两个页面共用一个窗口，所以是没有后退返回上一页的

# js正则表达

```javascript
/正则表达式主体/修饰符(可选)
```

```javascript
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<body>

<p>替换 "microsoft" 为 "Runoob" :</p>
<button onclick="myFunction()">点我</button>
<p id="demo">Visit microsoft!
Visit microsoft!	</p>

<script>
function myFunction() {
    var str = document.getElementById("demo").innerHTML; 
    var txt = str.replace(/microsoft/g,"Runoob");           //g是全局的，也就是说所有的microsoft都要变
    document.getElementById("demo").innerHTML = txt;        //如果换成i就是只改第一个
}
</script>

</body>
</html>
```

| i    | 执行对大小写不敏感的匹配。                               |
| ---- | -------------------------------------------------------- |
| g    | 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。 |
| m    | 执行多行匹配。                                           |

| [abc]  | 查找方括号之间的任何字符。 |
| ------ | -------------------------- |
| [0-9]  | 查找任何从 0 至 9 的数字。 |
| (x\|y) | 查找任何以 \| 分隔的选项。 |

元字符是拥有特殊含义的字符：

| 元字符 | 描述                                        |
| :----- | :------------------------------------------ |
| \d     | 查找数字。                                  |
| \s     | 查找空白字符。                              |
| \b     | 匹配单词边界。                              |
| \uxxxx | 查找以十六进制数 xxxx 规定的 Unicode 字符。 |

量词:

| 量词 | 描述                                  |
| :--- | :------------------------------------ |
| n+   | 匹配任何包含至少一个 *n* 的字符串。   |
| n*   | 匹配任何包含零个或多个 *n* 的字符串。 |
| n?   | 匹配任何包含零个或一个 *n* 的字符串。 |

## 创建正则表达式对象

var b = /[0-9]/修饰符(可选)

var b=new RegExp();

## 正则表达式判断是否正确

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		
		<div id="16"></div>
		<script type="text/javascript">
		var str = "Visit Runoob1!123";
		 var der="3347004610@qq.com";
		var n =/^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/;//A到Z的大小写字母，0到9，
		var r=new RegExp(/^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/);
		alert(r.test(der));
		//26个大小写英文字母表示为a-zA-Z
        // 数字表示为0-9
        //下划线表示为_
        //中划线表示为-
        //由于名称是由若干个字母、数字、下划线和中划线组成，所以需要用到+表示多次出现
		//分析域名部分：
		
	/**	 一般域名的规律为“[N级域名][三级域名.]二级域名.顶级域名”，比如“qq.com”、“www.qq.com”、“mp.weixin.qq.com”、“12-34.com.cn”，分析可得域名类似“** .**  .** .**”组成。
		
		“**”部分可以表示为[a-zA-Z0-9_-]+
		“.**”部分可以表示为\.[a-zA-Z0-9_-]+
		多个“.**”可以表示为(\.[a-zA-Z0-9_-]+)+
		 综上所述，域名部分可以表示为[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+
		**/
		var ok=n.test(str);
		var zij=n.test(der);
		alert(ok);
		alert(zij);
		</script>
	</body>
</html>
```

# eval函数可以执行字符串里面的值

## json对象

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>json</title>
	</head>
	<body>
		<script type="text/javascript">
			var s={
				name:"caoyanglin",
				age :18,
				xingbie:1
			}
        console.log(s);
		
		</script>
	</body>
</html>
```

JSON对象和JSON字符串相互转换

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>json</title>
	</head>
	<body>
		<script type="text/javascript">
			var s={
				name:"caoyanglin",
				age :18,
				xingbie:1
			}
			var s1=JSON.stringify(s);
			var s2=JSON.parse(s1);
        console.log(s);
		console.log(s1);
		console.log(s2);
		</script>
	</body>
</html>
```















