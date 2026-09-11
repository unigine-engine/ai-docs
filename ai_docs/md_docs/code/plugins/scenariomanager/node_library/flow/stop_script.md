# Stop Script


![](../img/stop_script.png)

### Description

Stops a running scenario graph by its script identifier. A **Script ID** below zero stops the graph the node itself belongs to, which makes it a way for a scenario to end itself.


The chain continues from **Event** after the stop has been queued.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/int.png) | **Script ID** | The identifier of the script to stop. A value below zero stops the current one. |
| ![](../img/types/exec.png) | **Event** | Fires after the stop has been queued. |


## See Also


- [Run Script](../../../../../code/plugins/scenariomanager/node_library/flow/run_script.md)
- [Get My Script ID](../../../../../code/plugins/scenariomanager/node_library/script/my_script_id.md)
