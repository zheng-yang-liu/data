# 第七章 JS事件

## 一、事件及事件的绑定方法

## 一）事件概念

#### 1、概念

事件是文档或者浏览器窗口中发生的，特定的交互瞬间。

#### 2、典型的事件

- 页面加载完毕，window.onload
- 浏览器窗口放大或缩小，触发resize事件
- 用户单击元素，触发click事件

### 二）绑定事件的方法

#### 1、在标签中添加事件属性

```
<button onclick="函数"></button>
```

#### 2、在脚本中使用匿名函数绑定事件

```
对象.事件=匿名函数
window.onload=function(){}
```

#### 3、在脚本中使用addEventListener()绑定事件

```
对象.addEventListener(“事件名”,函数,布尔值)
```

```
示例：
btn.addEventListener("click",function(){
			alert("我是第二种绑定事件的方法");
		},false)
```

```
btn.removeEventListener("click",function(){//解除绑定
			alert("我是第二种绑定事件的方法");
		},false);
```

## 二、鼠标事件

| **事件名**  | **描述**             |
| ----------- | -------------------- |
| onclick     | 鼠标点击某个对象     |
| ondblclick  | 鼠标双击某个对象     |
| onmouseover | 鼠标被移到某元素之上 |
| onmouseout  | 鼠标从某元素移开     |
| onmousedown | 某个鼠标按键被按下   |
| onmousemove | 鼠标被移动           |
| onmouseup   | 某个鼠标按键被松开   |

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		li{
			cursor: pointer;
			line-height: 40px;
		}
	</style>
</head>
<body>
	<ul>
		<li onclick="changeColor()">点我变色</li>
		<li>双击有惊喜！！！</li>
		<li>鼠标滑过字体变大，鼠标离开字体变小</li>
		<li><b>鼠标按下文字变为红色，鼠标按键松开文字变为绿色</b></li>
	</ul>
	<script>
		var li=document.getElementsByTagName('li');
		function changeColor(){
			li[0].style.background="red";
		}
		li[1].addEventListener("dblclick",function(){
			li[1].style.color="pink";
		},false)
		li[2].onmouseover=function(){
			li[2].style.fontSize="24px";
		}
		li[2].onmouseout=function(){
			li[2].style.fontSize="14px";
		}
		li[3].onmousedown=function(){
			li[3].style.color="red";
		}
		li[3].onmouseup=function(){
			li[3].style.color="green";
		}
		li[3].onmousemove=function(){
			console.log("1");
		}
	</script>
</body>
</html>
```

## 三、表单事件

| **事件名** | **描述**         |
| ---------- | ---------------- |
| onfocus    | 元素获得焦点     |
| onblur     | 元素失去焦点     |
| onchange   | 用户改变域的内容 |
| onreset    | 表单重置时触发   |
| onsubmit   | 表单提交时触发   |

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<form action="demo2.html" onreset="resetFn()" onsubmit="return submitFn()">
		<p>当输入框获取焦点时，修改背景色</p>
		<p>用户名：<input type="text"></p>
		<p>离开输入框,将输入文字转换成大写</p>
		<p>密码：<input type="text" id="pass"></p>
		<p>选中文本：<input type="text" onselect="selectFn()"></p>
		<p><input type="reset" value="重置"></p>
		<p><input type="submit" value="提交"></p>
	</form>
	
	<script>
		var input=document.getElementsByTagName('input');
		input[0].onfocus=function(){
			input[0].style.background="yellow";
		} 
		input[1].onblur=function(){
			input[1].value=input[1].value.toUpperCase();
		} 
		function selectFn(){
			alert("您已选中文本！");
		}
		//重置不支持input标签，支持form标签
		function resetFn(){
			alert("表单已重置");
		}
		function submitFn(){
			var pass=document.getElementById('pass').value;
			if (pass.length<6){
				
				alert('密码小于6位，请重新输入！');
				document.getElementById('pass').value="";
				document.getElementById('pass').focus();
				return false;
	
			}else{
				return true;

			}
			//alert("表单已提交");
		}
	</script>
</body>
</html>
```

## 四、键盘事件

| **事件名** | **描述**                             |
| ---------- | ------------------------------------ |
| onkeydown  | 某个键盘的键被按下                   |
| onkeypress | 某个键盘的键被按下并释放一个键时发生 |
| onkeyup    | 某个键盘的键被松开                   |

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<p>请按下任意一个键：<input type="text" onkeydown="keyDown()" onkeyup="keyUp()"></p>
	<p>请按下一个键并释放：<input type="text" onkeypress="keyPress()"></p>
	<script>
		var input=document.getElementsByTagName('input');
		function keyDown(){
			input[0].style.background="red";
		}
		function keyUp(){
			input[0].style.background="blue";
		}
		function keyPress(){
			input[1].style.background="pink";
		}
	</script>
</body>
</html>
```

## 五、UI事件

### 一）概念

UI（User Interface，用户界面）事件，指的是那些不一定与用户操作有关的事件。

### 二）事件类型

| **事件名** | **描述**                 | 代码          |
| ---------- | ------------------------ | ------------- |
| onload     | 某个页面或图像被完成加载 | window.onload |
| onresize   | 窗口或框架被调整尺寸     |               |
| onscroll   | 当文档被滚动时发生的事件 |               |

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		div {
		    border: 1px solid black;
		    width: 200px;
		    height: 100px;
		    overflow: scroll;
		}
	</style>
</head>
<body onresize="reSizeFn()">
	<h1>Hello World！！！</h1>
	<div id="myDiv">In my younger and more vulnerable years my father gave me some advice that I've been turning over in my mind ever since.
	<br>
	'Whenever you feel like criticizing anyone,' he told me, just remember that all the people in this world haven't had the advantages that you've had.'
	</div>
	<script>
		window.onload=function(){
			alert("页面加载完成");
		}
		function reSizeFn(){
			alert("您改变了浏览器窗口大小！");
		}
		var myDiv=document.getElementById("myDiv");
		myDiv.onscroll=function(){
			alert("您滚动了div！");
		}
	</script>
</body>
</html>
```

## 六、Event对象

### 一）功能语法 

#### 1、功能

用来获取事物的详细信息：鼠标位置、键盘按键

#### 2、获取event对象语法

```
var oEvent=e||event;
```

### 二）事件流

事件流有两种情况：一种是事件冒泡传播，另一种是捕获传播。

#### 1、事件冒泡传播

当一个元素接收到事件的时候会把他接收到的事件传给自己的父级，一直到window。

示例参考代码：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
#box1{
background-color:aqua;width: 600px;height: 600px;}
#box2{background-color:palevioletred;width: 400px;
height: 400px;}
#box3{background-color:gold;width: 200px;height: 200px;}
   </style>
</head>
<body>
<div id="box1">box1
<div id="box2">box2<div id="box3">box3 </div></div>
</div>
<script>
//给div添加点击事件，实现冒泡效果
document.querySelector('#box1').addEventListener('click', function(){
alert('我是大盒子');
//event.stopPropagation();   //停止冒泡的代码
},)
document.querySelector('#box2').addEventListener('click', function(){
alert('我是中盒子');
//event.stopPropagation();
},)
document.querySelector('#box3').addEventListener('click', function(){
alert('我是小盒子');
//event.stopPropagation();
},)
</script>
</body>
</html>
```

#### 2、阻止冒泡语法

```
event.stopPropagation();
event.cancelBubble=true;//IE支持，谷歌两种都兼容
```

#### 3、事件捕获传播

事件从外到内，大到小传播事件捕获传播。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
<style>
#box1{background-color:aqua;width: 600px;height: 600px;}
#box2{background-color:palevioletred;width: 400px;height: 400px;}
#box3{background-color:gold;width: 200px;height: 200px;}
</style>
</head>
<body>
<div id="box1">box1
<div id="box2">box2<div id="box3">box3 </div></div>
</div>
<script>
//给div添加点击事件，实现捕获效果
document.querySelector('#box1').addEventListener('click', function(){
alert('我是大盒子');
},true)
document.querySelector('#box2').addEventListener('click', function(){
alert('我是中盒子');
},true)
document.querySelector('#box3').addEventListener('click', function(){
alert('我是小盒子');
},true)
</script>
</body>
</html>
```

### 三）阻止默认行为

```
return false;
```

```
document.oncontextmenu=function(){//阻止右键菜单
		return false;  //阻止默认行为
}
```

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		*{
			padding: 0;margin: 0;list-style: none;
		}
		#menu{
			position: absolute;width: 300px;height: 200px;line-height: 40px;background: #fff;border: 1px #ccc solid;display: none;
			padding-left: 20px;
		}
	</style>
</head>
<body>
	<ul id="menu">
		<li>返回</li>
		<li>重新加载</li>
		<li>另存为（A）...</li>
		<li>打印（P）...</li>
		<li>查看网页源代码</li>
	</ul>
	<script>
		document.oncontextmenu=function(e){
			var oEvent=e||event;
			var menu=document.getElementById("menu");
			menu.style.display="block";
			menu.style.left=oEvent.clientX+"px";
			menu.style.top=oEvent.clientY+"px";
			return false;
		}
		document.onclick=function(){
			menu.style.display="none";
		}
	</script>
</body>
</html>
```



## 七、拖动元素

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		#box{
			width: 150px;height: 150px;background: red;position: absolute;cursor: move;
		}
	</style>
</head>
<body>
	<div id="box"></div>
	<script>
		var box=document.getElementById("box");
		box.onmousedown=function(e){
			var oEvent=e||event;
			//鼠标点击盒子的位置
			var x=oEvent.clientX-box.offsetLeft;
			var y=oEvent.clientY-box.offsetTop;
			document.onmousemove=function(e){
				var oEvent=e||event;
				//盒子到浏览器的左边距、上边距
				var left=oEvent.clientX-x;
				var top=oEvent.clientY-y;
				var maxW=document.documentElement.clientWidth-box.offsetWidth;
				var maxH=document.documentElement.clientHeight-box.offsetHeight;
				if(left<0)left=0;
				if(top<0)top=0;
				if(left>maxW)left=maxW;
				if(top>maxH)top=maxH;
				box.style.left=left+"px";
				box.style.top=top+"px";
			}
		}
		box.onmouseup=function(){
			document.onmousemove=null;
		}
	</script>
</body>
</html>
```

