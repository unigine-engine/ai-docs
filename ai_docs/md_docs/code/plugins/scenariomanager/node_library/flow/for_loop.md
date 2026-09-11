# For Loop


![](../img/for_loop.png)

### Description

Repeats the chain attached to **Body** for a range of integers, then continues from **Completed**. The loop counts from **Start** up to but not including **End**, exposing the current value through **Index**.


Each repeat waits for the whole body chain to finish before the next one starts, so a repeat that pauses (a [Delay](../../../../../code/plugins/scenariomanager/node_library/flow/delay.md), for example) holds the loop rather than letting the repeats overlap.


If **End** is less than or equal to **Start**, the body never runs and **Completed** fires immediately. The range is limited to 100,000 repeats: a wider range is clamped, and a warning is written to the console.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/int.png) | **Start** | The first value of the counter. |
| ![](../img/types/int.png) | **End** | The value to stop at. This value itself is not used. |
| ![](../img/types/exec.png) | **Body** | Fires once per repeat. |
| ![](../img/types/exec.png) | **Completed** | Fires after the last repeat has finished. |
| ![](../img/types/int.png) | **Index** | The counter value for the current repeat. |


## See Also


- [While Loop](../../../../../code/plugins/scenariomanager/node_library/flow/while_loop.md)
- [Do N](../../../../../code/plugins/scenariomanager/node_library/flow/do_n.md)
- [Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/sequence.md)
