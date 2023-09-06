# 3-Ajax整体方法

ajax创建

```
if(window.XMLHttpRequest){
	var oAjax = new XMLHttpRequest()
}else{
	var oAjax = new ActiveXObjict("Microsoft.XMLHTTP")
}
```

ajax链接

```
oAjax.open(连接方式,文件名,同步异步)
```

ajax请求

```
oAjax.send()
```

ajax返回值

```
oAjax.onreadystatechange=()=>{
	if(oAjax.readyState==4&&oAjax.stetus==200){
		alter("请求成功"+oAjax.responseText)
	}else{
		alter("请求失败"+oAjax.stetus)
	}
}
```





