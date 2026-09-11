# While Loop


![](../img/while_loop.png)

### Description

Repeats the chain attached to **Body** for as long as **Condition** is true, then continues from **Completed**. The condition is re-evaluated before every repeat, so a node feeding it is read again each time rather than being cached.


Each repeat waits for the whole body chain to finish before the condition is checked again. If the condition is already false when execution reaches the node, the body never runs.


Something inside the body has to eventually make the condition false, otherwise the loop keeps going until the **Max Iterations** limit stops it.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/bool.png) | **Condition** | Checked before every repeat: the body runs while this is true. |
| ![](../img/types/exec.png) | **Body** | Fires once per repeat. |
| ![](../img/types/exec.png) | **Completed** | Fires when the condition becomes false or the iteration limit is reached. |


## Parameters


- **Max Iterations** - A safety limit on the number of repeats, which stops the loop even if the condition is still true. Prevents a graph from hanging on a condition that never becomes false.


## See Also


- [For Loop](../../../../../code/plugins/scenariomanager/node_library/flow/for_loop.md)
- [Do N](../../../../../code/plugins/scenariomanager/node_library/flow/do_n.md)
- [Wait While](../../../../../code/plugins/scenariomanager/node_library/flow/wait_while.md)
