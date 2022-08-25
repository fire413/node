# node.js #

## 简介 ##

### 介绍 ###

Node.js是一种建立在Google Chrome's v8 engine上的non-block(非阻塞）、event-driven(基于事件的）I/O平台。<br />
Node.js平台使用的开发语言是JavaScript，平台提供了操作系统低层的API，方便做服务器端编程，具体包括文件操作、进程操作、通信操作等系统模块。

### Node.js可以用来做什么？ ###

- 具有复杂逻辑的动态网站
- WebSocket服务器
- 命令行工具
- 带有图形界面的本地应用程序

### 终端的基本使用 ###

#### 打开应用 ####（需要管理员权限）

- notepad 打开记事本
- mspaint 打开画图
- calc 打开计算器
- write 写字板
- sysdm.cpl 打开环境变量设置窗口
- D: 切换到D盘
- cd 当前盘下的文件 进入到当前盘下的文件

#### 常用命令 ####

- md 创建目录
- rmdir(rd) 删除目录，目录内没有文档
- echo on a text 创建空文件
- del 删除文件
- rm 文件名 删除文件
- cat 文件名 查看文件内容
- cat>文件名 向文件中写上内容（Ctrl+C退出文件内容的输入）
- cat>>文件名 向文件中追加内容

### node.js开发环境准备 ###

1. 普通安装
2. 多版本安装<br />
   卸载已有的node.js<br />
   下载nvm（https://github.com/corebutler/nvm-windows）<br />
   在C盘下创建目录dev，在dev中创建两个子目录nvm和nodejs，并把nvm包解压进去<br />
   在install.cmd文件上面右键以管理员身份运行<br />
   打开的cmd窗口直接回车，会生成一个settings.txt文件，吸引该文件中的配置信息<br />
   配置nvm环境变量<br />
   NVM_HOME  对应nvm文件夹地址<br />
   配置node.js环境变量<br />
   NVM_SYMLINK  对应nodejs文件夹地址<br />
   把配置好的环境变量加到path中
   %NVM_HOME%;%NVM_SYMLINK%;<br />
   测试：cmd中输入nvm version命令，会输出nvm版本号

#### nvm常用命令 ####

- nvm list 查看当前安装的Node.js所有版本
- node -v 查看当前nvm的版本
- nvm install 版本号，安装指定版本的Node.js（latest为最新版本）
- nvm uninstall 版本号 卸载指定版本的Node.js
- nvm use 版本号 选择指定版本 的Node.js

#### Node.js之Hello World ####

- 命令行方式REPL（cmd中运行）<br />
  REPL： read-eval-print-loop 读取代码-执行-打印结果-循环过程<br />
  在REPL环境中，下划线'_'表示最后一次执行结果<br />
  .exit可退出REPL环境<br />
- 运行文件方式<br />
- 全局对象概览<br />
  安装插件：Terminal Ctrl+Shift+t直接进入该文件的cmd

## node模块化 ##

### 全局成员概述 ###

    console.log(__filename); //包含文件名称的全路径
    console.log(__dirname);//不包含文件名称的路径
    global.console.log("global");  //global相当于window
    console.log(process.argv);
     //argv是一个数组，默认情况下，前两项数据分别是：Node.js环境的路径;当前执行的js文件的全路径
    //从第三个参数开始表示命令行参数
    console.log(process.arch);  //打印当前系统的架构（x64)

### 关于路径问题 ###

1. 当前目录 ./
2. 父级目录 ../
3. 根目录  /

### 模块化开发 ###

传统非模块化开发有如下的缺点：<br />

1. 命名冲突<br />
2. 文件依赖<br />
   前端标准的模块化规范：<br />
3. AMD -requirejs<br />
4. CMD -seajs <br />
   服务器端的模块化规范：<br />
5. Commonjs -Node.js<br />
   模块化相关的规则：<br />
6. 如何定义模块：一个js文件就是一个模块，模块内部的成员都是相互独立的<br />
7. 模块成员的导出和引入<br />
   方式1：<br />
   //in.js文件
    function sum(a,b){
    	return a+b;
    }
    //导出成员模块
    exports.sum=sum;
   <br />
   //out.js文件
    //引入模块
    var module=require("./in.js");
    //console.log(module.sum(12,13));
   方式2：<br />
    //in.js文件
    module.exports=sum;
   <br />
    //out.js文件
   var module=require("./in.js");
    console.log(module(12,13));
   <br />
   方式3：<br />
    //in.js文件
    global.sum=sum;
   <br />
    //out.js文件
   var module=require("./in.js");
    console.log(sum(12,13));
   <br />
   模块文件的后缀3中情况：.js .json .node
   加载优先级：.js>.json>.node
   模块分类：

- 自定义模块
- 系统核心模块

1. fs文件操作
2. http网络操作
3. path路径操作
4. querystring查询参数解析
5. url url解析

## ES6 ##

- 变量声明let与const
- 变量的解构赋值
- 字符串扩展
- 函数扩展

### 变量声明let与const ###

let变量声明规则：<br />

1. let声明的变量不存在预解析<br />
2. let声名的变量不允许重复(在同一个作用域内)<br />
3. ES6引入了块级作用域(块内部定义的变量，在外部是访问不到的)<br />
   {...}也是块级作用域，for循环也是块级作用域<br />
4. 在块级作用于域内，变量只能先声明再使用<br />
   const用来声明常量,主要规则有：<br />
5. const声明的常量不允许重新赋值<br />
6. const声明的常量必须初始化<br />
   let适用场合：<br />
7. 在for循环中使用let生命<br />
8. let不存在变量<br />
9. 暂时性死区（只在块级作用域内起作用，会绑定此区域）<br />
   `var tmp=123;
   if(true){
   tmp='abc'; //ReferenceError
   let tmp;
   }`<br />
10. 不允许在相同的作用域内，重复声明一个变量<br />

### 变量的解构赋值

1. 数组的解构赋值
   `//let [a,b,c]=[1,2,3];
   //console.log(a,b,c);`
   为数组指定默认值
   `//let [a=111,b,c]=[,2,3];
   //console.log(a,b,c);`

2. 对象的解构赋值
   `let {foo,bar}={foo:'hello',bar:'world'};
   //console.log(foo,bar);`
   为对象指定默认值：
   `let {foo:'hi',bar}={bar:'world'};
   //console.log(foo,bar);`

3. 对象属性别名(如果有了别名，那么原来的名字就无效了)
   `let {foo:abc,bar}={foo:'hello',bar:'world'};
   //console.log(abc,bar);`


4. 给内置对象Math对象直接赋值
   `//let {cos,sin,random}=Math;
   //	console.log(typeof cos);
   //	console.log(typeof sin);
   //	console.log(typeof random);`


5.字符串的解构赋值
`let [a,b,c,d,e]="hello";
console.log(a,b,c,d,e); `

### 关于查看对象类型的方法复习 ###

### 字符串相关扩展 ###

1. includes() 判断字符串中是否包含指定的字符串（有的话返回true，没有返回false）
   参数1：匹配的字符串 参数二：从第几个开始匹配
    `console.log('hello world'.includes('world'));//true`
    `console.log('hello world'.includes('world',7));\\false`
2. startsWith()   判断字符串是否以特定的字符或着字符串开始
   `var url='admin/index.php';
   console.log(url.startsWith('admin'));\\true`
3. endsWith()	判断字符串是否以特定的字符或着字符串结束
   `console.log(url.endsWith('php'));\\true`
4. 模板字符串 反引号表示模板，模板中的内容可以通过${}方式填充数据
   ``let tpl=`<div>
   			<span>${obj.username}</span>
   			<span>${obj.age}</span>
   			<span>${obj.gender}</span>
   		</div>`;
   console.log(tpl);``

### 函数扩展 ###

1. 参数默认值
   `function foo2(param='nihao'){
   	console.log(param);
   }
   foo2('hello');//hello
   foo2();//nihao`
2. 参数解构赋值
   `function foo4({uname='aa',age=11}={}){
   	console.log(uname,age);
   }
   foo4();//aa 11
   foo4({uname:'bb',age:22});//bb 22`
3. rest（剩余）参数
   `function foo5(a,b,...param){
   	console.log(a); //1
   	console.log(b); //2
   	console.log(param);  //param是一个数组,[3,4,5]
   }
   foo5(1,2,3,4,5);`

4. ...扩展运算符
   `function foo6(a,b,c,d,e){
   	console.log(a+b+c+d+e);
   }
   let arr=[1,2,3,4,5];
   //foo6.apply(null,arr);
   foo6(...arr); //相当于foo6.apply(null,arr);`
5. 箭头函数<br />
   没有传参<br />
    `let func1=()=>console.log("hello");
    func1();`<br />
   传递一个参数<br />
    `let func2=v=>v;  //该语句解析为 function func2(v){ return v;}`<br />
   传递两个或者两个以上<br />
    `let func3=(a,b)=>a;`<br />
   匿名函数<br />
    `arr4.forEach((element,index)=>{
    	console.log(element,index);
    })`<br />
   箭头函数注意事项：

- 箭头函数中的this取决于函数的定义，而不是调用
- 箭头函数不可以new
- 箭头函数不可以使用arguments获取参数列表，可以使用rest参数代替

### 类与继承 ###

定义类：
	`class Animal{
		constructor(name) {  //构造函数
			this.name=name;
		}
		static showInfo(){  //静态方法，只能由类调用
			console.log("hi");
		}
		showName(){  //普通函数
			console.log(this.name);
		}
	}`
继承类
	`class Dog extends Animal{
		constructor(name,color){ 
			super(name);   //继承类的属性
			this.color=color;
		}
		showColor(){
			console.log(this.color);
		}
	}`

## node基本操作 ##

### Buffer基本操作 ###

Buffer对象是Node处理二进制数据的一个接口，它是Node原生提供的全局对象，可以直接使用，不需要require('buffer')。

- 实例化
  Buffer from(array)
  Buffer alloc(size)
- 功能方法
  Buffer isEncoding()  判断是否支持该编码
  Buffer isBuffer()	判断是否为Buffer
  Buffer byteLength()	返回指定编码的字节长度，默认utf8
  Buffer concat()	将一组Buffer对象合并为一个Buffer对象
- 实例方法
  write() 向Buffer对象中写入内容
  参数一：写入的内容，参数二：从第几个开始，参数三：写入几个字节
  slice() 截取新的buffer对象
  参数一：开始位置，参数二：结束位置
  toString() 把buffer对象专程字符串
  toJson() 把buffer对象转成json形式的字符串

### 核心模块API ###

#### 路径操作 ####

1. const path=require('path'); 访问路径模块<br />
2. path.basename()  获取路径的最后一部分<br />
3. __dirname  当前运行文件的全路径<br />
4. path.dirname(path)  返回当前路径的目录<br />
5. path.extname(path)  获取扩展名<br />
6. 路径格式化处理：<br />
   path.format() obj->string<br />
   path.parse() string->obj<br />
   {
     root: 'F:\\',  \\文件的根路径
     dir: 'F:\\myweb\\node', \\文件的全路径
     base: '核心模块.js', \\文件的名称
     ext: '.js',   \\扩展名
     name: '核心模块'  \\文件名
   }<br />
7. path.isAbsolute(path) 判断路径是否为绝对路径<br />
8. path.join(...paths)  拼接路径<br />
   注：
   '..'表示上层路径<br />
   '.'表示当前路径<br />
   在连接路径的时候，会格式化路径<br />
9. path.normalize(path)  规范化路径<br />
10. path.relative（from，to） 计算相对路径<br />
    注：
    第一个路径为绝对路径的时候，只在前面加该运行文件的盘符地址<br />
    当两个都为绝对路径的时候，取最后一个绝对路径，再加盘符地址<br />
    第一个路径为相对路径的时候，前面会加上当前运行文件的绝对路径<br />
11. 两个特殊的属性 路径分隔符<br />
    path.delimiter  ';'<br />
    path.sep  '\'<br />

#### 文件操作 ####

1. 引入文件模块 const fs=require('fs'); <br />
2. fs.stat(path,callback)   (异步)<br /> 
   一般回调函数的第一个参数时错误对象，如果err为null，表示没有错误，否则报错了<br />
   stat.isFile()  //判断该路径指的是否使文件<br />
   stat.idDirectory()  //判断该路径指的是否使目录<br />
    /*
    Stats {<br />
      dev: 1585448918,  包含文件的设备的数字标识符<br />
      mode: 33206, 描述文件类型的模型和模式的位域<br />
      nlink: 1, 文件存在的硬链接数<br />
      uid: 0, 拥有文件的用户的数字用户标识符（POSIX）<br />
      gid: 0, 拥有文件的组（POSIX）的数字组标识符。<br />
      rdev: 0, 如果文件被视为“特殊”文件，则为数字设备标识符。<br />
      blksize: 4096, I / O操作的文件系统块大小。<br />
      ino: 281474976994107, 文件的文件系统特定的“ Inode”编号。<br />
      size: 0, 文件大小，以字节为单位。<br />
      blocks: 0, 为此文件分配的块数。<br />
      atimeMs: 1574992282712.278,  指示最后一次访问此文件的时间戳（以毫秒为单位）自POSIX纪元以来。 <br />
      mtimeMs: 1574992282712.278,  指示此文件最后一次修改的时间戳，以自POSIX纪元以来的毫秒数表示。<br />
      ctimeMs: 1574992282712.278,  指示上一次更改文件状态的时间戳记以自POSIX纪元以来的毫秒数表示。<br />
      birthtimeMs: 1574992282712.278,  指示此文件创建时间的时间戳，以POSIX纪元为单位（以毫秒为单位）。<br />
      atime: 2019-11-29T01:51:22.712Z,  //文件访问时间<br />
      mtime: 2019-11-29T01:51:22.712Z,  //文件数据发生变化的时间<br />
      ctime: 2019-11-29T01:51:22.712Z,  //文件的状态信息发生变化的时间（比如文件的权限）<br />
      birthtime: 2019-11-29T01:51:22.712Z  //文件创建的时间<br />
    }
    */
3. fs.statSync(path) 返回Stats对象  （同步）<br />
   读取文件<br />
   异步读取文件<br />
4. fs.readFile(file,[option],callback)<br />
   如果有第二个参数并且是编码，那么回调函数获取到的数据就是字符串<br />
   如果没有第二个参数，那么得到的就是Buffer实例对象<br />
   //同步读取文件<br />
5. fs.readFileSync(file,[option])<br />
   写入文件<br />
   //回调函数只有一个参数err<br />
6. fs.writeFile（file，data [，options]，callback）  //异步<br />
7. fs.writeFileSync（file，data [，options]）  //同步<br />
   注意：多次操作会覆盖前面的内容

#### 文件流式操作 ####

用于处理大文件数据流。<br />
fs.createReadStream(path [，options]) 读取文件的数据流<br />
fs.createWriteStream(path [，options]) 写入文件的数据流<br />
//处理流的方式：基于事件的处理方式<br />
//'data' 固定名称，绑定事件的名称<br />
//'end' 固定名称，绑定事件名称<br />
//chunk表示块，一块数据，每次读取一块<br />
    `fs.createReadStream(path).on('data',(chunk)=>{
    	fs.createWriteStream(path).write(chunk);
    });`<br />
    `readStream.on('end',()=>{
    	console.log('文件处理完成');
    })`<br />
//fs.createReadStream(spath).pipe()  管道运输数据流<br />
//输入流 从磁盘加载到内存<br />
//输出流 从内存加载到磁盘<br />
fs.createReadStream(spath).pipe(fs.createWriteStream(dpath));<br />

#### 文件目录操作 ####

1. 创建目录<br />
   异步：fs.mkdir（path [，options]，callback）<br />
   同步：fs.mkdirSync（path [，options]）<br />
2. 读取目录<br />
   异步：fs.readdir(path[,options],callback)<br />
   同步: fs.readdirSync(path[,options])<br />
3. 删除目录<br />
   异步 fs.rmdir(path[,options],callback)<br />
   同步 fs.rmdir(path[,options])<br />

## 包管理工具 ##

多个模块形成包，不过要满足特定的规则才能形成规范的包

### npm(node.js package management) ###

全球最大的模块生态系统，里面所有的模块都是开源的，也是Node.js的包管理工具
[官方网站](https://www.npmjs.com )
npm常用的命令：<br />

1. 安装包：<br />
   npm install -g 包名称(全局安装)<br />
   npm install 包名称（本地安装）<br />
2. 安装包的时候指定版本<br />
   npm install -g 包名称@版本号<br />
3. 卸载包<br />
   npm uninstall -g 包名称<br />
4. 更新包（更新到最新版本）<br />
   npm update -g 包名称<br />

--save  向生产环境中添加依赖dependencies<br />
--save-dev 向开发环境中添加依赖devDependencies<br />