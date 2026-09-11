# Assert


![](../img/assert.png)

### Description

Checks that a condition holds and stops the script if it does not.


When **Condition** is true, the execution flow continues through **Event**. When it is false, the message is written to the log as an error, the script is put into the error state, and **Event** does not fire - nothing further in the script runs.


> **Notice:** Use this node for conditions that indicate a broken scenario rather than for ordinary branching. To choose between two paths without stopping anything, use [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md).


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/bool.png) | **Condition** | The condition that is expected to be true. |
| ![](../img/types/string.png) | **Message** | The text reported when the condition fails. |
| ![](../img/types/exec.png) | **Event** | Fires when the condition holds. |


## See Also


- [Log](../../../../../code/plugins/scenariomanager/node_library/debug/log.md)
- [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md)
- [Stop Script](../../../../../code/plugins/scenariomanager/node_library/flow/stop_script.md)
