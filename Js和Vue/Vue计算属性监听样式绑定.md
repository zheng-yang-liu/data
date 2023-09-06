# 计算属性--computed

**computed**

```
语法  --computed:{}//在模板中调用时直接写出属性即可
```

**computed 和methods的区别**

````
computed是带缓存的需要数据发生改变才会重新进行计算，否则直接返回之前的计算结果。
methods里的函数在每次调用的时候都执行

```
computed在数据改变的时候执行
methods在函数调用的时候执行
```

调用的方式不同
computed的调用和属性一样
methods的调用使用函数的调用方法  

computed可以只定义一个函数作为属性，也可以定义get/set变成可读写的属性methods则不能
````

```
<html>
	<head>
    	<script></script>
	</head>
    <body>
    	<script></script>
    </body>
</html>
```



```
vm.site = 'abc软件 http://www.abc.com';


{{reversedMessage}}

<p>{{asd()}}</p>

 methods:{
  	asd:function(){
  	
  		return "hello"
  	}
  	
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
  
  
  
  
  可读写属性
  computed: {
    site: {
      // getter
      get: function () {
        return this.name + ' ' + this.url
      },
      // setter
      set: function (newValue) {
        var names = newValue.split(' ')
        this.name = names[0]
        this.url = names[names.length - 1]
      }
    }
  }
```



# 监听watch

监听就是对内置对象的状态或者属性变化进行监听并且做出反应的响应，监听属性，意思就是可以监视其他数据的变化。

**使用方法**

1、使用watch配置项，在配置项里面写上要监视的属性

每次属性值的变化都会触发handler函数回调，也可以监视计算属性的变化。

2、可以使用实例对象的$watch方法在外部监听属性的变化。

监听属性(数据)的变化

```
在Vue内
watch:{
	属性名:function(newValue,OldValue){}
}
在Vue外
Vue对象名.$watch("属性名",function(newValue,oldValue){})
```



# watch和computed的区别

```
总结：计算属性与侦听属性的区别：
(1)功能不同，计算属性用于解决模板冗余问题。侦听器侦听data中某一个数据变化

(2)计算属性具有缓存机制，侦听器没有缓存机制

(3)计算属性不支持异步操作，侦听器支持异步操作

(4)计算属性可以给vue新增属性，侦听器是 data中已有属性

(5)计算属性只要使用了就会执行一次，侦听器默认只有第一次改变才会执行
```



# 样式绑定

**v-bind:class**

## 设置一个对象动态切换样式

```
v-bind:class="{'样式名',属性名}"

通过属性的true和false来改变样式的使用的和禁用
new Vue({
  el: '#app',
  data: {
    属性名: true
  }
})

可以使用多个属性来叠加多个样式
<div v-bind:class="{ 'active': isActive, 'text-danger': hasError }">
```

## 直接绑定一个对象

```
v-bind:class="对象名"

new Vue({
  el: '#app',
  data: {
    classObject: {
      active: true,
      'text-danger': true//存在-需要使用单引号引起来
    }
  }
})
```

## 绑定返回对象的计算属性

```
<div v-bind:class="classObject"></div>

new Vue({
  el: '#app',
  data: {
    isActive: true,
    error: {
      value: true,
      type: 'fatal'
    }
  },
  computed: {
    classObject: function () {
      return {
  		base: true,
        active: this.isActive && !this.error.value,
        'text-danger': this.error.value && this.error.type === 'fatal',
      }
    }
  }
})
```

## 数组绑定样式

```
v-bind:class=[属性名]
在数据中，属性对应的值是样式表的名。

<div v-bind:class="[activeClass, errorClass]"></div>
new Vue({
  el: '#app',
  data: {
    activeClass: 'active',
    errorClass: 'text-danger'
  }
})
```

## 使用三元表达式来切换列表中的样式

```
<div v-bind:class="[errorClass ,isActive ? activeClass : '']">

new Vue({
  el: '#app',
  data: {
    isActive: true,
	activeClass: 'active',
    errorClass: 'text-danger'
  }
})
```

# style--内联样式

**1、在 v-bind:style 直接设置样式**

```
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">直接设置样式</div>

new Vue({
  el: '#app',
  data: {
    activeColor: 'green',
	fontSize: 30
  }
})
```

**2、直接绑定样式对象**

```
v-bind:style="对象名"


new Vue({
  el: '#app',
  data: {
    对象名: {
      color: 'green',
      fontSize: '30px'
    }
  }
```

**3、使用数组绑定多个样式**

```
 <div v-bind:style="[baseStyles, overridingStyles]">style绑定</div>
 
 
 new Vue({
  el: '#app',
  data: {
    baseStyles: {
      color: 'green',
      fontSize: '30px'
    },
	overridingStyles: {
      'font-weight': 'bold'
    }
  }
})
```

