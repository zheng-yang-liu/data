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
  // 选项
})
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
	{{5+5}}<br>
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
	id : 1
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
    <input v-model="message">
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
  methods: {
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
	message: 'abc.com'
  },
  filters: {//过滤器
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
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