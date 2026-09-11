# Sequence


![](../img/sequence.png)

### Description

Fires each of its outputs one after another, in top-to-bottom order. Each output waits for the whole chain of actions attached to it to finish before the next output fires, so the branches never overlap.


The number of outputs is not fixed: add or remove output ports in the node body to get as many branches as the scenario needs.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/exec.png) | **Event 0** | Fires first. |
| ![](../img/types/exec.png) | **Event 1** | Fires after the chain attached to **Event 0** has finished. |


## See Also


- [Conditional Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/cond_sequence.md)
- [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md)
- [For Loop](../../../../../code/plugins/scenariomanager/node_library/flow/for_loop.md)
