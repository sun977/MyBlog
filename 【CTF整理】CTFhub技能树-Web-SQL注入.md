### 【CTF整理】CTFhub技能树-Web-SQL注入



### 目录

- - - [【CTF整理】CTFhub技能树-Web-SQL注入](https://blog.csdn.net/weixin_42742658/article/details/106034915#CTFCTFhubWebSQL_0)

    - - [SQL整数型注入](https://blog.csdn.net/weixin_42742658/article/details/106034915#SQL_2)
      - [SQL字符型注入](https://blog.csdn.net/weixin_42742658/article/details/106034915#SQL_16)
      - [SQL报错注入](https://blog.csdn.net/weixin_42742658/article/details/106034915#SQL_43)
      - [SQL布尔型注入](https://blog.csdn.net/weixin_42742658/article/details/106034915#SQL_54)
      - [SQL时间注入](https://blog.csdn.net/weixin_42742658/article/details/106034915#SQL_65)
      - [MySQL结构](https://blog.csdn.net/weixin_42742658/article/details/106034915#MySQL_77)
      - [Cookie注入](https://blog.csdn.net/weixin_42742658/article/details/106034915#Cookie_80)
      - [UA注入](https://blog.csdn.net/weixin_42742658/article/details/106034915#UA_102)
      - [Referer注入](https://blog.csdn.net/weixin_42742658/article/details/106034915#Referer_124)



#### SQL整数型注入

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510130627900.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510130657104.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)确定闭合方式 ：1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510130805248.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510130824493.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510130913188.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 确定报错位有2个，（我选2注入点）

![img](https://img-blog.csdnimg.cn/20200510131001217.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到库名
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510131026390.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到表名
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510131048302.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到列名
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510131057555.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到flag

#### SQL字符型注入

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510131528362.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/202005101316323.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 确定闭合方式：1’
 【步骤和整形一样，不再使用，我这里采用sqlmap】

```
核心语法:

sqlmap -u "url+参数" --dbs   爆库
 
sqlmap -u "url+参数" -D 库名 --tables   爆表
 
sqlmap -u "url+参数" -D 库名 -T 表名 --columns   爆列名
 
sqlmap -u "url+参数" -D 库名 -T 表名 -C 列名 --dump  爆内容

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510131922816.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510132341158.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510132351626.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)最后一步爆内容始终爆不出结果，语句语法正常没有错误，原因未知，改用手注得到flag（一样的sql语句sqlmap不行手注成功，我是服了，满头的小问号？？？？）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510132648617.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

#### SQL报错注入

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510132903854.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510132916995.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)确定闭合方式：1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510133012888.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510133045891.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)确定2个报错位，开始报错注入

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510133204863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到库名
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510133226544.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到表名和列名
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510133438814.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)得到flag

#### SQL布尔型注入

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510133956918.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134013376.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134031841.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051013404337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 确定闭合方式：1
 （确定闭合方式是一种习惯，虽然我已经想用sqlmap做这道题了。。。。sqlmap会自动识别闭合方式， --technique B参数指定用布尔型盲注）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134227271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134411992.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134425340.png)




 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134441576.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

#### SQL时间注入

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134613577.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)确定闭合方式：1 （睡了5s才进入）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134735837.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134748983.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134803552.png)

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134845480.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510134856544.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

#### MySQL结构

没啥东西，sqlmap跑跑就没了

#### Cookie注入

开启Burp，设置firefox代理，抓包然后 send-to-repeater模拟提交
 修改数据包内cookie的值进行注入
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510135347655.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510135418162.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510135432140.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 确定闭合方式：1
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510135509836.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510135532514.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510135718776.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

确定2个报错位
 （还是HTML好看，清晰）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510135738361.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)爆库
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510135759170.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 爆表
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510135940739.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 爆列名
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051014001339.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)爆内容得到flag
 【我就弱弱的说一句，就不能给个正常一点的表名和列名嘛？？？非要这个随机的一串，我都不知道flag在哪，让我好找啊】

#### UA注入

【原理和cookie注入一样，只是注入点位置是User-Agent，这里直接用sqlmap】
 （–leve 3 的时候sqlmap会对数据包进行User-Agent检测）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510140800833.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510140815448.png)
 爆库

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510140848482.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510140902785.png)


爆表

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510140920779.png)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510140938484.png)

爆列名


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510141027791.png)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051014103546.png)
 爆内容，得到flag

#### Referer注入

Burp抓包修改referer内容
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510150638269.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510150652481.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510150705484.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510150718239.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)【使用sqlmap --leve 5 自动注入，注入到最后一步就是不出结果，遇到了和上面一样的问题，无奈全程手注，然后居然出flag这么干脆】

by 久违 2020.5