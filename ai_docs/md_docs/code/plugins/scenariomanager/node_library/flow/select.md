# Select


![](../img/select.png)

### Description

Outputs one of two values depending on a condition: **A** if **Condition** is true, **B** otherwise.


This is a data node - it has no execution ports and does not take part in the execution chain. It is evaluated when another node requests its output, which makes it the data counterpart of [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md): **Branch** chooses which actions run, **Select** chooses which value is passed on.


The inputs and the output are of the Any type: the actual type is resolved from whatever is connected, and both values must be of the same type.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/bool.png) | **Condition** | Selects which of the two values is passed to the output. |
| ![](../img/types/any.png) | **A** | Returned if the condition is true. |
| ![](../img/types/any.png) | **B** | Returned if the condition is false. |
| ![](../img/types/any.png) | **Value** | The selected value. |


## See Also


- [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md)
- [Switch](../../../../../code/plugins/scenariomanager/node_library/flow/switch.md)
