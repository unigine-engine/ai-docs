# Transition Result


![](../img/transition_result.png)

### Description

The output node inside a **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)** graph. Determines whether the transition should fire and when it starts. This node is created automatically and cannot be added or removed manually - every condition graph contains exactly one **Transition Result**.


See **[State Machines](../../../../../content/animations/state_machines/index.md#condition_graphs)** article for details.


> **Notice:** Available only inside condition graphs of a **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)**.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/bool.png) | **Can Transition** | Whether the transition is allowed. |
| ![](../img/types/float.png) | **Enter Time** | Normalized time in the source animation at which the transition starts. |


## Properties


| Use Enter Time | When enabled, the **Enter Time** input becomes active. |
|---|---|


## See Also


- [State Machines](../../../../../content/animations/state_machines/index.md#condition_graphs)
- [Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)
