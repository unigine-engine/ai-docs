# decal_base


A *decal_base* material creates coverings for [decals](../../../../objects/decals/index.md).

 Prior KnowledgeThis article assumes you have prior knowledge of the following topics. Please read them before proceeding:
- *[Materials settings](../../../../editor2/materials_settings/index.md)*
- *[mesh_base](../../../../content/materials/library/mesh_base/index.md)* material states, textures, parameters


### Common Material Settings


The *decal_base* material has some changes in common settings:


- **Transparent** option is not available for Decals, because decals work only with deferred objects.
- For alpha blending use [**blend**](#option_detail_blend) option in *States* tab.
- Alpha-test decal can't be rendered in separate buffers, it overwrite all the materials under the decal. It is pretty fast and can be used for roads, for example.
- **Render order** option allows you to specify the order of decals.


### See Also


- Samples located in `decals` folder.


## States


![States](states.png)

*Materials editor,Statestab.*


### Options


#### Water Decal


In case of enabling the **Water Decal** option, decals are projected only on the top of the water surface. When the option is disabled, decals are displayed on the meshes overwater and underwater.


| ![](water_decal_0.png) *Water Decal option is disabled* | ![](water_decal_1.png) *Water Decal option is enabled* |
|---|---|


#### Distance Fade


**Distance Fade** enables smooth fading depending on the distance to the surface where decal is projected. It activates **[Distance threshold](#parameter_fade)** and **[Distance power](#parameter_fade)**


#### Angle Fade


When you enable **Angle Fade** option, the angle of the surface will have influence of the decal projection. Enabling this option activates **[Angle threshold](#parameter_angle)** and **[Angle power](#parameter_angle)** parameters that allow to modify the angle where the decal shouldn't be projected.


The angle threshold allows you to increase the slope for projecting overlap material. It can even be rendered on surfaces that face downwards.


#### Normal Substitute


**Normal substitute** specifies a rendering mode for normals. By default, normal maps of a base and overlapping material are combined together. with this option enabled, only normals of the overlapping material are used


| ![](normal_substitution_off.png) *Normal substitute off* | ![](normal_substitution_on.png) *Normal substitute on* |
|---|---|


#### Specular Map


The state defines whether to use the B channel of the [Shading](#texture_shading) texture as a [specular](#texture_specular) texture.


#### Microfiber Map


The state defines whether to use the A channel of the [Shading](#texture_shading) texture as a [microfiber](#texture_microfiber) texture.


#### Screen Projection


Enables volumetric projection of the decal following the shape of the mesh.


| ![](screen_proj_off.jpg) | ![](screen_proj_on.jpg) |
|---|---|
| *Screen Projection disabled* | *Screen Projection enabled* |


#### Auxiliary


Enables Auxiliary rendering pass for the material. Can be used for custom post-effects, such as thermal vision etc. Activates the [auxiliary texture](#textures_auxiliary) and [parameter](#auxiliary_color_parameter).


#### Emission


Enables Emission effect for the material. Activates the [emission texture](#textures_emission) and [parameters](#parameter_emission).


#### Parallax


Enables [Parallax](#states_parallax) states used for providing a convex relief based on a parallax (height) texture.


#### Detail


Enables [Detail](#state_detail) states used for bringing detalization to the decal material.


### Detail States


**Detail** activates a set of textures (albedo, normal, shading) to form a material layer. It is applied for bringing detalization to the decal material.


#### Use Alpha for Blending


**Use alpha for blending** option indicates whether to use the alpha channel of the detail texture for blending.


#### 3D Texture


**3D Texture** option indicates whether to use 3D texture for the decal.


#### Blending


Available options are:


- **Alpha Blend** - blending depends on the alpha channel of the base albedo texture.
- **Overlay** - depending on the base albedo texture color, the base and detail textures colors are either multiplied (for dark color pixels) or screened (for light color pixels), which leads to the contrast increase while preserving highlights and shadows. Grey pixels are not effected at all. The blending is applied to the first UV coordinates of the mesh.
- **Multiply** - the base albedo texture color is multiplied by the detail texture color, resulting in darker colors. White pixels are not effected at all. The blending is applied to the first UV coordinates of the mesh.


### Parallax States


**Parallax** mapping enables the parallax effect that provides a convex relief based on a parallax (height) texture.


#### Shadow


Apply the parallax shadow effect.


#### Cutout


Apply the cutout effect that provides smooth edges between the opaque and transparent areas.


### UV Mapping


#### Base


Base option specifies which UV coordinates of the mesh will be used for base textures.


> **Notice:** **Triplanar** and **World** mapping options described below work properly only within the distance range of 10000 units from the origin.


- UV - map the texture using the UV coordinates of the mesh.
- World - map the texture using world transformation (the texture is always projected atop).
- Triplanar - map the texture without using UV coordinates of the mesh (textures are projected by using triplanar mapping).


#### Detail


Base option specifies which UV coordinates of the mesh will be used for detail textures.


> **Notice:** **Triplanar** and **World** mapping options described below work properly only within the distance range of 10000 units from the origin.


- UV - map the texture using the UV coordinates of the mesh.
- World - map the texture using world transformation (the texture is always projected atop).
- Triplanar - map the texture without using UV coordinates of the mesh (textures are projected by using triplanar mapping).


## Textures


Availability of some textures depends on the set *[States](#states)* values.


![Textures](textures.png)

*Materials editor,Texturestab.*


### Base Textures


#### Albedo


**[Albedo](../../../../content/materials/library/mesh_base/index.md#texture_albedo)** texture indicates the main color of the decal.


| ![](texture_d.png) | ![](texture_angle_d.png) |
|---|---|
| *Albedo texture applied* | *Albedo texture applied (another angle view)* |


#### Normal


**[Normal](../../../../content/materials/library/mesh_base/index.md#texture_normal)** texture stores height information required to achieve an effect of Normal Mapping


| ![](texture_n.png) | ![](texture_angle_n.png) |
|---|---|
| *Normal texture applied* | *Normal texture applied (another angle view)* |


> **Notice:** **Unigine Engine** expects a normal map in *DirectX* format. If your normal map is in *OpenGL* format, tick *[Invert G Channel](../../../../editor2/assets_workflow/texture_import.md#invert_g)* in the import menu. As a general rule, if the lighting seems weird, try inverting the G Channel and see if it gets better.


#### Shading


Shading texture is a container for four different textures:

- The R channel stores a [metalness](#texture_metalness) texture.
- The G channel stores a [roughness](#texture_roughness) texture.
- The B channel stores a [specular](#texture_specular) texture.
- The A channel stores a [microfiber](#texture_microfiber) texture.


##### Metalness


**[Metalness](../../../../content/materials/library/mesh_base/index.md#texture_metalness_channel)** texture stores information about material's metalness:

- White pixels indicate that material is metal.
- Black pixels indicate that material is dielectric.


##### Roughness


**[Roughness](../../../../content/materials/library/mesh_base/index.md#texture_roughness_channel)** texture stores information about material's [roughness](../../../../content/materials/library/mesh_base/pbr.md#roughness):

- White pixels indicate that material is rough.
- Black pixels indicate that material is smooth.


##### Specular


**[Specular](../../../../content/materials/library/mesh_base/index.md#texture_specular_channel)** texture stores the light reflectance information. It defines shininess and a highlight color of the surface.


> **Notice:** To use this channel, enable the [Specular Map](#option_specular_map) state.


| ![](texture_s.png) | ![](texture_angle_s.png) |
|---|---|
| *Specular texture applied* | *Specular texture applied (another angle view)* |


##### Microfiber


[**Microfiber**](../../../../content/materials/library/mesh_base/index.md#texture_microfiber_channel) texture creates an effect of napped surface.


> **Notice:** To use this channel, enable the [Microfiber Map](#option_microfiber_map) state.


| ![](texture_f.png) | ![](texture_angle_f.png) |
|---|---|
| *Microfiber texture applied* | *Microfiber texture applied (another angle view)* |


### Detail Textures


An additional set of the textures to form a material layer. The set contains all the textures from Base textures group.


> **Notice:** Detail textures are available when a **[Detail](#option_detail)** option is enabled.


### Parallax Texture


An additional texture to form a parallax effect.


> **Notice:** Parallax texture is available when a **[Parallax](#option_parallax)** option is enabled.


### Emission Texture


An additional texture (3 channels) to store information about a glowing color.


> **Notice:** Emission texture is available when a **[Emission](#option_emission)** option is enabled.


### Auxiliary Texture


An additional texture (4 channels) to be used for custom post-effects, such as thermal vision, etc.


> **Notice:** Auxiliary texture is available when a **[Auxiliary](#option_auxiliary)** option is enabled.


## Parameters


All of the parameters have set default values, which can be replaced by your own ones. Availability of some parameters depends on the set *[States](#states)* field values.


### Transform


![](parameters_transform.png)

*Materials editor,Parameterstab.*


- **[Base](#textures_base)** - base material coordinates transformation.
- **[Detail](#textures_detail)** - detail material coordinates transformation.


### Base Parameters


![](parameters_shading.png)

*Parameterswindow.*


#### Albedo


**Albedo** is a multiplier of the base color of the surface provided by the [albedo texture](#texture_albedo).


![](shading_d.png)


#### Metalness


**Albedo** is a multiplier of metalness.


#### Roughness


**Roughness** is a multiplier of the roughness of a surface.


#### Specular


**Specular** is a multiplier for the intensity of highlight provided by the [specular texture](#texture_specular).


#### Microfiber


**Microfiber** is a coefficient to scale the intensity of the microfiber (provided by a [microfiber texture](#texture_microfiber)). The higher the value, the higher the microfiber texture effect is.


![](shading_f.png)


#### Normal Intensity


**Normal Intensity** is an intensity of the relief of the [normal texture](#texture_normal).


![](shading_n.png)


#### Translucency


**Translucent** parameter is a scale of the translucency effect, which permits light to pass through the object, but diffuses it so objects on the opposite side are not clearly visible.


#### UV Transform


Base textures [coordinates transformation](../../../../content/materials/library/mesh_base/index.md#texture_transform).


#### Material Mask


**Material mask** - a decal [bit-mask](../../../../principles/bit_masking/index.md). If the material mask of the decal material matches the surface material, the decal will be projected.


### Visibility Parameters


![](parameters_visibility.png)

*Materials editor,Parameterstab.*


Visibility parameters indicates the influence of different shading effects over the material on which the decal is projected.


#### Albedo Visibility


**Albedo Visibility** - a parameter that specifies the influence of the albedo of the decal over the surface material.


#### Metalness Visibility


**Metalness Visibility** - a parameter that specifies the influence of the metalness texture of the decal over surface material.


#### Roughness Visibility


**Roughness Visibility** - a parameter that specifies the influence of the roughness of the decal over the surface material.


#### Normal Visibility


**Normal Visibility** - a parameter that specifies the influence of the normal texture over the surface material.


### Emission Parameters


![](parameters_emission.png)

*Materials editor,Parameterstab.*


A set of the shading parameters for detail material textures:


#### Color


**Color** is a color picker to choose a color multiplier for the [emission texture](#textures_emission).


#### Scale


**Scale** is a coefficient to scale emission texture intensity. The higher the value, the lighter and brighter light areas of the emission texture are.


### Detail Textures Parameters


![](parameters_detail.png)

*Materials editor,Parameterstab.*


A set of the shading parameters for detail material textures:


#### Albedo


**Albedo** - is a multiplier of the detail color of the surface provided by the detail albedo texture similar to the base texture *Albedo* parameter.


#### Metalness


**Metalness** - a parameter modifying the size of the highlight of the detail texture similar to the base texture *Metalness* parameter.


#### Roughness


**Roughness** - a parameter modifying the size of the highlight of the detail texture similar to the base texture *Roughness* parameter.


#### Specular


**Specular** - is a color picker to choose the auxiliary specular color for the detail specular texture similar to the base texture *Specular* parameter.


#### Microfiber


**Microfiber** - is a color picker to choose the auxiliary microfiber color for the detail microfiber texture similar to the base texture *Microfiber* parameter.


#### Albedo Visibility


**Albedo Visible** - a parameter that specifies the influence of the detail texture albedo over the base texture albedo.


#### Metalness Visibility


**Metalness Visible** - a parameter that specifies the influence of the detail texture metalness over the base texture metalness.


#### Roughness Visibility


**Roughness Visible** - a parameter that specifies the influence of the detail texture roughness over the base texture roughness.


#### Specular Visibility


**Specular Visible** - a parameter that specifies the influence of the detail texture specular over the base texture specular.


#### Microfiber Visibility


**Microfiber Visible** - a parameter that specifies the influence of the detail microfiber texture over the base texture.


#### Normal Visibility


**Normal Visible** - a parameter that specifies the influence of the detail normal texture over the base texture.


> **Notice:** Detail parameters are present if a **[Detail](../../../../content/materials/library/mesh_base/index.md#option_detail)** option is enabled.


### Fade Parameters


![](parameters_fade.png)

*Materials editor,Parameterstab.*


#### Distance Threshold


**Distance Threshold** is a coefficient to scale a threshold fade for projected overlap materials. The higher the value, the bigger area is rendered.


| ![](fade_threshold_0.png) *Fade threshold =0* | ![](fade_threshold_1.png) *Fade threshold =1* | ![](fade_threshold_2.png) *Fade threshold =2* |
|---|---|---|


#### Distance Power


**Distance Power** a coefficient that shows the converse intensity of decal depending on the distance. The lower the power value, the bigger area is rendered.


| ![](fade_pow_0.png) *Fade power =0* | ![](fade_pow_1.png) *Fade power =1* | ![](fade_pow_2.png) *Fade power =2* |
|---|---|---|


#### Angle Threshold


**Angle threshold** is a threshold angle value. A coefficient to scale a threshold angle for projected overlap materials. The lower the value, the bigger area is rendered.


![](fade_angle_threshold.png)


#### Angle Power


**Angle Power** - Angle fade power, indicates the intensity depending on the angle.


![](fade_angle_power.png)


### Parallax Parameters


![](parameters_parallax.png)

*Parallax parameters*


#### Height


**Height** is a coefficient to scale the power of the [parallax texture](#textures_parallax) displacements. The higher the value, the bigger the normals are.


#### Min Layers


**Min layers** parameter specifies the minimum step of the parallax mapping.


#### Max Layers


**Max layers** parameter specifies the maximum step of the parallax mapping.


#### Noise


**Noise** parameter specifies the size of the noise used for parallax mapping. The higher the value, the less visible the layers.


#### Cutout UV Transform


**Cutout UV Transform** parameter specifies parallax texture coordinates transformation:

- **(X, Y)** - scale
- **(Z, W)** - offset.


### Parallax Shadow Parameters


![](parameters_parallax.png)

*Parallax Shadow parameters*


#### Min Layers


**Min layers** parameter specifies the minimum step of the parallax shadows.


#### Max Layers


**Max layers** parameter specifies the maximum step of the parallax shadows.


#### Noise


**Noise** parameter specifies the size of the noise used for parallax shadows. The higher the value, the less visible are the shadow layers.


#### Intensity


**Intensity** parameter specifies the intensity of shadows provided by the parallax effect.


#### Softness


**Softness** parameter specifies the softness of shadows provided by the parallax effect.


#### Visibility


**Visibility** parameter specifies the visibility scale for parallax shadows.


#### Visibility Angle


**Visibility Angle** parameter controls angle-dependent visibility for parallax shadows.


#### Visibility Angle Threshold


**Visibility Angle Threshold** parameter specifies a coefficient to scale a threshold angle for parallax shadows.


### Options


#### Auxiliary Color


![](auxiliary_params.png)

*Auxiliary color parameter*


**Auxiliary** color parameter specifies the constant color for the auxiliary pass. It is a multiplier for the [auxiliary texture](#textures_auxiliary).
