# Unigine::Plugins::Syncker::Syncker Class (CPP)

**Header:** #include <plugins/Unigine/Syncker/UnigineSyncker.h>


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

### Members

## void setExtrapolationPeriod ( double period )

***Console*:**`syncker_extrapolation_period`Sets a new [extrapolation](../../../../code/plugins/syncker/index.md#interpolation) period value for the computer.
### Arguments

- *double* **period** - The extrapolation period value, in seconds. The default value is 0.0.

## double getExtrapolationPeriod () const

***Console*:**`syncker_extrapolation_period`Returns the current [extrapolation](../../../../code/plugins/syncker/index.md#interpolation) period value for the computer.
### Return value

Current extrapolation period value, in seconds. The default value is 0.0.
## void setInterpolationPeriod ( double period )

***Console*:**`syncker_interpolation_period`Sets a new [interpolation](../../../../code/plugins/syncker/index.md#interpolation) period value for the computer.
It is recommended to use this method when setting the [frequency of sending packets](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md#getSendRate_float) to Slaves.


```cpp
//On the Master
master->setSendRate(15.0f); // send packets 15 times per second

//Both on the Master and all Slaves
syncker->setInterpolationPeriod(0.1f); // 100 ms delay

```


### Arguments

- *double* **period** - The interpolation period value, in seconds. The default value is 0.04. > **Notice:** The value should not be less than ***1�/�[getSendRate()](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md#getSendRate_float)***, otherwise the image shall be "stuttering".

## double getInterpolationPeriod () const

***Console*:**`syncker_interpolation_period`Returns the current [interpolation](../../../../code/plugins/syncker/index.md#interpolation) period value for the computer.
It is recommended to use this method when setting the [frequency of sending packets](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md#getSendRate_float) to Slaves.


```cpp
//On the Master
master->setSendRate(15.0f); // send packets 15 times per second

//Both on the Master and all Slaves
syncker->setInterpolationPeriod(0.1f); // 100 ms delay

```


### Return value

Current interpolation period value, in seconds. The default value is 0.04.
> **Notice:** The value should not be less than ***1�/�[getSendRate()](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md#getSendRate_float)***, otherwise the image shall be "stuttering".

## void setInterpolation ( bool interpolation )

***Console*:**`syncker_interpolation`Sets a new value indicating if [interpolation and extrapolation](../../../../code/plugins/syncker/index.md#interpolation) are enabled for the computer to tackle the problem of lost packets between the master and slaves.
### Arguments

- *bool* **interpolation** - Set **true** to enable [interpolation and extrapolation](../../../../code/plugins/syncker/index.md#interpolation); **false** - to disable it.

## bool isInterpolation () const

***Console*:**`syncker_interpolation`Returns the current value indicating if [interpolation and extrapolation](../../../../code/plugins/syncker/index.md#interpolation) are enabled for the computer to tackle the problem of lost packets between the master and slaves.
### Return value

**true** if [interpolation and extrapolation](../../../../code/plugins/syncker/index.md#interpolation) is enabled ; otherwise **false**.
## void setDisconnectTimeout ( float timeout )

Sets a new timeout period after which a Slave is considered as disconnected.
### Arguments

- *float* **timeout** - The duration of the timeout period, in seconds.

## float getDisconnectTimeout () const

Returns the current timeout period after which a Slave is considered as disconnected.
### Return value

Current duration of the timeout period, in seconds.
## Syncker::ADDRESSING_METHOD getAddressingMethod () const

Returns the current packets [addressing method](../../../../code/plugins/syncker/index.md#addressing_modes) currently used by the Syncker for communication.
### Return value

Current packets addressing mode currently used by the Syncker.
## double getIFps () const

Returns the current duration of the last frame, in seconds. This value is more accurate than that of the *[Game](../../../../api/library/engine/class.game_cpp.md#IFps)* class and is represented by a double-precision value.
### Return value

Current duration of the last frame, in seconds.
## double getTime () const

Returns the current Master frame time, in seconds, (even if called from a Slave computer). It is the time of the last buffer swap operation (i.e., beginning of the next frame). This value is more accurate than that of the *[Game](../../../../api/library/engine/class.game_cpp.md#Time)* class and is represented by a double-precision value.
### Return value

Current Master frame time, in seconds.
## void setComputerName ( const char * name )

Sets a new name of the computer to be used when assigning a viewport to be displayed (see *[SpiderVision](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md)* plugin). This name can be set at the application startup via the [`computer_name`](../../../../code/plugins/syncker/options.md#computer_name) command-line argument. If not specified the name is obtained from the *[SpiderVision](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md)* plugin, or if the latter is unavailable the name will be taken from the Operating System settings.
### Arguments

- *const char ** **name** - The name of the computer to be set.

## String getComputerName () const

Returns the current name of the computer to be used when assigning a viewport to be displayed (see *[SpiderVision](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md)* plugin). This name can be set at the application startup via the [`computer_name`](../../../../code/plugins/syncker/options.md#computer_name) command-line argument. If not specified the name is obtained from the *[SpiderVision](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md)* plugin, or if the latter is unavailable the name will be taken from the Operating System settings.
### Return value

Current name of the computer to be set.
## Syncker::SWAP_SYNC_MODE getSwapSyncMode () const

Returns the current buffer swap synchronization mode currently used by the Syncker.
### Return value

Current buffer swap synchronization mode used by the Syncker.
One of the following:


- **DEFAULT** - default syncronization mode.
- **NVIDIA** - NVIDIA buffer swap synchronization. Detailed information on current sync status is displayed in the console (available only for NVIDIA Quadro GPUs with G-SYNC support).


---

## bool isInterpolation ( const Ptr < Node > & node ) const

Returns a value indicating if the given node is [interpolated](../../../../code/plugins/syncker/index.md#interpolation) by the Syncker.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to be checked.

### Return value

true if the given node is [interpolated](../../../../code/plugins/syncker/index.md#interpolation) by the Syncker; otherwise, false.
## void setDebug ( bool enabled , int x , int y , int align_mask )

***Console*:**`syncker_debug`Enables or disables displaying of debug information at the specified position on the screen.
### Arguments

- *bool* **enabled** - true to display the debug information; false - to hide it.
- *int* **x** - Horizontal margin of the debug information block. The default value is 10.
- *int* **y** - Vertical margin of the debug information block. The default value is 10.
- *int* **align_mask** - Alignment mask. One of the [Gui::ALIGN_*](../../../../api/library/gui/class.gui_cpp.md#ALIGN_BOTTOM) variables or their combination. The default value is Gui::ALIGN_RIGHT | Gui::ALIGN_BOTTOM.

## bool isDebug ( )

***Console*:**`syncker_debug`Returns a value indicating if the debug information is to be displayed.
### Return value

true if the debug information is to be displayed; otherwise, false.
## bool sendMessage ( const char * channel , const Ptr < Blob > & message , Syncker::DELIVERY_METHOD delivery_method = DELIVERY_METHOD.RELIABLE )

Sends a user message contained in the specified buffer using the given delivery method to the specified named channel via the UDP protocol.
### Arguments

- *const char ** **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **message** - Buffer, containing the user message.
- *Syncker::DELIVERY_METHOD* **delivery_method** - [Delivery mode](../../../../code/plugins/syncker/index.md#delivery_modes) to be used by the Syncker, one of the [DELIVERY_METHOD](#DELIVERY_METHOD) values.

### Return value

true if the message was sent successfully; otherwise, false.
## void setMessageReceivedCallback ( const char * channel , Unigine:: CallbackBase * func )

Sets a callback function to be fired when a UDP user message is sent. A callback is executed in the Main Thread, but it is undefined when exactly � either in *update()*, or *postUpdate()*, or *swap()*. To unsubscribe from this callback, set the callback pointer to nullptr.
### Arguments

- *const char ** **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels. If the specified channel does not exist, it shall be created.
- *Unigine::[CallbackBase](../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **func** - Callback pointer. To clear the callback, set this argument to nullptr.

## void removeMessageReceivedCallback ( const char * channel )

Removes a callback function to be fired when a UDP user message is received.
### Arguments

- *const char ** **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels. If the specified channel does not exist, it shall be created.
