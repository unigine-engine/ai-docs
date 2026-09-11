# impostor_material


The *impostor_material* material is used for [impostors](../../../editor2/tools/impostors_creator/index.md) of the *[Octahedral](../../../editor2/tools/impostors_creator/index.md#impostor_type)* type, both *Mesh Static* and *Mesh Clutter* objects.


## Base Options


![Base Options](impostor_material_base_options.png)


In addition to the common [material options](../../../editor2/materials_settings/index.md#options) and such *mesh_base* options as *[Material Mask](../../../content/materials/library/mesh_base/index.md#material_mask)*, *[Terrain Lerp](../../../content/materials/library/mesh_base/index.md#terrain_lerp)*, and *[Lightmap Cubic Filtering](../../../content/materials/library/mesh_base/index.md#option_light_map_cubic_filtering)*, this material has a specific option that configures the [object bounds](../../../principles/world_management/index.md#bounds):


| Bound Mode | - **Custom** � bound box around the impostor. The default values are taken from the source mesh. - **Default** � flat bound rectangle at the impostor spot. |
|---|---|
| Bound Minimum | Coordinates of the bound box minimum. |
| Bound Maximum | Coordinates of the bound box maximum. |
| Bound Scale | Scale of the flat bound at the impostor spot. |


## Post Processing


![Post Processing Options](impostor_material_post_processing.png)


Post processing options are described [here](../../../content/materials/library/mesh_base/index.md#post_processing).


## States


The States tab contains the following settings and options:


![States](impostor_material_states.png)


| AO Map | Enables the ambient occlusion effect. This effect is used to modulate global environment illumination using baked shadows from environment probes. Enabling the option activates the [ambient occlusion texture](#texture_ao). |
|---|---|
| Shading Map | Enables the [shading texture](#texture_shading) for the material. |
| Translucent Map | Enables the [translucent texture](#texture_translucent) for the material. |
| Depth Map | Enables the [depth texture](#texture_depth) for the material. |
| Depth Shadow Only | If enabled, depth offset is done for shadow only. If disabled, depth offset is done for both the impostor and its shadow. The offset value is adjusted by the *[Shadow Offset](#parameter_shadow_offset)* parameter. |
| Parallax Offset | Enables the use of the depth texture to distort the texture coordinates. The intensity of the distortion is defined by the *[Parallax Intensity](#parameter_parallax_intensity)* value. |
| Vertex Interpolation | The optimization technique that allows performing shader calculations per vertex. If disabled, shader calculations are done per fragment, which is more performance-consuming. |
| Opacity Jitter | Enables the effect of deferred transparency by using alpha testing and moving (jittering) of pixels. The extensity of effect is controlled by the *[Opacity Jitter Intensity](#parameter_opacity_jitter_intensity)* value. |


The following textures may be configured for impostors depending on the enabled states:


| Albedo | The albedo texture specifies the color of the impostor surface. The texture is created by the [Impostors Creator](../../../editor2/tools/impostors_creator/index.md) tool and is set automatically after generation. The texture is 4-channelled (*RGBA*): - *RGB* values store color information. - *Alpha (A)* value stores transparency information. |
|---|---|
| Normal | Normal map stores information required to achieve an effect of creating the illusion of depth for adding details without using additional polygons. When calculating lighting of the surface, the mesh geometry is overridden by the normals value. The 3-channel texture stores coordinates in Object space. |
| Shading | The shading texture is a container for four different textures: - *R* channel stores the *[metalness](../../../content/materials/library/mesh_base/index.md#texture_metalness_channel)* texture. - *G* channel stores the *[roughness](../../../content/materials/library/mesh_base/index.md#texture_roughness_channel)* texture. - *B* channel stores the *[specular](../../../content/materials/library/mesh_base/index.md#texture_specular_channel)* texture. - *A* channel stores the *[microfiber](../../../content/materials/library/mesh_base/index.md#texture_microfiber_channel)* texture. |
| Translucent | Translucent texture stores information on the material's translucency. For example, by using this texture, it is possible to specify parts of the object that aren't translucent (the *[Translucency](#parameter_translucency)* parameter won't affect them). The texture is 1-channelled. |
| Ambient Occlusion | Ambient occlusion texture modulates the global environment illumination, for example, when an object is lighter at the top from the sky above, and darker at the bottom from the ground below. The texture uses only *R* channel. |
| Depth | Depth texture stores information on the material's depth. The texture is 1-channelled. |


The following parameters may be configured for impostors depending on the enabled states:


| Atlas Number | Number of rows and columns in the atlas that stores the captured impostor images. |
|---|---|
| Metalness | Multiplier for metalness values stored in the [metalness texture](#texture_shading). |
| Roughness | Multiplier for the surface roughness values stored in the [metalness texture](#texture_shading). |
| Specular | Multiplier for the intensity of highlight provided by the [specular texture](#texture_shading). |
| Microfiber | Coefficient to scale the intensity of microfiber (provided by the [microfiber texture](#texture_shading)). The higher the value, the higher the microfiber texture effect is. |
| Translucency | Scale of the translucency effect, which allows the light to pass through the object, but diffuses it, so objects on the opposite side are not clearly visible. |
| Parallax Intensity | Intensity of the *[parallax offset](#parallax_offset)* distortion effect. |
| Shadow Offset | Offset value for impostor shadows. |
| Opacity Jitter Intensity | Multiplier for the jittering effect creating transparency. |
| Size | Size of the object for which impostors were grabbed. |
| Pivot Offset | Offset of the pivot point from the center of the object's bounding box. |
