# Anim Time Remaining


![](../img/anim_time_remaining.png)

### Description

Outputs the remaining playback time (in seconds) of the animation in the current state. Useful for triggering transitions before an animation finishes - for example, starting a blend to the next state 0.2 seconds before the current animation ends.


> **Notice:** Produces meaningful values only inside a **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)** graph of a **[State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)**, or in any graph nested within one. In other contexts, the value is always 0.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Time** | Remaining time in seconds. |


## See Also


- [Anim Time Remaining Fraction](../../../../../content/animations/graph/node_library/time/anim_time_remaining_fraction.md)
- [Anim Length](../../../../../content/animations/graph/node_library/time/anim_length.md)
- [Animation Ended](../../../../../content/animations/graph/node_library/time/animation_ended.md)
- [State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)
