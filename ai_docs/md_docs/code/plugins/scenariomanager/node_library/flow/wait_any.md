# Wait Any


![](../img/wait_any.png)

### Description

Fires **Event** as soon as any one of its execution inputs is triggered, and reports which one through **Index**. The index is the position of the triggered input, counting from zero at the top.


The node does not wait for the others and does not block them: a later trigger on a different input fires **Event** again with the new index. It merges several execution chains into one while keeping track of where the flow came from.


The number of inputs is not fixed: add or remove them in the node body.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action 0** | One of the inputs to react to. |
| ![](../img/types/exec.png) | **Action 1** | One of the inputs to react to. |
| ![](../img/types/exec.png) | **Event** | Fires when any input is triggered. |
| ![](../img/types/int.png) | **Index** | The position of the input that was triggered, counting from zero. |


## See Also


- [Wait All](../../../../../code/plugins/scenariomanager/node_library/flow/wait_all.md)
- [Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/sequence.md)
- [Switch](../../../../../code/plugins/scenariomanager/node_library/flow/switch.md)
