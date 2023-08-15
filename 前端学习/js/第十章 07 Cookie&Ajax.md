

# 第十章 Cookie&Ajax

## 一、Cookie

### 一）cookie简介

#### 1、概念

HTTP Cookie（也叫Web Cookie或浏览器 Cookie）是服务器发送到用户浏览器并保存在本地的一小块数据，它会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上。

#### 2、工作原理

 正常的cookie分发是通过扩展HTTP协议来实现的，服务器通过在HTTP的响应头中加上一行特殊的指示以提示浏览器按照指示生成相应的cookie。然而纯粹的客户端脚本如JavaScript等方式也可以生成cookie。

而cookie的使用是由浏览器按照一定的原则在后台自动发送给服务器的。浏览器检查所有存储的cookie，如果某个cookie所声明的作用范围大于等于将要请求的资源所在的位置，则把该cookie附在请求资源的HTTP请求头上发送给服务器。  

### 二）用途

通常，它用于告知服务端两个请求是否来自同一浏览器，如保持用户的登录状态。Cookie使基于无状态的HTTP协议记录稳定的状态信息成为了可能。

- 会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）
- 个性化设置（如用户自定义设置、主题等）
- 浏览器行为跟踪（如跟踪分析用户行为等）

### 三）cookie特性
- 同一个网站中所有页面共享一套Cookie

  例如：baidu.com/a.html  baidu.com/b.html这两个网址就是共用了一套cookie,且如果不使用一套cookie也麻烦，那也就是说登陆了a.html后，如果跳转到b.html还得再登陆，而使用一套cookie的话，就只用登陆一次

- 数量、大小有限

  cookie的大小和数量有限，根据浏览器的不同，cookie的大小也有区别，最小可能是4k，最大的可能是10k，且cookie数量也是有限制的，一般情况下，一个网站的cookie数量不会超过50条

- 过期时间

  过期时间是由自己设置的，超过时间后便自动删除了

### 四）使用JavaScript操作Cookie

#### 1、创建cookie

#####  1）语法

```
document.cookie=”名字=值 ”
```

##### 2）示例

```
<script>
document.cookie="user=family";
document.cookie="pass=123456";
alert(document.cookie);
</script>
```

注：*在本地测试cookie的时候即使是在localhost下也是不正常的，所以需要使用火狐浏览器来测试，因为在本地只有火狐浏览器能把cookie数据保留下来*

#### 2、删除cookie

##### 1)语法

```
过期时间：expires=时间
```

##### 2）示例

```
var oDate=new Date();
oDate.setDate(oDate.getDate()+8);//8天后过期
alert(oDate.getFullYear()+'-'+(oDate.getMonth()+1)+'-'+oDate.getDate());
document.cookie="user=family;
expires="+oDate";
```

注：如果需要cookie立即失效，可以使expires=-1。

### 五）封装cookie

将cookie的的操作封装到函数中，方便以后直接调用。

#### 1、创建cookie

setCookie(name,value,iDay)要传入三个值，分别表示：cookie名称、cookie值、存储时间

#### 2、获取cookie

getCookie(name)里面需要把cookie做一下字符串分割，分割后变为数组，再去循环数组，就可以得到cookie

#### 3、删除cookie

removeCookie(name)把时间设置为负1，即可代表时间已过期

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script>
	function setCookie(name,value,iDay){  //分别代表cookie名称、cookie值、存储时间
		//首先将cookie的格式拼出来
		//document.cookie="name=value;expires=date";
		//然后name就换为name,vlaue就换为value，至于date就要算出这个日期对象
		var oDate=new Date();
		oDate.setDate(oDate.getDate()+iDay);
		document.cookie='name+'='+value+';expires='+oDate';
	}
	//a=12; b=5; c=8; d=99
	function getCookie(name){
		//1、先给cookie做一下字符串分割，
		var arr=document.cookie.split("; ");//分割后变为数组，a=12 b=5 c=8 d=99
		//2、循环数组
		for(var i=0;i<arr.length;i++){
			var arr2=arr[i].split("=");  //根据“=”再次分割
			//arr2[0]——》存储的名称 abcd
			//arr2[1]——》存储的值 12 5 8 99
			if(arr2[0]==name){  //代表找到我想要的东西了 
				return arr2[1];
			}
		}
		//另一种可能，用户第一次来网站，还没有cookie，所以肯定什么也找不到。所以在循环一次后就直接return 一个字符串，告诉用户什么也没找到。
		return "";
	}
	function removeCookie(name){
		//name名称，再随便来个值1，后面的才是重点-1，时间过期了，所以就成为了负值
		setCookie(name,1,-1);
	}
	//setCookie('uesrName','huyangliuyi',365);
	//setCookie('password','987654',30);
	//试试看有没有读取到cookie
	//alert(getCookie('uesrName'));
	//删除cookie
	removeCookie('uesrName');
	//先看看里面有哪些数据
	alert(document.cookie);
	</script>
</body>
</html>
```

## 二、Ajax

### 一）简介

#### 1、概念

Ajax（Asynchronous Javascript And XML（异步JavaScript和XML））是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。

Ajax 不是一种新的编程语言，而是一种用于创建更好更快以及交互性更强的Web应用程序的技术。使用 JavaScript 向服务器提出请求并处理响应而不阻塞用户核心对象XMLHttpRequest。通过这个对象，JavaScript 可在不重载页面的情况与 Web 服务器交换数据，即在不需要刷新页面的情况下，就可以产生局部刷新的效果。

Ajax 是一种独立于 Web 服务器软件的浏览器技术。　Ajax 基于下列 Web 标准：

JavaScript、XML、HTML与 CSS 在 Ajax 中使用的 Web 标准已被良好定义，并被所有的主流浏览器支持。Ajax 应用程序独立于浏览器和平台。

#### 二）创建Ajax的步骤

#### 1、创建Ajax对象

```
非IE6语法：
var oAjax=new XMLHttpRequest();
老版本IE5 和 IE6语法：
var oAjax=new ActiveXObject("Microsoft.XMLHTTP")
```

```
if (window.XMLHttpRequest){
	var oAjax=new XMLHttpRequest();//  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
}else{
var oAjax=new ActiveXObject("Microsoft.XMLHTTP");// IE6, IE5 浏览器执行代码 
}
```

#### 2、连接到服务器

```
open(方法，文件名，同步异步)
参数一：post/get
参数二：请求的文件名
参数三：同步（false）  异步（true）
```

```
oAjax.open("GET","abc.txt",true);
```

1）post/get的区别：

|                      | **GET**                                                      | **POST**                                                     |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **缓存**             | **能被缓存**                                                 | **不能缓存**                                                 |
| **编码类型**         | **application/x-www-form-urlencoded**                        | **application/x-www-form-urlencoded 或 multipart/form-data。为二进制数据使用多重编码** |
| **历史**             | **参数保留在浏览器历史中**                                   | **参数不会保存在浏览器历史中**                               |
| **对数据长度的限制** | **当发送数据时，GET 方法向 URL 添加数据；URL 的长度是受限制的（URL 的最大长度是 2048 个字符）** | **无限制**                                                   |
| **对数据类型的限制** | **只允许 ASCII 字符**                                        | **没有限制，也允许二进制数据**                               |
| **安全性**           | **与 POST 相比，GET 的安全性较差，因为所发送的数据是 URL 的一部分** | **POST 比 GET 更安全，因为参数不会被保存在浏览器历史或 web 服务器日志中** |
| **可见性**           | **数据在 URL 中对所有人都是可见的**                          | **数据不会显示在 URL 中**                                    |

```
1、Get是用来从服务器上获得数据，而Post是用来向服务器上传递数据。
2、Get将表单中数据的按照variable=value的形式，添加到action所指向的URL后面，并且两者使用“?”连接，而各个变量之间使用“&”连接；Post是将表单中的数据放在form的数据体中，按照变量和值相对应的方式，传递到action所指向URL。
3、Get是不安全的，因为在传输过程，数据被放在请求的URL中，而Post的所有操作对用户来说都是不可见的。
4、Get传输的数据量小；而Post可以传输大量的数据，
5、Get限制Form表单的数据集的值必须为ASCII字符；而Post支持整个ISO10646字符集。默认是用ISO-8859-1编码
6、Get是Form的默认方法

```

2）同步异步区别:

- 同步交互：指发送一个请求,**需要等待返回,然后才能够发送下一个请求，有个等待过程；**
- 异步交互：指发送一个请求,**不需要等待返回,随时可以再发送下一个请求，即不需要等待。** 
- 区别：**一个需要等待，一个不需要等待，**在部分情况下，我们的项目开发中都会优先选择不需要等待的异步交互方式。

#### 3、发送请求

```
send()
```

```
oAjax.send();
```

#### 4、接收返回值

```
oAjax.onreadystatechange=function(){
		if (oAjax.readyState==4 && oAjax.status==200){
				alert("请求成功"+oAjax.responseText);
		}
		else{
				alert("请求失败"+oAjax.status);
		}
}
```

请求状态码：

```
onreadystatechange意思是当与服务器发生交互时，会发生的事件
readyState：告诉我们浏览器和服务器进行到哪一步了
从 0 到 4 发生变化。
0: 请求未初始化（还没有调用到open方法）
1: 服务器连接已建立（已调用send方法，正在发生请求）
2: 请求已接收（send方法完成，已接收到全部响应内容）
3: 请求处理中（解析响应内容）
4: 请求已完成，且响应已就绪
status	
200: "OK"
404: 未找到页面


```

## 三、JSON

### 一）json概念

JSON（JavaScript Object Notation）是一种轻量级的数据交换格式，它基于 ECMAScript 的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据

### 二）JSON语法规则

- 数据在名称/值对中

  JSON 数据的书写格式是：名称/值对

  ```
  "name" : "课工场"
  JSON 值：数字、字符串、逻辑值、数组、对象、null
  
  
  ```

  | **值**                  | **示例**                                                     |
  | ----------------------- | ------------------------------------------------------------ |
  | 数字（整数或浮点数）    | **{ "age":30 }**                                             |
  | 对象（在大括号中）      | { "name":"课工场" ,   "url":"http://www.kgc.cn/" }           |
  | 数组（在中括号中）      | {"sites": [{ "name":"课工场"   , "url":"http://www.kgc.cn/" }, { "name":"google" ,   "url":"www.google.com" } ]} |
  | 逻辑值（true 或 false） | { "flag":true }                                              |
  | **null**                | **{ "kgc":null }                                             |

- 数据由逗号分隔

- 大括号保存对象

- 中括号保存数组

### 三）JSON.parse()和JSON.stringify()

#### 1、JSON.parse()

通过 JSON.parse() 解析数据，这些数据会成为 JavaScript 对象。

https://www.w3school.com.cn/js/js_json_parse.asp

#### 2、JSON.stringify()

通过 JSON.stringify() 把 JavaScript 对象转换为字符串。

https://www.w3school.com.cn/js/js_json_stringify.asp