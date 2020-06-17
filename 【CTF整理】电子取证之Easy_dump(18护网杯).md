### 目录

- - - [电子取证之Easy_dump(18护网杯)](https://blog.csdn.net/weixin_42742658/article/details/106819187#Easy_dump18_2)

    - - [资源和连接](https://blog.csdn.net/weixin_42742658/article/details/106819187#_5)

      - [正文：](https://blog.csdn.net/weixin_42742658/article/details/106819187#_18)

      - - [0x01](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x01_62)
        - [0x02](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x02_67)
        - [0x03](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x03_74)
        - [0x04](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x04_82)
        - [0x05](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x05_86)
        - [0x06](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x06_91)
        - [0x07](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x07_97)
        - [0x08](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x08_103)
        - [0x09](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x09_126)
        - [0x10](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x10_131)
        - [0x11](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x11_168)
        - [0x12](https://blog.csdn.net/weixin_42742658/article/details/106819187#0x12_173)

      - [总结：](https://blog.csdn.net/weixin_42742658/article/details/106819187#_181)



### 电子取证之Easy_dump(18护网杯)

#### 资源和连接

原题资源：https://pan.baidu.com/s/1z73M2MRr6W6AfM57lomF-w
 提取码：1tf5

声明：本题的解法众多，我在重温这道题的时候也是借鉴了很多大佬的文章，但是本篇文章的内容都是自己所做所写，仅供大家技术交流。

参考链接：
 [2018护网杯——easy_dump](https://blog.csdn.net/weixin_40709439/article/details/83144569).
 [ctf内存取证----easy_dump](https://blog.csdn.net/https://blog.csdn.net/MOLLMY/article/details/100865618?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase).
 [2018护网杯 easy_dump](https://www.cnblogs.com/imbraininvat/p/12311149.html).

------

#### 正文：

知道题目的类型是电子取证里面的内存读取，那就首相想到的就是用volatility工具去分析，volatility工具的功能十分强大，这里简单介绍一下这个工具的使用。（工具自行安装也可以，但是kali自带）
 windows下一般运行环境为python2，python2 vol.py [参数] 调用即可，我用linux举例

volatility -f easy_dump.img imageinfo
 【获取内存操作系统】

volatility -f easy_dump.img kdbgscan
 【获取内存操作系统
 【imageinfo和kdbgscan这两个一般第一个最准确】

volatility -f easy_dump.img --profile=Win7SP1x64 netscan
 【–profile参数指定镜像】
 【内存网络扫描】

volatility -f easy_dump.img --profile=Win7SP1x64 amdscan
 【读取cmd命令】

volatility -f easy_dump.img --profile=Win7SP1x64 pslist
 【内存进程列举】

volatility -f easy_dump.img --profile=Win7SP1x64 hivelist
 【列举内存注册表】

volatility -f easy_dump.img --profile=Win7SP1x64 -o 0xfffff8a0013fb010 printkey
 【解析指定的注册表】

volatility -f easy_dump.img --profile=Win7SP1x64 -o  0xfffff8a0013fb010 printkey -K  “ControlSet001\Control\ComputerName\ComputerName”
 【获取主机名】

volatility -f easy_dump.img --profile=Win7SP1x64 -o 0xfffff8a0013fb010 printkey -K “SAM\Domains\Account\Users\Names”
 【获取windows主机用户名】

volatility -f easy_dump.img mimikatz
 【抓取用户密码】

volatility -f easy_dump.img filescan
 【文件扫描】

volatility -f easy_dump.img filescan | grep “flag”
 【配合grep文件扫描】

##### 0x01

1、利用利用 `volatility -f easy_dump.img imageinfo`查看镜像信息
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020061722184850.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)看 Suggested Profile(s) 的值，猜测它最有可能是`Win7SP1x64`的镜像【一般第一个最有可能】
 然后后面就用参数 `--profile`指定镜像为`Win7SP1x64`

##### 0x02

2、利用 `volatility -f easy_dump.img --profile=Win7SP1x64 psscan` 指定镜像进行进程扫描
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617222141264.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)这道题这里使用 `pslist`参数也可以把想要的东西找出
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617231119652.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 在这里发现这个notepad.exe ，想到看记事本里面的内容，寻找线索

##### 0x03

3、利用`volatility -f easy_dump.img --profile=Win7SP1x64 memdump -p 2616 -D ./`把记事本的内容导出来，可以看到导出文件2616.dmp
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617231457305.png)这里说一下两个参数：
 `procdump`：是提取进程的可执行文件
 `memdump`：是提取进程在内存中的信息
 这里我们记事本里面的信息，所以用`memdump`

##### 0x04

4、`strings -e l 2616.dmp | grep "flag"`在2616.dmp里面直接搜flag有关的信息，得到下一个提示是`jpg`
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617231928321.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

##### 0x05

5、那我们就开始内存文件读取搜jpg，`volatility -f easy_dump.img --profile=Win7SP1x64 filescan | grep "jpg"` 发现一个图片文件phos.jpg
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617232126943.png)导出来这个图片，file.None.0xfffffa8008355410.vacb【名称默认】
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617232538459.png)

##### 0x06

6、检查phos.jpg图片，图片看不了，使用binwalk查看
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617232303101.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)`binwlak file.None.0xfffffa8008355410.vacb`
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/202006172326036.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)发现里面有zip文件

##### 0x07

7、分离zip文件  `foremost file.None.0xfffffa8008355410.vacb`
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617232801216.png)分离后自动生成一个outpt文件，里面可以看分离出来的压缩文件
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617233115455.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)解压这个压缩文件，可以得到`message.img`文件，再次使用binwalk工具提取里面的文件
 `binwalk -e message.img` ，即可得到隐藏在里面的`hint.txt`文件，打开查看发现是一些数字
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617233607619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

##### 0x08

8、怀疑这些数字是坐标，于是上脚本转换一下试试 ，得到二维码图片

```
#脚本文件
import matplotlib.pyplot as plt
import numpy as np

x = []
y = []
with open('hint.txt','r') as f:
   datas = f.readlines()
   for data in datas:
        arr = data.split(' ')
        x.append(int(arr[0]))
        y.append(int(arr[1]))
     
plt.plot(x,y,'ks',ms=1)
plt.show()
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617233841199.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

##### 0x09

9、识别这个二维码
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617233916295.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到两个消息，一个是维吉尼亚加密，秘钥是aeolus，一个是加密文件被删除了，所以我们需要恢复一下这个被删除的文件

##### 0x10

10、使用testdisk恢复文件

这里介绍一下testdisk这个工具基本界面（kali自带）
 [testdisk工具介绍](https://www.cnblogs.com/cnsanshao/p/5978288.html).

输入：testdisk xxx 即可进入软件内部操作
 Proceed：继续
 Quit：退出，关闭

[ Analyse  ] 分析正确的分区结构并找到丢失的分区表
 [ Advanced ] 文件系统工具
 [ Geometry ] 更改硬盘类型
 [ Options  ] 修改高级选项
 [ Quit     ] 返回到硬盘检测

[  Type  ] ：改变文件系统的类型，这种修改并不会真正改变硬盘上的真正格式。
 [Superblock]  ：列出超级块，这是文件系统的基本元数据。
 [  List  ] ：列出所有文件，并复制（恢复）出来
 [Image Creation] ：对当前分区创建镜像文件
 [  Quit  ]：退出，返回

红色文件就表示已经删除的文件。当然你也可以选择一个红色的目录，表示恢复整个目录。

**这里我直接用图说明操作过程：**
 输入 ：`testdisk message2.img` 进入界面

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617234634303.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617234722634.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617234738135.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617234802377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617234817506.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)红色为我们需要恢复的文件，选择它之后按小写的“c”进入下一个界面选择导出路径
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617234855411.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)选中之后按大写的“C”确定，然后即可导出文件
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617234855400.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)我直接恢复到桌面，这里显示复制成功

##### 0x11

11、导出后需要使用 `ls -a`查看，找到文件后直接`strings`查看
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617235330212.png)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617235354747.png)

##### 0x12

12、发现一串字符串很像加密的维吉尼亚密码，用之前得到的秘钥解密
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617235510992.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

得到最终结果

累死我了写的。

#### 总结：

工具volatility 的使用还是不熟练，binwalk和foremost等还有许多参数的作用没有记下，testdisk恢复工具第一次使用，后面还要多学学，熟悉熟悉。越学越觉得有很多东西不会，有很多需要学。上学需要努力，上班需要努力，学东西还要加把劲啊。
 ps：上班体验很充实，虽然有时有些辛苦，但是很开心，同事们也很好，现阶段目标，努力一直在公司待下去，加油！

by 久违 2020.6.18 凌晨