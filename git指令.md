# git常用指令
## 创建版本库
设置用户：
```git
$ git conig --global user.name "Your Name"
$ git config --global user.email "email@example.com"

 mkdir learngit #创建文件夹
cd #进入文件夹`
git init                      #将这个目录变成git可以管理的仓库
git add ***                   #把文件添加到仓库
git commit -m"本次提交的说明"  #把文件提交到仓库
```
添加文件到Git仓库，分两步：
1. 使用命令git add <file>，注意，可反复多次使用，添加多个文件；
2. 使用命令git commit -m <message>，完成。

## 时光机穿梭
```
git status  #查看仓库状态
git diff    #查看修改了什么内容
```
### 版本回退
```
git log [--pretty=oneline]  #显示从最近到最远的提交日志，以便确定要回退到哪个版本
#head指向的版本就是当前版本
git reset --hard commit_id  #回退到commit--id这个版本
#HEAD^为回退到上一个版本
#HEAD^^为回退到上上个版本
cat 文件名  #查看文件内容  
git reflog #记录每一次命令，可用于恢复到新版  
```
### 工作区和暂存区
![aa](0.png)
我们把文件往Git版本库里添加的时候，是分两步执行的：
第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区(stage)；
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。
你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。
### 撤销和修改
1.未使用 git add
```git restore -- readme.txt```
命令git restore -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。
2.使用 git add
```git restore --staged readme.md #使用后回到场景1，再按1操作```
3.使用 git commit
版本回退，前提是没有提交到远程仓库
### 删除文件
从版本库中删除文件
```rm test.txt      #删除文件
git rm test.txt  #add删除操作
git commit -m""  #提交删除`
git restore <file> #误删后恢复到版本库最新版本```
