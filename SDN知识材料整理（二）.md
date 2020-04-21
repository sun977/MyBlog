## SDN知识材料整理（二）

### 一、SDN的三种技术架构

#### 1、ONF定义的基于OpenFlow的架构

特点：
 1） 转发与控制分离
 2）标准化转发面
 优点：流量调度有很大优势

#### 2、IETE提出的技术架构

特点：
 1）开放现有网络设备的能力
 2）向应用层提供标准的API
 优点：充分利用了现有的网络设备和路路由协议，便于快速实现。

#### 3、NICIRA提出的Overlay技术架构（从传统网络中抽象出虚拟网络）

特点：
 1）网络边缘软件化
 2）overlay技术
 优点：实现了与物理网络的解耦，部署非常灵活。

#### 4、ETSI的NFV技术构架（网络功能虚拟化技术）主要应用在运营商网络

NFV与SDN互补，但是有本质的区别，所以严格意义上不能算是SND的架构。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200221012922823.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20200221012938210.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

### 二、SDN的四个平面

#### 1、数据平面

1）若干网元（Network Element）：
 包含一个或多个SDN 数据路径（ Datapath ）
 2）SDN Datapath：逻辑上的网络设备，负责转发和处理数据：
 控制数据平面接口（Control Data Plane Interface, CDPI）代理、转发引擎（Forwarding Engine）表和处理功能（Processing Function）
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200221013518216.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

#### 2、控制平面

1）北向接口：控制平面和应用平面之间的接口
 2）南向接口：控制平面和数据平面之间的接口
 3）控制平面的作用：a 将SDN应用层请求转换到SDN Datapath。b 为SDN应用提供底层网络的抽象模型（状态或事件）。
 控制平面的关键技术：
  控制器，网络操作系统（NOS）或网络控制器。
  智能、核心均在SDN 控制器中实现
  开 源 SDN 控 制 器 ： NOX 、 POX 、 FloodLight 、 RYU 、OpenDayLight、 ONOS等

#### 3、应用平面

1）SDN应用逻辑与北向接口驱动
 2）通过北向接口和控制平面交互
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200221014322903.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

#### 4、管理平面

静态的工作：网元初始化配置，指定控制器、定义控制器及应用的控制范围。

### 三、SDN的两大接口（北向接口和南向接口）

#### 1、北向接口----应用平面和控制平面之间

1）应用平面与控制平面之间的接口（NBI），向应用层提供抽象的网络视图，使应用能直接控制网络的行为。
 2）提供开放的、与产商无关的接口。
 北向接口关键技术
 a）SDN北向接口设计：控制器将网络能力封装后开放接口，供上层业务调用。
 b）REST API成为SDN北向接口的主流设计

#### 2、南向接口----控制平面和数据平面之间

1）控制平面和数据平面之间的接口（CDPI） 。
 2）功能：转发行为控制、设备性能查询、统计报告、事件通知等。
 3）ONF体系架构：标准化的南向接口协议（Openflow），不依赖于底层具体厂商的交换设备

南向接口关键技术
 a）转发面开放协议：允许控制器控制交换机的配置以及相关转发行为。
 b）ONF定义的转发面开放协议：Openflow协议。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200221015124751.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

### 4、SDN的核心思想（解耦，抽象，可编程性）

#### 1、解耦

解耦：数据平面与控制平面的解耦（即从传统的设备中分离出两个平面）
 1）通过解耦合，控制平面负责上层的控制决策，数据平面负责数据的交换转发，双方遵循一定的开放接口进行通信；
 2）实现网络逻辑集中控制的前提；
 3）两个平面独立完成体系结构和技术的发展演进，有利于网络的技术创新与发展。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/202002210158329.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)4）解耦带来的问题与挑战
 a 网络规模的扩大，单一控制器成为网络性能的瓶颈；
 b 保持分布式网络节点状态的一致性，是一个重要的挑战；
 c 响应延迟，导致数据平面的可用性问题。

#### 2、抽象（网络功能的抽象）

1）ONF网络构架实现转发抽象，分布状态抽象和配置抽象
 a-转发抽象（forwarding abstration）：隐藏了底层的硬件实现，转发行为与硬件无关；
 b-分布状态抽象（distribution abstration）：屏蔽分布式控制的实现细节，为上层应用提供全局网络视图；
 c-配置抽象（specification abstration）：网络行为的表达通过网络编程语言实现，将抽象配置映射为物理配置
 2）overlay网络构架实现对网络基础设施的抽象

#### 3、可编程性（网络可编程）

1）传统网络的管理接口： CLI、SNMP等，是初级的网络编程方式；
 2）网络管理者需要基于整个网络的，而不是基于某一设备的可编程，
 3）网络可编程相关研究：主动网络（Active Networking）、4D架构

SDN开放的可编程接口：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200221020620573.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)
 SDN可编程接口的作用：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200221020712983.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc0MjY1OA==,size_16,color_FFFFFF,t_70)

### 四，总结

对SDN知识体系的总结可以加深对知识点的理解，同时在整理的过程也是思考的过程。我喜欢一个人夜深人静学习，这时候思路异常的清晰。睡了睡了，明天继续。
 by 久违 2020.2.20