# 【渗透整理】DOS命令基础(1)

1、【dir】打开用户菜单
                /w ：所有文件一屏内显示
                /s  ： 当下目录下的所有目录
                *.txt  ：显示当前目录下所有.txt 后缀的文件    
2、【cd】改变当前目录（进入文件目录）
                  “  .  ”表示当前目录
                   “ .. ”表示上一级目录（cd .. 返回上一级文件目录）
3、【type】查看当前文件目录下的某个目录，查看文件
                  eg：type 1.txt 
4、【echo】回显，输入，写文件
                  eg：echo “你好！”    > 1.txt     写入“你好！”到新建的文本文档1.txt中
                  eg：echo “你也是！”    >> 1.txt    追加“你也是！”到1.txt文本文档中
5、【del】删除文件
6、【md】创建文件夹
7、【copy】将一份或者多份文件复制到另一个位置
                   eg：copy 1.txt  .\test    复制1.txt到test文件中
8、【ren】重命名文件
                  eg ： ren 1.txt  2.txt  文件1.txt重名为2.txt
9、【rd】删除目录(rd只能删除目录，del可以删除文件也可以是目录)
             -s ：删除目录和目录底下的内容
             -q ：安静模式，不询问是否删除
10、【ping】测试网络连通性
              -t ： 持续的ping某个主机
              -a ：将地址解析为主机名
              -4 ： 强制使用ipv4
              -6 ：强制使用ipv6
11、【tracert】路由跟踪（显示路径）
              -d ： 不进行DNS解析
              -h ：最大跳跃点书
12、【ver】查看系统版本
13、【ipconfig】查看电脑网络配置
14、【taskmgr】任务管理器
15、【tasklist】显示正在运行的进程
16、【kill】结束进程
17、【time】显示时间
18、【D：】进入D盘
19、【/？】指定命令帮助
20、【tree】显示目录树形结构

### net

这个命令是网络命令中最重要的一个。功能十分强大

【net view】使用此命令查看远程主机的所有共享资源。

【net use】把远程主机的某个共享资源影射为本地盘符。

【net stop】入侵后发现远程主机的某个服务碍手碍脚，怎么办？利用这个命令停掉就ok了，用法和net start同。

【net user】

查看和帐户有关的情况，包括新建帐户、删除帐户、查看特定帐户、激活帐户、帐户禁用等。不带参数的net user，可以查看所有用户，包括已经禁用的。

1，net user abcd 1234 /add，新建一个用户名为abcd，密码为1234的帐户，默认为user组成员。

2，net user abcd /del，将用户名为abcd的用户删除。

3，net user abcd /active:no，将用户名为abcd的用户禁用。

4，net user abcd /active:yes，激活用户名为abcd的用户。

5，net user abcd，查看用户名为abcd的用户的情况

【net localgroup】　查看所有和用户组有关的信息和进行相关操作。不带参数的net  localgroup即列出当前所有的用户组。在入侵过程中，我们一般利用它来把某个帐户提升为administrator组帐户，这样我们利用这个帐户就可以控制整个远程主机了。

【net time】这个命令可以查看远程主机当前的时间。

net use \\ip\ipc$ " " /user:" " 建立ipc空链接

net use \\ip\ipc$ "密码" /user:"用户名" 建立ipc非空链接

net use h: \\ip\c$ "密码" /user:"用户名" 直接登陆后映射对方c：到本地为h:

net use h: \\ip\c$ 登陆后映射对方c：到本地为h:

net use \\ip\ipc$ /del 删除ipc链接

net use h: /del 删除映射对方到本地的为h：的映射

net user 用户名 密码 /add 建立用户

net user guest /active:yes 激活guest用户

net user 查看有哪些用户

net user 帐户名 查看帐户的属性

net localgroup ***istrators 用户名 /add 把“用户”添加到管理员中使其具有管理员权限，注意：***istrator后加s用复数

net start 查看开启了哪些服务net start 服务

net start schedule)net stop 服务名 停止某服务

net time \\目标ip 查看对方时间

net time \\目标ip /set 设置本地计算机时间与“目标ip”主机的时间同步，加上参数/yes可取消确认信息

net view 查看本地局域网内开启了哪些共享

net view \\ip 查看对方局域网内开启了哪些共享

net config 显示系统网络设置

net send ip "文本信息" 向对方发信息

net ver 局域网内正在使用的网络连接类型和信息

net share 查看本地开启的共享

net share ipc$ 开启ipc$共享

net share ipc$ /del 删除ipc$共享

net share c$ /del 删除c：共享

