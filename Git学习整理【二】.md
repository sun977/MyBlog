# Git学习整理【二】

### 分支管理

git中master是默认主分支，一般比较稳定。git鼓励使用分支，充分利用git的分支功能，可以极大地提高工作效率。

##### 1）创建分支

```
$ git branch branch-name  //创建某分支
$ git branch -d branch-name  //删除某分支
$ git branch  //查看所有分支【*为当前工作分支】
$ git checkout branch-name  //切换到某个分支上
$ git checkout -b branch-name  //创建并切换到某个分支上
$ git merge branch-name  //合并某分支到当前分支
$ git merge dev //在master分支上操作，意思是合并dev分支到master上.
版本改进：
$ git switch branch-name  //创建分支
$ git switch -c branch-name  //创建并切换到该分支
12345678910
```

##### 2）分支冲突

假设有两个分支：master和dev分支，master上不做任何操作，在dev上修改，完了之后直接到master上合并dev即可，这种合并模式叫Fast-forward。但是如果master和dev同时对一个文件进行了修改，且他们的修改不一样，这时在合并master和dev的时候就会出现冲突。我们查看这个文件，git会用<<<<<<<，  =======，>>>>>>>>>来区分不同的修改是属于哪个分支上，这时需要我们手动选择我们想要的一种修改，然后提交。

```
$ git log --graph --pretty=oneline --abbrev-commit   //查看分支合并情况
$ git log --graph  //可以看到分支合并图
12
```

##### 3）分支管理策略

```
$ git merge --no-ff -m "merge with no-ff" dev  // 合并的时候禁用fast-forward模式
为什么要这样？原因如下：
1、fast-forward模式下合并，删除分支后，会丢掉被合并分支的信息。
2、只有禁用了ff，后面git log的时候才能看到文件曾经做了哪些修改。
团队中如何利用分支功能？建议如下：
1、master相对稳定，有大的版本更新可以使用，例如verion-2.0。
2、dev作为开发分支，团队中每个人自己的小分支做好了往dev上面合并。
3、最后工程结束了，再把dev合并到master上。
12345678
```

##### 4）利用分支改bug

假设你正在dev分支上工作，其他分支出下一个bug

```
$ git status  //查看当前工作区
$ git stash  //暂存当前的工作现场【以便你创建bug分支来解决bug】
$ git switch -c branch-bug-name  //创建并切换一个bug分支，用来解决bug
$ 去解决bug，完成然后回到出现bug的分支上
$ git megre --no-ff -m “fix bug” branch-bug-name  //合并bug分支
$ git switch dev //切换回到正在工作的分支
$ git stash pop  //回到之前的工作现场，继续工作，over
$ git cherry-pick 版本号  // 把之前的bug修改合并到某分支上【只合并修改不合并分支，用之前可以先git log一下】
12345678
```

【注】git stash apply //恢复工作现场，但是stash内容不删除，想删除git stash drop
 git stash pop //恢复工作现场并删除stash内容（一步到位）

##### 5）删除分支（未合并）

```
$ git branch -d branch-name  //通常情况下这样删除，但是未合并则会出现以下错误：
error: The branch 'branch-name' is not fully merged.
If you are sure you want to delete it, run 'git branch -D branch-name'
$ git branch -D branch-name  //-D表示强制删除
1234
```

##### 6）分支的远程操作

当你从远程克隆版本库的时候，实际上git是把本地的master和远程版本库的master分支关联了起来，并且默认的远程库名是origin（可自行修改）。

```
$ git remote  //看远程版本库
$ git remote  //看远程版本库详细信息
12
```

（1）推送分支：
 推送分支，就是把该分支上所有的本地提交的内容推送到远程分支上，推送时可以指定哪一个分支。（有些分支完全可以不推送不如bug分支）

```
$ git push origin master  //把master分支上的内容推送到远程库origin上
$ git push origin dev   //同理
master是主分支，需要时刻与远程同
【推送时显示的  origin/master 意思是远程库的主分支】
1234
```

（2）抓取分支：
 多人写作的时候，大家都会把自己的修改往远程库的master和dev上推送，现在假设你叫A，有自己的一个库，有一个人叫B拷贝了你的库。当B拷贝A的库到本地的时候，B默认是只能看到master分支，但是他要修改，所以B创建了一个dev-B分支，B必须创建远程库origin的dev分支到本地，于是B输入一行命令：

```
$ git checkout -b dev-B origin/dev  //远程库的dev分支和本地的dev-B关联
1
```

然后B就可以修改，假设B对readme.txt这个文本做了修改并提交push，而A也正好对readme.txt做了修改，并试图提交push到远程。A会push失败，因为A的push和B的冲突，这时候就需要A用git pull先把B推送的修改抓下来，然后本地合并，解决冲突，然后在提交，再push。

```
$ git pull
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
12345678910
```

git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接(关联)：

```
$ git branch --set-upstream-to=origin/dev dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
12
```

再pull：

```
$ git pull
Auto-merging env.txt
CONFLICT (add/add): Merge conflict in env.txt
Automatic merge failed; fix conflicts and then commit the result.
1234
```

这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push即可。
 【步骤小结】：多人协作模
 1、首先，可以试图用git push origin 推送自己的修改。
 2、如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并。
 3、如果合并有冲突，则解决冲突，并在本地提交。
 4、没有冲突或者解决掉冲突后，再用git push origin 推送就能成功！
 5、如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to  origin/。

##### 7）变基

```
$ git rebase  //可以把本地未push的分叉提交历史整理成直线
1
```

### 标签管理

##### 创建标签

创建标签首先要先切换到需要打标签的分支上。

```
$ git tag v1.0   //创建了叫1.0的标签
$ git tag   //可以查看当前所有标签
$ git tag 版本号   //对需要打标签版本打标签
$ git show tag-name   //查看标签信息
$ git tag -a v2.0 -m “mesage”    //创建带有说明的标签，-a指定标签名，-m制定说明文字
$ git tag -d v1.0   //删除标签（标签在本地）
$ git push origin tag-name   //推送某个标签到远程
$git push origin --tags   //推送所有标签到远程
如果标签在远程想删除：
$ git tag -d v1.0   //先删除本地的标签
$ git push origin :refs/tags/v1.0    //删除远程的标签v1.0
1234567891011
```

【注意】：标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签
 命令git tag 用于新建一个标签，默认为HEAD，也可以指定一个版本号（commit id）。

### 在GitHub上如何参与一个项目

如何参与一个开源项目呢？比如人气极高的bootstrap项目，这是一个非常强大的CSS框架，你可以访问它的项目主页https://github.com/twbs/bootstrap，点“Fork”就在自己的账号下克隆了一个bootstrap仓库，然后，从自己的账号下clone。
 一定要从自己的账号下clone仓库，这样你才能推送修改。如果从bootstrap的作者的仓库地克隆，你将没有权限，不能推送修改。
 【参与步骤：】
 1 先在参与项目的主页下“Fork”到自己的账号里
 2 然后从自己的账号里clone到本地修改【这样才有push权限】
 【如果从原项目主页直接clone，将没有push权限】
 3 如果希望对方接受你的修改，可以发起pull request。

### 给git命令配置别名

配置别名，把status命名为st，下次敲st即可。

```
$ git config --global alias.st status
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
.........

123456
```

by  久违
 2020.3.9