# Format


![](../img/format.png)

### Description

Builds a string by substituting the connected values into the **Template** parameter.


Placeholders are written as {0}, {1} and so on, numbered from the topmost input. A placeholder may be used more than once, and one that has no matching input is left in the result as written.


The number of inputs is not fixed: add or remove input ports in the node body to substitute as many values as the template needs. Values of any type are converted to text before substitution.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/string.png) | **Arg 0** | The value substituted for {0}. |
| ![](../img/types/string.png) | **Arg 1** | The value substituted for {1}. |
| ![](../img/types/string.png) | **Result** | The resulting string. |


## See Also


- [To String](../../../../../code/plugins/scenariomanager/node_library/string/to_string.md)
- [Format Log](../../../../../code/plugins/scenariomanager/node_library/debug/flog.md)
