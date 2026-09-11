# Do N


![](../img/do_n.png)

### Description

Passes the execution flow through a limited number of times. The first **N** triggers fire **Body**; every trigger after that fires **Done** instead. Triggering **Reset** sets the counter back to zero.


Unlike [For Loop](../../../../../code/plugins/scenariomanager/node_library/flow/for_loop.md), this node does not repeat anything on its own: it passes through once per trigger and counts how many times it has done so.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/exec.png) | **Reset** | Sets the counter back to zero. |
| ![](../img/types/int.png) | **N** | How many times the node passes through. |
| ![](../img/types/exec.png) | **Body** | Fires while the counter has not reached **N**. |
| ![](../img/types/exec.png) | **Done** | Fires on every trigger after the counter has reached **N**. |


## See Also


- [Do Once](../../../../../code/plugins/scenariomanager/node_library/flow/do_once.md)
- [For Loop](../../../../../code/plugins/scenariomanager/node_library/flow/for_loop.md)
- [Gate](../../../../../code/plugins/scenariomanager/node_library/flow/gate.md)
