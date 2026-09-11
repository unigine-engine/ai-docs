# Texture Cube Node


![](../img/texture_cube.png)

### Description

This node represents a texture, that combines six images mapped onto a cube, and is mainly used to create a 360� panorama. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify Direction - a vector pointing in direction from the center of the cube to a point on the cube, at which a cubemap texel is to be taken.


You can create such texture from an HDRI panorama by simply selecting the Cube Map preset in the [texture import parameters](../../../../../editor2/assets_workflow/texture_import.md#texture_preset) or add a `_c` postfix to the file name before importing it. In this case the Engine shall generate mipmaps for the texture, looking like matte GGX reflections giving a smooth blurred result. This can be useful for imitation of matte reflections based on this texture.


You can use this texture type to create panorama, for imitation of FAKE reflections based on a custom panorama, for FAKE refractions, or something else - the scope of applications is limited by your fantasy!
