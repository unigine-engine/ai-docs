# Array Append


![](../img/array_append.png)

### Description

Adds a value to the end of the array stored in the variable named by **Var Name**.


The node writes to the variable directly rather than taking an array through a port, so the change is immediately visible to [Get Variable](../../../../../code/plugins/scenariomanager/node_library/variables/get.md) with the same name.


If the variable does not hold an array yet, it is replaced with a new empty array before the value is added - appending to an unset variable is safe and needs no separate initialization.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/any.png) | **Value** | The value to add. |
| ![](../img/types/exec.png) | **Event** | Fires after the value has been added. |


## See Also


- [Array Create](../../../../../code/plugins/scenariomanager/node_library/array/create.md)
- [Set Element](../../../../../code/plugins/scenariomanager/node_library/array/set.md)
- [Array Clear](../../../../../code/plugins/scenariomanager/node_library/array/clear.md)
