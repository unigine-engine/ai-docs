# Length Node


![](../img/length.png)

### Description

Outputs the euclidean length of the input vector which is the result of the following operation: **[Sqrt](../../../../../content/materials/graph/node_library/math/square_root.md) ( [Dot](../../../../../content/materials/graph/node_library/math/dot_product.md) ( Input, Input ))**.


## Usage Examples

**Distance-Based Coloring**

[![](../img/length.gif)](../img/length.gif)


This example demonstrates how to dynamically change an object's color based on its distance from the camera using the **Length** node.


The **[Camera Position](../../../../../content/materials/graph/node_library/input/camera_position.md)** vector (in *Object* space) is passed into the **Length** node to compute the distance between the camera and the object. The resulting distance is then clamped to a defined range [0, 20] using the **[Clamp](../../../../../content/materials/graph/node_library/math/clamp.md)** node. The clamped value is passed into a **[Rerange](../../../../../content/materials/graph/node_library/math/rerange.md)** node, which converts it from the source range [0, 20] to a new target range [0, 1]. Finally, the remapped value drives a **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node, blending smoothly between red (closer distances) and green (farther distances).


| [**View Fullscreen**](https://matgraph.unigine.com/DocsLength_2.21/fullView) |
|---|
