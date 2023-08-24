# 第四部分 VUE-axios

## 一、介绍及安装

### 一）axios

#### 1、概念

`axios` 是一个基于Promise 用于浏览器和 nodejs 的 HTTP 客户端。简单的理解就是ajax的封装。

#### 2、特征

- 从浏览器中创建 XMLHttpRequest
- 从 node.js 发出 http 请求
- 支持 Promise API
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防止 CSRF/XSRF（跨站请求伪造，Cross-site request forgery）

#### 3、axios API体系

![](vue-5.png)

### 二）安装

#### 1、使用nmp安装

```
npm install axios
```

#### 2、使用CDN

```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

## 二、示例

### 一）发送一个GET请求

```
语法：
axios.get(url) //将参数写到URL中。
axios.get(url,{params:{参数列表}})
```

```test1.html
<!DOCTYPE html>
<html>
<head>
<script src="axios.min.js"></script>
</head>
<body>
<script>
//通过给定的ID来发送请求
axios.get('/user?ID=12345')
  .then(function(response){
    console.log(response);
  })
  .catch(function(error){
    console.log(error);
  });
 
</script>
</body>
</html>
```

或者

```test2.html
<!DOCTYPE html>
<!--需要配合user目录下的php文件来应用-->
<html>
<head>
<script src="axios.min.js"></script>
</head>
<body>
<script>
//以上请求也可以通过这种方式来发送
axios.get('/user',{
  params:{
    ID:12345
  }
})
.then(function(response){
  console.log(response);
})
.catch(function(error){
  console.log(error);
});
</script>
</body>
</html>
```

### 二）发送一个POST请求

```
<!DOCTYPE html>
<html>
<head>
<script src="axios.min.js"></script>
</head>
<body>
<script>
axios.post("/user/p.php",{
fName:"Tao",
lName:"Li"
})
.then(function(res){
  console.log(res);
})
.catch(function(error){
  console.log(error);
});
</script>
</body>
</html>
```

### 三）一次性并发多个请求

```
语法：axios.all([请求1,请求2,...])
```

```
function getUserAccount(){
  return axios.get('/user/12345');
}
function getUserPermissions(){
  return axios.get('/user/12345/permissions');
}
axios.all([getUserAccount(),getUserPermissions()])
  .then(axios.spread(function(acct,perms){
    //当这两个请求都完成的时候会触发这个函数，两个参数分别代表返回的结果
  }))
```

```
<!DOCTYPE html>
<html>
<head>
<script src="axios.min.js"></script>
</head>
<body>
<script>
function getUserAccount(){
  return axios.get('/user/?ID=12345');
}
function getUserPermissions(){
  return axios.get('/user/?ID=666');
}
axios.all([getUserAccount(),getUserPermissions()])
  .then(axios.spread(function(acct,perms){
    console.log(acct,perms);
  }))
</script>
</body>
</html>
```

### 四）与VUE整合示例

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - axios</title>
<script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>
<script src="https://cdn.staticfile.org/axios/0.18.0/axios.min.js"></script>
</head>
<body>
<div id="app">
  {{ info }}
</div>
<script type = "text/javascript">
new Vue({
  el: '#app',
  data () {
    return {
      info: null
    }
  },
  mounted () {
    axios
      .post('/user/?id=123')
      .then(response => (this.info = response))
      .catch(function (error) { // 请求失败处理
        console.log(error);
      });
  }
})
</script>
</body>
</html>
```

## 三、axios的API

### 一）axios可以通过配置（config）来发送请求

#### 1、axios(config)

```
<script src="axios.min.js"></script>
<script>
axios({
    method:"POST",
    url:'/user/p2.php',
    data:{
        firstName:"Fred",
        lastName:"Flintstone"
    }
}).then(function(response){
  console.log(response);
})
.catch(function(error){
  console.log(error);
});
</script>
```

#### 2、axios(url[,config])

```
//发送一个`GET`请求（默认的请求方式）
axios('/user/12345');
```

#### 3、请求方式的别名

这里对所有已经支持的请求方式都提供了方便的别名

```
axios.request(config);
axios.get(url[,config]);
axios.delete(url[,config]);
axios.head(url[,config]);
axios.post(url[,data[,config]]);
axios.put(url[,data[,config]])
axios.patch(url[,data[,config]])
```

注意：当我们在使用别名方法的时候，`url,method,data`这几个参数不需要在配置中声明。

#### 4、并发请求（concurrency）

帮助处理并发请求的辅助函数

```
//iterable是一个可以迭代的参数如数组等
axios.all(iterable)
//callback要等到所有请求都完成才会执行
axios.spread(callback)
```

#### 5、创建一个axios实例，并自定义其配置

```
var instance = axios.create({
  baseURL:"https://some-domain.com/api/",
  timeout:1000,
  headers: {'X-Custom-Header':'foobar'}
});
```

实例的方法：

以下是实例方法，注意已经定义的配置将和利用create创建的实例的配置合并

```
axios#request(config)
axios#get(url[,config])
axios#delete(url[,config])
axios#head(url[,config])
axios#post(url[,data[,config]])
axios#put(url[,data[,config]])
axios#patch(url[,data[,config]])
```

