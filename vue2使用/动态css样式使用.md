# 动态css样式使用
使用逻辑

1. 使用v-bind语法结合css样式绑定样式
2. 使用条件选择表达式选择符合条件的样式进行css渲染

## 使用v-bind语法结合css样式绑定样式

实现点击按钮改变div盒子样式

```
.one{
	background-color:red;

}
.two{
	background-color:green;
}
div{
    width:100px;
    height:100px;
}

<div :class="sty" @click="changeclass">点击我改变我的背景颜色</div>

data(){
    return{
        sty:'one',
        isclass:false
    }
},
methods:{
    changeclass(){
        console.log("点击");
        console.log(this.isclass);
        if(this.isclass){
        	this.sty='one';
        }else{
        	this.sty='two';
        }
        this.isclass=!this.isclass;
        }
    }
}
```

使用条件选择表达式选择符合条件的样式进行css渲染

```
.one{
	background-color:red;

}
.two{
	background-color:green;
}
div{
    width:100px;
    height:100px;
}

<div :class="isclass?'one':'two'" @click="isclass=!isclass;">点击我改变我的背景颜色</div>

data(){
    return{
        sty:'one',
        isclass:false
    }
},

```

