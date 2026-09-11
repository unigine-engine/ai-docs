# Portal


Nodes that carry a value or the execution flow between distant parts of the same graph without a wire. A portal in and a portal out that share a **name** form a pair.


A long wire across a large graph is hard to follow; a named pair keeps the layout readable while the connection stays explicit.


## How Names Are Matched


An execution portal triggers every portal out that carries its name, so one portal in can start several branches at once. A data portal out takes its value from the first matching portal in, so each value is best given a name of its own.


Data portals fetch the value at the moment it is read rather than storing it. To hold a value over time, use a [variable](../../../../../../code/plugins/scenariomanager/node_library/variables/index.md).


> **Notice:** Portals reach only within the graph that holds them. To cross into another graph, use the pins of a [Subgraph](../../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md).


## Articles in This Section

- [Data Portal In Node](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_in.md)

- [Data Portal Out Node](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_out.md)

- [Exec Portal In Node](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_in.md)

- [Exec Portal Out Node](../../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_out.md)
