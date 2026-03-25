# Texture 3D Node


![](../img/texture_3d.png)

### Description

This node represents the texture type that is used to store some spatial information (like clouds or fog density, or voxel lighting data), it is also called a *Volume Texture* or *Voxel Texture*. To sample data from such a texture connect it to the [Sample Texture](../../../../../content/materials/graph/node_library/textures/sample_texture.md) node and specify UVW coordinates.


You can create such texture from a 2D texture by selecting the Volume preset in the [texture import parameters](../../../../../editor2/assets_workflow/texture_import.md#texture_preset) or add a `_v` postfix to the file name before importing it. In this case the Engine Importer shall "slice" this texture into horizontal layers as many times as many texture *widths* can fit into texture *height*. For example, if you want to get a 64 x 64 x 64 3D texture you'll have to import a texture having the resolution of 64 x 4096. Usually this texture is used to sample certain data from it for different positions in space (like volumetrics or voxel-based lighting). The main advantage of this texture is that you can get intermediate values not only horizontally within a layer, but along the third axis as well.
