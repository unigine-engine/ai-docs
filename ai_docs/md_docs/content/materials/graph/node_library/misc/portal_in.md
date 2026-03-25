# Portal In Node


![](../img/portal_in.png)

### Description

This node enables you to create a portal entrance (you can specify a name and color for it). When working with complex or large graphs, you may end up with your wires are all over the place criscrossing each other and you may want more visual clarity. That's when portals come into play - you can connect a wire to a Portal In node at one location and then place a [Portal Out](../../../../../content/materials/graph/node_library/misc/portal_out.md) node at any other location you need and take what you've supplied to Portal In from a Portal Out (like you dug a tunnel for your wire under the node graph).


Selecting a Portal In node shows a dashed line tracing all corresponding Portal Out nodes.


![](../img/portal_link.png)


## Usage Examples

**Example 1**

[![](../img/portal_in_ex_1.png)](../img/portal_in_ex_1.png)

The node is used to connect nodes by passing a value to a portal at one location and take this value from this portal at **multiple** other locations. This works similar to a variable in programming, but here you can put a value only once and take it as many times as you need. Portals do not use names for synchronization, so you can actually create multiple portals having the same name, but we don't recommend you to do so, as you may get lost in this ambiguity.
