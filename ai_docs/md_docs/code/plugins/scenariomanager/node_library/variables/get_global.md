# Get Global


![](../img/get_global.png)

### Description

Reads the global variable named by **Var Name** and outputs its value.


Global variables are shared by every script running in the Scenario Manager, so this node reads values written by [Set Global](../../../../../code/plugins/scenariomanager/node_library/variables/set_global.md) in any script. Reading a global that has never been set gives an empty value.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/any.png) | **Value** | The value currently stored in the global variable. |


## See Also


- [Set Global](../../../../../code/plugins/scenariomanager/node_library/variables/set_global.md)
- [Get Variable](../../../../../code/plugins/scenariomanager/node_library/variables/get.md)
