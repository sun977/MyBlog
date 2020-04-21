#### 踩坑小记，Git上传到远程库的时候发现一个文件夹上传不成功，报错如下

```
fatal: in unpopulated submodule 'spider'
```

#### 原因是这个文件夹来自的库是第三方库，通常这种情况就会出现报错

#### 解决办法：

```
$ git  rm -rf --cached spider/ 
$ git add spider/ 
$ git commit -m"second add spider"
```

#### 完美解决

by 久违 2020.4.20

