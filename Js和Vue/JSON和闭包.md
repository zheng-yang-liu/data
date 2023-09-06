# json



是一种轻量级的数据交换格式，是基于ECMAScript的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。

## json值的类型

**数字、字符串、逻辑值、数组、对象、null**

## json语法

key/value

数据在名称/值对中

数据由逗号隔开

大括号保存对象

中括号保存数组



字符串转换为json数据

```
JSON.parse(str)

var k='{"name":"liuzhengyang"}'
var ToJson = JSON.parse(k)
```

JSON转字符串

```
JSON.stringify(str)

var k={name:'liuzhengyang'}
var ToString= JSON.stringify(k)
```



# 闭包

## **局部变量和全局变量的区别**

声明位置不同

作用域不同

生存周期不同

## **隐式全局变量的全局变量**

没有使用var声明的变量称为隐式全局变量

全局变量不能被删除，隐式全局变量可以被删除

## **闭包概念**

定义在函数内部的函数

能读取其他函数内部变量的函数

可以将函数内部和函数外部连接起来

## **用途**

可以读取函数内部变量

让这些变量的值始终保持在内存中

## **缺点**

内存占用大、可能会导致内存泄漏

会在父函数外部改变父函数内部变量的值

## 使用闭包编写点赞

```
var but1 = document.getElementById("but1");

function Fn() {
  var n = 0;
  function m() {
    n++;
    return n;
  }
  return m;
}
var fn1 = Fn();
but1.onclick = function () {
  but1.innerHTML = "点击了" + fn1() + "次";
};
```

























## 使用闭包编写点赞

```
var btn = document.getElementById("but1")

function Fn(){
	var num =0
	function add(){
		num++
		return num
	}
	return add
}

var but1 = Fn()
but
```











