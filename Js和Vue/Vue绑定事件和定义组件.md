# 事件处理器

**事件修饰符**

```
.stop - 阻止冒泡  
.prevent - 阻止默认事件
.capture - 阻止捕获
.self - 只监听触发该元素的事件
.once - 只触发一次
.left - 左键事件
.right - 右键事件
.middle - 中间滚轮事件
```

**按键修饰符**

```
@keydown

@keyup
```



```
全部的按键别名：
.enter  -
.tab
.delete (捕获 "删除" 和 "退格" 键)
.esc
.space  - 空格
.up
.down
.left
.right
.ctrl
.alt
.shift
.meta
```

# 表单

**数据绑定   v-model**

文本框   -input  textarea

复选框   -type="checkbox"

```
<input type="checkbox" id="runoob" value="abc.com" v-model="checkedNames">
<label for="runoob">Runoob</label>
```

单选    - type="radio"

列表     - select

```
<select v-model="selected" name="website">
    <option value="">选择一个网站</option>
    <option value="www.abc.com">ABC</option>
    <option value="www.google.com">Google</option>
</select>
```



**修饰符**

```

lazy    --- 改变input  绑定的数据为在change事件中同步

.number

.trim

```

# 组件

## 概念

 **----自定义标签**



## 组件使用的步骤

注册组件

```
Vue.component('组件名',{配置项})
new Vue({
	el:"#app",
	components:{}
})
```

使用组件

```
<组件名></组件名>       ---不指出驼峰命名
```

## 全局组件

```
Vue.component('组件名称', { })//第1个参数是标签名称，第2个参数是一个选项对象。全局组件注册后，任何vue实例都可以用。
```

data是以匿名函数的形式编写有返回值且返回值为一个对象，在vue中尽量少使用箭头函数

```
Vue.component('abc', {
  data:function(){
	return {
		count:0
		}
	},
  template: '<h1 v-on:click=count++>{{count}}</h1>'
})
```

## 局部组件

在实例选项中注册局部组件，注册的组件只能在这个实例中使用。

```
var child = {
	配置项
	template:''
}

new Vue ({
	el:"#app",
	components:{
		组件名：child
	}
})
```

全局组件和局部组件的区别

```
1、使用范围不同，

	全局组件可以在页面中任何位置使用，局部组件只能在定义它的el中使用，不能在其他位置使用。
2、定义组件的方法不同

	全局组件可以使用“Vue.component(tagName,options)”定义，局部组件可以通过Vue实例中components属性定义。
```

## 自定义属性  ---- 传递数据

```
prop 是为组件传递的数据的一个自定义属性。父组件的数据需要通过 props 把数据传给子组件，子组件需要显式地用 props 选项声明 "prop"：prop
```

```
<child message="hello!"></child>

Vue.component('child', {
  // 声明 props
  props: ['message'],
  // 同样也可以在 vm 实例中像 “this.message” 这样使用
  template: '<span>{{ message }}</span>'
})
new Vue({
  el: '#app'
})
```

动态props   --使用v-bind传递可变数据

```
<child v-bind:message="parentMsg"></child>
// 注册
Vue.component('child', {
  // 声明 props
  props: ['message'],
  // 同样也可以在 vm 实例中像 “this.message” 这样使用
  template: '<span>{{ message }}</span>'
})

// 创建根实例
new Vue({
  el: '#app',
  data: {
	parentMsg: '父组件内容'
  }
})
```

