# Unigine::Plugins::DataBridge::Server Class (CPP)

**Header:** #include <plugins/Unigine/DataBridge/UnigineDataBridge.h>


This class is inherited from [NetworkInstance](../../../../api/library/plugins/databridge/class.networkinstance_cpp.md) class.


## Server Class

---

## bool init ( NetworkInstance::ADDRESSING_METHOD in_addressing_method , const char * broadcast_address , const char * multicast_address , unsigned short udp_port )

Initializes the Server with the specified arguments.
### Arguments

- *[NetworkInstance::ADDRESSING_METHOD](../../../../api/library/plugins/databridge/class.networkinstance_cpp.md#ADDRESSING_METHOD)* **in_addressing_method** - Addressing mode to be used.
- *const char ** **broadcast_address** - Broadcast address to be used.
- *const char ** **multicast_address** - Multicast address to be used.
- *unsigned short* **udp_port** - Server UDP port to be used.

### Return value

true if the Server is initialized; otherwise, false.
