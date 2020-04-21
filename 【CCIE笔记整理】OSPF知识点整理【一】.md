## 【CCIE笔记整理】OSPF知识点整理【一】



### 目录

- - [【CCIE笔记整理】OSPF知识点整理【一】](https://blog.csdn.net/weixin_42742658/article/details/105071501#CCIEOSPF_0)

  - - [OSPF介绍：](https://blog.csdn.net/weixin_42742658/article/details/105071501#OSPF_3)

    - [1、OSPF的基本原理：](https://blog.csdn.net/weixin_42742658/article/details/105071501#1OSPF_15)

    - [2、OSPF的网络类型：](https://blog.csdn.net/weixin_42742658/article/details/105071501#2OSPF_31)

    - - - - [详细如下：](https://blog.csdn.net/weixin_42742658/article/details/105071501#_38)

    - [3、OSPF的路由类型：](https://blog.csdn.net/weixin_42742658/article/details/105071501#3OSPF_76)

    - [4、OSPF的三张表（邻居表，拓扑表--链路状态数据库，路由表）：](https://blog.csdn.net/weixin_42742658/article/details/105071501#4OSPF_83)

    - [5、OSPF的五种报文：](https://blog.csdn.net/weixin_42742658/article/details/105071501#5OSPF_91)

    - [6、OSPF的 LSA 类型：](https://blog.csdn.net/weixin_42742658/article/details/105071501#6OSPF_LSA__103)

    - - - [在OSPF中，OE1和OE2的区别：](https://blog.csdn.net/weixin_42742658/article/details/105071501#OSPFOE1OE2_141)

        - - [路由优先级（cost小更优先）：O > O IA > O E1 > O E2](https://blog.csdn.net/weixin_42742658/article/details/105071501#costO__O_IA__O_E1__O_E2_146)

    - [7、OSPF的末节（Stub）区域：](https://blog.csdn.net/weixin_42742658/article/details/105071501#7OSPFStub_148)

    - - - [Stub区域的由来：](https://blog.csdn.net/weixin_42742658/article/details/105071501#Stub_149)
        - [Stub区域的定义和作用：（阻止了四号和五号LSA进入）](https://blog.csdn.net/weixin_42742658/article/details/105071501#StubLSA_151)
        - [完全末节区域和非完全末节区域：](https://blog.csdn.net/weixin_42742658/article/details/105071501#_154)

    - [8、OSPF邻居的建立：](https://blog.csdn.net/weixin_42742658/article/details/105071501#8OSPF_174)

    - - - [建立邻居的4个阶段：](https://blog.csdn.net/weixin_42742658/article/details/105071501#4_175)
        - [邻居的状态：](https://blog.csdn.net/weixin_42742658/article/details/105071501#_182)
        - [邻居建立的必要条件：](https://blog.csdn.net/weixin_42742658/article/details/105071501#_199)

    - [9、OSPF的宣告：](https://blog.csdn.net/weixin_42742658/article/details/105071501#9OSPF_224)

    - [10、OSPF的认证：](https://blog.csdn.net/weixin_42742658/article/details/105071501#10OSPF_251)

    - [11、OSPF的路由汇总：](https://blog.csdn.net/weixin_42742658/article/details/105071501#11OSPF_306)

    - [12、OSPF的虚链路：](https://blog.csdn.net/weixin_42742658/article/details/105071501#12OSPF_318)

    - [OSPF多区域案例图：](https://blog.csdn.net/weixin_42742658/article/details/105071501#OSPF_344)

    - [OSPF知识结构图：](https://blog.csdn.net/weixin_42742658/article/details/105071501#OSPF_346)

    - [后续【CCIE笔记整理】OSPF知识点整理【二】将扩充以下内容：](https://blog.csdn.net/weixin_42742658/article/details/105071501#CCIEOSPF_351)

    - - - [OSPF的路由重分发（路由相互引入）：](https://blog.csdn.net/weixin_42742658/article/details/105071501#OSPF_353)
        - [OSPF的度量（cost）：](https://blog.csdn.net/weixin_42742658/article/details/105071501#OSPFcost_354)
        - [OSPF默认路由注入：](https://blog.csdn.net/weixin_42742658/article/details/105071501#OSPF_355)
        - [OSPF管理距离的应用：](https://blog.csdn.net/weixin_42742658/article/details/105071501#OSPF_356)
        - [OSPF综合实验：](https://blog.csdn.net/weixin_42742658/article/details/105071501#OSPF_357)



### OSPF介绍：

OSPF开放最短路径优先协议（Open Shortest Path First,OSPF）。OSPF是一个链路状态协议，与所有的距离矢量协议相比，ospf一个主要的特点是他的收敛速度快，这使得它可以支持更大型的网络，它的特征有：

- 1）收敛速度快，适用于大型网络。
- 2）是无类别的路由协议，支持不连续子网，VLSM和CIDR以及手工汇总。
- 3）支持区域划分，结构化网络，这使得SPF计算频率更低，链路状态数据库和路由表更小，链路状态更新的开销更低。
- 4）支持简单口令和MD5认证
- 5）采用触发更新，无路由环路，还可以使用路由标记（Tag）进行外部路由的监控。
- 6）支持等价负载均衡
- 7）OSPF路由协议的甘管理距离（AD）是110.
- 8）OSPF采用链路的开销（cast）作为链路度量标准。
- 9）为了确保LSDB（链路状态数据库）同步，每个30分钟进行一次链路状态刷新。

### 1、OSPF的基本原理：

- 1、  宣告OSPF的路由器从所有启动OSPF进程的接口上发出hello数据包。
- 2、  邻接关系的建立是由交换Hello信息的路由器类型和网络类型决定的。
- 3、  每一台路由器都会在所有形成邻接关系的邻居之间发送链路状态通告（LSA），LSA描述了路由器所有链路、接口、路由器的邻居以及链路状态信息。
- 4、  每一台收到从邻居（neighbor）发出的LSA的路由器都会把这些LSA记录在自己的链路状态数据库（LSDB）中，并且发送一份LSA备份给其他的邻居neighbors。
- 5、  通过LSA泛洪扩散到整个区域，区域内所有路由器都会形成相同的LSDB。
- 6、  当这些路由器的LSDB完全相同时，每一台路由器将以自身为根，使用SPF算法计算出一个无环拓扑，描述自己所知道的到达每一个目的地的最短路径。
- 7、  每一台路由器都将从SPF算法树中构建出自己的路由表。 
  - 1. 区域内路由（最优）
  - 1. 区域间路
  - 1. E1外部路
  - 1. E2外部路

OSPF邻居之间交换的Hello数据包称为keepalive，并且每30min重传一次LSA。

### 2、OSPF的网络类型：

- 1、点到点网络类型（point-to-point）：
- 2、广播型网络（broadcast）：
- 3、非广播多路访问（NBMA）：
- 4、点到多点网络（point-to-multipoint）：
- 5、虚链路（virtual links）：

###### 详细如下：

- 1、点到点网络（point-to-point）：
   如果数据链路层封装的是HDLC或者PPP协议的，在运行ospf的时候，默认的网络类型就是点到点网络。是连接单独的一对路由器的。 【默认串口连接】
   \#show interface 接口 【查看接口底下的封装方式，HDLC或者PPP】
   \#show ip interface 接口 【查看该接口的网络类型Network Type】
   注： 如果两台路由器是以太网连接的，也不存在第三个路由器，这个时候可以选择把网络类型改成点到点网络。
   修改方式:

```
#int fa0/0
#ip ospf network point-to-point
```

- 2、广播型网络（broadcast）：
   广播型网络，像以太网络，ethernet封装，在运行ospf的时候默认就是广播型网络，hello间隔10s，dead间隔40s，dead间隔是hello间隔的4倍。能自动发现邻居。会选举 指定路由器（DR）和  备份指定路由器（BDR）。DR和BDR会监听224.0.0.6这个地址，其他路由器会向这个地址发送消息。DR会向224.0.0.5这个地址发送消息，其他路由器监听这个地址，获取DR发送的消息。
   DR和BDR的选举：：
   1）每台路由器先比较优先级大小（默认优先级是1），在比较router-id大小，大的为DR，次大的为BDR。
   2）DR和BDR的选举是稳定的，所以选举结果一旦形成，就不会更改DR和BDR的身份（有新的更大的router-id的路由器加入到网络中也不会改变原有的DR和BDR）。除非出现故障，重新选举。
   3）其他路由器和DR，BDR之间只能形成FULL的邻接关系，DRother之间只能形成 2-way 的关系，这是正常状态。
   修改路由器默认优先级的方法：

```
#int fa0/0
#ip ospf priority 255 【1~255，数字与大优先级越高】
```

- 3、非广播多路访问（NBMA）：
   NBMA网 络,像 X,25、 帧中继和 ATM等,可 以连接两台以上的路由器,但 是它们没有广播数据包的能力 。 一 台在  NBMA网络上的由器发送的数据包将不能被其他与之相连的路由器收到 。 结果是,在这些网络上的路由器有必要增加另外的配置来获得它们的邻居。
   在 NBMA网络上的0SPF路由器需要选举 DR和 BDR,并 且所有的 0SPF数据包都是单播的。
   像封装成Frame-relay的网络，运行ospf的时候默认就是NBMA网络，这种网络不能自己发现邻居，需要手动配置，hello间隔30s，dead间隔120s，也会选举DR和BDR。
- 4、点到多点网络（point-to-multipoint）：
   点到多点网络（有一种说法叫P-to-MP网络），让每一个节点都和其他节点之间形成邻居关系，直接传递信息。这种方式不需要选举DR和BDR。OSPF数据包以单播的形式发送给每一个邻居。这种网络适合于各种拓扑，缺点在于交互复杂。不是ospf默认的网络类型，可以手动设置，hello间隔30s，dead间隔120s。配置方法：

```
#int s1/0  【互联的路由器的每个接口都要设置】
#ip ospf network point-to-multipoint

```

- 5、虚链路（virtual links）：
   虚链路将在后面部分讲述,它可以被路由器认为是没有编号的点到点网络的一种特殊置。在虚链路上0SPF数据包是以单播方式发送的。

### 3、OSPF的路由类型：

- 1、内部路由器（Internal Router）：所有接口都在同一个区域内的路由器。
- 2、主干路由器（Backbone Router）：至少有一个接口连接骨干区域（area 0）的路由器。【内部路由器也是主干路由器】
- 3、区域边界路由器（ABR）：路由器连接多个区域（其中一个区域必须是骨干区域area 0），对于每一个区域都有一个独立的链路状态数据库。
- 4、自制系统边界路由器（ASBR）：与AS外部相连的路由器。同一台路由设备可能既是ABR又是ASBR。ASBR可以认为是和外界通信的路由器，它负责学习外部的其他路由协议产生的路由，把它们通过重分发的方式注入到本ospf区域。
- 【图：各个路由器角色】

### 4、OSPF的三张表（邻居表，拓扑表–链路状态数据库，路由表）：

- 1、邻居表（Neighbor Table）：OSPF用邻居机制来发现和维持路由的存在，邻居表存储了双向通信的邻居关系OSPF路由器列表的信息。
- 2、拓扑表（Topology Table）：OSPF用LSA（Link State Advertisement 链路状态通告）来描述网络拓扑信息，然后OSPF路由器用拓扑数据库来存储网络的这些LSA。
- 3、路由表（Routing Table）：对链路状态数据库进行SPF（Dijkstra）计算，而得出的OSPF路由表。
   OSPF 网络结构：自治系统，区域
   OSPF 算法：Dijkstra’s SPF 算法。
   OSPF 成员类型：指定路由器 (DR) ,  ==备份指定路由器 (BDR) ==, 其他路由 (DRother)。

### 5、OSPF的五种报文：

OSPF报文封装在IP报文的负载中，不使用TCP，而使用LSAck实现自己的确认机制。

- 1、Hello：  建立并维护邻居关系。hello组播地址 224.0.0.5/6。【DRother通知所有的DR/BDR使用组播地址224.0.0.6，DR通知DRother使用组播地址224.0.0.5】
- 2、DBD：   DatabaseDescribe 数据库描述，建立邻居时发送，描述自身接口状态。
- 3、LSR ：  LinkState Request 链路状态请求，向邻居请求。
- 4、LSU：   LinkState Update  链路状态更新，发送的是LSA。【LSA是属于LSU里面的消息】
- 5、LSAck：  对DBD、LSR、LSU进行确认

LSA的老化时间是3600s，正常情况下每隔1800s，LSA会全部刷新一遍。
 OSPF的序列号，用于判断这个LSA是否是最新LSA。
 序列号范围：0x80000001~0x7fffffffffff。

### 6、OSPF的 LSA 类型：

- 1、一号LSA：路由器LSA（Router Link）
   \* 谁产生：区域内的每个路由器都会产生。
   \* 传递范围：只能在本区域内传递。
   \* 作用：描述区域内的拓扑情况，链路情况，形成区域内的路由。O的路由描述这个路由器是不是ABR或者ASBR。
   \* 查看：#show ip ospf database router
- 2、二号LSA：网络LSA（Net Link）：【有指定路由器（DR）的网络才会产生】
  - 谁产生：指定路由器（DR）产生。
  - 传递范围：区域内部传递。
  - 作用：告诉其他的路由器（DRother路由器），本区域所有连接的路由器的Router-ID以及掩码。
  - 查看：#show ip ospf database network
- 3、三号LSA：网络汇总LSA（Summary Net）：【传递过程中产生者改变】
  - 谁产生：区域边界路由器（ABR）产生。
  - 传递范围：整个OSPF网络传递，每经过一个ABR，产生者就会变成那个ABR。
  - 作用：描述区域间的路由，OIA的路由，一个LSA就是一个路由。告诉本区域路由器如何去往别的区域。
  - 查看：#show ip ospf database summary
- 4、四号LSA：ASBR汇总LSA（ASBR Summary LSA）：
  - 谁产生：区域边界路由器（ABR）产生。
  - 传递范围：整个OSPF网络传递。
  - 作用：向其他区域的路由器描述谁是自制系统边界路由器（ASBR），即指向ASBR路由器 。
  - 查看：#show ip ospf database asbr-summary
- 5、五号LSA：自制系统外部汇总LSA（External LSA）：【传递过程中产生者不变】
  - 谁产生：自制系统边界路由器（ASBR）产生。
  - 传递范围：整个OSPF网络传递。
  - 作用：描述了AS之外的外部路由。告诉本自治区内的路由器如何通往外部AS。
  - 查看：#show ip ospf database external
- 6、七号LSA：NSSA外部LSA（NSSA External LSA ）：【NSSA 非完全末节区域】
  - 谁产生：ASBR产生，关于NSSA的信息。
  - 传递范围：在NSSA区域内传递。
  - 作用：产生关于NSSA区域的信息，在传出本区域的时候，ABR可以将七号LSA装换为五号LSA给其他区域学习。
- 7、注意：一，三，五号LSA携带路由信息，二和四号LSA不携带路由信息。    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324162047552.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)路由标识符表：
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200324162239162.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

##### 在OSPF中，OE1和OE2的区别：

OE1：在传递过程中，度量是根据链路的cost进行增加。
 OE2：在传递过程中，度量是不变的，不去计算OSPF内部链路的cost。【默认引入的时候就是OE2，默认度量20】

###### 路由优先级（cost小更优先）：O > O IA > O E1 > O E2

### 7、OSPF的末节（Stub）区域：

##### Stub区域的由来：

一个学习了大量外部路由的ASBR路由器，将大量的路由信息引入到内部区域，这将大大的占用内部区域的资源，导致内部区域的性能低下。为了减少大量的外部路由信息，可以将内部区域做成stub区域，stub区域不接受外部的路由条目，而改用默认路由代替这些外部路由，这样就减少了内部区域的路由条目，使性能提高。

##### Stub区域的定义和作用：（阻止了四号和五号LSA进入）

stub区域是一个不允许AS外部LSA通告器内部进行泛洪扩散的区域。如果一个区域内没有五号LSA，那么四号LSA也就没有存在的必要了。所以Stub区域阻止了四号和五号LSA的进入。当把一个区域设置成stub区域时，区域边界路由器（ABR）会自动向该区域注入三号LSA的默认路由（默认路由是由三号LSA通告的，所以不会传递到这个区域外部）。

##### 完全末节区域和非完全末节区域：

- 1、完全末节区域：不仅阻止了四号和五号LSA，使用缺省默认路由到达OSPF自制系统外部，还同时阻止了三号LSA。它阻止了所有的汇总LSA，除了唯一一条缺省默认的三号LSA。
- 2、非完全末节区域：允许外部路由通告到ospf自制系统内部，而同时保留自制系统其余部分的末节区域特征。即NSSA区域，允许引入本区域的路由器引入外部路由，但是不允许其他区域的外部路由进来。NSSA区域引入的路由是以七号LSA的方式在本区域内传递，在传出这个区域的时候，ABR会将七号LSA转成五号LSA向外传递。这里注意：ABR 不会自动注入默认路由向本区域，需要管理员在ABR上手动配置默认路由。【这一点与stub区域不同】

```
#router ospf 1
#area 2 nssa default-information-originate 【ABR上手工注入默认路由的方法】
```

| 区域类型\LSA类型       | 1 和 2 号LSA | 3号LSA                     | 4号LSA | 5号LSA | 7号LSA |
| ---------------------- | ------------ | -------------------------- | ------ | ------ | ------ |
| 骨干区域（area 0）     | 允许         | 允许                       | 允许   | 允许   | 不允许 |
| 非骨干区域，非末节区域 | 允许         | 允许                       | 允许   | 允许   | 不允许 |
| 末节区域               | 允许         | 允许                       | 不允许 | 不允许 | 不允许 |
| 完全末节区域           | 允许         | 不允许（只有一条默认路由） | 不允许 | 不允许 | 不允许 |
| 非完全末节区域（NSSA） | 允许         | 允许                       | 允许   | 不允许 | 允许   |

### 8、OSPF邻居的建立：

##### 建立邻居的4个阶段：

- 1、邻居路由器发现阶段
- 2、双向通信阶段：当两台相互连接的路由器在他们的Hello数据包中都互相列出来对方路由器的router-id的时候，路由器的双向通信阶段就算完成了。
- 3、数据库同步阶段：路由器之间进行交互数据库描述，链路状态请求，链路状态更新和链路状态确认数据包信息，以便确保邻居的链路状态数据库中包含相同的数据库信息。
- 4、完全邻接阶段（full adjacency）。
   查看邻居：#show ip ospf neighbor

##### 邻居的状态：

OSPF路由器需要邻居路由器在几种邻居状态之间转换后 (在邻居数据结构中讲述),才能形成邻居之间的完全邻接关系 （full adjacency）。

- 1、失效状态（Down）：这是一个邻居会话的初始状态，用来指明在最近一个dead间隔内还没有收到邻居的hello包。
- 2、尝试状态（Attempt）：这种状态仅仅适用于NBMA网络上的邻居，在NBMA网络中，邻居是手工配置的。
- 3、初始状态（Init）：这一状态表明在最近的一个dead间隔内，路由器收到了邻居的hello包，但是双向通信阶段还未建立。
- 4、双向通信状态（2-way）：这一状态表明本地的路由器已经在来自邻居的hello包中看到了自己的路由器router-id，双向通信的会话建立成功。
- 5、信息交换初始状态（ExStart）：在这种状态下，本地路由器和它的邻居讲建立主从关系，并确定数据库描述数据包的序列号，以便为数据库描述文件的信息交互做准备。这里router-id高的将作为主路由器。
- 6、信息交换状态（Exchange）：在这状态下，本地路由器会和它的邻居交换数据库描述数据包。同时也会发送链路状态请求数据包给邻居路由器，用来请求最新的LSA。
- 7、信息加载状态（Loading）：在这状态下，邻居间交互发送链路状态请求数据包，用来请求最新的LSA通告，本地路由器接收这些LSA通告。
- 8、完全邻接状态（FULL）：邻居关系完全建立。

注：在邻居关系的创建中，OSPF协议使用了五种数据包（报文）中的以下3中类型的数据包（报文）：
 1）数据库描述数据包（DBD）
 2）链路状态请求数据包（LSR）
 3）链路状态更新数据包（LSU）

##### 邻居建立的必要条件：

- 1、认证要一致：认证方式和认证秘钥都一致 【后面介绍OSPF的认证】
- 2、区域号要一致：【area 0之类的】
- 3、hello间隔要一致：

```
#int 接口
#ip ospf hello-interval 10  【设置hello间隔的方法】
```

- 4、dead间隔要一致：

```
#int 接口
#ip ospf dead-interval 40  【设置dead间隔的方法】
```

- 5、如果配置了stub区域或者NSSA区域，那么区域类型也要一致：

```
#router ospf 1 
#area 1 stub  【修改区域类型的方式】
```

- 6、网络类型要一致：

```
#int 接口
#ip ospf network point-to-point 【修改网络类型的方式】
```

### 9、OSPF的宣告：

OSPF宣告一般有3种方式：

- 1、精确宣告：宣告路由的接口地址

```
#router ospf 1 
#router-id 1.1.1.1
#network 192.168.12.1 0.0.0.0 area 0 
#network 172.16.12.1 0.0.0.0 area 0 
```

- 2、网段式宣告：

```
#router ospf 1 
#router-id 2.2.2.2
#network 192.168.12.0 0.0.0.255 area 1
#network 172.16.12.0 0.0.0.255 area 1

```

- 3、接口宣告：

```
#router ospf 1
#router-id 3.3.3.3
#int s1/1
#ip ospf 1 area 0 
#int lo0 
【环回口作为主机对待的时候，会默认变成32位的掩码，这里为了让它显示原来的掩码，需要改变它的网络类型为点到点网络】
#ip ospf 1 area 0 
```

### 10、OSPF的认证：

OSPF认证从安全性角度讲，可以分为：明文认证 和 密文认证
 从开启方式来讲可以分为：区域开启认证 和 接口开启认证 【若两种同时存在，接口认证优先】
 合格的认证分为认证方式和认证秘钥两部分

- 1、开启区域明文认证：

```
R1
#router ospf 1
#area 0 authentication
```

- 2、开启接口明文认证：

```
R2
#int s1/1【假设S1/1和R1相连】
#ip ospf authentication   【虽然R1和R2开启地方（一个区域，一个接口）不一样，但是配置完成后两者可以建立邻居关系】
```

- 3、开启接口明文+秘钥认证：

```
R1
#int s1/0 【假设S1/0与R2相连】
#ip ospf authentication   【开认证】
#ip ospf authentication-key cisco  【配秘钥（这里秘钥是明文传输），注意后面不要有空格】
R2
#int s1/1 【假设S1/1与R1相连】
#ip ospf authentication 
#ip ospf authentication-key cisco
```

- 4、开启区域密文+秘钥认证：

```
R1
#router ospf 1
#area 0 authentication message-digest  【密文，信息摘要算法】
#int s1/0
#ip ospf authentication-key md5 cisco  【只能在接口下做】
R2
#router ospf 1
#area 0 authentication message-digest 
#int s1/1
#ip ospf authentication-key md5 cisco  【MD5算法加密了秘钥cisco】

```

- 5、开启接口密文+秘钥认证：

```
R1
#int s1/0
#ip ospf authentication message-digest
#ip ospf message-digest-key 1 md5 cisco 
R2
#int s1/1
#ip ospf authentication message-digest
#ip ospf message-digest-key 1 md5 cisco 
```

### 11、OSPF的路由汇总：

- 1、区域内间路由汇总（以区域为单位）：在ABR上汇总

```
ABR(config-router)#area 1 range 172.16.0.0 255.255.252.0 【ABR上汇总OSPF area 1的路由】
```

- 2、外部路由汇总（以AS为单位）：在ASBR上汇总

```
ASBR(config-router)#summary-address 172.16.0.0 255.255.252.0
```

### 12、OSPF的虚链路：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200325013448201.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)如图所示，图中的area 0 和area 2之间没有直接相连，夹着一个area 1，所以area 2成了一个孤岛，现在想让area 2 也连接到骨干区域area 0，实现这个需求的技术就是虚链路。虚链路经过的区域area 1 在这里叫做传送区。R1是ABR，但是R2不是ABR，虚链路技术可以使得R2也具有ABR的功能。

```
配置：
R1
#router ospf 1 
#router-id 1.1.1.1
#area 1 virtual-link 2.2.2.2  【对端的router-id】
R2
#router ospf 1 
#router-id 2.2.2.2
#area 1 virtual-link 1.1.1.1  【对端的router-id】
```

查看虚链路：#show ip ospf virtual-link
 注：
 1）虚链路只是一种修复无法避免的网络拓扑问题的一种临时手段，一般不用。
 2）图中这条虚链路是链接area 0的链路，虚链路的hello间隔是10s，dead间隔是40s，一旦虚链路成型，hello报文会被抑制们无法送达。
 3）因为虚链路是area 0的链路，所以如果area 0做了区域的认证，虚链路也会继承。
 4）若果area 0被分割，也将用到虚链路技术。

OSPF Virtual-Link的创建规则：
 1）Virtual-link必须配置在两台ABR之键。
 2）配置了Virtual-link所经过的区域必须拥有全部的路由选择信息，即必须是传送区（Transit Area）。
 3）传送区（Transit Area）不能是Stub Area。
 4）另外，如果网络中有Virual-link存在，则被认为该网络是一个设计的比较糟糕的网络。

### OSPF多区域案例图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200325020232716.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

### OSPF知识结构图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200325020335968.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

### 后续【CCIE笔记整理】OSPF知识点整理【二】将扩充以下内容：

##### OSPF的路由重分发（路由相互引入）：

##### OSPF的度量（cost）：

##### OSPF默认路由注入：

##### OSPF管理距离的应用：

##### OSPF综合实验：

by 久违 2020.3.25