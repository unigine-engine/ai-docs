# Set Global


![](../img/set_global.png)

### Description

Writes a value to the global variable named by **Var Name**, replacing whatever it held before.


Global variables are shared by every script running in the Scenario Manager, which makes this node the way to pass a value from one script to another. The change is visible to [Get Global](../../../../../code/plugins/scenariomanager/node_library/variables/get_global.md) in any script from the moment it is written.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/any.png) | **Value** | The value to store. |
| ![](../img/types/exec.png) | **Event** | Fires after the value has been stored. |


## See Also


- [Get Global](../../../../../code/plugins/scenariomanager/node_library/variables/get_global.md)
- [Set Variable](../../../../../code/plugins/scenariomanager/node_library/variables/set.md)
- [Send Event](../../../../../code/plugins/scenariomanager/node_library/events/send_event.md)
