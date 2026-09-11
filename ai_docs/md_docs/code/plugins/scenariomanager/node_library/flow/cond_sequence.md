# Conditional Sequence


![](../img/conditional_sequence.png)

### Description

Fires each of its outputs in top-to-bottom order, but skips the ones whose condition is false. It is a [Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/sequence.md) with a per-branch condition: each output has a matching condition input, and the output fires only if that input is true.


Conditions are checked one by one as execution proceeds, not all at once up front. A condition that changes while an earlier branch is running affects the branches that have not been reached yet.


The number of condition-output pairs is not fixed: add or remove ports in the node body as needed.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/bool.png) | **Cond 0** | The condition for **Out 0**. |
| ![](../img/types/bool.png) | **Cond 1** | The condition for **Out 1**. |
| ![](../img/types/exec.png) | **Out 0** | Fires if **Cond 0** is true. |
| ![](../img/types/exec.png) | **Out 1** | Fires after **Out 0** has finished, if **Cond 1** is true. |


## See Also


- [Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/sequence.md)
- [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md)
- [Switch](../../../../../code/plugins/scenariomanager/node_library/flow/switch.md)
