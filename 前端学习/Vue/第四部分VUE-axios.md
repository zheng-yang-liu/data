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
语法：axios.all([请求1,请求2,...]).then(axios.spread(function(res1,res2){}))
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
  mounted(){
    axios
      .post('/user/?ID=123')
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
axios.get(url[,config]); //GET 请求用于从服务器获取数据
axios.delete(url[,config]); //DELETE 请求用于删除服务器上的数据
axios.head(url[,config]);
axios.post(url[,data[,config]]); //POST 请求用于向服务器新增数据
axios.put(url[,data[,config]]); //PUT 请求用于更新服务器上的数据（侧重于完整更新：如更新用户的完整信息）
axios.patch(url[,data[,config]]) //PATCH 请求用于更新服务器上的数据（侧重于部分更新：例如只更新用户的手机号）
```

注意：当我们在使用别名方法的时候，`url,method,data`这几个参数不需要在配置中声明。

```
axios
  .request({
    method: "GET",
    url: "http://localhost/",
  })
  .then((response) => {
    console.log(response);
  });
```

#### 4、并发请求（concurrency）

帮助处理并发请求的辅助函数

```
//iterable是一个可以迭代的参数如数组等
axios.all(iterable)
//callback要等到所有请求都完成才会执行
axios.spread(callback)
```

#### 5、创建一个axios实例，并自定义其配置

创建axios对象的方法：

```
var a=axios.create({})
```

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

```
<script src="axios.min.js"></script>
<script>
var instance = axios.create({
  baseURL:"http://localhost/",
  timeout:2000,
  headers: {'X-Custom-Header':'foobar'}
});
instance
  .request('index.php?ID=32')
  .then((response) => {
    document.write(response.data);
  });
</script>
```

### 二）请求的配置（request config）

以下就是请求的配置选项（前面内容中，出现config处的内容都是配置选项），只有`url`选项是必须的，如果`method`选项未定义，那么它默认是以`GET的方式`发出请求。

```
{
  //url是请求的服务器地址
  url:'/user',
  //method是请求资源的方式
  method:'get'//default
  //如果url不是绝对地址，那么baseURL将会加到url的前面
  //当url是相对地址的时候，设置baseURL会非常的方便
  baseURL:'https://some-domain.com/api/',
  //transformRequest选项允许我们在请求发送到服务器之前对请求的数据做出一些改动
  //该选项只适用于以下请求方式：`put/post/patch`
  //数组里面的最后一个函数必须返回一个字符串、-一个ArrayBuffer或者Stream
  transformRequest:[function(data){
    //在这里根据自己的需求改变数据
    return data;
  }],
  //transformResponse选项允许我们在数据传送到then/catch方法之前对数据进行改动
  transformResponse:[function(data){
    //在这里根据自己的需求改变数据
    return data;
  }],
  //headers选项是需要被发送的自定义请求头信息
  headers: {'X-Requested-With':'XMLHttpRequest'},
  //params选项是要随请求一起发送的请求参数----一般链接在URL后面
  //他的类型必须是一个纯对象或者是URLSearchParams对象
  params: {
    ID:12345
  },
  //paramsSerializer是一个可选的函数，起作用是让参数（params）序列化
  //例如(https://www.npmjs.com/package/qs,http://api.jquery.com/jquery.param)
  paramsSerializer: function(params){
    return Qs.stringify(params,{arrayFormat:'brackets'})
  },
  //data选项是作为一个请求体而需要被发送的数据
  //该选项只适用于方法：put/post/patch
  //当没有设置`transformRequest`选项时dada必须是以下几种类型之一
 //string/plain/object/ArrayBuffer/ArrayBufferView/URLSearchParams
  //仅仅浏览器：FormData/File/Bold
  //仅node:Stream
  data {
    firstName:"Fred"
  },
  //timeout选项定义了请求发出的延迟毫秒数
  //如果请求花费的时间超过延迟的时间，那么请求会被终止
  timeout:1000,
  //withCredentails选项表明了是否是跨域请求
  withCredentials:false,//default
  //adapter适配器选项允许自定义处理请求，这会使得测试变得方便
  //返回一个promise,并提供验证返回
  adapter: function(config){
    /*..........*/
  },
  //auth表明HTTP基础的认证应该被使用，并提供证书
  //这会设置一个authorization头（header）,并覆盖你在header设置的Authorization头信息
  auth: {
    username:"zhangsan",
    password: "s00sdkf"
  },
  //返回数据的格式
  //其可选项是arraybuffer,blob,document,json,text,stream
  responseType:'json',//default
  xsrfCookieName: 'XSRF-TOKEN',//default
  xsrfHeaderName:'X-XSRF-TOKEN',//default
  //onUploadProgress上传进度事件
  onUploadProgress:function(progressEvent){
    //下载进度的事件
onDownloadProgress:function(progressEvent){
}
  },
  //相应内容的最大值
  maxContentLength:2000,
  //validateStatus定义了是否根据http相应状态码，来resolve或者reject promise
  //如果validateStatus返回true(或者设置为null或者undefined),那么promise的状态将会是resolved,否则其状态就是rejected
  validateStatus:function(status){
    return status >= 200 && status <300;//default
  },
  //maxRedirects定义了在nodejs中重定向的最大数量
  maxRedirects: 5,//default
  //httpAgent/httpsAgent定义了当发送http/https请求要用到的自定义代理
  //keeyAlive在选项中没有被默认激活
  httpAgent: new http.Agent({keeyAlive:true}),
  httpsAgent: new https.Agent({keeyAlive:true}),
  //proxy定义了主机名字和端口号，
  //auth表明http基本认证应该与proxy代理链接，并提供证书
  //这将会设置一个`Proxy-Authorization` header,并且会覆盖掉已经存在的`Proxy-Authorization`  header
  proxy: {
    host:'127.0.0.1',
    port: 9000,
    auth: {
      username:'skda',
      password:'radsd'
    }
  },
  //cancelToken定义了一个用于取消请求的cancel token
  //详见cancelation部分
  cancelToken: new cancelToken(function(cancel){
  })
}
```

## 四、请求返回的内容

```
{
  data:{},
  status:200,
  //从服务器返回的http状态文本
  statusText:'OK',
  //响应头信息
  headers: {},
  //`config`是在请求的时候的一些配置信息
  config: {}
}
你可以这样来获取响应信息
axios.get('/user/12345')
  .then(function(res){
    console.log(res.data);
    console.log(res.status);
    console.log(res.statusText);
    console.log(res.headers);
    console.log(res.config);
  })

```

## 五、默认配置

你可以设置默认配置，对所有请求都有效。

#### 1、 全局默认配置

```
axios.defaults.baseURL = 'http://api.exmple.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['content-Type'] = 'appliction/x-www-form-urlencoded';
```

#### 2、自定义的实例默认设置

```
//当创建实例的时候配置默认配置
var instance = axios.create({
    baseURL: 'https://api.example.com'
});
//当实例创建时候修改配置
instance.defaults.headers.common["Authorization"] = AUTH_TOKEN;
```

#### 3、配置中的有优先级

`config配置`将会以优先级别来合并，顺序是`lib/defauts.js`中的默认配置，然后是实例中的默认配置，最后是请求中的`config参数的配置`，越往后等级越高，后面的会覆盖前面的例子。

```
//创建一个实例的时候会使用libray目录中的默认配置
//在这里timeout配置的值为0，来自于libray的默认值
var instance = axios.create();
//回覆盖掉library的默认值
//现在所有的请求都要等2.5S之后才会发出
instance.defaults.timeout = 2500;
//这里的timeout回覆盖之前的2.5S变成5s
instance.get('/longRequest',{
  timeout: 5000
});
```

## 六、拦截器

### 一）添加拦截器

可以在请求、响应在到达then/catch之前拦截他们

```
//添加一个请求拦截器
axios.interceptors.request.use(function(config){
  //在请求发出之前进行一些操作
  return config;
},function(err){
  //Do something with request error
  return Promise.reject(error);
});
//添加一个响应拦截器
axios.interceptors.response.use(function(res){
  //在这里对返回的数据进行处理
  return res;
},function(err){
  //Do something with response error
  return Promise.reject(error);
})
```

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
	//添加一个响应拦截器
	axios.interceptors.response.use(function(res){
  		return res.data;
	},function(err){	
  	return Promise.reject(error);
	});
    axios
      .post('/user/?ID=123')
      .then(response => (this.info = response))
      .catch(function (error) { // 请求失败处理
        console.log(error);
      });
     }
    });
    </script>
   </body>
   </html>
```

### 二）取消拦截器

```
var myInterceptor = axios.interceptor.request.use(function(){/*....*/});
axios.interceptors.request.eject(myInterceptor);
```

### 三）给自定义的axios实例添加拦截器

```
var instance = axios.create();
instance.interceptors.request.use(function(){})
```

## 七、错误处理

```
axios.get('/user/12345')
  .catch(function(error){
    if(error.response){
      //请求已经发出，但是服务器响应返回的状态吗不在2xx的范围内
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.header);
    }else {
      //一些错误是在设置请求的时候触发
      console.log('Error',error.message);
    }
    console.log(error.config);
  });

```

## 八、取消

通过一个cancel token来取消一个请求

使用CancelToken.source工厂函数来创建一个cancel token

```
var CancelToken = axios.CancelToken;
var source = CancelToken.source();
axios.get('/user/12345',{
  cancelToken: source.token
}).catch(function(thrown){
  if(axios.isCancel(thrown)){
    console.log('Request canceled',thrown.message);
  }else {
    //handle error
  }
});
//取消请求（信息的参数可以设置的）
source.cance("操作被用户取消");
```

给cancelToken构造函数传递一个executor function来创建一个cancel token:

```
var cancelToken = axios.CancelToken;
var cance;
axios.get('/user/12345',{
  cancelToken: new CancelToken(function(c){
    //这个executor函数接受一个cancel function作为参数
    cancel = c;
  })
})
//取消请求
cancel();

```

