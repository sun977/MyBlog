# 单区域OSPF动态路由协议详情和实验（OSPF3-1）（OSPF路由协议概述和工作过程，OSPF基本概念详解和数据包类型与临街关系，单区域配置）

### 文章目录

- [一：OSPF的基本概念和工作过程](https://blog.csdn.net/CN_TangZheng/article/details/102693173#OSPF_9)
- - - [1.1：OSPF路由协议概述](https://blog.csdn.net/CN_TangZheng/article/details/102693173#11OSPF_11)
    - - - [1.1.1：自治系统（AS）](https://blog.csdn.net/CN_TangZheng/article/details/102693173#111AS_13)
        - [1.1.2：内部网关协议（IGP）](https://blog.csdn.net/CN_TangZheng/article/details/102693173#112IGP_19)
        - [1.1.3：外部网关协议（EGP）](https://blog.csdn.net/CN_TangZheng/article/details/102693173#113EGP_27)
        - [1.1.4：OSPF是链路状态路由协议](https://blog.csdn.net/CN_TangZheng/article/details/102693173#114OSPF_32)

    - [1.2：OSPF的工作过程](https://blog.csdn.net/CN_TangZheng/article/details/102693173#12OSPF_36)
    - - - [1.2.1：建立邻居列表](https://blog.csdn.net/CN_TangZheng/article/details/102693173#121_38)
        - [1.2.2：链路状态数据库](https://blog.csdn.net/CN_TangZheng/article/details/102693173#122_42)
        - [1.2.3：形成路由表](https://blog.csdn.net/CN_TangZheng/article/details/102693173#123_46)

    - [1.3：OSPF的基本概念](https://blog.csdn.net/CN_TangZheng/article/details/102693173#13OSPF_52)
    - - - [1.3.1：OSPF区域](https://blog.csdn.net/CN_TangZheng/article/details/102693173#131OSPF_54)
        - [1.3.2：Router ID](https://blog.csdn.net/CN_TangZheng/article/details/102693173#132Router_ID_68)
        - [1.3.3：Router ID选取规则](https://blog.csdn.net/CN_TangZheng/article/details/102693173#133Router_ID_73)
        - [1.3.4：DR 和 BDR](https://blog.csdn.net/CN_TangZheng/article/details/102693173#134DR__BDR_81)
        - [1.3.5：DR 和 BDR 的选举方法](https://blog.csdn.net/CN_TangZheng/article/details/102693173#135DR__BDR__99)
        - [1.3.6：DR 和 BDR 的选举过程](https://blog.csdn.net/CN_TangZheng/article/details/102693173#136DR__BDR__107)
        - [1.3.7：OSPF的组播地址](https://blog.csdn.net/CN_TangZheng/article/details/102693173#137OSPF_114)
        - [1.3.8：OSPF的度量值为COST](https://blog.csdn.net/CN_TangZheng/article/details/102693173#138OSPFCOST_122)

- [二：OSPF的数据包类型](https://blog.csdn.net/CN_TangZheng/article/details/102693173#OSPF_131)
- - - [2.1：OSPF数据包](https://blog.csdn.net/CN_TangZheng/article/details/102693173#21OSPF_133)
    - [2.2：OSPF的包类型](https://blog.csdn.net/CN_TangZheng/article/details/102693173#22OSPF_138)

- [三：OSPF邻接关系](https://blog.csdn.net/CN_TangZheng/article/details/102693173#OSPF_151)
- - - [3.1：OSPF邻接关系的建立（7个状态）（重点）](https://blog.csdn.net/CN_TangZheng/article/details/102693173#31OSPF7_153)
    - [3.2：OSPF的网络类型](https://blog.csdn.net/CN_TangZheng/article/details/102693173#32OSPF_169)
    - [3.3：以下几方面考虑OSPF的使用（应用环境）](https://blog.csdn.net/CN_TangZheng/article/details/102693173#33OSPF_173)
    - [3.4：OSPF的特点（重点）](https://blog.csdn.net/CN_TangZheng/article/details/102693173#34OSPF_177)
    - [3.5：OSPF与RIP的比较](https://blog.csdn.net/CN_TangZheng/article/details/102693173#35OSPFRIP_181)

- [四：OSPF单域的配置](https://blog.csdn.net/CN_TangZheng/article/details/102693173#OSPF_186)
- - - [4.1：OSPF的基本配置命令](https://blog.csdn.net/CN_TangZheng/article/details/102693173#41OSPF_188)

- [五：OSPF单域配置实验](https://blog.csdn.net/CN_TangZheng/article/details/102693173#OSPF_214)
- - - [5.1：实验目的](https://blog.csdn.net/CN_TangZheng/article/details/102693173#51_216)
    - [5.2：环境](https://blog.csdn.net/CN_TangZheng/article/details/102693173#52_220)
    - [5.3：实验过程（七步）](https://blog.csdn.net/CN_TangZheng/article/details/102693173#53_228)
    - [5.4：总结](https://blog.csdn.net/CN_TangZheng/article/details/102693173#54_244)



# 前言

OSPF路由协议是用于网际协议（IP）网络的链路状态路由协议。该协议使用链路状态路由算法的内部网关协议（IGP），在单一自治系统（AS）内部工作。适用于IPv4的OSPFv2协议定义于RFC 2328，RFC 5340定义了适用于IPv6的OSPFv3。

开放式最短路径优先（Open Shortest Path  First，OSPF）是目前广泛使用的一种动态路由协议，它属于链路状态路由协议，具有路由变化收敛速度快、无路由环路、支持变长子网掩码（VLSM）和汇总、层次区域划分等优点。在网络中使用OSPF协议后，大部分路由将由OSPF协议自行计算和生成，无须网络管理员人工配置，当网络拓扑发生变化时，协议可以自动计算、更正路由，极大地方便了网络管理。但如果使用时不结合具体网络应用环境，不做好细致的规划，OSPF协议的使用效果会大打折扣，甚至引发故障。

OSPF协议是一种链路状态协议。每个路由器负责发现、维护与邻居的关系，并将已知的邻居列表和链路费用LSU(Link State  Update)报文描述，通过可靠的泛洪与自治系统AS(Autonomous  System)内的其他路由器周期性交互，学习到整个自治系统的网络拓扑结构;并通过自治系统边界的路由器注入其他AS的路由信息，从而得到整个Internet的路由信息。每隔一个特定时间或当链路状态发生变化时，重新生成LSA，路由器通过泛洪机制将新LSA通告出去，以便实现路由的实时更新。

# 一：OSPF的基本概念和工作过程

### 1.1：OSPF路由协议概述

##### 1.1.1：自治系统（AS）

多个路由跑相同路由进程协议的区域 成为AS区域系统。
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xMzUxMzYyOTUucG5n?x-oss-process=image/format,png)

##### 1.1.2：内部网关协议（IGP）

在区域内部跑的进程协议

如：RIP，OSPF，ISIS等
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xMzUzNDQ4MTUucG5n?x-oss-process=image/format,png)

##### 1.1.3：外部网关协议（EGP）

在区域外跑的进程协议
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xMzU1MjI0MDUucG5n?x-oss-process=image/format,png)

##### 1.1.4：OSPF是链路状态路由协议

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xMzU4MDMwNDkucG5n?x-oss-process=image/format,png)

### 1.2：OSPF的工作过程

##### 1.2.1：建立邻居列表

如图，A通过建立邻接关系，学习到所有的链路状态信息，即所有的网段信息。

##### 1.2.2：链路状态数据库

A将学习到的链路状态信息存储在自己的链路状态数据库中。

##### 1.2.3：形成路由表

A的链路状态数据库通过 Dijkstra算法 算出A到达每一个地点的最短路径，形成最短路径树。最终生成路由表。
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDAwMjYwNTcucG5n?x-oss-process=image/format,png)
 )

### 1.3：OSPF的基本概念

##### 1.3.1：OSPF区域

OSPF在AS内划分多个区域，其中必须有个骨干区域，且骨干区域有且仅有一个。骨干区域负责区域间路由信息传播。

另，其他区域必须经过骨干区域转发，所有区域必须和骨干区域直接连接！

其他称作标准区域或非主干区域。

区域ID可以表示层一个十进制的数字。即area 0（0-9）

每个OSPF路由器只维护所在区域的完整链路状态信息
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDA1MTkxMTAucG5n?x-oss-process=image/format,png)

##### 1.3.2：Router ID

OSPF区域内唯一标识路由器的IP地址。
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDA2Mjg2NjAucG5n?x-oss-process=image/format,png)

##### 1.3.3：Router ID选取规则

优先选取loopback接口最为Router ID，因为loopback是路由器上的虚接口，这样的话，即使物理端口损坏也不影响Router ID。

也可以使用 router-id 命令指定Router ID。这个命令是我们常用的。
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDA5MTE3MjEucG5n?x-oss-process=image/format,png)

##### 1.3.4：DR 和 BDR

DR ，BDR 和其他路由中

1 DR： 区域当中的主路由，有且仅有一个

2 BDR:区域当中的备份路由，有且仅有一个

3 除了DR 和 BDR 都是其他路由

其他路由器只和 DR 和 BDR 形成邻接关系。主路由负责通告信息，备份路由负责准备顶替 DR

其他路由器发送信息只能到达DR 和BDR（一个组播） ，DR再发送通告信息（第二个组播）。其中存在两个组播信息。

DR 和 BDR 负责监控其他路由发来的信息。
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDEzMTYyOTgucG5n?x-oss-process=image/format,png)

##### 1.3.5：DR 和 BDR 的选举方法

路由优先级也被称为路由的“管理距离”，是一个正整数，范围0~255，它用于指定路由协议的优先级。

常见的OSPF路由优先级为110.
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDE3MzkzMzcucG5n?x-oss-process=image/format,png)

##### 1.3.6：DR 和 BDR 的选举过程

路由器的优先级可以影响一个选举过程，但是他不能强制更换已经存在的DR或BDR路由器。

即，我们第一个启动的OSPF路由器就会变成DR。第二个启动的OSPF的路由器会变成BDR。而第三个和以后开启的路由器即使路径再短，也无法更改现有的DR 和 BDR。
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDE4NDUzNTgucG5n?x-oss-process=image/format,png)

##### 1.3.7：OSPF的组播地址

224.0.0.5   DR/BDR发出的

224.0.0.6  其他路由发出的
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDE5NTE2MTEucG5n?x-oss-process=image/format,png)

##### 1.3.8：OSPF的度量值为COST

COST=10^8/BW    BW(带宽)   COST 数制越小越好，说明带宽越高

COST越低，带宽越高，路径越短。

最短路径是基于接口指定的代价cost计算的
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDIyMDMyODUucG5n?x-oss-process=image/format,png)

# 二：OSPF的数据包类型

### 2.1：OSPF数据包

承载在IP数据包内，使用协议号89
 ![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDIyNTQ5MTMucG5n?x-oss-process=image/format,png)

### 2.2：OSPF的包类型

| OSPF的包类型            | 描述                                                         |
| ----------------------- | ------------------------------------------------------------ |
| Hello包                 | 用于发现和维持邻居关系，选举DR 和BDR                         |
| 数据库描述包（DBD）     | 用于向邻居发送摘要信息以同步链路状态数据库                   |
| 链路状态请求包（LSR）   | 在路由器收到包含新信息的DBD后发送，用于请求更详细的信息      |
| 链路了状态更新包（LSU） | 收到LSR后发送链路状态通告（LSA），一个LSU数据包可能包含几个LSA |
| 链路状态确认包（LSAck） | 确认已经收到LSU，每个LSA需要被分别确认                       |

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDIzNTA1NzcucG5n?x-oss-process=image/format,png)

# 三：OSPF邻接关系

### 3.1：OSPF邻接关系的建立（7个状态）（重点）

| 状态                    | 描述                                                         |
| ----------------------- | ------------------------------------------------------------ |
| Down状态                | 只知道自己的ID，不知道其他任何路由器                         |
| Init状态（初始化状态）  | Down状态的端口接收到Hello信息后，自动激活init状态，此时，只能接收Hello包，不能发送Hello包 |
| 2-Way状态               | route系统加载完成后从Init状态进入2-Way状态。2-Way状态中既可以接收Hello包也可以发送Hello包（选举出两个最大的Router ID，但是并不会确定主从路由身份） |
| ExStart状态(准启动状态) | 确定主从路由身份。即确定DR和BDR身份。                        |
| Exchange状态            | 交换DBD信息库，同时接收到后也会有LSACK包。                   |
| Loading状态             | 最繁忙状态，包的种类最多，有LSR,LSU（包含多个LSA），LSACK，形成的路由表 |
| Full 状态               | 稳定状态开始转发数据包                                       |

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDM0MzA1NjkucG5n?x-oss-process=image/format,png)

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDQ2NDcyMTYucG5n?x-oss-process=image/format,png)

### 3.2：OSPF的网络类型

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDUxMTI2NjMucG5n?x-oss-process=image/format,png)

### 3.3：以下几方面考虑OSPF的使用（应用环境）

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDUyMjA3OTQucG5n?x-oss-process=image/format,png)

### 3.4：OSPF的特点（重点）

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDU0MDk1MjUucG5n?x-oss-process=image/format,png)

### 3.5：OSPF与RIP的比较

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyOC8xNDU2MTgyNTkucG5n?x-oss-process=image/format,png)

# 四：OSPF单域的配置

### 4.1：OSPF的基本配置命令

inverse-mask 反掩码=255减去正掩码

```css
启动OSPF路由进程
Router（config）#router ospf process-id  
指定OSPF协议运行的接口和所在区域
Router（config-router）#network address inverse-mask area area-id 
修改接口的优先级
Router（config-if）#ip ospf priority priority
修改接口的cost值
Router（config-if）#ip ospf cost cost
12345678
查看路由表
Router#show ip route
查看邻居列表及其状态
Router#show ip ospf neighbor
查看OSPF的配置
Router#show ip ospf
查看OSPF接口的数据结构
Router#show ip ospf interface type number
12345678
```

# 五：OSPF单域配置实验

### 5.1：实验目的

配置OSPF实现全网互通

### 5.2：环境

GNS3软件

三台初始化路由器

两台初始化主机

### 5.3：实验过程（七步）

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyMi8yMjQyMDQ0NzEucG5n?x-oss-process=image/format,png)

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyMi8yMjUyNTA3MzkucG5n?x-oss-process=image/format,png)

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyMi8yMzA5MTUwNzUucG5n?x-oss-process=image/format,png)

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyMi8yMzA4MTg4OTYucG5n?x-oss-process=image/format,png)

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyMi8yMzMxMjkwODMucG5n?x-oss-process=image/format,png)

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyMi8yMzMzNTA3MzgucG5n?x-oss-process=image/format,png)

![mark](https://imgconvert.csdnimg.cn/aHR0cDovL3Rhbmd6aGVuZy1waWNnby5vc3MtY24taGFuZ3pob3UuYWxpeXVuY3MuY29tL2ltZy8yMDE5MTAyMi8yMzM1MDY4MjcucG5n?x-oss-process=image/format,png)

### 5.4：总结

1.注意IP地址不要搞错

2.配置Router ID 命令：

int loopback 0

ip add 1.1.1.1 255.255.255.255

no shut

3.配置OSPF命令

router ospf 1（同一个区域，路由器的进程号必须相同）

router-id 1.1.1.1（进入router id）

network 192.168.10.0 0.0.0.255 area 0（宣告直连网段和区域）