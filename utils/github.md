## git的相关命令
git init

git add filenames

git commit -m "describe"

git status

git diff filename

git log

git log --pretty=oneline  //减少日志的显示

git reset --hard HEAD^/HEAD^^/HEAD~100  指定回退到多少个版本

git reflog  查看历史版本号

git checkout --filename  撤销修改，丢弃工作区的修改（理解工作区与暂存区）

git clone url   克隆远程仓库的东西

git checkout -b dev  创建dev分支并且切换到dev分支，等价于git branch dev和git checkout dev

git checkout -d dev  删除分支

git branch 查看所有分支

git checkout master 切换到master分支

git merge dev 合并dev分支

git merge --no-ff -m "describe" dev 合并dev分支信息任然保存

git log --graph  查看分支合并图

git stash  存数工作现场，然后去修改bug再次返回

git stash list  查看现场

git stash pop  返回现场，等价于git stash apply + git stash drop

git branch -D name  强行删除一个从未被合并的分支

git tag v1.0  创建标签
> 多人协作开发：每个人建立不同的分支
* git push origin branchname  推送自己的修改
* 如果推送失败，git pull 视图合并(如果显示no tracking information)
则远程分支与本地分支没有建立联系，需要重新创建
git branch --set-upstream branch-name origin/branchname
* 如果有冲突，解决冲突，并且在本地提交
* 没有冲突或冲突已经解决，git puash origin branchname

参考连接： [https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000]()
## git常用命令
1. 将远程仓库的文件clone到本地：
```
git clone url(https)
```
2. 本地文件连接到远程仓库
```
cd folder
git init
git add .
git commit -m "备注信息" -a
//远程建立仓库，复制url
git remote add origin url
git push -u origin master
```
3.撤销操作
```
git add 后撤销
撤销所有的add文件： git reset HEAD .
撤销单个add文件: git reset HEAD -filename

git commit 后撤销
只回退commit的信息，保留修改代码: git reset --soft head
彻底回退到上次commit的版本，不保留修改代码git reset --hard head^
head : 当前版本
head^: 上一个版本
--hard 会抛弃当前工作区的修改
--soft 会回退到之前的版本，但是保留当前工作区的修改，可以重新提交

撤销所有本地改动代码
git checkout.

本地代码回退到与远程仓库保持一致
git reset --hard

git push撤销
回滚此次push到服务器的代码
git log查看commit的信息
git revert 以前commit的id
git push此时本地回滚的代码到服务器就可以了

git merge 撤销
git checkout
git reset --hard
```
4. git忽略而不提交文件的3种情况
- 从未提交过的文件可以使用.gitignore
```
//在.gitignore文件中添加忽略的文件夹或者文件，例如:log/文件夹
log/*
```
- 已经推送（push）过的文件，想从git远程仓库中删除，并在以后的提交中忽略，但是本地还是保留这个文件
```
git rm --cached Xml/config.xml
```
- 已经推送(push)过的文件，想在以后提交的时候忽略此文件，即使本地已经修改过，不删除远程仓库中对应的文件
```
git update-index --assume-unchanged Xml/config.xml
//如果要忽略一个目录
git update-index --assume-unchanged $(git ls-files | tr '\n' ' ')
```

### vim编辑器
vim -R file 查看文件只读

esc 常用的命令

:args 显示正在编辑的文件名称

:wq 保存并退出

:q!  强制退出

