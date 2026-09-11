# On Parameter Changed


![](../img/on_parameter_changed.png)

### Description

Starts an execution chain whenever the [DataBridge](../../../../../code/plugins/databridge/index_cpp.md) parameter named by the **Path** parameter changes, and reports both the new and the previous value.


The node subscribes to the parameter rather than polling it, so the chain runs only when something actually writes to it - no cost on the frames in between.


It also fires once when the script starts, provided the parameter already holds a value, so that **New Value** is usable from the first tick. On that first firing there is no previous value and **Old Value** is empty.


The path is taken from the parameter in the node body and cannot be changed while the script is running, because the subscription is set up when the script loads.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Event** | Fires when the parameter changes. |
| ![](../img/types/any.png) | **New Value** | The value the parameter holds now. |
| ![](../img/types/any.png) | **Old Value** | The value the parameter held at the previous firing. |


## See Also


- [Get Parameter](../../../../../code/plugins/scenariomanager/node_library/databridge/get.md)
- [Set Parameter](../../../../../code/plugins/scenariomanager/node_library/databridge/set.md)
- [On Event](../../../../../code/plugins/scenariomanager/node_library/events/on_event.md)
