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

10.快照（每次提交必须快照，建议使用git stage .而不是使用过期的git add .,commit只会提交快照内容，如果快照后做了修改，commit不会提交）[注意git stage是git add的新版本，不建议使用git add]
git stage .

11.提交(其实是提交到本地仓库，注意在提交之前必须先进行快照git stage)
git commit -m "add TableViewController and modify ViewController"

12.推送到远程服务器（github）
git push

13.取消文件修改（还没有stage或者还没有commit，撤销未提交的修改）（可以修改一个文件，例如TMTableViewController.m，可以做git stage,也可以不做git stage，但是不能做commit）
git reset --hard HEAD


14.取消文件修改,恢复到上次stage（撤销stage未提交的修改）（可以修改一个文件，例如TMTableViewController.m，然后做git stage,但是不能做commit，并且stage如果指定了某个文件，那么checkout必须是某个文件）
git checkout —-git/TMTableViewController.m

15.取消文件修改，恢复到上一次commit（撤销commit后的修改）（可以修改一个文件，例如TMTableViewController.m，然后做git stage,做git commit，下面的命令将恢复到最近一次提交，上上次的使用git revert HEAD^）
git revert HEAD

16.创建并切换分支(下面创建了一个dev分支并切换到dev分支中，下面的命令等于git branch dev[创建分支]和git checkout dev[切换分支]两句)
git checkout -b dev

17.查看分支(本地分支，可以使用git branch -r查看远程分支情况)
git branch

18.推送分支到远程服务器（在此之前可以修改一部分内容提交，由于第一次推送此分支需要加上相应参数-u origin dev）
git push -u origin dev

19.合并分支（例如在dev分支修改了TMTableViewController.m并且提交、推送到远程服务器;切换会master时如果有没有提交的修改可以暂存，使用git stash）[下面的命令执行之后可以git push推送到远程服务器]
git merge dev

20.删除分支dev（从本地仓库）
git branch -d dev

21.删除远程分支（类似的删除远程tag git push origin —tag <tagname>）[其实也可以推送一个空分支，就相当于删除远程分支 git push origin:dev]
git push origin --delete dev

22.获取远程分支（例如本地已删除但是没有删除远程分支，下面第二句命令第一dev是本地分支名称，第二个是远程分支名称，通过命令进行映射，这样查看就会发现本地多了一个dev分支）
git fetch origin dev
git checkout -b dev origin/dev

23.从远程分支克隆文件到本地(下面的命令是克隆每个分支到本地，如果不加参数-b dev就是克隆主分支到本地,一般会在主分支文件夹再创建一个文件夹作为分支文件)[注意运行下面的命令之前先在一个文件夹做初始化，不要放到主分支文件夹内，cd到新建文件夹在执行如下命令]
git init
git add .
git commit
git clone -b dev https://github.com/jianxin160/gittest.git

24.提交分支修改并推送到远程（注意cd到分支下再提交、推送）
git stage .
git commit -m “modify tableViewController.m”
git push

25.合并分支并提交（先cd到主分支目录下）
git checkout master
git pull
git merge dev
git push

26.衍合（前面使用了合并merge，其实合并还能使用衍合，区别就是合并是确实产生了合并后的新版本，衍合没有产生新节点只是会以补丁形式存在，二者选择原则：变化较多使用merge，只需要解决一次冲突；变化较少使用rebase需要多次解决冲突，但是合并是线性的比较整洁）【下面的例子可以先在两个分支master和dev上分别修改123.rtf，并且分别提交、推送，再到dev分支下执行rebase，如果发生冲突需求修改冲突然后git add 123.rtf 最好执行git rebase —-continue和git rebase —-skip跳过】
git rebase origin/master

27.合并master（再次到master，执行合并）
git merge dev

28.解决冲突(发生冲突后只要修改对应文件删除<<<等然后正常提交、推送即可)
git add 123.rtf
git commit -m “modify 123.rtf”
git push







