# XML Base Material File Format


## Base Material File Structure


A base material is a `*.basemat` ("Base Material") text file that contains all of the information to provide a required image. The base material is created by programmers and cannot be edited via [Parameters](../../../editor2/materials_settings/index.md) window: its properties can be adjusted and assets can be set only in the text file.


It is based on the `*.xml` file type and shares all its methods.


There are 3 basic entities of the `*.basemat` file:


- **Element.** A component that may contain attributes, other elements, some content etc.
- **Attribute.** A component placed inside the element tag containing the specified value.
- **Value.** A component specifying the value of the attribute.


The syntax is the following:


```xml
<parent_element attribute="value">
 <child_element_1/>
 <child_element_2>content</child_element_2>
</parent_element>

```


All of the `*.basemat` file elements, attributes and values are listed below.


> **Notice:** Unigine has the limit of **32767** material parameters.


## Base Material Element


A <base_material/> element defines a base material with the given properties (options, states, textures, parameters, shaders). Elements inside the <base_material/> element can be arrange freely (for example, you can specify parameters first and then add states).


It can have the attributes listed below.


### guid


A GUID for the base material.


The guid attribute is optional. The GUID for the base material will be generated from its file path in runtime, if the *guid* attribute isn't specified.


### parameters_prefix


The prefix added to all material parameters when they are passed to the shader.


### defines


The attribute that specifies names of definitions that will be passed to the shader.


### default


The attribute indicating that the material should be used as a default material for the [bound](#element_bind) nodes.


> **Warning:** Don't use this attribute for the user base materials.


### editable


A flag, indicating if all the base material settings can be changed in the [Parameters](../../../editor2/materials_settings/index.md) window or via [API](../../../api/library/rendering/class.material_cpp.md).


Available values:


- 0 � unchangeable (by default)
- 1 � changeable


You can set the flag to 1 in the following cases:


- When implementing a custom base material: you can adjust it via the *Parameters* window to achieve the desired result and then transfer the obtained values to the `*.basemat` file.
- When customizing an existing base material that is used for a specific effect (e.g., a postprocess material): instead of inheriting a user material that stores a couple of changed parameters, you can adjust the base material so one material corresponds to one effect.


> **Notice:** Despite the fact that the base material becomes editable, you cannot save changes made to it via the *Parameters* window.


### hidden


A flag, indicating if a material is displayed in the *[Materials Hierarchy](../../../editor2/materials_settings/organizing_materials/index.md)*.


Available values:


- 0 � displayed (by default)
- 1 � hidden


### options_hidden


A flag, indicating if the [Options](#element_options) section is displayed for the material in the Common tab.


Available values:


- 0 � displayed (by default)
- 1 � hidden


### preview_hidden


A flag, indicating if the material preview is displayed.


Available values:


- 0 � displayed (by default)
- 1 � hidden


### namespace


The material namespace.


> **Notice:** The Engine has its own reserved namespaces: *Unigine* and *Editor*.


### Usage Example


For example, to create the custom base material named custom_base, create a file `custom_base.basemat` and type:


```xml
<base_material parameters_prefix="m" editable="0">
...
</base_material>
```


## Blend Element


A <blend/> element allows you to set a [blending](../../../principles/render/blending/index.md) option value.


It can have the attributes listed below.


### src and dest


A polygon color (source image) and a screen buffer color (destination image) multipliers.


Available values for both attributes:


- none � blending is not used.
- zero � RGBA components of the source/destination image color are multiplied by zero.
- one � RGBA components of the source/destination image color are multiplied by one.
- src_color � RGBA components of the source/destination image color are multiplied by the mR, mG, mB, mA components (per component).
- one_minus_src_color � RGBA components of the source/destination image color are multiplied by the 1�- �mR , 1�- �mG , 1�- �mB , 1�- �mA  components (per component).
- src_alpha � RGBA components of the source/destination image color are multiplied by the mA component.
- one_minus_src_alpha � RGBA components of the source/destination image color are multiplied by the 1�- �mA  component.
- dest_color � RGBA components of the source/destination image color are multiplied by the bR, bG, bB, bA components (per component).
- one_minus_dest_color � RGBA components of the source/destination image color are multiplied by the 1�- �bR , 1�- �bG , 1�- �bB , 1�- �bA  components (per component).
- dest_alpha � RGBA components of the source/destination image color are multiplied by the bA component.
- one_minus_dest_alpha � RGBA components of the source/destination image color are multiplied by the 1�- �bA  component. Where mR, mG, mB, mA are normalized Red, Blue, Green and Alpha material image channels; bR, bG, bB, bA are normalized Red, Blue, Green and Alpha background image channels.


### Usage Example


For example, if you want the opaque areas to receive a material color and transparent areas to receive a screen buffer color, type:


```xml
<blend src="one" dest="one_minus_src_alpha"/>
```


### Material Settings


In the *Parameters* window, blending option value can be set in the **Transparency** section of the  [Common](../../../editor2/materials_settings/index.md#common_tab)  tab.


## Options Element


An <options/> element allows you to set a value for a common option.


It can have the attributes listed below.


### order


[Rendering order](../../../editor2/materials_settings/index.md#order) of the material. Specifies the priority of the material rendering.


Available values:


- -128 � 127. The default value is 0. The higher the rendering order, the lower the rendering priority (the material with the -128 order will be rendered first).


### shadow_mask


A [shadow mask](../../../editor2/materials_settings/index.md#shadow_mask) used to control shadows cast by an object lit by light sources.


Available values:


- Integer, representing a mask. The default value is ~0.


### viewport_mask


A [viewport mask](../../../editor2/materials_settings/index.md#viewport_mask).


Available values:


- Integer, representing a mask. The default value is ~0.


### transparent


A flag indicating whether the material is [transparent](../../../editor2/materials_settings/index.md#blending).


Available values:


- 0 � the material is opaque
- 1 � the *Alpha test* blending preset.
- 2 � the *Alpha blend*, *Additive*, *Multiplicative* or *Custom* blending preset.


### depth_mask


A flag indicating if writing in the [depth buffer](../../../editor2/materials_settings/index.md#depth_write) is enabled for a material.


Available values:


- 0 � not used
- 1 � used (by default)


### depth_pre_pass


A flag indicating if the [native depth pre-pass](../../../principles/render/sequence/index.md#depth_pre_pass) is performed for a material.


Available values:


- 0 � is performed
- 1 � not performed


### transparent_order


The [Transparent Order](../../../editor2/materials_settings/index.md#transparent_order) option of a material.


Available values:


- 0 � Before SSR (by default)
- 1 � Before Post
- 2 � After Post


### two_sided


A flag indicating if a [Two Sided](../../../editor2/materials_settings/index.md#two_sided) option is enabled for a material.


Available values:


- 0 � disabled (by default)
- 1 � enabled


### depth_test


A flag indicating if a [Depth Test](../../../editor2/materials_settings/index.md#depth_test) option is enabled for a material.


Available values:


- 0 � disabled
- 1 � enabled (by default)


### cast_shadow


A flag indicating if a [Cast Proj and Omni Shadow](../../../editor2/materials_settings/index.md#cast_shadow) option is enabled for a material.


Available values:


- 0 � disabled
- 1 � enabled (by default)


### cast_world_shadow


A flag indicating if a [Cast World shadow](../../../editor2/materials_settings/index.md#cast_world_shadow) option is enabled for a material.


Available values:


- 0 � disabled
- 1 � enabled (by default)


### Usage Example


For example, to enable an Alpha test option, type:


```xml
<options alpha_test="1"/>
```


### Material Settings


In the *Parameters* window, a common option value can be set in the **Options** section of the  [Common](../../../editor2/materials_settings/index.md#common_tab)  tab.


## Group Element


A <group/> element specifies the group which states, textures or parameters of the base material belong to. The element is optional: states, textures or parameters can be defined out of it. You can also specify the *group* attribute for the *<state/>*,*<texture/>* or *<parameter/>* element instead of using the *<group/>* element.


### name


Name of the group.


### Usage Example


For example, some states of the *mesh_base* material can be grouped as follows:


```xml
<base_material name="mesh_base" editable="0" parameters_prefix="m" defines="VERTEX_ATTRIBUTE_GEOMETRY">
	<group name="Default">
		<state name="workflow" items="metalness,specular" defines="items"/>
		<state name="deferred" title="Deferred Buffers" tooltip="Deferred buffers rendering">1</state>
		<state name="multiple_environment_probes" transparent="2" defines="name">0</state>
	</group>
</base_material>

```


Or the *[group](#state_group)* attribute can be used instead of the corresponding element:


```xml
<base_material name="mesh_base" editable="0" parameters_prefix="m" defines="VERTEX_ATTRIBUTE_GEOMETRY">
	<state name="workflow" items="metalness,specular" defines="items" group="Default"/>
	<state name="deferred" title="Deferred Buffers" group="Default">1</state>
	<state name="multiple_environment_probes" transparent="2" defines="name" group="Default">0</state>
</base_material>

```


## State Element


A <state/> element allows you to set a mode for rendering passes and a value for rendering options. The states change a set of definitions passed to shaders, so any changes made to a state cause recompiling shaders.


### name


Name of the state.


Below are some of the values available:


- terrain_lerp � Replace material's albedo texture by the projected albedo texture of the ObjectTerrainGlobal to ensure smooth blending with the terrain. Used in the [mesh_base](../../../content/materials/library/mesh_base/index.md#terrain_lerp) material.
- use_taa � Enable [Temporal Anti-Aliasing](../../../principles/render/antialiasing/taa.md) for the post material. Enabling this state has an impact on performance, as TAA in this case is applied twice (stage of the [rendering sequence](../../../principles/render/sequence/index.md) plus for the post material).


### hidden


A flag indicating whether the state is hidden in the *[Materials Hierarchy](../../../editor2/materials_settings/organizing_materials/index.md)*


### type


A type of the the state value.


Available values:


- **toggle** - switch that enables/disables the state
- **switch** - multiple values switch
- **int** - integer value


### items


A set of available items for a multiple values **[switch](#switch)**.


### switch_group


A flag indicating that this state is a switch enabling or disabling a [group](#element_group).


```xml
<state name="additional_mask" switch_group="Additional mask"/>

```


### defines


The attribute that specifies names of definitions that will be passed to the shader:


| name | A name specified via *[name](#state_name)*. ```xml <state name="vertex_color" defines="name"/> ``` In the example above the following definition will be passed to the shader: VERTEX_COLOR. |
|---|---|
| items | A set of multiple values specified via *[items](#state_items) (in the upper case)*. ```xml <state name="workflow" items="metalness,specular" defines="items"/> ``` In the example above the following definitions will be passed to the shader: METALNESS and SPECULAR. |
| name_items | A name specified via *[name](#state_name)* followed by a set of multiple values specified via *[items](#state_items)*. ```xml <state name="opacity_map" transparent="1,2" items="main,normal" defines="name_items"/> ``` In the example above the following definitions will be passed to the shader: OPACITY_MAP_MAIN and OPACITY_MAP_NORMAL. |


### pass_defines


The attribute that specifies passes to which the [definitions](#state_defines) will be passed.


| Pass name | Description |
|---|---|
| **all** | Specifies if the material is rendered during all the passes. |
| **deferred** | Specifies if the material is rendered into the deferred buffer during the deferred rendering pass (i.e. all passes for opaque geometry). |
| **forward** | Specifies if the material is rendered during the forward rendering pass including [environment probe light](#pass_light_environment_probe), [omni light](#pass_light_omni), [projected light](#pass_light_proj), [world light](#pass_light_world) and [ambient](#pass_ambient) passes. |
| **depth_pre_pass** | Specifies if the material is rendered into the depth buffer during the native depth pre-pass. |
| **auxiliary** | Specifies if the material is rendered into the auxiliary buffer during the auxiliary rendering pass. |
| **efraction** | Specifies if the material is rendered into the refractions buffer during the refraction rendering pass. |
| **velocity** | Specifies if the material is rendered during the velocity pass. |
| **ambient** | Specifies if the ambient light is rendered for the material during the ambient pass. |
| **emission** | Specifies if the material is rendered during the emission rendering pass. |
| **light_omni** | Specifies if the material is rendered illuminated by the [omnidirectional light sources](../../../objects/lights/omni/index.md) during the omni light pass. |
| **light_proj** | Specifies if the material is rendered illuminated by the [projected light sources](../../../objects/lights/proj/index.md) during the projected light pass. |
| **light_world** | Specifies if the material is rendered illuminated by the [world light sources](../../../objects/lights/world/index.md) during the world light pass. |
| **light_environment_probe** | Specifies if the material is rendered illuminated by the [environment probes](../../../objects/lights/envprobe/index.md) during the corresponding rendering pass. |
| **light_voxel_probe** | Specifies if the material is rendered illuminated by the [voxel probes](../../../objects/lights/voxelprobe/index.md) during the corresponding rendering pass. |
| **light_all** | Specifies if the material is rendered illuminated by the all lights in the scene during the [environment probe light](#pass_light_environment_probe), [omni light](#pass_light_omni), [projected light](#pass_light_proj), [world light](#pass_light_world) passes. |
| **shadow** | Specifies if the material is rendered during the shadows rendering pass. |
| **transparent** | Specifies if the material is rendered during the [forward](#pass_forward), [refraction](#pass_refraction) and [transparent blur](#pass_transparent_blur) passes. |
| **wireframe** | Specifies if the material is rendered during the wireframe pass. |
| **visualizer_solid** | Specifies if the material is rendered during the visualizer solid pass. |
| **reflection** | Specifies if the material is rendered during the reflection pass. |
| **transparent_blur** | Specifies if the transparent blur effect is used for the material rendered during the transparent blur pass. This effect allows creating a matte transparent materials. |
| **post** | Specifies if the material is rendered during the post materials rendering pass. |
| ***Custom Pass*** | Name of the custom rendering pass. Up to 32 custom passes are supported. |


### title


A state title that will be displayed in the editor.


### tooltip


A tooltip for a state. The tooltip will be displayed in the editor when the state is pointed with the mouse.


### group


A group which a state belongs to. The attribute can be used instead the [group](#element_group) element.


### widget


A type of the widget reqiured to set a state value.


### internal


A flag indicating if the state is internal (i.e. cannot be changed via UnigineEditor but used by internal logic). The child materials don't inherit internal states, so callbacks on these states aren't fired for them.


Available values:


- 0 � not internal (by default)
- 1 � internal


### State Conditions


A state can have a [condition](#conditions) specified as an attribute. For example, the following state will be displayed when the [transparent](#transparent) option is set to *Opaque* or *Alpha test* and the *Parallax* state is enabled:


```xml
<state name="parallax_depth_cutout" parallax="1" transparent="0,1"/>

```


### Usage Example


For example, if you want to specify the deferred pass, enabled by default, type:


```xml
<state name="deferred" type="switch" items="none,default">1</state>
```


> **Notice:** Do not forget to specify a [shader](#element_shader) for the pass.


## Texture Element


A <texture/> element allows you to specify a texture to be used.


### name


Texture name.


### pass


A pass during which a texture will be rendered.


Available values:


- wireframe � the wireframe pass
- visualizer_solid � the visualizer solid pass
- deferred � the deferred pass
- auxiliary � the auxiliary pass
- emission � the emission pass
- refraction � the refraction pass
- reflection � the reflection pass
- transparent_blur � the transparent blur pass
- ambient � the ambient pass
- light_environment_probe � the environment probe pass
- light_omni � the omni-directional light pass
- light_proj � the projected light pass
- light_world � the world light pass
- light_all � the [environment probe](#texture_pass_light_environment_probe), [omni-directional light](#texture_pass_light_omni), [projected light](#texture_pass_light_proj), [world light](#texture_pass_light_world) passes
- depth_pre_pass � the native depth pre-pass
- shadow � the shadows pass
- post � the post-process pass
- forward � the [environment probe](#texture_pass_light_environment_probe), [omni-directional light](#texture_pass_light_omni), [projected light](#texture_pass_light_proj), [world light](#texture_pass_light_world) and [ambient](#texture_pass_ambient) passes
- transparent � the [forward](#texture_pass_forward), [refraction](#texture_pass_refraction), [transparent blur](#texture_pass_transparent_blur) passes


### source


A type of the texture.


Available values:


- image - standard texture image (by default).
- gbuffer_albedo - texture that uses the G-buffer to store albedo values.
- gbuffer_shading - texture that uses the G-buffer to store shading data.
- gbuffer_normal - texture that uses the G-buffer to store normal values.
- gbuffer_velocity - texture that uses the G-buffer to store velocity values.
- gbuffer_material_mask - texture that uses the G-buffer to store material mask data.
- gbuffer_lightmap - texture that uses the G-buffer to store lightmap values.
- gbuffer_geodetic_flat_position - texture that uses the G-buffer to store flat plane coordinates.
- auxiliary - auxiliary texture that is used for different post effects (an auxiliary pass).
- refraction - texture that stores refraction data.
- transparent_blur - 1-channel **R16F** mask that stores intensity of blurring for transparent materials. The mask specifies where to blur the material.
- lights - 2D array texture of the **RG11B10F** format that stores diffuse light in the first layer (RGB) and specular light in the second layer (RGB).
- environment_probes - 2D array texture of the **RGBA16F** format that stores reflections in the first layer (RGBA) and ambient lights in the second layer (RGBA).
- bent_normal - RG11B10F texture that stores bent normals (RGB) used for smooth ambient lighting.
- ssao - texture that stores SSAO (Screen Space Ambient Occlusion) data.
- ssgi - texture that stores SSGI (Screen Space Global Illumination) data.
- ssr - texture that stores SSR (Screen Space Reflections) data.
- ssr_depth - texture that stores SSR (Screen Space Reflections) depth data.
- dof_mask - texture that stores a DoF (Depth of Field) mask.
- auto_exposure - **RG16F** texture that stores intensity of the exposure (R) and luminance (G).
- screen_color - texture that stores screen color data and can be used for post effects.
- screen_color_old - texture that stores Color Old (previous frame) data.
- screen_color_old_reprojection - texture that stores Color Old (previous frame) Reprojection data.
- normal_unpack - texture that stores unpacked normals. Available for the following post-effects: SSR, SSGI, SSRTGI, Shadows screen space.
- current_depth - texture that stores current depth data for all geometry on the scene.
- opacity_depth - texture that stores depth data for opacity geometry and can be used for soft particles and volumetrics.
- linear_depth - texture that stores linear depth data.
- opacity_screen - texture that stores the deferred composite and emission data.
- light_image - texture storing the light values provided by projected light sources.
- light_shadow_depth - texture storing depth values (used to render shadows).
- light_shadow_color - texture used to render translucent shadows: G-channel stores depth values, R-channel - transparency values.
- transparent_environment_probes - texture that stores environment probes rendered on transparent objects. Available only when [Multiple environment probes](../../../principles/render/sequence/index.md#transparent_multiple_env_probe_on) are enabled.
- reflection_2d - texture storing reflection values (used to render 2D reflections).
- reflection_cube - texture storing reflection values (used to render cube-mapped reflections).
- scattering_sky_lut - texture that stores sky scattering LUT data.
- scattering_ground_lut - texture that stores ground scattering LUT data.
- wbuffer_constant_id - [constant texture](../../../principles/render/sequence/index.md#wbuffer_constant), **R32U**. A texture of this type stores the ID value of the water mesh which is used to load the corresponding textures and parameters for it.
- wbuffer_diffuse - [diffuse texture](../../../principles/render/sequence/index.md#wbuffer_diffuse). The diffuse color of the water is black, and diffuse texture is necessary for decals, that will be displayed over the water surface
- wbuffer_normal - [normal texture](../../../principles/render/sequence/index.md#wbuffer_normal) stores normal data for lighting, and alpha channel stores mesh transparency values (it can be used for soft intersections with water geometry)
- wbuffer_water - [water texture](../../../principles/render/sequence/index.md#wbuffer_water), **RG8**. It is used to create the procedural foam mask. The mask shows where the foam will be depicted
- wbuffer_wu_mask - [underwater mask texture](../../../principles/render/sequence/index.md#wbuffer_underwater_mask), **RGB8**. The underwater mask is used only for [Global water](../../../objects/objects/water/water_object.md), since [water mesh](../../../objects/objects/water/water_mesh.md) doesn't have an underwater mode
- wbuffer_ss_environment - **RGBA16** [underwater fog texture](../../../principles/render/sequence/index.md#wbuffer_underwater_fog) that stores water bottom coloring values (RGB) and fog transparency (A).
- clouds_screen - **RGBA16F** texture into which clouds are rendered.
- clouds_static_coverage - texture that stores clouds static coverage data.
- clouds_dynamic_coverage - texture that stores clouds dynamic coverage data.
- field_height_array - heightmap texture that is used to create an additional height displacement for water surface.
- field_shoreline_array - field shoreline texture.
- decal_depth - texture that stores depth data for decals.
- decal_albedo - texture that stores albedo color data for decals.
- decal_normal - texture that stores normal data for decals.
- decal_shading -a texture that stores shading data for decals.
- procedural - procedurally generated texture.
- filter - filtering texture.


### unit


A number of the Texture Mapping Unit (slot) to be used for the texture. The unit specifies a slot of a shader, to which the texture will be passed. The maximum available number of units is 32, the first 16 units supports filtering. If the unit is greater or equal 16, no filtering will be used for the texture.


### format


A texture format.


Available values:


- srgb � standard RGB color model format.
- signed � signed normalized format.
- integer � integer normalized format.


### wrap


A texture wrapping methods.


Available values:


- clamp � texture is clamped along all axes
- clamp_x � texture is clamped along X-axis
- clamp_y � texture is clamped along Y-axis
- clamp_z � texture is clamped along Z-axis
- border � texture is bordered along all axes
- border_x � texture is bordered along X-axis
- border_y � texture is bordered along Y-axis
- border_z � texture is bordered along Z-axis
- repeat � no wrap, a texture is tiled along all axes.


### anisotropy


A flag, indicating if the anisotropy for the texture is enabled.


Available values:


- 0  �- �disabled (by default)
- 1  �- �enabled


### filter


A type of the texture filtering.


Available values:


- point  � � point filtering (when enablled, disables anisotropy filtering) �
- linear  � � linear filtering �
- bilinear  � � bilinear filtering �


### title


A texture title that will be displayed in the editor.


### group


A group which a texture belongs to. The attribute is optional: you can use the *[group](#element_group)* element instead.


### widget


A type of the widget reqiured to set a parameter.


### tooltip


A tooltip for a texture. The tooltip will be displayed in the editor when the texture field is pointed with the mouse.


### hidden


A flag indicating whether the texture is displayed in UnigineEditor.


### shader


A shader type to which the texture is binded to.


Available values:


- all - texture should be bound to all shaders.
- fragment - texture should be bound to fragment shaders only (by default).


### materials


A list of post-process materials to be used.


### force_streaming


A flag indicating if a texture is uploaded immediately.


Available values:


- 0 � disabled (by default).
- 1 � enabled.


### Texture Conditions


A texture can have a [condition](#conditions) specified as an attribute. For example, the following texture will be displayed when the [transparent](#transparent) option is set to *Opaque* or *Alpha test* and the *Parallax* state is enabled:


```xml
<texture name="parallax"	parallax="1" transparent="0,1">core/textures/common/red.texture</texture>

```


## Parameter Definition


The parameter is defined using one of the following type-specific tags:


- <float/>
- <float2/>
- <float3/>
- <float4/>
- <int/>
- <int2/>
- <int3/>
- <int4/>
- [<combiner/>](#parameter_combine)


Type aliases can also be used to define a parameter of a certain type with the corresponding widget:


- **mask24** (type = *int*, widget = *mask24*)
- **mask32** (type = *int*, widget = *mask32*)
- **uv** (type = *float4*, widget = *uv*)
- **color**(type = *float4*, widget = *color*)
- **slider**(type = *float*, widget = *slider*)


### expression


A flag indicating if the parameter is controlled via [expression](#element_expression) (UnigineScript).


Available values:


- 0 � not controlled via expression (by default).
- 1 � controlled via expression.


### name


Name of the parameter.


### title


A parameter title that will be displayed in the UnigineEditor.


### tooltip


A tooltip for a parameter. The tooltip will be displayed in the UnigineEditor when the parameter field is pointed with the mouse.


### group


A group which a parameter belongs to. The attribute is optional: you can use the *[group](#element_group)* element instead.


### Combiner Parameters


For the parameter of the *combiner* type the names of the combined parameters are used as attributes that specify *combiner masks*. Available values:


- **XYZW** � all values of the parameter are taken into account when combining with the other parameters.
- **XYZ** � the 4th component of the parameter isn't taken into account.
- **X** � only the 1st component of the parameter is taken into account.
- **Y** � only th 2nd component of the parameter is taken into account.
- **Z** � only the 3rd component of the parameter is taken into account.
- **W** � only th 4th component of the parameter is taken into account.


### pass


A pass during which a parameter will be used.


Available values:


- wireframe � the wireframe pass
- visualizer_solid � the visualizer solid pass
- deferred � the deferred pass
- auxiliary � the auxiliary pass
- emission � the emission pass
- refraction � the refraction pass
- reflection � the reflection pass
- transparent_blur � the transparent blur pass
- ambient � the ambient pass
- light_environment_probe � the environment probe pass
- light_voxel_probe � the voxel probe pass
- light_omni � the omni-directional light pass
- light_proj � the projected light pass
- light_world � the world light pass
- light_all � the [environment probe](#parameter_pass_light_environment_probe), [omni-directional light](#parameter_pass_light_omni), [projected light](#parameter_pass_light_proj), [world light](#parameter_pass_light_world) passes
- depth_pre_pass � the native depth pre-pass
- shadow � the shadows pass
- post � the post-process pass
- forward � the [environment probe](#parameter_pass_light_environment_probe), [omni-directional light](#parameter_pass_light_omni), [projected light](#parameter_pass_light_proj), [world light](#parameter_pass_light_world) and [ambient](#parameter_pass_ambient) passes
- transparent � the [forward](#parameter_pass_forward), [refraction](#parameter_pass_refraction), [transparent blur](#parameter_pass_transparent_blur) passes
- custom_pass_name � name of a custom rendering pass. Up to 32 custom passes are supported.


### shared


A flag indicating if the parameter will be exported to the shader.


Available values:


- 0 � parameter is not exported
- 1 � parameter is exported (by default)


### internal


A flag indicating if the parameter is internal (i.e. cannot be changed via UnigineEditor but used by internal logic).


Available values:


- 0 � not internal (by default)
- 1 � internal


### hidden


A flag indicating if the parameter is hidden in UnigineEditor.


Available values:


- 0 � not hidden(by default)
- 1 � hidden


### min and max


[Minimum](../../../api/library/rendering/class.material_cpp.md#getUIItemSliderMinValue_int_float) and [maximum](../../../api/library/rendering/class.material_cpp.md#getUIItemSliderMaxValue_int_float) available values of the parameter.


### deferred_unit


A number of deferred units to be used.


### shader_name


A name of a shader to which the parameter value is passed. If the *[prefix](#parameter_prefix)* or *[parameters_prefix](#base_material_parameters_prefix)* attribute is specified, it will be used as a prefix for the shader name.


### prefix


A prefix for a name of a shader to which the parameter value is passed.


### expand


A flag indicating if the specified maximum and minimum values of the parameter can be exceeded.


Available values:


- 0 � disabled
- 1 � enabled


### min_expand


A flag indicating if the specified minimum value of the parameter can be decreased.


Available values:


- 0 � disabled
- 1 � enabled


### max_expand


A flag indicating if the specified maximum value of the parameter can be increased.


Available values:


- 0 � disabled
- 1 � enabled


### widget


A type of the widget reqiured to set a parameter value.


Available values:


- **mask24** - widget that allows specifying a 24-bit mask
- **mask32** - widget that allows specifying a 32-bit mask
- **uv** - widget that allows specifying a UV coordinates
- **vec** - widget that allows specifying vector elements
- **color** - widget that allows picking a color
- **slider** - widget that allows selecting float values from a continuous range of allowed values.


### Parameter Conditions


A parameter can have a [condition](#conditions) specified as an attribute. For example, the following parameter will be displayed when the *Auxiliary* state is enabled:


```xml
<color name="auxiliary_color" auxiliary="1"></color>

```


### Usage Example


An example of different types of parameters declaration:


```xml
<float4 name="expression_parameter" expression="1" shared="1">vec4(1.0f,1.0f,0.0f,0.0f)</float4>
<slider name="slider_parameter" shared="1" min="0.0" max="4.0" max_expand="1">1.0</slider>
<color name="color_parameter" shared="1">1.0 1.0 1.0 1.0</color>


```


## Expression Element


An <expression/> element specifies a fragment of code written in UnigineScript and stored in a separate `*.usc` file, that can generate various elements used in the material (e.g., textures, texture arrays, unstructured buffers, etc.) or contain other logic.


### name


Name of the expression. The name must be unique as it is used when executing the expression via the [*runExpression()*](../../../api/library/rendering/class.material_cpp.md#runExpression_cstr_int_int_int_int) function of the Material class.

> **Notice:** If the value of this attribute is a name of a [render callback](../../../api/library/rendering/class.render_cpp.md#getEventBegin_Event) (e.g. *CALLBACK_BEGIN_SSAO*), the expression code of the `*.usc` file specified by the [**path**](#expression_path) attribute will be executed automatically at the corresponding stage of the [rendering sequence](../../../principles/render/sequence/index.md). Materials containing such expressions are called [scriptable](../../../content/materials/scriptable.md).


### path


Path to the `*.usc` file containing expression code written in UnigineScript.


### Usage Example


An example of expression declaration:


```xml
<!--...-->
<expression name="expr_name" path="expression.usc"/>

```


An example of expression code:


```cpp
// typical most frequently used parameters passed to the expression when it is called.
int in_width;
int in_height;
int in_depth;
Material in_material;
// If you need extra parameters, you should set them via Material::setParameter*("param_name", value) before calling Material::runExpression()
// then you can access them in the expression via in_material.getParameter*("param_name")

// ...

// get a temporary texture
Texture texture = engine.render.getTemporaryTexture(in_width, in_height);

// modify the temporary texture

// set the modified texture as albedo texture of the material
in_material->setTexture("albedo", texture);


```


## Shader Element


A <shader/> element allows you to specify vertex, fragment and geometry shaders to be used for the described pass.


> **Notice:** You can use HLSL shading language to write shaders.


### pass


A pass for the shader to be applied.


Available values:


- wireframe � the wireframe pass
- visualizer_solid � the visualizer solid pass
- deferred � the deferred pass
- auxiliary � the auxiliary pass
- emission � the emission pass
- refraction � the refraction pass
- reflection � the reflection pass
- transparent_blur � the transparent blur pass
- ambient � the ambient pass
- light_environment_probe � the environment probe light pass
- light_voxel_probe � the voxel probe light pass
- light_omni � the omni-directional light pass
- light_proj � the projected light pass
- light_world � the world light pass
- depth_pre_pass � the native depth pre-pass
- shadow � the shadows pass
- post � the post-process pass
- custom_pass_name � name of a custom rendering pass. Up to 32 custom passes are supported.


### node


An object or a decal to which a shader will be applied.


Available values:


- [object_dynamic](../../../api/library/objects/class.objectdynamic_cpp.md)  - dynamic object
- [object_mesh_static](../../../api/library/objects/class.objectmeshstatic_cpp.md)  - static mesh
- [object_mesh_cluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)  - mesh cluster
- [object_mesh_clutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)  - mesh clutter
- [object_mesh_skinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)  - skinned mesh
- [object_mesh_dynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)  - dynamic mesh
- [object_landscape_terrain](../../../api/library/objects/landscape_terrain/index.md)  - landscape terrain object
- [object_terrain_global](../../../api/library/objects/class.objectterrainglobal_cpp.md)  - global terrain object
- [object_grass](../../../api/library/objects/class.objectgrass_cpp.md)  - grass object
- [object_particles](../../../api/library/objects/class.objectparticles_cpp.md)  � particles
- [object_billboards](../../../api/library/objects/class.objectbillboards_cpp.md)  � billboards
- [object_volume_box](../../../api/library/objects/class.objectvolumebox_cpp.md)  - volume box
- [object_volume_sphere](../../../api/library/objects/class.objectvolumesphere_cpp.md)  - volume sphere
- [object_volume_omni](../../../api/library/objects/class.objectvolumeomni_cpp.md)  - volume omni object
- [object_volume_proj](../../../api/library/objects/class.objectvolumeproj_cpp.md)  - volume projected object
- [object_gui](../../../api/library/objects/class.objectgui_cpp.md)  - GUI object
- [object_gui_mesh](../../../api/library/objects/class.objectguimesh_cpp.md)  - GUI mesh
- [object_water_global](../../../api/library/objects/class.objectwaterglobal_cpp.md)  - global water object
- [object_water_mesh](../../../api/library/objects/class.objectwatermesh_cpp.md)  - water mesh
- [object_sky](../../../api/library/objects/class.objectsky_cpp.md)  - sky object
- [object_clouds](../../../api/library/objects/class.objectcloudlayer_cpp.md)  - clouds object
- [object_extern](../../../api/library/objects/class.objectextern_cpp.md)  - external object
- [object_text](../../../api/library/objects/class.objecttext_cpp.md)  - text object
- [decal_proj](../../../api/library/decals/class.decalproj_cpp.md)  - projected decal
- [decal_ortho](../../../api/library/decals/class.decalortho_cpp.md)  - orthograhic decal
- [decal_mesh](../../../api/library/decals/class.decalmesh_cpp.md)  - mesh decal


### defines


A list of the shader definitions to be used.


> **Notice:** An example of a defines attribute usage is shown in the [Custom Materials](../../../content/materials/custom.md) article.


### *_defines


#### Options Definitions


A list of the [option-specific](#element_options) definitions to be passed to the shader.


A name of such attribute is constructed as follows:

<option_name> + _defines
For example, to specify transparency-related definitions, use the *transparent_defines* attribute. If the *[two_sided](#two_sided)* flag is set for the material, specify the *two_sided_defines* attribute.


#### States Definitions


A list of the [state-specific](#element_state) definitions to be passed to the shader.


A name of such attribute is constructed as follows:

<state_name> + _defines
For example, to specify transparency-related definitions, use the *transparent_defines* attribute. If the *[two_sided](#two_sided)* flag is set for the material, specify the *two_sided_defines* attribute.


> **Notice:** An example of the *_defines attributes usage is shown in the [Custom Materials](../../../content/materials/custom.md) article.


### vertex


A path to a `*.vert` vertex shader to be used. If the vertex shader isn't specified, the default `core/shaders/common/empty.vert` shader will be used.


### control


A path to a `*.cont` control shader (also known as hull) to be used.


### evaluate


A path to `*.eval` evaluation shader (also known as domain) to be used.


### geometry


A path to a `*.geom` geometry shader to be used.


### fragment


A path to a `*.frag` fragment shader to be used.


### compute


A path to a `*.comp` compute shader to be used.


### Shader Conditions


A shader can have a [condition](#conditions) specified as an attribute. For example, the following shader will be applied when the *Auxiliary* state is enabled:


```xml
<shader pass="auxiliary" node="object_mesh_static"
		auxiliary="1"
		defines="BASE_AUXILIARY"
		two_sided_defines=",TWO_SIDED"
		vertex="core/shaders/mesh/auxiliary/auxiliary.shader"
		fragment="core/shaders/mesh/auxiliary/auxiliary.shader"/>

```


### Usage Example


An example of the ambient pass shader, applied to the dynamic mesh:


```xml
<shader pass="ambient" node="object_mesh_dynamic"
	vertex="shaders/vertex.shader"
	geometry="shaders/geometry.shader"
	fragment="shaders/fragment.shader"/>

```


## Bind Element


Each <shader/> element specifies an [node](#shader_node) to which the shader will be applied, so if, for example, you have shaders for the mesh object, the material could not be applied to the clutter object. A <bind/> element allows you to apply shaders written for one type of nodes to another types of nodes, so you can just bind a clutter object to the mesh for the shader to be applied for it.


### node


A node to be binded.


Available values:


- [object_dynamic](../../../api/library/objects/class.objectdynamic_cpp.md)  - dynamic object
- [object_mesh_static](../../../api/library/objects/class.objectmeshstatic_cpp.md)  - static mesh
- [object_mesh_cluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)  - mesh cluster
- [object_mesh_clutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)  - mesh clutter
- [object_mesh_skinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)  - skinned mesh
- [object_mesh_dynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)  - dynamic mesh
- [object_landscape_terrain](../../../api/library/objects/landscape_terrain/index.md)  - landscape terrain object
- [object_terrain_global](../../../api/library/objects/class.objectterrainglobal_cpp.md)  - global terrain object
- [object_grass](../../../api/library/objects/class.objectgrass_cpp.md)  - grass object
- [object_particles](../../../api/library/objects/class.objectparticles_cpp.md)  � particles
- [object_billboards](../../../api/library/objects/class.objectbillboards_cpp.md)  � billboards
- [object_volume_box](../../../api/library/objects/class.objectvolumebox_cpp.md)  - volume box
- [object_volume_sphere](../../../api/library/objects/class.objectvolumesphere_cpp.md)  - volume sphere
- [object_volume_omni](../../../api/library/objects/class.objectvolumeomni_cpp.md)  - volume omni object
- [object_volume_proj](../../../api/library/objects/class.objectvolumeproj_cpp.md)  - volume projected object
- [object_gui](../../../api/library/objects/class.objectgui_cpp.md)  - GUI object
- [object_gui_mesh](../../../api/library/objects/class.objectguimesh_cpp.md)  - GUI mesh
- [object_water_global](../../../api/library/objects/class.objectwaterglobal_cpp.md)  - global water object
- [object_water_mesh](../../../api/library/objects/class.objectwatermesh_cpp.md)  - water mesh
- [object_sky](../../../api/library/objects/class.objectsky_cpp.md)  - sky object
- [object_clouds](../../../api/library/objects/class.objectcloudlayer_cpp.md)  - clouds object
- [object_extern](../../../api/library/objects/class.objectextern_cpp.md)  - external object
- [object_text](../../../api/library/objects/class.objecttext_cpp.md)  - text object
- [decal_proj](../../../api/library/decals/class.decalproj_cpp.md)  - projected decal
- [decal_ortho](../../../api/library/decals/class.decalortho_cpp.md)  - orthograhic decal
- [decal_mesh](../../../api/library/decals/class.decalmesh_cpp.md)  - mesh decal


### to


A node to bind.


Available values are the same as for [node](#bind_node) attribute.


### defines


A list of the definitions to be used if the material is binded.


### Usage Example


An example of binding a mesh skinned object to a mesh object (with the mesh skinned definition):


```xml
<bind object="mesh_skinned" to="mesh" defines="MESH_SKINNED"></bind>
```


## Base Material Conditions


A **condition** specifies when the state, texture, parameter or shader is displayed in UnigineEditor. The condition is an attribute of the [state](#element_state), [texture](#element_texture), [parameter](#element_parameter) or [shader](#element_shader) element. The following conditions are available:


- **transparent** � the element will be displayed when the [transparent](#transparent) option is set to the specified value. For example, the Multiple Environment Probes state will be displayed only when the *transparent* option is set to 2 (the *Alpha blend*, *Additive*, *Multiplicative* or *Custom* blending preset is used): ```xml <state name="multiple_environment_probes" transparent="2" defines="name">0</state> ```
- An option specified in the *[options](#element_options)* element, except the following: *[order](#order)*, *[shadow_mask](#shadow_mask)*, *[viewport_mask](#viewport_mask)*.
- A [state name](#state_name). For example, the *auxiliary_color* parameter will be displayed only if the *Auxiliary* state is enabled: ```xml <color name="auxiliary_color" auxiliary="1">1.0 1.0 1.0 1.0</color> ```


> **Notice:** The order of conditions declaration and usage doesn't matter: you can specify a condition for an element before this condition is declared in the `*.basemat` file.
