# Unigine::Plugins::DataBridge::NetworkInstance Class (CS)


This class provides access to the network instance, which may be either [Server](../../../../api/library/plugins/databridge/class.server_cs.md) or [Client](../../../../api/library/plugins/databridge/class.client_cs.md).


## NetworkInstance Class

### Enums

## ADDRESSING_METHOD

| Name | Description |
|---|---|
| **BROADCAST** = 0 | [Broadcast addressing mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) (one-to-all): hosts have different IP-addresses, but a single port. |
| **UNICAST** = 1 | [Unicast addressing mode](../../../../code/plugins/syncker/index.md#addressing_unicast) (one-to-one): hosts have different IP-addresses (some may be the same) and different ports. |
| **MULTICAST** = 2 | [Multicast addressing mode](../../../../code/plugins/syncker/index.md#addressing_multicast) (one-to-many): hosts have different IP-addresses, but a single port. |

### Properties

## 🔒︎ double Time

The server frame time, in seconds (even if called from a Client computer). It is the time of the last buffer swap operation (i.e., beginning of the next frame). This value is more accurate than that of the [Game](../../../../api/library/engine/class.game_cs.md#Time) class.
## 🔒︎ double IFps

The duration of the last frame. This method is more accurate than the same method of the [Game](../../../../api/library/engine/class.game_cs.md#getIFps_float) class and returns a double-precision value.
### Members

---

## void Update ( )

Updates the network instance.
## void Shutdown ( )

Shuts down the network instance.
## void SetDisconnectTimeout ( float seconds )

Sets a timeout period after which a Client is considered as disconnected.
### Arguments

- *float* **seconds** - Duration of the timeout period, in seconds.

## float GetDisconnectTimeout ( )

Returns the current timeout period after which a Client is considered as disconnected.
### Return value

Duration of the timeout period, in seconds.
