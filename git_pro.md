#git pro 笔记
######Git 保存的不是文件差异或者变化量，而只是一系列文件快照。Git 中的分支，其实本质上仅仅是个指向 commit 对象的可变指针，

 >## git br 
 > * 仅仅是建立了一个新的分支，但不会自动切换到这个分支中去
 > * 如果要切换到其他分支，需要git checkout test,这样 HEAD 就指向了test分支
 > * git checkout -b test：创建分支test并且切换到分支test上去
 
 >##git diff
 > * git diff --staged 
 > 	已经暂存起来的文件和上次提交时的快照之间的差异
 > * 单单 git diff 不过是显示还没有暂存起来的改动
 
 >## git commit
 > * git commit -a -m
 >   Git会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add，但是注意：若文件没有跟踪过，则不会一起提交。
 >	git add 过的文件，即为跟踪后的文件
 
 >## 移除文件
 > * git rm 从暂存区域移除并且从工作区中删除
 > * git rm --cached  仅从暂存区域移除,不会把工作区的也删了，如：误提交了一个文件a.log，可以用git rm --cached a.log
 
 >## 撤销修改
 > * git commit --amend 
 > 	如果提交了，但是发现有修改的文件忘提交，些时可以用git commit --amend，它会把本次提交合到上一次，但是注意：如果已经推送到远程要慎用。
 > * 撤销暂存区的修改： git reset HEAD 
 > * 撤销未暂存文件的修改： git checkout -- filename ， git checkout . 会把所以文件都撤销
 
 >## 远程分支
 > * git remote -v 查看远程分支
 > * git remote show origin 某个远程仓库的详细信息
 > * git remote rename pb paul 修改远程分支的名字，将pb 改成 paul
 > * git fetch 只是将远端的数据拉到本地仓库，并不自动合并到当前工作分支
 > * git pull 自动抓取数据下来，然后将远端分支自动合并到本地仓库中当前分支
 > * git push [远程名] [本地分支]:[远程分支] 将本地分支推送到远程分支
 > * git push [远程名] :[远程分支] 删除远程分支
 
 >## tag
 > * git tag -l 显示当前的tag list
 > * git show v1.1 显示某一tag的详细信息
 > * git tag -a v1.2 -m 'test' 添加标签
 > * git push origin v1.2 将v1.2推送到远程（注：git push并不会把标签也推送出去）
 > * git push origin --tags 将本地所有标签推送到远程
 
 >##分支合并
 > * git merge 
 > 合并后，会重新做一个新的快照，并自动创建一个指向它的提交对象，这个提交对象它有两个祖先
 > * 注意遇到冲突时，解决后，git add 将未merge的文件加到暂存区，然后提交
 
 >## git rebase
  > * git rebase 会打乱历史，使历史显示成一条链，更美观 
  >> 1、git co test 先切到功能分支
 >> 2、git rebase master 然后衍合master
 >> 3、git co master 然后回到主分支
 >> 4、git merge test 然后快速合并功能分支，即完成了rebase
  
## 一旦分支中的提交对象发布到公共仓库，就千万不要对该分支进行rebase操作。
>在进行衍合的时候，实际上抛弃了一些现存的提交对象而创造了一些类似但不同的新的提交对象。如果你把原来分支中的提交对象发布出去，并且其他人更新下载后在其基础上开展工作，而稍后你又用 git rebase 抛弃这些提交对象，把新的重演后的提交对象发布出去的话，你的合作者就不得不重新合并他们的工作，这样当你再次从他们那里获取内容时，提交历史就会变得一团糟。


 >## git merge 快速合并，不会打乱历史
 >> 1、git co master 切到主分支
 >> 2、git merge test 快速合并，将功能分支合到master
 
 -------------------------------------------
 
 
 > * ### 服务器上的git协议
 > * ssh协议是拥有对网络仓库的读写权限
 
 --------------------------------------
 
 ### git 工具
 
 > * git reflog  查看引用日志(在你工作的同时，Git 在后台的工作之一就是保存一份引用日志——一份记录最近几个月你的 HEAD 和分支引用的日志)
 
 > * git show HEAD 查看当前提交，等价于git show HEAD~0
 > * git show HEAD^，等价于git show HEAD~1
 
 ### git stash
 > * 储藏你的工作
 > * git stash
 > * git stash list
 > * git stash pop
 
 ### filter-branch 这个会大面积地修改你的历史
>  git filter-branch --tree-filter 'rm -f passwords.txt' HEAD
>  你会在所有快照中删除一个名叫 password.txt 的文件，无论它是否存在
 
 
 ### git blame
 > 当你在追踪代码中的缺陷想知道这是什么时候为什么被引进来的，用这个命令
 
 
 
 
 
 
 
 
