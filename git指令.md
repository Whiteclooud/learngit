# git常用指令
## 创建仓库
设置用户：
'''git
$ git conig --global user.name "Your Name"
$ git config --global user.email "email@example.com"
'''
' mkdir learngit #创建文件夹'
'cd #进入文件夹'
'git init #将这个目录变成git可以管理的仓库'
'git add ***  #把文件添加到仓库'
'git commit -m"本次提交的说明"  #把文件提交到仓库'
添加文件到Git仓库，分两步：
1. 使用命令git add <file>，注意，可反复多次使用，添加多个文件；
2. 使用命令git commit -m <message>，完成。