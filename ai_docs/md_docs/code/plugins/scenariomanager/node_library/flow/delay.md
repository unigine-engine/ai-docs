# Delay


![](../img/delay.png)

### Description

Pauses the execution chain for a given number of seconds, then continues. Everything attached to **Event** runs after the delay has elapsed, while the rest of the graph keeps running in the meantime.


While a delay is pending, triggering the node again is ignored - the pending delay is not restarted and no second delay is started. To restart a delay on every trigger, reset the chain that leads to it instead.


A negative or non-finite number of seconds is treated as zero, which continues the chain on the next tick.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/float.png) | **Seconds** | How long to wait, in seconds. |
| ![](../img/types/exec.png) | **Event** | Fires when the delay has elapsed. |


## See Also


- [Throttle](../../../../../code/plugins/scenariomanager/node_library/flow/throttle.md)
- [Wait Until](../../../../../code/plugins/scenariomanager/node_library/flow/wait_until.md)
- [Wait While](../../../../../code/plugins/scenariomanager/node_library/flow/wait_while.md)
