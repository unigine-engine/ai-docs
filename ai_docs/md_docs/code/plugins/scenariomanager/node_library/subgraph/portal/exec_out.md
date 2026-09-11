# Exec Portal Out


![](../../img/exec_portal_out.png)

### Description

Continues the execution flow that an [Exec Portal In](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_in.md) of the same **name** sent, resuming the sequence at this point in the graph.


Several portals out may share one name, in which case all of them run when that name is triggered.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/exec.png) | **Event** | Triggered when a portal in of the same name is reached. |


## See Also


- [Exec Portal In](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_in.md)
- [Data Portal Out](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_out.md)
- [Exec Trigger](../../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md)
