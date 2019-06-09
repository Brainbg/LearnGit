# Git学习

## 用Git上传项目到GitHub


## 准备环境

### Git客户端
https://gitforwindows.org/

### 配置SSH
```
1、查看个人用户的.ssh目录下有没有id_rsa和id_rsa.pub这两个文件，如果没有，则用下面的命令创建

 ssh-keygen -t rsa -C "email" //生成新的SSH秘钥，注意C必须为大写的才有效，后续要求输入密码，直接两个`Enter`键 即可,毕竟日常使用不需要这么麻烦。

2、登录GitHub，打开Settings>SSH and GPG keys>New SSH key，填上任意Title，在Key文本框里
   粘贴 id_rsa.pub 文件的内容（用记事本打开即可）。

```


### 调出git命令窗口
例如我们现在要上传一个名为MyGit的项目

### 1、在GitHub上创建一个名为MyGit的库
![](https://brian-1258565516.cos.ap-guangzhou.myqcloud.com/img/create_new.png)

### 2、 在MyGit的文件目录下,右击，选择Git Bash here，输入git init 进行初始化

```
git init
```
![](https://brian-1258565516.cos.ap-guangzhou.myqcloud.com/img/git_init.png)
### 3、配置GitHub的用户名和邮箱,告诉它，你是谁
```
查看
git config user.name
git config user.email

修改
git config --global user.name "Brainbg"
git config --global user.email "1057234389@qq.com"
```
##### 如果你跳过了这一步，可能就会这么提示
![](https://brian-1258565516.cos.ap-guangzhou.myqcloud.com/img/add_userName_Email.png)
### 4、添加文件

```
添加所有文件
git add .

添加单文件
git add <file> 
如：git add "README.md"
```

### 5、提交
```
git commit -m <message> //提交文件
如：git commit -m "第一次提交"
```
### 6、连接远程地址
```
git remote add origin "远程库地址"   

双引号可以省略
比如： git remote add origin "https://github.com/Brain-RD/MyGit.git"
或 git remote add origin https://github.com/Brain-RD/MyGit.git
```

### 7、推送上仓库
 ```
 git push -u origin master
 ```
 
### 8、输入账号密码
![](https://brian-1258565516.cos.ap-guangzhou.myqcloud.com/img/username.png)
![](https://brian-1258565516.cos.ap-guangzhou.myqcloud.com/img/enter_password.png)

### gitignore文件






## Git常用命令
```
注：<file> 表示一个文件 ，如 README.md

ctrl + L //清屏
ctrl + c //中断
```
### 创建版本库
```
git init 初始化版本库
git clone "远程库地址"  //克隆库到本地
```

### 查看状态
```
git status  //查看当前状态
git diff 
```


### 增删改查
```


git help <command>  //显示command的help,如：git help push
git show //显示已提交的信息
git add . //添加所有文件
git add <file> //添加单文件


```

### 查看log
```
git log //显示从最近到最远的提交日志
git log --pretty=oneline //显示commit id全部id的提交日志
git log --oneline //显示commit id前7位的提交日志
git log <file> //
git log -p <file> //
git log -p -2 //查看最近两次详细修改内容的diff
git log --stat #查看提交统计信息
```
### 版本回退
```
git reset --hard HEAD^  //回退到上一个版本 
git reset --hard <commit_id> //回到指定的版本(版本号没必要写全，前几位即可)
git reflog  //查看历史记录的版本号id（记录你的每一次命令,不论是否已经提交,都可用来进行版本回退时，查看版本号）
git status //当前状态
```
* HEAD指向的版本就是当前版本，因此Git允许我们重新指定所有已提交的版本中的一个，使用命令git reset --hard commit_id。

* 想要回退到哪个版本，可用git log查看提交历史。

* 想要回到未来的哪个版本来，可用git reflog查看命令历史。



### 对比
```
git diff //是工作区(work dict)和暂存区(stage)的比较
git diff --cached //是暂存区(stage)和分支(master)的比较
git diff HEAD -- README.md //查看工作区和版本库里面最新版本的区别
```
### 撤销修改
```
git checkout -- <file> //把文件在工作区的修改全部撤销,让这个文件回到最近一次git commit或git add时的状态。
git reset HEAD <file> //把暂存区的修改撤销掉，重新放回工作区(该文件被 git add 后，可如此撤销，再用git checkout撤销工作区的修改)
```
### 删除
```
git rm <file> //删除文件
git checkout -- <file> //误删的文件恢复到最新版本,该命令是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
```
### 创建与合并分支
```
git branch //查看分支
git branch <name> // 创建分支
git checkout <name> //切换分支
git checkout -b <name> //创建+切换分支
git merge <name>  //合并某分支到当前分支(注意是当前分支，如果分支不对会出现其他问题)
git branch -d <name> //删除分支
git branch -D <name> //强制删除还没合并的分支

```

### 远程分支
```
git fetch origin dev（dev为远程仓库的分支名）：原有主分支，不成功

git pull origin dev(远程分支名称)：会直接与本地分支合并

git push --set-upstream origin 分支名


git checkout -b <local-branch> origin/<branch>：从远程仓库里拉取一条本地不存在的名为`MVP`的分支时
例：git checkout -b MVP origin/MVP

git clone -b <branch> <url>：拉取一条分支到本地，本地为空项目
例：git clone -b MVP git@github.com:Brainbg/LearnAndroid.git

git branch -m old_branch new_branch 将本地分支进行改名

git push origin -d <branch> 删除远程分支
例：git push origin -d LearnGraphics

git push origin  <branch> 推送分支到远程
例：git push origin Graphics

```

### 解决冲突
```
git log --graph  //查看分支合并图。
git log --graph --pretty=oneline --abbrev-commit //美观地展示分支合并的提交图

git merge --no-ff -m "message" dev //合并某分支到当前分支，并生成新的commit
//合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

```
### Bug分支
```
git stash //暂存工作区
git stash list //查看储存列表
git stash apply //恢复储存
git stash apply stash@{index} //恢复指定的stash

git stash drop //默认删除stash@{0}的stash
git stash drop stash@{index}//删除指定的stash

git stash pop //恢复储存同时把储存删除掉

git stash clear // 清空所有stash
```

### 多人协作
```
git remote //查看远程版本库
git remote -v //更详细查看远程版本库

git push origin master //推送主分支到远程库，需要指定分支
如：git push origin dev

git pull //拉取远程库到本地

git branch --set-upstream-to=origin/<branch> dev //创建本地dev分支与远程origin/分支的链接关系

```
### 变基
```
git rebase //变基，rebase操作可以把本地未push的分叉提交历史整理成直线
```
### 标签
```
git tag <name> //创建一个新标签，默认标签是打在最新提交的commit上的
git tag //查看所有标签
git tag <name> <commit_id> //给任意一个提交打上标签
git show <tagname> // 查看标签信息
git tag -a <tagname> -m <message> <commit_id> //打上标签并且写上说明
git tag -d <tagname> //删除标签
git push origin <tagname> //推送标签到远程库
git push origin --tags //一次性推送全部尚未推送到远程的本地标签
git push origin :refs/tags/<tagname> //删除远程库里的标签
```
### 远程库
```
git remote add origin <url> 
git remote rm origin //删除远程库

//同项目及关联多个远程库
git remote add github <url> //关联Github的远程库，取名github
git remote add gitee <url> //关联码云的远程库，gitee
//同项目推送多个远程库
git push github master
git push gitee master

//强制推送
git push --force
git push --force-with-lease
```




### 参考资料
[Git廖雪峰](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)  
[从远程仓库获取所有分支](https://blog.csdn.net/wu1169668869/article/details/83345633)


