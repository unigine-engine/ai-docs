# Preview Output Pose


![](../img/preview_output_pose.png)

### Description

Marks the pose that is rendered in the standalone preview viewport of a subgraph. It lets you preview a subgraph on its own, without opening the parent graph. The node is used only for preview: it is ignored when the graph is compiled, so it has no effect on the runtime result.


Its input accepts only the mirror output of the [Sub Graph Outputs](../../../../../content/animations/graph/node_library/subgraph/sub_graph_outputs.md) node, so the preview reflects exactly what the subgraph delivers to the parent graph rather than an arbitrary internal node.


> **Notice:** Available only inside subgraphs.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_pose.png) | **Pose** | The pose to display in the standalone preview. Connect it to the mirror output of the [Sub Graph Outputs](../../../../../content/animations/graph/node_library/subgraph/sub_graph_outputs.md) node. |


## See Also


- [Subgraphs](../../../../../content/animations/sub_graphs/index.md)
- [Sub Graph Outputs](../../../../../content/animations/graph/node_library/subgraph/sub_graph_outputs.md)
- [SubGraph](../../../../../content/animations/graph/node_library/subgraph/sub_graph.md)
