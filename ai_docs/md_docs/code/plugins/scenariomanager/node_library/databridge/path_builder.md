# Path Builder


![](../img/path_builder.png)

### Description

Joins its inputs into a [DataBridge](../../../../../code/plugins/databridge/index_cpp.md) path, inserting a slash between them. Segments plane, fuel and level give plane/fuel/level.


Empty segments are skipped rather than producing a double slash, so a path can be assembled from parts that are not always set.


The number of inputs is not fixed: add or remove input ports in the node body to build a path from as many segments as needed. Each segment is taken from its parameter in the node body, or from the port when something is connected to it - which is how a graph builds a path that depends on what happens at runtime.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/string.png) | **Seg 0** | The first path segment. |
| ![](../img/types/string.png) | **Seg 1** | The second path segment. |
| ![](../img/types/string.png) | **Path** | The assembled path. |


## See Also


- [Get Parameter](../../../../../code/plugins/scenariomanager/node_library/databridge/get.md)
- [List Children](../../../../../code/plugins/scenariomanager/node_library/databridge/list_children.md)
- [Format](../../../../../code/plugins/scenariomanager/node_library/string/format.md)
