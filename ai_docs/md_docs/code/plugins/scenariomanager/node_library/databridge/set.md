# Set Parameter


![](../img/set_parameter.png)

### Description

Writes a value to the [DataBridge](../../../../../code/plugins/databridge/index_cpp.md) parameter at the given path. Everything subscribed to that parameter - components, other graphs, or the interface - sees the new value.


An empty path is skipped. The execution flow continues in either case.


To write several parameters at once, use [Batch Set](../../../../../code/plugins/scenariomanager/node_library/databridge/batch_set.md).


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/string.png) | **Path** | The path of the parameter to write. |
| ![](../img/types/any.png) | **Value** | The value to write. |
| ![](../img/types/exec.png) | **Event** | Fires after the value has been written. |


## See Also


- [Get Parameter](../../../../../code/plugins/scenariomanager/node_library/databridge/get.md)
- [Batch Set](../../../../../code/plugins/scenariomanager/node_library/databridge/batch_set.md)
- [Path Builder](../../../../../code/plugins/scenariomanager/node_library/databridge/path_builder.md)
