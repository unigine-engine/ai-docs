# Unigine::Plugins::Syncker::Manager Class (CS)

> **Notice:** This class is a singleton.


> **Notice:** [Syncker](../../../../code/plugins/syncker/index.md) plugin must be loaded.


This class represents Syncker manager interface used to initialize and destroy Syncker in master and slave applications.


## Manager Class

### Enums

## SPIDER_VISION_EASYBLEND_SYNC_TYPE

| Name | Description |
|---|---|
| **NETWORK** = 0 | The instance sends the full *[EasyBlend](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#easyblend)* data over the network: distortion mesh, source file name, all relevant EasyBlend parameters, and any additional related metadata. Use this mode when the instance should act as a source of complete EasyBlend configuration data. |
| **LOAD_FROM_LOCAL_STORAGE** = 1 | The instance sends only a reference (typically the file path) to the *[EasyBlend](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#easyblend)* configuration file. Receiving instances are expected to reload the required EasyBlend data from their own local storage. This reduces network traffic, since only the file path is transmitted instead of the full configuration data. |

### Properties

## bool DebugWindow

The value indicating if the syncker's debug window is enabled.
## 🔒︎ Syncker Syncker

The [Syncker interface](../../../../api/library/plugins/syncker/class.syncker_syncker_cs.md).
## 🔒︎ bool IsSynckerInitialized

The value indicating if the Syncker (Master or Slave) was initialized.
## 🔒︎ Slave Slave

The [Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cs.md).
## 🔒︎ bool IsSlaveInitialized

The value indicating if the Slave was initialized.
## 🔒︎ Master Master

The [Master interface](../../../../api/library/plugins/syncker/class.syncker_master_cs.md).
## 🔒︎ bool IsMasterInitialized

The value indicating if the Master was initialized.
## 🔒︎ bool ArgAllowExtraSlaves

The value indicating if additional Slaves can be connected after starting the session set by the command line argument "[-sync_allow_extra_slaves](../../../../code/plugins/syncker/options.md#sync_allow_extra_slaves)".
> **Notice:** Available for Slave only.

## 🔒︎ int ArgUdpSlavePort

The UDP port used by the Slave set by the command line argument "[-sync_slave_port](../../../../code/plugins/syncker/options.md#sync_slave_port)".
> **Notice:** Available for Slave only.

## 🔒︎ int ArgUdpPort

The UDP port value set by the command line argument "[-sync_port](../../../../code/plugins/syncker/options.md#sync_port)".
## 🔒︎ string ArgMasterAddress

The IP address of the Master set by the command line argument "[-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address)".
> **Notice:** Available for Slave only.

## 🔒︎ string ArgMulticastAddress

The multicast address of the Master set by the command line argument "[-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address)".
## 🔒︎ string ArgBroadcastAddress

The broadcast address of the Master set by the command line argument "[-sync_broadcast_address](../../../../code/plugins/syncker/options.md#sync_broadcast_address)".
## 🔒︎ int ArgPeersCount

The number of peers set by the command line argument "[-sync_count](../../../../code/plugins/syncker/options.md#sync_count)".
## 🔒︎ Syncker.SWAP_SYNC_MODE ArgSwapSyncMode

The swap synchronization mode set by the command line argument `-sync_swap`.
## 🔒︎ Syncker.ADDRESSING_METHOD ArgAddressingMethod

The addressing mode value set by the command line argument "[-sync_method](../../../../code/plugins/syncker/options.md#sync_method)".
## 🔒︎ bool ArgIsMaster

The value indicating if the command line argument "[-sync_master](../../../../code/plugins/syncker/options.md#sync_master)" equals to 1.
## 🔒︎ bool ArgInitSyncker

The value indicating if the command line argument "[-sync_init](../../../../code/plugins/syncker/options.md#sync_master)" equals to 1.
## Manager.SPIDER_VISION_EASYBLEND_SYNC_TYPE EasyblendSyncType

The [EasyBlend](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#easyblend) synchronization strategy used by this instance when sending updates to other devices.
### Members

---

## Master InitMaster ( )

Initializes the Syncker as the Master application using values specified via the [command-line arguments](../../../../code/plugins/syncker/options.md).
### Return value

## Master InitMasterBroadcast ( int peers_count , string broadcast_address , ushort udp_port , Syncker.SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Master application with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled.

> **Notice:** Slaves must be [initialized with broadcast mode enabled](#initSlaveBroadcast_ushort_int_Slave) as well.

### Arguments

- *int* **peers_count** - Total number of Syncker hosts in the network (including the Master itself). Similar to specifying the [-sync_count](../../../../code/plugins/syncker/options.md#sync_count) command-line argument.
- *string* **broadcast_address** - Broadcast address to be used. Similar to specifying the [-sync_broadcast_address](../../../../code/plugins/syncker/options.md#sync_broadcast_address) command-line argument.
- *ushort* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker.SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Master interface](../../../../api/library/plugins/syncker/class.syncker_master_cs.md) instance.
## Master InitMasterMulticast ( int peers_count , string multicast_address , ushort udp_port , Syncker.SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Master application with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled.
### Arguments

- *int* **peers_count** - Total number of Syncker hosts in the network (including the Master itself). Similar to specifying the [-sync_count](../../../../code/plugins/syncker/options.md#sync_count) command-line argument.
- *string* **multicast_address** - Multicast address to be used. Similar to specifying the [-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address) command-line argument.
- *ushort* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker.SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

## Master InitMasterUnicast ( int peers_count , ushort udp_port , Syncker.SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Master application with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled.

> **Notice:** Slaves must be [initialized with unicast mode enabled](#initSlaveUnicast_ushort_ushort_int_Slave) as well.

### Arguments

- *int* **peers_count** - Total number of Syncker hosts in the network (including the Master itself). Similar to specifying the [-sync_count](../../../../code/plugins/syncker/options.md#sync_count) command-line argument.
- *ushort* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker.SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

## Slave InitSlave ( )

Initializes the Syncker as the Slave application using values specified via the [command-line arguments](../../../../code/plugins/syncker/options.md).
### Return value

## void DestroySyncker ( )

Performs shutdown and destroys the Syncker.
> **Notice:** Called automatically, when the plugin is unloaded.


## Slave InitSlaveBroadcast ( ushort udp_port , Syncker.SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Master's IP address will be detected automatically.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *ushort* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker.SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cs.md) instance.
## Slave InitSlaveBroadcast ( string master_address , ushort udp_port , Syncker.SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Master's IP address is specified explicitly.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *string* **master_address** - Master IP address to be used. Similar to specifying the [-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address) command-line argument.
- *ushort* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker.SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cs.md) instance.
## Slave InitSlaveMulticast ( string multicast_address , ushort udp_port , Syncker.SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Master's IP address will be detected automatically.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *string* **multicast_address** - Multicast address to be used. Similar to specifying the [-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address) command-line argument.
- *ushort* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker.SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cs.md) instance.
## Slave InitSlaveMulticast ( string master_address , string multicast_address , ushort udp_port , Syncker.SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Master's IP address is specified explicitly.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *string* **master_address** - Master IP address to be used. Similar to specifying the [-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address) command-line argument.
- *string* **multicast_address** - Multicast address to be used. Similar to specifying the [-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address) command-line argument.
- *ushort* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker.SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cs.md) instance.
## Slave InitSlaveUnicast ( ushort master_udp_port , ushort slave_udp_port = 0 , Syncker.SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Master's IP address will be detected automatically.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *ushort* **master_udp_port** - UDP port to be used by the Master.
- *ushort* **slave_udp_port** - UDP port to be used by the Slave. Similar to specifying the [-sync_slave_port](../../../../code/plugins/syncker/options.md#sync_slave_port) command-line argument.
- *Syncker.SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cs.md) instance.
## Slave InitSlaveUnicast ( string master_address , ushort master_udp_port , ushort slave_udp_port = 0 , Syncker.SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Master's IP address is specified explicitly.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *string* **master_address** - Master IP address to be used. Similar to specifying the [-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address) command-line argument.
- *ushort* **master_udp_port** - UDP port to be used by the Master.
- *ushort* **slave_udp_port** - UDP port to be used by the Slave. Similar to specifying the [-sync_slave_port](../../../../code/plugins/syncker/options.md#sync_slave_port) command-line argument.
- *Syncker.SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cs.md) instance.
## Syncker InitSyncker ( )

Initializes the Syncker as Master or Slave application depending on the values specified via the [command-line arguments](../../../../code/plugins/syncker/options.md).
### Return value

[Syncker interface](../../../../api/library/plugins/syncker/class.syncker_slave_cs.md) instance. It is the base class for Master and Slave.
