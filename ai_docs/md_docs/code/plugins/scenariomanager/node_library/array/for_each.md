# For Each


![](../img/for_each.png)

### Description

Walks through an array element by element. **Body** fires once for every element, with **Element** and **Index** holding the current one; when the whole array has been covered, **Completed** fires.


Each iteration waits for the chain attached to **Body** to finish before the next one starts, so a loop body containing [Delay](../../../../../code/plugins/scenariomanager/node_library/flow/delay.md) or another node that spans several frames works as expected.


The array is copied when the loop starts, and the loop runs over that copy. Changing the source array while the loop is running does not affect the elements it visits or how many iterations it makes.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Starts the loop. |
| ![](../img/types/array.png) | **Array** | The array to walk through. |
| ![](../img/types/exec.png) | **Body** | Fires once per element. |
| ![](../img/types/exec.png) | **Completed** | Fires after the last element has been processed. |
| ![](../img/types/any.png) | **Element** | The element of the current iteration. |
| ![](../img/types/int.png) | **Index** | The position of the current element, counted from 0. |


## See Also


- [For Loop](../../../../../code/plugins/scenariomanager/node_library/flow/for_loop.md)
- [While Loop](../../../../../code/plugins/scenariomanager/node_library/flow/while_loop.md)
- [Array Length](../../../../../code/plugins/scenariomanager/node_library/array/length.md)
