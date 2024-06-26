---
title: Network08-IPv4
date: 2024-05-12 16:59:24
tags:
- network
- 基础知识
categories: 数据通信
cover: https://tuchuang-1258743955.cos.ap-beijing.myqcloud.com/image/20240512170022.png
---
## 背景
- IPv4在[IETF](https://zh.wikipedia.org/wiki/IETF "IETF")于1981年9月发布的 [RFC 791](https://tools.ietf.org/html/rfc791) 中被描述
- IPv4是一种[无连接](https://zh.wikipedia.org/wiki/%E7%84%A1%E9%80%A3%E6%8E%A5%E5%BC%8F%E9%80%9A%E8%A8%8A "无连接式通信")的协议，操作在使用[分组交换](https://zh.wikipedia.org/wiki/%E5%88%86%E7%BB%84%E4%BA%A4%E6%8D%A2 "分组交换")的链路层（如[以太网](https://zh.wikipedia.org/wiki/%E4%BB%A5%E5%A4%AA%E7%BD%91 "以太网")）上。此协议会尽最大努力交付数据包，意即它不保证任何数据包均能送达目的地，也不保证所有数据包均按照正确的顺序无重复地到达。这些方面是由上层的传输协议（如[传输控制协议](https://zh.wikipedia.org/wiki/%E4%BC%A0%E8%BE%93%E6%8E%A7%E5%88%B6%E5%8D%8F%E8%AE%AE "传输控制协议")）处理的。

> 个人理解，其实IP协议主要的目的就是实现网络通信寻址，就像朋友之间互相串个门，总要知道你家地址，我才能找到你把~
## IPv4报头
![image.png](https://tuchuang-1258743955.cos.ap-beijing.myqcloud.com/image/20230128144136.png)
下面是各个字段的解释，标粗的是重点。

（1）版本（4位）：该字段定义IP协议版本，负责向处理机所运行的IP软件指明此IP数据报是哪个版本，所有字段都要按照此版本的协议来解释。如果计算机使用其他版本，则丢弃数据报。 [3] 

（2）头部长度（4位）：该字段定义数据报协议头长度，表示协议头部具有32位字长的数量。协议头最小值为5，最大值为15。 [3] 

（3）服务（8位）：该字段定义上层协议对处理当前数据报所期望的服务质量，并对数据报按照重要性级别进行分配。前3位成为优先位，后面4位成为服务类型，最后1位没有定义。这些8位字段用于分配优先级、延迟、吞吐量以及可靠性。 [3] 

（4）**总长度**（16位）：该字段定义整个IP数据报的字节长度，包括协议头部和数据。其最大值为65535字节。[以太网协议](https://baike.baidu.com/item/%E4%BB%A5%E5%A4%AA%E7%BD%91%E5%8D%8F%E8%AE%AE/12776893?fromModule=lemma_inlink)对能够封装在一个帧中的数据有最小值和最大值的限制（46~1500个字节）。 [3] 

（5）标识（16位）：该字段包含一个整数，用于识别当前数据报。当数据报分段时，标识字段的值被复制到所有的分段之中。该字段由发送端分配帮助接收端集中数据报分段。 [3] 

（6）标记（3位）：该字段由3位字段构成，其中最低位（MF）控制分段，存在下一个分段置为1，否则置0代表该分段是最后一个分段。中间位（DF）指出数据报是否可进行分段，如果为1则机器不能将该数据报进行分段。第三位即最高位保留不使用，值为0。 [3] 

（7）分段偏移（13位）：该字段指出分段数据在源数据报中的相对位置，支持目标IP适当重建源数据。 [3] 

（8）**生存时间**（8位）：该字段是一种计数器，在丢弃数据报的每个点值依次减1直至减少为0。这样确保数据报拥有有限的环路过程（即TTL），限制了数据报的寿命。 [3] 

（9）协议（8位）：该字段指出在IP处理过程完成之后，有哪种上层协议接收导入数据报。这个字段的值对接收方的网络层了解数据属于哪个协议很有帮助。 [3] 

（10）头部校验和（16位）：该字段帮助确保IP协议头的完整性。由于某些协议头字段的改变，这就需要对每个点重新计算和检验。计算过程是先将校验和字段置为0，然后将整个头部每16位划分为一部分，将个部分相加，再将计算结果取反码，插入到校验和字段中。 [3] 

（11）**源地址**（32位）：源主机[IP地址](https://baike.baidu.com/item/IP%E5%9C%B0%E5%9D%80/150859?fromModule=lemma_inlink)，该字段在IPv4数据报从源主机到目的主机传输期间必须保持不变。 [3] 

（12）**目的地址**（32位）：目标主机IP地址，该字段在IPv4数据报从源主机到目的主机传输期间同样必须保持不变。

## IP地址分类
**网络地址**
网络地址可用来识别设备所在的网络，网络地址位于IP地址的前段。当组织或企业申请IP地址时，所获得的并非IP地址，而是取得一个唯一的、能够识别的网络地址。同一网络上的所有设备，都有相同的网络地址。IP路由的功能是根据IP地址中的网络地址，决定要将IP信息包送至所指明的那个网络。 

**主机地址**

主机地址位于IP地址的后段，可用来识别网络上设备。同一网络上的设备都会有相同的网络地址，而各设备之间则是以主机地址来区别。 

由于各个网络的规模大小不一，大型的网络应该使用较短的网络地址，以便能使用较多的主机地址；反之，较小的网络则应该使用较长的网络地址。为了符合不同网络规模的需求，IP在设计时便根据网络地址的长度，设计与划分IP地址。 



### 五种地址等级

- A类：(1.0.0.0-126.0.0.0)（默认子网掩码：255.0.0.0或 0xFF000000）第一个字节为网络号，后三个字节为主机号。该类IP地址的最前面为“0”，所以地址的网络号取值于1~126之间。一般用于大型网络。
- B类：(128.0.0.0-191.255.0.0)（默认子网掩码：255.255.0.0或0xFFFF0000）前两个字节为网络号，后两个字节为主机号。该类IP地址的最前面为“10”，所以地址的网络号取值于128~191之间。一般用于中等规模网络。
- C类：(192.0.0.0-223.255.255.0)（子网掩码：255.255.255.0或 0xFFFFFF00）前三个字节为网络号，最后一个字节为主机号。该类IP地址的最前面为“110”，所以地址的网络号取值于192~223之间。一般用于小型网络。
- D类：是多播地址。该类IP地址的最前面为“1110”，所以地址的网络号取值于224~239之间。一般用于多路广播用户。
- E类：是保留地址。该类IP地址的最前面为“1111”，所以地址的网络号取值于240~255之间。

在设计IP时，着眼于路由与管理上的需求，因此制定了5种IP地址的等级。不过，一般最常用到的便是A、B、C类这三种等级的IP地址。5种等级分别使用不同长度的网络地址，因此适用于大、中，小型网络。IP地址的管理机构可根据申请者的网络规模，决定要赋予哪种等级。 

传统IP地址的运行方式，由于以等级来划分，因此称为等级式的划分方式。相对的，后来又产生了无等级的划分方式，也就是CIDR（.Classless Inter-Domain Routing）。 

### 特殊IP地址

在实际应用上，有些网络地址与主机地址有特别的用途，因此在分配或管理IP地址时，要特别注意这些限制。 

**广播地址**

所有主机号部分为1的地址是广播地址。广播地址分为两种：直接广播地址和有限广播地址。 

在一特定[子网](https://baike.baidu.com/item/%E5%AD%90%E7%BD%91/1186929?fromModule=lemma_inlink)中，主机地址部分为全I的地址称为直接广播地址。一台主机使用直接广播地址，可以向任何指定的网络直接广播它的数据报，很多IP协议利用这个功能向一个子网上广播数据。 

32个bit全为l的IP地址(即255.255.255.255)被称为[有限广播地址](https://baike.baidu.com/item/%E6%9C%89%E9%99%90%E5%B9%BF%E6%92%AD%E5%9C%B0%E5%9D%80/9293191?fromModule=lemma_inlink)或本地网广播地址，该地址被用作在本网络内部广播。使用有限广播地址，主机在不知道自己的网络地址的情况下，也可以向本子网上所有的其他主机发送消息。 [2] 

[广播地址](https://baike.baidu.com/item/%E5%B9%BF%E6%92%AD%E5%9C%B0%E5%9D%80/8614095?fromModule=lemma_inlink)不像其他的IP地址那样分配给某台具体的主机。因为它是指满足一定条件的一组计算机。广播地址只能作为IP报文的目的地址，表示该报文的一组接收者。 [2] 

**组播地址**

D类IP地址就是组播地址，即在224.0.0.0~239.255.255.255范围内的每个IP地址，实际上代表一组特定的主机。 

[组播地址](https://baike.baidu.com/item/%E7%BB%84%E6%92%AD%E5%9C%B0%E5%9D%80/6095039?fromModule=lemma_inlink)与广播地址相似之处是都只能作为IP报文的目的地址，表示该报文的一组接收者，而不能把它分配给某台具体的主机。 

组播地址和广播地址的区别在于广播地址是按主机的物理位置来划分各组的(属于同一个子网)，而组播地址指定一个逻辑组，参与该组的计算机可能遍布整个Internet。组播地址主要用于[电视会议](https://baike.baidu.com/item/%E7%94%B5%E8%A7%86%E4%BC%9A%E8%AE%AE/414236?fromModule=lemma_inlink)、[视频点播](https://baike.baidu.com/item/%E8%A7%86%E9%A2%91%E7%82%B9%E6%92%AD/1043527?fromModule=lemma_inlink)等应用。 

网络中的路由器根据参与的主机位置，为该组播的通信组形成一棵发送树。服务器在发送数据时，只需发送一份数据报文，该报文的目的地址为相应的组播地址。路由器根据已经形成的发送树依次转发，只是在树的分岔点处复制数据报，向多个网络转发一份副本。经过多个路由器的转发后，则该数据报可以到达所有登记到该组的主机处。这样就大大减少了源端主机的负担和网络资源的浪费。 [2] 

**0地址**

主机号为0的IP地址从来不分配给任何-一个单个的主机号为0，例如，202.112.7.0就是--个典型的C类网络地址，表示该网络本身。 

网络号为0的IP地址是指本网络上的某台主机。例如如果一台主机(IP地址为202.112.7.13)接收到一个IP报文，它的目的地址中网络号部分为0，而主机号部分与它自己的地址匹配(即IP地址为0.0.0.13)，则接收方把该IP地址解释成为本网络的主机地址，并接收该IP数据报。 

0.0.0.0代表本主机地址。网络上任何主机都可以用它来表示自己。 

**回送地址**

原本属于A类地址范围内的IP地址127.0.0.0~127.255.255.255却并没有包含在A类地址之内。 

任何一个以数字127开头的IP地址(127.x.x.x)都叫做[回送地址](https://baike.baidu.com/item/%E5%9B%9E%E9%80%81%E5%9C%B0%E5%9D%80/8021522?fromModule=lemma_inlink)。它是一个保留地址，最常见的表示形式为127.0.0.1。 

在每个主机上对应于IP地址127.0.0.1有个接口，称为回送接口。IP协议规定，当任何程序用回送地址作为目的地址时，计算机上的协议软件不会把该数据报向网络上发送，而是把数据直接返回给本主机。因此网络号等于127的数据报文不能出现于任何网络上，主机和路由器不能为该地址广播任何寻径信息。回送地址的用途是，可以实现对本机网络协议的测试或实现本地进程间的通信。 

## 子网掩码
- 引入子网掩码(NetMask)，从逻辑上把一个大网络划分成一些小网络。子网掩码是由一系列的1和0构成，通过将其同IP地址做“与”运算来指出一个IP地址的网络号是什么。对于传统IP地址分类来说，A类地址的子网掩码是255.0.0.0；B类地址的子网掩码是255.255.0.0；C类地址的子网掩码是255.255.255.0。例如，如果要将一个B类网络166.111.0.0划分为多个C类子网来用的话，只要将其子网掩码设置为255.255.255.0即可，这样166.111.1.1和166.111.2.1就分属于不同的网络了。像这样，通过较长的子网掩码将一个网络划分为多个网络的方法就叫做划分子网(Subnetting)。 
## 产生背景
上文中我们介绍了，其实一开始IPv4地址是分为了abcde五类，这种分法呢，不灵活，会有地址浪费的情况，所以才出现了子网掩码这个东西。在后面的发展中，前人在IP地址3种主要类型里，各保留了3个区域作为**私有地址**，其地址范围如下：   
- A类地址：10.0.0.0～10.255.255.255   
-  B类地址：172.16.0.0～172.31.255.255   
-  C类地址：192.168.0.0～192.168.255.255

子网掩码的出现带给了人们极大的便利
- 企业内网划分，可以给多个部门，分配多个网段，不需要局限于abc三类网络地址来划分，比如我一段10.0.0.0/8的地址就足够拆分成N个小地址段了
- 子网掩码也显著提高了IP地址的分配效率，有效解决了IP地址资源紧张的局面

这也就是我们熟知的三大私网地址。

## 子网掩码如何使用？
> 在这里，就不讲二进制到十进制的换算了
- 子网掩码的设定必须遵循一定的规则。与[二进制](https://baike.baidu.com/item/%E4%BA%8C%E8%BF%9B%E5%88%B6/0?fromModule=lemma_inlink)IP地址相同，子网掩码由1和0组成，且1和0分别连续。子网掩码的长度也是32位，左边是网络位，用[二进制](https://baike.baidu.com/item/%E4%BA%8C%E8%BF%9B%E5%88%B6/0?fromModule=lemma_inlink)数字“1”表示，1的数目等于网络位的长度；右边是主机位，用[二进制数字](https://baike.baidu.com/item/%E4%BA%8C%E8%BF%9B%E5%88%B6%E6%95%B0%E5%AD%97/5920908?fromModule=lemma_inlink)“0”表示，0的数目等于主机位的长度。这样做的目的是为了让掩码与IP地址做按位与运算时用0遮住原主机数，而不改变原网络段数字，而且很容易通过0的位数确定子网的主机数（2的主机位数次方-2，因为主机号全为1时表示该网络[广播地址](https://baike.baidu.com/item/%E5%B9%BF%E6%92%AD%E5%9C%B0%E5%9D%80/0?fromModule=lemma_inlink)，全为0时表示该网络的[网络号](https://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E5%8F%B7/0?fromModule=lemma_inlink)，这是两个特殊地址）。通过子网掩码，才能表明一台主机所在的子网与其他子网的关系，使网络正常工作。
### 计算方式
> 笔者不擅长数学，所以，遇到划分子网，都是网上找专门的计算器，不过基本的逻辑还是要清楚的。

IPv4地址被分为三部分：网络部分（network）、子网部分（subnetwork，常被认为是网络部分的一部分）和主机（host）部分。共有三类IP地址，它们分别指定了各部分占多少位。

| 类别  | 起始位（二进制） | 开始        | 结束            | 点分十进制掩码       |
| --- | -------- | --------- | ------------- | ------------- |
| A   | 0        | 0.0.0.0   | 127.0.0.0     | 255.0.0.0     |
| B   | 10       | 128.0.0.0 | 191.255.0.0   | 255.255.0.0   |
| C   | 110      | 192.0.0.0 | 223.255.255.0 | 255.255.255.0 |

子网的划分是一个将主机部分的若干位分配到网络部分的过程。例如，对于一个给定的A类网络：10.0.0.0，子网掩码：255.0.0.0可以将其划分为256个子网（从10.0.0.0到10.255.0.0）——第一个八位位组表示网络地址，第二个表示子网号，而最后两个表示主机部分。用子网掩码对主机地址进行位与操作，就能够提取出完整的子网地址（参见下面的例子）。
- 子网掩码并不局限于整数个八位位组的情况。例如，255.254.0.0（或“/15”）同样是一个有效的掩码。如果将它应用到A类地址上，就会产生128个间隔为2的子网（例如1.2.0.1～1.3.255.254，1.4.0.1～1.5.255.254等等

> 如何判断一个网段有多少可用地址呢，只需要把子网掩码换算为10进制，然后用32去减，得几就是2的几次方，比如一个/24的子网掩码，32-24=8，2的8次方是256，再减去网络号和广播位，得到可用地址是254