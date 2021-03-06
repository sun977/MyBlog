[一、SDN概述](https://blog.csdn.net/weixin_43265596/article/details/89787232#一、SDN概述)

[1.1 SDN概念](https://blog.csdn.net/weixin_43265596/article/details/89787232#1.1 SDN概念)

[1.2 SDN产生的原因](https://blog.csdn.net/weixin_43265596/article/details/89787232#1.2 SDN产生的原因)

[二、SDN架构](https://blog.csdn.net/weixin_43265596/article/details/89787232#二、SDN架构)

[2.1 SDN的基本架构](https://blog.csdn.net/weixin_43265596/article/details/89787232#2.1 SDN的基本架构)

[2.2 ONF定义的SDN架构](https://blog.csdn.net/weixin_43265596/article/details/89787232#2.2 ONF定义的SDN架构)

[1. 数据平面](https://blog.csdn.net/weixin_43265596/article/details/89787232#1. 数据平面)

[2. 控制平面](https://blog.csdn.net/weixin_43265596/article/details/89787232#2. 控制平面)

[3. 应用平面](https://blog.csdn.net/weixin_43265596/article/details/89787232#3. 应用平面)

[4. 管理平面](https://blog.csdn.net/weixin_43265596/article/details/89787232#4. 管理平面)

[5. SDN控制数据平面接口（CDPI）](https://blog.csdn.net/weixin_43265596/article/details/89787232#5. SDN控制数据平面接口（CDPI）)

[6. SDN北向接口（NBI）](https://blog.csdn.net/weixin_43265596/article/details/89787232#6. SDN北向接口（NBI）)

[三、SDN的核心概念](https://blog.csdn.net/weixin_43265596/article/details/89787232#三、SDN的核心概念)

[3.1 数据控制分离](https://blog.csdn.net/weixin_43265596/article/details/89787232#3.1 数据控制分离)

[3.1.1 数控分离历史](https://blog.csdn.net/weixin_43265596/article/details/89787232#3.1.1 数控分离历史)

[3.1.2 SDN数控分离](https://blog.csdn.net/weixin_43265596/article/details/89787232#3.1.2 SDN数控分离)

[3.1.3 SDN数控分离的优点](https://blog.csdn.net/weixin_43265596/article/details/89787232#3.1.3 SDN数控分离的优点)

[3.1.4 SDN数控分离面临的问题](https://blog.csdn.net/weixin_43265596/article/details/89787232#3.1.4 SDN数控分离面临的问题)

[3.2 抽象](https://blog.csdn.net/weixin_43265596/article/details/89787232#3.2 抽象)

[3.3 网络可编程](https://blog.csdn.net/weixin_43265596/article/details/89787232#3.3 网络可编程)

[3.3.1 网络可编程历史](https://blog.csdn.net/weixin_43265596/article/details/89787232#3.3.1 网络可编程历史)

[3.3.2 SDN可编程](https://blog.csdn.net/weixin_43265596/article/details/89787232#3.3.2 SDN可编程)

------

# 一、SDN概述

## 1.1 SDN概念

SDN是一种将网络控制功能与转发功能分离、实现控制可编程的新兴网络架构。这种架构将从控制层从网络设备转移到外部计算设备，使得底层的基础设施对于应用和网络服务而言是透明的、抽象的，网络可被视为一个逻辑的或虚拟的实体。

## 1.2 SDN产生的原因

- 传统网络及其设备的只可配置、不可编程
- 网络的分布式控制与管理架构带来的制约

# 二、SDN架构

## 2.1 SDN的基本架构

![img](https://img-blog.csdnimg.cn/20190503135616929.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI2NTU5Ng==,size_16,color_FFFFFF,t_70)

SDN采用了集中式的控制平面和分布式的转发平面，两个平面相互分离，控制平面利用控制—转发通信接口对转发平面上的网络设备进行集中式控制，并提供灵活的可编程能力，具备以上特点的网络架构都可以被认为是一种广义的SDN。

在 SDN  架构中，控制平面通过控制—转发通信接口对网络设备进行集中控制，这部分控制信令的流量发生在控制器与网络设备之间，独立于终端间通信产生的数据流量，网络设备通过接收控制信令生成转发表，并据此决定数据流量的处理，不再需要使用复杂的分布式网络协议来进行数据转发，如下图所示。

![img](https://img-blog.csdnimg.cn/20190503140022916.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI2NTU5Ng==,size_16,color_FFFFFF,t_70)

SDN  并不是某一种具体的网络协议，而是一种网络体系框架，这种框架中可以包含多种接口协议。如使用OpenFlow等南向接口协议实现SDN 控制器与  SDN 交换机的交互，使用北向 API实现业务应用与 SDN  控制器的交互。这样就使得基于SDN的网络架构更加系统化，具备更好的感知与管控能力，从而推动网络向新的方向发展。

## 2.2 ONF定义的SDN架构

ONF定义的架构共由四个平面组成，即数据平面、控制平面、应用平面以及右侧的控制管理平面。各平面之间使用不同的接口协议进行交互。

![img](https://img-blog.csdnimg.cn/20190503135616951.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI2NTU5Ng==,size_16,color_FFFFFF,t_70)

### 1. 数据平面

由若干王元组成，每个网元可以包含一个或多个SDN Datapath。每个SDN Datapath是一个逻辑上的网络设备，它没有控制能力，只是单纯用来转发和处理数据，它在逻辑上代表全部或部分的物理资源。一个SDN Datapath包含控制数据平面接口代理、转发引擎表和处理功能三部分。

### 2. 控制平面

即所谓的SDN控制器。SDN控制器是一个逻辑上集中的实体，它主要负责两个任务，一是将SDN应用层请求转换到SDN Datapath，二是为SDN应用提供底层网络的抽象模型（可以是状态、事件）。一个SDN控制器包含北向接口代理、SDN控制逻辑以及控制数据平面接口驱动三部分。SDN控制器只是要求逻辑上完整，因此它可以由多个控制器实例组成，也可以是层级式的控制器集群；从地理位置上讲，既可以是所有控制器实例在同一位置，也可以是多个实例分散在不同的位置。

### 3. 应用平面

由若干SDN应用组成，SDN应用时用户关注的应用程序。它可以通过北向接口与SDN控制器进行交互，即这些应用能够通过可编程方式把需要请求的网络行为提交给控制器。一个SDN应用可以包含多个北向接口驱动（使用多种不同的北向API），同时SDN应用也可以对本身的功能进行抽象、封装来对外提供北向代理接口，封装后的接口就形成了更为高级的北向接口。

### 4. 管理平面

负责一系列静态的工作，这些工作比较适合在应用、控制、数据平面外实现，比如对网元进行配置、指定SDN Datapath的控制器，同时负责定义SDN控制器以及SDN应用能控制的范围。

### 5. SDN控制数据平面接口（CDPI）

SDN CDPI是控制平面和数据平面之间的接口，它提供的主要功能包括：对所有的转发行为进行控制、设备性能查询、统计报告、事件通知。SDN一个很重要的价值就体现在CDPI的实现上，它应该是一个开放的、与厂商无关的接口。

### 6. SDN北向接口（NBI）

SDN NBI是应用平面和控制平面之间的一系列接口。它主要负责提供抽象的网络视图，并使应用能直接控制网络的行为，其中包含从不同层对网络及功能进行的抽象，这个接口也应该是一个开放的、与厂商无关的接口。

# 三、SDN的核心概念

SDN的核心思想就是要分离控制平面与数据平面，并使用集中式的控制器来完成对网络的可编程任务，控制器通过北向接口和南向接口协议分别与上层应用和下层转发设备实现交互。正是这种集中式控制和数据控制分离（解耦）的特点使SDN具有了强大的可编程能力，这种强大的可编程性使网络能够真正地被软件所定义，达到简化网络运维、灵活管理调度的目标，同时为了使SDN能够实现大规模的部署，就需要通过东西向接口协议支持多控制器间的协同。

## 3.1 数据控制分离

### 3.1.1 数控分离历史

**（1）ForCES**

![img](https://img-blog.csdnimg.cn/20190512160807393.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI2NTU5Ng==,size_16,color_FFFFFF,t_70)

一个满足 ForCES  规范的网络设备，其基本结构如图所示。可以看出，一个ForCES的网络单元（NE）可以包含至少一个（或多个，用于冗余备份）控制单元（CE）和多达几百个转发单元（FE）。每个FE包含一个或者多个物理介质接口  Fi/f，该接口用来接收从该网络单元外部来的报文或者将报文传输到其他的网络单元，这些FE接口的集合就是NE的外部接口。在网络单元外部还有两个辅助实体：CE管理者（CEM）和FE管理者（FEM），它们用来在配置阶段对相应的CE和FE进行配置。图中Fp为CE和FE间的接口（通信过程由ForCES协议的标准协议完成），其间可以经过一跳（Single  Hop）或多跳（Multi-Hop）网络实现。Fi表示FE间的接口，Fr表示CE间的接口，Fe表示CE管理者和CE间的接口，Ff表示FE管理者和FE间的接口，Fl表示CE管理者和FE管理者之间的接口。ForCES的这种架构具有底层资源功能模块以及控制面与转发面分离的特点，为新一代网络提供了较好的功能灵活性。

**（2）4D项目**

![img](https://img-blog.csdnimg.cn/20190512160807409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI2NTU5Ng==,size_16,color_FFFFFF,t_70)

4D项目倡导4个主要平面：数据平面基于决策平面产生的状态来处理报文；发现平面用于在网络中发现物理网元并创建逻辑标识符识别它们，决策平面定义了标识符的范围和特久化，并执行彼此间的自动发现和管理；扩散平面提供一个连接路由器或交换机的健壮、高效的通信基础结构，从而能够将决策面产生的状态扩散到数据面上，而自身不产生任何状态；决策平面用于处理网络控制诸如可达性、负载均衡、访问控制、安全和接口配置等功能。这样做的优势在于可以从分布式系统问题中独立出网络的控制逻辑，这种架构有助于实现更健壮、更安全的网络，同时便于对异构网络进行有效管理。

### 3.1.2 SDN数控分离

（1）从功能实现来说，控制平面的主要功能是建立本地的数据集合，该数据集合一般被称为路由信息库（RIB），RIB需要与网内其他控制平面实例的信息保持一致，这一点通常使用分布式路由协议（如 OSPF）来完成。

（2）接下来，控制平面需要基于RIB创建转发表，用于指导设备出入端口之间的数据流量转发。转发表通常被称为转发信息库（FIB）， FIB 需要经常在设备的控制和数据平面之间进行镜像，以保证转发行为与路由决策一致，因此，FIB实际上是两个平面之间连接的纽带。

（3）数据平面的主要功能是，根据RIB创建的FIB进行数据的高速转发。另外，数据平面还可以根据需要处理一些其他的服务功能，如较短的事件侦测时间等，这是因为某些服务有非常严格的性能需求，需要放在数据平面以保证快速执行。

 

### 3.1.3 SDN数控分离的优点

（1）全局集中控制和分布高速转发：这是SDN的最主要优势，一方面可以实现控制平面的全局优化；另一方面可以实现高性能的网络转发能力。

（2）灵活可编程与性能的平衡：SDN数控分离的设计更加平衡，以FIB为分界线实际上降低了SDN的编程灵活性，但是没有暴露商用设备的高速转发实现细节，因此也使得网络设备商更容易接受SDN的理念。

（3)开放性和IT化：数据控制分离在一定程度上可以降低网络设备和控制软件的成本。当前的网络设备是捆绑控制平面功能软件一起出售的，由于软件开发由网络设备公司完成，对用户不透明，因此网络设备及其控制平面软件的定价权完全掌握在少数公司手中，造成了总体价格高昂。在数据控制平面分离以后，尤其是使用开放的接口协议后，将会实现交换设备的制造与功能软件的开发相分离，这样可以实现模块的透明化，从而有效降低成本。

### 3.1.4 SDN数控分离面临的问题

（1）可扩展性问题：这是SDN面临的最大问题，数据控制分离后，原来分布式的控制平面集中化了，即随着网络规模扩大，单个控制节点的服务能力极有可能会成为网络性能的瓶颈（即单点故障）。

（2）一致性问题：在传统网络中，网络状态一致性是由分布式协议保证的，在SDN数据控制分离后，集中控制器需要负起这个责任，如何快速侦测到分布式网络节点的状态不一致性，并快速解决这类问题。

（3）可用性问题：可用性是指网络无故障的时间占总时间的比例，传统网络设备是高可用的，即发向控制平面的请求会实时得到响应，因此，网络比较稳定，但是在SDN数据控制分离后，控制平面网络的延迟可能会导致数据平面可用性问题。

## 3.2 抽象

ONF网络架构实现转发抽象、分布状态抽象和配置抽象。

（1）转发抽象是数据平面抽象成通用的转发模型，隐藏了底层的硬件实现，转发行为与硬件无关，如MAC表、MPLS标签表、路由表、ACL访问控制列表等抽象成统一的流表。

（2）分布状态抽象屏蔽分布式控制的实现细节，为上层应用提供全局网络视图。

（3）配置抽象是网络行为的表达通过网络编程语言实现，将抽象配置映射为物理配置。Overlay网络架构实现对基础网络设施的抽象。

## 3.3 网络可编程

### 3.3.1 网络可编程历史

传统网络根本没有可编程这个概念。

1.主动网络

主动网络的基本思想是，打破传统网络只能被动传输信息的模式，允许网络中的节点在用户数据上执行用户所需的计算。例如，主动网络的用户可以向网络中的主动节点（如路由器）发送一个定制化的压缩程序，并要求该节点收到相应的包时都执行这个压缩程序。DARPA主动网络架构可以划分成3个主要层次：主动应用（AA）、执行环境（EE）和节点操作系统（Node OS），如图所示。

![img](https://img-blog.csdnimg.cn/20190512160807412.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI2NTU5Ng==,size_16,color_FFFFFF,t_70)

（1）主动应用（AA）是一个协议的程序代码，它通过主动分组加载到主动节点中，并在主动节点中对分组进行转发和计算来完成某种通信功能。

（2）执行环境（EE）是在Node OS上的一个用户级操作系统，它可以同时支持多个AA的执行，并负责AA之间的互相隔离。EE为AA提供了一个可调用的编程接口，一个主动网络节点可以具有多个执行环境，每一种执行环境完成一种特定的功能。

（3）节点操作系统（Node  OS）类似于一般操作系统的内核，它位于主动网络节点最底层的功能层次，管理和控制对主动网络节点硬件资源的使用。因此，EE在Node  OS中运行，一个Node OS可以并发地支持多个EE，协调EE对节点中可利用资源（内存区域、CPU 周期、链路带宽等）的使用。

2.主动网络的数据类型

（1）封装模型

![img](https://img-blog.csdnimg.cn/20190512160807431.png)

节点的可执行代码被封装在数据分组内，为in-band方式。这种模型利用数据分组携带代码从而在网络中添加新的功能，同时使用缓存来改善代码分发的效率，而可编程路由器根据数据分组的分组头由管理员定义一系列的操作行为。如图是主动网络封装报文的一种格式，其中包含了IP报文、可执行的程序码和用户数据，交换设备会根据原先的源目的地址来转发报文。可以看到，每条消息甚至每个报文都携带了一段可执行的代码，当报文到达交换机或路由器后，报文中的代码就会被分发到每个交换机的可执行环境中，然后控制交换机的行为或者修改报文。

（2）可编程路由器/交换机模型

![img](https://img-blog.csdnimg.cn/20190512160807429.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI2NTU5Ng==,size_16,color_FFFFFF,t_70)

节点的可执行代码被封装在数据分组内，为in-band方式。这种模型利用数据分组携带代码从而在网络中添加新的功能，同时使用缓存来改善代码分发的效率，而可编程路由器根据可编程路由器/交换机模型数据分组的分组头由管理员定义一系列的操作行为。如图  是主动网络封装报文的一种格式，其中包含了IP报文、可执行的程序码和用户数据，交换设备会根据原先的源目的地址来转发报文。可以看到，每条消息甚至每个报文都携带了一段可执行的代码，当报文到达交换机或路由器后，报文中的代码就会被分发到每个交换机的可执行环境中，然后控制交换机的行为或者修改报文。

### 3.3.2 SDN可编程

（1）SDN可编程通过为开发者们提供强大的编程接口，从而使网络有了很好的编程能力。对上层应用的开发者来说，SDN的编程接口主要体现在北向接口上，北向接口提供了一系列丰富的API，开发者可以在此基础上设计自己的应用而不必关心底层的硬件细节，就像目前在x86体系的计算机上编程一样，不用关心底层寄存器、驱动等具体的细节。SDN南向接口用于控制器和转发设备建立双向会话，通过不同的南向接口协议， SDN  控制器就可以兼容不同的硬件设备，同时可以在设备中实现上层应用的逻辑。SDN的东西向接口主要用于控制器集群内部控制器之间的通信，用于增强整个控制平面的可靠性和可拓展性。

（2）可编程能力体现在很多的层次上，从下往上依次为芯片可编程（如P4、POF）、FIB可编程（如OpenFlow）、RIB可编程（如BGP、PCEP）、设备OS可编程、设备配置可编程（如CLI、NETCONF/YANG、OVSDB）、控制器可编程和业务可编程（如GBP、NEMO）。