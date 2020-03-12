# Some Specifications digest, 规范摘要

Bluetooth® Specification
================================================
# Sig Mesh蓝牙自组网
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

#### 2.1.5 Lower transport layer
The lower transport layer defines how upper transport layer messages are segmented and reassembled into multiple Lower Transport PDUs to deliver large upper transport layer messages to other nodes. It also defines a single control message to manage segmentation and reassembly.
#### 2.1.6 Network layer
The network layer defines how transport messages are addressed towards one or more elements. It defines the network message format that allows Transport PDUs to be transported by the bearer layer. The network layer decides whether to relay/forward messages, accept them for further processing, or reject them. It also defines how a network message is encrypted and authenticated.
#### 2.1.7 Bearer layer
The bearer layer defines how network messages are transported between nodes. There are two bearers defined, the advertising bearer and the GATT bearer. Additional bearers may be defined in the future.
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
