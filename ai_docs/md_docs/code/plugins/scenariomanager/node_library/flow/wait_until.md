# Wait Until


![](../img/wait_until.png)

### Description

Pauses the execution chain until a condition becomes true. The condition is checked every tick while the node waits, and **Done** fires as soon as it holds.


If the condition is already true when execution reaches the node, **Done** fires immediately and nothing is paused.


A **Timeout** greater than zero limits the wait: if the condition has not become true by then, **Timed Out** fires instead of **Done**. A timeout of zero or less waits indefinitely.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/bool.png) | **Condition** | The condition to wait for. |
| ![](../img/types/float.png) | **Timeout** | How long to wait before giving up, in seconds. Zero or less waits indefinitely. |
| ![](../img/types/exec.png) | **Done** | Fires when the condition becomes true. |
| ![](../img/types/exec.png) | **Timed Out** | Fires when the timeout elapses before the condition holds. |


## See Also


- [Wait While](../../../../../code/plugins/scenariomanager/node_library/flow/wait_while.md)
- [Delay](../../../../../code/plugins/scenariomanager/node_library/flow/delay.md)
- [Wait All](../../../../../code/plugins/scenariomanager/node_library/flow/wait_all.md)
