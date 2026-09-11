# Wait While


![](../img/wait_while.png)

### Description

Pauses the execution chain for as long as a condition stays true. The condition is checked every tick while the node waits, and **Done** fires as soon as it becomes false.


If the condition is already false when execution reaches the node, **Done** fires immediately and nothing is paused. This is the inverse of [Wait Until](../../../../../code/plugins/scenariomanager/node_library/flow/wait_until.md).


A **Timeout** greater than zero limits the wait: if the condition is still true by then, **Timed Out** fires instead of **Done**. A timeout of zero or less waits indefinitely.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/bool.png) | **Condition** | The condition to wait on: the node waits while this is true. |
| ![](../img/types/float.png) | **Timeout** | How long to wait before giving up, in seconds. Zero or less waits indefinitely. |
| ![](../img/types/exec.png) | **Done** | Fires when the condition becomes false. |
| ![](../img/types/exec.png) | **Timed Out** | Fires when the timeout elapses before the condition becomes false. |


## See Also


- [Wait Until](../../../../../code/plugins/scenariomanager/node_library/flow/wait_until.md)
- [Delay](../../../../../code/plugins/scenariomanager/node_library/flow/delay.md)
- [While Loop](../../../../../code/plugins/scenariomanager/node_library/flow/while_loop.md)
