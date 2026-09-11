# Exec Done


![](../img/exec_done.png)

### Description

Declares one execution pin that the graph finishes on, and hands control back to the parent when triggered. Each of these nodes becomes one output execution pin on the [Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md) node in the parent graph.


Declaring more than one lets the subgraph report which way it ended, so the parent can continue differently after a success than after a failure - the same role [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md) plays within a single graph.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Finishes the subgraph through this pin. |


## See Also


- [Exec Trigger](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md)
- [Subgraph Output](../../../../../code/plugins/scenariomanager/node_library/subgraph/output.md)
- [Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md)
