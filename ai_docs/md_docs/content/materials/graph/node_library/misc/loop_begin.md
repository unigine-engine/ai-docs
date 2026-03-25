# Loop Begin Node


![](../img/loop_begin.png)

### Description

Loops make it possible to repeat an arbitrary set of operations multiple times. The Loop Begin node enables you to create variables to which you can write data via the [Loop End](../../../../../content/materials/graph/node_library/misc/loop_end.md) node and again read this data in Loop Begin. In order for the two nodes to work together in a loop with the same set of variables, they should be connected together.


- Add - input data for use within the loop.
- Loop - pointer linking to the [Loop End](../../../../../content/materials/graph/node_library/misc/loop_end.md) node.
- Index - current iteration index. > **Notice:** The loop begins from 0, so if it has 16 iterations, the index of the last one will be 15.
- Maximum Iterations - number of iterations in the loop.


Double-click the Loop Begin node to open the loop constructor, where you can set the Maximum Iterations value and add inputs for the variables you will use in the loop. You can edit the created inputs, changing their type, name, and order in the node list. Delete any unused inputs as needed.


Available input variable types include *float, float2, float3, float4, int, int2, int3, int4, bool, float2*2, float3*3, float4*4*. To learn more about working with loops, follow [this link](https://developer.unigine.com/en/docs/latest/content/materials/graph/#loops).


## Usage Examples

**Example 1**


For a detailed description, please refer to the [Loop Sample](https://developer.unigine.com/en/docs/future/content/materials/graph/samples/loop/?rlang=cpp).


| [**View Fullscreen**](https://matgraph.unigine.com/SampleLoop_2.21/fullView) |
|---|
