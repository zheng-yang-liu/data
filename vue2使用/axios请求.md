# axios请求

## axios安装和使用

安装axios依赖

```
npm install axios

```

.vue文件

这是一种引入的方法还有其他的方法

```
import axios from 'axios'
```

## post请求

```
 axios.post('url链接',{
         需要传递的数据
     })
     .then(res=>{
     	请求成功后执行
 	})

```

### post请求header头参数

```
 axios.post('url链接',{
     	需要传递的数据
     }.{
     headers:{
     	在header头里边传递的数据
     }
     })
     .then(res=>{
     	请求成功后执行
     })

```



## get请求

```
axios.get('url链接?id=0&name=张三)
    .then(res=>{
    请求成功后执行
    })
```

### get请求传递参数

```
axios.get('url链接',{
        params:{
            需要传递的数据
        }
    })
    .then(res=>{
    	请求成功后执行
    })
```



### get请求header头参数

```
axios.get('url链接',{
        params:{
        	需要传递的数据
        },
        headers:{
        	在header头里边传递的数据
        }
    })
    .then(res=>{
    	请求成功后执行
    })
```

## axios请求封装

**用于处理重复的请求操作**

创建封装的js文件

创建utils文件夹新建request.js文件

```
框架
// 封装axios
import axios from "axios"
import router from "@/router"
import elementUI from "element-ui"

// 实例化
//创建一个axios实例如果在5秒内未响应，请求被取消
const a= axios.create({
    timeout:5*1000
})


其他需要操作的内容



export default a;
```

.vue文件引入

```
import request from '@/utils/request'
使用的时候把原来的axios换成本次引入的名
```

拦截请求发出

**interceptors.request.use(config=>{return })**

```
// 拦截请求发出
a.interceptors.request.use(config=>{
    console.log(config);
    // 改变头信息
    let token =localStorage.getItem('token');
    if(token){
        config.headers.Authorization=token;
    } 

    return config
})
```

localStorage.getItem(‘token’)是JavaScript中的一个方法，用于**从浏览器本地存储中获取一个键为’token’的值。**

拦截返回值

**.interceptors.response.use(sucess=>{请求成功return },error=>{接口请求不通过return })**

```
// 拦截返回值
a.interceptors.response.use(sucess=>{
    if(sucess.data.code == 401){
        router.push('/')
        return Promise.resolve("请登录");//返回的是错误的值catch
    }else if(sucess.data.code == 200){
        return Promise.resolve(sucess.data);
    }else{
        elementUI.Message.error("接口请求失败");
        return Promise.reject(sucess.data.msg);
    }

},error=>{
    // 接口请求不同通过
    elementUI.Message.error("接口错误,请重试");
    return Promise.reject("接口请求错误");
})
```

