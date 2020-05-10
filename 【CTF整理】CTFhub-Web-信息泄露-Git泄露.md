### 【CTF整理】CTFhub-Web-信息泄露-Git泄露

#### 一、 log

##### 进入界面，得到一个url，根据提示直接开干

##### 1、使用dirsearch扫描url，发现url低下存在敏感文件.git

```
python3 dirsearch.py -u <url> -e * 
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510122728933.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510122753881.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

##### 2、使用GitHack进行文件恢复【这里需要将扫描到的.git加在url后面】,然后在GitHack所在目录下的dist目录下得到恢复的文件。

```
python2 GitHack.py <url>  (url格式：http(s)://xxx/.git)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510123459481.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510123514903.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

###### 3、进入dist目录中的刚恢复的文件内打开git，读取git日志，发现：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510123636810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

##### 回退到“add flag”的那个版本，即可查看flag

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510123734819.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

#### 二、Stash

##### dirsearch扫描发现.git文件（找到思路），GitHack恢复到本地dist目录下，进入恢复的目录下打开git操作

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510124133838.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

```
git log  //查看日志
```

##### 这里可以使用Stash栈pop出flag，也可以直接回到add flag的版本查看，这里我使用pop出，得到flag

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510124359188.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510124430119.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

#### 三、Index

##### 如法炮制，dirsearch目录扫描，GitHack恢复到本地，git读取flag（git log发现这里的flag直接在当前工作区，可是ls显示啥也没有，无奈回到当前版本才显示出来，我满头的小问号？？？？）![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510124847602.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510124855235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200510124902173.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

by 久违 2020.5