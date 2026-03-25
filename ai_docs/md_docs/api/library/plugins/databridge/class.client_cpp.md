# Unigine::Plugins::DataBridge::Client Class (CPP)

**Header:** #include <plugins/Unigine/DataBridge/UnigineDataBridge.h>


This class is inherited from [NetworkInstance](../../../../api/library/plugins/databridge/class.networkinstance_cpp.md) class.


## Client Class

### Members

## long long getID () const

Returns the current ID of the Client.
### Return value

Current ID of the client combined as follows: IP address (32 bits) + port number (16 bits).
---

## bool init ( NetworkInstance::ADDRESSING_METHOD in_addressing_method , const char * server_address , const char * multicast_address , unsigned short server_udp_port , unsigned short client_udp_port )

Initializes the Client with the specified arguments.
### Arguments

- *[NetworkInstance::ADDRESSING_METHOD](../../../../api/library/plugins/databridge/class.networkinstance_cpp.md#ADDRESSING_METHOD)* **in_addressing_method** - Addressing mode to be used.
- *const char ** **server_address** - Server IP address to be used.
- *const char ** **multicast_address** - Multicast address to be used.
- *unsigned short* **server_udp_port** - Server UDP port to be used.
- *unsigned short* **client_udp_port** - Client UDP port to be used.

### Return value

true if the Client is initialized; otherwise, false.
## bool isConnected ( ) const

Returns a value indicating if the Client is connected.
### Return value

true if the Client is connected; otherwise, false.
## bool isReady ( ) const

Returns a value indicating if the Client is ready for operation: is connected and received data from the Server.
### Return value

true if the Client is ready for operation; otherwise - false.
