# Anim Time


![](../img/anim_time.png)

### Description

Outputs the current playback time (in seconds) of the animation playing in the current state. Useful for triggering events at specific moments during animation playback or for calculating how far into the animation playback has progressed.


> **Notice:** Produces meaningful values only inside a **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)** graph of a **[State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)**, or in any graph nested within one. In other contexts, the value is always 0.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Time** | Current playback time in seconds. |


## See Also


- [Anim Time Fraction](../../../../../content/animations/graph/node_library/time/anim_time_fraction.md)
- [Anim Length](../../../../../content/animations/graph/node_library/time/anim_length.md)
- [State Time](../../../../../content/animations/graph/node_library/time/state_time.md)
