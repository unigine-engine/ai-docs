# Unigine::Plugins::DataBridge::Server Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is inherited from [NetworkInstance](../../../../api/library/plugins/databridge/class.networkinstance_usc.md) class.


## Server Class

---

## bool init ( int in_addressing_method , string broadcast_address , string multicast_address , int udp_port )

Initializes the Server with the specified arguments.
### Arguments

- *int* **in_addressing_method** - Addressing mode to be used.
- *string* **broadcast_address** - Broadcast address to be used.
- *string* **multicast_address** - Multicast address to be used.
- *int* **udp_port** - Server UDP port to be used.

### Return value

true if the Server is initialized; otherwise, false.
