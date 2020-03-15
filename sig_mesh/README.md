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

基本模型层定义的数据项集合，消息以及模型用于配置和管理一个mesh网络

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

网络资源被实现了配置客户模型的节点管理，称之为配置客户端（通常是一个智能手机或者其他移动计算机设备），配置那些运行配置服务模型的节点，通常Provisioner组网设备（下文就称之为**网管**，每个mesh只能有一个网管）管理地址分配，确保unicast地址不重复，还有为网络层和访问层层生成和分发网络应用密钥，网管也知道与之安全通讯的各独立节点的设备密钥，包括分发更新网络和应用密钥。

#### 2.2.2 Devices and nodes｜设备和节点
A device that is not a member of a mesh network is known as an unprovisioned device. A device that is a member of a mesh network is known as a node. A Provisioner is used to manage the transitions between an unprovisioned device and a node.

未入网的设备称之为未入网设备，已入网的设备称之为节点，网管用来管理未入网设备和节点的转换。

An unprovisioned device cannot send or receive mesh messages; however, it advertises its presence to Provisioners. A Provisioner will invite an unprovisioned device into a mesh network after it has been authenticated, converting the unprovisioned device into a node.

未入网设备不能收发mesh网络消息，只能向网管广播他的存在，网管将已验证的未入网设备加入到mesh网络，使它成为节点。

A node can send or receive mesh messages and is managed by a Configuration Client, that may also be the same device as the Provisioner, over the mesh network to configure how the node communicates with other nodes. A Configuration Client can remove a node from a mesh network, which reverts it back to an unprovisioned device.

节点能够收发mesh网络消息，受配置客户端管理（往往与网管是同一个设备），通过mesh网络配置一个节点如何与其他节点通讯，配置客户端能够把节点从网络中删除，使他成为未入网设备。

A device may support multiple instances of a node by offering itself to be provisioned to another mesh network after already being provisioned to a mesh network. Each instance of a mesh network is determined by addresses and a device key obtained by the device during provisioning.

一个设备可以支持多个节点实例，在于它入网后加入到其它mesh网络，每个mesh网络实例取决于节点地址和在入网时获得的设备密钥（DEVICE KEY）

#### 2.2.3 Adding devices to a mesh network｜添加设备到mesh网络
Devices are added to a mesh network by a Provisioner, at which point they become nodes. The provisioning of devices into a mesh network differs from the point-to-point bonding and pairing that is typically used in Bluetooth wireless technology. Provisioning of devices is enabled using either a simple advertising bearer or a point-to-point GATT-based bearer. A single provisioning protocol is used over both bearers. Provisioning over an advertising-based bearer is implemented by all devices. Provisioning over a GATT-based bearer allows devices such as legacy phones (i.e., devices that do not support provisioning over an advertising bearer natively) to be Provisioners.
To assist with provisioning of multiple devices, a device has an attention timer that can be set by a Provisioner. When set to a non-zero value, the device identifies itself using any means it can. For example, the device may flash a light, make a sound, or vibrate. When the attention timer expires, the device stops identifying itself. This allows a Provisioner to send a single message to a device to cause it to identify itself and the device automatically stops identifying itself after a given time.

设备通过网管加入到mesh网络，使它变成节点，设备入网过程不同于点到点的绑定或者配对的典型蓝牙无线技术，设备入网既可以通过简单的广播传递也可以通过基于过时手机的GATT传递的方式（比如不支持本地通过广播传递）成为网管，为了协助多种设备组网，设备有一个可以被网管设置的通知定时器，如果被设为非0值，就会用各种可能的方式标识，比如闪灯，发出声音或者震动等，如果定时器超时，设备就停止标识，这样也可以由网管发送一个简单消息让设备启动标识，等超时后自动停止

The protocol to run over these two bearers is a derivative of the Security Manager protocol of v4.2 of the Bluetooth Core Specification to introduce the ability to authenticate devices that have a very limited user interface, such as a light or a switch. The Security Manager protocol requires a reliable bearer, something that cannot be guaranteed by the advertising provisioning bearer; therefore the protocol used in this specification is designed to enable reliable delivery of messages independent of the bearer. The similarity to the Security Manager protocol enables significant reuse of existing code on devices that have implemented such functionality.

基于这两个传递层的协议是蓝牙核心规范v4.2安全管理协议的派生，引入对设备进行身份验证的能力导致十分有限的用户接口，比如照明和开关。安全管理协议要求可靠的传递层，广播组网传递有时候不能保证；所以，本规范使用的协议设计为独立于传递层以保证消息可靠发送，与安全管理协议相似使得现有设备实现这些功能的代码能够大量重用。

#### 2.2.4 Communications support｜通讯支持
Many current devices are unable to advertise or comprehend mesh messages without being updated. To enable these devices to communicate with a node in a mesh network without the need for an operating system update or similar hardware/software update, the specification enables the use of GATT connectivity for all existing devices.

现有的许多设备在没有升级时不能够广播或识别mesh网络消息，为了能够让这些设备不做操作系统升级或者类似的软硬件升级的前提下能够与mesh网络节点通讯,本规范采用GATT为所有存量提供连接

#### 2.2.5 Low power support｜低功耗支持
The features within this specification enable many devices in the mesh network to be battery-powered or to use techniques such as energy harvesting. Such devices may be constrained in how they can function as a part of a mesh network (e.g., devices that only send data when interacted with). This specification does not require devices to coordinate transmissions, make connections, or restart security on every connection; thus facilitating low power operation. Devices needing low power support can associate themselves with an always-on device that stores and relays messages on their behalf, using the concept known as Friendship (see Section 3.6.6). However, devices that relay messages will receive messages as well as forward messages a majority of the time and are likely to use significantly more power than could be provided by typical small batteries or capacitors.
本规范的特性之一就是mesh网络中的节点能使用电池供电或者使用能量收集等技术。...Friend Node...Low Power Node方式

### 2.3 Architectural concepts｜网络架构的概念
The mesh networking architecture uses several different concepts: states, messages, bindings, elements, addressing, models, publish-subscribe, mesh keys, and associations.

mesh 自组网架构有一些不同的概念：数据项集合、消息、绑定、成员、地址分配、模型、发布-订阅、自组网密钥以及关联等

#### 2.3.1 States｜数据项集合
A state is a value representing a condition of an element.

数据项集合代表了成员的数据集合

An element exposing a state is referred to as a server. For example, the simplest server is a Generic OnOff Server, representing that it is either on or off.

成员用服务的方式暴露一个数据项集合，比如，最简单的服务是通用开关服务，表示它的值是开或关

An element accessing a state is referred to as a client. For example, the simplest client is a Generic OnOff Client (a binary switch) that is able to control a Generic OnOff Server via messages defined by the Generic OnOff Model.

一个成员通过客户端的方式访问数据项集合，比如，最简单的客户端是通用开关客户端（二进制开关）就可以通过通用开关模型定义的消息控制通用开关服务。

States that are composed of two of more values are known as composite states. For example, a color-changing lamp can control color hue separately from color saturation and brightness.

数据项集合包括两个或更多数据项组合，比如调色灯泡能够独立于亮度饱和度单独控制色度。


#### 2.3.2 Bound states｜绑定数据项集合
When a state is bound to another state, a change in one results in a change in the other. Bound states may be from different models in one or more elements. For example, a common type of binding is between a Level state and an OnOff state: changing the Level to 0 changes the bound OnOff state to Off and changing the Level to a non-zero value changes the bound OnOff state to On.

当一个数据项集合和另一个数据项集合绑定，一个变化会影响另一个，绑定的数据项集合可以来自一个或多个成员的不同模型。比如，一个公共的绑定类型是等级数据项集合和开关数据项集合：等级调到0时，开关数据项要变为off，再调到非0值时，开关数据项要变为on。

#### 2.3.3 Messages｜消息
All communication within a mesh network is accomplished by sending messages. Messages operate on states. For each state, there is a defined set of messages that a server supports and a client may use to request a value of a state or to change a state. A server may also transmit unsolicited messages carrying information about states and/or changing states.

mesh网络的所以通讯均通过发送消息。消息操作数据项集合。对于每个数据项集合，就是定义一套服务支撑的消息，客户端用它请求数据项量或者改变数据项，服务也可以自发转送带有数据项信息或者数据项改变的消息。

A message is defined as having an opcode, associated parameters, and behavior. An opcode may be a single octet (for special messages that require maximum possible payload for parameters), 2 octets (for standard messages), or 3 octets (for vendor-specific messages).

消息定义包含：opcode操作码，关联参数以及行为，opcode可以是单字节（一些特殊消息要求最大参数量），双字节（bainzhun标准消息）或者3字节（用户自定义消息）

A total message size, including an opcode, is determined by the underlying transport layer, which may use a Segmentation and Reassembly (SAR) mechanism. To maximize performance and avoid the overhead of SAR, a design goal is to fit messages in a single segment. The transport layer provides up to 11 octets for a non-segmented message, leaving up to 10 octets that are available for parameters when using a 1-octet opcode, up to 9 octets available for parameters when using a 2-octet opcode, and up to 8 octets available for parameters when using a vendor-specific 3-octet opcode.

消息的大小，包括opcaode取决于下一传输层，或许是采用分段重组（SAR）方式。为获得最佳性能又要避免SAR溢出，一种方式是一个消息正好一段segement.传输层提供最大11字节的不分段消息传输，对于单字节的opcode，将有最多10个字节的参数，双字节最多9个，3字节最多8个字节用作参数传输。

The transport layer provides a mechanism of SAR capable of transporting up to 32 segments. The maximum message size when using the SAR is 384 octets. This means (excluding an Application MIC) up to 379 octets are available for parameters when using a 1-octet opcode, up to 378 octets are available for parameters when using a 2-octet opcode, and up to 377 octets are available for parameters when using a vendor-specific 3-octet opcode.

传输层提供的SAR机制最大传输32个分段segments。用SAR机制传输的消息最大字节数是384，剔除MIC,单字节opcode最大传送379字节，双字节虽大378，3字节opcode多大传送377字节的参数。

SAR effectively does not impose any extra overhead on the access layer payload per segment: a 10-octet message is transported as an unsegmented message, and a 20-octet message is transported as a segmented message that uses two segments.

10字节的消息按照不分段消息传送，20字节消息则分为两个段传送

Message definitions contain tables of parameters. In a message payload, parameters follow an opcode, and parameter offsets are in octets unless otherwise specified.

消息定义包含参数表，一个消息包含的参数在opcode之后，没有其他规定的情况下按字节偏移。

Messages are defined as acknowledged or unacknowledged. An acknowledged message requires a response whereas an unacknowledged message does not require a response.

消息定义为响应与非响应两种，响应消息要求有回复，非响应消息则不需要。

#### 2.3.4 Elements|元素？成员！！！
An element is an addressable entity within a node. Each node has at least one element, the primary element, and may have one or more additional secondary elements. The number and structure of elements is static and does not change throughout the lifetime of a node (that is, as long as the node is part of a network).

成员是节点中包含的带地址的实体，一个节点至少有一个成员，称之为首员，还可以有一个或多个次员，成员的个数与结构是静态的，在节点的生命周期里面不会变化，（意味着与节点一样是网络的一个组成部分）

The primary element is addressed using the first unicast address assigned to the node during provisioning. Each additional secondary element is addressed using the subsequent addresses. These unicast element addresses allow nodes to identify which element within a node is transmitting or receiving a message.

首员的地址就是入网时分配的unicast地址，其他每个次员使用子地址。这些唯一的成员地址使得节点能够区分节点内的哪个成员发送或者接收消息。

If the number and structure of elements changes, for example due to a firmware update, the node must be reprovisioned. The Node Removal procedure (see Section 3.10.7) is used when a firmware update is performed that changes the number or structure of elements.

如果因固件升级等原因导致了节点成员的数量与结构发生了改变，这个节点必须要重新入网。要采用节点移除的步骤。

Messages are dispatched within models based on opcodes and element addresses.

消息通过基于操作码与成员地址的模型分发。

An element is not allowed to contain multiple instances of models that use the same message in the same way (for example, receive an “On” message).

成员不允许包含多个在相同场合使用同样的消息的模型的实例。（比如，都接收“On”消息）。

When multiple models within the same element use the same message, the models are said to “overlap.” To implement multiple instances of overlapping models within a single node (for example, to control multiple light fixtures that can be turned on and off), the node is required to contain multiple elements.

当一个成员使用同样的消息使用多个模型时，称之为模型“重叠”，用来实现单节点中多个模型实例重叠（比如，控制多个灯具的同时开关），这个节点就要包含多个成员！！！（上一句话的解释，总之，一个成员不能有多个模型）

For example, a light fixture may have two lamps, each implementing an instance of the Light Lightness Server model and an instance of the Generic Power OnOff Server model. This requires that the node contain two elements, one for each lamp. When it receives an "On" message, the node uses the unicast address of the element to identify which instance of the Generic Power OnOff Server model the message is addressed to.

例如，一个灯具包括2个灯泡，每个都是亮度服务模型和通用开关服务模型的实例，这就要求该节点包含两个成员，每个灯泡对应一个成员，当收到“On”消息的时候，节点通过成员的unicast地址识别具有通用开关服务模型的地址把消息发送过去（就实现两个灯泡的同时开关，同时调节亮度）

In another example, a dual-socket power strip contains two independent energy measurement sensors that can measure power consumed by an appliance connected to a socket. This would require that the node have two Sensor Data states, each in a separate element. The first element, the primary element, would be identified using the unicast address for the node and would include a state for the first energy sensor as well as states representing the configuration of the node. The second element, a secondary element, would be identified using a unicast element address and would include the state for the second energy sensor.

再例如，双口插座包含两个独立的电量传感器用来测量每个插座的耗电量，这就要求节点包含两个传感器数据项集合，每个对应不同成员，第一个成员，即首员，用节点的unicast地址标识，包括第一个传感器的数据项，以及作为节点配置的数据项集合显示。第二个成员作为次员通过成员地址识别，并包括第二个电量传感器的数据项量

Each element has a GATT Bluetooth Namespace Descriptor [5] value that helps identify which part of the node this element represents. These namespace descriptor values use the same definitions as GATT. For example, the elements of the temperature sensor would use the values “inside” and “outside.”

每个成员有一个GATT蓝牙命名空间的描述名称，用来表示该成员代表节点的哪个部分，这些命名空间描述名称由GATT统一定义。例如，温度传感器成员将采用“inside”和“outside”

#### 2.3.5 Addresses｜地址
An address may be a unicast address, a virtual address, or a group address. There is also a special value to represent an unassigned address that is not used in messages.

地址可以是unicast地址，虚拟地址，或者群组地址。也有特定的值表示为未分配的地址（保留地址），不能在消息中使用

A unicast address is allocated to an element and always represents a single element of a node. There are 32767 unicast addresses per mesh network.

unicast地址指向成员，总是代表节点中的一个成员。每个，mesh网络共有32767个unicast地址。

A virtual address is a multicast address and can represent multiple elements on one or more nodes. Each virtual address logically represents a Label UUID, which is a 128-bit value that does not have to be managed centrally. Each message sent to a Label UUID includes the full Label UUID in the message integrity check value that is used to authenticate the message. To reduce the overhead of checking every known Label UUID, a hash of the Label UUID is used. There are 16384 hash values, each of which codifies a set of virtual addresses. While there are only 16384 hash values used in a virtual address, each hash value can represent millions of possible Label UUIDs; therefore, the number of virtual addresses is considered very large

虚拟地址是多指向地址，能代表一个或或多个节点中的多个成员，每个虚拟地址逻辑上代表一个UUID标签，它是一个不必集中管理的128位的值（16字节），发给UUID标签的每个消息包括完整的标签UUID的完整性校验，用于消息验证，采用标签UUID的哈希值校验已知的标签UUID，以降低开销。共有16384个哈希值集合，每个代表一个虚拟地址的集合，尽管只有16384个哈希值用于虚拟地址，但是每个哈希值能代表上百万个可能的标签UUID, 所以，虚拟地址的数量可以看作非常大。

A group address is a multicast address and can represent multiple elements on one or more nodes. There are 16384 group addresses per mesh network. There are a set of fixed group addresses that are used to address a subset of all primary elements of nodes based on the functionality of those nodes. All other group addresses are known as dynamically assigned group addresses. There are 256 fixed group addresses and 16128 dynamically assigned group addresses.

群组地址是个多指向地址，能代表一个或或多个节点中的多个成员，每个mesh网络有16384个群组地址，有一固定群组地址集合用于按功能划分的所有节点的首员组成的子网，其他群组地址动态分配。共有256个固定群组地址和16128个动态分配的群组地址。

#### 2.3.6 Models｜（应用/场景/功能）模型
A model defines the basic functionality of a node. A node may include multiple models. A model defines the required states (as described in Section 2.3.1), the messages that act upon those states (as described in Section 2.3.3), and any associated behavior.

模型用来定义节点的基本功能。一个节点有可能包括多个模型。一个模型定义要求的数据项集合，消息作用于这些数据项集合和相关行为。

A mesh application is specified using a client-server architecture communicating with a publish-subscribe paradigm. Due to the nature of mesh networks and the recognition that the configuration of behavior isperformed by a Configuration Client, an application is not defined in a single end-to-end specification such as a profile. Instead, an application is defined in a client model, a server model, and a control model.

一个mesh应用规范为采用客户端-服务端的架构和发布-订阅通讯的方式，按照mesh网络生态，可以认为通过配置客户端执行配置行为，应用不可定义为简单的端到端的规范。相反，**应用要定义为客户端模型，服务端模型以及控制模型**

This specification defines three types of model: server models, client models, and control models:

规范定义了三个模型，**应用要定义为客户端模型，服务端模型以及控制模型**

 - Server model: A server model is composed of one or more states spanning one or more elements. The server model defines a set of mandatory messages that it can transmit or receive, the behavior required of the element when it transmits and receives such messages, and any additional behavior that occurs after messages are transmitted or received.

 - 服务端模型：跨越一个或多个成员的一个或多个数据项集合组成服务端模型。服务端模型定义一套法定的消息集合用于发送和接收，当成员收到这些消息时要求相应的动作，在消息发送或接受之后，这些附加的动作就会发生。（消息驱动）

 - Client model: A client model defines a set of messages (both mandatory and optional) that a client uses to request, change, or consume corresponding server states, as defined by a server model. The client model does not have state.

 - 客户端模型：客户端模型定义一套消息集合（包含法定和可选两种），用于客户端请求，改变或接受服务端定义的数据项集合，客户端没有数据项

 - Control model: A control model may contain client model functionality to communicate with other server models and server model functionality to communicate with other client models. A control model may also contain control logic, which is a set of rules and behaviors that coordinate the interactions between other models that the control model connects to.

  - 控制模型：控制模型可能包含和其他服务端通讯的客户端模型的功能，以及和其他客户端通讯的服务端模型的功能，控制模型也包含控制逻辑，是与连接到控制模型的其他模型交互的规则和动作的集合

A single device may include server, client, and control models.

单一设备可以包括服务端模型、客户端模型以及控制模型。

For example, Figure 2.2 shows the element-model structure for a device that implements a server model (Device C) with a state and supporting messages R, S, T, X, Y, Z; and two devices that implement a client model, with Device A supporting messages X, Y, and Z and Device B supporting messages R, S, T, and Z.

举个例子，下图的是一个实现了服务端模型的成员模型结构的设备C（Device C)，有一个数据项，支持消息R, S, T, X, Y, Z;另外两个实现客户端模型的设备，设备A(Device A ),支持消息X, Y, Z，设备B(Device B),支持消息R, S, T, Z

![Figure 2.2: Client-server model communication](https://sinoprobe.dscloud.me:8443/doc/images/Client-server_model_communication.png)

In another example, Figure 2.3 shows the element-model structure of a device that implements a control model. Device C can communicate with server models as a client (supporting messages X, Y, and Z and messages R, S, and T respectively) and can communicate with client models as a server (supporting messages A, B, and C).

再举一个例子，下图的是一个实现了控制模型的成员模型结构的设备C，设备C通过客户端模型与服务端模型通讯（支持消息X,Y,Z和消息R,S,T）,又作为服务端与客户端模型通讯（支持消息A,B,C）,无所不能的样子


![Figure 2.3: Control model communication](https://sinoprobe.dscloud.me:8443/doc/images/Control_model_communication.png)

A lighting controller is an example of an implementation of a control model. The lighting controller needs to function as a client to sensors (to measure occupancy and/or ambient light) and to light sources (such as lamps or other luminaires). The lighting controller also would function as a server to a settings client (such as a smartphone application that configures its parameters). Such a lighting controller may be included within a sensor or light source or it may a separate device.

照明控制器是一个实现控制模型的例子，照明控制器需要传感器的客户端（测量占用率和/或环境光）和光源的客户端（比如灯泡或其他发光体）的功能，照明控制器又要作为服务端为设置客户端（比如智能手机设置照明参数）提供服务的功能，所以，照明控制器用包括传感器及光源或者他们是个独立的设备。

Models can define functions of a device as a network node, such as key management, address assignment, and relaying of messages. Models also define physical behaviors of a device built around a network node, such as power control, lighting control, and sensor data collection. There may be nodes implementing only network-related functions, such as Relay nodes or Proxy nodes, while the majority of nodes are able to interact with the physical world by means of controlling electrical power, controlling light emissions, or sensing environmental data.



A message can be used by multiple different models. Message behavior is the same in each model, enabling a common understanding among client, server, and control models because the behavior is consistent regardless of the models that send and process the message.



Model specifications are designed to be very small and self-contained. A model can, at the specification definition time, require other models that must also be instantiated within the same node. This is called extending, which means a model can extend other models.

Models that do not extend other models are referred to as root models.
Model specifications are immutable（不可改变）: it is not possible to remove or add behavior to a model, whether the desired behavior is optional behavior or mandatory. Models are not versioned and have no feature bits. If additional behavior is required in a model, then a new extended model is defined that exposes the required behavior and can be implemented alongside the original model.
Therefore, knowledge of the models supported by an element determines the exact behavior exposed by that element.
Models may be defined and adopted by Bluetooth SIG and may be defined by vendors. Models defined by Bluetooth SIG are known as SIG adopted models, and models defined by vendors are known as vendor models. Models are identified by unique identifiers, which can be either 16 bits, for SIG adopted models, or 32 bits, for vendor models.
For example, Figure 2.4 shows the element-model structure of a device that implements a root model with two bound states and a set of messages operating on each state. The root model is within the primary element and is extended by the extended model that adds another state on a secondary element. Messages are not capable of differentiating among multiple instances of the same state on the same element. Therefore, when more than one instance of a given state is present on a device, each instance is required to be in a separate element. In this example, the second instance of State X is required to be located on the second element because it is the same type of a state and thus has the same types of messages serving it.

![Figure 2.4: Element-model structure of a device](https://sinoprobe.dscloud.me:8443/doc/images/Element-model_structure_of_a_device.png)

This example structure may be multiplied for a composite device. For example, a composite device may have multiple instances of the same root model (or extended models), each on a separate element (or set of elements). Also, if a model (root or extended) needs more than one instance of a particular state, the states must be distributed across several elements so that, at most, a single instance of any given state is on an element.
Figure 2.5 illustrates how the element-model structure of the device in Figure 2.4 might be implemented in a composite device. The element-model structure of the device is described by the Composition Data (see Section 4.2.1) that is read by a Configuration Client after provisioning (see Section 5), using the Configuration Server model and the Configuration Client model (see Sections 4.4.1 and 4.4.2).

![Figure 2.5: Element-model structure of a composite device](https://sinoprobe.dscloud.me:8443/doc/images/Element-model_structure_of_a_composite_device.png)

#### 2.3.7 Example device｜举个设备的例子
To help explain how the arrangement of models within elements determines the state and behavior of a device, we will use a dual-socket smart power strip device (shown in Figure 2.6) as an example. This device has a single radio that has the low energy feature of Bluetooth and two independent power sockets, each capable of controlling the power output. This example includes states, messages, and models defined in the Mesh Model specification [11].

![Figure 2.7: Element-model structure for the example device](https://sinoprobe.dscloud.me:8443/doc/images/Element-model_structure_for_the_example_device.png)

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
