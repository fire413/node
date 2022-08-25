npm安装机制：

1.在node_modules中查找是否存在

存在，不再重新安装

不存在，在registry中查找网址

下载包到根目录的.npm文件夹下

解压包到根目录的node_modules文件夹下

npm安装原理

执行声明周期函数preinstall，有则执行，没有则不执行

确定首层依赖模块，dependencity、Devdependencity

寻找首层依赖下的模块

扁平化模块（去除冗余模块）

安装模块，执行模块生命周期（按照 preinstall、install、postinstall 的顺序）

执行工程自身生命周期（按照 install、postinstall、prepublish、prepare 的顺序）

##### 介绍下 webpack 热更新原理，是如何做到在不刷新浏览器的前提下更新页面

1.修改一个或多个页面

2.文件系统通知webpack

3.webpack重新构建，通知HRM更新

4.HMR Server 使用webSocket通知HMR runtime 需要更新，HMR运行时通过HTTP请求更新jsonp；
5.HMR运行时替换更新中的模块，如果确定这些模块无法更新，则触发整个页面刷新。

浏览器是通过 websocket 和 webpack-dev-server 进行通信的



webpack监听到文件系统发生变化，根据配置文件对模块进行重新打包



