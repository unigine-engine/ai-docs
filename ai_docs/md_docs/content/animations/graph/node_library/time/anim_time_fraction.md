# Anim Time Fraction


![](../img/anim_time_fraction.png)

### Description

Outputs the current playback time as a normalized fraction of the total animation length. A value of 0.3 means 30% of the animation has played. This is convenient for transitions or effects that depend on relative animation progress rather than absolute time.


> **Notice:** Produces meaningful values only inside a **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)** graph of a **[State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)**, or in any graph nested within one. In other contexts, the value is always 0.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Fraction** | Current playback time as a fraction [0..1]. |


## See Also


- [Anim Time](../../../../../content/animations/graph/node_library/time/anim_time.md)
- [Anim Time Remaining Fraction](../../../../../content/animations/graph/node_library/time/anim_time_remaining_fraction.md)
- [Anim Length](../../../../../content/animations/graph/node_library/time/anim_length.md)
