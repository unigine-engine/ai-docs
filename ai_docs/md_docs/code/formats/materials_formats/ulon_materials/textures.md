# Textures


The material texture is an image that maps to object's surfaces to provide color details and more.


The syntax is the following:


```cpp
Texture[Dimension] name = "directory/name.format"  <attributes>

```


> **Notice:** If the name of the texture is not specified, then the name will be equal to the texture source type. The following declarations are equal:
> ```cpp
> Texture <source="gbuffer_normal" unit=0>
> Texture gbuffer_normal <source="gbuffer_normal" unit=0>
>
> ```


## Types of Textures


- **Texture** (or **Texture2D**) � a two-dimensional (2D) [texture](../../../../api/library/rendering/class.texture_cpp.md) image where each element is a float
- **TextureRamp** � 2D curves in a form of a ramp texture
- **Texture2DArray** � a homogeneous array of 2D textures where each texture has the same data format, filtering type, and dimensions (including mipmap levels)
- **Texture2DUint** � a two-dimensional texture image where each element is an *unsigned int*
- **Texture2DInt** � a two-dimensional texture image where each element is an *int*
- **Texture3D** � is a volume texture that contains 3D texels
- **TextureCube** � an array of 2D textures with 6 elements for each face of the cube
- **TextureCubeArray** � an array of *[TextureCube](#texturecube)*


## Usage Examples


```cpp
BaseMaterial
{
	Texture diffuse = "core/textures/common/white.texture" <unit=0 auto_init=true>
}

```


```glsl
float4 texture_color = TEXTURE(tex_diffuse, IN_UV);

```


If *auto_init* is set to true, the texture will be declared automatically in the shader the following way:


```glsl
INIT_TEXTURE(0, tex_diffuse)

```


The texture can now be accessed in the shader via the **tex_diffuse** name. You don�t need to initialize it separately.


The engine has some default textures. You can use shortcuts to reference them (instead of specifying the full path).


| Shortcut | Full directory path |
|---|---|
| white | core/textures/common/white.texture |
| black | core/textures/common/black.texture |
| noise | core/textures/common/noise.texture |
| normal | core/textures/common/normal.texture |
| red | core/textures/common/red.texture |
| grain | core/textures/common/grain.texture |
| cube_white | core/textures/common/environment_white.texture |
| environment_default | core/textures/common/environment_default.texture |


## Arguments


### unit


***Integer***


The texture slot to be used by this texture.


Available values:


- 0..63. Only the first 16 slots can use textures with [filters](#filter). If the *unit* argument is not specified, then the slot is assigned automatically according on the number of textures defined before: ```cpp Texture2D // unit = 0 assigned by default Texture2D <unit=5> // unit = 5 assigned by user Texture3D  // unit = 2 assigned by default, because it is the third defined texture in the material ```


### auto_init


***Boolean***


Determines whether the texture should be automatically declared to the shader.


Available values:


- false � not auto initialized, requires manual initialization
- true � auto initialized (*by default*)


### shader_name


***String***


Texture name in the shader. If specified the provided texture name is used, otherwise default [naming logic](#usage) is used.


### filter


***String***


The type of the filter for the texture sampler.


Available values:


- point � point texture filtering (*by default*)
- linear � linear texture filtering
- bilinear � bilinear texture filtering


### source


***String***


Defines the type of the source this texture comes from.


Available values:


- asset � a standard image texture that is loaded from a disk (*by default*).
- custom � a custom type of texture that can be created via [API methods](../../../../api/library/rendering/class.renderer_cpp.md#createCustomTexture3D_cstr_int_int_int_int_int_Texture).
- procedural � a texture of unknown format that is set manually.
- gbuffer_albedo � a texture that uses [the G-buffer to store albedo values](../../../../principles/render/sequence/index.md#albedo).
- gbuffer_shading � a texture that uses [the G-buffer to store shading data](../../../../principles/render/sequence/index.md#shading).
- gbuffer_normal � a texture that uses [the G-buffer to store normal values](../../../../principles/render/sequence/index.md#normal).
- gbuffer_velocity � a texture that uses [the G-buffer to store velocity values](../../../../principles/render/sequence/index.md#velocity).
- gbuffer_features � a texture that uses [the G-buffer to store specific feature values](../../../../api/library/rendering/class.render_cpp.md#setSSBevel_int_void).
- auxiliary � an auxiliary texture that is used [for different post effects (an auxiliary pass)](../../../../principles/render/sequence/index.md#auxiliary).
- refraction � a texture that [stores refraction data](../../../../principles/render/sequence/index.md#refraction).
- refraction_mask � a texture [storing the refraction mask](../../../../principles/render/sequence/index.md#refraction_apply).
- transparent_blur � a 1-channel R16F mask that stores intensity of blurring for transparent materials. The mask specifies where to blur the material.
- lights � a 2D array texture of the RG11B10F format that stores diffuse light in the first layer (RGB) and specular light in the second layer (RGB).
- gbuffer_material_mask � a texture that uses [the G-buffer to store material mask data](../../../../principles/render/sequence/index.md#material_mask).
- gbuffer_lightmap � a texture that uses [the G-buffer to store lightmap values](../../../../principles/render/sequence/index.md#light_map).
- gbuffer_geodetic_flat_position � a texture that uses the G-buffer to store flat plane coordinates.
- bent_normal � an RG11B10F texture that stores bent normals (RGB) used for smooth ambient lighting.
- ssao � a texture that [stores SSAO (Screen Space Ambient Occlusion) data](../../../../principles/render/sequence/index.md#ssao).
- ssgi � a texture that [stores SSGI (Screen Space Global Illumination) data](../../../../principles/render/sequence/index.md#ssgi).
- ssr � a texture that [stores SSR (Screen Space Reflections) data](../../../../principles/render/sequence/index.md#ssr).
- curvature � a texture that is used for [the Screen-Space dirt effect (SSDirt)](../../../../editor2/settings/render_settings/ssdirt/index.md).
- dof_mask � a texture that [stores a DoF (Depth of Field) mask](../../../../principles/render/sequence/index.md#dof).
- auto_exposure � an RG16F texture that stores intensity of the exposure (R) and luminance (G).
- screen_color � a texture that [stores screen color data](../../../../principles/render/sequence/index.md#opaque_deferred) and can be used for post effects.
- screen_color_old � a texture that [stores Color Old (previous frame) data](../../../../principles/render/sequence/index.md#linear_depth_for_ss).
- screen_color_old_reprojection � a texture that [stores Color Old (previous frame) reprojection data](../../../../principles/render/sequence/index.md#linear_depth_for_ss).
- normal_unpack � a texture that stores [unpacked normals](../../../../principles/render/sequence/index.md#linear_depth_for_ss). Available for the following post-effects: SSR, SSGI, SSRTGI, Shadows screen space.
- current_depth � a texture that stores [current depth data](../../../../principles/render/sequence/index.md#depth) for all geometry on the scene.
- opacity_depth � a texture that stores [opacity depth data for opacity geometry](../../../../principles/render/sequence/index.md#depth_pre_pass) and can be used for soft particles and volumetrics.
- linear_depth � a texture that stores [linear depth data](../../../../principles/render/sequence/index.md#linear_depth_for_ss).
- opacity_screen � a texture that stores the [deferred composite](../../../../principles/render/sequence/index.md#deferred_composite) and [emission](../../../../principles/render/sequence/index.md#emission) data.
- light_image � a texture storing the light values provided by projected light sources.
- light_shadow_depth � a texture storing depth values (used to render shadows).
- light_shadow_color � a texture used to render translucent shadows: G-channel stores depth values, R-channel - transparency values.
- transparent_environment_probes � a texture that stores [environment probes rendered on transparent objects](../../../../principles/render/sequence/index.md#deferred_reflection). Available only when the Multiple environment probes option is enabled.
- reflection_2d � a texture storing reflection values (used to render 2D reflections).
- reflection_cube � a texture storing reflection values (used to render [cube-mapped reflections](../../../../principles/render/sequence/index.md#dynamic_reflections)).
- scattering_sky_lut � a texture that stores [sky scattering LUT data](../../../../principles/render/sequence/index.md#common_pass).
- wbuffer_constant_id � a constant texture, R32U. A texture of this type stores the ID value of the [water mesh](../../../../principles/render/sequence/index.md#water) which is used to load the corresponding textures and parameters for it.
- wbuffer_diffuse � a [diffuse texture](../../../../principles/render/sequence/index.md#wbuffer_diffuse). The diffuse color of the water is black, and diffuse texture is necessary for decals that will be displayed over the water surface.
- wbuffer_normal � a [normal texture](../../../../principles/render/sequence/index.md#wbuffer_normal) stores normal data for lighting, alpha channel stores mesh transparency values (can be used for soft intersections with water geometry).
- wbuffer_water � a [water texture](../../../../principles/render/sequence/index.md#wbuffer_water), RG8. It is used to create the procedural foam mask. The mask shows where the foam will be depicted
- wbuffer_ss_environment � an RGBA16 [underwater fog texture](../../../../principles/render/sequence/index.md#wbuffer_underwater_fog) that stores water bottom coloring values (RGB) and fog transparency (A).
- wbuffer_wu_mask � an [underwater mask texture](../../../../principles/render/sequence/index.md#wbuffer_underwater_mask), RGB8. The underwater mask is used only for *Global Water*, since water mesh doesn't have an underwater mode
- wbuffer_planar_reflection � a water gbuffer texture for the planar reflection.
- clouds_static_coverage � a texture that stores clouds static coverage data.
- clouds_dynamic_coverage � a texture that stores clouds dynamic coverage data.
- clouds_screen � an RGBA16F texture into which clouds are rendered.
- terrain_global_depth � a texture that stores depth data for terrain global.
- terrain_global_flat_position � a texture that stores the flat position for terrain global.
- field_height_array � a heightmap texture that is used to create an additional height displacement for the water surface.
- field_shoreline_array � a [field shoreline texture](../../../../principles/render/sequence/index.md#field_shoreline).
- decal_depth � a texture that stores depth data for decals.
- decal_albedo � a texture that stores albedo color data for decals.
- decal_normal � a texture that stores [normal data for decals](../../../../principles/render/sequence/index.md#decals).
- decal_shading � a texture that stores shading data for decals.
- curve � 2d curves stored in a form of a texture. For this type of textures one or more two-dimensional curves (*Curve2d*) with some keys (*CurveKey*) must be specified. Usage Example: ```cpp TextureCurve emission_color if[emission_color_type == 1]  <unit=8> { Curve2d red <repeat_mode_end=clamp repeat_mode_start=clamp> { CurveKey key <point=[0.0 1.0] left_tangent=[0 0] right_tangent=[0 0]> CurveKey key <point=[1.0 1.0] left_tangent=[0 0] right_tangent=[0 0]> } Curve2d green <repeat_mode_end=clamp repeat_mode_start=clamp> { CurveKey key <point=[0.0 1.0] left_tangent=[0 0] right_tangent=[0 0]> CurveKey key <point=[1.0 1.0] left_tangent=[0 0] right_tangent=[0 0]> } Curve2d blue <repeat_mode_end=clamp repeat_mode_start=clamp> { CurveKey key <point=[0.0 1.0] left_tangent=[0 0] right_tangent=[0 0]> CurveKey key <point=[1.0 1.0] left_tangent=[0 0] right_tangent=[0 0]> } } ``` The syntax of ***Curve2d***: ```cpp Curve2d name <arguments> ``` Arguments: The syntaxis of *CurveKey*: ```cpp CurveKey name <arguments> ``` Arguments:

  - repeat_mode_end (*string*) � the mode for the beginning of the curve to be used for repeating the sequence defined by the key points of the curve (tiling curves).
  - repeat_mode_start (*string*) � the mode for the end of the curve to be used for repeating the sequence defined by the key points of the curve (tiling curves). Available values:

    - clamp � the value of the start or the end key is retained. Use this option if you don't want any changes before or after the effect created by the curve (*by default*).
    - loop � the curve is tiled. The created effect is repeated cyclically. If the values of the first and the last key are different, the transition between the curves will be abrupt.
    - ping_pong � every next curve section is a reflection of the previous curve section. The created effect is repeated in the forward-and-backward manner.

  - point (*float*) � a new key point with the specified coordinates.
  - left_tangent (*float*) � coordinates for the left tangent at the specified key point of the curve.
  - right_tangent (*float*) � coordinates for the right tangent at the specified key point of the curve.


### anisotropy


***Boolean***


Enables the anisotropic filtering (works alongside with other types of texture filtering). By default 2x anisotropy is used.


Available values:


- **false** � disable
- **true** � enable (*by default*)


### shader


***String***


The type of shader to which this texture will be passed.


Available values:


- *all* � pass the texture to all shaders (*by default*)
- *fragment* � pass the texture to the fragment (pixel) shader only


### shared


***Boolean***


Enables the texture passing and binding to shaders.


Available values:


- false � disable
- true � enable


### internal


***Boolean***


Enables the mode when texture values are not saved for the inherited materials. Also, hides the texture in the Editor.


Available values:


- false � disable mode (*by default*)
- true � enable mode


### editable


***Boolean***


A flag indicating if texture can be changed in the *[Parameters](../../../../editor2/materials_settings/index.md)* window or via [API](../../../../api/library/rendering/class.material_cpp.md).


Available values:


- false � unchangeable
- true � changeable (by default)


### hidden


***Boolean***

Hides the texture in the Editor. The default value is the same as the value of [internal](#internal) argument.


Available values:


- **false** � show the texture
- **true** � hide the texture


### force_streaming


***Boolean***


Disables the asynchronous streaming and loads the texture immediately as soon as it is required (rendering sequence stops until the texture is loaded).


Available values:


- false � use the standard asynchronous streaming (*by default*)
- true � disable the asynchronous streaming and load the texture immediately


### pass


***Array of Strings***


The set of passes to which the texture is passed. By default the texture is passed to all passes.


Available values:


- **custom_pass_name** � name of a custom rendering pass (up to 32 custom passes are supported)
- **wireframe** � the wireframe pass
- **visualizer_solid** � the visualizer solid pass
- **deferred** � the deferred pass
- **auxiliary** � the auxiliary pass
- **emission** � the emission pass
- **refraction** � the refraction pass
- **reflection** � the reflection pass
- **transparent_blur** � the transparent blur pass
- **ambient** � the ambient pass
- **light_voxel_probe** � the *Voxel Probe* light pass
- **light_environment_probe** � the *Environment Probe* pass
- **light_omni** � the omni-directional light pass
- **light_proj** � the projected light pass
- **light_world** � the world light pass
- **depth_pre_pass** � the native depth pre-pass
- **ms_depth** - the *SRAA* pass
- **shadow** � the shadows pass
- **post** � the post-process pass
- **procedural_decals** - the procedural decal pass
- **procedural_fields** - the procedural field pass
- **light_all** � the *[Environment Probe](#texture_pass_light_environment_probe), [Omni Light](#texture_pass_light_omni), [Proj Light](#texture_pass_light_proj), [World Light](#texture_pass_light_world)* passes
- **forward** � the *[Environment Probe](#texture_pass_light_environment_probe), [Omni Light](#texture_pass_light_omni), [Proj Light](#texture_pass_light_proj), [World Light](#texture_pass_light_world)* and [ambient](#texture_pass_ambient) passes
- **transparent** � the [forward](#texture_pass_forward), [refraction](#texture_pass_refraction), [transparent blur](#texture_pass_transparent_blur) passes
- **object** � [deferred](#texture_pass_deferred), [auxiliary](#texture_pass_auxiliary), [emission](#texture_pass_emission), [refraction](#texture_pass_refraction), [reflection](#texture_pass_reflection), [transparent blur](#texture_pass_transparent_blur), [ambient](#texture_pass_ambient), *[Voxel Probe](#texture_pass_light_voxel_probe), [Environment Probe](#texture_pass_light_environment_probe), [Omni Light](#texture_pass_light_omni), [Proj Light](#texture_pass_light_proj), [World Light](#texture_pass_light_world)*, [shadow](#texture_pass_shadow) and [native depth passes](#texture_pass_depth_pre_pass)


> **Notice:** To make one or more passes use this state, write passes in square brackets and separate them with spaces. For example:
>
>
> ```cpp
> State wireframe_antialiasing <pass=[wireframe post custom_pass_name]>
>
> ```


### wrap


***String***


The type of texture wrapping when the coordinate in the specified dimension [U V W] is out of the limits range [0..1].


Available values:


- clamp - clamps the coordinates [U V W] between 0 and 1 (the values higher than 1 are clamped to the edge resulting in a stretched edge pattern)
- clamp_x - clamps the U coordinate between 0 and 1 (the value higher than 1 are clamped to the edge resulting in a stretched edge pattern)
- сlamp_y - clamps the W coordinate between 0 and 1 (the value higher than 1 are clamped to the edge resulting in a stretched edge pattern)
- clamp_z - clamps the V coordinate between 0 and 1 (the value higher than 1 are clamped to the edge resulting in a stretched edge pattern)
- border - returns the white color for UVW coordinates outside the [0..1] range
- **border_x** - returns the color for the U coordinate outside the [0..1] range (color by default - black)
- **border_y** - returns the color for the V coordinate outside the [0..1] range (color by default - black)
- **border_z** - returns the color for the W coordinate outside the [0..1] range (color by default - black)
- border_one - if specified, the return color is set to white for the [border_x](#border_x), [border_y](#border_y), and [border_z](#border_z) modes
- repeat - repeats the texture image when coordinates are outside of the range [0..1] (*by default*)


Usage Example:


```cpp
wrap = [clamp_x border_y clamp_z]

```


### title


***String***


Specifies the texture title to be displayed in the Editor.


### tooltip


***String***


Specifies the tooltip for the texture to be displayed in the Editor.
