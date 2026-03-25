# State Portal


![](../img/state_portal.png)

### Description

Reduces visual clutter in a state machine by replacing multiple identical transitions with a single one. Select which states the portal represents via checkboxes, then draw one transition from the portal instead of a separate transition from each state.


A portal groups multiple states into a single transition source. However, transitioning **into** a portal with multiple states does not work because a single **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)** cannot determine which of the portal's states to transition to.


Self-transitions are automatically excluded - if the portal's destination state is also listed among the portal's states, that transition is skipped.


See **[State Machines](../../../../../content/animations/state_machines/index.md#state_portals)** article for details.


> **Notice:** Available only inside a **[State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)**.


## Properties


Portal properties are configured via the [Selected Item](../../../../../content/animations/graph/index.md#side_panels) panel.


| States | Checkboxes for each state in the state machine. Select which states this portal represents. |
|---|---|


## See Also


- [State Machines](../../../../../content/animations/state_machines/index.md#state_portals)
- [State](../../../../../content/animations/graph/node_library/state_machine/state.md)
- [State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)
