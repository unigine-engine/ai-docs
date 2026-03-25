# Unigine::Plugins::DataBridge::Client Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is inherited from [NetworkInstance](../../../../api/library/plugins/databridge/class.networkinstance_usc.md) class.


## Client Class

### Members

## long getID () const

Returns the current ID of the Client.
### Return value

Current ID of the client combined as follows: IP address (32 bits) + port number (16 bits).
---

## bool init ( int in_addressing_method , string server_address , string multicast_address , int server_udp_port , int client_udp_port )

Initializes the Client with the specified arguments.
### Arguments

- *int* **in_addressing_method** - Addressing mode to be used.
- *string* **server_address** - Server IP address to be used.
- *string* **multicast_address** - Multicast address to be used.
- *int* **server_udp_port** - Server UDP port to be used.
- *int* **client_udp_port** - Client UDP port to be used.

### Return value

true if the Client is initialized; otherwise, false.
## bool isConnected ( )

Returns a value indicating if the Client is connected.
### Return value

true if the Client is connected; otherwise, false.
## bool isReady ( )

Returns a value indicating if the Client is ready for operation: is connected and received data from the Server.
### Return value

**1** if the Client is ready for operation; otherwise - **0**.
