# Throttle


![](../img/throttle.png)

### Description

Limits how often the execution flow passes through. A trigger fires **Event** only if at least **Min Interval** seconds have passed since the previous one; triggers that arrive sooner are dropped.


Dropped triggers are not queued - they are discarded, and nothing fires for them later. Unlike [Delay](../../../../../code/plugins/scenariomanager/node_library/flow/delay.md), which postpones every trigger, a throttle passes some through immediately and ignores the rest.


The first trigger always passes through.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/float.png) | **Min Interval** | The minimum time between two triggers that pass through, in seconds. |
| ![](../img/types/exec.png) | **Event** | Fires when a trigger passes through. |


## See Also


- [Delay](../../../../../code/plugins/scenariomanager/node_library/flow/delay.md)
- [Do Once](../../../../../code/plugins/scenariomanager/node_library/flow/do_once.md)
- [Gate](../../../../../code/plugins/scenariomanager/node_library/flow/gate.md)
