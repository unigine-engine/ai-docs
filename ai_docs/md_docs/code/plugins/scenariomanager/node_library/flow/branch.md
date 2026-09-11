# Branch


![](../img/branch.png)

### Description

Sends the execution flow along one of two outputs depending on a condition. This is the if-else of a graph: when execution reaches the node, **True** fires if **Condition** is true, and **False** fires otherwise. Exactly one of the two outputs fires each time.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/bool.png) | **Condition** | The condition to check. |
| ![](../img/types/exec.png) | **True** | Fires when the condition is true. |
| ![](../img/types/exec.png) | **False** | Fires when the condition is false. |


## See Also


- [Select](../../../../../code/plugins/scenariomanager/node_library/flow/select.md)
- [Switch](../../../../../code/plugins/scenariomanager/node_library/flow/switch.md)
- [Conditional Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/cond_sequence.md)
