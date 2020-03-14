# Sig Mesh蓝牙自组网(Part of Bluetooth® Specification)
================================================
## I Mesh Profile|概述

- Revision: v1.0.1
- Revision Date: 2019-01-21
- Group Prepared By: Mesh Working Group
- Feedback Email: mesh-main@bluetooth.org
-----------------------------------------------
### 2 Mesh system architecture|Mesh系统架构(p15/153)
This section provides an overview of the mesh network operation and layered system architecture.

本章节给出mesh网络操作与分层的系统架构总览。

#### 2.1 Layered architecture
The Mesh Profile specification is defined as a layered architecture as shown in Figure 2.1.

mesh规范定义了下图所列的分层结构
```
Model Layer|模型层
```
```
Foundation Model Layer|基本模型层
```
```
Access Layer｜访问层
```
```
Upper Transport Layer｜高级传输层
```
```
Low Transport Layer｜低级传输层
```
```
Network Layer｜网络层
```
```
Bearer Layer｜传递层
```
```
Bluetooth Low Energy Core Specification低功耗蓝牙核心规范（传说中的Ble4.0...5.2）
```
Figure 2.1: Mesh system architecture图2.1 mesh系统架构
##### 2.1.1 Model layer｜模型层

The Model layer defines models that are used to standardize the operation of typical user scenarios and are defined in the Bluetooth Mesh Model specification or other higher layer specifications. Examples of higher layer model specifications include models for lighting and sensors.

模型层定义的模型用于规范化在*蓝牙自组网模型规范*中定义的典型用户场景操作，以及其他高层次的规范；比如高层次模型包括照明和传感器模型。

#### 2.1.2 Foundation Model layer｜基本模型层
The Foundation Model layer defines the states, messages, and models required to configure and manage a mesh network.

基本模型层定义的状态，消息以及模型用于配置和管理一个mesh网络

#### 2.1.3 Access layer|访问层
The access layer defines how higher layer applications can use the upper transport layer. It defines the format of the application data; it defines and controls the application data encryption and decryption performed in the upper transport layer; and it checks whether the incoming application data has been received in the context of the right network and application keys before forwarding it to the higher layer.

访问层定义了高层应用如何使用高级传输层，定了应用数据的格式；同时也定义和控制在高级传输层的加密和解密操作；用于在接收到的应用数据在提交到上一层之前，确认是否来自正确的网络(network key)和正确的应用密钥(app key)

#### 2.1.4 Upper transport layer｜高级传输层
The upper transport layer encrypts, decrypts, and authenticates application data and is designed to provide confidentiality of access messages. It also defines how transport control messages are used to manage the upper transport layer between nodes, including when used by the Friend feature.

高级传输层处理应用数据的解密、解密、验证应用数据，设计为提供访问消息的机密性。同时也定义了网络节点之间如何传输控制消息，用于管理高级传输层，包括何时被友好特性所用（应该是友好节点的特征值吧）

#### 2.1.5 Lower transport layer|低级传输层
The lower transport layer defines how upper transport layer messages are segmented and reassembled into multiple Lower Transport PDUs to deliver large upper transport layer messages to other nodes. It also defines a single control message to manage segmentation and reassembly.

低级传输层定义了如何将高级传输层的消息分段重组成低级传输的协议数据单元PDU(protocol data unit数据帧)传输到其他节点的高级传输层，同时定义了用于管理分段重组的单一控制消息
#### 2.1.6 Network layer｜网络层
The network layer defines how transport messages are addressed towards one or more elements. It defines the network message format that allows Transport PDUs to be transported by the bearer layer. The network layer decides whether to relay/forward messages, accept them for further processing, or reject them. It also defines how a network message is encrypted and authenticated.

网络层定义了如何传输带有地址的消息给一个或多个元素(elements,应该叫成员比较合适)，网络层定义了网络消息格式,能够被传递层传输的传输PDU
#### 2.1.7 Bearer layer｜传递层
The bearer layer defines how network messages are transported between nodes. There are two bearers defined, the advertising bearer and the GATT bearer. Additional bearers may be defined in the future.

传递层定义了网络消息如何在节点之间传输。有两种传递方式，广播传递和GATT传递。其他的传方式也有可能在未来被定义！加油哦！
### 2.2 Overview of mesh operation｜自组网操作综述
The mesh network operation defined by this specification is designed to:
 - enable messages to be sent from one element to one or more elements;
 - allow messages to be relayed via other nodes to extend the range of communication;
 - secure messages against known security attacks, including eavesdropping attacks, man-in-the-middle attacks, replay attacks, trash-can attacks, brute-force key attacks, and possible additional security attacks not documented here;
 - work on existing devices in the market today;
 - deliver messages in a timely manner;
 - continue to work when one or more devices are moved or stop operating; and
 - have built-in forward compatibility to support future versions of the Mesh Profile specification.

 按照本规范定义的自组网操作将被设计为：
  - 一个节点成员能够向一个或多个成员发送消息
  - 为了扩展通讯的范围，允许其他多个节点中继传递消息
  - 消息安全阻止已知的安全攻击，包括窃听攻击，中间人攻击，帧重放攻击，回收窃听攻击，暴力密钥破解攻击等，以及其他未列举的安全攻击
  - 市场存量设备可用
  - 及时传递信息
  - 在一个或多个设备移除或者停用的情况下网络保持可用，以及
  - 具有内置的前向兼容性，以支持未来的mesh版本

This specification defines a managed-flood-based mesh network, which uses broadcast channels to transmit messages so that other nodes can receive messages and relay these messages; thus extending the range of the original message. Any device in a managed-flood mesh network can send a message at any time as long as there is a sufficient density of devices that are listening and relaying messages. Enhancements to add routing functionality and define a routing-based mesh network may be considered for a future revision of this specification.

本规范定义了一个基于可管理泛洪的自组网路，它应用广播通道传输消息，其他网络节点就能够接受或中继消息；这样就使得原始消息的范围得到扩展，基于可管理泛洪的自组网路中的任意一个设备在任何时候可以发消息，有足够的密度的设备在监听和中继消息，渐入路由功能以及定义基于路由放入自组网络是本规范未来需要增强的部分。

There are a number of methods used by this specification to restrict the unlimited relaying of messages in a managed-flood mesh network. The two main methods used are the network message cache method and the time to live method.


本规范有很多方法限制消息的无限中继转发，最主要的两个方法是网络消息缓存方法和消息存活时间方法。

The network message cache is designed to prevent devices from relaying previously received messages by adding all messages to a cached list. When a message is received, it is checked against the list and ignored if already present. If not already received, then it is added to the cache so that it can be ignored in the future. To prevent this list from becoming too long, the number of messages that are cached is limited by implementation.

消息缓存通过转发预先收保存在缓存到队列中的所有消息，当接收到已经在缓存中的消息时，就会被忽略。为了防止这个缓存队列过大，在实现时要限制队列的消息数量。

Each message includes a Time to Live (TTL) value that limits the number of times a message can be relayed. Each time a message is received and then relayed (up to a maximum of 126 times) by a device, the TTL value is decremented by 1.

每个消息都有一个存活期限TTL,TTL数值限定了一个消息能够被转发的次数，消息每次被设备收发一次（最大126次），TTL数值减少1.

#### 2.2.1 Network and subnets｜网络与子网
A mesh network consists of nodes sharing four common resources:
 - network addresses used to identify source and destination of messages (see Section 3.4.2);
 - network keys used to secure and authenticate messages at the network layer (see Section 3.8.6.3);
 - application keys used to secure and authenticate messages at the access layer (see Section 3.8.6.2); and
 - an IV Index used to extend the lifetime of the network (see Section 3.8.4).

 由节点组成的自组网络要交互四个资源:
 - 网络地址用来区分消息的来源与目的地
 - 网络密钥用来在网络层安全认证消息
 - 应用密钥用来在访问层安全认证消息
 - IV序号用来扩展网络

A network can have one or more subnets that facilitate ”area” isolation (e.g., isolated hotel room subnets within a hotel network). A subnet is a group of nodes that can communicate with each other at a network layer because they share a network key. A node may belong to one or more subnets by knowing one or more network keys. At the time of provisioning, a device is provisioned to one subnet and may be added to more subnets using the Configuration Model.

一个网络有一个或者多个子网，实现区域隔离（比如，在一个酒店的网络中，隔离出客房子网）。子网就是节点的分组，这些节点在网络层相互通讯，因为他们有共同的网络密钥，一个节点可能属于一个或者多个子网带有一个或者多个网络密钥，在组网时，一个设备加入到一个子网，从而**通过使用配置模型**可能被添加到多个子网。

There is one special subnet called the primary subnet, which is based on the primary NetKey (see Section 3.8.6.4). Nodes on the primary subnet participate in the IV Update procedure (see Section 3.10.5), and propagate IV updates to other subnets, while nodes on other subnets only propagate the IV Index updates to those subnets.

首个子网是个特殊的子网，它基于初始网络密钥，在初始子网的节点要参与IV更新过程，并把更新的IV传播给其他子网，其他子网的节点只在其子网内传播IV序号更新。

The network resources are managed by a node that implements the Configuration Client model, known as the Configuration Client, (typically a smart phone or other mobile computing device) and are allocated to nodes at the time of configuration (see Section 5) using the Configuration Server model (see Section 4.4.1). In particular, a Provisioner manages allocation of addresses to make sure no duplicate unicast addresses are allocated, whereas a Configuration Client generates and distributes network andapplication keys and makes sure that devices that need to communicate with each other share proper keys for both network and access layers. The Configuration Client also knows device keys (see Section 3.8.6.1), which are used to secure communication with each individual node, including distributing updated network and application keys.

网络资源被实现了配置客户模型的节点管理，称之为配置客户端（或叫网关，每个mesh只能有一个网关，通常是一个智能手机或者其他移动计算机设备），配置那些运行配置服务模型的节点，通常网关管理地址分配，确保unicast地址不重复，还有为网络层和访问层层生成和分发网络应用密钥，网关也知道与之安全通讯的各独立节点的设备密钥，包括分发更新网络和应用密钥。

## II Mesh Model 模型

- Revision: v1.0.1
- Revision Date: 2019-01-21
- Group Prepared By: Mesh Working Group
- Feedback Email: mesh-main@bluetooth.org
-----------------------------------------------


## III Mesh Device Properties 设备属性

- Revision: v1.2
- Revision Date: 2019-12-17
- Group Prepared By: Mesh Working Group
- Feedback Email: mesh-main@bluetooth.org
-----------------------------------------------


=================================================
>welcome to SinoProbe data collection system.
```all rights belong to original person or organizations,if not be authorized,please let us konw by email:tnsm#163.com,we should delete ASAP.```
