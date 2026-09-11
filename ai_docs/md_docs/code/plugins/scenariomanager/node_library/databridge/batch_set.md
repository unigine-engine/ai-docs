# Batch Set


![](../img/batch_set.png)

### Description

Writes several [DataBridge](../../../../../code/plugins/databridge/index_cpp.md) parameters in one step, which keeps a graph readable when a single action has to update a group of related values.


Inputs come in pairs: each **Path** is followed by the **Value** written to it. The number of pairs is not fixed - add or remove input ports in the node body to write as many parameters as needed. Pairs with an empty path are skipped.


The parameters are written in order, from the topmost pair down.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/string.png) | **Path 0** | The path of the first parameter to write. |
| ![](../img/types/float.png) | **Value 0** | The value written to the first parameter. |
| ![](../img/types/string.png) | **Path 1** | The path of the second parameter to write. |
| ![](../img/types/float.png) | **Value 1** | The value written to the second parameter. |
| ![](../img/types/exec.png) | **Event** | Fires after all the parameters have been written. |


## See Also


- [Set Parameter](../../../../../code/plugins/scenariomanager/node_library/databridge/set.md)
- [Path Builder](../../../../../code/plugins/scenariomanager/node_library/databridge/path_builder.md)
- [Get Parameter](../../../../../code/plugins/scenariomanager/node_library/databridge/get.md)
