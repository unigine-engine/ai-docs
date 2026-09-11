# Gate


![](../img/gate.png)

### Description

Passes the execution flow through only while the gate is open. Triggering **Action** fires **Event** if the gate is open, and does nothing if it is closed.


The gate itself is controlled by three separate execution inputs - **Open**, **Close** and **Toggle**. Triggering them changes the state only: they never fire **Event**, even when the gate is open.


The gate starts open unless **Start Closed** is enabled, and keeps its state until it is changed or the scenario is restarted.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Passes through the gate if it is open. |
| ![](../img/types/exec.png) | **Open** | Opens the gate. |
| ![](../img/types/exec.png) | **Close** | Closes the gate. |
| ![](../img/types/exec.png) | **Toggle** | Opens the gate if it is closed and closes it if it is open. |
| ![](../img/types/bool.png) | **Start Closed** | Whether the gate is closed before it is opened for the first time. |
| ![](../img/types/exec.png) | **Event** | Fires when **Action** is triggered while the gate is open. |


## See Also


- [Latch](../../../../../code/plugins/scenariomanager/node_library/flow/latch.md)
- [Do Once](../../../../../code/plugins/scenariomanager/node_library/flow/do_once.md)
- [Throttle](../../../../../code/plugins/scenariomanager/node_library/flow/throttle.md)
