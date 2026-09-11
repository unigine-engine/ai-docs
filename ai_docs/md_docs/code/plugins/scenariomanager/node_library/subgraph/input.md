# Subgraph Input


![](../img/subgraph_input.png)

### Description

Declares one data pin that the graph receives from whoever uses it, and outputs the value supplied for it. Each of these nodes becomes one input pin on the [Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md) node in the parent graph.


The type of the pin and the value it falls back to when the parent leaves it unconnected are set on the node itself.


Where several inputs are declared, the order they are arranged in is the order the pins appear in on the parent side.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/any.png) | **Value** | The value supplied by the parent graph. |


## See Also


- [Subgraph Output](../../../../../code/plugins/scenariomanager/node_library/subgraph/output.md)
- [Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md)
- [Exec Trigger](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md)
