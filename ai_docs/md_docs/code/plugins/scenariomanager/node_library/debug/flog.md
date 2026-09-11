# Format Log


![](../img/format_log.png)

### Description

Writes a message to the log with the connected values substituted into the **Format** parameter.


Placeholders are written as {0}, {1} and so on, numbered from the topmost value input. The number of inputs is not fixed: add or remove input ports in the node body to report as many values as needed. Values of any type are converted to text before substitution.


As with [Log](../../../../../code/plugins/scenariomanager/node_library/debug/log.md), the **Level** parameter selects how the entry is reported, and **Tag** adds a label to the prefix.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/any.png) | **Arg 0** | The value substituted for {0}. |
| ![](../img/types/any.png) | **Arg 1** | The value substituted for {1}. |
| ![](../img/types/exec.png) | **Event** | Fires after the message has been written. |


## See Also


- [Log](../../../../../code/plugins/scenariomanager/node_library/debug/log.md)
- [Format](../../../../../code/plugins/scenariomanager/node_library/string/format.md)
- [Print to Screen](../../../../../code/plugins/scenariomanager/node_library/debug/print_screen.md)
