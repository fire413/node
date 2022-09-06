1.首先在项目目录下初始化本地仓库

git init

2.添加所有文件( . 表示所有)

git add .

3.提交所有文件到本地仓库

git commit -m "备注信息"

4.连接到远程仓库

git remote add origin 你的远程仓库地址

5.将项目推送到远程仓库

git push -u origin master

![img](https:////upload-images.jianshu.io/upload_images/4753754-4a1c79b7d85d2b59.png?imageMogr2/auto-orient/strip|imageView2/2/w/604/format/webp)

如果出现这个错误可能是因为远程仓库的[README.md](https://link.jianshu.com?t=http://git.oschina.net/zzjian/location/blob/master/README.md?dir=0&filepath=README.md&oid=366e9135cf3a1bd73be8b473367e28c4b4424092&sha=c8b0c591cae09abfd3b487f7e66722113cc66a89)文件没有pull到本地仓库而导致的冲突

输入git pull --rebase origin master 将文件拉到本地后重新输入步骤5即可解决。
来源链接：https://www.jianshu.com/p/2a8b4e627991