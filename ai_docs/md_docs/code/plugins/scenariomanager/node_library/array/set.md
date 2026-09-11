# Set Element


![](../img/set_element.png)

### Description

Replaces the element at the given position in the array stored in the variable named by **Var Name**.


The node writes to the variable directly rather than taking an array through a port, so the change is immediately visible to [Get Variable](../../../../../code/plugins/scenariomanager/node_library/variables/get.md) with the same name.


If the index falls outside the array, nothing is written. The execution flow continues in either case.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/int.png) | **Index** | The position of the element to replace, counted from 0. |
| ![](../img/types/any.png) | **Value** | The value to write. |
| ![](../img/types/exec.png) | **Event** | Fires after the node has run. |


## See Also


- [Get Element](../../../../../code/plugins/scenariomanager/node_library/array/get.md)
- [Array Append](../../../../../code/plugins/scenariomanager/node_library/array/append.md)
- [Set Variable](../../../../../code/plugins/scenariomanager/node_library/variables/set.md)
