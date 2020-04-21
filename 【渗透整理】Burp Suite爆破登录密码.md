# 【渗透整理】Burp Suite爆破登录密码

之前我写的《【渗透整理】SQL注入篇》里面有一些关于burp抓包的内容，不过那里面的burp是辅助sqlmap的，而这次主要的使用工具就是它，关于burp的使用我之后再系统的整理一下，这里先简单记一下Instuder模块的用法。

使用的主机：106.75.79.26 ，环境：DVWA  Brute Force ，游戏开始

## 1、初步尝试

看到输入用户名，密码的登录框，习惯性先上了sql注入的一套（虽然这不是本文的重点），然后惊喜的发现万能密码admin’ or ‘1’='1可以用，直接登录成功解决问题，没后面什么事了。

## 2、Burp爆破

1、抓包：
 随便在用户名和密码框里面输入，然后用burp抓包观察，可以看到用户名和密码是怎么提交的。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226110933299.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 然后鼠标右键选择send to instuder ，接下来我们到instuder模块下来搞事情。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226111051925.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)进入instuder之后先clear一下，然后自己ADD需要爆破的参数，由于这里是两个参数admin和123，我选择了 cluster bomb方式，下面是我挖来的：

```
四种暴力破解方式的区别：

   一个字典，两个参数，先匹配第一项，再匹配第二项【sniper】

   一个字典，两个参数，同用户名同密码【battering ram】

   两个字典，两个参数，同行匹配，短的截止【pitch fork】

   两个字典，两个参数，交叉匹配，所有可能【cluster bomb】
123456789
```

然后点payloads设置参数
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226111624941.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)点load…可以导入字典，我自己为了测试，随便写了几个，字典的获取可以自己到网上找，好的字典在爆破的时候后可以起到事半功倍的效果。payloads list选择2，设置完成之后点击start attack开始爆破。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226112127943.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)等burp完成之后，长度Length不一样的就是密码了，这里直接爆出用户名是admin，密码是password，我们用这个用户和密码尝试登陆，登陆成功。`在这

## 3、总结

Burp的字典爆破可以一站式爆出结果，很方便，但是字典攻击一般很耗时，穷举的爆破一般渗透中不是上选，而且这种爆破手段对字典有要求，理论上时间充足的话足够优秀的字典无敌。但是可惜实战中不会用那么多时间。burp的爆破先记在这里，以便以后过来看看。

by 久违 2019.12.26
 （最近写的频率有点小高，加油一下）