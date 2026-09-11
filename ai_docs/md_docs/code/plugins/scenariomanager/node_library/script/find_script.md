# Find Script By Name


![](../img/find_script_by_name.png)

### Description

Looks up a running script by name and outputs its identifier, which can then be passed to [Stop Script](../../../../../code/plugins/scenariomanager/node_library/flow/stop_script.md).


Only running scripts are found. If no script with that name is running, the output is -1 - check for that value before using the result.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/string.png) | **Name** | The name of the script to look for. |
| ![](../img/types/int.png) | **Script ID** | The identifier of the script, or -1 if no running script has that name. |


## See Also


- [Stop Script](../../../../../code/plugins/scenariomanager/node_library/flow/stop_script.md)
- [Run Script](../../../../../code/plugins/scenariomanager/node_library/flow/run_script.md)
- [Get My Script ID](../../../../../code/plugins/scenariomanager/node_library/script/my_script_id.md)
