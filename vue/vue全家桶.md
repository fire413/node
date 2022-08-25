1.业务概述
根据不同的应用场景，电商系统一般提供了PC端、PC后台管、小程序、移动web、移动APP等多种终端访问方式。
基于vue技术的SPA项目
前端项目技术栈：1.Vue
	            2.Vue-router
	            3.Element-ui
	            4.Axios
	            5.Echarts
后端项目技术栈：1.Node.js
	            2.Express
	            3.Jwt(状态保持工具)
	            4.Mysql
	            5.Sequelize（仓库管理）
2.1前端项目初始化步骤：1.安装Vue脚手架
		        2.通过Vue脚手架创建项目
		        3.配置Vue路由
		        4.配置Element-UI组件库
		        5.配置axios库
		        6.初始化git远程仓库	
		        7.将本地项目托管到github或者码云中

git全局设置：git config --global user.name "fire314"
	git config --global user.email "2194388731@qq.com"
创建 git 仓库：
mkdir vue-project
cd vue-project
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin https://gitee.com/fire314/vue-project.git
git push -u origin master
已有仓库：
cd existing_git_repo（cd到项目目录中）
git remote add origin https://gitee.com/fire314/vue-project.git
git push -u origin master

在后台server文件中安装依赖包：npm install
查看接口：node .\app.js

登录与退出功能：
登录业务流程：1.在登陆页面输入用户名和密码
	        2.调用后台接口进行验证
	        3.通过验证之后，根据后台的相应状态跳转到项目主页
登陆业务的相关技术点：1.http是无状态的
		       2.通过cookie在客户端记录状态
		       3.通过session在服务器端记录状态
		       4.通过token方式维持状态
尽量在每写一个功能的时候都创建一个分支
创建分支：git checkout -b 分支名
查看分支：git branch

3.登录/退出功能
3.1登录页面的布局
通过Element-UI组件实现布局：1.el-form
			  2.el-form-item
			  3.el-input
			  4.el-button
			  5.字体图标
路由导航守卫控制访问权限
如果用户没有登录，但是直接通过URL访问特定页面，需要重新导航到登陆页面
// 挂载路由导航守卫
router.beforeEach((to, from, next) => {
  // to 将要访问的路径
  // from 代表从哪个路径跳转而来
  // next 是一个函数，表示放行
  // 两种方式： next() 放行  next('/login') 强制跳转
  if (to.path === '/login') return next()
  // 获取token
  const tokenStr = window.sessionStorage.getItem('token')
  // 没有token强制跳转到登录页
  if (!tokenStr) return next('/login')
  next()
})
退出功能实现原理：销毁本地的token
// 清空token
window.sessionStorage.clear()
//跳转到登陆页面
this.$router.push("/login")

查看状态：git status
添加文件：git add .
提交代码： git commit -m "完成了登录功能"
将login分支上的代码合并到主分支master上
切换分支：git checkout master
查看分支：git branch
合并分支：git merge login
推送代码到云上：git push
推送一个新的分支到云上：git push -u origin login



主页布局
通过axios请求拦截器添加token，保证拥有获取数据的权限







vue框架的特点：更加轻量、渐进式框架、响应的更新机制、学习成本低。
Vue.component缺点：
1.全局定义：强调要求每个coponent中的命名不得重复
2.字符串模板：缺乏语法高亮，在HTML有多行的时候，需要用到丑陋的\
3.不支持CSS：HTML和JavaScript组件化的时候，CSS明显被遗漏
4.没有构建步骤：限制只能使用HTML和ES5，而不能使用预处理器



其他指令：
v-pre：不再解析{{}}中的内容，直接显示原文
v-cloak:等页面全部加载完才渲染
v-once：只渲染一次
扩展实例构造器：
var authorExtend=Vue.extend({
     templete: '',
     data:function(){
           return {
                prop1:'',
                prop2:''
           }
     }
});
Vue.set全局操作
mixins选项操作：全局混入比原生混入先执行
extends选项：只支持构造器里面的方法，且扩展智能放对象，不能放数组
delimiters选项：分隔符选项，是一个数组，更改插值表达式的分隔符



