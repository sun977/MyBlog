# Windows cmd 设置编码格

问题描述：在Windows cmd里面type .txt文件时，打开出现乱码。
 问题根源：我的电脑txt文件打开默认编码格式是UTF-8，windows cmd默认编码格式是JBK，打开格式不一样。
 解决办办法：

### 一、设置Windows cmd的编码格式为UTF-8

打开cmd输入chcp xxx即可。（xxx是不同编码格式的页代码，不同编码页代码如下图）
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200308174535559.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)这里输入chcp 65001即可改成UTF-8格式，但只是本次有效，永久更改需要改动注册表。
 恢复成JBK可以用chcp 936命令。
 如还无法显示UTF-8文本，则戳：
 https://www.cnblogs.com/QQParadise/articles/1685177.html

### 二、将文本文件txt格式改为ANSI：

打开需要修改的txt文件，文件–>另存为，选择编码格式为ANSI，确定，即可。
 同样是本次有效，永久修改需要改动注册表。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200308175136753.png)
 【注意】：我们遇到的大多数软件都是UTF-8编码格式的，所以一些程序员会把cmd默认的编码格式永久改成UTF-8，这样做可能引起其他的电脑问题（能自信解决的大佬请绕过），可能会蓝屏死机。建议不要改成永久，反正就一句chcp 65501命令。

by 久违
 2020.3.7