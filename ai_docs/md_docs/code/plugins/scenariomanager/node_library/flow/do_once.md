# Do Once


![](../img/do_once.png)

### Description

Passes the execution flow through the first time it is triggered and blocks every trigger after that. Triggering **Reset** makes the node pass through once more.


Useful for one-off actions in a chain that runs repeatedly - showing a hint the first time a step is reached, for example.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/exec.png) | **Reset** | Allows the node to pass through once again. |
| ![](../img/types/exec.png) | **Event** | Fires the first time the node is triggered after a reset. |


## See Also


- [Do N](../../../../../code/plugins/scenariomanager/node_library/flow/do_n.md)
- [Gate](../../../../../code/plugins/scenariomanager/node_library/flow/gate.md)
- [Throttle](../../../../../code/plugins/scenariomanager/node_library/flow/throttle.md)
