# On Event


![](../img/on_event.png)

### Description

Starts an execution chain when a custom event with the name given in the **Event Name** parameter is raised by [Send Event](../../../../../code/plugins/scenariomanager/node_library/events/send_event.md).


Several nodes may listen for the same name, in which case all of them fire. Whether an event sent from another script arrives here depends on how it was sent - only events sent as global cross script boundaries.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Event** | Fires when an event with the given name is raised. |


## See Also


- [Send Event](../../../../../code/plugins/scenariomanager/node_library/events/send_event.md)
- [On Init](../../../../../code/plugins/scenariomanager/node_library/events/on_init.md)
- [Get Global](../../../../../code/plugins/scenariomanager/node_library/variables/get_global.md)
