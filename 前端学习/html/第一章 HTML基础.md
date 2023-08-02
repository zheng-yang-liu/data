# 第一章 HTML基础

## 一、基本概念

#### 1、www(万维网)

world wide web(万维网),是互联网上的一种服务，通过网络提供HTTP服务，也可以理解为web服务（网站服务）

#### 2、网站和网页

网站是网页和资源的集合，在服务器上表现为一个文件夹。

databases：数据库文件，用于存储数据的备份。

logfiles:用于存储日志文件。（log,日志）

wwwroot:网站的根目录

#### 3、前端和后端

前端：页面及交互，即用户可以接触到的内容。主要用到的技术HTML+CSS+JS

HTML功能：组织页面内容

CSS：布局定位，网页美化

 js:网页交互及特效

后端：在服务器上运行程序，用于访问数据库，实现业务逻辑程序。



## 二、web标准

w3c（万维网联盟）



## 三、HTML 

HTML（hyper text markup language)超文本标记语言，通过标签来表示网页中的文本、图片、按钮等网页元素的一种语言。

### 一）基本的标签

#### 1、标签构成（单双分类）

单标签：由一个标签构成，标签内一般会书写关闭符。如：<br / ><hr /> <img /><input> 

双标签：<div></div> <li></li><p></p>

#### 2、标签构成（结构）

<标签名 属性名=”属性值“   属性名=”属性值“>

#### 3、一个网页基本结构



```
<!DOCTYPE html>   --文档类型声明
<html>
<head>
    <title></title>  网页标题
    <meta name="keywords"   content="鸭脖,美味鸭脖"/> 元数据标签(网页关键字)
    <meta name="description"   content=""/>     网页的描述信息
    <meta chartset="UTF-8" /> 指定网页所用的字符集
    <style></style>
    <link href=""  type="text/css" />
    <script></script>
</head>
<body></body>

</html>
```

#### 4、常用标签

- h1-h6: 标题标签
- hr:水平线标签
- p: 段落标签
- br:换行标签

<!-- 注释信息 快捷键: ctrl+/ -->

- 图片标签：

  <img src="图片资源的地址"  alt=""  title=""  width="" height=""  border=""/>

  alt="" 指图片无法显示时的提示文本

  title="" 鼠标悬停的提示文本

- 超链接

  ```
  <a href="跳转的网页" title="鼠标悬停的提示文本"  target="_blank/_self/框架名"></a>
  ```

  href:指定跳转地址。

  target:指定跳转位置。有三个取值：_blank,在新窗口或新标签下打开链接， _ self，默认值，在当前标签或者窗口下打开链接。框架名，用于指定在指定的框架中打开链路。

  空链接：

  ```
  <a href="#">xxx</a>
  ```

  锚链接：实现同一个页面不同位置跳转。

  实现锚链接的步骤：

  1）创建锚点

  ```
  <a name="锚点名"></a>
  ```

  2）锚链接

  ```
  <a href="#锚点名">xxx</a>
  ```

- 背景颜色和背景图片

<body bgcolor="#ffff00">  背景颜色

<<body background="图片地址">   背景图片

- 列表

  - 有序列表

  ```
  <ol type="1/a/A/I/i">
      <li>起床</li>
       <li>吃饭</li>
       <li>上学</li>
  </ol>
  ```

  - 无序列表 

```
<ul type="disc">
	<li>项目一,disc实心圆</li>
	<li>项目二，square正方形</li>
	<li>项目三circle空心圆</li>
</ul>
```

- 定义列表

```
<dl>
	<dt>茶</dt>
	<dd>是一种饮品，来自于东方古国中国</dd>
</dl>
```



- 表格

  ```
  <table>
  	<tr><td>1</td><td>2</td></tr>
  	<tr><td>1</td><td>2</td></tr>
  </table>
  
  cellspacing 单元格的间距
  cellpadding 单元格的内容到单元格边缘的距离
  tr:行标签
  td:单元格
  th:表头，功能相当于单元格，可以使单元中的文本加粗居中显示
  align:left(左对齐)，right(右对齐)，center(居中对齐)，用于设置整个表格或者单元格内容的对齐方式。
  colspan：跨列属性
  rowspan：跨行属性
  caption:标题
  ```

  实现单元格跨行、跨列步骤：

  1、制作出标准的表格

  2、找到需要设置跨行、跨列属性的单元格，为其添加跨行或跨列属性。

  3、删除因跨行或跨列而多余出来的单元格。

  示例：

```
<table border="1" width="200">
	<caption>成绩表</caption>
	<thead><tr><td>1</td><td>张三</td><td>李四</td></tr></thead> 
	<tbody>
	<tr><td>1</td><td rowspan="2">2</td><td rowspan="2">3</td></tr>
	<tr><td>1</td><td rowspan="2">2</td><td rowspan="2">3</td></tr>
	<tr><td>1</td><td rowspan="2">2</td><td rowspan="2">3</td></tr>
	</tbody>
	<tfoot><tr><td>1</td></tr></tfoot>

</table>
```

```
表格的子标签：
<thead></thead>  表格的头部

<tbody></tbody>表格的主体

<tfoot></tfoot> 表格的底部
```



#### 5、路径

相对路径：从当前文件夹开始到达到要访问的资源的路径叫做相对路径。

绝对路径：对于网站来说，从网站根目录开始的路径叫绝对路径。

