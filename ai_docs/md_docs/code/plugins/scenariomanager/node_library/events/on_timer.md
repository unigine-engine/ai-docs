# On Timer


![](../img/on_timer.png)

### Description

Fires at regular intervals while the script is running, which makes it the way to run something periodically without checking the time on every frame.


**Elapsed** reports how long has actually passed since the previous firing. Because the interval is checked once per frame, this is usually slightly more than **Interval**; use it instead of the nominal interval when the exact time matters.


The **Fire Immediately** parameter controls the first firing: when it is enabled the node fires as soon as the script starts, with **Elapsed** set to 0, and then keeps to the interval. When it is disabled the first firing happens one interval after the start.


An interval of zero or less stops the node from firing at all.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Interval** | The time between firings, in seconds. |
| ![](../img/types/exec.png) | **Event** | Fires each time the interval has elapsed. |
| ![](../img/types/float.png) | **Elapsed** | The time since the previous firing, in seconds. |


## See Also


- [On Update](../../../../../code/plugins/scenariomanager/node_library/events/on_update.md)
- [Delay](../../../../../code/plugins/scenariomanager/node_library/flow/delay.md)
- [Throttle](../../../../../code/plugins/scenariomanager/node_library/flow/throttle.md)
