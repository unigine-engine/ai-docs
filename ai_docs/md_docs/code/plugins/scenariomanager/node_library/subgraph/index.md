# Subgraph Nodes


Nodes that let one graph be used inside another, so that logic written once can be reused wherever it is needed instead of being copied. They also cover [portals](../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/index.md), which carry a value or a trigger across a graph without a wire.


## The Interface of a Subgraph


A graph becomes reusable by declaring what it takes and returns. [Subgraph Input](../../../../../code/plugins/scenariomanager/node_library/subgraph/input.md) and [Subgraph Output](../../../../../code/plugins/scenariomanager/node_library/subgraph/output.md) declare its data pins, and [Exec Trigger](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md) and [Exec Done](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_done.md) its execution pins.


These nodes are what the [Subgraph](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md) node shows as pins on the parent side, in the order the interface nodes are arranged in.


## Evaluated or Executed


Whether a subgraph runs like a function or like a sequence follows from its interface. One with no [Exec Trigger](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md) has no execution pins and is evaluated whenever its result is needed, exactly as an arithmetic node is.


Adding an Exec Trigger gives it execution pins, so the parent decides when it runs.


## Recursion


> **Warning:** A subgraph cannot reference itself, directly or through another subgraph that leads back to it. Such a chain is refused when the subgraph is loaded, an error is reported to the console, and the graph holding it stops.


## Articles in This Section

- [Event Subgraph Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/event_ref.md)

- [Exec Done Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_done.md)

- [Exec Trigger Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/exec_trigger.md)

- [Subgraph Input Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/input.md)

- [Subgraph Output Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/output.md)

- [Subgraph Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/ref.md)

- [Portal](../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/index.md)

  - [Data Portal In Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_in.md)
  - [Data Portal Out Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/data_out.md)
  - [Exec Portal In Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_in.md)
  - [Exec Portal Out Node](../../../../../code/plugins/scenariomanager/node_library/subgraph/portal/exec_out.md)
