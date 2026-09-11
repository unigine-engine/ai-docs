# Switch


![](../img/switch.png)

### Description

Sends the execution flow to the output whose match value equals **Value**. Each case output has a matching value input, checked from top to bottom; the first one that equals **Value** fires, and the rest are skipped. If none of them matches, **Default** fires.


Exactly one output fires each time. The number of cases is not fixed: add or remove case ports in the node body, and each new case gets its own match value.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/int.png) | **Value** | The value to compare against each case. |
| ![](../img/types/int.png) | **Match 0** | The value that makes **Case 0** fire. |
| ![](../img/types/int.png) | **Match 1** | The value that makes **Case 1** fire. |
| ![](../img/types/exec.png) | **Case 0** | Fires if **Value** equals **Match 0**. |
| ![](../img/types/exec.png) | **Case 1** | Fires if **Value** equals **Match 1**. |
| ![](../img/types/exec.png) | **Default** | Fires if no case matches. |


## See Also


- [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md)
- [Select](../../../../../code/plugins/scenariomanager/node_library/flow/select.md)
- [Conditional Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/cond_sequence.md)
