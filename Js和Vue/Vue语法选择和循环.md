# Vue 语法

```
mounted(){}--声明周期

methods:{}--自定义函数
```

# 表达式--任何

转为字符串

```
变量.toString()
```

字母大写

```
str.toUpperCase()
```

字母小写

```
str.toLowerCase()
```

查看变量类型

```
typeof(变量名)
```

提取字符串

```
str.slice(1)//从1开始到结束

前取后不取
```

反序输出

```
数组.reverse()
```

拼接数组为字符串

```
数组.join("")
```

取得字符串中的某个位置的字符

```
str.charAt(1)
```

# 修饰符

```
用于阻止事件的默认行为

.prevent
```

# input--输入框

```
<input type="text" v-model="inputValue" />

{{inputValue}}
```

# select--下拉列表

```
<select name="city" id="city" v-model="selectValue">
    <option value="北京">北京</option>
    <option value="上海">上海</option>
    <option value="保定">保定</option>
</select>

{{selectValue}}}
```

textarea--多行文本输入框

```
<textarea>
    name="textarea"
    id="textarea"
    cols="30"
    rows="10"
    v-model="textareraValue"
    >
</textarea>
{{textareraValue}}
```

# checkbox--复选框

```
<!-- 复选框 -->
<input type="checkbox" id="checkbox" v-model="checkboxValue" />

{{checkboxValue}}
```

# radio--单选框

```
 <!-- 单选框 -->
<input type="radio" id="radio" v-model="radioVale" value="nihao" name="radio"/>
<input type="radio" id="radio" v-model="radioVale" value="zaijian" name="radio"/>
{{radioVale}}
```



# 过滤器

```
{{ str| 自定义规则}}



filters:{
	自定义规则名:function(value){
		
		return 返回改变后的值
	}
}
```



**template**

--模板标签，设置命令的适用范围



# 判断语句

```
v-if

v-else

v-else-if

v-show
```



# 循环

```
v-for="(value,key,index) in 对象"

v-for="(item,index) in 数组"

v-for="item in 10"
```




