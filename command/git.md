### 时光穿梭机
```shell
git status
git add .
git add <file>
git commit -m <comment>

git rm <file> //使用git删除文件,(可以使用下面的 git restore <file> 恢复)
git rm --cached <file>   //删除已经加入版本控制的文件

git diff <file>    //比较不同
git diff HEAD -- <file> //查看工作区和版本库里面最新版本的区别

git log --pretty=oneline   //一行打印log

git reset --hard HEAD^  //回到上一个版本
git reset --hard HEAD^^ //回到上二个版本
git reflog  //查看提交的版本号
git reset --hard 1103dd6  //回到对应的版本号

git restore <file>  //丢弃当前的更改
git checkout -- <file>  //丢弃当前的更改,没有--就变成了 '切换到另一个分支' 的命令

git reset HEAD <file>   //把暂存区的修改撤销掉,重新放回工作区
```

### 远程仓库
```shell
git remote add origin git@github.com:lwd45/LearnGit.git //关联远程仓库,远程仓库在本地的名字是origin

git push -u origin master   //将本地master分支推送到远程
//由于远程库是空的,我们第一次推送master分支时,加上了-u参数
//Git不但会把本地的master分支内容推送的远程新的master分支
//还会把本地的master分支和远程的master分支关联起来
//在以后的推送或者拉取时就可以简化命令
git push origin master  //把本地master分支的最新修改推送至远程

git remote -v   //查看与远程库建立的关系
git remote rm <origin>  //解除了本地和远程的绑定关系
```

### 分支管理
```shell
git switch <dev>   //切换分支
git checkout <dev>    //切换分支
git switch -c <dev>   //切换分支,没有就创建
git checkout -b <dev>   //切换分支,没有就创建
//-b相当于以下两条命令 git branch dev    git checkout dev
git switch -c <dev> origin/<dev>  //切换分支,没有就创建,并且和远程对应的分支关联

git branch  //查看本地所有分支
git branch -a   //查看本地和远程所有分支
git merge <dev>   //将 dev 分支合并到 '当前所在' 的分支
git branch -d <dev> //删除 dev 分支

git log --graph --pretty=oneline --abbrev-commit  //图像的方式查看分支

git merge --no-ff -m "merge with no-ff" dev   //禁用Fast forward模式合并
// --no-ff参数,表示禁用Fast forward
// 因为本次合并要创建一个新的commit, 所以加上-m参数

git stash   //把当前工作现场储藏起来,等以后恢复现场后继续工作
git stash list    //查看stash list
git stash apply <stash@{0}>  //恢复stash,但是stash内容并不删除
git stash drop    //删除stash
git stash pop   //恢复的同时把stash内容也删了

git cherry-pick <4c805e2>   //复制一个特定的提交到当前分支,只复制该提交的修改

git branch -D <dev>    //强行删除分支,丢弃一个没有被合并过的分支

git remote    //查看远程库的信息
git remote -v    //查看远程库,显示更详细的信息

git push origin <branch-name>    //把本地该分支上的所有本地提交推送到远程库,推送失败可以先pull拉取
git push origin //如果当前分支和远程分支建立了联系,可以直接推送到远程,推送失败可以先pull拉取

git branch --set-upstream-to=origin/<远程dev> <本地dev>   //将本地分支与远程分支建立联系
git pull    //拉取远程最新代码到本地,如果合并有冲突,需要手动解决
```

### tag管理
```shell
git tag           //查看所有标签
git tag <name>    //当前分支打一个新标签
git tag <tagName> <commitID:f52c633>  //给之前的一个提交打上标签
git show <tagname>        // 查看标签信息
git tag -a <tagname> -m <"version 0.1 released"> 1094adb   //打标签并附上说明, -a指定标签名, -m指定说明文字
git tag -d <tagname>   //删除标签
git push origin <tagname>   //将标签推送到远程
git push origin --tags      //一次性推送全部尚未推送到远程的本地标签

//要删除远程标签需要先本地删除再远程删除
git tag -d <tagname>
git push origin :refs/tags/<tagname>
```

### git rebase
```shell
git rebase <master> //以master为基准, 当前分支所有提交都会处于master最新的后面
git rebase -i <master_id> // 将当前分支所有提交合并成一个提交（保留第一个不变后面的都squash）
git push --forse //更新远程分支，将远程分支也压缩成一个提交
```

### other(配置文件都在 `.git/config` 里面)
```shell
git config --global alias.st status //设置别名 st 表示 status
git config --global alias.unstage 'reset HEAD'  //设置别名 unstage 表示  reset HEAD
```