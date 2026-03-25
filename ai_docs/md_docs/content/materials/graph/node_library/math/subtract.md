# Subtract Node


![](../img/subtract.png)

### Description

Outputs the subtraction result of the two input values A and B. Subtraction between vector data types are done per-component.


If A and B have a different number of components, a cast is performed to match the one with the greater number of components.


Subtraction operation is not commutative so the order of values is important.


## Usage Examples

**Example 1**

[![](../img/subtract_ex_1.png)](../img/subtract_ex_1.png)


Subtracting two textures (non-commutative). The upper **Subtract** node takes color values from the first **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node (first texture) and subtracts the values from the second **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** node (second texture) from them providing *Albedo* values for the **Material**. While the lower **Subtract** node does vice versa subtracting values of the first texture from the values of the second one providing *Emission* values for the **Material** producing a nice looking effect.


**Gradient Mask with Subtract and Divide**

[![](../img/subtract_ex_2.gif)](../img/subtract_ex_2.gif)


Gradient mask controlling interpolation (along U-axis) between two given textures, with *Slider1* controlling the position of the transition and *Slider2* controlling transition softness. Outputs of two **[Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** nodes are connected to the **[Lerp](../../../../../content/materials/graph/node_library/math/lerp.md)** node that performs linear interpolation between texture values with an interpolation coefficient. To getthis coefficient we take U coordinate from the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)** node and subtract it from the current *Slider1* value, the result is then passed to the **[Divide](../../../../../content/materials/graph/node_library/math/divide.md)** node to be divided by the value of *Slider2*, then the result is summed up with *Slider1* value and passed to the **[Clamp](../../../../../content/materials/graph/node_library/math/clamp.md)** node to be restricted to the [0;1] range. The result of linear interpolation provides *Albedo* values for the **Material**.
