# State Time


![](../img/state_time.png)

### Description

Outputs the time in seconds since the current state was entered. The timer resets to zero each time a transition into the state occurs and increases by the frame delta time every frame.


> **Notice:** Produces meaningful values only inside a **[Condition](../../../../../content/animations/graph/node_library/state_machine/condition.md)** graph of a **[State Machine](../../../../../content/animations/graph/node_library/state_machine/index.md)**, or in any graph nested within one. In other contexts, the value is always 0.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Time** | Seconds elapsed since the current state was entered. |


## See Also


- [Time](../../../../../content/animations/graph/node_library/time/index.md)
- [Animation Ended](../../../../../content/animations/graph/node_library/time/animation_ended.md)
- [Anim Time](../../../../../content/animations/graph/node_library/time/anim_time.md)
