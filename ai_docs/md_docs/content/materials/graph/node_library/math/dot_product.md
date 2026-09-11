# Dot Product Node


![](../img/dot_product.png)

### Description

Outputs the dot product of two vectors A and B, which is the sum of the multiplication of each vectors components. For example, if A and B are 3-component vectors, then the result is `A.x * B.x + A.y * B.y + A.z * B.z`.


If A and B have a different number of components, a cast is performed to match the one with the greater number of components.


The geometric interpretation of the dot product is that it represents the magnitude of one vector's projection onto another. This projection can be visualized as the "shadow" of one vector cast onto the axis defined by the direction of the other.


The dot product is commutative, so the order of arguments is not important.


This operation is essential in shading, determining light intensity based on the alignment between the surface normal and the light direction.


## Usage Examples

**View-Dependent Shading**

[![](../img/dot_product_1.png)](../img/dot_product_1.png)


The example demonstrates a view-dependent shading effect, where color transitions are based on the alignment between the view direction and the surface normal.


The outputs of the **[View Direction](../../../../../content/materials/graph/node_library/input/view_direction.md)** and **[Vertex Normal](../../../../../content/materials/graph/node_library/input/vertex_normal.md)** nodes in *Tangent* space are connected to the **Dot Product** node that calculates the dot product of these vectors. The result is inverted by subtracting it from 1 using **input adapter** and passed to the **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node as a linear interpolation coefficient. The **Lerp** node blends between two colors � red and green � based on this coefficient. The result of linear interpolation provides *Albedo* values for the **Material**.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsDotProduct_2.21/fullView) |
|---|
