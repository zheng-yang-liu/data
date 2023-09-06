**api**

应用程序接口

# vue简介

vue是**构建web界面**的**javascript**库**，通过简单的api提供高效的数据绑定和灵活的**组件系统主要关注视图层，方便现有的效果和第三方库整合。



Vue.js 的核心是一个允许你采用**简洁的HTML模板语法来声明式的将数据渲染进 DOM 的系统。**



# Vue的安装方法  

**使用本地Vue库文件**

```
<script src="路径"></script>
```

**使用网络CDN资源**

```
<script src="连接"></script>
```

**使用NPM安装**



# 实例化Vue

```
var vm = new Vue({
	//小括号里面套大括号
	//其他选型
})
```





# 模板语法

## 基本格式

```
<div id="app"></div>

new Vue({
	el:"#app",
	data:{
		
	}
})
```



## 1、插入文本  插值表达式

```
{{变量名}}
```

# 2、html

使用v-html添加页面dom元素

```
<div v-html="htmlTag"></div>
```

# 3、属性

**v-bind:属性=“值”**

```
绑定class
<div v-bind:class="{'classs1':true}"></div>
<div v-bind:style="style"></div>

new Vue({
	el:'#app',
	data:{
		style:'color:red'
	}
})
```

**v-model**---双向绑定数据

**v-model:属性名="属性值"**

```
//单选按钮
< input type="chackbox" v-model="value">


new Vue({
	el:'#app',
	data:{
		value:false
	}
})
```







vu是构建web界面的javascript库，可以通过简单的api提供高效的数据绑定和灵活的组件的系统，主要关注视图层，方便将现有效果和第三方库进行整合



vue的核心是，可以使用简单的html语法模板来**声明式的**将数据渲染进dom的系统











