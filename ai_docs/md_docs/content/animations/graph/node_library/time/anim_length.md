# Anim Length


![](../img/anim_length.png)

### Description

Outputs the total duration (in seconds) of the animation playing in the current state. This can be used to calculate normalized playback progress or to set up time-based logic relative to animation length.


> **Notice:** Produces meaningful values only inside a **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)** graph of a **[State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)**, or in any graph nested within one. In other contexts, the value is always 0.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Length** | Total animation length in seconds. |


## See Also


- [Anim Time](../../../../../content/animations/graph/node_library/time/anim_time.md)
- [Anim Time Remaining](../../../../../content/animations/graph/node_library/time/anim_time_remaining.md)
- [Animation Ended](../../../../../content/animations/graph/node_library/time/animation_ended.md)
