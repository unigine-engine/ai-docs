# Screen UV Node


![](../img/screen_uv.png)

### Description

Provides access to the position in the Screen UV coordinates. The output represent the [Screen Coord](../../../../../content/materials/graph/node_library/input/screen_coord.md) node output normalized in the [0, 1] range.


This node is useful for creating post-effects that require information about screen-space UV.


## Usage Examples

**Example 1**

[![](../img/screen_uv_ex_1.png)](../img/screen_uv_ex_1.png)


This example demonstrates a material that applies a texture to the rendered image (screen) as a post-effect (e.g., to create a lens dirt effect). The material retrieves the final rendered image (Screen Color) from the [Texture Buffer Screen Color](../../../../../content/materials/graph/node_library/textures/texture_buffer_screen_color.md) node and adds a custom Albedo texture using the [Add](../../../../../content/materials/graph/node_library/math/add.md) node. The intensity of the custom Albedo texture can be controlled by a slider, which is blended via the [Multiply](../../../../../content/materials/graph/node_library/math/multiply.md) node.


> **Notice:** The [Post Effect](../../../../../content/materials/graph/index.md#common_settings) material type is used in this example.


The Screen UV node ensures that the texture is properly applied to the rendered image, even if the screen size changes.


To see the result, set the material to the [Custom Post Materials](../../../../../editor2/settings/render_settings/custom_post/index.md) (*Settings -> World -> Runtime -> Render -> Custom Post Materials*).


| [**View Fullscreen**](https://matgraph.unigine.com/DocsScreenUV_2.21/fullView) |
|---|
