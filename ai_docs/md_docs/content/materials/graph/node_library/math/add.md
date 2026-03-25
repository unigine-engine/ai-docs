# Add Node


![](../img/add.png)

### Description

Outputs the sum of the two input values A and B. Addition between vector data types are done per-component.


If A and B have a different number of components, a cast is performed to match the one with the greater number of components.


Addition operation is commutative so the order of values is not important.


## Usage Examples

**Example 1**

[![](../img/add_ex_1.png)](../img/add_ex_1.png)


The **Add** node takes color values from the first **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node and adds to them the values from the second **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node providing *Albedo* values for the **Material**. This node can be used to implement *Additive* Blending Mode (or *Linear Dodge*), for example.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsAdd_2.21/fullView) |
|---|
