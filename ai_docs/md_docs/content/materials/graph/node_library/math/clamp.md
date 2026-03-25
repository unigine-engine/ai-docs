# Clamp Node


![](../img/clamp.png)

### Description

Outputs the input value clamped between Min and Max.


- Min is returned if input is less than Min
- value is returned if input is between Min and Max
- Max is returned if input is greater than Max


This node is used when you want to cut the unnecessary ranges of values higher and lower than certain limits (Min and Max).


## Usage Examples

**Gradient Mask**

[![](../img/subtract_ex_2.gif)](../img/subtract_ex_2.gif)


Gradient mask controlling interpolation (along U-axis) between two given textures, with *Slider1* controlling the position of the transition and *Slider2* controlling transition softness. Outputs of two **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** nodes are connected to the **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node that performs linear interpolation between texture values with an interpolation coefficient. To get this coefficient we take U coordinate from the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node and subtract it from the current *Slider1* value using the **[Subtract](../../../../../content/materials/graph/node_library/math/subtract.md)** node, the result is then passed to the **[Divide](../../../../../content/materials/graph/node_library/math/divide.md)** node to be divided by the value of *Slider2*, then the result is summed up with *Slider1* value and passed to the **Clamp** node to be restricted to the [0;1] range. The result of linear interpolation provides *Albedo* values for the **Material**.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsClamp_2.21/fullView) |
|---|
