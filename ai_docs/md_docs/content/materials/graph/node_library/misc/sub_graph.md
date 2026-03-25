# Sub Graph Node


![](../img/sub_graph.png)

### Description

This is a custom node implementing certain functionality, constructed using other graph nodes, and saved to an `.msubgraph` asset on disk. To specify such an asset to the Sub Graph node, double-click the node and select the desired asset. For your convenience there is a set of subgraphs available out-of-the-box in the `core/subgraphs` folder implementing different functionality like *Parallax Occlusion Mapping*, *Fresnel* effect, and others to be used in your materials (new subgraphs can be added with SDK releases).


*Inputs* and *outputs* of the subgraph are defined when creating the subgraph and are stored in the asset. When you create an input in the subgraph, the data you connect to it is considered to be a default value. That's why the subgraph works even when nothing is connected to its ports, as default values are used in this case.


The set of usecases for subgraphs includes creation of custom nodes, grouping several nodes into a single container-node to save space and reduce visual complexity and a lot more.
