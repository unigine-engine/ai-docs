# Unigine::Plugins::DataBridge::NetworkManager Class (CS)


This class manages the DataBridge network.


## NetworkManager Class

### Properties

## 🔒︎ double IFps

The duration of the last frame. This method is more accurate than the same method of the [Game](../../../../api/library/engine/class.game_cs.md#getIFps_float) class and returns a double-precision value.
## 🔒︎ double Time

The server frame time, in seconds (even if called from a Client computer). It is the time of the last buffer swap operation (i.e., beginning of the next frame). This value is more accurate than that of the [Game](../../../../api/library/engine/class.game_cs.md#Time) class.
## 🔒︎ bool IsHttpServerInitialized

The
### Members

---

## Server InitServerBroadcast ( string broadcast_address , ushort udp_port )

Initializes the application as the Server with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Clients must be initialized with the same mode enabled.
### Arguments

- *string* **broadcast_address** - Broadcast address of the Server that is used to send data to Clients over the network.
- *ushort* **udp_port** - UDP port to be used.

### Return value

Server interface instance.
## Server InitServerMulticast ( string multicast_address , ushort udp_port )

Initializes the application as the Server with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Clients must be initialized with the same mode enabled.
### Arguments

- *string* **multicast_address** - Multicast address of the Server that is used to send data to Clients over the network.
- *ushort* **udp_port** - UDP port to be used.

### Return value

Server interface instance.
## Server InitServerUnicast ( ushort udp_port )

Initializes the application as the Server with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Clients must be initialized with the same mode enabled.
### Arguments

- *ushort* **udp_port** - UDP port to be used.

### Return value

Server interface instance.
## Client InitClientBroadcast ( ushort udp_port )

Initializes the application as a Client with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Server's IP address will be detected automatically. Server must be initialized with the same mode.
### Arguments

- *ushort* **udp_port** - UDP port to be used.

### Return value

Client interface instance.
## Client InitClientBroadcast ( string server_address , ushort udp_port )

Initializes the application as a Client with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Server's IP address is specified explicitly. Server must be initialized with the same mode.
### Arguments

- *string* **server_address** - Server IP address to be used.
- *ushort* **udp_port** - UDP port to be used.

### Return value

Client interface instance.
## Client InitClientMulticast ( string multicast_address , ushort udp_port )

Initializes the application as a Client with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Server's IP address will be detected automatically. Server must be initialized with the same mode.
### Arguments

- *string* **multicast_address** - Multicast address to be used.
- *ushort* **udp_port** - UDP port to be used.

### Return value

Client interface instance.
## Client InitClientMulticast ( string server_address , string multicast_address , ushort udp_port )

Initializes the application as a Client with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Server's IP address is specified explicitly. Server must be initialized with the same mode.
### Arguments

- *string* **server_address** - Server IP address to be used.
- *string* **multicast_address** - Multicast address to be used.
- *ushort* **udp_port** - UDP port to be used.

### Return value

Client interface instance.
## Client InitClientUnicast ( ushort server_udp_port , ushort client_udp_port )

Initializes the application as a Client with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Server's IP address will be detected automatically. Server must be initialized with the same mode.
### Arguments

- *ushort* **server_udp_port** - UDP port to be used by the Server.
- *ushort* **client_udp_port** - UDP port to be used by the Client.

### Return value

Client interface instance.
## Client InitClientUnicast ( string server_address , ushort server_udp_port , ushort client_udp_port )

Initializes the application as a Client with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Server's IP address is specified explicitly. Server must be initialized with the same mode.
### Arguments

- *string* **server_address** - Server IP address to be used.
- *ushort* **server_udp_port** - UDP port to be used by the Server.
- *ushort* **client_udp_port** - UDP port to be used by the Client.

### Return value

Client interface instance.
## bool IsInitialized ( )

Returns a value indicating if the network manager is initialized.
### Return value

true if the network manager is initialized; otherwise, false.
## bool IsServer ( )

Returns the value indicating whether the application is Server.
### Return value

true if the application is Server, otherwise false.
## NetworkInstance GetInstance ( )

Returns the [base class interface](../../../../api/library/plugins/databridge/class.networkinstance_cs.md) for Server and Client.
### Return value

[network instance](../../../../api/library/plugins/databridge/class.networkinstance_cs.md) interface. It is the base class for Server and Client.
## Server GetServer ( )

Returns the [Server interface](../../../../api/library/plugins/databridge/class.server_cs.md).
### Return value

## Client GetClient ( )

Returns the [Client interface](../../../../api/library/plugins/databridge/class.client_cs.md).
### Return value

[Client interface](../../../../api/library/plugins/databridge/class.client_cs.md) instance.
## void DestroyInstance ( )

Performs shutdown and destroys the network instance.
> **Notice:** Called automatically, when the DataBridge plugin is unloaded.


## bool InitHttpServer ( ushort port )

### Arguments

- *ushort* **port**

## bool StopHttpServer ( )
