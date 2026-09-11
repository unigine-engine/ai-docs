# On Update


![](../img/on_update.png)

### Description

Fires every frame while the script is running. Use it for logic that has to be checked continuously, such as watching a distance or moving something a little at a time.


Since the chain runs on every frame, keep it short, and scale per-frame changes by [Delta Time](../../../../../code/plugins/scenariomanager/node_library/time/dt.md) so they do not depend on the frame rate. For work that only has to happen at intervals, [On Timer](../../../../../code/plugins/scenariomanager/node_library/events/on_timer.md) is cheaper.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Event** | Fires once per frame. |


## See Also


- [On Init](../../../../../code/plugins/scenariomanager/node_library/events/on_init.md)
- [On Timer](../../../../../code/plugins/scenariomanager/node_library/events/on_timer.md)
- [Delta Time](../../../../../code/plugins/scenariomanager/node_library/time/dt.md)
