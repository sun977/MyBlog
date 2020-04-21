# 【渗透整理】Linux命令基础(1)

## 1、系统操作

1、【sync】把内存中的数据写到磁盘中（关机或者重启前都需先执行sync）

2、【shutdown -r now】立即重启

3、【reboot】立即重启

4、【shutdown -h now】立即关机

5、【shutdown -h 20：00】定时晚上20：00关机

6、【shutdown -h + 10】10分钟后关闭系统

7、【whoami】查看当前操作的用户

8、【who】查看所有的终端

9、【uname -r】显示正在使用的内核版本

10、【uname -m】显示机器的处理器架构（如X86_64）

11、【lsb_release -a】显示系统发行版本

12、【date】显示时间日期

13、【cal 2019】显示2019年的日历

14、【cat /proc/cpuinfo】显示cpu信息

15、【top】动态显示cpu，内存，进程等使用状况（windows任务管理器）

16、【clear】清空命令行

17、【ps】显示当前进程 ps -aux 显示进程所有信息

### 2、新建操作

1、【mkdir +文件名】新建一个文件夹（目录）

2、【touch + 文件名】新建一个文件（touch abc.sh 新建一个abc.sh文件）

3、【echo “abc” > test.txt】新建一个test.txt文件，并写入“abc”

4、【echo “efg” >> test.txt】

### 3、目录和文件操作

1、【cd+路径】进入目录

2、【cd ..】返回上一级目录

3、【ls】查看目录或者文件

4、【ls -a】显示目录下所有的内容，包括隐藏内容

5、【ls -l】使用较长的格式输出信息

6、【rmkdir】删除空目录

7、【rm】删除目录和文件

8、【rm -rf 文件名/目录名】删除目录或者文件 rm -r 递归删除文件  rm -f 强制删除

9、【cp】复制文件或者目录 

10、【cp test1.txt  ./new/test2.txt】复制test1.txt 到new目录下到test2.txt文件

11、【mv】移动文件或目录 eg：mv ./test2/test2.txt ./test 移动test2目录下的test2.txt到test目录下

12、【tar -zcvf】压缩

13、【tar -zxvf】解压

14、【pwd】多去当前目录位置

15、【cat】显示文件内容，由第一行开始显示，并且显示所有文件 

16、【vi或vim】打开vi或vim编辑器编辑文件 eg： vim test.txt 文件

17、【tac】从最后一行倒序显示，并显示所有内容

18、【more】根据窗口大小，一页一页显示内容

19、【head】只显示头几行

20、【tail】只显示尾几行 tail -n 10 test.txt 查看文本文件test.txt前10行

21、【nl】显示时，输出行号

22、【static-sh】显示文件内容

23、【paste】读取文件内容

24、【diff】读取文件

25、【od】od -A o test 以八进制显示，od -A d test 以十进制显示，od -A x test 以十六进制显示

26、【bzmore】读取文件

27、【file】查看文件类型

28、【pwd】显示当前工作路径

29、【locate】locate a.txt 在系统内全局查找包含a.txt字样的文件

30、【whereis】查看文件的路径

## 4、文件权限管理

1、【chgrp】chgrp group_name test.txt  改变文件所在的组（组名必须在etc/group中）

2、【chown】chown ower_name  test.txt 改变文件test.txt的所有者（拥有者名必须在etc/password中）

3、【chmod】更改文件权限，chmod 777 test.txt （第一个7：群组，第二个7：拥有者，第三个7：其他权限）
        每个7是最高的权限，对应r-w-x 读-写-可执行 ，7是：111,代表读写执行权限都有。4是100，代表只有读权限

## 5、网络监测

1、【ifconfig】 获取网卡配置信息，同windows的ipconfig

2、【ping】测试网络连通性

3、【who】查看当前主机用户端信息

## 6、用户与权限

1、【useradd+用户名】添加用户

2、【userdel -r +用户名】删除用户，r表示把用户的主目录一起删除

3、【usermod -g +组名+用户名】修改用户的组

4、【usermod -aG+组名+用户名】将用户添加到组

5、【group +用户名】查看用户的组

6、【cat  /etc/group +用户】 查看用户详情：用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录Shell 

7、【cat  /etc/password】查看password文件，只有root可以修改（密码是加密存储的）

8、【cat  /etc/shadow】查看shadow文件（是password的镜像文件，密码加密存储，只有root可以进入）

9、【passwd [ludf] 用户名】 ：用户改自己密码，不需要输入用户名，选项-d:指定空口令,-l:禁用某用户，-u解禁某用户，-f：强迫用户下次登录时修改口令 

10、【groupadd 组名】添加组名

11、【groupdel 组名】删除组名

12、【groupmod -n 新组名 就组名】修改组名

13、【su -用户】切换用户（完整的用户环境，相当于登录）

14、【su 用户名】切换用户（环境变量没变）

15、【sudo +命令】 以root的身份执行命令（输入用户自己的密码，而su为输入要切换用户的密码，普通用户需设置/etc/sudoers才可用sudo） 

## 7、磁盘管理

#### df：列出文件系统的整体磁盘使用量

#### du：检查磁盘空间使用量

#### fdisk：用于磁盘分区

1、【df -h】显示磁盘的使用情况及挂载点

2、【df -a】列出所有的文件系统，包括系统特有的 /proc 等文件系统 

3、【df -h /var/log】显示log所在分区的挂载点，目录所在的磁盘即可用的磁盘容量

4、【du -sm /var/log/* \| sort -rn】 根据占用磁盘空间大小排序（MB）某目录下文件和目录大小 

5、【fdisk -l】查所有分区的总容量

6、【fdisk /dev/sdb】对硬盘sdb进行分区

7、【mount 装置文件名  挂载点】把某个设备挂载到系统，这样系统才可以访问
         （挂载：）

8、【mount /dev/sdb1  /mnt】硬盘sdb1挂载到/mnt目录

9、【umount  /dev/sda1】取消挂载





















