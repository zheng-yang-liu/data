# vuex路由管理

安装vuex

可以在新建项目时进行勾选也可以自行安装

自行安装

```
npm install vuex --save
```

创建文件

创建store文件夹index.js文件

index.js文件框架

```
// 引入vuex
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    // 定义的数据
  },
  getters: {
    // 针对数据进行二次计算
    名称(state){
      return 显示的值
    }
  },
  // $store.commit(tape函数名称,改变的值)
  // 变量的修改只能应用以该页面刷新便会原样
  mutations: {
    // 操作数据 state
    // 同步操作
    // 用来改变state的值
    名称(state,传参(可有可无)){
      函数体
    }
  },
  actions: {
    // 操作数据 state
    // 异步操作
  },
  modules: {
    // 
  }
})

```

全局使用

```
在script中使用前面需要加tihs.
全局使用state定义的属性
    {{$store.state.name}}
    {{$store.state.属性名}}
    
全局使用getters二次处理数据
    {{$store.getters.userID}}
    {{$store.getters.函数名}}
```

局部使用

```
局部使用state定义的属性

	{{name}}
	{{userinfo}}

    import {mapState} from "vuex"
    //计算属性
    computed:{
    //拓展运算符
        ...mapState(['name', 'userinfo']),
        ...mapState(['属性名', '属性名']),
    },
局部使用getters定义的属性
	
	{{userID}}
	
	import {mapGetters} from "vuex"
	//计算属性
	 computed:{
            //拓展运算符
            ...mapGetters(['userID','setAge'])
            ...mapGetters(['函数名','函数名'])
     },

```

模板

```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    // 在这里定义你的变量数据
  },
  mutations: {
    // 在这里定义你的状态变更方法
  },
  actions: {
    // 在这里定义你的异步操作
  },
  getters: {
    // 在这里定义你的计算属性
  }
})

```

