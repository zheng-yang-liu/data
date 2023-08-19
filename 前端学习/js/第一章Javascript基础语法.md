# 第一章 Javascript基础语法

## 一、javascript简介

### 一）前端javascript功能

- 表单验证
- 网页特效
- 动态改变页面内容

### 二）概念

javascript是一种基于对象和事件驱动的脚本语言。

特点：

- 交互、脚本语言、解释性语言
- 边解释边执行

### 三）组成

ECMAScript (核心语法)

BOM（浏览器对象模型）browser object model

DOM（文档对象模型） document object model

### 四）javascript基本结构

```
<script type="text/javascript">
    <!--
          JavaScript 语句;
    -->
</script >

```

如：

```
alert("hello"); //弹出消息
	document.write("<h1>hello world!</h1>");//document.write()向网页输出内容
	document.write('<div style="border:1px dashed #f00;width:100px;height:100px;"></div>');
```



### 五）javascript执行原理

javascript脚本下载到浏览器，在客户端的浏览器上执行。

### 六）在网页中使用javascript脚本有三种方式

#### 1、在网页的<script type="text/javascript"></script>标签中放置javascript代码

```
<script type="text/javascript">
	javascript代码
</script>
```

#### 2、使用外部js文件

将js脚本放置到单独的js文件，在网页中使用<script src="js文件"></script>标签来调用外部文件。

#### 3、在标签中调用js脚本

在标签的事件属性值中添加js脚本。

```
<button onclick="alert('你点我了！')">按钮1</button>
```

## 二、ECMAScript语法

### 一）变量

1、变量的声明和赋值

- 先声明变量再赋值

- 同时声明和赋值变量，如： **var i, j, k = 15;**
- 不声明直接赋值，如： **userName= “六月”;i=1;**

### 二）数据类型

编程语言中使用的数据的分类叫作数据类型

- undefined，未定义，声明变量后未赋值，该变量存储的数据类型是未定义。
- null，空值，与undefined值相等。
- number，数值。可以用于进行算术运算的数据类型。
- boolean，布尔型，true,false。
- string，字符串，用双引号或单引号括起来。

使用typeof()函数可以判断数据的类型。

### 三）运算符

### 四）注释

/* ....*/   多行注释

//.....  单行注释

## 三、程序结构

### 一）程序结构分类

- 顺序结构
- 选择结构
- 循环结构

### 二）分支结构

#### 1、if语句

语法：

##### 1)单分支

if(条件){

​	代码块

}

##### 2）双分支

if(条件){

​	代码块1

}else{

​	代码块2

}

##### 3）多分支

if(条件1){

​	代码块1

}else if(条件2){

​	代码块2

}else if(条件3){

​	代码块3

}

..

else{

​	代码块n

}

var name=prompt("请输入您的姓名");

```
prompt("提示文本","默认值") //弹出一个输入框，提示用户输入内容。
parseInt(str) //将一个字符串转换为一个整数。
NaN 非数字
isNaN() 判断一个字符是否为纯数字，纯数字isNaN()函数的返回结果是false,非纯数字返回是true。
//isNaN()实例：
var k="19a";//纯数字isNaN()函数的返回结果是false,非纯数字返回是true
document.write(isNaN(k));

parseFloat(str) 将一个字符串转换为一个浮点数。
//parseFloat(str)实例：
var str="19.3a";
document.write(parseFloat(str));

break语句，终止代码块或循环的运行。

random() //用于生成0-1之间的一个随机数。
```

#### 2、switch语句

```
switch (表达式)
{         
        case 常量1 : 
 	     	javaScript语句1;
	     	break;
	     	......
	     case 常量2 : 
 	     	javaScript语句2;
	     	break;
	     	......
 	default: 
             javaScript语句n;
             break ;       
}

```



事件：

onclick 单击事件，某个元素单击时触发的事件。

onload,页面加载事件，整个网页加载完成后触发的一个事件。



