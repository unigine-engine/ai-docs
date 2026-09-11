# Latch


![](../img/latch.png)

### Description

Remembers an on/off state and reports it both as a value and as events. Triggering **Set** switches the state on, triggering **Reset** switches it off, and **State** always holds the current value.


The **On Set** and **On Reset** outputs fire only when the state actually changes: setting a latch that is already set fires nothing. This makes the node useful for reacting to a transition rather than to every trigger.


Unlike [Gate](../../../../../code/plugins/scenariomanager/node_library/flow/gate.md), a latch does not pass an execution flow through - it stores a state that other nodes read.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Set** | Switches the state on. |
| ![](../img/types/exec.png) | **Reset** | Switches the state off. |
| ![](../img/types/exec.png) | **On Set** | Fires when the state changes from off to on. |
| ![](../img/types/exec.png) | **On Reset** | Fires when the state changes from on to off. |
| ![](../img/types/bool.png) | **State** | The current state. |


## Parameters


- **Start Set** - Whether the state is on before the latch is triggered for the first time.


## See Also


- [Gate](../../../../../code/plugins/scenariomanager/node_library/flow/gate.md)
- [Do Once](../../../../../code/plugins/scenariomanager/node_library/flow/do_once.md)
- [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md)
