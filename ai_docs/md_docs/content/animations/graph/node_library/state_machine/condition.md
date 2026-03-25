# Condition


![](../img/condition.png)

### Description

A pass-through routing node inside a state machine. A **Condition** evaluates its transition rules immediately when reached and routes to the next state without playing any animation. All transition parameters (duration, priority, conditions) are configured on this node.


Each Condition represents a single transition and can only lead to one target state. To branch into multiple states based on different conditions, chain several Condition nodes together - each one evaluating its own rule and routing to its own target.


Unlike a **[State](../../../../../content/animations/graph/node_library/state_machine/state.md)**, a Condition does not produce a pose. It has its own graph that only determines whether the transition should be taken. Double-click a Condition node to open this graph and define the transition logic.


> **Notice:** Available only inside a **[State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)**.


See **[State Machines](../../../../../content/animations/state_machines/index.md)** article for details.


## Properties


| Condition | Name of the condition node. Must be unique among states and conditions within the state machine. |
|---|---|
| Duration | Blend duration of the transition in seconds. |
| Priority | Priority level for transition evaluation. Higher priority transitions are evaluated first. |
| Can Be Interrupted | When enabled, this transition can be interrupted by other transitions before it completes. |


Condition properties are configured via the [Selected Item](../../../../../content/animations/graph/index.md#side_panels) panel.


## See Also


- [State Machines](../../../../../content/animations/state_machines/index.md)
- [State](../../../../../content/animations/graph/node_library/state_machine/state.md)
- [State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)
