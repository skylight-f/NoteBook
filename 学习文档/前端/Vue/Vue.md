# 路由模式

1. hash  - 即地址栏中url中的#符号; 如http://www.xxxx.com/#/hello

2. history --利用了HTML5 history interface 中新增的 pushState() 和 replaceState() 方法。（这个方法就是面试中常问到的，怎么去除url中的# 号，此方法需要后端apache 或 nginx进行简单的路由配置，否则或报404.）

   注： “这两种配置就是解决url中有没有#号的问题，如果不在意#号，就使用hash，否则使用history”

## element table表格使用v-if来回切换内容冲突

问题：多个table表格使用v-if切换展示时，多个相同的标签被渲染，导致table表格渲染内容出错

如果不添加key来区分则会出现数据冲突

解决方法：给table加个:key就可以

# 生命周期钩子函数

- beforeCreate()
- created()
- beforeMount()
- mounted()
- beforeUpdate()
- updated()
- beforeDestroy()
- destroyed()
- activated()
- deactivated()
- errorCaptured()

# computed() 和 watch() 

- computed: 

  ​	计算属性里面的值是响应式的

  ​	必须依赖其他属性来计算值,computed的值有缓存

- watch: 只要监听到值的变化就会执行回调,在回调当中可以执行一些逻辑操作

# v-if  和  v-show 
**（1）手段：**
v-if是动态的向DOM树内添加或者删除DOM元素；
v-show是通过设置DOM元素的display样式属性控制显隐；
**（2）编译过程：**
v-if切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件；
v-show只是简单的基于css切换；
**（3）编译条件：**
v-if是惰性的，如果初始条件为假，则什么也不做；只有在条件第一次变为真时才开始局部编译（编译被缓存？编译被缓存后，然后再切换的时候进行局部卸载);
v-show是在任何条件下（首次条件是否为真）都被编译，然后被缓存，而且DOM元素保留；
**（4）性能消耗：**
v-if有更高的切换消耗；
v-show有更高的初始渲染消耗；
**（5）使用场景：**
v-if适合运营条件不大可能改变；
v-show适合频繁切换。

# 组件中的 data 什么时候可以使用对象

组件复用时,实例会共享data,如果data是对象,那么修改一处组件的data,会影响所有的组件,所以需要将data写成函数,

 如果组件确定只有一处使用,data可以写成对象(但仍然强烈不建议)

# 组件之间通讯/共享数据

父子传值 v-bind 属性绑定

子父传值 v-on 事件绑定

兄弟组件 eventbus

- $on 接受数据的那个组件
- $emit 发送数据的那个组件

## VueX 

- VueX 是实现组件全局状态(数据)管理的机制,可以方便的实现组件之间的数据共享
- 能够在vuex中集中管理共享的数据,易于开发和后期维护
- 存储在vuex 中的数据都是响应式的,能后保证数据与页面的同步

> 一般情况下,只有组件之间共享的数据,才有必要存储到vuex中,对于组件的私有数据,一九存储在组件自身的data中即可



# vue2 借助 componsition-api写vue3的语法

npm install @vue/composition-api

```javascript
import { onMounted, reactive } from '@vue/composition-api'
import router from '@/router/index'
import store from '@/store/index'
```

为什么不直接升级只vue3

成本问题

为什么要使用`componsition-api`, `componsition-api`语法优势明显

# 如何使用


以上的内容相比大家见得很多了，但是几乎没有在jym的文章中找到关于如何使用router和vuex等，大家都只介绍如何使用setup，ref，reactive，就可以像vue3一样使用componsition-api风格的代码了，但只字不提router，vuex等等，

vue2中使用componsition-api中的setup中没有this，但是vue-router4.0以下是没有useRouter这样的方法的，之前常规的`this.$router`书写路由的写法显然就没法使用了。

那么如何像vue3一样的写法在vue2搭配`componsition-api`中使用router呢？


- vue-router

想必大家都还记得，在vue2中想要使用router，需要new 一个VueRouter实例，并且挂载在main.js中的vue实例上，这样我们才可以在全局使用`this.router`



由此想到了什么，直接在对应的页面，想`import { useRouter } from 'vue-router'` 一样，直接在页面引入router实例，然后调用便好了。

- vuex

# vue2 深度监听
