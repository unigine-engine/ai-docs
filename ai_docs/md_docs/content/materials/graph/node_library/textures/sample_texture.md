# Sample Texture Node


![](../img/sample_texture.png)

### Description

Takes an input texture (2D, 3D, 2D array, 2D int, or cubemap) and returns a value from this texture depending on the current parameter values selected for this node, other inputs are used to provide additional information required to obtain output.


> **Notice:** This node has parameters (see below) that define its behavior, to view and change them double-click somewhere inside the node.


This node automatically detects the type of texture connected to its input (2D, 3D, 2D array, 2D int, or cubemap) and what it is going to be used for.  For example, if you connect a [2D Texture](../../../../../content/materials/graph/node_library/textures/texture_2d.md) the node will automatically activate a UV input, for a [2D Texture Array](../../../../../content/materials/graph/node_library/textures/texture_2d_array.md) it will expect UV and array element Index, for a [3D Texture](../../../../../content/materials/graph/node_library/textures/texture_3d.md) - UVW coordinates, or a Direction vector for cubemaps ([Texture Cube](../../../../../content/materials/graph/node_library/textures/texture_2d.md)), for [Texture 2D Int](../../../../../content/materials/graph/node_library/textures/texture_2d_int.md) nodes an integer output is activated. Moreover, this node contains settings for interpolation of values when sampling a texture (filtering).


## Parameters

| #### Type |
|---|
| Sampling and filtering type to be used. One of the following options:: - **Default** - default sampling using UV coordinates. - **Mip** - Texture sampling using a mipmap-level. - **Mip offset** - Texture sampling using a mipmap-level offset. - **Grad** - Gradient texture sampling allows you to specify the two gradients for how the texture coordinates change locally: DDX and DDY values are vectors that represent the change of each texture coordinate per pixel of the window's X and Y coordinates. - **Fetch** - Direct texel fetch, enables direct access to texel values with non-normalized coordinates. - **Point** - Point filtering - **Catmull** - Catmull-Rom filtering - **Cubic** - Cubic filtering - **Manual linear** - Manual linear filtering |

| #### Normal Space |
|---|
| Normal space to be used. One of the following options:: - **Tangent Space for UV0** - define normals using the tangent space based on the first UV-channel (UV0). - **Tangent Space for UV1** - define normals using the tangent space based on the second UV-channel (UV1). - **Tangent Space Auto-Calculated** - define normals using the tangent space calculated automatically. - **Object Space** - define normals using object space. |
