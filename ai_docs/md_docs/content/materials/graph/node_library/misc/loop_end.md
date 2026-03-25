# Loop End Node


![](../img/loop_end.png)

### Description

Loops make it possible to repeat an arbitrary set of operations multiple times. The [Loop Begin](../../../../../content/materials/graph/node_library/misc/loop_begin.md) node enables you to create variables to which you can write data via the Loop End node and again read this data in [Loop Begin](../../../../../content/materials/graph/node_library/misc/loop_begin.md). In order for the two nodes to work together in a loop with the same set of variables, they should be connected together.


- Loop - pointer linking to the [Loop Begin](../../../../../content/materials/graph/node_library/misc/loop_begin.md) node.
- Break - boolean value used to determine whether the loop should continue, or break. If the value is 0 the specified number of loop iterations are repeated, when the value is 1 the loop breaks immediately.


After linking the loop nodes, the Loop End node will display a list of variables from the linked [Loop Begin](../../../../../content/materials/graph/node_library/misc/loop_begin.md) node. To learn more about working with loops, follow [this link](https://developer.unigine.com/en/docs/latest/content/materials/graph/#loops).


## Usage Examples

**Example 1**


For a detailed description, please refer to the [Loop Sample](https://developer.unigine.com/en/docs/future/content/materials/graph/samples/loop/?rlang=cpp).


| [**View Fullscreen**](https://matgraph.unigine.com/SampleLoop_2.21/fullView) |
|---|
