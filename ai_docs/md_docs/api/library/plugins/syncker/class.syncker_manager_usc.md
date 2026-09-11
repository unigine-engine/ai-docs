# Unigine::Plugins::Syncker::Manager Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


> **Notice:** [Syncker](../../../../code/plugins/syncker/index.md) plugin must be loaded.


This class represents Syncker manager interface used to initialize and destroy Syncker in master and slave applications.


## Manager Class

### Members

## void setDebugWindow ( bool window )

Sets a new value indicating if the syncker's debug window is enabled.
### Arguments

- *bool* **window** - Set **true** to enable the Syncker's debug window; **false** - to disable it.

## bool isDebugWindow () const

Returns the current value indicating if the syncker's debug window is enabled.
### Return value

**true** if the Syncker's debug window is enabled ; otherwise **false**.
## Syncker getSyncker () const

Returns the current [Syncker interface](../../../../api/library/plugins/syncker/class.syncker_syncker_usc.md).
### Return value

Current [Syncker interface](../../../../api/library/plugins/syncker/class.syncker_syncker_usc.md) instance. It is the base class for Master and Slave.
## bool isSynckerInitialized () const

Returns the current value indicating if the Syncker (Master or Slave) was initialized.
### Return value

**true** if the Syncker (master or slave) was initialized; otherwise **false**.
## Slave getSlave () const

Returns the current [Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_usc.md).
### Return value

Current Slave interface instance.
## bool isSlaveInitialized () const

Returns the current value indicating if the Slave was initialized.
### Return value

**true** if the Slave was initialized; otherwise **false**.
## Master getMaster () const

Returns the current [Master interface](../../../../api/library/plugins/syncker/class.syncker_master_usc.md).
### Return value

Current [Master interface](../../../../api/library/plugins/syncker/class.syncker_master_usc.md) instance.
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
## int getArgSwapSyncMode () const

Returns the current swap synchronization mode set by the command line argument `-sync_swap`.
### Return value

Current swap synchronization mode.
## int getArgAddressingMethod () const

Returns the current addressing mode value set by the command line argument "[-sync_method](../../../../code/plugins/syncker/options.md#sync_method)".
### Return value

Current addressing mode: one of the [ADDRESSING_METHOD](../../../../api/library/plugins/syncker/class.syncker_syncker_usc.md#ADDRESSING_METHOD) enum values.
## bool getArgIsMaster () const

Returns the current value indicating if the command line argument "[-sync_master](../../../../code/plugins/syncker/options.md#sync_master)" equals to 1.
### Return value

**true** if the command line argument "-sync_master" equals to 1; otherwise **false**.
## bool getArgInitSyncker () const

Returns the current value indicating if the command line argument "[-sync_init](../../../../code/plugins/syncker/options.md#sync_master)" equals to 1.
### Return value

**true** if the command line argument "-sync_init" equals to 1; otherwise **false**.
## void setEasyblendSyncType ( )

Sets a new [EasyBlend](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#easyblend) synchronization strategy used by this instance when sending updates to other devices.
### Arguments

- **type** - The

## getEasyblendSyncType () const

Returns the current [EasyBlend](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#easyblend) synchronization strategy used by this instance when sending updates to other devices.
### Return value

Current
---

## Master engine.syncker. initMaster ( )

Initializes the Syncker as the Master application using values specified via the [command-line arguments](../../../../code/plugins/syncker/options.md).
### Return value

[Master interface](../../../../api/library/plugins/syncker/class.syncker_master_usc.md) instance.
## Master engine.syncker. initMasterBroadcast ( int peers_count , string broadcast_address , int udp_port , int swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Master application with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled.

> **Notice:** Slaves must be [initialized with broadcast mode enabled](#initSlaveBroadcast_ushort_int_Slave) as well.

### Arguments

- *int* **peers_count** - Total number of Syncker hosts in the network (including the Master itself). Similar to specifying the [-sync_count](../../../../code/plugins/syncker/options.md#sync_count) command-line argument.
- *string* **broadcast_address** - Broadcast address to be used. Similar to specifying the [-sync_broadcast_address](../../../../code/plugins/syncker/options.md#sync_broadcast_address) command-line argument.
- *int* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *int* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Master interface](../../../../api/library/plugins/syncker/class.syncker_master_usc.md) instance.
## Master engine.syncker. initMasterMulticast ( int peers_count , string multicast_address , int udp_port , int swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Master application with the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled.
### Arguments

- *int* **peers_count** - Total number of Syncker hosts in the network (including the Master itself). Similar to specifying the [-sync_count](../../../../code/plugins/syncker/options.md#sync_count) command-line argument.
- *string* **multicast_address** - Multicast address to be used. Similar to specifying the [-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address) command-line argument.
- *int* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *int* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Master interface](../../../../api/library/plugins/syncker/class.syncker_master_usc.md) instance.
## Master engine.syncker. initMasterUnicast ( int peers_count , int udp_port , int swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Master application with the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled.

> **Notice:** Slaves must be [initialized with unicast mode enabled](#initSlaveUnicast_ushort_ushort_int_Slave) as well.

### Arguments

- *int* **peers_count** - Total number of Syncker hosts in the network (including the Master itself). Similar to specifying the [-sync_count](../../../../code/plugins/syncker/options.md#sync_count) command-line argument.
- *int* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *int* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Master interface](../../../../api/library/plugins/syncker/class.syncker_master_usc.md) instance.
## Slave engine.syncker. initSlave ( )

Initializes the Syncker as the Slave application using values specified via the [command-line arguments](../../../../code/plugins/syncker/options.md).
### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_usc.md) instance.
## void engine.syncker. destroySyncker ( )

Performs shutdown and destroys the Syncker.
> **Notice:** Called automatically, when the plugin is unloaded.


## Slave engine.syncker. initSlaveBroadcast ( int udp_port , int swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Master's IP address will be detected automatically.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *int* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *int* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_usc.md) instance.
## Slave engine.syncker. initSlaveBroadcast ( string master_address , int udp_port , int swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [broadcast mode](../../../../code/plugins/syncker/index.md#addressing_broadcast) enabled. Master's IP address is specified explicitly.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *string* **master_address** - Master IP address to be used. Similar to specifying the [-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address) command-line argument.
- *int* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *int* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_usc.md) instance.
## Slave engine.syncker. initSlaveMulticast ( string multicast_address , int udp_port , int swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Master's IP address will be detected automatically.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *string* **multicast_address** - Multicast address to be used. Similar to specifying the [-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address) command-line argument.
- *int* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *int* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_usc.md) instance.
## Slave engine.syncker. initSlaveMulticast ( string master_address , string multicast_address , int udp_port , int swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [multicast mode](../../../../code/plugins/syncker/index.md#addressing_multicast) enabled. Master's IP address is specified explicitly.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *string* **master_address** - Master IP address to be used. Similar to specifying the [-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address) command-line argument.
- *string* **multicast_address** - Multicast address to be used. Similar to specifying the [-sync_multicast_address](../../../../code/plugins/syncker/options.md#sync_multicast_address) command-line argument.
- *int* **udp_port** - UDP port to be used. Similar to specifying the [-sync_port](../../../../code/plugins/syncker/options.md#sync_port) command-line argument.
- *int* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_usc.md) instance.
## Slave engine.syncker. initSlaveUnicast ( int master_udp_port , int slave_udp_port = 0 , int swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Master's IP address will be detected automatically.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *int* **master_udp_port** - UDP port to be used by the Master.
- *int* **slave_udp_port** - UDP port to be used by the Slave. Similar to specifying the [-sync_slave_port](../../../../code/plugins/syncker/options.md#sync_slave_port) command-line argument.
- *int* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_usc.md) instance.
## Slave engine.syncker. initSlaveUnicast ( string master_address , int master_udp_port , int slave_udp_port = 0 , int swap_mode = Syncker.SWAP_SYNC_MODE.DEFAULT )

Initializes the Syncker as the Slave application with the specified parameters and the [unicast mode](../../../../code/plugins/syncker/index.md#addressing_unicast) enabled. Master's IP address is specified explicitly.

> **Notice:** Master must be initialized with broadcast mode enabled as well.

### Arguments

- *string* **master_address** - Master IP address to be used. Similar to specifying the [-sync_master_address](../../../../code/plugins/syncker/options.md#sync_master_address) command-line argument.
- *int* **master_udp_port** - UDP port to be used by the Master.
- *int* **slave_udp_port** - UDP port to be used by the Slave. Similar to specifying the [-sync_slave_port](../../../../code/plugins/syncker/options.md#sync_slave_port) command-line argument.
- *int* **swap_mode** - Swap synchronization mode to be used by the Syncker. Similar to specifying the [-sync_swap](../../../../code/plugins/syncker/options.md#sync_swap) command-line argument.

### Return value

[Slave interface](../../../../api/library/plugins/syncker/class.syncker_slave_usc.md) instance.
## Syncker engine.syncker. initSyncker ( )

Initializes the Syncker as Master or Slave application depending on the values specified via the [command-line arguments](../../../../code/plugins/syncker/options.md).
### Return value

[Syncker interface](../../../../api/library/plugins/syncker/class.syncker_slave_usc.md) instance. It is the base class for Master and Slave.
