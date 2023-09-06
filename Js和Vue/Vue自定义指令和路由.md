# Vue 自定义指令

```
Vue,directive('指令名',{})   或者
Vue,directive('指令名',function(){}) 
```

```
var app = new Vue({
	el:"#app",
	data:{},
	directives:{
		指令名:{
			
		}
	}
})
```

## 自定义指令中的钩子函数

`bind` 在指令插入书调用

`inserted`元素插入到DOM树时调用

`update` 数据更新时调用

`componentUpdated`  完成一个跟新周期时调用 标签发生改变

`unbind`  指令销毁时调用

## 钩子函数中的参数

el   

​	当前指令绑定的元素

binding

​	`name` 指令名不包含v-

​	`value` 指令的绑定值 只取最后结果

​	`oldValue` 指令绑定的前一个值，只在update 和 componentUpdate 中可用	

​	`expression` 指令绑定的表达式

​	`arg`  传给指令的参数例如 `v-bind:class`  中的class就是参数

​	`modifiers` 获取指令的修饰符，结果为一个对象

```
例如： v-my-directive.foo.bar, 修饰符对象 modifiers 的值是 { foo: true, bar: true }。
```

​	`vnode` Vue编译生成的虚拟节点 

​	`oldVnode` 上一个虚拟节点 可用钩子同 `oldValue` 



# 路由

## 路由连接

```
<router-link to="路径"><router-link>
```

## 路由入口

```
<router-view><router-view>
```

## 定义路由组件

```
const first = {template:'<div>first</div>'}
```

## 定义路由规则

```
const routes = [
	{path:'地址',component:组件名}
	{path:'/first,component:first}
]
```

## 创建路由实例

```
var router = new VueRouter({
	routes//路由规则，可以在外也可以在内
})
```

## 挂载路由

```
var app = new Vue({
	el:'#app',
	data:{},
	router
})
```

## 路由连接修饰符

`replace` 导航后不会留下记录

`append` 在当前路径添加要跳转的路径

`tag` 连接渲染转换后的标签

`active-class` 选中激活后链继的样式 --class的名为 ` active-class="_active`

`exact-active-class` 连接被精确匹配时使用的样式

```
exact-active-class 和 active-class 的区别

router-link 默认情况下的路由是模糊匹配，例如当前路径是 /article/1 那么也会激活 ，所以当设置 exact-active-class 以后，这个 router-link 只有在当前路由被全包含匹配时才会被激活 exact-active-class 中的 class
```

`event` 连接激活的方式

```
鼠标悬浮激活连接
<router-link to="/NEW"  event="mouseover">资讯</router-link>
```



