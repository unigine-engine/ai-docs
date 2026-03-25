# Unigine::Plugins::DataBridge::Server Class (CS)


This class is inherited from [NetworkInstance](../../../../api/library/plugins/databridge/class.networkinstance_cs.md) class.


## Server Class

### Members

---

## bool Init ( NetworkInstance.ADDRESSING_METHOD in_addressing_method , string broadcast_address , string multicast_address , ushort udp_port )

Initializes the Server with the specified arguments.
### Arguments

- *[NetworkInstance.ADDRESSING_METHOD](../../../../api/library/plugins/databridge/class.networkinstance_cs.md#ADDRESSING_METHOD)* **in_addressing_method** - Addressing mode to be used.
- *string* **broadcast_address** - Broadcast address to be used.
- *string* **multicast_address** - Multicast address to be used.
- *ushort* **udp_port** - Server UDP port to be used.

### Return value

true if the Server is initialized; otherwise, false.
