# git常用指令
## 创建版本库
设置用户：
```git
$ git conig --global user.name "Your Name"
$ git config --global user.email "email@example.com"

 mkdir learngit #创建文件夹
cd #进入文件夹  
cd ..\   #返回上一级目录
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
![aa](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)  
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
git restore <file> #误删后恢复到版本库最新版
```  
## 远程仓库
### 添加远程仓库
```
git remote add origin git@github.com:Whiteclooud/learngit.git  #在本地关联远程库  
git push -u origin master   #第一次推送加-u(会把本地与远程的分支关联起来)，以后推送可省略  
```
### 删除远程仓库
先查看远程库信息
```git remote -v```  
再根据名字删除
```git remote rm origin```  
### 根据远程仓库克隆  
```git clone git@github.com:Whiteclooud/gitskills.git #克隆一个本地仓库```   

## 分支管理  
### 创建与合并分支  
#### 分支概念
一开始，master分支是一条直线，git用master指向最新提交，用head指向master。这样就能确定当前分支以及当前分支的提交点。  
![aa](https://www.liaoxuefeng.com/files/attachments/919022325462368/0)  
当创建新分支例如`dev`时，指向`master`相同的提交，再把`head`指向`dev`，就表示当前分支再`dev`上。  
![aa](https://www.liaoxuefeng.com/files/attachments/919022363210080/l)  
从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指针不变：  
![aa](https://www.liaoxuefeng.com/files/attachments/919022387118368/l)  
假如我们在dev上的工作完成了，就可以把dev合并到master上。Git怎么合并呢？最简单的方法，就是直接把master指向dev的当前提交，就完成了合并：  
![aa](https://www.liaoxuefeng.com/files/attachments/919022412005504/0)  
合并完分支后，甚至可以删除dev分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条master分支：  
！[aa](https://www.liaoxuefeng.com/files/attachments/919022479428512/0)
#### 指令

```
#创建并切换
git checkout -b dev
#相当于
git branch dev
git checkout dev
#更科学的指令
git switch -c dev  #创建并切换
git switch master  #切换到已有的
git branch -d <name>  #删除分支

git branch      #查看当前分支
git merge dev   #合成分支
```  
### 解决冲突  
当2个分支内容不一致时，合并分支就会产生冲突，必须手动处理解决冲突后再提交。
master和featre1有冲突时，变成这样：  
![aa](https://www.liaoxuefeng.com/files/attachments/919023000423040/0)  
解冲突后，变成了这样：  
![aa](https://www.liaoxuefeng.com/files/attachments/919023031831104/0)
```git status```可以告诉我们冲突的文件。  
```git log --graph```查看分支合并图  

### 分支管理策略    
在合并分支时，git默认使用```fast forward```模式：删除分支后会丢掉分支信息。  
```git merge --no--ff dev```禁用ff模式：在合并时会生成一个新的commit,这样在分支历史中可以查看分支信息。  
合并后像这样：  
![aa](https://www.liaoxuefeng.com/files/attachments/919023225142304/0)  
用```fast forward```合并就看不出来曾经做过合并，```--no--ff```合并后有历史分支，能看出来曾经做过合并。  
**分支策略**  
在实际开发中，我们应按照几个基本原则进行分支管理:
首先，```master```分支要非常稳定，仅用于发布新版本，平时不能在上面干活；  
干活都在```dev```分支上，所以```dev```分支是不稳定的，要发布新版本时将```dev```合并到```master```上再在```master```上发布。  

### bug分支  
```git stash```：将当前的工作区的文件‘储藏起来’,等以后回复现场后再继续工作。  
当有bug，且当前任务没完成时，可用```git stash```暂时储藏文件，此时用```git status```查看工作区就是干干净净的，可以创建分支来修复bug。从哪个分支上修复bug就在哪创建临时分支。