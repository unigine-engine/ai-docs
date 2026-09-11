# Unigine::Plugins::DataBridge::NetworkManager Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class manages the DataBridge network.


## NetworkManager Class

### Members

## double getIFps () const

Returns the current duration of the last frame. This method is more accurate than the same method of the [Game](../../../../api/library/engine/class.game_usc.md#getIFps_float) class and returns a double-precision value.
### Return value

Current duration of the previous frame, in seconds.
## double getTime () const

Returns the current server frame time, in seconds (even if called from a Client computer). It is the time of the last buffer swap operation (i.e., beginning of the next frame). This value is more accurate than that of the [Game](../../../../api/library/engine/class.game_usc.md#Time) class.
### Return value

Current server frame time, in seconds
## bool isHttpServerInitialized () const

Returns the current
### Return value

**true** if is enabled ; otherwise **false**.
---

## Server initServerBroadcast ( string broadcast_address , int udp_port )

Initializes the application as the Server with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Clients must be initialized with the same mode enabled.
### Arguments

- *string* **broadcast_address** - Broadcast address of the Server that is used to send data to Clients over the network.
- *int* **udp_port** - UDP port to be used.

### Return value

Server interface instance.
## Server initServerMulticast ( string multicast_address , int udp_port )

Initializes the application as the Server with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Clients must be initialized with the same mode enabled.
### Arguments

- *string* **multicast_address** - Multicast address of the Server that is used to send data to Clients over the network.
- *int* **udp_port** - UDP port to be used.

### Return value

Server interface instance.
## Server initServerUnicast ( int udp_port )

Initializes the application as the Server with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Clients must be initialized with the same mode enabled.
### Arguments

- *int* **udp_port** - UDP port to be used.

### Return value

Server interface instance.
## Client initClientBroadcast ( int udp_port )

Initializes the application as a Client with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Server's IP address will be detected automatically. Server must be initialized with the same mode.
### Arguments

- *int* **udp_port** - UDP port to be used.

### Return value

Client interface instance.
## Client initClientBroadcast ( string server_address , int udp_port )

Initializes the application as a Client with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Server's IP address is specified explicitly. Server must be initialized with the same mode.
### Arguments

- *string* **server_address** - Server IP address to be used.
- *int* **udp_port** - UDP port to be used.

### Return value

Client interface instance.
## Client initClientMulticast ( string multicast_address , int udp_port )

Initializes the application as a Client with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Server's IP address will be detected automatically. Server must be initialized with the same mode.
### Arguments

- *string* **multicast_address** - Multicast address to be used.
- *int* **udp_port** - UDP port to be used.

### Return value

Client interface instance.
## Client initClientMulticast ( string server_address , string multicast_address , int udp_port )

Initializes the application as a Client with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Server's IP address is specified explicitly. Server must be initialized with the same mode.
### Arguments

- *string* **server_address** - Server IP address to be used.
- *string* **multicast_address** - Multicast address to be used.
- *int* **udp_port** - UDP port to be used.

### Return value

Client interface instance.
## Client initClientUnicast ( int server_udp_port , int client_udp_port )

Initializes the application as a Client with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Server's IP address will be detected automatically. Server must be initialized with the same mode.
### Arguments

- *int* **server_udp_port** - UDP port to be used by the Server.
- *int* **client_udp_port** - UDP port to be used by the Client.

### Return value

Client interface instance.
## Client initClientUnicast ( string server_address , int server_udp_port , int client_udp_port )

Initializes the application as a Client with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Server's IP address is specified explicitly. Server must be initialized with the same mode.
### Arguments

- *string* **server_address** - Server IP address to be used.
- *int* **server_udp_port** - UDP port to be used by the Server.
- *int* **client_udp_port** - UDP port to be used by the Client.

### Return value

Client interface instance.
## bool isInitialized ( )

Returns a value indicating if the network manager is initialized.
### Return value

true if the network manager is initialized; otherwise, false.
## bool isServer ( )

Returns the value indicating whether the application is Server.
### Return value

true if the application is Server, otherwise false.
## NetworkInstance getInstance ( )

Returns the [base class interface](../../../../api/library/plugins/databridge/class.networkinstance_usc.md) for Server and Client.
### Return value

[network instance](../../../../api/library/plugins/databridge/class.networkinstance_usc.md) interface. It is the base class for Server and Client.
## Server getServer ( )

Returns the [Server interface](../../../../api/library/plugins/databridge/class.server_usc.md).
### Return value

[Server interface](../../../../api/library/plugins/databridge/class.server_usc.md) instance.
## Client getClient ( )

Returns the [Client interface](../../../../api/library/plugins/databridge/class.client_usc.md).
### Return value

[Client interface](../../../../api/library/plugins/databridge/class.client_usc.md) instance.
## void destroyInstance ( )

Performs shutdown and destroys the network instance.
> **Notice:** Called automatically, when the DataBridge plugin is unloaded.


## int initHttpServer ( int port )

### Arguments

- *int* **port**

## int stopHttpServer ( )
