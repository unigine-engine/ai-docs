# Delta Time


![](../img/delta_time.png)

### Description

Outputs the duration of the current frame, in seconds.


Multiply a per-second rate by this value to get a change that stays the same regardless of the frame rate: a value moving at 2 units per second advances by **Dt** multiplied by 2 each frame.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Dt** | The duration of the current frame, in seconds. |


## See Also


- [Game Time](../../../../../code/plugins/scenariomanager/node_library/time/time.md)
- [Frame Count](../../../../../code/plugins/scenariomanager/node_library/time/frame.md)
