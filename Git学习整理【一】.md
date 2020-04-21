# Git学习整理【一】

## 创建版本库

```
$ mkdir MyGitRep（库名为例）
$ cd MyGitRep  // 进入库目录（文件夹）内
$ git init   // 把目录变成Git可管理的仓库,初始化。（多出.git文件，一般是隐藏的）
123
```

## 添加文件到版本库（提交）

```
$ git add readme.txt //文本文件，以readme.txt为例【工作区--->暂存区】
$ git commit -m "修改描述" //不写描述加*【暂存区--->当前分支上】
12
```

可以多次git add file-name，然后一起提交git commit -m “message”。

```
$ git status //查看当前状态（工作区） 
On branch master
nothing to commit, working tree clean
表示当前分支上的工作区空闲。

12345
```

## 版本回退

假设readme.txt有几个版本，每个版本有相应的版本描述和版本号(版本号系统随机)
 版本1：version 1
 版本2：version 2
 版本3：version 3

```
$ git log //查看提交历史记录，方便找回版本号
【HEAD指向当前工作的版本】
$ git log --pretty=oneline //简略输出提交历史信息
$ git reflog // 查看命令历史，方便找回版本号
$ git reset --hard HEAD^  //返回上一个版本【HEAD^表示上一个最近版本】
$ git reset --hard 9775  //返回版本号是9775的版本【版本号很长不必写全】
123456
```

## 管理修改

git跟踪的是修改而不是文件，readme.txt每次修改之后都要git add 然后git commit，因为分支上只会保留add后的修改。【工作区–>git add–>暂存区–>git
 commit -m*–>分支(版本库)】
 提交之后可以用

```
$ git diff HEAD --readme.txt  //查看工作区的readme和分支上(版本库)的readme的区别
1
```

小结：每次修改如果不git add到暂存区，就不会git commit到分支上(版本库里)

## 撤销修改

```
$ git checkout --readme.txt //可以丢弃工作区的修改（错误修改还没有add到暂存区）
$ git checkout //用版本库的文件替换工作区的文件（一键还原）
$ git reset HEAD readme.txt //可以撤销暂存区的修改，重新回到工作区（已经add过到暂存区）【HEAD表示最新版本】
如果错误的修改已经提交到版本库(分支)里，则要版本回退到上一个版本git reset --hard HEAD^
1234
```

## 删除文件

注意，在文件管理器rm一个文件并不代表在git版本库里也rm了这个文件【这一点体现在：文件删除了，但是可以从版本中回复过来】
 所以，通常有两种情况：
 情况一：想删除某个文件

```
$ rm readme.txt //文件管理器中删除
$ git rm readme.txt //从版本库中删除
12
```

情况二：误删某个文件

```
$ rm readme.txt //误删
$ git status //查看状态，发现被误删
$ git checkout --readme.txt //从版本库中恢复出误删的文件
123
```

## 从GitHub上克隆版本库到本地

在github上找到你想拷贝的版本库的连接

```
$ git clone https://github.com/sun977/learngit.git //借助Http协议克隆库到本地
$ git clone git@github.com:sun977/learngit.get  //借助ssh协议克隆库到本地
12
```

克隆远程库到本地之前最好先cd到你要存放库的目录下。

## 从本地发布版本库到GitHub

1）在自己的github上创建一个空版本库learngit
 2）在本地库下输入运行命令：

```
$ git remote add origin git@github.com:sun977/learngit.git   //通过URL远程关联github上的learngit空版本库。
$ git push -u origin master  //把本地库push到远程库上
如果出现：fatal: remote origin already exists.则
$ git remote rm origin //然后重新关联并push
关联之后，后面的提交都只需要push即可，不需要再次关联。
参数-u在第一次push的时候使用，他是把本地的master分支和远程库的master分支关联起来。
$ git push origin master  //后面本地提交
1234567
```

by  久违
 2020.3.5