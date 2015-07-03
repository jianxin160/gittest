1.查看git
cat ~/.gitconfig

2.配置git(注意下面配置的用户名和密码是本地操作用户名、密码，跟github没有任何关系)
git config --global user.name
git config --global user.mail

3.查看常用命令(q退出查看)
git help <command>

4.给项目添加git版本库（本地版本库,add后面的点代表当前目录所有文件）【这一步就相当于XCode创建项目时选择了创建本地git仓库】
git init
git add .
git commit -m "init"

5.提交项目到github(连接github有两种方式：https或者ssh，后者需要秘钥)
github创建项目：
a.要将项目放到github可以在github创建一个项目然后将本地仓库传入github；
b.直接连接github直接创建仓库并提交；
c.直接在github上使用导入代码功能
这里直接使用第一种方式(到github上登录查看https地址，执行如下命令后输入github的用户名密码即可)
git remote add origin https://github.com/jianxin160/gittest.git
git push -u origin master

6.查看提交日志
git log <file>

--7.更新到最新版本
--git pull

8.查看当前状态（可以先修改几个文件并添加几个文件）
git status

9.查看修改文件的差异
git diff <file>

9-1.添加（由于前面除了修改几个文件还添加了几个文件）
9-1git add .

11.提交
git commit -m "add TableViewController and modify ViewController"

12.推送到远程服务器（github）
git push

13.取消文件修改（可以修改一个文件，例如TMTableViewController.m）
git checkout —-git/TMTableViewController.m

14.
