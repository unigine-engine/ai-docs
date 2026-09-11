# Get Variable


![](../img/get_variable.png)

### Description

Reads the local variable named by **Var Name** and outputs its value.


The variable is local to the script, so each script that uses this name keeps its own value. Reading a variable that has never been set gives an empty value.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/any.png) | **Value** | The value currently stored in the variable. |


## See Also


- [Set Variable](../../../../../code/plugins/scenariomanager/node_library/variables/set.md)
- [Get Global](../../../../../code/plugins/scenariomanager/node_library/variables/get_global.md)
