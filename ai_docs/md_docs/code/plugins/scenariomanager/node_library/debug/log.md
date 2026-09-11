# Log


![](../img/log_debug.png)

### Description

Writes a message to the log and continues the execution chain.


The **Level** parameter selects how the entry is reported - as a message, a warning or an error. Entries are prefixed with SM Script, or with SM [tag] when **Tag** is set.


To insert values into the text, use [Format Log](../../../../../code/plugins/scenariomanager/node_library/debug/flog.md).


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/string.png) | **Message** | The text to write. |
| ![](../img/types/string.png) | **Tag** | An optional label added to the prefix to identify the source of the entry. |
| ![](../img/types/exec.png) | **Event** | Fires after the message has been written. |


## See Also


- [Format Log](../../../../../code/plugins/scenariomanager/node_library/debug/flog.md)
- [Print to Screen](../../../../../code/plugins/scenariomanager/node_library/debug/print_screen.md)
- [Assert](../../../../../code/plugins/scenariomanager/node_library/debug/assert.md)
