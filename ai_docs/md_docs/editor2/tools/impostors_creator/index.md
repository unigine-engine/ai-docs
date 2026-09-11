# Generating Impostors with Impostors Creator


*Impostors Creator* tool is used to create impostors that are rendered instead of real objects at large distances. Impostors are commonly used to optimize performance if you use mesh clutters: at a certain distance from the camera, they are rendered instead of the real geometry.


> **Notice:** To open the *Impostors Creator* tool, choose *Tools -> Impostors Creator* in the Menu Bar.
> To learn how to use the tool, watch [this video tutorial](#video_tutorial).


![](impostors_creator.png)

*Impostors Creator Tool*


The Impostors Creator tool allows generating impostors for a **single object** or for **objects baked into a mesh clutter**. The type of the created Impostor object will differ depending on the source object to be baked and the [impostor type](#impostor_type) (approach to taking images).


The tool also provides special settings for generating impostors for vegetation. Impostor textures generated for vegetation ensure that when rotating a camera around any tree, its trunk will exactly match its geometry original regardless of the tree shape complexity.


### See Also


- The articles on [grass_impostor_base](../../../content/materials/library/grass_impostor_base/index.md) and [billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md) materials.
- The articles on *[Grass](../../../objects/objects/grass/index.md)* and *[Billboards](../../../objects/objects/billboards/index.md)* objects.
- The part of the [Content Optimization](../../../videotutorials/essentials/content_optimization.md) video tutorial dedicated to [generating impostors](https://youtu.be/Iqsr3fEvnis?t=161).


## Impostors Creator Settings


The *Impostors Creator* tool has the following settings.


| Impostor Type | Type of projection into which the images of an object are captured from different view directions (images are currently captured from the top hemisphere only for both projection types): - ***Octahedral*** (advanced approach): images are captured into a compact, more visually accurate and distortion-minimized format using octahedral projection that provides a uniform distribution of view angles. This type of impostor has no gimbal lock issue. Additionally, it features depth testing of the object image, not only its shadow. The type of the created impostor object is: - *[Static Mesh](../../../objects/objects/mesh/index.md)* for an individual object (*[Static Mesh](../../../objects/objects/mesh/index.md), [Dynamic Mesh](../../../objects/objects/mesh_dynamic/index.md), [Skinned Mesh](../../../objects/objects/mesh_skinned_legacy/index.md)*) - *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md)* for a *Mesh Clutter* object - ***Spherical*** (prior workflow): images are captured into a spherical layout, which stores views in a simple grid. The texture may be optimized to store images of elongated objects. This type also fits if you don't need the top view of the object, only the horizontal images around it. Depth testing is performed for shadows only. The type of the created impostor object is: - *Billboards* for an individual object (*[Static Mesh](../../../objects/objects/mesh/index.md), [Dynamic Mesh](../../../objects/objects/mesh_dynamic/index.md), [Skinned Mesh](../../../objects/objects/mesh_skinned_legacy/index.md)*) - *Grass* for a *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md)* object |
|---|---|


### Textures


The tool allows generating the following textures for impostors:


| Final Image | Specifies if the final image (the model as it is) should be generated for the impostor. Here you can also specify a postfix for the image name (_final by default). |
|---|---|
| Albedo | Specifies if the albedo texture should be generated for the impostor. Here you can also specify a postfix for the texture name (_alb by default). For this texture, the following modes are also available: - **With SSAO** � when chosen, the albedo color is multiplied by the SSAO coefficient. It allows you to improve the relief effect of the impostor. - **Without SSAO** � the albedo color from the albedo buffer is saved to the texture. If the option is set, the generated impostors will be lighter. |
| Normal | Specifies if the normal texture should be generated for the impostor. Here you can also specify a postfix for the texture name (_n by default). For this texture, the following modes are also available: - **For Vegetation** � when chosen, the grabbed normal texture looks rounded (i.e. it differs from the normal data stored in the normal buffer). - **For Other Objects** � the normal data from the normal buffer is saved to the texture. The difference between these modes is noticeable when the original vegetation object has translucency properly set up. |
| Shading | Specifies if the shading texture should be generated for the impostor. Here you can also specify a postfix for the texture name (_sh by default). |
| Baked AO | Specifies if the ambient occlusion texture should be generated for the impostor. Here you can also specify a postfix for the texture name (_baked_ao by default). If generated, this texture is automatically applied in the material. |
| SSAO | Specifies if the SSAO texture (not ray-traced SSAO) should be generated for the impostor. Here you can also specify a postfix for the texture name (_ao by default). The SSAO texture is automatically applied in the material if there is no baked AO texture. |
| Translucence | Specifies if the translucence texture should be generated for the impostor. Here you can also specify a postfix for the texture name (_t by default). For this texture, the following modes are also available: - **For Vegetation** � when chosen, the grabbed translucence texture stores information on vegetation translucence. It imitates the translucency of a tree crown at the edges. - **For Other Objects** � the translucence data from the translucence buffer is saved to the texture. |
| Depth | Specifies if the depth texture should be generated for the impostor. Here you can also specify a postfix for the image name (_depth by default). For this texture, only `.dds` format is available. ![](impostors_with_depth_off.jpg) ![](impostors_with_depth_on.jpg) Both using the *Depth* texture and baking the *Albedo* texture with [**SSAO**](#albedo) affect the final appearance of your impostors. Different combinations of these options can produce varying results, so it�s important to choose the one that best suits your specific use case and achieves the most realistic look. The image below demonstrates how different combinations of these two settings impact the final result. ![](ssao_depth_combos.png) |
| Opacity Lerp Map | Specifies if an additional texture should be generated for the impostor. This texture is used for smooth linear interpolation of sprites when the camera rotates around the object avoiding abrupt switching between the sprites. Here you can also specify a postfix for the image name (_opacity by default). For this texture, only `.dds` format is available. Available for [Spherical](#impostor_type) impostor type only. |


The following pictures show the difference between impostors, which textures have been baked in different modes:


![](for_vegetation.jpg) ![](for_other_objects.jpg)


> **Notice:** For the grabbed textures, point filtering is used.


For each texture, you can choose the format:


- `.tga`
- `.png`
- `.dds`
- `.psd`
- `.tiff`


All textures are imported with the *[Unchanged](../../../editor2/assets_workflow/texture_import.md#unchanged)* flag disabled. It means that [runtimes](../../../editor2/assets_workflow/assets_runtimes.md) are created for the generated impostor textures.


### Settings


#### Common Settings


The following settings are related to all types of grabbed textures:


| Resolution | The size of the grabbed texture. |
|---|---|
| Supersampling | The number of samples per pixel used for supersampling. The grabbed image is rendered in higher resolution (N times bigger) and than down-sampled to the [specified size](#resolution). The *higher* the value, the more reduced aliasing is. You can specify any of the available values for textures of any resolution. For example, for 4K textures you can specify 4x or even 8x supersampling. The option is available even for 8K textures. Available values: 1x, 2x, 4x, 8x. |
| Padding | Texture padding. The recommended value is 256. |


#### Octahedral Type Settings


The following setting is related to the generated *[impostor material](../../../editor2/tools/impostors_creator/impostor_material.md)* of the *[Octahedral](#impostor_type)* type:


| Atlas Size | The size of the created atlas texture that stores all captured images. Atlas is always a square texture. ![](tree_atlas_texture.png) *Altas size 10x10* |
|---|---|


#### Spherical Type Settings


The following settings are related to generated impostor materials ([billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md#lerp_mode) and [grass_impostor_base](../../../content/materials/library/grass_impostor_base/index.md#lerp_mode)) of the *[Spherical](#impostor_type)* type:


| Aspect | Aspect ratio (width/height) of the grabbed images. The aspect affects the size of the impostor texture cell that stores the grabbed frame (see the related material parameter). For example: - If you need to grab the impostor for an object which height far exceeds the width (e.g. pine tree, lamp post, etc.), you should use the 4/1 aspect. In this case, the height of the texture cell will be 4 times bigger than the width. For horizontal objects (e.g. fallen pine tree), the 1/4 aspect should be used. - If the original object's width to height aspect is near 1 (e.g. spherical or cuboid-shaped objects), the 1/1 value should be used. \| ![](aspect_4to1.jpg) \| \|---\| \| *Aspect = 4/1* \| | ![](aspect_4to1.jpg) | *Aspect = 4/1* |  |  |
|---|---|---|---|---|---|
| ![](aspect_4to1.jpg) |  |  |  |  |  |
| *Aspect = 4/1* |  |  |  |  |  |
| Phi | The number of frames to be grabbed into the impostor texture when the camera rotates horizontally around the object (i.e. left or right). Available values: 4, 8, 16, 32, 64. \| ![](phi_0.png) *Phi = 4* \| \|---\| \| ![](phi_1.png) *Phi = 8* \| | ![](phi_0.png) *Phi = 4* | ![](phi_1.png) *Phi = 8* |  |  |
| ![](phi_0.png) *Phi = 4* |  |  |  |  |  |
| ![](phi_1.png) *Phi = 8* |  |  |  |  |  |
| Theta | The number of frames to be grabbed into the impostor texture when the camera rotates vertically around the object (i.e. upward or downward). Available values: 1, 2, 4, 8, 16. \| ![](theta_0.png) \| ![](theta_1.png) \| \|---\|---\| \| *Theta = 2* \| *Theta = 4* \| > **Notice:** When selected value is equal to 1, **Lerp Mode** for the impostor material ([billboards_impostor_base](../../../content/materials/library/billboards_impostor_base/index.md#lerp_mode) and [grass_impostor_base](../../../content/materials/library/grass_impostor_base/index.md#lerp_mode)) shall be set to **Horizontal Only**. | ![](theta_0.png) | ![](theta_1.png) | *Theta = 2* | *Theta = 4* |
| ![](theta_0.png) | ![](theta_1.png) |  |  |  |  |
| *Theta = 2* | *Theta = 4* |  |  |  |  |


## Video Tutorial


Watch the part of the [Content Optimization video tutorial](#video_tutorial) on generating impostors.
