# Data Portal In


![](../../img/data_portal_in.png)

### Description

Makes the connected value available to every [Data Portal Out](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_out.md) in the same graph that carries the same **name**, without a wire between them.


This keeps a value that is read in several distant places from being wired across the whole graph.


> **Notice:** The value is fetched when a portal out asks for it, not stored here, so each read gets the value as it is at that moment. To hold a value over time, use a [variable](../../../../../../code/plugins/scenariomanager/node_library/variables/index.md).


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/any.png) | **Value** | The value to make available under this name. |


## See Also


- [Data Portal Out](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_out.md)
- [Exec Portal In](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_in.md)
- [Subgraph Input](../../../../../../code/plugins/scenariomanager/node_library/subgraph/input.md)
