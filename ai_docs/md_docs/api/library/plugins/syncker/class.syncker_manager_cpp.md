# Unigine::Plugins::Syncker::Manager Class (CPP)

**Header:** #include <plugins/Unigine/Syncker/UnigineSyncker.h>

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

### Members

## void setDebugWindow ( bool window )

Sets a new value indicating if the syncker's debug window is enabled.
### Arguments

- *bool* **window** - Set **true** to enable the Syncker's debug window; **false** - to disable it.

## bool isDebugWindow () const

Returns the current value indicating if the syncker's debug window is enabled.
### Return value

**true** if the Syncker's debug window is enabled ; otherwise **false**.
## Syncker * getSyncker () const

Returns the current [Syncker interface](../../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md).
### Return value

Current pointer to the [Syncker interface](../../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md). It is the base class for Master and Slave.
## bool isSynckerInitialized () const

Returns the current value indicating if the Syncker (Master or Slave) was initialized.
### Return value

**true** if the Syncker (master or slave) was initialized; otherwise **false**.
## Slave * getSlave () const

Returns the current [Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cpp.md).
### Return value

Current pointer to the Slave interface.
## bool isSlaveInitialized () const

Returns the current value indicating if the Slave was initialized.
### Return value

**true** if the Slave was initialized; otherwise **false**.
## Master * getMaster () const

Returns the current [Master interface](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md).
### Return value

Current pointer to the [Master interface](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md).
## bool isMasterInitialized () const

Returns the current value indicating if the Master was initialized.
### Return value

**true** if the Master was initialized; otherwise **false**.
## bool getArgAllowExtraSlaves () const

Returns the current value indicating if additional Slaves can be connected after starting the session set by the command line argument "[-sync_allow_extra_slaves](../../../../code/plugins/syncker/options.md#sync_allow_extra_slaves)".
> **Notice:** Available for Slave only.

### Return value

**true** if additional Slaves can be connected after starting the session; otherwise **false**.
## int getArgUdpSlavePort () const

Returns the current UDP port used by the Slave set by the command line argument "[-sync_slave_port](../../../../code/plugins/syncker/options.md#sync_slave_port)".
> **Notice:** Available for Slave only.

### Return value

Current UDP port used by the Slave. The default value is 0 (any unused port available).
## int getArgUdpPort () const

Returns the current UDP port value set by the command line argument "[-sync_port](../../../../code/plugins/syncker/options.md#sync_port)".
### Return value

Current UDP port number. The default value is 8890.
## const char * getArgMasterAddress () const

Returns the current IP address of the Master set by the command line argument "[-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address)".
> **Notice:** Available for Slave only.

### Return value

Current IP address of the Master.
## const char * getArgMulticastAddress () const

Returns the current multicast address of the Master set by the command line argument "[-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address)".
### Return value

Current multicast address of the Master. The default value is 239.0.0.1
## const char * getArgBroadcastAddress () const

Returns the current broadcast address of the Master set by the command line argument "[-sync_broadcast_address](../../../../code/plugins/syncker/options.md#sync_broadcast_address)".
### Return value

Current broadcast address of the Master.
## int getArgPeersCount () const

Returns the current number of peers set by the command line argument "[-sync_count](../../../../code/plugins/syncker/options.md#sync_count)".
### Return value

Current number of peers. The default value is 1. The number of peers includes all Slaves in the network + the Master.
## Syncker::SWAP_SYNC_MODE getArgSwapSyncMode () const

Returns the current swap synchronization mode set by the command line argument `-sync_swap`.
### Return value

Current swap synchronization mode.
## Syncker::ADDRESSING_METHOD getArgAddressingMethod () const

Returns the current addressing mode value set by the command line argument "[-sync_method](../../../../code/plugins/syncker/options.md#sync_method)".
### Return value

Current addressing mode: one of the [ADDRESSING_METHOD](../../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md#ADDRESSING_METHOD) enum values.
## bool getArgIsMaster () const

Returns the current value indicating if the command line argument "[-sync_master](../../../../code/plugins/syncker/options.md#sync_master)" equals to 1.
### Return value

**true** if the command line argument "-sync_master" equals to 1; otherwise **false**.
## bool getArgInitSyncker () const

Returns the current value indicating if the command line argument "[-sync_init](../../../../code/plugins/syncker/options.md#sync_master)" equals to 1.
### Return value

**true** if the command line argument "-sync_init" equals to 1; otherwise **false**.
## void setEasyblendSyncType ( Manager::SPIDER_VISION_EASYBLEND_SYNC_TYPE type )

Sets a new [EasyBlend](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#easyblend) synchronization strategy used by this instance when sending updates to other devices.
### Arguments

- *Manager::SPIDER_VISION_EASYBLEND_SYNC_TYPE* **type** - The

## Manager::SPIDER_VISION_EASYBLEND_SYNC_TYPE getEasyblendSyncType () const

Returns the current [EasyBlend](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#easyblend) synchronization strategy used by this instance when sending updates to other devices.
### Return value

Current
---

## Master * initMaster ( )

Initializes the Syncker as the Master application using values specified via the [command-line arguments](../../../../code/plugins/syncker/options.md).
### Return value

Pointer to the [Master interface](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md).
## Master * initMasterBroadcast ( int peers_count , const char * broadcast_address , unsigned short udp_port , Syncker::SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Master application with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled.

> **Notice:** Slaves must be [initialized with broadcast mode enabled](#initSlaveBroadcast_ushort_int_Slave) as well.

### Arguments

- *int* **peers_count** - Total number of Syncker hosts in the network (including the Master itself). Similar to specifying the [-sync_count](../../../../code/plugins/syncker/options.md#sync_count) command-line argument.
- *const char ** **broadcast_address** - Broadcast address to be used. Similar to specifying the [-sync_broadcast_address](../../../../code/plugins/syncker/options.md#sync_broadcast_address) command-line argument.
- *unsigned short* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker::SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

Pointer to the [Master interface](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md).
## Master * initMasterMulticast ( int peers_count , const char * multicast_address , unsigned short udp_port , Syncker::SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Master application with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled.
### Arguments

- *int* **peers_count** - Total number of Syncker hosts in the network (including the Master itself). Similar to specifying the [-sync_count](../../../../code/plugins/syncker/options.md#sync_count) command-line argument.
- *const char ** **multicast_address** - Multicast address to be used. Similar to specifying the [-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address) command-line argument.
- *unsigned short* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker::SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

Pointer to the [Master interface](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md).
## Master * initMasterUnicast ( int peers_count , unsigned short udp_port , Syncker::SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Master application with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled.

> **Notice:** Slaves must be [initialized with unicast mode enabled](#initSlaveUnicast_ushort_ushort_int_Slave) as well.

### Arguments

- *int* **peers_count** - Total number of Syncker hosts in the network (including the Master itself). Similar to specifying the [-sync_count](../../../../code/plugins/syncker/options.md#sync_count) command-line argument.
- *unsigned short* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker::SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

Pointer to the [Master interface](../../../../api/library/plugins/syncker/class.syncker_master_cpp.md).
## Slave * initSlave ( )

Initializes the Syncker as the Slave application using values specified via the [command-line arguments](../../../../code/plugins/syncker/options.md).
### Return value

Pointer to the [Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cpp.md).
## void destroySyncker ( )

Performs shutdown and destroys the Syncker.
> **Notice:** Called automatically, when the plugin is unloaded.


## Slave * initSlaveBroadcast ( unsigned short udp_port , Syncker::SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Master's IP address will be detected automatically.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *unsigned short* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker::SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

Pointer to the [slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cpp.md).
## Slave * initSlaveBroadcast ( const char * master_address , unsigned short udp_port , Syncker::SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Master's IP address is specified explicitly.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *const char ** **master_address** - Master IP address to be used. Similar to specifying the [-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address) command-line argument.
- *unsigned short* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker::SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

Pointer to the [slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cpp.md).
## Slave * initSlaveMulticast ( const char * multicast_address , unsigned short udp_port , Syncker::SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Master's IP address will be detected automatically.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *const char ** **multicast_address** - Multicast address to be used. Similar to specifying the [-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address) command-line argument.
- *unsigned short* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker::SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

Pointer to the [slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cpp.md).
## Slave * initSlaveMulticast ( const char * master_address , const char * multicast_address , unsigned short udp_port , Syncker::SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Master's IP address is specified explicitly.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *const char ** **master_address** - Master IP address to be used. Similar to specifying the [-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address) command-line argument.
- *const char ** **multicast_address** - Multicast address to be used. Similar to specifying the [-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address) command-line argument.
- *unsigned short* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *Syncker::SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

Pointer to the [slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cpp.md).
## Slave * initSlaveUnicast ( unsigned short master_udp_port , unsigned short slave_udp_port = 0 , Syncker::SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Master's IP address will be detected automatically.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *unsigned short* **master_udp_port** - UDP port to be used by the Master.
- *unsigned short* **slave_udp_port** - UDP port to be used by the Slave. Similar to specifying the [-sync_slave_port](../../../../code/plugins/syncker/options.md#sync_slave_port) command-line argument.
- *Syncker::SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

Pointer to the [slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cpp.md).
## Slave * initSlaveUnicast ( const char * master_address , unsigned short master_udp_port , unsigned short slave_udp_port = 0 , Syncker::SWAP_SYNC_MODE swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Master's IP address is specified explicitly.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *const char ** **master_address** - Master IP address to be used. Similar to specifying the [-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address) command-line argument.
- *unsigned short* **master_udp_port** - UDP port to be used by the Master.
- *unsigned short* **slave_udp_port** - UDP port to be used by the Slave. Similar to specifying the [-sync_slave_port](../../../../code/plugins/syncker/options.md#sync_slave_port) command-line argument.
- *Syncker::SWAP_SYNC_MODE* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

Pointer to the [slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_cpp.md).
## Syncker * initSyncker ( )

Initializes the Syncker as Master or Slave application depending on the values specified via the [command-line arguments](../../../../code/plugins/syncker/options.md).
### Return value

Pointer to the [syncker interface](../../../../api/library/plugins/syncker/class.syncker_syncker_cpp.md). It is the base class for Master and Slave.
## Manager * get ( )

Returns the [Manager](../../../../api/library/plugins/syncker/class.syncker_manager_cpp.md) interface.
### Return value

Pointer to the [manager interface](../../../../api/library/plugins/syncker/class.syncker_manager_cpp.md).
