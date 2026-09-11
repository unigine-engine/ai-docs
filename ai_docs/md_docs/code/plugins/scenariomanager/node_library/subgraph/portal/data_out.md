# Data Portal Out


![](../../img/data_portal_out.png)

### Description

Outputs the value that a [Data Portal In](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_in.md) of the same **name** carries, reading it where it is needed instead of wiring it across the graph.


The value is fetched at the moment it is read, so it is always current.


> **Notice:** Where more than one portal in shares a name, the first one found supplies the value. Give each value its own name to keep the result predictable. A name with no matching portal in produces nothing.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/any.png) | **Value** | The value carried under this name. |


## See Also


- [Data Portal In](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_in.md)
- [Exec Portal Out](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_out.md)
- [Subgraph Output](../../../../../../code/plugins/scenariomanager/node_library/subgraph/output.md)
