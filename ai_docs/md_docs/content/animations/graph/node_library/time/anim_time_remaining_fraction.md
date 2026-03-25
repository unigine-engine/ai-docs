# Anim Time Remaining Fraction


![](../img/anim_time_remaining_fraction.png)

### Description

Outputs the remaining playback time as a normalized fraction of the total animation length. A value of 0.1 means 10% of the animation is left. This is useful for transitions that should fire at a consistent relative point regardless of animation length.


> **Notice:** Produces meaningful values only inside a **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)** graph of a **[State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)**, or in any graph nested within one. In other contexts, the value is always 0.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Fraction** | Remaining time as a fraction [0..1]. |


## See Also


- [Anim Time Remaining](../../../../../content/animations/graph/node_library/time/anim_time_remaining.md)
- [Anim Time Fraction](../../../../../content/animations/graph/node_library/time/anim_time_fraction.md)
- [Animation Ended](../../../../../content/animations/graph/node_library/time/animation_ended.md)
