# Multiply Node


![](../img/multiply.png)

### Description

Outputs the product of the two input factor values A and B. Multiplication between vector data types is done per-component.


If A and B have a different number of components, a cast is performed to match the one with the greater number of components.


Multiplication operation is commutative so the order of values is not important.


## Usage Examples

**Example 1**

[![](../img/multiply_ex_1.png)](../img/multiply_ex_1.png)


The **Multiply** node multiplies color values from the first **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node by the values from the second **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node and provides *Albedo* values for the **Material**. This node can be used to implement *Multiply* Blending Mode, for example.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsMultiply_2.21/fullView) |
|---|
