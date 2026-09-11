# Run Script


![](../img/run_script.png)

### Description

Starts another scenario graph by asset path. The graph is loaded and starts running as a separate script, independently of the one that started it.


The chain continues from **Event** right away, without waiting for the started graph to finish. An empty path starts nothing, but the chain still continues.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/exec.png) | **Action** | Triggers the node. |
| ![](../img/types/string.png) | **File** | The path to the `*.sgraph` asset to run. |
| ![](../img/types/exec.png) | **Event** | Fires after the graph has been queued to start. |


## See Also


- [Stop Script](../../../../../code/plugins/scenariomanager/node_library/flow/stop_script.md)
- [Sequence](../../../../../code/plugins/scenariomanager/node_library/flow/sequence.md)
