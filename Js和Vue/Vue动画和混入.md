# 动画   -transition

将单个可变化元素放到transition标签中

## 动画样式

v  可替换成transition的标签name名

### v-if变为true时应用的样式

**v-enter{}    作用--设置开始状态**
**v-enter-active{}   作用--应用动画**

v-enter-to{} --结束状态不设置的情况下默认为元素的初始状态

### v-if变为false时应用的样式

**v-leave-to{}   作用--离开过度的结束状态**
**v-leave-active     作用--设置动画**

v-leave   --- 离开过渡的开始状态，默认不设置的情况下为元素的初始窗台



```html
<style>
    .hello-enter-active,   //应用动画
    .hello-leave-active {
    transition: all 1s;
    }
    .hello-enter,       //变为true时的初始状态
    .hello-leave-to {   //变为false的结束状态
    transform: translateX(10px);
    opacity: 0;
    }
</style>
     
<transition>
    <div v-if="show">HELLO</div>
</transition>
```

# 混入   mixin

当混入出现冲突时

属性(钩子函数)  --- 两者合并

自定义方法        ---Vue替换mixin

## 全局混入

```
Vue.mixin(混入名,{混入对象})
```

```
Vue.mixin('show',{
	data(){
		return:{
			num:0
		}
	},
	mounted(){},  //钩子函数
	methods:{},  //自定义函数
	watch:{},  //监听
	components:{},  //自定义组件
	computed{},  //计算属性
})
```

## 局部混入

```
var show = {
	data(){
		return:{
			num:0
		}
	},
	mounted(){},  //钩子函数
	methods:{},  //自定义函数
	watch:{},  //监听
	components:{},  //自定义组件
	computed{},  //计算属性
}

var app  = new Vue({
	el:'#app',
	mixins:[show]
})
```

