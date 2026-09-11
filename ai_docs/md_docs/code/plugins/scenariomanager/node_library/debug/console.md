# Console Command


![](../img/console_command.png)

### Description

Runs an engine [console](../../../../../code/console/index.md) command, which lets a graph change a render setting, toggle a debug view, or do anything else the console offers.


An empty command is skipped. The execution flow continues in either case.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/string.png) | **Command** | The console command to run, written as it would be typed in the console. |
| ![](../img/types/exec.png) | **Event** | Fires after the command has been run. |


## See Also


- [Log](../../../../../code/plugins/scenariomanager/node_library/debug/log.md)
- [Print to Screen](../../../../../code/plugins/scenariomanager/node_library/debug/print_screen.md)
