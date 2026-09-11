# Exec Portal In


![](../../img/exec_portal_in.png)

### Description

Sends the execution flow to every [Exec Portal Out](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_out.md) in the same graph whose **name** matches, without a wire between them.


A long wire across a large graph is hard to follow; a named pair of portals carries the flow to a distant part of the same graph and keeps the layout readable.


Because every matching portal is triggered, one portal in can start several branches at once.


> **Notice:** Portals reach only within the graph that holds them. To cross into another graph, use the pins of a [Subgraph](../../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md). A portal with an empty name does nothing.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/exec.png) | **Action** | Sends the flow to the matching portals. |


## See Also


- [Exec Portal Out](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_out.md)
- [Data Portal In](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_in.md)
- [Subgraph](../../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md)
