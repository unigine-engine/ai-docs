# Syncker-Specific Options


There are 2 types of *Syncker*-specific options:


- *Command-line options* used to specify screen configuration, addressing mode, multicast address of the *Master* computer, or a port to be used on the application start-up. These options have the same syntax as the other [start-up command-line options](../../../code/command_line.md).
- *Console options* that can be run from the application console on the *Master* or *Slave* sides.


## Command-Line Options


### Common Options


The following command-line options can be run on *Master* or *Slave* application start-up:


| Name | Description | Arguments | Default |
|---|---|---|---|
| sync_init | Initializes *Syncker*. ```bash -sync_init 1 ``` | Flag. | 1 |
| sync_master | Sets the flag indicating whether the computer is *Master*. ```bash -sync_master 1 ``` | *Master* flag. | 1 |
| sync_method | Sets the addressing mode to be used by *Syncker*. One of the following: *[unicast](../../../code/plugins/syncker/index.md#addressing_unicast), [multicast](../../../code/plugins/syncker/index.md#addressing_multicast), [broadcast](../../../code/plugins/syncker/index.md#addressing_broadcast)*. ```bash -sync_method broadcast ``` | Addressing mode. | unicast |
| sync_multicast_address | Sets a *multicast* address that is used by the *Master* computer to send messages to *Slave* over the network. ```bash -sync_multicast_address "xxx.xxx.xxx.xxx" ``` | A *multicast* address in the *xxx.xxx.xxx.xxx* format. | 239.0.0.1 |
| sync_port | Sets the *UDP* port to be used to send and receive messages for the *Syncker*. ```bash -sync_port 8890 ``` | *UDP* port number. | 8890 |
| sync_swap | Sets the buffer swapping method to be used by *Syncker*. One of the following: default, NVIDIA (available only for NVIDIA Quadro GPUs with G-SYNC support). ```bash -sync_swap nvidia ``` | Buffer swap synchronization mode. | default |
| sync_swap_nvidia_group | Sets NVIDIA's swap group. ```bash -sync_swap_nvidia_group 1 ``` | NVIDIA's swap group. | 1 |
| sync_swap_nvidia_barrier | Sets NVIDIA's swap barrier. ```bash -sync_swap_nvidia_barrier 1 ``` | NVIDIA's swap barrier. | 1 |
| computer_name | Sets the name of the computer to be used in viewport configuration stored in the [configuration file](../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file). ```bash -computer_name <comp_name> ``` | Computer name. | � |


### Master Options


The following command-line options can be run on the *Master* application start-up:


| Name | Description | Arguments | Default |
|---|---|---|---|
| sync_count | Sets a number of *Syncker* hosts (including *Master* itself) in the network. ```bash -sync_count 3 ``` | Number of hosts. | 1 |
| sync_broadcast_address | Sets a broadcast address of the *Master* computer that is used to broadcast messages to *Slave* over the network. If the key is not specified, *Syncker* shall try to determine the value automatically. ```bash -sync_broadcast_address "xxx.xxx.xxx.xxx" ``` | A broadcast address in the *xxx.xxx.xxx.xxx* format. | � |
| sync_allow_extra_slaves | Sets the flag indicating whether additional *Slave* PCs can be connected after starting the session. ```bash -sync_allow_extra_slaves 1 ``` | Extra *Slave* flag. | 0 |


### Slave Options


The following command-line options can be run on the *Slave* application start-up:


| Name | Description | Arguments | Default |
|---|---|---|---|
| sync_slave_port | Sets a UDP port to be used by *Slave*. 0 � means any unused port available. ```bash -sync_slave_port 0 ``` | *UDP* port number. | 0 |
| sync_master_address | Sets the address of the *Master* computer. If the key is not specified, *Syncker* shall try to determine the value automatically. ```bash -sync_master_address "xxx.xxx.xxx.xxx" ``` | *Master*'s address in the *xxx.xxx.xxx.xxx* format. | � |


## Console Commands


The following console commands can be run on a *Master* or *Slave* computer.


| Name | Description | Arguments |
|---|---|---|
| `sync` | - **Command.** Runs the specified console command on *Master* and all *Slave* PCs. ```text sync show_profiler 3 //shows the profiler on all computers ``` | A console command to run. |
| `syncker_interpolation` | - **Variable.** Prints the value indicating if [interpolation and extrapolation](../../../code/plugins/syncker/index.md#interpolation) are enabled on the computer. - **Command.** Enables or disables [interpolation and extrapolation](../../../code/plugins/syncker/index.md#interpolation) on the computer. ```text syncker_interpolation 1 ``` | 0 � disabled 1 � enabled (by default) |
| `syncker_interpolation_period` | - **Variable.** Prints the current [interpolation](../../../code/plugins/syncker/index.md#interpolation) period value for the computer, in seconds. - **Command.** Sets the interpolation period for the computer. ```text syncker_interpolation_period 0.04 ``` | Interpolation period, in seconds (0.04 � by default) |
| `syncker_extrapolation_period` | - **Variable.** Prints the current [extrapolation](../../../code/plugins/syncker/index.md#interpolation) period value for the computer, in seconds. - **Command.** Sets the extrapolation period for the computer. ```text syncker_extrapolation_period 0.2 ``` | Extrapolation period, in seconds (0.0 � by default) |
| `syncker_setup` | - **Variable.** Prints the value indicating if screen/ projection setup mode is active. - **Command.** Enables or disables screen/ projection setup mode. ```text syncker_setup 1 ``` | 0 � return to standard mode. 1 � enter the screen/ projection setup mode. |
| `syncker_debug` | - **Variable.** Prints the value indicating if the [debug window](../../../code/plugins/syncker/index.md#debug_window) is active. - **Command.** Shows or hides the [debug window](../../../code/plugins/syncker/index.md#debug_window). ```text syncker_debug 1 ``` | 0 � hide the debug window. 1 � show the debug window. |
