安装node npm express express-generation
创建项目：pxpress 项目名称
初始化：npm install
在bin目录下的www.js中复制：(app.js中就不通用暴露出去了)
var http=require('http');
var server=http.createServer(app);
server.losten(port);
运行node app.js
安装mysql:npm install mysql --save
创建数据库以及表
创建util文件夹，在其目录下创建dbconfig.js文件（用于连接数据库）：
const mysql =require('mysql')
module.exports= {
// 数据库配置
const config = {
	host:'localhost',
	port: '3306',
	user:'root',
	passwprd:'root',
	database:'db'
	}
// 链接数据库，使用mysql连接池的方式
sqlConnect:function(sql,aqlArr,callback){
var pool=mysql.createPool(this.config)
pool.getConnection(（err,conn）=>{
if(err){
console.log('连接失败')
return;
}
//事件驱动回调
conn.query(sql,sqlArr,callBack);
// 释放连接
conn.release();
})
}

在router文件夹下的index.js中添加：
var dbconfig=require('地址')
var sql='select * from cate';
var sqlArr=[];
var callBack=(err,data)=>{
if(err){
console.log("连接出错了")；
}else{
res.send({
'list':data
})
}
}


热启动：
安装npm install nodemon -g