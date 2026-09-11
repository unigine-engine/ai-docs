# Mesh


Implements the basic render functionality of the mesh. Can be used for the following objects:


- [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)
- [ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)
- [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)
- [ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)
- [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)
- [ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)


You can find the source code for this abstract material here: `<SDK>/data/core/materials/abstract/mesh/mesh.abstmat`


## Features


The abstract material for a mesh has features implemented as internal states that can be enabled on demand in the child material:


| Name | Description |
|---|---|
| [Engine](#feature_engine) | Essential features of the *Mesh* material. |
| [Post Processing](#feature_post_processing) | Post Processing effects that are supported by the material. |
| [Specular AA](#feature_specular_aa) | [Specular Anti-Aliasing](../../../content/materials/library/mesh_base/index.md#option_specular_aa) feature. |
| [Tessellation](#feature_tessellation) | Mesh [Tessellation](../../../content/materials/library/mesh_base/index.md#tessellated_displacement) feature. |


> **Notice:** The following states, options and parameters are the base functionality that is also available in the [Mesh Transparent](../../../code/materials_shaders/abstract_materials/mesh_transparent.md) and [Mesh Unlit](../../../code/materials_shaders/abstract_materials/mesh_unlit.md) abstract materials.


### Engine


Engine group.

| alpha_fade ( State ) |  |
|---|---|
| Description: | Adds smooth transitions in the areas neighboring with visibility limits of the mesh (defined by fade and visibility settings for a surface to which the material is assigned). Can be used for smooth transitions between LODs. |
| Internal: | true |
| Default: | **false** |
| gbuffer ( State ) |  |
| Description: | Enables writing of deferred buffers for the material. |
| Editable: | false |
| Default: | **true** |
| lightmap ( State ) |  |
| Description: | Enables lightmaps for the geometry to which this material is assigned. |
| Internal: | true |
| Default: | **false** |
| wireframe_antialiasing ( State ) |  |
| Description: | Enables antialiasing of wireframes for the geometry to which this material is assigned. |
| Internal: | true |
| Default: | **false** |
| force_velocity ( State ) |  |
| Description: | Enabling this option forces the Engine to calculate velocity required for the mesh to support [TAA](../../../principles/render/antialiasing/taa.md). |
| Editable: | false |
| Default: | **false** |
| dynamic ( State ) |  |
| Description: | Enables writing to [velocity buffer](../../../principles/render/sequence/index.md#velocity). |
| Internal: | true |
| Default: | **false** |
| Condition: | (!force_velocity) |
| static_shadow ( State ) |  |
| Description: | Enables using the **Unigine::mesh_static_shadow** material instead of this material for shadows. Disabled for forward materials that support *ObjectMeshStatic* or *ObjectParticles*. |
| Editable: | false |
| Default: | **false** |
| Condition: | (!tessellation_shadow && !custom_depth) |
| custom_depth ( State ) |  |
| Description: | Enables writing custom depth to the Z-Buffer. |
| Editable: | false |
| Default: | **0** |
| custom_depth_shadow ( State ) |  |
| Description: | Flag indicating whether custom depth affects shadows. |
| Editable: | false |
| Default: | **true** |
| Condition: | (custom_depth) |
| tessellation ( State ) |  |
| Description: | Enables tessellation for the geometry to which this material is assigned. |
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
| blend_src ( Option ) |  |
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
| Default: | **none** |
| overlap ( Option ) |  |
| Description: | Render polygons, to which the material is applied, on the top of the render. This can be used for UI elements. |
| Editable: | false |
| Default: | **false** |
| two_sided ( Option ) |  |
| Description: | Render polygons, to which the material is applied, two times per lighting pass. This option should be disabled to gain performance, when you don't need both sides of polygons to be rendered. |
| Editable: | false |
| Default: | **false** |
| depth_test ( Option ) |  |
| Description: | Toggles depth testing for the material on and off. This can be used to make objects occluded by others visible (e.g. a character behind a wall). |
| Editable: | false |
| Default: | **true** |
| depth_mask ( Option ) |  |
| Description: | A flag indicating if writing in the [depth buffer](../../../editor2/materials_settings/index.md#depth_write) is enabled for a material (only for *[Object](../../../api/library/objects/class.object_cpp.md)*). |
| Editable: | false |
| Default: | **true** |


### Post Processing


The following states define bits in the material mask:

| material_ssao ( State ) |  |
|---|---|
| Description: | Enables the screen-space ambient occlusion (SSAO) for this material (Alpha Test and Opaque only, non Alpha Blend materials). |
| Default: | **true** |
| Condition: | (gbuffer)&&(transparent!=2) |
| material_ssr ( State ) |  |
| Description: | Enables the screen-space reflections (SSR) for this material (Alpha Test and Opaque only, non Alpha Blend materials). |
| Default: | **true** |
| Condition: | (gbuffer)&&(transparent!=2) |
| material_sssss ( State ) |  |
| Description: | Enables the Screen-Space Subsurface Scattering (SSSSS) for this material (Alpha Test and Opaque only, non Alpha Blend materials). |
| Default: | **false** |
| Condition: | (gbuffer)&&(transparent!=2) |
| material_dof ( State ) |  |
| Description: | Enables the Depth of Field (DOF) effect for this material. |
| Default: | **true** |
| Condition: | (gbuffer) |
| material_motion_blur ( State ) |  |
| Description: | Enables the motion blur for this material. |
| Default: | **true** |
| Condition: | (gbuffer) |
| material_screen_space_shadows ( State ) |  |
| Description: | Enables the screen space shadows for this material. |
| Default: | **true** |
| Condition: | (gbuffer) |
| material_shoreline_wetness ( State ) |  |
| Description: | Enables the wetness effect for objects near the shoreline for this material (Alpha Test and Opaque only, non Alpha Blend materials). |
| Default: | **true** |
| Condition: | (gbuffer)&&(transparent!=2) |


### Specular AA


| specular_aa ( State ) |  |
|---|---|
| Description: | Anti-aliasing of specular highlights. This anti-aliasing is performed by increasing roughness at places where normals change their orientation. Geometry of the model is used, the normal map is not required. |
| Editable: | true |
| Internal: | false |
| Default: | **false** |
| specular_aa_intensity ( Slider ) |  |
| Description: | Strength of the specular anti-aliasing effect between 0 and 1. Higher values produce a blurrier result with less aliasing. |
| Editable: | true |
| Internal: | false |
| specular_aa_threshold ( Slider ) |  |
| Description: | Maximum value for the offset to be subtracted from the smoothness value to reduce artifacts. |
| specular_aa_albedo_impact ( State ) |  |
| Description: | Intensity of darkening the albedo on metal surfaces. |
| specular_aa_specular_impact ( Slider ) |  |
| Description: | Intensity of darkening the specular on dielectric surfaces. |
| specular_aa_roughness_impact ( State ) |  |
| Description: | Intensity of roughness. |


### Tessellation


| tessellation_shadow ( State ) |  |
|---|---|
| Description: | Enables tessellation for the shadow pass. |
| Default: | **false** |
| Condition: | (tessellation) |


| tessellation_density ( Slider ) |  |
|---|---|
| Description: | Coefficient for subpixel reduction of polygons. The value of **1** corresponds to the highest mesh density defined by the **Factor** parameter. **Notice**: *although lower values help significantly reduce the number of polygons and improve the performance, be careful as visual artifacts may appear when the camera moves. To get rid of wiggling and keep the small number of polygons, it is recommended to increase **Density** while decreasing **Factor** values.* |
| Default: | **0.5** |
| Condition: | (tessellation) |
| tessellation_shadow_factor ( Slider ) |  |
| Description: | Coefficient of tessellation intensity for shadow polygons: *higher* values produce *more* polygons. |
| Default: | **0.25** |
| Condition: | (tessellation)&&(tessellation_shadow) |
| tessellation_shadow_density ( Slider ) |  |
| Description: | Coefficient for subpixel reduction of shadow polygons. The value of **1** corresponds to the highest mesh density defined by the **Shadow Factor** parameter. |
| Default: | **0.1** |
| Condition: | (tessellation)&&(tessellation_shadow) |
| tessellation_distance_falloff_near ( Slider ) |  |
| Description: | Distance (in units) from the camera where tessellation falloff starts. |
| Default: | **2** |
| Condition: | (tessellation) |
| tessellation_distance_falloff_far ( Slider ) |  |
| Description: | Tessellation falloff distance range, in units. Tessellation effect is rendered at the distance range from **Near** to **Near + Far**. |
| Default: | **50** |
| Condition: | (tessellation) |
| tessellation_distance_falloff_exp ( Slider ) |  |
| Description: | Determines how fast the tessellation intensity decreases with the distance. |
| Default: | **1** |
| Condition: | (tessellation) |
| tessellation_distance_falloff_max_mip ( Slider ) |  |
| Description: | Maximum allowed mipmap level of the **Displacement** texture to avoid losing tessellation details with the distance. |
| Default: | **6** |
| Condition: | (tessellation) |
| tessellation_culling_near ( Slider ) |  |
| Description: | Distance (in units) from the camera where the tessellation culling starts. |
| Default: | **1** |
| Condition: | (tessellation) |
| tessellation_culling_back_face ( Slider ) |  |
| Description: | Angle (in degrees) between the camera and a polygon of the control mesh, at which the polygon is not tessellated. |
| Default: | **0.5** |
| Condition: | (tessellation) |
| tessellation_culling_screen_border ( Slider ) |  |
| Description: | Screen border offset used to prevent undesired culling of tessellated polygons outside the screen. |
| Default: | **0.1** |
| Condition: | (tessellation) |
| tessellation_shadow_culling_back_face ( Slider ) |  |
| Description: | Angle (in degrees) between the camera and a shadow polygon of the control mesh, at which this polygon is not tessellated. |
| Default: | **0.8** |
| Condition: | (tessellation)&&(tessellation_shadow) |
| tessellation_shadow_culling_screen_border ( Slider ) |  |
| Description: | Screen border offset used to prevent undesired culling of tessellated shadow polygons outside the screen. |
| Default: | **0.05** |
| Condition: | (tessellation)&&(tessellation_shadow) |


## Shaders


Here's the list of available shader code that includes types for the current abstract material. These custom shaders are included in the abstract material's shader in the corresponding place via marker.


### common


All shader code that you describe here (variables, functions, defines, constants, etc.) is included in every other type of shader: vertex, control, evaluate, fragment.


### vertex_struct


Using the following structures you can get access to the base and user data in these shaders: vertex, control, evaluate, fragment.


| Name | Arguments | Description |
|---|---|---|
| INIT_BASE_DATA | *(none)* | Initializes the base structure variables (available in all shaders). |
| INIT_USER_DATA | **TYPE** � type of the user data **NAME** � name of the user data | Initializes user data that will be interpolated between vertices and **passed through the shader pipeline**. |
| INIT_USER_NOINTERPOLATION_DATA | **TYPE** � type of the user data **NAME** � name of the user data | Initializes user data that won�t be interpolated between vertices but still **will be passed through shader pipeline**. |


**INIT_BASE_DATA** initializes the following set of semantics:


| Name | Type | Description | Access |
|---|---|---|---|
| INIT_POSITION | float4 | Adds position |  |
| INIT_FRONTFACE | bool | Adds an input semantic indicating primitive face (frontface or not). | (none) |
| INIT_DATA_POSITION | float3 | Adds view-space position. |  |
| INIT_DATA_OBLIQUE_FRUSTUM | float | Adds oblique frustum. | (none) |
| INIT_DATA_ALPHA_FADE | float | Adds alpha fade. | *(none)* |
| INIT_DATA_TESSELLATION_FACTOR | float | Adds tessellation factor. Requires [tessellation](#feature_tessellation) enabled. |  |
| INIT_DATA_TESSELLATION_MIP | float | Adds a custom tessellation mip semantic. Requires [tessellation](#feature_tessellation) enabled. | (none) |
| INIT_DATA_TESSELLATION_SCALE | float | Adds a custom tessellation scale semantic. Requires [tessellation](#feature_tessellation) enabled. | (none) |
| INIT_DATA_UV | float4 | Adds a custom uv coordinate semantic. |  |
| INIT_DATA_NEW_POSITION | float3 | Adds a custom new position semantic. Updates automatically. | (none) |
| INIT_DATA_OLD_POSITION | float3 | Adds a custom old position semantic. Updates automatically. | (none) |
| INIT_DATA_COLOR | float4 | Adds a custom color semantic. |  |
| INIT_DATA_BINORMAL | float3 | Adds a custom binormal semantic. |  |
| INIT_DATA_NORMAL | float3 | Adds a custom normal semantic. |  |
| INIT_DATA_SIGN_BINORMAL | float | Adds a custom binormal sign semantic. |  |


### vertex


Performs operations (e.g., transformations) on individual vertices received from the Input Assembler stage. You can use the provided **Input data** to modify **[Output data](#vertex_output_data)**.


#### Input Data


| Name | Type | Description |
|---|---|---|
| VERTEX_IN_POSITION | float3 | Vertex position in object space |
| VERTEX_IN_UV | float4 | UV coordinates of the vertex |
| VERTEX_IN_COLOR | float4 | Color of the vertex |
| VERTEX_IN_BASIS | float4 | Basis quaternion in space. Updates automatically to correctly calculate velocity. |
| VERTEX_IN_TANGENT | float3 | Tangent of the basis in object space. Updates automatically to correctly calculate velocity. |
| VERTEX_IN_BINORMAL | float3 | Binormal of the basis in object space. Updates automatically to correctly calculate velocity. |
| VERTEX_IN_NORMAL | float3 | Normal of the basis in object space. Updates automatically to correctly calculate velocity. |
| DATA_SIGN_BINORMAL | float | Sign of the binormal in object space. |
| VERTEX_IN_TRANSFORM | float4x4 | Transforms from object space to view space. |
| VERTEX_IN_MODELVIEW | float4x4 | Transforms from world space to view space. Updates automatically to correctly calculate velocity. |
| VERTEX_IN_IMODELVIEW | float4x4 | Transforms from view space to world space. Updates automatically to correctly calculate velocity. |
| VERTEX_IN_INSTANCE | uint | Object�s batched instance ID. |
| VERTEX_IN_TIME | float | Current global engine time elapsed since the engine initialization in ms. Updates automatically to correctly calculate velocity. |
| VERTEX_IN_GAME_TIME | float | Current game time that relates to Game::setScale and Game::setIFps. Updates automatically to correctly calculate velocity. |


Use these variables as they are automatically updated during the material processing (for example, due to velocity calculations the vertex shader is executed twice).


#### Output Data


| Name | Type | Description |
|---|---|---|
| DATA_POSITION | float3 | Vertex position in view space |
| DATA_TANGENT | float3 | Vertex tangent in view space |
| DATA_BINORMAL | float3 | Vertex binormal in view space |
| DATA_NORMAL | float3 | Vertex normal in view space |
| DATA_UV | float4 | Contains a set of vertex UV coordinates: - **xy** � base UV - **zw** � lightmap UV |
| DATA_COLOR | float4 | Vertex RGBA color |
| DATA_TESSELLATION_FACTOR | float | Mesh tessellation factor. Available only when tessellation state is enabled. |


### evaluate


All tessellated vertex data get interpolated here.


#### Input Data


> **Notice:** - Use prefix **IN_EVAL_** instead of **IN_** (e.g. *IN_EVAL_DATA_POSITION(index)*) in order to get a non-interpolated value for the specific vertex of the current patch, where index is a triangle vertex index ranging from 0 to 2.
> - All **IN_#DATA_NAME** here will implicitly call **IN_INTERPOLATE_DATA()**.


#### Functions


> **Notice:** Texture sampling functions take into account the **DATA_TESSELLATION_MIP**.


| Name | Arguments | Description |
|---|---|---|
| TEXTURE | **Name** � name of the texture slot **UV** � texture uv value | Samples a texture. |
| TEXTURE_MIP_OFFSET | **Name** � name of the texture slot **UV** � texture uv value **Offset** � texture uv offset value | Samples a texture with mipmap offset. |


### fragment


Produces color values for each interpolated pixel fragment. You can use the provided **Input data** to modify **[Output data](#fragment_output_data)**.


#### Input Data


| Name | Type | Description |
|---|---|---|
| DATA_NORMAL | float3 | Normal in view space |
| DATA_BINORMAL | float3 | Binormal in view space |
| DATA_TANGENT | float3 | Tangent in view space |
| DATA_UV | float4 | A set of UV coordinates - **xy** � base UV - **zw** � lightmap UV |
| DATA_COLOR | float4 | Vertex color |
| DATA_ALPHA_FADE | float | Alpha fade value |


#### Output Data


> **Notice:** For Alpha Test and Transparent materials (in one of the following passes: *Deferred, Auxiliary, Shadow*), opacity threshold discards pixel if **opacity <= threshold**.


| Name | Type | Default | Description |
|---|---|---|---|
| OUT_FRAG_ALBEDO | float3 | (0, 0, 0) | GBuffer albedo color modifier |
| OUT_FRAG_OPACITY | float | 1 | Alpha of the current pixel |
| OUT_FRAG_OPACITY_THRESHOLD | float | 0.5 | Opacity threshold |
| OUT_FRAG_METALNESS | float | 0 | GBuffer metalness value |
| OUT_FRAG_ROUGHNESS | float | 0 | GBuffer roughness value |
| OUT_FRAG_SPECULAR | float | 0 | GBuffer specular value |
| OUT_FRAG_MICROFIBER | float | 0 | GBuffer microfiber value |
| OUT_FRAG_NORMAL | float3 | DATA_NORMAL | Normal in view space |
| OUT_FRAG_TRANSLUCENT | float | 0 | GBuffer translucent value |
| OUT_FRAG_BEVEL | float | 0 | Bevel radius |
| OUT_FRAG_CAVITY | float | 0 | Cavity mask |
| OUT_FRAG_CONVEXITY | float | 0 | Convexity mask |
| OUT_FRAG_EMISSION | float3 | (0, 0, 0) | Emission color value (requires enabled [emission](#emission)) |
| OUT_FRAG_AUXILIARY | float4 | (0, 0, 0, 0) | Auxiliary color value (requires enabled [auxiliary](#auxiliary)) |
| OUT_FRAG_DELTA_DEPTH | float | 0 | Delta depth (requires enabled [custom_depth](#custom_depth)) |


## Usage Examples


### Normal Mapping


<details>
<summary>Normal Mapping | Close</summary>

```xml
BaseMaterial <parent=Unigine::mesh>
{
	Texture2D normal = "core/textures/post_filter_wet_normal.dds"

	Color albedo = [1 1 1 1]

	// optimization
	State static_shadow = true
	State vertex_velocity = false

	Shader vertex_struct =
	#{
		INIT_BASE_DATA
	#}

	Shader common =
	#{
		float3 color_to_normal_ts(float4 color)
		{
			float3 normal;
			normal.xy = color.xy * 2.0f - float2_one;
			normal.z = sqrt(saturate(1.0f - length(normal.xy)));
			return normalize(normal);
		}

		float3 sample_normalmap(float2 uv, float3x3 rotate_view_to_tangent)
		{
			float4 normalmap = TEXTURE(tex_normal, uv);
			float3 normal = color_to_normal_ts(normalmap);
			return mul3(normal, rotate_view_to_tangent);
		}
	#}

	Shader fragment =
	#{
		const float3x3 rotate_view_to_tangent = matrix3Row(DATA_TANGENT, DATA_BINORMAL, DATA_NORMAL);

		OUT_FRAG_ALBEDO = var_albedo.rgb;
		OUT_FRAG_SPECULAR = 0.5f;
		OUT_FRAG_ROUGHNESS = 1.0f;
		OUT_FRAG_METALNESS = 0.0f;
		OUT_FRAG_NORMAL = sample_normalmap(DATA_UV.xy, rotate_view_to_tangent);
	#}
}

```

</details>


### Albedo Texture


<details>
<summary>Albedo Texture | Close</summary>

```xml
BaseMaterial <parent=Unigine::mesh>
{
	Texture2D albedo = "core/textures/common/checker_d.dds"
	Color albedo = [1 1 1 1]

	// optimization
	State static_shadow = true
	State vertex_velocity = false

	Shader vertex_struct =
	#{
		INIT_BASE_DATA
	#}

	Shader common =
	#{
		float3 sample_albedo(float2 uv)
		{
			return TEXTURE(tex_albedo, uv).rgb * var_albedo.rgb;
		}
	#}

	Shader fragment =
	#{
		OUT_FRAG_ALBEDO = sample_albedo(DATA_UV.xy);
		OUT_FRAG_SPECULAR = 0.5f;
		OUT_FRAG_ROUGHNESS = 1.0f;
		OUT_FRAG_METALNESS = 0.0f;
	#}
}

```

</details>
