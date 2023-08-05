

# 第六章 DOM操作

## 一、DOM基础

### 一）DOM构成

- core DOM  核心DOM，适用所有标签类文档操作。
- HTML DOM, HTML 文档的标准模型
- XML DOM,XML (可扩展标记语言）文档的标准模型

### 二）DOM树

#### 1、dom树中的节点类型

- 文档节点(node)
- 根节点（root)
- 元素节点（element)
- 文本节点（text）
- 属性节点（attribute)
- 注释comments节点

#### 2、节点之间关系

- 父子关系（parent-child)
- 邻居关系（兄弟关系,sibling)

### 三）通过节点属性访问节点

| **属性名称**    | 描述                                                       |
| --------------- | ---------------------------------------------------------- |
| parentNode      | 返回节点的父节点                                           |
| childNodes      | 返回子节点集合，childNodes[i]                              |
| firstChild      | 返回节点的第一个子节点，最普遍的用法是访问该元素的文本节点 |
| lastChild       | 返回节点的最后一个子节点                                   |
| nextSibling     | 下一个节点                                                 |
| previousSibling | 上一个节点                                                 |

| **属性名称**           | 描述                     |
| ---------------------- | ------------------------ |
| firstElementChild      | 返回节点的第一个子节点   |
| lastElementChild       | 返回节点的最后一个子节点 |
| nextElementSibling     | 下一个节点               |
| previousElementSibling | 上一个节点               |

```
<section id="a1"><h1 id="no1">第一章</h1><p>第一段内容</p></section><body></html>
<script>
	//var h1=document.getElementById('no1');
	//alert(h1.parentNode.innerHTML); //获取当前节点的父节点
	//alert(document.getElementById('a1').childNodes.length);//获取父节点下的所有子节点，得到的结果是一个数组
	//document.getElementById('a1').childNodes[0].innerHTML="第八章";//childNodes[索引]访问某个子节点
	//document.getElementById('a1').firstChild.innerHTML="第八章";//访问第一个子节点
	//document.getElementById('a1').lastChild.innerHTML="最后一段落";//访问最后一个子节点
	document.getElementById('a1').childNodes[0].nextSibling.innerHTML="aaaaaaa";//nextSibling获取同一级节点的下一个节点
	document.getElementById('a1').childNodes[1].previousSibling.innerHTML="kkkkkkkkk";
</script>//previousSibling获取同一级节点的上一个节点
alert(document.getElementById('a1').firstElementChild.innerHTML) //第一个子元素节点
//alert(document.getElementById('a1').lastElementChild.innerHTML);//最后一个子元素节点
//alert(document.getElementById('no1').nextElementSibling.innerHTML);//下一个元素节点
alert(document.getElementsByTagName('p')[0].previousElementSibling.innerHTML);上一个元素节点
```

### 四）节点组成

nodeName：节点名称

nodeValue：节点值

nodeType：节点类型

| 节点                 | 节点名称（nodeName） | 节点类型（nodeType） | 节点值（nodeValue） |
| -------------------- | -------------------- | -------------------- | ------------------- |
| 文档节点(node)       | #document            | 9                    | null                |
| 元素节点（element)   | 标签名               | 1                    |                     |
| 文本节点（text）     | #text                | 3                    | 文本内容            |
| 属性节点（attribute) | 属性名               | 2                    | 属性值              |
| 注释comments节点     | #comments            | 8                    |                     |
| 根节点（root)        |                      |                      |                     |

## 二、操作节点属性

### 一）设置属性

setAttribute()方法添加指定的属性，并为其赋指定的值。

```
对象.setAttribute(属性名,属性值)
```

### 二）获取属性值

getAttribute()方法返回指定属性名的属性值

```
对象.getAttribute(属性名)
```

### 三）删除属性

removeAttribute()方法删除指定的属性

```
对象.removeAttribute(属性名)
```



```
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>Core DOM操作属性</title>
</head>
<body>
<h1>这是一个大标题</h1>
<button onclick="f()">居中对齐</button><button onclick="d()">右对齐</button><button onclick="m()">删除属性值</button><button onclick="g()">获取属性</button><button onclick="del()">删除属性</button>
<script>
function f(){
	document.getElementsByTagName('h1')[0].setAttribute('align','center');
}
function d(){
	document.getElementsByTagName('h1')[0].setAttribute('align','right');
}
function m(){
	document.getElementsByTagName('h1')[0].setAttribute('align','');
}
function g(){
	alert(document.getElementsByTagName('h1')[0].getAttribute('align'));
}
function del(){
	document.getElementsByTagName('h1')[0].removeAttribute('align');
}
</script>
</body>
</html>

```



