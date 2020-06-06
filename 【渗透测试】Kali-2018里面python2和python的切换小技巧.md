### 【渗透测试】Kali-2018里面python2和python的切换小技巧

我自己使用的kali是2018版本的，这个版本里面的python环境同时安装了python2和python3，但是默认情况下kali会使用python2，这里记一下kali切换python2和python3的方法：

使用 ls /usr/bin/python* 可以查看kali是否安装了双版本的python
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200607003232462.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 默认是python2版本
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200607003948728.png)

1、暂时修改当前python版本

```
修改当前版本到python3.7版本
alias python="/usr/bin/python3.7"    
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200607003915977.png)

```
 修改当前版本回到python2
 alias python="/usr/bin/python2.7" 
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200607004236883.png)
 如果你需要快速的在版本2和3之间切换使用，那么也可以用python2和python3暂时区分这两个版本【就和windows区分一样，只不过只在当前的界面有效，是暂时的】

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200607004457882.png)

2、永久修改当前python版本

说是永久，其实只是重新开启一个终端之后还有效罢了

```
修改默认python2和python3的优先级
update-alternatives --install /usr/bin/python python /usr/bin/python2 100
update-alternatives --install /usr/bin/python python /usr/bin/python3 150
此时150>100 ，所以默认显示python3 
```