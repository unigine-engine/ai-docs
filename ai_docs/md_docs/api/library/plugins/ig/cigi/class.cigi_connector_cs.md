# IG::CIGI::Connector Class (CS)


This class implements the connection between the IG Plugin and the CIGI protocol.

> **Notice:** [IG](../../../../../api/library/plugins/ig/api/index.md) plugin must be loaded.


## IG::CIGI::Connector Class

### Enums

## CIGI_MODE

| Name | Description |
|---|---|
| **STANDBY** = 0 | Standby mode of the IG. This is the normal real-time operating mode for the IG. All packets issued by the Host will be processed by the IG. The IG should not perform diagnostics in this mode. |
| **OPERATE** = 1 | Operate mode of the IG. This is the normal real-time operating mode for the IG. All packets issued by the Host will be processed by the IG. The IG should not perform diagnostics in this mode. |
| **DEBUG** = 2 | Debug mode of the IG. This mode is similar to the Operate mode but provides data and/or error logging and other debugging features to aid integration or troubleshooting of the Host and IG interface. Because of the overhead of these debugging features, the IG may not always operate in a hard real-time fashion. |
| **OFFLINE** = 3 | Offline Maintenance mode of the IG. In this mode, the IG ignores all data from the Host and sends only Start of Frame packets. This mode can be activated only from the IG. Because the IG Control packets from the Host are ignored by the IG, the IG must be placed into Reset/Standby mode before the Host can initiate further mode changes. |

### Properties

## 🔒︎ bool IsInitialized

The value indicating if the CIGI Connector was initialized successfully.
## int IGStatus

The current IG status. The following values are supported:
- 0 - normal
- 1-255 - an error has occurred

.
## bool Synchronous

The value indicating if synchronous operation mode is currently enabled (when disabled, asynchronous mode is used).
## 🔒︎ bool IsInterpolation

The value indicating if interpolation and extrapolation are enabled.
## CIGI.CIGI_MODE IGMode

The current IG mode.
## 🔒︎ uint IGFrame

The number of the current frame for the IG.
## 🔒︎ uint HostFrame

The number of the current frame for the Host.
## 🔒︎ double Time

The IG's simulation time.
## 🔒︎ double LastReceivedHostTime

The last received Host time (*timestamp* value in "IG Control").
### Members

---

## int Init ( int version , string host , int send , int recv , int size = 1432 )

Initializes the CIGI Connector using the given parameters.
### Arguments

- *int* **version** - CIGI protocol version. One of the [CIGI_VERSION_*](#CIGI_VERSION_30) values.
- *string* **host** - CIGI Host address.
- *int* **send** - TCP port number to be used for sending packets to the CIGI Host.
- *int* **recv** - TCP port number to be used for receiving packets from the CIGI Host.
- *int* **size** - Packet size. The default value is 1432.

### Return value

1 if the CIGI Connector was initialized successfully; otherwise, 0.
## int Shutdown ( )

Returns a value indicating if the CIGI Connector was shutdown successfully.
### Return value

true if the CIGI Connector was shutdown successfully; otherwise, false.
## IntPtr AddOnConnectCallback ( OnConnectDelegate func )

Adds a callback function to be fired when the Host has connected.
### Arguments

- *OnConnectDelegate* **func** - Callback function with the following signature: void OnConnectDelegate(*void*)

### Return value

ID of the last added connect callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnConnectCallback_void_ptr_bool) this callback when necessary.
## bool RemoveOnConnectCallback ( IntPtr id )

Removes the specified callback from the list of Connect callbacks.
### Arguments

- *IntPtr* **id** - Connect callback ID obtained when [adding](#addOnConnectCallback_CallbackBase_ptr_void_ptr) it.

### Return value

True if the Connect callback with the given ID was removed successfully; otherwise false.
## IntPtr AddOnReceivePacketCallback ( int cigi_opcode , OnReceivePacketDelegate func )

Sets a callback function to be fired when a packet of the specified type has been received from the Host.
### Arguments

- *int* **cigi_opcode** - CIGI data packet opcode. One of the [CIGI_OPCODE_*](#CIGI_OPCODE_IG_CONTROL) values.
- *OnReceivePacketDelegate* **func** - Callback function with the following signature: void OnReceivePacketDelegate(*CigiHostPacket*)

### Return value

ID of the last added Receive Packet callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnReceivePacketCallback_void_ptr_bool) this callback when necessary.
## bool RemoveOnReceivePacketCallback ( IntPtr id )

Removes the specified callback from the list of Receive Packet callbacks.
### Arguments

- *IntPtr* **id** - Receive Packet callback ID obtained when [adding](#addOnReceivePacketCallback_int_CallbackBase1_ptr_void_ptr) it.

### Return value

true if the Receive Packet callback with the given ID was removed successfully; otherwise false.
## int GetNumHostPackets ( )

Returns the total number of packets received from the Host.
### Return value

Total number of packets received from the Host.
## CigiIGPacket GetHostPacket ( int num )

Returns the specified [CIGI Host packet](../../../../../api/library/plugins/ig/cigi/class.icigihostpacket_cs.md).
### Arguments

- *int* **num** - ID of the Host packet.

### Return value

CIGI Host packet.
## CigiIGPacket CreateIGPacket ( int ig_opcode )

Creates IG Packet to be sent to the Host.
### Arguments

- *int* **ig_opcode** - IG opcode, one of [CIGI_OPCODE_*](#CIGI_OPCODE_START_OF_FRAME) values.

### Return value

IG Packet to be sent to the Host.
## void AddIGPacket ( CigiIGPacket packet )

Sends the specified [IG packet](../../../../../api/library/plugins/ig/cigi/class.icigiigpacket_cs.md) to the Host.
### Arguments

- *[CigiIGPacket](../../../../../api/library/plugins/ig/cigi/class.icigiigpacket_cs.md)* **packet** - IG Packet to be sent to the Host.

## void SetProcessPacket ( int op_code , bool enabled )

Sets a value indicating if the specified IG packets received are to be processed or skipped.
### Arguments

- *int* **op_code** - IG opcode, one of [CIGI_OPCODE_*](#CIGI_OPCODE_START_OF_FRAME) values.
- *bool* **enabled** - true to process packets of the specified type, **false** to skip them.

## void ShowDebug ( )

Displays the debug information.
