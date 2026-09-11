# Event Subgraph


![](../img/event_subgraph.png)

### Description

Runs another graph that reacts to events on its own, rather than being called for a result. The graph to use is chosen by the **file** parameter.


Where the [Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md) node is triggered by its parent and hands control back, this one hosts a graph that starts from its own event nodes and runs alongside. Behaviour that reacts on its own schedule - watching for a condition, or handling a signal whenever it arrives - belongs here.


> **Notice:** The referenced graph is loaded the first time the node runs. A file that is missing or fails to load is reported to the console.


> **Warning:** As with any subgraph, a chain of references that leads back to the graph holding it is refused and stops that graph with an error.


## See Also


- [Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md)
- [On Event](../../../../../code/plugins/scenariomanager/node_library/events/on_event.md)
- [Exec Trigger](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md)
