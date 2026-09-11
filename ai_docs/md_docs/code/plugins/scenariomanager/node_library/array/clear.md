# Array Clear


![](../img/array_clear.png)

### Description

Removes all elements from the array stored in the variable named by **Var Name**, leaving an empty array.


The node writes to the variable directly rather than taking an array through a port, so the change is immediately visible to [Get Variable](../../../../../code/plugins/scenariomanager/node_library/variables/get.md) with the same name.


The variable is set to an empty array whatever it held before, so the node can also be used to initialize it.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/exec.png) | **Event** | Fires after the array has been emptied. |


## See Also


- [Array Create](../../../../../code/plugins/scenariomanager/node_library/array/create.md)
- [Array Append](../../../../../code/plugins/scenariomanager/node_library/array/append.md)
- [Array Length](../../../../../code/plugins/scenariomanager/node_library/array/length.md)
