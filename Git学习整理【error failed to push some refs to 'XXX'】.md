##### 踩坑小记，GitHub上新建一个版本库，手贱点了自动生成README.md文件，然后关联库，git push的时候提示这个错误：

```
error: failed to push some refs to 'xxx'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

##### 原因：本地库和远程库不同步。因为远程库上有一个README.md文件，本地没有，所以需要把远程库上的README.md文件先同步到本地，之后再进行push。

```
$ git pull --rebase origin master
$ git push origin master
```

##### 问题解决

by 久违 2020.4.20

