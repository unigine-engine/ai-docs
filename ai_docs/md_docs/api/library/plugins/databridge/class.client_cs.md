# Unigine::Plugins::DataBridge::Client Class (CS)


This class is inherited from [NetworkInstance](../../../../api/library/plugins/databridge/class.networkinstance_cs.md) class.


## Client Class

### Properties

## 🔒︎ long ID

The ID of the Client.
### Members

---

## bool Init ( NetworkInstance.ADDRESSING_METHOD in_addressing_method , string server_address , string multicast_address , ushort server_udp_port , ushort client_udp_port )

Initializes the Client with the specified arguments.
### Arguments

- *[NetworkInstance.ADDRESSING_METHOD](../../../../api/library/plugins/databridge/class.networkinstance_cs.md#ADDRESSING_METHOD)* **in_addressing_method** - Addressing mode to be used.
- *string* **server_address** - Server IP address to be used.
- *string* **multicast_address** - Multicast address to be used.
- *ushort* **server_udp_port** - Server UDP port to be used.
- *ushort* **client_udp_port** - Client UDP port to be used.

### Return value

true if the Client is initialized; otherwise, false.
## bool IsConnected ( )

Returns a value indicating if the Client is connected.
### Return value

true if the Client is connected; otherwise, false.
## bool IsReady ( )

Returns a value indicating if the Client is ready for operation: is connected and received data from the Server.
### Return value

true if the Client is ready for operation; otherwise - false.
