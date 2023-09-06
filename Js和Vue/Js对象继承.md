# **原型链继承**

**子对象.prototype = new 父对象构造函数()**



**原型链继承 prototype**

```
子对象.prototype= 父对象.prototype

子对象.prototype.constructor = 子对象
```



**利用空对象作为中介**

```
var F=function(){}

F.prototype=father.prototype

child.prototype=new F()

child.prototype.constructor=child
```

**函数封装继承**

```
function ex(Child,Parent){
	var F=function()
	F.prototype=Parent.prototype
	Child.prototype = new F()
	child.prototypt.constructor= Child
}
```

# 构造函数继承

**call()**和**apply()**

通过call()方法把父类的this指向子类的this

```
Parent.call(this,属性)

Parent.apply(this,属性)（属性为数组形式）
```

**组合继承**

# 拷贝继承

把父对像的所有属性和方法，拷贝进子对象，将父对象的原型对象（prototyper指向的对象）的属性，一一拷贝给子对象的原型对象（即子对象的prototype指向的对象）。

```
function ex(Child,Parent){
	var p=Parent.prototype
	var c=Child.prototype
	for(var i in p){
		c[i]=p[i]
	}
}
```





# Cookie

**用途**

会话状态管理

个性化设置

浏览器行为追踪

**特性**

同一个网站所有页面共享一套Cookie

数量大小有限

有过期时间o

**创建Cookie**

```
document.cookie="名字=值"



expires="时间"
```

**删除Cookie**

```
expires=时间
```

## **封装Cookie**

创建Cookie

```
setCookie(name,value,iDay){
	
}
```

获取Cookie

```
里面需要把cookie做一下字符串分割，分割后变为数组，再去循环数组，就可以得到cookie

name(想要得到=cookie)
getCookie(name){
	分割字符串来获取元素
}
```

删除Cookie

```
把时间设置为负1，即可代表时间已过期

removeCookie(name){
	setCookit(name,1,-1)
}
```



# Ajax

创建Ajax

```
if(window.XMLHttpRequest){
	//非IE6
	var oAjax =new XMLHttpRequest()
}else{
	//老版本 
	var oAjax = new ActiveObject("Microsoft.XMLHTTP")
}
```

链接服务器

```
oAjax.open("方法","文件名",同步异步)

同步false
异步true
```

同步：发送一个请求，需要等待返回然后才能进行下一个请求，需要等待

异步：发送一个请求，不需要等待返回随时能进行下一个请求，不需要等待

发送请求

```
oAjax.send()
```

接受返回值

```
oAjax.onreadystatechange=function(){
	if(oAjax.readyState == 4 && oAjax.stetus==200){
		alter("请求成功"+oAjax.responseTex)
	}else{
    
    }
}
```

