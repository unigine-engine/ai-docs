# Exec Trigger


![](../img/exec_trigger.png)

### Description

Declares one execution pin that starts the graph, and passes control on when the parent triggers it. Each of these nodes becomes one input execution pin on the [Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md) node in the parent graph.


Declaring more than one gives the subgraph several entry points, so a single reusable graph can offer separate actions - one to start something and another to cancel it.


> **Notice:** The presence of this node is what decides how the subgraph is used. Without it the subgraph has no execution pins and is evaluated whenever its result is needed; with it the parent decides when it runs.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Event** | Triggered when the parent graph triggers this entry point. |


## See Also


- [Exec Done](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_done.md)
- [Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md)
- [Subgraph Input](../../../../../code/plugins/scenariomanager/node_library/subgraph/input.md)
