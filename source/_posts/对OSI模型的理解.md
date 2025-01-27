---
title: 对OSI模型的理解
tags:
  - 网络
categories: []
date: 2020-12-26 00:00:00
---


​		OSI模型各层功能的正式定义说实话，说的就不是个人话。学完之后还是有点懵。就如网络层之间能不能直接进行通信？书上的概念给的挺暧昧的，感觉好像能。在翻了很多解释后，也终于对osi模型有了更深刻的认知。

​		书上是自底向上介绍的，但我个人觉得自顶向下更容易理解。所以我这里从上往下介绍并给出比喻，可能有些不准确。参考了另一位的文章，将其比喻为一个公司收发快递的过程，并对我认为其描述不完善的地方做了一些补充和更改。

<!-- more -->

<1>  应用层

​    OSI参考模型中最靠近用户的一层，是为计算机用户提供应用接口，也为用户直接提供各种网络服务。

​    <font color=red>实际公司A的老板就是我们所述的用户，而他要发送的商业报价单，就是应用层提供的一种网络服务，当然，老板也可以选择其他服务，比如说，发一份商业合同，发一份询价单，等等。</font>

<2>  表示层

​    表示层提供各种用于应用层数据的编码和转换功能,确保一个系统的应用层发送的数据能被另一个系统的应用层识别。如果必要，该层可提供一种标准表示形式，用于将计算机内部的多种数据格式转换成通信中采用的标准表示形式。数据压缩和加密也是表示层可提供的转换功能之一。

​    <font color=red>由于公司A和公司B是不同国家的公司，他们之间的商定统一用英语作为交流的语言，所以此时表示层（公司的文秘），就是将应用层的传递信息转翻译成英语。同时为了防止别的公司看到，公司A的人也会对这份报价单做一些加密的处理。这就是表示的作用，将应用层的数据转换翻译等。</font>

<3>  会话层

​    会话层就是负责建立、管理和终止表示层实体之间的通信会话。该层的通信由不同设备中的应用程序之间的服务请求和响应组成。   

   <font color=red> 会话层的同事拿到表示层的同事转换后资料，会话层的同事那里可能会掌握本公司与其他好多公司的联系方式，这里公司就是实际传递过程中的实体。他们要管理本公司与外界好多公司的联系会话。当接收到表示层的数据后，会话层将会建立并记录本次会话，他首先要找到公司B的地址信息，然后将整份资料放进信封，并写上地址和联系方式。准备将资料寄出。等到确定公司B接收到此份报价单后，此次会话就算结束了，外联部的同事就会终止此次会话。</font>

<4>  传输层

​    传输层建立了主机端到端的链接，传输层的作用是为上层协议提供端到端的可靠和透明的数据传输服务，包括处理差错控制和流量控制等问题。该层向高层屏蔽了下层数据通信的细节，使高层用户看到的只是在两个传输实体间的一条主机到主机的、可由用户控制和设定的、可靠的数据通路。我们通常说的，TCP UDP就是在这一层。端口号既是这里的“端”。

​    <font color=red>传输层就相当于公司中的负责快递邮件收发的人，公司自己的投递员，他们负责将上一层的要寄出的资料投递到快递公司或邮局。</font>

<5>  网络层

​    本层通过IP寻址来建立两个节点之间的连接，为源端的运输层送来的分组，选择合适的路由和交换节点，正确无误地按照地址传送给目的端的运输层。就是通常说的IP层。这一层就是我们经常说的IP协议层。IP协议是Internet的基础。

   <font color=red>网络层就相当于快递公司庞大的快递网络，全国不同的集散中心，比如说，从深圳发往北京的顺丰快递，首先要到顺丰的深圳集散中心，从深圳集散中心再送到武汉集散中心，从武汉集散中心再寄到北京顺义集散中心。这个每个集散中心，就相当于网络中的一个IP节点。</font>

<6>  数据链路层 

​    将比特组合成字节,再将字节组合成帧,使用链路层地址 (以太网使用MAC地址)来访问介质,并进行差错检测。

​    <font color=red>数据链路层就先当于把散件打包，集装到运输工具上。</font>

<7> 物理层   

​    实际最终信号的传输是通过物理层实现的。通过物理介质传输比特流。规定了电平、速度和电缆针脚。常用设备有（各种物理设备）集线器、中继器、调制解调器、网线、双绞线、同轴电缆。这些都是物理层的传输介质。

​     <font color=red>  快递寄送过程中的走的路，就相当于我们的物理层，例如汽车走的公路，火车走铁轨，飞机走航线。物理层还包含了开车、开飞机这一含义。比如无线通信就相当于用飞机传输，传输过程就相当于把飞机开到目的地；用线缆传输相当于用汽车运</font>



#### 个人对osi的一些理解

1.回答开头的问题，网络层之间不能直接通信。网络端只会在数据头部封装源地址和目的地址，并为数据包的传送选择路径（即选择经过哪几个路由器）。做完这些工作他就会把这些东西做成一个SDU传给链路层，链路层再操作后传给物理层，物理层再进行真正的数据传输。即使是无线通信，其收发设备和传输介质（空间（空气）即是其传输介质）也归属于物理层。数据链路层同理。

![](E:\cetools\Hexo\blog\source\osi1.jpg)

![osi2](E:\cetools\Hexo\blog\source\osi2.png)

2.上文红字只是比喻，与OSI的差距还是很大的。就比如，我们比喻数字链路层是将散件打包到运输车，然后物理层相当于车和开车。但实际物理层的传输方式并不是“开车”，而是把物品打碎成分子，运到另一端，再重新组合成原样。即，按位（bit）传输。

本身一个货物（数据）可能有10kg（假定等于100bit），到达数据链路层后，和其他货物一起打包装车，装了123kg（一个帧，总共1234bit），然后还原成分子（1bit），通过信道1bit1bit的送。在接收端，再把数据1bit1bit在数据链路层还原成一个帧，再向上传输。不断拆解头部，最后数据到达目的进程（应用层）。

3.没了，再想起来在补充￣▽￣

也可能永远没了（







