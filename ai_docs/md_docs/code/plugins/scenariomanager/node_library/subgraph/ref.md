# Subgraph


![](../img/subgraph.png)

### Description

Runs another graph as part of this one. The graph to use is chosen by the **file** parameter, and the node takes its pins from that graph's interface nodes - one for each [Subgraph Input](../../../../../code/plugins/scenariomanager/node_library/subgraph/input.md), [Subgraph Output](../../../../../code/plugins/scenariomanager/node_library/subgraph/output.md), [Exec Trigger](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md) and [Exec Done](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_done.md) it declares.


Logic that appears in several places is worth moving into a graph of its own and referencing here, so that a correction is made once rather than in every copy.


Whether the node has execution pins follows from the referenced graph: one that declares no Exec Trigger is evaluated whenever its result is needed, and one that declares any is run when triggered.


> **Notice:** The referenced graph is loaded the first time the node runs. A file that is missing or fails to load is reported to the console and the node produces nothing.


> **Warning:** A graph cannot reference itself, directly or through a chain of subgraphs leading back to it. Such a chain is refused and the graph holding it stops with an error.


## See Also


- [Event Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/event_ref.md)
- [Subgraph Input](../../../../../code/plugins/scenariomanager/node_library/subgraph/input.md)
- [Exec Trigger](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md)
