# Get My Script ID


![](../img/get_my_script_id.png)

### Description

Outputs the identifier of the script this node belongs to.


Identifiers are assigned when a script starts, so the same graph run twice gets two different ones. Pass the value to [Stop Script](../../../../../code/plugins/scenariomanager/node_library/flow/stop_script.md) to have a graph stop itself.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/int.png) | **Script ID** | The identifier of the running script, or -1 if it is not available. |


## See Also


- [Find Script By Name](../../../../../code/plugins/scenariomanager/node_library/script/find_script.md)
- [Get My Script Name](../../../../../code/plugins/scenariomanager/node_library/script/my_script_name.md)
- [Stop Script](../../../../../code/plugins/scenariomanager/node_library/flow/stop_script.md)
