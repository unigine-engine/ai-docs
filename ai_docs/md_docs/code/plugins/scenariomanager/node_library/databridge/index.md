# DataBridge Nodes


Nodes that read and write [DataBridge](../../../../../code/plugins/databridge/index_cpp.md) parameters, which is how a graph exchanges data with components, other subsystems, and anything else published on the bus.


> **Notice:** These nodes require the [DataBridge](../../../../../code/plugins/databridge/index_cpp.md) plugin to be enabled and loaded.


## Parameter Paths


Every parameter is addressed by a path whose segments are separated by a slash, such as plane/fuel/level. Paths are arranged in a tree: [List Children](../../../../../code/plugins/scenariomanager/node_library/databridge/list_children.md) reports what a node of that tree contains, and [Path Builder](../../../../../code/plugins/scenariomanager/node_library/databridge/path_builder.md) assembles a path from separate pieces, which is how a graph addresses a different object depending on what happens at runtime.


Each node takes its path either from the **Path** parameter in the node body or from the port of the same name when something is connected to it.


## Values and Types


Parameters carry values of their own types, which are converted to and from port values automatically. Types with no counterpart on the bus - execution, arrays, and the smaller matrices - are written as text.


## Articles in This Section

- [Batch Set Node](../../../../../code/plugins/scenariomanager/node_library/databridge/batch_set.md)

- [Get Parameter Node](../../../../../code/plugins/scenariomanager/node_library/databridge/get.md)

- [List Children Node](../../../../../code/plugins/scenariomanager/node_library/databridge/list_children.md)

- [On Parameter Changed Node](../../../../../code/plugins/scenariomanager/node_library/databridge/on_changed.md)

- [Path Builder Node](../../../../../code/plugins/scenariomanager/node_library/databridge/path_builder.md)

- [Set Parameter Node](../../../../../code/plugins/scenariomanager/node_library/databridge/set.md)
