# Decal


Implements the basic render functionality for decals. Can be used for the following objects:


- [DecalProj](../../../api/library/decals/class.decalproj_cpp.md)
- [DecalOrtho](../../../api/library/decals/class.decalortho_cpp.md)
- [DecalMesh](../../../api/library/decals/class.decalmesh_cpp.md)


You can find the source code for this abstract material here: `<SDK>/data/core/materials/abstract/decal/decal.abstmat`


## Features


The abstract material for decals has features implemented as internal states that can be enabled on demand in the child material.


| blend_src ( Option ) |  |
|---|---|
| Description: | Option used to scale the source color (the color of an overlaying material). |
| Editable: | false |
| Default: | **src_alpha** |
| blend_dest ( Option ) |  |
| Description: | Option used to scale the destination color (the color of an obscured material). |
| Editable: | false |
| Default: | **one_minus_src_alpha** |
| transparent ( Option ) |  |
| Description: | Transparency type of the material. |
| Editable: | false |
| Default: | **blend** |
| alpha_fade ( State ) |  |
| Description: | Adds smooth transitions in the areas neighboring with visibility limits (defined by [fade and visibility settings](../../../objects/decals/proj/index.md#visibility)). Can be used for smooth transitions between LODs. |
| Internal: | true |
| Default: | **false** |
| screen_projection ( State ) |  |
| Description: | Enables [screen projection](../../../content/materials/library/decal_base/index.md#option_screen_proj) for the decal instead of projecting it onto a surface. (only Mesh decals are supported) |
| Editable: | false |
| Default: | **false** |
| emission ( State ) |  |
| Description: | Enables emission rendering. This effect simulates glow from extremely bright surfaces and can be used to create self-luminous objects (lamps, fire, etc.) |
| Editable: | false |
| Default: | **false** |
| auxiliary ( State ) |  |
| Description: | Enables auxiliary rendering pass for the material. Can be used for custom post-effects, such as thermal vision, etc. |
| Editable: | false |
| Default: | **false** |
| albedo ( State ) |  |
| Description: | Enables the output to the decal albedo buffer. |
| Editable: | false |
| Default: | **true** |
| metalness_specular_translucent ( State ) |  |
| Description: | Enables the output to the decal shading buffer. |
| Editable: | false |
| Default: | **true** |
| roughness_microfiber ( State ) |  |
| Description: | Enables the output to the decal shading buffer. |
| Editable: | false |
| Default: | **true** |
| normal ( State ) |  |
| Description: | Enables the output to the decal normal buffer. |
| Editable: | false |
| Default: | **true** |
| normal_substitute ( State ) |  |
| Description: | Rendering mode for normals. By default, normal maps of a base and overlapping material are combined together. With this option enabled, only normals of the overlapping material are used. |
| Editable: | false |
| Default: | **false** |
| tbn_mode ( State ) |  |
| Description: | Defines the tangent space (*Tangent-Binormal-Normal* matrix) used for normal mapping: - **Take From Decal Mesh** (0) � normals of the decal mesh (for *Mesh* decals) or plane (for *Orthographic* and *Projected* decals) are used; - **Up Direction of Decal** (1) � decal's local up vector is used; - **GBuffer Normal** (2) � normals from the screen *normal* buffer are used; - **GBuffer Depth Based Normal** (3) � normals are constructed based on the screen *depth* buffer content. Unlike *GBuffer Normal*, this option provides unaltered normals as they are presented in the scene geometry. |
| Editable: | false |
| Default: | **0** |
| material_mask ( Mask24 ) |  |
| Description: | Decal bit-mask. A decal will be projected onto a surface if this mask matches the mask of the surface material (one bit, at least). |
| Default: | **0xffffffff** |
| Condition: | (gbuffer) |
| viewport_mask ( Option ) |  |
| Description: | Viewport mask of the material. A surface, having this material assigned, will be rendered into a viewport, if its viewport mask and the material viewport mask match the viewport mask of the camera (one bit, at least). |
| Default: | **0xffffffff** |
| order ( Option ) |  |
| Description: | Sort order used when rendering transparent objects with alpha blending. *Transparent* objects should be set lowest order numbers and thus rendered first, while *opaque* objects should be set highest order numbers to be rendered last. |
| Default: | **false** |


## Shaders


Here's the list of available shader code that includes types for the current abstract material. These custom shaders are included in the abstract material's shader in the corresponding place via marker.


### common


All shader code that you describe here (variables, functions, defines, constants, etc.) is included in every other type of shader: vertex, fragment.


### vertex_struct


Using the following structures you can get access to the base and user data in these shaders: vertex, fragment.


| Name | Arguments | Description |
|---|---|---|
| INIT_USER_DATA | **TYPE** � type of the user data **NAME** � name of the user data | Initializes user data that will be interpolated between vertices and passed through the shader pipeline. |


### vertex


Performs operations (e.g., transformations) on individual vertices received from the Input Assembler stage and passes them to the hidden geometry shader. You can use the provided **Input data** to modify **[Output data](#vertex_output_data)**.


#### Input Data


| Name | Type | Description |
|---|---|---|
| VERTEX_IN_TRANSFORM | float4x4 | Transforms from object space to view space. |
| VERTEX_IN_ITRANSFORM | float4x4 | Transforms from view space to object space. |
| VERTEX_IN_MODELVIEW | float4x4 | Transforms from world space to view space. |
| VERTEX_IN_IMODELVIEW | float4x4 | Transforms from view space to world space. |
| VERTEX_IN_TIME | float | Current global engine time elapsed since the engine initialization in ms. Updates automatically to correctly calculate velocity. |
| VERTEX_IN_GAME_TIME | float | Current game time that relates to Game::setScale and Game::setIFps. Updates automatically to correctly calculate velocity. |
| VERTEX_IN_POSITION | float3 | Vertex position in object space. |
| VERTEX_IN_UV | float4 | Vertex projected UV. |
| VERTEX_IN_COLOR | float4 | Color of the vertex. Constant value � float4(1, 1, 1, 1) (only for DecalProj and DecalOrtho). |
| VERTEX_IN_BASIS | float4 | Vertex encoded basis, use getTangentBasis(). Constant value � float4(0, 0, 0, -1) (only for DecalProj and DecalOrtho). |
| VERTEX_IN_TANGENT | float3 | Vertex object space tangent. Constant value � float3(1, 0, 0) (only for DecalProj and DecalOrtho). |
| VERTEX_IN_BINORMAL | float3 | Vertex object space binormal. Constant value � float3(0, -1, 0) (only for DecalProj and DecalOrtho). |
| VERTEX_IN_NORMAL | float3 | Vertex object space normal. Constant value � float3(0, 0, 1) (only for DecalProj and DecalOrtho). |


#### Output Data


| Name | Type | Description |
|---|---|---|
| DATA_POSITION | float3 | Vertex position in view space |
| DATA_TANGENT | float3 | Vertex tangent in view space |
| DATA_BINORMAL | float3 | Vertex binormal in view space |
| DATA_NORMAL | float3 | Vertex normal in view space |
| DATA_UV | float4 | Contains a set of vertex UV coordinates. For DecalMesh: - **xy** � base UV - **zw** � lightmap UV For DecalProj/DecalOrtho: - **xy** � UV for current vertex - **zw** � 0, 0 |
| DATA_COLOR | float4 | Vertex RGBA color |


### fragment


Produces shading data for each interpolated pixel fragment.


#### Input Data


| Name | Type | Description |
|---|---|---|
| DATA_TANGENT | float3 | Position in view space. |
| DATA_BINORMAL | float3 | Tangent in view space. |
| DATA_NORMAL | float3 | Binormal in view space. |
| DATA_SIGN_BINORMAL | float | Sign of the binormal. |
| DATA_UV | float4 | A set of UV coordinates. For DecalMesh: - **xy** � base UV - **zw** � lightmap UV For DecalProj/DecalOrtho: - **xy** � UV for current vertex - **zw** � 0, 0 |
| DATA_COLOR | float4 | RGBA color. |
| PROJECTED_NORMAL | float3 | Normal in view space. |
| PROJECTED_POSITION | float3 | Fragment camera world space position. |
| SCENE_NORMAL | float3 | GBuffer normal. |
| SCENE_POSITION | float3 | Fragment object space position. |


#### Output Data


| Name | Type | Default | Description |
|---|---|---|---|
| OUT_FRAG_OPACITY | float | Defined for most cases separately. (check abstract material source code for reference) | Decal global visibility |
| OUT_FRAG_AUXILIARY | float4 | (0, 0, 0, 0) | Auxiliary color modifier (requires enabled [auxiliary](#auxiliary)) |
| OUT_FRAG_OPACITY_AUXILIARY | float | 1 | Auxiliary visibility (requires enabled [auxiliary](#auxiliary)) |
| OUT_FRAG_EMISSION | float3 | (0, 0, 0) | Emission color modifier (requires enabled [emission](#emission)) |
| OUT_FRAG_ALBEDO | float3 | (0, 0, 0) | GBuffer albedo color modifier (requires enabled [albedo](#albedo)) |
| OUT_FRAG_OPACITY_ALBEDO | float | 1 | Albedo color visibility (requires enabled [albedo](#albedo)) |
| OUT_FRAG_METALNESS | float | 0 | GBuffer metalness modifier (requires enabled [metalness_specular_translucent](#metalness_specular_translucent)) |
| OUT_FRAG_SPECULAR | float | 0.0 | GBuffer specular modifier (requires enabled [metalness_specular_translucent](#metalness_specular_translucent)) |
| OUT_FRAG_TRANSLUCENT | float | 0 | GBuffer translucent modifier (requires enabled [metalness_specular_translucent](#metalness_specular_translucent)) |
| OUT_FRAG_OPACITY_METALNESS_SPECULAR_TRANSLUCENT | float3 | 1 | Metalness, specular and translucent visibility (requires enabled [metalness_specular_translucent](#metalness_specular_translucent)) |
| OUT_FRAG_ROUGHNESS | float | 0 | GBuffer roughness modifier (requires enabled [roughness_microfiber](#roughness_microfiber)) |
| OUT_FRAG_MICROFIBER | float | 0 | GBuffer microfiber modifier (requires enabled [roughness_microfiber](#roughness_microfiber)) |
| OUT_FRAG_OPACITY_ROUGHNESS_MICROFIBER | float | 0 | Roughness and microfiber visibility (requires enabled [roughness_microfiber](#roughness_microfiber)) |
| OUT_FRAG_NORMAL | float3 | DATA_NORMAL | Normal in modelview space (requires enabled [normal](#normal)) |
| OUT_FRAG_OPACITY_NORMAL | float | 1 | Normal visibility (requires enabled [normal](#normal)) |


#### Textures


List of available textures that are pre-defined and used in the fragment shader.


| Name | Type | Description |
|---|---|---|
| depth | 2D | Texture that stores the native opacity depth. |
| material_mask | 2D | Texture that stores the material mask. |
| gbuffer_normal | 2D | Texture that uses the G-buffer to store encoded normal. |


## Usage Example


<details>
<summary>Decal | Close</summary>

```xml
BaseMaterial <parent=Unigine::decal>
{
	TextureCube cubemap = "core/textures/common/environment_probe_default.texture"
	Slider z_offset = 0.5f <min=0 max=0.8>

	Shader common=
	#{
		float3 sample_albedo(float3 scene_position, float3 data_normal)
		{
			const float3x3 view_to_camera_world = toFloat3x3(s_imodelview);
			const float3x3 rotate_view_to_world = view_to_camera_world;

			float3 view_direction  = positionToViewDirection(scene_position);

			float3 cube_sample_uvw = reflect(-view_direction, data_normal);
			cube_sample_uvw = mul3(rotate_view_to_world, cube_sample_uvw) - float3(0.0f, 0.0f, var_z_offset);
			return TEXTURE(tex_cubemap, cube_sample_uvw).rgb;
		}
	#}

	Shader fragment=
	#{
		OUT_FRAG_ALBEDO = sample_albedo(SCENE_POSITION, DATA_NORMAL);
		OUT_FRAG_SPECULAR = 1.0f;
		OUT_FRAG_ROUGHNESS = 1.0f;
	#}
}

```

</details>
