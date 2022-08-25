路由钩子函数

1. 导航被触发
2. 在失活的组件里调用beforeRouteLeave守卫
3. 调用全局守卫beforeEach
4. 在重用的组件里调用beforeRouteUpdate守卫
5. 在路由配置里调用beforeEnter
6. 解析异步路由组件
7. 在被激活的组件里调用beforeRouteEnter
8. 调用全局的beforeResolve守卫
9. 导航被确认
10. 调用全局的afterEach钩子
11. 触发DOM更新
12. 调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数，创建好的组件实例会作为回调函数的参数传入。

全局前置守卫beforeEach   全局解析守卫beforeResolve  全局后置钩子afterEach

路由独享守卫 beforeEnter

组件内的守卫

渲染该组件被confirm前调用beforeRouteEnter  组件被复用时调用beforeRouteUpdate   导航离开该组件时调用beforeRouteLeave

vue生命周期

beforeCreated create beforeMounted mount beforeUpdated update beforeDestoryed destory

混入

路由钩子函数

数组方法

push pop unshift shift sort some every concat reduce include indexOf splice...

from   of

es6

let、const  Promise  各个类型新增的方法 map class 迭代器

vue自定义指令

Vue.directive()

1、全局自定义指令
（1）定义全局自定义指令
以下就是一个自定义指令让文本框获取焦点的实例：

//自定义全局的指令

```js
Vue.directive('focus', {
     //第一个参数永远是el，表示原生的js对象
     bind: function (el) { //当指令绑定到元素上的时候，会立即执行bind函数，只执行一次，此时元素还没有插入到DOM中,focus聚焦此时不会生效
         el.focus()
     },
     inserted: function (el) { //当元素插入到DOM中的时候，会执行inserted函数，只执行一次
         el.focus()
     },
     updated: function () { //当VNode的时候，会执行updated函数，可能出发多次
     }
 });
（2）使用全局自定义指令
（2）使用全局自定义指令
```

```html
<input type="text" class="form-control" v-model="keywords" v-focus">
```

2、私有自定义指令
（1）和私有自定义过滤器类似，也是将作为和methods平级的属性定义在VM的实例中

```js
directives: {
    'fontweight': {
        bind: function (el, bingding) {
            el.style.fontWeight = bingding.value;
        }
    },
    'fontsize': function (el, bingding) { //这个function等同于把代码写到了bind和update中去
        el.style.fontSize = parseInt(bingding.value) + 'px';
    }
}
（2）在dom中使用该指令
```

```html
 <div id="app2" v-color="'pink'" v-fontweight="200" v-fontsize="20">
    <p>{{date | dateFormat}}</p>
 </div>
```

















