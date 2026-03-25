# Animation Ended


![](../img/animation_ended.png)

### Description

Outputs whether the animation of the current state has finished playing. Commonly used in transition conditions to move to the next state when a non-looping animation completes (for example, transitioning from a "Jump" state to a "Land" state once the jump animation reaches its end).


> **Notice:** Produces meaningful values only inside a **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)** graph of a **[State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)**, or in any graph nested within one. In other contexts, the value is always false.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/bool.png) | **Ended** | true if the non-looping animation has reached its end. |


## See Also


- [State Time](../../../../../content/animations/graph/node_library/time/state_time.md)
- [Time](../../../../../content/animations/graph/node_library/time/index.md)
- [Anim Time](../../../../../content/animations/graph/node_library/time/anim_time.md)
