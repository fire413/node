vue3项目目录结构

![image-20201028100636212](https://i.loli.net/2020/10/28/LxD4JTZsF683qjS.png)

ref()  

reactive()

toRefs()

生命周期

setup(): 开始创建组件之前，在beforeCreate、created之前执行，创建的是data与methods。

onBeforeMount(): 组件挂载到节点之前执行

onMounted():组件挂载到节点之后执行

onBeforeUpdate():组件更新之前执行

onUpdated():组件更新之后执行

onBeforeUnmount():组件卸载之前执行

onUnmount():组件卸载之后执行

onActivated(): 被包含在`<keep-alive>`中的组件，会多出两个生命周期钩子函数。被激活时执行。

onDeactivated(): 比如从 A 组件，切换到 B 组件，A 组件消失时执行。

onErrorCaptured(): 当捕获一个来自子孙组件的异常时激活钩子函数（以后用到再讲，不好展现）。

注：使用`<keep-alive>`组件会将数据保留在内存中，比如我们不想每次看到一个页面都重新加载数据，就可以使用`<keep-alive>`组件解决。

vue2.x与vue3.x生命周期函数对比：

![image-20201028165136723](https://i.loli.net/2020/10/28/twuBEg6SskbRQ9q.png)