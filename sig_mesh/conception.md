# Fundamental Concepts and Terminology
## Mesh Network
The term “mesh network” refers to a type of wireless network topology, where each network Node participates in the distribution of data across the network, by relaying data to other Nodes which are in range. There are two primary techniques used to relay data across the mesh networks, namely routing and flooding. Bluetooth mesh networking uses a specialised and highly optimized version of flooding called managed flooding.

## Routing
Mesh networks which use the routing technique, send data along a selected path, via specific Nodes to reach its destination. Dedicated devices called routers are responsible for determining the paths which data must follow. This reliance on routers can give rise to single points of failure and a network which is not robust or reliable.

## Flooding
Mesh networks which use the flooding technique, broadcast data such that it is received by all Nodes within direct range. They, in turn, relay the received data by broadcasting it again such that it is received by another set of in-range Nodes. Only Nodes to which the data was addressed will act upon the data.

Flooding means that messages take multiple paths to reach their destination. There is no reliance on routers and as such, substantially less risk of the network containing single points of failure. This makes mesh networks which use flooding, highly reliable.

## Managed Flooding
Bluetooth mesh networking leverages the strengths of the flooding approach and optimises its operation such that it is both reliable and efficient. A number of features of design of Bluetooth mesh networking, contribute to the efficiency of managed flooding:

## Heartbeats
– Heartbeat messages are transmitted by nodes periodically. A heartbeat message indicates to other nodes in the network that the node sending the heartbeat is still active. In addition, heartbeat messages contain data which allows receiving nodes to determine how far away the sender is, in terms of the number of hops required to reach it. This knowledge can be exploited with the TTL field.

## TTL
– TTL is a field which all Bluetooth mesh PDUs include. It controls the maximum number of hops, over which a message will be relayed. Setting the TTL allows nodes to exercise control over relaying and conserve energy, by ensuring messages are not relayed further than is required. Heartbeat messages allow nodes to determine what the optimum TTL value should be for each message published.

## Message Cache
– a Network Message Cache must be implemented by all nodes. The cache contains all recently seen messages and if a message is found to be in the cache, indicating the node has seen and processed it before, it is immediately discarded.

## Friendship
– Probably the most significant optimisation mechanism in a Bluetooth mesh network is provided by the combination of Friend and Low Power Nodes. Friend nodes provide a message “store and forward” service to associated Low Power Nodes. This allows Low Power Nodes to operate in an energy efficient manner and to only switch their radio on in “receive mode” after asking the associated Friend to deliver any messages it has in its store. The rest of the time, the radio of the Low Power Node only gets switched on when it needs to transmit data.

## Subnets
– Subnets are a mechanism which allow a Bluetooth mesh network to be partitioned. This is primarily for security purposes but it does also have the benefit that messages sent using a subnet are not relayed beyond that subnet. This conserves energy.

## Device
A Device is a Bluetooth device which is capable of being provisioned and thus becoming a Node and member of the network.

## Node
A Node is a Bluetooth device which has been provisioned and as such, is a member of a network. A node may belong to more than one distinct network.

## Network
A mesh network is a set of Nodes which share a common Network Key.

## Subnet
Networks may contain one or more subnets. Subnets are intended to allow secure isolation of different areas such as, for example, individual rooms in a hotel. A Node is a member of a subnet by virtue of it possessing the subnet’s Network Key. A Node may belong to one or more subnets by possessing one or more subnet NetKeys.

## Element
Elements in General
An Element is an addressable entity within a device. This means that it is some part of a device which has at least one, independent State value which represents some condition of the Element. All nodes must have at least one Element. Some Nodes will have multiple Elements. A composite light switch containing multiple switches might be a Node which has multiple Elements, for example.

## Primary Elements
The Element in a Node which contains the Configuration Server Model, is known as the Primary Element.

## Address
Bluetooth mesh uses a system of various address types to identify individual Elements or sets of Elements.

## Unicast Addresses
A Unicast Address identifies a single, specific Element of a Node. A Provisioner manages the allocation of unicast addresses and ensures that no duplicates are allocated within a network.

## Group Addresses
A Group Address is a multicast address which represents one or more Elements. Group Addresses are either defined by the Bluetooth SIG and are known as SIG Fixed Group Addresses or they are assigned dynamically. Up to 256 SIG Fixed Group Addresses are allowed, of which at the time of writing, only 4 have been defined. These are named All-proxies, All-friends, All-relays and All-nodes.

There may be up to *16383 group addresses* in a mesh network.

## Virtual Addresses
A Virtual Address is an address which may be assigned to one or more Elements, spanning one or more Nodes. It takes the form of a 128-bit UUID value with which any Element can be associated, and is much like a label.

There may be up to *70 trillion virtual addresses* in a mesh network.

## The Unassigned Address
This is a special address type, with a value of 0x0000. Its use indicates that an Element has not yet been configured or had a Unicast Address assigned to it.

## Publish Address
An address used as the destination to which messages are published is termed the Publish Address. A Publish Address may be a Unicast Address, a pre-configured Group Address or a Virtual Address.

## Destination (DST)
The Address to which a Message is sent.

## Source
The Address from which a Message is sent.

## TTL
TTL stands for *Time To Live* and is a field in mesh network PDUs. Its purpose is to control whether or not a received message should be relayed, and to limit the total number of hops over which a message is ultimately relayed within the network. A value of zero indicates that a message has not been relayed and should not be relayed. This means that a node can send a message to other nodes which are in direct radio range (Neighbors) and indicate that receiving node(s) should not relay the message. If a message is sent with a TTL of 2 or more, then each time it is relayed, the TTL value is decremented. A value of 1 then means that the message may have been relayed at least once, but that it should not be relayed again.

## Neighbors
The Nodes that are in direct radio range (i.e. a single hop away), are known as Neighbors.

## Feature
Features define some of the most fundamental functionality of a Node. All Nodes have the ability to transmit and receive mesh Messages. Nodes can also optionally support one or more additional features, of which the following are currently defined. Note that a feature may be enabled or disabled on a particular device.

## The Relay Feature
The ability to receive and retransmit mesh Messages over the advertising bearer to enable larger networks. A Node that supports the Relay feature and has the Relay feature enabled is known as a Relay Node.

## The Proxy Feature
The ability to receive and retransmit mesh Messages between GATT and advertising bearers. A Node that supports the Proxy feature and has the Proxy feature enabled is known as a Proxy Node.

## The Low Power Feature
The ability to operate within a mesh network at significantly reduced receiver duty cycles when working in conjunction with a Node supporting the Friend feature. A Node that supports the Low Power feature and has the Low Power feature enabled is known as a Low Power Node (LPN).

## The Friend Feature
The ability to help a Node supporting the Low Power feature to operate efficiently, by storing Messages destined for that Node and only delivering them when the Low Power Node polls the Friend Node. A Node that supports the Friend feature and has the Friend feature enabled is known as a Friend Node. The relationship between the Friend and the Low Power Node is known as Friendship.

## Model
A Model defines a set of States, State Transitions, State Bindings, Messages and other associated behaviors. An Element within a Node must support one or more models and it is the model or models that define the functionality that an Element has. There are a number of models that are defined by the Bluetooth SIG and many of them are deliberately positioned as “generic” models, having potential utility within a wide range of device types.

All communication within a Bluetooth mesh network is accomplished using messages, defined as part of a Model specification.

There are three broad categories of model; Server, Client and Controller.

A model may extend another model. Models which do not extend other models are called “root models”. Changing a model by adding or removing a behavior is not permitted. The correct response to new requirements is to extend the existing model.

Understanding the concept of a Model is best done through considering an example.

The simplest generic model is the Generic OnOff Server Model. It defines a single State, called Generic OnOff, which may have a value of 0x00 representing Off or 0x01 representing On. The model defines four types of Message. The four Messages are:

 - Generic OnOff Get
 - Generic OnOff Set
 - Generic OnOff Set Unacknowledged
 - Generic OnOff Status

The Generic OnOff Get Message, when received by an Element which supports the Generic OnOff Server Model, causes the Element to reply with a Generic OnOff Status Message, which reports the current value of the Generic OnOff State.

The Generic OnOff Set Message, when received by an Element which supports the Generic OnOff Server Model, causes the value of the Generic OnOff State to be changed, and it is to be expected that the physical device in which the Element is contained, will reflect this change of State value in some expected way (such as a light switching on or off). Generic OnOff Set is known as a Acknowledged Message which means that it requires a response from the Element. In the case of Generic OnOff Set, the expected response is a Generic OnOff Status Message.

The Generic OnOff Set Unacknowledged Message has the same semantics as the Generic OnOff Set Message except that it does not require the Element to respond with a Status Message.

The Generic OnOff Status Message may be sent by an Element to report its OnOff status. It is an unacknowledged message in that no response is required from Elements which receive it.

Models defined by the Bluetooth SIG are known as SIG Models. Vendors may define their own models too and these are known as Vendor Models.

## Configuration Model
There are numerous ways in which a mesh network device may be configured and this is represented by the Statesdefined by the Configuration Server Model. For example, the Secure Network Beacon state indicates whether or not the node is broadcasting as a Secure Network Beacon, the Friend state indicates support or otherwise for the Friend Feature and the AppKey List contains the list of Application Keys for applications this node is associated with. The Configuration Server Model allows the configuration of such State values via the Configuration Client Model.

## Composition Data
Composition Data is a State value which belongs to the Configuration Server Model and is always present in all Primary Elements. It contains information about the node, the elements it contains and the models and features it supports. It is a composite state which consists of one or more pages of information.

## Application
Mesh applications use the mesh network and some combination of one or more client, server and/or controller Modelsto provide user level functionality, typically involving related types of device. So for example, a mesh lighting application might involve the Generic OnOff Server Model and the Generic OnOff Client Model for controlling simple lights, plus the Generic Level Server Model and the Generic Level Client Model for controlling dimmable lights.

## State
A State represents the condition of some aspect of an Element together with some associated behaviors. For example, a simple light bulb node which contains a Primary Element only, might support the Generic OnOff Model which includes the Generic OnOff State. This State defines a value of 0x00 which indicates that the light bulb is currently OFF and 0x01 which means that it is ON.

States may be multi-dimensional. For example, the Light HSL state combines Hue, Lightness and Saturation state values into a single State.

## Characteristic
A Characteristic is a data type which represents a given kind of Property data exposed by a server. Bluetooth Characteristics are relevant to both Bluetooth mesh and to Bluetooth Low Energy GATT. Characteristics define a type, data format (e.g. uint8), the units that the value of an instance of the characteristic are expressed in (e.g. degrees celsius), and sometimes, valid value ranges or enumerations which are valid for the type.

Characteristics have no associated context and do not have defined behaviors.

## Property
A Property provides the context for interpretting a concrete instance of a Characteristic.

For example, the Temperature 8 Characteristic, is a type which represents a temperature measurement, has a format of uint8 and uses units of 0.5 degrees celsius. Several properties are defined for this characteristic, thus allowing it to be interpretted in various contexts. The Present Indoor Ambient Temperature property indicates that the Temperature 8 characteristic should be interpretted as being a measurement which was taken indoors, whereas the Present Outdoor Ambient Temperature property relates to measurements taken outdoors, and the Present Ambient Temperature property is not specific about the type of location, and this is left to be derived from other, location properties.

Characteristic values are deemed to be either scalar values or non-scalar values. In either case, the raw value of a property must be interpretted according to certain rules. Non-scalar values are simply interpretted according to the associated characteristic’s Format field in its definition. Scalar values are interpretted by applying an equation to each of the characteristic’s fields, involving a series of parameters that are defined for each of the characteristic’s fields individually. The equation used is:

```
R = C * M * 10d * 2b
```

where:

 - R = represented value
 - C = raw value
 - M = multiplier
 - d = decimal exponent
 - b = binary exponent
States involved in mesh operations are inferred from the opcode of the mesh message whereas Properties are explicitly referenced by a property ID in property related messages such as the Generic User Property Get message.

## State Transition
Changes from one State to another are called State Transitions. Various things can trigger a State Transition. A “set message” arriving and being processed at an Element would probably cause a State Transition. Implementations may trigger State Transitions as a consequence of asynchronous actions such as, for example, an action being triggered by a local timer. Physical interactions with a device by a user, such as pressing a button, might also cause a State Transition.

State transitions may take place instantaneously or may take a period of time to complete. The time it takes for a Stateto transition from one state value to another target state value is called the Transition Time.

Some messages allow a transition delay to be specified, indicating a period of time which must elapse before a state transition starts.

## State Binding
Models may define relationships between one State, and another whereby a change to the first state will give rise to a defined change in the other state. The relationship between these two states and the definition of the changes that one may trigger in the other, is called a State Binding. State Bindings may exist between States in the same model or different models. One State may be bound to multiple, other States.

## Time State
The Time State represents the current time in terms of the present TAI time, the TAI-UTC Delta and local time zone offset. It plays a key role in the execution of Scenes.

## Time Authority
Time Authority is a bit field within the Time State. When set to 1, this indicates that the Element has access to a reliable source of time. The reliable time source may be an external source, such as GPS or NTP or be a real time clock, integral to the Element or its parent Node.

## Mesh Time Authority
A Node may play various roles in propagating time across the mesh and the particular role played by a node is indicated by the Time Role State. A node which plays the role of Mesh Time Authority, publishes Time Status messages but does not process received Time Status messages.

## Mesh Time Client
A Node may play various roles in propagating time across the mesh and the particular role played by a node is indicated by the Time Role State. A node which plays the role of Mesh Time Client, processes received Time Status messages but does not publish them.

## Mesh Time Relay
A Node may play various roles in propagating time across the mesh and the particular role played by a node is indicated by the Time Role State. A node which plays the role of Mesh Time Relay, both publishes Time Status messages and processes received Time Status messages.

## TAI
The International Atomic Time, the time standard which Bluetooth mesh times are based upon.

## TAI-UTC Delta
The number of seconds between the TAI time and the UTC time

## UTC
Coordinated Universal Time, a commonly used standard for regulating clocks.

## Message
Communication between nodes in a mesh network is accomplished through sending messages. Messages are associated with Models and operate on States. Some messages require a response and are termed acknowledged messages. Others do not and are termed unacknowledged messages. Common message types include those that request the current value of a given State in a particular Element, those which request that the value of a given State in a particular Element be changed, and those which report the current value of a State, possibly in response to the state value having been requested by another node via a acknowledged message.

## Access Message
An Access Message is a class of mesh Message which is either sent from a Model to the Access Layer or is received by a Model from the Access Layer. Access Messages are concerned with reporting or setting State.

## Control Message
Control Messages are a type of mesh Message which are concerned with the operation of the mesh network. Examples include Heartbeat messages and Friend Request messages. Control Messages are processed in the Upper Transportand Lower Transport layers of the mesh protocol stack.

## Acknowledged Message
A acknowledged message is a class of mesh Access Message which must always be responded to. Responses are normally Status Messages. If no response to a acknowledged message is received, the sender must retransmit or cancel the message. Importantly, to avoid the possibility of inadvertently causing multiple state transitions at the receiving Element, in the case of retransmissions being necessary, operations associated with acknowledged messages must be idempotent.

## unacknowledged message
An unacknowledged message is a class of mesh Access Message to which a response is not required. Status Messagesare an example of unacknowledged messages.

## Mesh Beacon
Mesh beacons are packets advertised periodically by nodes and unprovisioned devices. The mesh beacon payload is contained within a Bluetooth GAP AD Type called the Mesh Beacon AD Type. See the Bluetooth Core Specification Supplement for more information on AD Types in general.

Currently, two types of mesh beacon are defined; the Unprovisioned Device Beacon and the Secure Network Beacon.

The Unprovisioned Device Beacon allows a Provisioner to discover the device and initiate the Provisioning procedure.

The Secure Network Beacon is used to indicate the security status of a Node with respect to a particular Subnet the node is a member of, regarding the IV Update and Key Refresh security procedures.

## Status Message
A Status Message is a class of mesh Message which is used to convey the current value of a given State. It may be sent as a response to a Acknowledged Message or sent in response to a locally triggered state change or on a timed basis.

## Idempotence
An operation which produces the same result when executed once or multiple times is said to be idempotent. Mesh Acknowledged Messages must be associated with idempotent operations.

## Publish / Subscribe
Messages sent and received across the mesh network conform to a publish-subscribe model of communication.

Sending messages from one node to a set of one or more other nodes is referred to as Publishing. Configuring a node to receive certain messages is known as Subscribing.

Nodes may publish unsolicited messages or may publish messages in reply to other messages.

Unsolicited messages may be published to a unicast address, group address or virtual address. The address to which messages are published is known as the Publish Address. Reply messages are always published to the source address of the message to which a reply is being sent.

The list of Publish Addresses a node has subscribed to is stored in a Subscription List which is part of the Configuration Server Model. Addresses in the Subscription List are used to select or filter out messages received.

## Server
In a mesh network, *an Element which is a Server*, implements a server model and has one or more items of State which may be subject to State Transitions. State Transitions may be triggered by Messages received from Clients.

## Client
In a mesh network, a Client is an Element which implements a client model and which sends messages to a Server. Unlike a Server, a Client does not have State.

## Control Model
A Control Model implemented by an Element gives it the ability to act as both a Client, with the ability to communicate with other, compatible Servers, and a Server, able to communicate with other, compatible Clients. Control Models may include control logic which specifies the rules for coordinating the interactions between the Control Model and other client and server models.

## Bearer
A Bearer is a communications system or protocol stack which is used to transport data between end points on behalf of another system or protocol stack. The bearer is usually described or depicted as sitting underneath and providing services to, another stack which sits above it. As an example, the Wireless Application Protocol, an early mobile internet technology, could be used over a choice of several different bearers, including SMS and GPRS. Bluetooth mesh may be used over either of two bearers, the Advertising Bearer or the GATT Bearer.

## Advertising Bearer
One of the available bearers in the Bluetooth mesh stack. This bearer makes use of Bluetooth GAP advertising and scanning to receive Messages and broadcast Messages from / to other Nodes.

## GATT Bearer
One of the available bearers in the Bluetooth mesh stack. This bearer allows a device which does not support the Advertising Bearer to communicate indirectly with nodes of a mesh network which do, using a protocol known as the Proxy Protocol. A node which is able to relay mesh messages between nodes which use the Advertising Bearer and nodes which use the GATT Bearer is known as a Proxy Node.

Proxy Protocol PDUs are sent by a GATT Bearer Client by writing to a GATT Characteristic in the Proxy Node called the Mesh Proxy Data In characteristic. PDUs are received by a GATT Bearer Client as notification messages relating to the GATT Mesh Proxy Data Out characteristic.

## Mesh Provisioning Service
The Mesh Provisioning Service is a GATT service, implemented by a Proxy Node, which supports those Proxy Protocol PDUs concerned with Provisioning.

## Mesh Proxy Service
The Mesh Proxy Service is a GATT service, implemented by a Proxy Node, which supports those Proxy Protocol PDUs not concerned with Provisioning.

## Proxy Client
The Mesh Proxy Service, in common with all GATT services defines a client role and a server role. A Bluetooth device which connects to and interacts with a node which implements the Mesh Proxy Service is said to be the Proxy Client with respect to its interaction with the other device, which is referred to in this context as the Proxy Server.

## Proxy Server
The Mesh Proxy Service, in common with all GATT services defines a client role and a server role. A Bluetooth mesh proxy node which implements the Mesh Proxy Service is said to be the Proxy Server with respect to its interaction with a connected GATT client, which is referred to in this context as the Proxy Client.

## Proxy Configuration Message
Proxy Clients can exercise fine control over precisely what network traffic they receive by configuring a filter which the Proxy Server applies. Proxy configuration messages are exchanged between a Proxy Client and Proxy Server and allow the configuration of the proxy filter.

## Proxy Filter
Proxy Clients can control what network traffic they receive by configuring a filter which the Proxy Server applies. This filter is called a proxy filter. Filters take the form of white lists and black lists and they each specify lists of destination addresses. Addresses in the list may be any mix of the supported address types, namely unicast, group or virtual addresses. Messages with destination addresses not included in a white list filter are dropped by the Proxy Server’s proxy filter. Similarly, messages with destinations which are included in black list filters are dropped. Proxy configuration messages are exchanged between the Proxy Client and Proxy Server and allow the configuration of the proxy filter. .

## Node Identity
Node Identity is the name of a field which is included in the Service Data field within advertising packets broadcast by Bluetooth mesh proxy nodes. Its value is derived from a combination of the Proxy node’s Unicast Address and a network identifier, such as the network ID for one of the subnets it is enabled on.

## Heartbeat
Nodes can be configured to send a message known as a Heartbeat message, periodically. The purpose of the Heartbeat message is to indicate to other nodes that the node sending the Heartbeat message is still active and to allow its distance from the recipient to be determined, in terms of the number of hops needed to deliver the Heartbeat message.

Heartbeat behavior is configured using the Configuration Server Model. Amongst other things, it is possible to configure the address to which Heartbeat messages must be sent (typically a Group Address), the frequency with which a Heartbeat message must be sent and whether to send heartbeat messages indefinitely or for a limited and specified number of times.

Heartbeat messages contain and retain unchanged, the initial TTL set by the heartbeat originator. This allows recipients to determine how many hops it took for the message to arrive and therefore to optimise messages they subsequently address to the heartbeat source node by setting the TTL to a value no higher than it needs to be.

Nodes may be configured to send Heartbeat messages whenever particular node Features are enabled or disabled.

## Friend Request
A Friend Request is a type of Control Message which is sent by a Low Power Node to initiate the finding of a Friend.

## More Data
MD is an acronym which stands for More Data and is the name of a single bit field, found within Access Layer PDUs to indicate to a low power node (LPN) that the Friend which sent the message has at least one more message to send.

## Scene
A Scene is a stored collection of States which may be *recalled and made* current by the receipt of a given message or at a specified time. Scenes are identified by a 16-bit Scene Number, which is unique within the mesh network.

Scenes make it easy for entire environments, such as a room, to have each of its mesh nodes, its lights, heating system, air conditioning system and so on, all switch to a predefined, complimentary state, in a single, coordinated action.

## Scene Register
The Scene Register is an array of 17 memorized Scene Numbers with the first array member at index position zero, containing the Scene Number of the currently active Scene or a value of 0x0000 if no Scene is active. The other array members contain the Scene Number of a memorized Scene or the value 0x0000 if no Scene is memorized in that member of the Scene Register array.

## Security Keys
The Bluetooth mesh specification defines two main types of security key; Network Keys (NetKeys) and Application Keys (AppKeys) plus a special type of AppKey, known as Device Keys (DevKeys).

## Network Key (NetKey)
A NetKey secures communication at the Network Layer and is shared across all Nodes in the network or all nodes in a particular Subnet. Possession of a given NetKey is what defines membership of a given mesh network or subnet.

## Application Key (AppKey)
An AppKey secures communication at the Access Layer and is shared across all Nodes which participate in a given mesh Application. A Provisioner is responsible for generating and distributing AppKeys.

## Device Key (DevKey)
Each Node possesses a unique DevKey. Only the node which the DevKey belongs to plus a Provisioner know the DevKey, which is used to secure communication between the node and the Provisioner.

## Network ID
A Network ID is a unique, public identifier derived from a Network Key. Its purpose is to enable the fast and efficient lookup of network keys for use in authentication and encryption operations.

## Key Index
NetKeys and AppKeys are too long to be transported in single segment messages. To make messaging as efficient as possible therefore, keys are allocated a globally unique 12-bit index value known as the Key Index and which acts as a short identifier for the key. Messages include key index values which may be referenced against key lists maintained by Configuration Clients.

## Key Bindings
Application Keys may be used within a single network only. As such, there is an association between an Application Key and a Network Key. This association is known as a Key Binding.

## IV Index
The IV (Initialisation Vector) Index is a 32-bit value which is shared by all Nodes in a network. Its purpose is to provide entropy (randomness) in the calculation of message *Nonce values*. It is updated by the IV Update procedure.

## Nonce
A Nonce is a number which may only be used once. In communications security, a nonce can be used as a way of safeguarding against replay attacks since copies of old communications cannot be reused without detection. In a Bluetooth mesh network, each time a message is encrypted, it is given a new nonce value. The nonce has various parts to it, including a sequence number and a value known as the IV Index. The IV Index gets changed whenever required, to ensure that Nonce values cannot wrap round and be repeated. See the IV Update procedure.

## IV Update
Nonce values must be unique. The sequence number inside a nonce must not be allowed to wrap around, therefore. The IV Index serves this purpose. Whenever a node determines that it is at risk of exhausting its sequence number values within a maximum of 96 hours, or if it determines that another node is in this situation, it initiates the IV Update procedure, which causes a new IV Index value to be selected and used for subsequent communication. During execution of the IV Update procedure, both the old and new IV Index values are accepted.

## Key Refresh
If the security of any one or more of a mesh network’s network or application keys is deemed compromised or at risk of compromise then the Key Refresh Procedure is used to generate and distribute replacement keys. A prime example of keys being compromised concerns the removal of a node from the network. If, for example, a mesh light was faulty and disposed of, then the keys it contains could in theory be harvested and used in what is known as a “trash can attack”. To address the risk of trash can attacks, a Node Removal Procedure is defined. Node Removal includes triggering of the Key Refresh Procedure.

## Network Message Cache
All Nodes must implement a cache which stores all recently seen messages. If a message, on being processed by the network layer, is found to be in the Network Message Cache, it is immediately discarded. This helps optimise performance and energy utilisation of the Node and of the mesh network overall.

## Provisioning（堪比金先生之吸星大法）
“Provisioning” is the process by which a device is added to a mesh network. After being provisioned, a device is referred to as a Node.

Provisioning involves a five step process:

  - Step 1. Beaconing

An unprovisioned device which is not yet in the process of being provisioned indicates its availability to be provisioned by advertising as an Unprovisioned Device beacon.

 - Step 2. Invitation

In this step, the Provisioner uses an available bearer to send an invitation to the device to be provisioned, in the form of a Provisioning Invite PDU. The Beaconing device responds with information about itself in a Provisioning Capabilities PDU.

 - Step 3. Exchanging Public Keys

The Provisioner and the device to be provisioned, exchange their public keys, either directly or using an Out Of Band (OOB) method.

 - Step 4. Authentication

During the authentication step, the device to be provisioned outputs a random, single or multi-digit number to the user in some form, using an action appropriate to its capabilities. For example, it might flash an LED a number of times. The user enters the digit(s) output by the new device into the Provisioner and a cryptographic exchange takes place between the two devices, involving the random number, to complete the authentication of each of the two devices to the other.

 - Step 5. Distribution of the Provisioning Data

After authentication has successfully completed, a session key is generated and used to secure the subsequent distribution of the data required to complete the provisioning process, including the NetKey.

## Provisioner
A Provisioner is a device which is able to add another device to the network. As such, it is responsible for generating and distributing NetKeys. It is expected that Provisioners will typically be smartphone or tablet applications. Other implementations are possible, however.

## Network Interface
The mesh Network Layer supports receiving and sending messages from / to a variety of different bearers. Some nodes will support multiple bearer types, such as supporting both the advertising bearer and the GATT bearer. The Network Layer may have multiple instances of given bearer type, such as for example, to support multiple GATT client connections. An instance of a bearer is connected to the Network Layer via a Network Interface.

A special network interface, the Local Interface is defined and allows the sending of messages between Elements in the same Node.

## Input Filter
An instance of a Network Interface has an associated input filter which decides whether or not a message, received via a particular Bearer should be delivered to the Network Layer.

## Outut Filter
An instance of a Network Interface has an associated output filter which decides whether or not a message, received from the Network Layer should be passed to a Bearer or if instead it should be dropped.

## System Architecture
```
Mesh Stack
```
### Model Layer
The Model Layer is concerned with the implementation of Models and as such, the implementation of behaviors, Messages, States, State Bindings and so on, as defined in one or more model specifications.

### Foundation Model Layer
The Foundation Model Layer is responsible for the implementation of those models concerned with the configuration and management of a mesh network.

### Access Layer
The Access Layer of the Bluetooth mesh protocol stack is responsible for defining how applications can make use of the Upper Transport Layer. This includes defining the format of application data, defining and controlling the encryption and decryption process which is performed in the Upper Transport Layer and verifying that data received from the Upper Transport Layer is for the right network and application, before forwarding the data up the stack.

### Upper Transport Layer
The Upper Transport Layer of the Bluetooth mesh protocol stack is responsible for the encryption, decryption and authentication of application data passing to and from the Access Layer. It also has responsibility for transport control Messages, which are internally generated and sent between the upper transport layers on different peer Nodes. These include Messages related to Friendship and Heartbeats.

### Lower Transport Layer
The Lower Transport Layer takes PDUs from the Upper Transport Layer and sends them to the Lower Transport Layer on a peer device. Where required, it performs segmentation and reassembly of PDUs. For longer packets, which will not fit into a single Transport PDU, the Lower Transport Layer will perform segmentation, splitting the PDU into multiple Transport PDUs. The receiving Lower Transport Layer on the other device, will reassemble the segments into a single Upper Transport Layer PDU and pass this up the stack.

### Network Layer
The Network Layer defines the various Message address types and a network Message format which allows Transport Layer PDUs to be transported by the bearer layer. It can support multiple bearers, each of which may have multiple network interfaces, including the local interface, which is used for communication between Elements that are part of the same Node. The Network Layer determines which network interface(s) to output Messages over. An input filter is applied to Messages arriving from the Bearer Layer, to determine whether or not they should be delivered to the network layer for further processing. Output Messages are subject to an output filter to control whether or not they are dropped or delivered to the Bearer Layer.

The Relay and Proxy features may be implemented by the Network Layer.

### Bearer Layer
The Bearer Layer defines how PDUs are transported between nodes using an underlying Bluetooth Low Energy stack. Currently, two bearers are defined, the Advertising Bearer and the GATT Bearer.

# Limits
 - 32767 *Elements(NOT NODES OR DEVICES)* in a mesh network

 - 127 Hops can be made by a mesh message at most

 - 16383 Group Addresses in a mesh network

 - 70 trillion Virtual Addresses in a mesh network

 - 340 unidecillion mesh networks

 - 4096 Applications in a mesh network

 - 4096 Subnets in a mesh network

 - 65535 Scenes in a mesh network

```
A Node that is away from a network for longer than 48 weeks must be reprovisioned
```
