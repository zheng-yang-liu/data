# CSS层叠样式表

## 一、CSS介绍

#### 1、概念

CSS层叠样式，是一种对网页内容进行布局定位和美化的语言。

#### 2、功能

网页元素进行布局定位和美化

#### 3、分类

- 行内样式

书写在标签的Style属性中，只影响该标签的样式，如：

```
<span style="color:#f00;">层叠样式表</span>
```

- 内部样式

放到网页的<style></style>标签中，只影响该页面中的网页元素。如：

```
<!DOCTYPE html>
<head>
	<style>
		*{
		font-size:60px;
		}
	</style>
</head>
<body>
<h1>一级标题</h1>
<span style="color:#f00;">层叠样式表</span>
</body>
</html>
```

- 外部样式

放到单独的CSS文件中，需要在页面中使用<link href="样式表文件" rel="stylesheet" />来进行连接。（link标签必须放置在head标签中）如：

#### 4、样式出冲突时的优先级

行内样式优先，其它两个样式，后面的样式覆盖前面的样式。

#### 5、样式表的结构

选择器{

属性名:属性值;

属性名:属性值;

}

#### 6、选择器分类

- ID选择器

  用标签的ID值作为选择器的名称，并在前面加#的选择器。

  ```
  <div id="main"></div> <style>#main{width:100px;height:100px;background:#ff0;}</style>
  ```

- 类选择器

  使用.类名作为选择器名称。调用该类的标签都会应用该样式表。

  ```
  <div id="main" class="b2"></div> <style>.b2{border:2px solid #00f;}</style>
  ```

- 标签选择器

  使用标签名作为选择器。

！important>ID选择器>类选择器>标签选择器>浏览器默认样式

- *通配符

  一般用于清除浏览器默认的一些样式时使用。*{margin:0px;padding:0px;}

- 伪类选择器

  超链接伪类选择器

  a:link{}  未访问过的超链接的样式

  a:visited{} 访问过的超链接的样式

  a:hover{} 鼠标悬停的超链接的样式

  a:active{}  选定激活状态的超链接样式

  ```
  选择器:first-child{   #一组元素中的第一个元素,先找第一个子元素，再匹配选择器，如果一致就应用该样式，否则不应用。
  }
  选择器:nth-child(index){ #一组元素中的指定索引元素
  }
  选择器:last-child{	 #一组元素中的最后元素
  }
  选择器:first-of-type{} #直接找第一个匹配的选择器，应用样式表。
  选择器:nth-of-type(index){}
  选择器:last-of-type{}
  
  ```

  

- 组合选择器

  - 空格分隔
  
    ul li  后代关系
  
  - 大于号分隔
  
    ul>li 父子关系
  
  - 逗号分隔
  
    集体声明，当多个选择器的样式表完全一致时可以使用集体声明
  
  - ~分隔
  
       同级别的兄弟关系，如div ~ ul表示div 后的所有ul的样式。
  
  - +分隔符
  
    向下邻兄弟
  
    

## 二、字体、文本样式

## 一）字体样式

font-size    字体大小 ,像素（PX）em(行高)

font-weight 字体粗体 bolder,normal

font-family 字体类型,后跟一个用逗分开的字体列表。

font-style  字体风格 （normal,italic)

font: font-weight font-size/line-height font-family;

font:粗细 大小/行高 字体类型 （简写方式）

### 二）文本样式

line-height 行高

Text-transform 文本转换	

color 前景色

text-decoration:underline（下划线）

​							line-through (删除线)

​							none （无修饰）

​							overline(上划线)



word-spacing 单词间距

letter-spacing 字母间距

vertical-align 垂直对齐方式：顶部（top）、居中（middle)、底部(bottom)和基线(baseline)

text-indent :首行缩进

text-align:文本水平对齐方式（left左对齐，center居中对齐，right右对齐）

white-space:normal,nowrap(强制不换行)

over-flow:hidden;

text-over:ellipsis

text-shadow 字体阴影

### 三）关于网页颜色

网页中十六进制颜色值：R(红)，G（绿），B（蓝）三种颜色。色彩的三要素：色调、亮度、饱和度

用十进制来表示，每种颜色的取值都是0-255，用十六进制来表示每颜色取值是从00-ff,  如：红色十六进制的颜色是：#ff0000,绿色：#00ff00,蓝色：#0000ff.

rgb(红，绿，蓝)  每种颜色的取值是0-255

rgba(红，绿，蓝,透明度)  ，透明度取值是0-1，1不透明，0完全透明。



## 三、盒子模型

### 一）盒子属性

宽度：width

高度:height

内填充：padding(padding-left,padding-right,padding-bottom,padding-top)

边框：border:(border-left,border-right,border-bottom,border-top)

border-radius:圆角半径

外边框：margin（margin-left,margin-right,margin-bottom,margin-top)

margin:20px 50px; marign:上右下左

box-sizing:content-box,border-box,设定盒子的计算方式

box-shadow :盒子阴影

### 二）背景

背景颜色：background-color

背景图片：background-image:url();

背景重复：background-repeat:repeat-x,repeat-y,no-repeat;

背景尺寸： background-size

设置背景图原点：background-origin  padding-box, content-box,border-box

裁剪图片(指定背景绘制区域)：background-clip:border-box,padding-box,content-box,text

图片固定：background-attachment：fixed,scroll

背景图片位置：background-position:水平偏移距离 垂直偏移距离



## 四、浮动

### 一）浮动的三大特征

1、浮动的元素会脱离文档流，表现为向左或向右浮动。

2、浮动元素不再独占一行，浮动元素紧贴上一个浮动元素的边缘或容器的边缘。

3、占用文档空间，文档流会环绕浮动元素显示。

float:left/right

### 二）清除浮动

清除浮动：使浮动元素前后的元素不浮动的影响，换行显示。

clear:left; 清除左浮动

clear:right;清除右浮动

clear:both;清除左右浮动

## 五、盒子的box-sizing属性

box-sizing:border-box,content-box,设定不同的计算盒子宽度和高度方法。默认值是content-box.

box-sizing的取值是content-box 盒子的宽度计算：

盒子所占页面空的宽度=width+padding-left+padding-right+border-left+border-right+margin-left+magin-right

盒子所占页面空的宽度=height+padding-top+padding-bottom+border-top+border-bottom+margin-top+margin-bottom

box-sizing的取值是border-box 盒子的宽度计算：

盒子所占页面空的宽度=盒子width(border-left+border-right+paddint-left+padding-right)

盒子所占页面空的高度=盒子height(border-top+border-bottom+paddint-top+padding-bottom)

## 六、定位与盒子塌陷

### 一）定位和属性

position位置，取值:static,absolute,fixed,relative,sticky

left,top,bottom,right

### 二）定位的分类

#### 1、静态（static)

按照页面元素在文档流中的位置来进行定位,元素的默认的定位方式。

#### 2、绝对定位（absolute)

相对于第一个有定位属性的父元素的定位。绝对定位相当浮动效果，不占父容器宽和高度。

#### 3、相对定位（relative)

相对于元素原始位置的定位。元素原有的空间仍会保留。

#### 4、固定定位（fixed)

相对于浏览器窗口的定位。

#### 5、粘性定位（sticky）

不脱文档流，用于窗口滚动定位。在元素达到某个位置时将其固定。

### 三）绝对定位特点

绝对定位使元素脱离文档流，相当浮动效果，不占父容器宽和高度，会产生盒子塌陷现象。

## 七、元素的层叠属性

元素的层叠属性：

z-index属性可以设置元素的堆叠顺序，z-index的默认值是0，即文字流层。数值越大越靠上层。

body {
  cursor: url('./utils/default.cur'),auto;
}

## 八、display和overflow和鼠标样式

### 一）display

用于设置网页元素显示属性，常见的显示属性有三个：inline(行级)，block(块级),inline-block。

display:inline,元素在网页上显示时，以行级元素的方式来显示。

display:block,元素在网页上显示时，以块级元素的方式来显示。

display:inline-block,元素在网页上显示时，以行级块元素的方式来显示。

### 二）overflow

功能：指内容超出区域显示范围后区域的显示方式。

常见取值:

auto  自动，根据内容的多少来决定是否显示滚动条。

scroll，垂直和水平滚动条均显示。

hidden 溢出隐藏。

### 三）鼠标样式

cursor

 cursor: url('./utils/default.cur'),auto;

## 九、弹性布局

### 一）弹性布局的概念

弹性布局是css中一种布局手段，可以代替浮动来完成页面的布局。flex可以使元素具有弹性，让元素可以跟着页面大小的改变而改变。

### 二）弹性布局的实现

#### 1、弹性容器

要使用弹性盒子，必须先将一个元素设置为弹性容器，可以通过display来设置弹性容器。
display:flex 来设计为块级弹性容器
display:inline-flex 设计为行内的弹性容器（不会独占一行）

#### 2、主轴与侧轴

##### 1）主轴

弹性元素的排列方向成为主轴

##### 2）侧轴

与主轴垂直方向的称为侧轴

##### 3）设置主轴方向的属性

- flex-direction:row(默认值，弹性元素在容器中水平排列（从左向右排列）)
  主轴: 从左向右
- flex-direction:row-reverse(弹性元素在容器中反向水平排列（从右向左排列）)
  主轴: 从右向左
- flex-direction:column(弹性元素在容器中纵向排列（自上向下排列）)
  主轴: 自上向下
- flex-direction:column-reverse(弹性元素在容器中反向纵向排列（自下向上排列）)
  主轴: 自下向上

##### 4）flex-wrap属性

功能：设置弹性元素是否在弹性容器中自动换行

- flex-wrap:nowrap;  

  默认值 元素不会自动换行

- lex-wrap:wrap;

  元素沿着辅轴方向自动换行,如果元素是从左向右排列的，那么辅轴就是自上向下（向下排列）

- flex-wrap:wrap-reverse;

  元素沿着侧轴反方向换行，如果元素是从左向右排列的，那么辅轴就是自下向上（向上排列）

```
.a{
    width: 400px;
    border: 10px solid red ;
    display: flex;
    flex-wrap: nowrap;
    }
        .a li{
            flex-shrink: 0;
            font-size: 50px;
            line-height: 100px;
            text-align: center;
            list-style: none;
            height: 100px;
            width: 100px;
            background-color:red ;
        }
```

##### 5)flex-flow	

wrap和direction的简写属性

flex-flow:row wrap;

```
.a{ width: 400px; border: 10px solid red ; display: flex; flex-flow: row wrap; }
```

#### 6)justify-content

主轴上的元素如何排列,如何分配主轴上的空白空间

justify-content:flex-start;   元素沿着主轴起边排列

```
 .a{
            width: 800px;
            border: 10px solid red ;
            display: flex;
            /* flex-flow: row wrap; */
            justify-content: flex-start;
        }
        .a li{
            flex-shrink: 0;
            font-size: 50px;
            line-height: 100px;
            text-align: center;
            list-style: none;
            height: 100px;
            width: 100px;
            background-color:red ;
        }
```

justify-content:flex-end;   元素沿着主轴终边排列

justify-content:center;  元素居中排列 

justify-content:space-around; 空白分布到元素两侧（中间的距离比两边的距离大）

![](pic\3-20.png)

justify-content:space-between;   空白均匀分布到元素的中间

![](pic\3-21.png)

justify-content:space-evenly; 空白分布到元素的单侧（每一边的距离一样）

![](pic\3-22.png)

##### 7)align-items

元素在辅轴上如何对齐（元素间的关系）

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
.a{
	width:600px;
	height:500px;
	border:5px solid #f00;
	display:flex;
	align-items: flex-start;
	}
.a li{
	width:100px;
	list-style:none;
	}
.a li:nth-of-type(1){
	background-color:#09F
	}
.a li:nth-of-type(2){
	background-color:#F30;
	}
.a li:nth-of-type(3){
	background-color:#9C9;
	}
    </style>
</head>
<body>
    <ul class="a">
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
    
</body>
</html>
```

align-items:stretch

默认值,将元素的长度设置为相同的值)设置行与行的高度(每一行的高度是相同的) 并不是所有行的高度都是一样的

align-items:flex-start;(元素不会拉伸，沿着辅轴起边对齐)

align-items:flex-end;(元素不会拉伸，沿着辅轴终边对齐)

align-items:center;(元素不会拉伸，居中对齐)

align-items:baseline;元素不会拉伸,元素沿基线对齐。



##### 8)align-content

设置辅轴空白空间的分布

- align-content:center   上下的空白相等，元素在中间

- align-content:flex-start(元素靠上对齐，空白在下面)

- align-content:flex-end(元素靠下对齐，空白在上面)

- align-content:space-around；(用法同justify-content一样)

- align-content:space-between；(用法同justify-content一样)

- align-content:space-evenly;(用法同justify-content一样)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
.a{
	width:600px;
	height:500px;
	border:5px solid #f00;
    display: -webkit-flex;
    display: flex;
    -webkit-flex-wrap:wrap;
    flex-wrap: wrap;
    -webkit-align-content: center;
    align-content: center;
	}
.a li{
	width:100px;
	height:100px;
	list-style:none;
	}
.a li:nth-of-type(1){
	background-color:#09F
	}
.a li:nth-of-type(2){
	background-color:#F30;
	}
.a li:nth-of-type(3){
	background-color:#9C9;
	}
    </style>
</head>
<body>
    <ul class="a">
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
    
</body>
</html>
```

```
设置元素垂直水平居中:justify-content:center;(水平方向) align-items:center;(垂直方向)
```

```
弹性元素:弹性容器的子元素是弹性元素（弹性项）
一个元素可以同时是弹性元素和弹性容器
注意:弹性元素的直接子元素才是弹性元素（后代元素不是）
```

#### 2、弹性元素

##### 1)flex-grow

指定弹性元素的伸展的系数,当父元素有多余空间时，子元素如何伸展。父元素的剩余空间会按照比例进行分配

flex-grow:0，默认值 不占据剩余空间

flex-grow:1，平均分配剩余空间把盒子占满)值越大分配的空间越大



```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
.a{
	width:600px;
	height:500px;
	border:5px solid #f00;
    display: -webkit-flex;
    display: flex;
	}
.a li{
	width:100px;
	height:100px;
	list-style:none;
	flex-grow:0;  /*设置子元素的伸展属性*/
	}
.a li:nth-of-type(1){
	background-color:#09F
	}
.a li:nth-of-type(2){
	background-color:#F30;
	}
.a li:nth-of-type(3){
	background-color:#9C9;
	}
    </style>
</head>
<body>
    <ul class="a">
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
    
</body>
</html>
```

##### 2）flex-shrink

指定弹性元素的收缩系数，当父元素中的空间不足以容纳所有子元素时，如何对子元素进行收缩。

flex-shrink:1;(默认值 等比例收缩)

```
 .a{
            width: 200px;
            border: 10px solid red ;
            display: flex;
            /* flex-wrap: nowrap; */
        }
        .a li{
           flex-shrink: 1;
            font-size: 50px;
            line-height: 100px;
            text-align: center;
            list-style: none;
            height: 100px;
            width: 100px;
            background-color:red ;
        }
```

flex-shrink:0;不收缩，缩减多少是根据 缩减系数和元素大小来决定（元素越大缩减的越多）

##### 3）align-self

用来覆盖当前弹性元素上的align-items，单独为某一个元素设置align-items

```
.a :nth-of-type(1)
{
align-self: stretch;
background-color: yellow;
}
```

##### 4）flex-basis

设置元素在主轴上的基础长度，auto是默认值，表示参照元素自身的高度和宽度，如果传递了一个具体的数值，则以该值为准。
如果主轴是 横向 的 则 该值指定的就是元素的宽度
如果主轴是 纵向 的 则 该值指定的就是元素的高度

```
.a{
            width: 600px;
            border: 10px solid red ;
            display: flex;
            flex-flow: row wrap;
}
.a li{
            flex-basis: 50px;
            /* flex-grow: 1; */
            flex-shrink: 1;
            font-size: 50px;
            line-height: 100px;
            text-align: center;
            list-style: none;
            width: 100px;
            background-color:red ;
        }
```

##### 5）flex 可以设置弹性元素的三个样式（增长 缩减 基础）

flex:initial，默认值 相当于flex:0 1 auto;

flex:auto，相当于 flex:1 1 auto;

flex:none，相当于 flex:0 0 auto;

##### 6）order	

order:1，决定弹性元素的排列顺序 把元素排列到第一个。

### 三）网页响应式布局

#### 1、左侧固定，右侧宽度自适应

```
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>左侧固定，右侧宽度自适应</title>
<style>
	*{
		margin:0px;
		padding:0px;
		}
	.container{
		width:100%;
		height:600px;
		background:#F90;
		}
	.a1{
		width:200px;
		height:400px;
		float:left;
		background:#6C6;
		margin-left:-100%;
		}
		.a2{
		width:100%;
		height:400px;
		float:left;
		background:#F30;
		padding-left:200px;
		box-sizing:border-box;
		}
	.content{
		padding-left:200px;
		}
</style>

</head>

<body>
	<div class="container">
        <div class="a2">媒体查询语句也是CSS语句，使用它可以查询屏幕的宽度和高度，从而进行页面布局。实际上媒体查询语句就是一个判断语句。</div>
        <div class="a1">left</div>
    </div>
</body>
</html>

```

#### 2、双飞翼布局

```
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<style>
	*{
		margin:0px;
		padding:0px;
		}
	.container{
		width:100%;
		height:600px;
		background:#F90;
		}
	.a1{
		width:200px;
		height:400px;
		float:left;
		background:#6C6;
		margin-left:-100%;
		}
		.a2{
		width:100%;
		height:400px;
		float:left;
		background:#F30;
		padding-left:200px;
		padding-right:200px;
		box-sizing:border-box;
		}
	.content{
		padding-left:200px;
		}
	.a3{
		width:200px;
		height:400px;
		float:left;
		background:#ff0;
		margin-left:-200px;
		}
</style>

</head>

<body>
	<div class="container">
        <div class="a2">媒体查询语句也是CSS语句</div>
        <div class="a1">left</div>
         <div class="a3">right</div>
    </div>
</body>
</html>

```

#### 3、圣杯布局

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<style>
	*{
		margin:0px;
		padding:0px;
		}
	.container{
		min-width:600px;/*盒子的最小宽度，此例中大于等该宽度值时，盒子区域小于最小值时，盒子保持最小值的宽度*/
		/*max-width,最大宽度，min-height最小高度，max-height最大高度*/
		height:600px;
		background:#F90;
		margin:0px 200px;
		}
	.a1{
		width:200px;
		height:400px;
		float:left;
		background:#6C6;
		margin-left:-100%;
		position:relative;
		left:-200px;
		}
		.a2{
		width:100%;
		height:400px;
		float:left;
		background:#F30;
		}

	.a3{
		width:200px;
		height:400px;
		float:left;
		background:#ff0;
		margin-left:-200px;
		position:relative;
		right:-200px;
		}
</style>

</head>

<body>
	<div class="container">
        <div class="a2">媒体查询语句也是CSS语句，使用它可以查询屏幕的宽度和高度</div>
        <div class="a1">left</div>
         <div class="a3">right</div>
    </div>
</body>
</html>
```



### 四）媒体查询

媒体查询语句也是CSS语句，使用它可以查询屏幕的宽度和高度，从而进行页面布局。实际上媒体查询语句就是一个判断语句。

```
@media(min-width/max-width/min-heihgt/max-height:值){
样式表
}

@media (min-width:值) and (max-width:值) {
				/* 一行两列 */
				.box ul li{
					width: 50%;
					margin-bottom: 10px;
				}
			}
```

如：

```
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<style>
	.box{
		width:200px;
		height:200px;
		background:#f00;
		}
	@media (max-width:600px){
		.box{
			width:400px;
			height:400px;
			background:#ff0;
			}
		}
</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
```



## 十、动画

### 一）2D 转换

#### 1、位移

transform:translate(x,y)  元素沿X，Y轴位置发生位移

transform:translateX(value)  元素沿X轴位置发生位移

transform:translateY(value)  元素沿Y轴位置发生位移

#### 2、旋转角度

transform:rotate(角度) 

```
<!DOCTYPE html>
<html>
<head>
<title>无标题文档</title>
<style>
.d2{
	width:200px;
	height:200px;
	background:#F60;
	transform:rotate(-30deg);
	border-top-left-radius:100px;
	border:1px solid #ccc;
	margin:100px;
	}
</style>
</head>
<body>
	<div class="d2"></div>
</body>
</html>

```

#### 3、缩放

transform:scale(水平缩放比例，垂直缩放比例) 

```
<!DOCTYPE html>
<html>
<head>
<title>无标题文档</title>
<style>
.d2{
	width:200px;
	height:200px;
	background:#F60;
	transform:scale(0.5,2);
	border-top-left-radius:100px;
	border:1px solid #ccc;
	margin:100px;
	}
</style>
</head>
<body>
	<div class="d2"></div>
</body>
</html>
```

#### scaleX() 方法

#### scaleY() 方法

#### 4、倾斜

skew(xdeg,ydeg) 沿着X轴和Y的方向进行倾斜。

skewX(xdeg) 沿着X轴方向进行倾斜。

skewY(xdeg) 沿着Y轴的方向进行倾斜。

```
<!DOCTYPE html>
<html>
<head>
<title>无标题文档</title>
<style>
.d2{
	width:200px;
	height:200px;
	background:#F60;
  transform: skew(20deg, 10deg);
	border:1px solid #ccc;
	margin:200px;
	}
</style>
</head>
<body>
	<div class="d2"></div>
</body>
</html>
```

#### 5、maxtrix方法

matrix(scaleX(),skewY(),skewX(),scaleY(),translateX(),translateY())

#### 6、transform-origin设置旋转的轴心位置

```
<!DOCTYPE html>
<html>
<head>
<title>无标题文档</title>
<style>
*{padding:0px;margin:0px;}
.d2{
	width:200px;
	height:200px;
	background:#F60;
  	transform:rotate(60deg);
	transform-origin:100% 0%;/*设置旋转中心的坐标，默认是盒子的正中心*/
	margin:200px;
	}
.d3{
	width:200px;
	height:200px;
	background:#ff0;
	position:absolute;
	top:200px;
	left:200px;
	}
</style>
</head>
<body>
	<div class="d2">无标题文档无标题文档无标题文档无标题文档无标题文档无标题文档无标题文档</div>
	<div class="d3">无标题文档无标题文档无标题文档无标题文档无标题文档无标题文档无标题文档</div>
</body>
</html>
```

### 二）3D转换

#### 1、rotateX()

方法使元素绕其 X 轴旋转给定角度

#### 2、rotateY() 方法

使元素绕其 Y 轴旋转给定角度

#### 3、rotateZ() 方法

使元素绕其 Z 轴旋转给定角度

![](pic\3-23.png)

### 三）CSS 过渡

#### 1、transition: 样式属性1 时间1,样式属性2 时间2;

```
<!DOCTYPE html>
<html>
<head>
<style> 
div {
  width: 100px;
  height: 100px;
  background: red;
  transition: width 2s,background 2s;
}

div:hover {
  width: 300px;
  background:#ff0;
}
</style>
</head>
<body>
<h1>transition 属性</h1>
<p>请把鼠标悬停在下面的 div 元素上，来查看过渡效果：</p>
<div></div>
<p><b>注释：</b>本例在 Internet Explorer 9 和更早版本中不起作用。</p>

</body>
</html>

```

#### 2、指定过渡的速度曲线

transition-timing-function

- `ease` - 规定过渡效果，先缓慢地开始，然后加速，然后缓慢地结束（默认）
- `linear` - 规定从开始到结束具有相同速度的过渡效果
- `ease-in` -规定缓慢开始的过渡效果
- `ease-out` - 规定缓慢结束的过渡效果
- `ease-in-out` - 规定开始和结束较慢的过渡效果
- `cubic-bezier(n,n,n,n)` - 允许您在三次贝塞尔函数中定义自己的值

#### 3、延迟过渡效果

`transition-delay` 属性规定过渡效果的延迟（以秒计）

#### 4、过渡 + 转换

```
<!DOCTYPE html>
<html>
<head>
<style> 
div {
  width: 100px;
  height: 100px;
  background: red;
  transition: width 2s, height 2s, transform 2s;
}
div:hover {
  width: 300px;
  height: 300px;
  transform: rotate(180deg);
}
</style>
</head>
<body>
<h1>Transition + Transform</h1>
<p>请把鼠标悬停在下面的 div 元素上：</p>
<div></div>
<p><b>注释：</b>本例在 Internet Explorer 9 和更早版本中不起作用。</p>
</body>
</html>

```

### 四）动画

参见：

https://www.w3school.com.cn/cssref/pr_animation.asp