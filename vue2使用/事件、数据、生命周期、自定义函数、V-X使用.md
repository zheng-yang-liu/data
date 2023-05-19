## 事件、数据、生命周期函数、自定义函数、v-X使用

## 事件

### 点击事件

```
click
<div @click="函数名">点击我</div>
```

### 值改变事件(常用于表单选择框)

```
onchange
@onchange="函数名"
<form name="f">
    用户名：<input type="text" name="username">
    <select name="gushi" id="" onchange="ah();" >
        <option value="唱歌">唱歌</option>
        <option value="跳舞">跳舞</option>
        <option value="游戏">游戏</option>
        <option value="其他">其他</option>
    </select>
</form>
```

鼠标按下事件

```
mousedown
@mousedown="函数名"
```

鼠标抬起事件

```
mouseup
@mouseup="函数名"
```



### 数据定义和使用

数据的定义

```
data(){
	return{
		数据名:值
	}
}
```

数据的使用

```
<div>{{数据名}}</div>
```

### 生命周期函数

```
在页面加载的时候执行代码
mounted(){

},
created(){

}
```

### 自定义函数

```
methods(){
	函数名(){
		函数体
	}
}
```

### v-X使用

**v-mode**l双向动态数据绑定，多用于网页输入数据的绑定

```
<div v-model="数据"></div>
```

**v-bind**单向动态数据绑定，多用于标签属性的动态绑定

```
主要用于属性绑定，比如class属性，style属性，value属性，href属性等等，只要是属性，就可以用v-bind指令进行绑定。
v-bind:有一个对应的语法糖，也就是简写方式 :属性名
```

动态绑定样式

```
 .inner{
 	color:red,
 	font-size:20px
 }
 <div :class="inner">我是inner</div>
```

**v-if/ v-else**条件选择，用于同类型元素不同条件触发

```
<div v-for="index in 5">
	<div v-if="index>3">当index大于3时输出这个div</div>
	<div v-else>当index小于等于3时输出这个div</div>
</div>

```

**v-on**绑定事件

```
v-on使用方法
	v-on:事件名="函数"
简写（常用点击事件click）
	@事件名="函数"
```

**v-text**插入文本

```
<div v-text="文本内容或者定义的数据"></div>

使用v-text可以将html文本转换成可识别的标签
<div v-text="msg"></div>
data(){
	return{
		msg:'<h2>这是经过转化后的h2标签</h2>'
	}
}
```

