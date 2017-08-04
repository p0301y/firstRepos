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