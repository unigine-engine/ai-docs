# Unigine::Plugins::Syncker::Syncker Class (CS)


This class represents the base interface of the Syncker, from which Master and Slave interfaces are inherited. It contains all common functions available for both Slave and Master.


> **Notice:** [Syncker](../../../../code/plugins/syncker/index.md) plugin must be loaded.


## Syncker Class

### Enums

## DELIVERY_METHOD

[Delivery mode](../../../../code/plugins/syncker/index.md#delivery_modes) to be used by the Syncker.
| Name | Description |
|---|---|
| **UNRELIABLE** = 0 | [Unreliable delivery mode](../../../../code/plugins/syncker/index.md#delivery_unreliable). Pure UDP. Packets may be lost, duplicated, or received in an order that differs from the one they were sent. Packets are not compressed, fragmented, or merged. |
| **SEQUENCED** = 1 | [Sequenced delivery mode](../../../../code/plugins/syncker/index.md#delivery_sequenced). Packets may be lost, but never duplicated, they arrive in the exact order they were sent. |
| **RELIABLE** = 2 | [Reliable delivery mode](../../../../code/plugins/syncker/index.md#delivery_reliable). Reliable and sequenced mode, enabled by default. All packets shall be delivered to the recipient in the exact order they were sent. |

## ADDRESSING_METHOD

[Addressing mode](../../../../code/plugins/syncker/index.md#addressing_modes) to be used by the Syncker.
| Name | Description |
|---|---|
| **BROADCAST** = 0 | [Broadcast addressing mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) (one-to-all): hosts have different IP-addresses, but a single port. |
| **UNICAST** = 1 | [Unicast addressing mode](../../../../code/plugins/syncker/index.md#addressing_unicast) (one-to-one): hosts have different IP-addresses (some may be the same) and different ports. |
| **MULTICAST** = 2 | [Multicast addressing mode](../../../../code/plugins/syncker/index.md#addressing_multicast) (one-to-many): hosts have different IP-addresses, but a single port. |

## SWAP_SYNC_MODE

Buffer swap synchronization mode.
| Name | Description |
|---|---|
| **DEFAULT** = 0 | Default buffer swap synchronization. |
| **NVIDIA** = | NVIDIA buffer swap synchronization. Detailed information on current sync status is displayed in the console. > **Notice:** This mode is available only for NVIDIA Quadro GPUs with G-SYNC support. |

### Properties

## double ExtrapolationPeriod

***Console*:**`syncker_extrapolation_period`The [extrapolation](../../../../code/plugins/syncker/index.md#interpolation) period value for the computer.
## double InterpolationPeriod

***Console*:**`syncker_interpolation_period`The [interpolation](../../../../code/plugins/syncker/index.md#interpolation) period value for the computer.
It is recommended to use this method when setting the [frequency of sending packets](../../../../api/library/plugins/syncker/class.syncker_master_cs.md#getSendRate_float) to Slaves.


```cpp
//On the Master
master->setSendRate(15.0f); // send packets 15 times per second

//Both on the Master and all Slaves
syncker->setInterpolationPeriod(0.1f); // 100 ms delay

```


## bool Interpolation

***Console*:**`syncker_interpolation`The value indicating if [interpolation and extrapolation](../../../../code/plugins/syncker/index.md#interpolation) are enabled for the computer to tackle the problem of lost packets between the master and slaves.
## float DisconnectTimeout

The timeout period after which a Slave is considered as disconnected.
## 🔒︎ Syncker.ADDRESSING_METHOD AddressingMethod

The packets [addressing method](../../../../code/plugins/syncker/index.md#addressing_modes) currently used by the Syncker for communication.
## 🔒︎ double IFps

The duration of the last frame, in seconds. This value is more accurate than that of the *[Game](../../../../api/library/engine/class.game_cs.md#IFps)* class and is represented by a double-precision value.
## 🔒︎ double Time

The Master frame time, in seconds, (even if called from a Slave computer). It is the time of the last buffer swap operation (i.e., beginning of the next frame). This value is more accurate than that of the *[Game](../../../../api/library/engine/class.game_cs.md#Time)* class and is represented by a double-precision value.
## string ComputerName

The name of the computer to be used when assigning a viewport to be displayed (see *[SpiderVision](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md)* plugin). This name can be set at the application startup via the [`computer_name`](../../../../code/plugins/syncker/options.md#computer_name) command-line argument. If not specified the name is obtained from the *[SpiderVision](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md)* plugin, or if the latter is unavailable the name will be taken from the Operating System settings.
## 🔒︎ Syncker.SWAP_SYNC_MODE SwapSyncMode

The buffer swap synchronization mode currently used by the Syncker.
### Members

---

## bool IsInterpolation ( Node node )

Returns a value indicating if the given node is [interpolated](../../../../code/plugins/syncker/index.md#interpolation) by the Syncker.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to be checked.

### Return value

true if the given node is [interpolated](../../../../code/plugins/syncker/index.md#interpolation) by the Syncker; otherwise, false.
## void SetDebug ( bool enabled , int x , int y , int align_mask )

***Console*:**`syncker_debug`Enables or disables displaying of debug information at the specified position on the screen.
### Arguments

- *bool* **enabled** - true to display the debug information; false - to hide it.
- *int* **x** - Horizontal margin of the debug information block. The default value is 10.
- *int* **y** - Vertical margin of the debug information block. The default value is 10.
- *int* **align_mask** - Alignment mask. One of the [Gui::ALIGN_*](../../../../api/library/gui/class.gui_cs.md#ALIGN_BOTTOM) variables or their combination. The default value is Gui::ALIGN_RIGHT | Gui::ALIGN_BOTTOM.

## bool IsDebug ( )

***Console*:**`syncker_debug`Returns a value indicating if the debug information is to be displayed.
### Return value

true if the debug information is to be displayed; otherwise, false.
## bool SendMessage ( string channel , Blob message , Syncker.DELIVERY_METHOD delivery_method = DELIVERY_METHOD.RELIABLE )

Sends a user message contained in the specified buffer using the given delivery method to the specified named channel via the UDP protocol.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *[Blob](../../../../api/library/common/class.blob_cs.md)* **message** - Buffer, containing the user message.
- *Syncker.DELIVERY_METHOD* **delivery_method** - [Delivery mode](../../../../code/plugins/syncker/index.md#delivery_modes) to be used by the Syncker, one of the [DELIVERY_METHOD](#DELIVERY_METHOD) values.

### Return value

true if the message was sent successfully; otherwise, false.
## void SetMessageReceivedCallback ( string channel )

Sets a callback function to be fired when a UDP user message is sent. A callback is executed in the Main Thread, but it is undefined when exactly � either in *update()*, or *postUpdate()*, or *swap()*. To unsubscribe from this callback, set the callback pointer to nullptr.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels. If the specified channel does not exist, it shall be created.

## void RemoveMessageReceivedCallback ( string channel )

Removes a callback function to be fired when a UDP user message is received.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels. If the specified channel does not exist, it shall be created.
