# git

## 安装

git官网：https://git-scm.com

## 最小配置

### 配置user信息

$git config --global user.name 'your name'

$git config --global user.email 'your email'

### config的三个作用域

$ git config --local    只对某个仓库有效

$ git config --global  对当前用户所有仓库有效

$ git config --system  对系统所有登录的用户有效

### 显示config的配置，加--list

$ git config --list--local 

$ git config --list--global

$ git config --list--system

## 建立git仓库

两种情况：

1.把已有的项目代码纳入git管理

$cd 项目代码所在的文件夹

$git init

2.新建的项目直接用Git管理

$cd 某个文件夹

$git init your_project  #会在当前路径下创建和项目名称同名的文件夹

$cd your_project

## 往仓库里添加文件



![image-20200910161832660](https://i.loli.net/2020/09/10/tCKqWvf6Ocl2AJ8.png)

## 文件重命名

传统：

1.$mv 原文件名 新文件名  ------------此时会删除原文件，新增新文件

2.$ git add 新文件名     -------------将新文件添加到暂存区

3.$git rm 原文件名   ------------------将原文件从git中删除

4.$git commit -m'提交新文件'    ---------------------提交文件

简便方法：

$git mv 原文件名  新文件名

$git commit  -m'提交新文件'    -------------------提交文件

## 命令行查看版本演变历史

$git log --oneline   查看简介列表

$git log -n2 --oneline  最近两次的提交

$git log --all   查看所有分支的提交历史

$git log --graph   图形化展示提交历史

$git log 分支名  查看指定分支的提交历史

## 图形界面查看版本演变历史

$gitk  ------------进入到图形化界面

## .git目录

![image-20200911162507157](https://i.loli.net/2020/09/11/IQZwGzELWjsOthy.png)

$cat 文件名   查看文件

$ls -al   查看文件夹下的目录

$git cat-file -t 对象哈希值序列    查看对象的类型

$git cat-file -p 对象哈希值序列    查看对象的内容

三大类型：commit blob tree

![image-20200911171954637](https://i.loli.net/2020/09/11/M9OegHhIj4wcmW6.png)

例子：

![image-20200914114854155](C:\Users\ZC\AppData\Roaming\Typora\typora-user-images\image-20200914114854155.png)

分离头指针时提交的commit没有与任何分支与tag挂钩，被视为不重要的commit，会被git当作垃圾清理掉

## 删除分支

$git branch -d 分支名  

## 修改commit的message

![image-20200915094256486](https://i.loli.net/2020/09/15/tyTWSJQiaVHD8u1.png)

### 修改最新的commit的message:

1.输入命令$git commit --amend，进入到vi编辑器界面，修改message信息

![image-20200915094937784](https://i.loli.net/2020/09/15/iRwN9TlHhcWjIsp.png)

2.保存退出vi编辑器，界面提示修改成功

![image-20200915095226025](https://i.loli.net/2020/09/15/keREHqy5IJvGxzD.png)

### 修改老旧的commit的message(变基操作):

1.输入命令$git rebase -i 被变的commit的父亲的哈希值，跳转界面，将需要修改的commit前面的pick修改成r，保存退出

![image-20200915100156261](https://i.loli.net/2020/09/15/qJyCsgK5HBGjMWO.png)

2.进入到另一个vi编辑器界面，修改对应的commit的message

![image-20200915100322701](https://i.loli.net/2020/09/15/A1rsLNVkWhX42J9.png)

3.保存退出vi编辑器，界面提示修改成功

![image-20200915100452509](https://i.loli.net/2020/09/15/bIrXhVlqQ6w1zSO.png)

### 连续几个commit合并成一个

1.输入命令$git rebase -i 被变的commit的祖宗的哈希值，进入到vi编辑器界面，在需要修改的commit前面的pick修改成s，保存退出（合并3636b0f、6c42411，这两个commit，基于3636b0f,所以3636b0f前面是pick）

![image-20200915103847359](https://i.loli.net/2020/09/15/y8RF4VBYsnzu3pf.png)

2.进入到另一个vi界面，添加message新信息，保存退出

![image-20200915104056321](https://i.loli.net/2020/09/15/73pX5dTKlutDCQ1.png)

3.修改成功

![image-20200915104213710](https://i.loli.net/2020/09/15/q7vXgnTK9Z4aoLt.png)

### 间隔几个commit合并成一个

1.输入命令$git rebase -i 被变的commit的祖宗的哈希值，进入到vi编辑器界面，将需要合并的commit放到一起，在需要修改的commit前面的pick修改成s，保存退出（合并4efa8d8a、ea7bc0689,这两个commit，基于ea7bc0689,所以ea7bc0689前面是pick,由于进入的vi界面只有前面两个commit，需要自己手动将ea7bc0689这个commit输入到界面）

![image-20200915105255440](https://i.loli.net/2020/09/15/AuxH2ZPOn1T7FUB.png)

2.跳出提示信息，通过$git rebase --continue命名，进入到另一个vi界面，添加message新信息，保存退出

![image-20200915105905516](https://i.loli.net/2020/09/15/pP3qorecKLCdzHh.png)

3.修改成功

![image-20200915110117879](https://i.loli.net/2020/09/15/gy75QTBJfN4eC6F.png)

撤回rebase操作：[https://blog.csdn.net/chengde6896383/article/details/83418488](https://blog.csdn.net/chengde6896383/article/details/83418488)

## 常见操作

### 暂存区与HEAD所有文件的差异

$git diff --cached   (--cached表示暂存区与HEAD之间所有文件的差异)

其中HEAD指向master，master指向最新的提交

### 工作区与暂存区所有文件的差异

$git diff    (默认时比较工作区与暂存区之间所有文件的差异)

$git diff -- 文件名   指比较指定文件在工作区和暂存区之间的差异

$git diff -- 文件名 文件名  ...   比较指定多个文件在工作区和暂存区之间的差异

### 暂存区恢复成HEAD

$ git reset HEAD

### 工作区文件恢复成暂存区的样子

git checkout -- 文件名    将工作区的该文件恢复成暂存区的文件

### 取消暂存区部分文件的更改

$ git reset HEAD --指定地撤销文件的文件路径

### 消除最近几次的提交

git reset --hard  要恢复到的commit的哈希值

### 查看不同提交的指定文件的差异

git diff 分支1 分支2 --指定文件

git diff 分支1的commit的哈希值 分支2的commit的哈希值 -- 指定文件

![image-20200924163454436](https://i.loli.net/2020/09/24/rAq9zmlKRJh1Cjw.png)

### 删除文件

$git rm 文件名 

在目录区删除文件夹 rm -rf 文件夹名称

### 临时加塞任务解决方案

git stash  将信息存放到stash中，将先任务搁置，进行临时任务

git stash list   查看stash中的信息

git stash apply       把存放在stash中的信息放出来，用git stash list命令查看前面存放信息还在

git stash pop 把存放在stash中的信息放出来，用git stash list命令查看前面存放信息不存在

![image-20200924170431207](https://i.loli.net/2020/09/24/tGpziISYcJdWZuk.png)

![image-20200924170534542](https://i.loli.net/2020/09/24/SHKOhJegixRvloV.png)

![image-20200924170619289](https://i.loli.net/2020/09/24/NSqQi2R7EC3wuKm.png)

### 指定不需要git管理的文件

vi .gitignore

在.gitignore文件中添加要忽视的文件名或者文件夹名，注意文件夹名称后面要带‘/’，表示忽视该文件夹下的所有文件

将git仓库备份到本地

常用的传输协议

| 常用协议       | 语法格式                                                     | 说明                     |
| -------------- | ------------------------------------------------------------ | ------------------------ |
| 本地协议（1）  | /path/to/repo.git                                            | 哑协议                   |
| 本地协议（2）  | file:///path/to/repo.git                                     | 智能协议                 |
| http/https协议 | http://git-server.com:port/path/to/repo.git  https://git-server.com:port/path/to/repo.git | 平时接触到的都是智能协议 |
| ssh协议        | user@git-server.com:path/to/repo.git                         | 工作中最常用的智能协议   |

哑协议与智能协议的区别

哑协议传输进度不可见，智能协议传输可见，哑协议比智能协议传输速度快。

克隆不在工作区的裸仓库

![image-20201108145621390](C:\Users\ZC\AppData\Roaming\Typora\typora-user-images\image-20201108145621390.png)

$git remote -v     查看当前配置有哪些远程仓库

$git remote zhineng（远程仓库名称，自定义） file:///f/git/beifen/zhineng.git    为当前配置添加远程仓库

$git push zhineng      将本地文件备份到远程仓库

$git push --set-upstream zhineng master

## 常见命令：

$pwd  当前工作路径

$clear 清屏

$cp 要拷贝的文件路径  目标文件夹路径    复制文件

$cp -r 要拷贝的文件夹路径  目标文件夹路径    复制文件夹

$git status   查看工作目录和暂存区

$git log  查看提交日志

$ls -al

$git add 一个或者多个文件夹或者文件

$git add -u  将发生更新的文件放到暂存区

$git commit -m'提交信息描述'     提交到仓库

$mkdir 文件夹名称     新建文件夹

$vi 文件名称   查看文件内容，退出时输入q

$mv 原文件名 新文件名

$git reset --hard   清除暂存区所有内容

$git branch -av    查看本地所有分支

$git checkout  分支名  切换分支

$find 文件夹路径 -type f   查看该路径下的所有文件

$git diff HEAD HEAD^1(HEAD的父亲，HEAD^^表示HEAD父亲的父亲，也可以这样表示：HEAD~2)    比较差异

新建文件的两种方式：

touch 文件名     ------------直接新建一个文件

vi 文件名   ------------------新建一个文件，并进入vi编辑界面，如果文件已经存在，则直接进入vi编辑界面

$git clean -df 文件夹名称   删除目录区的文件夹以及该文件夹下面的所有文件

$git clean -f 文件名称   删除目录区的文件



## **vi编辑器

常见命令：

| **Keystrokes** | **Result**                   |
| -------------- | ---------------------------- |
| ZZ             | 保存文件，退出               |
| :wq            | 保存文件，退出（和 ZZ 类似） |
| :q             | 退出。防止没有保存就退出。   |
| :q!            | 退出。无论保存与否，都退出。 |

 ![image-20200914173537640](https://i.loli.net/2020/09/14/yYwsnUK5PtlVcHp.png)

对事业部的建议与意见

对项目的优化

对页面的配置





