# Lerp Node


![](../img/lerp.png)

### Description

This node is used to blend (linear interpolation) between two input values or colors A and B depending on the Coefficient.


- if Coefficient = 0 the node outputs A value
- if Coefficient = 0.5 the node outputs a halfway blend between A and B
- if Coefficient = 1 the node outputs B value
- for all other Coefficient values the node outputs a linear blend of A and B


## Usage Examples

**Gradient Mask**

[![](../img/subtract_ex_2.gif)](../img/subtract_ex_2.gif)


Gradient mask controlling interpolation (along U-axis) between two given textures, with *Slider1* controlling the position of the transition and *Slider2* controlling transition softness. Outputs of two **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** nodes are connected to the **Lerp** node that performs linear interpolation between texture values with an interpolation coefficient. To get this coefficient we take U coordinate from the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node and subtract it from the current *Slider1* value using the **[Subtract](../../../../../content/materials/graph/node_library/math/subtract.md)** node, the result is then passed to the **[Divide](../../../../../content/materials/graph/node_library/math/divide.md)** node to be divided by the value of *Slider2*, then the result is summed up with *Slider1* value and passed to the **[Clamp](../../../../../content/materials/graph/node_library/math/clamp.md)** node to be restricted to the [0;1] range. The result of linear interpolation provides *Albedo* values for the **Material**.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsLerp_2.21/fullView) |
|---|
