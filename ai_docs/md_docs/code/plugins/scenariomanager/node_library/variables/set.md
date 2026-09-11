# Set Variable


![](../img/set_variable.png)

### Description

Writes a value to the local variable named by **Var Name**, replacing whatever it held before.


The variable is local to the script, so each script that uses this name keeps its own value. The variable is created on the first write and takes the type of the value written to it.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/any.png) | **Value** | The value to store. |
| ![](../img/types/exec.png) | **Event** | Fires after the value has been stored. |


## See Also


- [Get Variable](../../../../../code/plugins/scenariomanager/node_library/variables/get.md)
- [Set Global](../../../../../code/plugins/scenariomanager/node_library/variables/set_global.md)
