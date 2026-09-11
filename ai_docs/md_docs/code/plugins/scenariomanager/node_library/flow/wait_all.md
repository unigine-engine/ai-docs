# Wait All


![](../img/wait_all.png)

### Description

Waits until every one of its execution inputs has been triggered, then fires **Done** once. The inputs can be triggered in any order and at any time - the node remembers which ones have already arrived.


Once **Done** has fired, the node starts over: all inputs have to be triggered again for it to fire a second time. Triggering the same input twice before the others have arrived does not count as two.


The number of inputs is not fixed: add or remove them in the node body, up to 30. Use this node to join branches that were split by a [Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/sequence.md) and may finish at different times.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action 0** | One of the inputs to wait for. |
| ![](../img/types/exec.png) | **Action 1** | One of the inputs to wait for. |
| ![](../img/types/exec.png) | **Done** | Fires when every input has been triggered. |


## See Also


- [Wait Any](../../../../../code/plugins/scenariomanager/node_library/flow/wait_any.md)
- [Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/sequence.md)
- [Wait Until](../../../../../code/plugins/scenariomanager/node_library/flow/wait_until.md)
