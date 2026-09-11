# List Children


![](../img/list_children.png)

### Description

Reports what the [DataBridge](../../../../../code/plugins/databridge/index_cpp.md) parameter at the given path contains, as an array of the names of its immediate children.


Only the names are returned, not the full paths - combine a name with the parent path using [Path Builder](../../../../../code/plugins/scenariomanager/node_library/databridge/path_builder.md) to address a child. Walking the array with [For Each](../../../../../code/plugins/scenariomanager/node_library/array/for_each.md) is the way to handle every child in turn without knowing in advance how many there are.


If no parameter exists at the path, the outputs keep whatever they held before.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/string.png) | **Path** | The path of the parameter whose children are listed. |
| ![](../img/types/array.png) | **Names** | The names of the immediate children. |
| ![](../img/types/int.png) | **Count** | The number of children. |


## See Also


- [Path Builder](../../../../../code/plugins/scenariomanager/node_library/databridge/path_builder.md)
- [Get Parameter](../../../../../code/plugins/scenariomanager/node_library/databridge/get.md)
- [For Each](../../../../../code/plugins/scenariomanager/node_library/array/for_each.md)
