# Send Event


![](../img/send_event.png)

### Description

Raises a custom event by name. Every [On Event](../../../../../code/plugins/scenariomanager/node_library/events/on_event.md) node listening for that name starts its chain.


The **Global** parameter sets how far the event reaches. When it is disabled the event stays inside the script that sent it; when it is enabled the event reaches every script running in the Scenario Manager, which is how one script triggers another.


An event carries no value. To pass data along with it, write the value to a global variable with [Set Global](../../../../../code/plugins/scenariomanager/node_library/variables/set_global.md) before sending, and read it in the receiving chain.


The execution flow continues through **Event** after the event has been raised.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/string.png) | **Event Name** | The name of the event to raise. |
| ![](../img/types/exec.png) | **Event** | Fires after the event has been raised. |


## See Also


- [On Event](../../../../../code/plugins/scenariomanager/node_library/events/on_event.md)
- [Set Global](../../../../../code/plugins/scenariomanager/node_library/variables/set_global.md)
- [Run Script](../../../../../code/plugins/scenariomanager/node_library/flow/run_script.md)
