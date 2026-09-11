# Events Nodes


Nodes that start an execution chain. Every chain in a graph begins at one of these, because a node that nothing triggers never runs.


## Entry Points


Four of these nodes are tied to the life cycle of the script and are triggered by the Scenario Manager itself:


- [On Init](../../../../../code/plugins/scenariomanager/node_library/events/on_init.md) - once, when the script starts.
- [On Update](../../../../../code/plugins/scenariomanager/node_library/events/on_update.md) - every frame.
- [On Shutdown](../../../../../code/plugins/scenariomanager/node_library/events/on_shutdown.md) - once, when the script stops.
- [On Timer](../../../../../code/plugins/scenariomanager/node_library/events/on_timer.md) - at regular intervals.


The remaining two carry custom events: [Send Event](../../../../../code/plugins/scenariomanager/node_library/events/send_event.md) raises an event by name, and [On Event](../../../../../code/plugins/scenariomanager/node_library/events/on_event.md) starts a chain when an event of that name arrives. Together they let one part of a graph - or one script - trigger another without a wire between them.


## Articles in This Section

- [On Event Node](../../../../../code/plugins/scenariomanager/node_library/events/on_event.md)

- [On Init Node](../../../../../code/plugins/scenariomanager/node_library/events/on_init.md)

- [On Shutdown Node](../../../../../code/plugins/scenariomanager/node_library/events/on_shutdown.md)

- [On Timer Node](../../../../../code/plugins/scenariomanager/node_library/events/on_timer.md)

- [On Update Node](../../../../../code/plugins/scenariomanager/node_library/events/on_update.md)

- [Send Event Node](../../../../../code/plugins/scenariomanager/node_library/events/send_event.md)
