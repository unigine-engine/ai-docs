# Get Parameter


![](../img/get_parameter.png)

### Description

Reads the value of the [DataBridge](../../../../../code/plugins/databridge/index_cpp.md) parameter at the given path.


When no parameter exists at that path, or it holds no value yet, **Exists** is false and **Value** keeps whatever it held before. Check **Exists** before using the result.


The node has no execution ports and is evaluated whenever its output is needed. To act at the moment a parameter changes rather than poll it, use [On Parameter Changed](../../../../../code/plugins/scenariomanager/node_library/databridge/on_changed.md).


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/string.png) | **Path** | The path of the parameter to read. |
| ![](../img/types/any.png) | **Value** | The value of the parameter. |
| ![](../img/types/bool.png) | **Exists** | true if a parameter with a value was found at the path. |


## See Also


- [Set Parameter](../../../../../code/plugins/scenariomanager/node_library/databridge/set.md)
- [On Parameter Changed](../../../../../code/plugins/scenariomanager/node_library/databridge/on_changed.md)
- [Path Builder](../../../../../code/plugins/scenariomanager/node_library/databridge/path_builder.md)
