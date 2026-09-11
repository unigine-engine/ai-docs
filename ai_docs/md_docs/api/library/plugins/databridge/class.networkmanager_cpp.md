# Unigine::Plugins::DataBridge::NetworkManager Class (CPP)

**Header:** #include <plugins/Unigine/DataBridge/UnigineDataBridge.h>


This class manages the DataBridge network.


## NetworkManager Class

### Members

## double getIFps () const

Returns the current duration of the last frame. This method is more accurate than the same method of the [Game](../../../../api/library/engine/class.game_cpp.md#getIFps_float) class and returns a double-precision value.
### Return value

Current duration of the previous frame, in seconds.
## double getTime () const

Returns the current server frame time, in seconds (even if called from a Client computer). It is the time of the last buffer swap operation (i.e., beginning of the next frame). This value is more accurate than that of the [Game](../../../../api/library/engine/class.game_cpp.md#Time) class.
### Return value

Current server frame time, in seconds
## bool isHttpServerInitialized () const

Returns the current
### Return value

**true** if is enabled ; otherwise **false**.
---

## Server * initServerBroadcast ( const char * broadcast_address , unsigned short udp_port )

Initializes the application as the Server with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Clients must be initialized with the same mode enabled.
### Arguments

- *const char ** **broadcast_address** - Broadcast address of the Server that is used to send data to Clients over the network.
- *unsigned short* **udp_port** - UDP port to be used.

### Return value

Pointer to the Server interface.
## Server * initServerMulticast ( const char * multicast_address , unsigned short udp_port )

Initializes the application as the Server with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Clients must be initialized with the same mode enabled.
### Arguments

- *const char ** **multicast_address** - Multicast address of the Server that is used to send data to Clients over the network.
- *unsigned short* **udp_port** - UDP port to be used.

### Return value

Pointer to the Server interface.
## Server * initServerUnicast ( unsigned short udp_port )

Initializes the application as the Server with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Clients must be initialized with the same mode enabled.
### Arguments

- *unsigned short* **udp_port** - UDP port to be used.

### Return value

Pointer to the Server interface.
## Client * initClientBroadcast ( unsigned short udp_port )

Initializes the application as a Client with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Server's IP address will be detected automatically. Server must be initialized with the same mode.
### Arguments

- *unsigned short* **udp_port** - UDP port to be used.

### Return value

Pointer to the Client interface.
## Client * initClientBroadcast ( const char * server_address , unsigned short udp_port )

Initializes the application as a Client with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Server's IP address is specified explicitly. Server must be initialized with the same mode.
### Arguments

- *const char ** **server_address** - Server IP address to be used.
- *unsigned short* **udp_port** - UDP port to be used.

### Return value

Pointer to the Client interface.
## Client * initClientMulticast ( const char * multicast_address , unsigned short udp_port )

Initializes the application as a Client with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Server's IP address will be detected automatically. Server must be initialized with the same mode.
### Arguments

- *const char ** **multicast_address** - Multicast address to be used.
- *unsigned short* **udp_port** - UDP port to be used.

### Return value

Pointer to the Client interface.
## Client * initClientMulticast ( const char * server_address , const char * multicast_address , unsigned short udp_port )

Initializes the application as a Client with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Server's IP address is specified explicitly. Server must be initialized with the same mode.
### Arguments

- *const char ** **server_address** - Server IP address to be used.
- *const char ** **multicast_address** - Multicast address to be used.
- *unsigned short* **udp_port** - UDP port to be used.

### Return value

Pointer to the Client interface.
## Client * initClientUnicast ( unsigned short server_udp_port , unsigned short client_udp_port )

Initializes the application as a Client with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Server's IP address will be detected automatically. Server must be initialized with the same mode.
### Arguments

- *unsigned short* **server_udp_port** - UDP port to be used by the Server.
- *unsigned short* **client_udp_port** - UDP port to be used by the Client.

### Return value

Pointer to the Client interface.
## Client * initClientUnicast ( const char * server_address , unsigned short server_udp_port , unsigned short client_udp_port )

Initializes the application as a Client with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Server's IP address is specified explicitly. Server must be initialized with the same mode.
### Arguments

- *const char ** **server_address** - Server IP address to be used.
- *unsigned short* **server_udp_port** - UDP port to be used by the Server.
- *unsigned short* **client_udp_port** - UDP port to be used by the Client.

### Return value

Pointer to the Client interface.
## bool isInitialized ( ) const

Returns a value indicating if the network manager is initialized.
### Return value

true if the network manager is initialized; otherwise, false.
## bool isServer ( ) const

Returns the value indicating whether the application is Server.
### Return value

true if the application is Server, otherwise false.
## NetworkInstance * getInstance ( ) const

Returns the [base class interface](../../../../api/library/plugins/databridge/class.networkinstance_cpp.md) for Server and Client.
### Return value

Pointer to the [network instance](../../../../api/library/plugins/databridge/class.networkinstance_cpp.md) interface. It is the base class for Server and Client.
## Server * getServer ( ) const

Returns the [Server interface](../../../../api/library/plugins/databridge/class.server_cpp.md).
### Return value

Pointer to the [Server interface](../../../../api/library/plugins/databridge/class.server_cpp.md).
## Client * getClient ( ) const

Returns the [Client interface](../../../../api/library/plugins/databridge/class.client_cpp.md).
### Return value

Pointer to the [Client interface](../../../../api/library/plugins/databridge/class.client_cpp.md).
## void destroyInstance ( )

Performs shutdown and destroys the network instance.
> **Notice:** Called automatically, when the DataBridge plugin is unloaded.


## bool initHttpServer ( unsigned short port )

### Arguments

- *unsigned short* **port**

## bool stopHttpServer ( )
