

# 第一章 VUE基础

## 一、关于VUE

### 一）简介

VUE是构建web界面的javascript库，是一套可以通过简单的API提供高效的数据绑定和灵活的组件的系统。它主要关注视图层，方便与即有的效果和第三方库整合。

官网：https://cn.vue.org

VUE不支持IE8及以下版本。

### 二）VUE安装

#### 1、使用本地VUE库文件

下载VUE，然后面网页上使用（下载地址：https://v2.vuejs.org/js/vue.min.js）

```
< script src="js/vue.js">< /script>
```

#### 2、使用网络CDN(内容分发网络 )资源

以下推荐国外比较稳定的两个 CDN，国内还没发现哪一家比较好，目前还是建议下载到本地。

- **Staticfile CDN（国内）** : https://cdn.staticfile.org/vue/2.2.2/vue.min.js
- **unpkg**：https://unpkg.com/vue@2.6.14/dist/vue.min.js。
- **cdnjs** : https://cdnjs.cloudflare.com/ajax/libs/vue/2.1.8/vue.min.js

```
< script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js">< /script>
```

### 3、使用NPM安装（略）

### 三）初视VUE

使用VUE编写"Hello VUE"程序

#### 实例化 Vue

```
var vm = new Vue({
  el:选择器,
  data:{}
})
el:指定数据渲染的范围。
data:数据源，定义对象的属性。
```

示例：

```
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>Hello VUE</title>
<script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>
</head>
<body>
    <h1 id="title">{{text}}</h1>
<script type="text/javascript">
    var vm = new Vue({
        el: '#title',
        data: {
           text:"hello World!"
        }
    })
</script>
</body>
</html>
```

代码分析：**{{ }}** 用于输出对象属性和函数返回值。在 Vue 构造器中有一个el 参数，它是 DOM 元素中的 id（title）。**data** 用于定义属性。

## 二、VUE模板语法

Vue.js 的核心是一个允许你采用简洁的HTML模板语法来声明式的将数据渲染进 DOM 的系统。

### 一）插值

插值，即向网页中插入数据。

#### 1、插入文本

使用 {{...}}（双大括号）的向网页中插入文本值。参见实例"hello vue".不支持插入HTML代码。

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue插入文本</title>
<script src="https://cdn.staticfile.org/vue/2.7.0/vue.min.js"></script>
</head>
<body>
<div id="app">
  <p>{{ message }}</p>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  }
})
</script>
</body>
</html>
```

#### 2、Html

使用v-html指令输出 html 代码。

```
<div id="app">
    <div v-html="message"></div>
</div>
    
<script>
new Vue({
  el: '#app',
  data: {
    message: '<h1>一级标题</h1>'
  }
})
</script>
```

#### 3、属性

HTML 属性中的值应使用 v-bind 指令。

下面实例判断 use 的值，如果为 true 使用 class1 类的样式，否则不使用该类：

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>HTML 属性</title>
<style>
.class1{
  background: #444;
  color: #eee;
}
</style>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  <label for="r1">修改颜色</label><input type="checkbox" v-model="use" id="r1">
  <br><br>
  <div v-bind:class="{'class1':use}">
    v-bind:class 指令{{use}}
  </div>
</div>
    
<script>
new Vue({
    el: '#app',
  data:{
      use: false
  }
});
</script>
</body>

</html>
```

v-bind:v-bind属性绑定(简写`:`),是单向的,他会将data中的数据投影到绑定的地方,在被绑定的地方对数据修改时,data中的原始数据是不会改变的。

默认的语法格式：v-bind:属性名="属性值",属性值为data中相关的键名。

v-model：绑定是双向的,不仅将data中的数据对标签内进行绑定,还会将标签中的数据反向绑定到data中,标签数据改变后data中的数据也会同步改变。

默认的语法格式：v-model:属性名="属性值"

```
<!DOCTYPE html>
<html lang="zh_CN">
<head>
    <meta charset="UTF-8">
    <title>dome6</title>
</head>

<body>
    <div id="dome">
        <!-- 属性绑定 -->
        <input type="text" v-bind:value="bind"><br>
        v-bind的简写:<input type="text" :value="bind">
        <p>{{bind}}</p>
        <!-- 双向绑定 -->
        <input type="text" v-model:value="model"><br>
        v-model的简写:<input type="text" v-model="model">
        <p>{{model}}</p>
        <!-- 事件绑定 -->
        <button v-on:click="von">我被点了{{on}}次</button>
        <button @click="von">简写版被点了{{on}}次</button>
    </div>    
</body>

<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script><script>
    new Vue({
        el: "#dome",
        data: {
            bind : '我是属性绑定',
            model : '我是双向绑定', 
            on : 0
        },
        methods: {
            von(){
                this.on += 1
            }
        }
    })
</script>
</html>
```

#### 4、表达式

Vue.js 都提供了完全的 JavaScript 表达式支持。

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例-表达式</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
	{{5+5}}<br>{{z}}
	{{ ok ? 'YES' : 'NO' }}<br>
	{{ message.split('').reverse().join('') }}
	<div v-bind:id="'list-' + id">表达式测试</div>
</div>
<script>
new Vue({
  el: '#app',
  data: {
	ok: true,
    message: 'VUE Test',
	id : 1,
	z:36+2
  }
})
</script>
</body>
</html>
```

#### 5、指令

指令是带有 v- 前缀的特殊属性。指令用于在表达式的值改变时，将某些行为应用到 DOM 上。下例中的v-if 指令将根据表达式 seen 的值(true 或 false )来决定是否插入 p 元素。

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 -指令</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
    <p v-if="seen">现在你看到我了</p>
    <template v-if="ok">
      <h1>VUE教程</h1>
      <p>学的不仅是技术，更是梦想！</p>
      <p>哈哈哈，打字辛苦啊！！！</p>
    </template>
</div>
    
<script>
new Vue({
  el: '#app',
  data: {
    seen: true,
    ok: true
  }
})
</script>
</body>
</html>
```

#### 6、参数

参数在指令后以冒号指明。例如， v-bind 指令被用来响应地更新 HTML 属性：

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 -参数</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
    <pre><a v-bind:href="url">测试实例 -参数</a></pre>
</div>
	
<script>
new Vue({
  el: '#app',
  data: {
    url: 'http://www.abc.com'
  }
})
</script>
</body>
</html>
```

在这里 href 是参数，告知 v-bind 指令将该元素的 href 属性与表达式 url 的值绑定。

#### 7、修饰符

修饰符是以半角句号 **.** 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，**.prevent** 修饰符告诉 **v-on** 指令对于触发的事件调用 **event.preventDefault()**：

```
<form v-on:submit.prevent="onSubmit"></form>
```

```
<div id="app">
<form v-on:submit.prevent="onSubmit" action="b.html">
	<input type="text" name="useranme"  />
	<input type="submit" value="提交" />
	<div>{{hint}}</div>
</form>
</div>
<script>
	new Vue({
	el:"#app",
	data:{
	hint:''
},
	methods:{
		onSubmit:function(){
			this.hint="您的数据不合法!"
		}
	}
});
</script>
```



#### 8、用户输入

在 input 输入框中我们可以使用 v-model 指令来实现双向数据绑定：

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 双向数据绑定</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
    <p>{{ message }}</p>
    <input type="text"v-model:value="message">
</div>
	
<script>
new Vue({
  el: '#app',
  data: {
    message: 'Hello!'
  }
})
</script>
</body>
</html>
```

**v-model** 指令用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。

按钮的事件我们可以使用 v-on 监听事件，并对用户的输入进行响应。

以下实例在用户点击按钮后对字符串进行反转操作：

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 -VUE用户输入</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">反转字符串</button>
</div>
	
<script>
new Vue({
  el: '#app',
  data: {
    message: 'Hello World!'
  },
  methods: {//方法
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
</body>
</html>
```

#### 9、过滤器

Vue.js 允许你自定义过滤器，被用作一些常见的文本格式化。由"管道符"指示, 格式如下：

```
<!-- 在两个大括号中 -->
{{ message | capitalize }}

<!-- 在 v-bind 指令中 -->
<div v-bind:id="rawId | formatId"></div>
```

过滤器函数接受表达式的值作为第一个参数。

以下实例对输入的字符串第一个字母转为大写：

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 过滤器</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  {{ message | capitalize }}
</div>
	
<script>
new Vue({
  el: '#app',
  data: {
	message: 'abc.com' //Abc.com
  },
  filters: {//过滤器
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString() //toString()将前面的对象转换为字符串对象
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
})
</script>
</body>
</html>
```

过滤器可以串联：

```
{{ message | filterA | filterB }}
```

过滤器是 JavaScript 函数，因此可以接受参数：

```
{{ message | filterA('arg1', arg2) }}
```

这里，message 是第一个参数，字符串 'arg1' 将传给过滤器作为第二个参数， arg2 表达式的值将被求值然后传给过滤器作为第三个参数。

#### 10、缩写

### v-bind 缩写

Vue.js 为两个最为常用的指令提供了特别的缩写：

```
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```

### v-on 缩写

```
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```

## 三、Vue.js 条件语句

### 一）条件判断

### 1、v-if

在元素 和 template 中使用 v-if 指令。v-if值可以是属性、表达式(值只能是true或false)，或者true或false。

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - if</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
    <p v-if="seen">现在你看到我了</p>
    <template v-if="ok"><!--<template>是模板占位符，标签本身不会被渲染-->
      <h1>VUE教程</h1>
      <p>学的不仅是技术，更是梦想！</p>
    </template>
</div>
    
<script>
new Vue({
  el: '#app',
  data: {
    seen: true,
    ok: true
  }
})
</script>
</body>
</html>
```

#### 2、v-else

配合v-if使用。

```
<div id="app">
    <div v-if="Math.random() > 0.5">
      Sorry
    </div>
    <div v-else>
      Not sorry
    </div>
</div>
    
<script>
new Vue({
  el: '#app'
})
</script>
```

#### 3、v-else-if

用作 v-if 的 else-if 块。可以链式的多次使用：

```
<div id="app">
    <div v-if="type === 'A'">
      A
    </div>
    <div v-else-if="type === 'B'">
      B
    </div>
    <div v-else-if="type === 'C'">
      C
    </div>
    <div v-else>
      Not A/B/C
    </div>
</div>
    
<script>
new Vue({
  el: '#app',
  data: {
    type: 'C'
  }
})
</script>
```

#### 4、v-show

v-show 指令指令来根据条件展示元素

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - v-show </title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
    <h1 v-show="ok">Hello!</h1>
</div>
	
<script>
new Vue({
  el: '#app',
  data: {
    ok: true
  }
})
</script>
</body>
</html>
```

## 四、Vue.js 循环语句

vue.js使用v-for来实现渲染的循环。

### 一）源数据数组使用v-for

循环使用 v-for 指令，要以 **site in sites** 形式的特殊语法， sites 是源数据数组， site 是数组元素迭代的别名。

```
<div id="app">
  <ol>
    <li v-for="site in sites">
      {{ site.name }}
    </li>
  </ol>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    sites: [
      { name: 'sogou' },
      { name: 'Google' },
      { name: 'Taobao' }
    ]
  }
})
</script>
```

### 二）模板中使用 v-for

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - v-for</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  <ul>
    <template v-for="site in sites">
      <li>{{ site.name }}</li>
      <li>--------------</li>
    </template>
  </ul>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    sites: [
      { name: 'sohu' },
      { name: 'Google' },
      { name: 'Taobao' }
    ]
  }
})
</script>
</body>
</html>
```

### 三）v-for 迭代对象属性

v-for 可以通过对象的属性来迭代数据。

语法 格式：(v-for="(value,key,index) in 对象名")  

前面的值value,key,index可以取其中的一部分。第一个参数是值，第二个是键，第三个是索引，变量可以不是value,key,index.

```
<div id="app">
  <ul>
    <li v-for="(value,key,index) in object">
    {{key}}-{{ value }}
    </li>
  </ul>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    object: {
      name: 'VUE教程',
      url: 'http://www.abc.com',
      slogan: '学的不仅是技术，更是梦想！'
    }
  }
})
</script>
```

### 四）v-for 迭代整数

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - v-for 迭代整数</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  <ul>
    <li v-for="n in 10">
     {{ n }}
    </li>
  </ul>
</div>

<script>
new Vue({
  el: '#app'
})
</script>
</body>
</html>
```

## 五、Vue.js 计算属性

### 一）计算属性: computed

```
语法：computed:{}  //在模板中调用时直接写属性名即可。
```

功能：可以用于获取或设置属性。

### 二） 示例

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 -字符串反转</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  {{ message.split('').reverse().join('') }}
</div>

<script>
new Vue({
  el: '#app',
  data: {
    message: 'I like VUE!'
  }
})
</script>
</body>
</html>
```

或者：

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 计算属性</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  <p>原始字符串: {{ message }}</p>
  <p>计算后反转字符串: {{ reversedMessage }}</p>
  <p>{{asd()}}</p>
</div>

<script>
var vm = new Vue({
  el: '#app',
  data: {
    message: 'I like VUE!'
  },
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
})
</script>
</body>
</html>
实例 2 中声明了一个计算属性 reversedMessage 。
提供的函数将用作属性 vm.reversedMessage 的 getter 。
vm.reversedMessage 依赖于 vm.message，在 vm.message 发生改变时，vm.reversedMessage 也会更新。
```

## 三）computed 和 methods区别

一般来说可以使用methods替换computed,但两者也有如下区别：

```
1、computed（计算属性）是带缓存的，需要依赖数据发生改变，才会重新进行计算，否则直接返回之前的计算结果，而methods里的函数（即实例方法）在每次调用时候都要执行。
2、在HTML的插值里调用方式不一样，computed的调用像属性一样访问，methods定义的成员必须以函数的形式调用。
3、computed中的成员可以只定义一个函数作为属性，也可以定义get/set变成可读写的属性，这点是methods不可以做到的。
```

### 四）setter

computed 属性默认只有 getter ,在需要时你也可以提供一个 setter 

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - setter </title>
<script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  <p>{{ site }}</p>
</div>

<script>
var vm = new Vue({
  el: '#app',
  data: {
	name: 'Google',
	url: 'http://www.google.com'
  },
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
})
// 调用 setter， vm.name 和 vm.url 也会被对应更新
vm.site = 'abc软件 http://www.abc.com';
document.write('name: ' + vm.name);
document.write('<br>');
document.write('url: ' + vm.url);
</script>
</body>
</html>
```

## 六、属性监听

### 一）概念

监听就是对内置对象的状态或者属性变化进行监听并且做出反应的响应，监听属性，意思就是可以监视其他数据的变化。

### 二）应用方法

1、使用watch配置项，在配置项里面写上要监视的属性

每次属性值的变化都会触发handler函数回调，也可以监视计算属性的变化。

2、可以使用实例对象的$watch方法在外部监听属性的变化。

```
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>
	<script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>
</head>
   <body>
      <div id = "computed_props">
         千米 : <input type = "text" v-model = "kilometers">
         米 : <input type = "text" v-model = "meters">
      </div>
	   <p id="info"></p>
      <script type = "text/javascript">
         var vm = new Vue({
            el: '#computed_props',
            data: {
               kilometers : 0,
               meters:0
            },
            methods: {
            },
            computed :{
            },
            watch : {
               kilometers:function() {
                  this.meters = this.kilometers * 1000
               },
               meters : function () {
                  
                  this. kilometers =this.meters/1000;
               }
            }
         });
         // $watch 是一个实例方法
		vm.$watch('kilometers', function (newValue, oldValue) {
			// 这个回调将在 vm.kilometers 改变后调用
		    document.getElementById ("info").innerHTML = "修改前值为: " + oldValue + "，修改后值为: " + newValue;
		})
      </script>
   </body>
</html>
```

## 七、样式绑定

class 与 style 是 HTML 元素的属性，用于设置元素的样式，我们可以用 v-bind 来设置样式属性。

Vue.js v-bind 在处理 class 和 style 时， 表达式的结果类型除了字符串之外，还可以是对象或数组。

### 一）class 属性绑定

#### 1、为 v-bind:class 设置一个对象，从而动态的切换 class

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - v-bind:class</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<style>
.active {
	width: 100px;
	height: 100px;
	background: green;
}
</style>
</head>
<body>
<div id="app">
  <div v-bind:class="{ 'active': isActive }"></div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    isActive: true
  }
})
</script>
</body>
</html>
```

#### 2、在对象中传入更多属性用来动态切换多个 class 

```
语法格式：v-bind:class={样式表选择器名:属性名,样式表选择器名:属性名,...}
```

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 动态切换多个 class</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<style>
.active {
	width: 100px;
	height: 100px;
	background: green;
}
.text-danger {
	background: red;
}
</style>
</head>
<body>
<div id="app">
  <div v-bind:class="{ 'active': isActive, 'text-danger': hasError }">
  </div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    isActive: true,
	hasError: true
  }
})
</script>
</body>
</html>
```

#### 3、直接绑定数据里的一个对象

1）v-bind:class="data子对象名（data的一个属性名）"

2）data子对象书写格式：

​		键名:{样式表名1：布尔值，样式表名2：布尔值,...}

注：样式表名中杠（-）需要给键名加单引号。

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 直接绑定数据里的对象</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<style>
.active {
	width: 100px;
	height: 100px;
	background: green;
}
.text-danger {
	background: red;
}
</style>
</head>
<body>
<div id="app">
  <div v-bind:class="classObject"></div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    classObject: {
      active: true,
      'text-danger': true
    }
  }
})
</script>
</body>
</html>
```

#### 4、绑定返回对象的计算属性

```
1、语法：v-bind:class=计算属性
2、计算属性返回一个对象{键名（样式表）:比较或逻辑表达 }
```



```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 绑定返回对象的计算属性</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<style>
.base {
  width: 100px;
  height: 100px;
}
.active {
  background: green;
}
.text-danger {
  background: red;
}
</style>
</head>
<body>
<div id="app">
  <div v-bind:class="classObject"></div>
</div>
<script>

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
</script>
</body>
</html>
```

#### 5、数组语法

可以把一个数组传给 **v-bind:class** 

```
语法：v-bind:class=[属性名]
在数据中，属性对应的值是样式表的名。
```

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 数组值</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<style>
.active {
	width: 100px;
	height: 100px;
	background: green;
}
.text-danger {
	background: red;
}
</style>
</head>
<body>
<div id="app">
	<div v-bind:class="[activeClass, errorClass]"></div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    activeClass: 'active',
    errorClass: 'text-danger'
  }
})
</script>
</body>
</html>
```

#### 6、使用三元表达式来切换列表中的 class

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 三元表达式来切换列表</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
<style>
.text-danger {
	width: 100px;
	height: 100px;
	background: red;
}
.active {
	width: 100px;
	height: 100px;
	background: green;
}
</style>
</head>
<body>
<div id="app">
	<div v-bind:class="[errorClass ,isActive ? activeClass : '']"></div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    isActive: true,
	activeClass: 'active',
    errorClass: 'text-danger'
  }
})
</script>
</body>
</html>
```

### 二）style(内联样式)

1、在 **v-bind:style** 直接设置样式

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 直接设置样式</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
	<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">直接设置样式</div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    activeColor: 'green',
	fontSize: 30
  }
})
</script>
</body>
</html>
```

#### 2、直接绑定到一个样式对象，让模板更清晰

```
v-bind:style="data里的属性名"，该属性的属性值是一个样式表对象
```



```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 直接绑定到一个样式对象</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  <div v-bind:style="styleObject">绑定到一个样式对象</div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    styleObject: {
      color: 'green',
      fontSize: '30px'
    }
  }
})
</script>
</body>
</html>
```

#### 3、使用数组将多个样式对象应用到一个元素上

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 使用数组将多个样式对象应用到一个元素上</title>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
</head>
<body>
<div id="app">
  <div v-bind:style="[baseStyles, overridingStyles]">style绑定</div>
</div>

<script>
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
</script>
</body>
</html>
```



---

练习：

1、已知接受到的数据是：

{
	boss:"zhangsheng",
	pass:["123","333","666","567","886","765","333","999"]
	}

请输出8个li,每个li中的账户是zhangsheng1...zhangsheng8,并且其密码与pass数组中的值相同。

2、生成一个10行三列的表格，并且表格要隔行换色。

3、在段落标签中插入10张图片。

4、单击超链接出现菜单。