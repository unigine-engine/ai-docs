# Parallax Functions


This documentation article contains information functions of the UUSL. This information can be used as the reference document for writing shaders.


To start using common UUSL functionality, include the `core/materials/shaders/api/parallax.h` file.


```glsl
#include <core/materials/shaders/api/parallax.h>
```


## Parallax Structures


## struct ParallaxIn

Parallax occlusion mapping input structure containing vital information.
### Fields

- *float3* **view_ts** - Normalized view direction in tangent space.
- *float2* **uv** - Texture UV coordinates.
- *float* **max_layers** - Parallax occlusion maximum steps. Recommended value: **[1, 64]**.
- *float* **min_layers** - Parallax occlusion minimum steps. Recommended value: **[1, 64]**.
- *float* **noise** - Size of the noise used for parallax mapping. Recommended value: **[0, 2]**.
- *float* **scale** - Parallax height map offset scale. Recommended value: **[0, 0.2]**.
- *float2* **screen_coord** - Screen-space coordinates.
- *float* **uv_aspect_ratio** - Aspect ratio of UV transform.


## struct Parallax

Parallax occlusion mapping output structure.
### Fields

- *float2* **uv** - UV modified by parallax occlusion mapping.
- *float2* **uv_offset** - UV delta.
- *float* **height** - Current pixel parallax occlusion mapping height.
- *float* **depth_offset** - Current pixel depth modifier.


## struct ParallaxShadowIn

Input data for the parallax occlusion shadowing.
### Fields

- *float3* **light_ts** - Normalized light direction in tangent space.
- *float* **max_layers** - Parallax occlusion maximum steps. Recommended value: **[1, 64]**.
- *float* **min_layers** - Parallax occlusion minimum steps. Recommended value: **[1, 64]**.
- *float* **noise** - Size of the noise used for parallax mapping. Recommended value: **[0, 2]**.
- *float* **intensity** - Shadow intensity. Recommended value: **[0, inf)**.
- *float* **softness** - Shadow softness. Recommended value: **[0, inf)**.
- *float* **visible** - Shadow visibility. Recommended value: **[0, 1]**.
- *float* **angle_visible** - Visibility angle.
- *float* **angle_visible_threshold** - Visibility angle threshold.


## Parallax Functions


## float4 parallaxCutoutUVTransform ( float4 parallax_uv_transform , float4 cutout_uv_transform )

Returns the UV transform for the cutout effect providing smooth edges between the opaque and transparent areas. The resulting UV transform is used as the cutout transform in the [parallaxOcclusionMapping()](#parallaxOcclusionMapping_ParallaxIn_float4_Texture2D) function.
### Arguments

- *float4* **parallax_uv_transform** - Parallax texture coordinates transformation: (X,Y) � scale, (Z,W) � offset.
- *float4* **cutout_uv_transform** - UV transform: (X,Y) � scale, (Z,W) � offset.

### Return value

Resulting UV transform: (X,Y) � scale, (Z,W) � offset.
## Parallax parallaxOcclusionMapping ( ParallaxIn data , float4 cutout_transform , Texture2D TEX_HEIGHT )

Returns the calculated parallax occlusion mapping data.
### Arguments

- *ParallaxIn* **data** - [Parallax occlusion mapping input data](#ParallaxIn).
- *float4* **cutout_transform** - [UV transform for the cutout effect](#parallaxCutoutUVTransform_float4_float4).
- *Texture2D* **TEX_HEIGHT** - 2D height texture.

### Return value

[Parallax occlusion mapping output data](#Parallax).
## Parallax parallaxOcclusionMapping ( ParallaxIn data , Texture2D TEX_HEIGHT )

Returns the calculated parallax occlusion mapping data.
### Arguments

- *ParallaxIn* **data** - [Parallax occlusion mapping input data](#ParallaxIn).
- *Texture2D* **TEX_HEIGHT** - 2D height texture.

### Return value

[Parallax occlusion mapping output data](#Parallax).
## float parallaxShadow ( ParallaxShadowIn data , ParallaxIn data_p , Parallax parallax , Texture2D TEX_HEIGHT )

Returns the calculated shadow value for the parallax occlusion mapping effect.
### Arguments

- *ParallaxShadowIn* **data** - [Input data for the parallax occlusion shadowing](#ParallaxShadowIn).
- *ParallaxIn* **data_p** - [Parallax occlusion mapping input data](#ParallaxIn).
- *Parallax* **parallax** - [Parallax occlusion mapping output data](#Parallax).
- *Texture2D* **TEX_HEIGHT** - 2D height texture.

### Return value

Shadow value.
## Usage Examples


### Basic


```glsl
BaseMaterial <parent=Unigine::mesh>
{
	// optimization
	State static_shadow = true
	State vertex_velocity = false
	State custom_depth = 1

	Group "Base"
	{
		Texture2D albedo = "core/textures/common/checker_d.texture"

		Color albedo = [1 1 1 1]
		Slider specular = 0.5f
		Slider translucent = 0.0f
		Slider roughness = 1.0f
		Slider metalness = 0.0f
	}

	Group "Parallax Occlusion Mapping"
	{
		Texture2D height = "core/textures/displacement_default.texture"

		Slider parallax_height = 0.1 <min=0 max=0.2>
		Slider parallax_min_layers = 1 <min=1 max=64>
		Slider parallax_max_layers = 16 <min=1 max=64>
	}

	Shader vertex_struct =
	#{
		INIT_BASE_DATA
	#}

	Shader common =
	#{
		// Include builtin Parallax Occlusion Mapping functionality
		#include <core/materials/shaders/api/parallax.h>
	#}

	Shader fragment =
	#{
		const float3x3 rotate_tangent_to_view = matrix3Col(DATA_TANGENT, DATA_BINORMAL, DATA_NORMAL);
		float3 view = positionToViewDirection(DATA_POSITION);


		// Fill GBuffer
		OUT_FRAG_ALBEDO = var_albedo.rgb;
		OUT_FRAG_SPECULAR = var_specular;
		OUT_FRAG_TRANSLUCENT = var_translucent;
		OUT_FRAG_ROUGHNESS = var_roughness;
		OUT_FRAG_METALNESS = var_metalness;

		float2 base_uv = DATA_UV.xy;

		// Fill neccessary data for the Parallax Occlusion Mapping
		ParallaxIn data;
		data.uv_aspect_ratio = 1.0f;
		data.screen_coord = IN_POSITION.xy;
		data.min_layers = var_parallax_min_layers;
		data.max_layers = var_parallax_max_layers;
		data.view_ts = -normalize(mul3(view, rotate_tangent_to_view));
		data.noise = 1.0f;
		data.scale = var_parallax_height;
		data.uv = base_uv;

		// Compute parallax occlusion mapping
		Parallax pom = parallaxOcclusionMapping(data, TEXTURE_OUT(tex_height));

		// Update base texture UV
		base_uv -= pom.uv_offset;

		// Apply albedo texture
		OUT_FRAG_ALBEDO *= TEXTURE(tex_albedo, base_uv).rgb;
	#}
}


```


### Advanced


```glsl
BaseMaterial <parent=Unigine::mesh>
{
	// optimization
	State static_shadow = true
	State vertex_velocity = false
	State custom_depth = 1

	Group "Base"
	{
		Texture2D albedo = "core/textures/common/checker_d.texture"
		UV uv_transform = [1 1 0 0]

		Slider albedo_detail_visibility = 0.5
		Texture2D albedo_detail = "core/textures/displacement_default.texture"
		UV detail_uv_transform = [10 10 0 0]

		Color albedo = [1 1 1 1]
		Slider specular = 0.5f
		Slider translucent = 0.0f
		Slider roughness = 1.0f
		Slider metalness = 0.0f
	}

	Group "Parallax Occlusion Mapping"
	{
		Texture2D height = "core/textures/displacement_default.texture"

		Slider parallax_height = 0.1 <min=0 max=0.2>
		Slider parallax_min_layers = 1 <min=1 max=64>
		Slider parallax_max_layers = 16 <min=1 max=64>

		State parallax_cutout = false
		Group "Cutout" if [parallax_cutout] <toggle_state=parallax_cutout>
		{
			UV parallax_uv_transform = [1 1 0 0]
		}

		State parallax_depth_cutout = false
		State parallax_shadow = false
	}

	Shader vertex_struct =
	#{
		INIT_BASE_DATA
	#}

	Shader common =
	#{
		// Include builtin Parallax Occlusion Mapping functionality
		#include <core/materials/shaders/api/parallax.h>
	#}

	Shader fragment =
	#{
		const float3x3 rotate_tangent_to_view = matrix3Col(DATA_TANGENT, DATA_BINORMAL, DATA_NORMAL);
		float3 view = positionToViewDirection(DATA_POSITION);


		// Fill GBuffer
		OUT_FRAG_ALBEDO = var_albedo.rgb;
		OUT_FRAG_SPECULAR = var_specular;
		OUT_FRAG_TRANSLUCENT = var_translucent;
		OUT_FRAG_ROUGHNESS = var_roughness;
		OUT_FRAG_METALNESS = var_metalness;

		float2 detail_uv = uvTransform(DATA_UV.xy, var_detail_uv_transform);
		float2 base_uv = uvTransform(DATA_UV.xy, var_uv_transform);

		// Fill neccessary data for the Parallax Occlusion Mapping
		ParallaxIn data;
		data.uv_aspect_ratio = var_uv_transform.y / var_uv_transform.x;
		data.screen_coord = IN_POSITION.xy;
		data.min_layers = var_parallax_min_layers;
		data.max_layers = var_parallax_max_layers;
		data.view_ts = -normalize(mul3(view, rotate_tangent_to_view));
		data.noise = 1.0f;
		data.scale = var_parallax_height;
		data.uv = base_uv;

		// Compute POM data
		#ifdef STATE_PARALLAX_CUTOUT
			float4 cutout_transform = parallaxCutoutUVTransform(var_parallax_uv_transform, var_uv_transform);
			Parallax pom = parallaxOcclusionMapping(data, cutout_transform, TEXTURE_OUT(tex_height));
			if (pom.height < -EPSILON)
				discard;
		#else
			Parallax pom = parallaxOcclusionMapping(data, TEXTURE_OUT(tex_height));
		#endif

		// Apply shadow from POM
		#ifdef STATE_PARALLAX_SHADOW
			ParallaxShadowIn data_shadow_in;
			data_shadow_in.max_layers = var_parallax_max_layers;
			data_shadow_in.min_layers = var_parallax_min_layers;
			data_shadow_in.noise = 1.0f;

			data_shadow_in.intensity = 0.5f;
			data_shadow_in.softness = 4.0f;

			data_shadow_in.visible = 1.0f;
			data_shadow_in.angle_visible = 0.5;
			data_shadow_in.angle_visible_threshold = 0.1;

			float3 light_dir_ws = mul3(s_scattering_sun_dir, s_imodelview);
			data_shadow_in.light_ts = normalize(mul(light_dir_ws, rotate_tangent_to_view));

			float shadow = parallaxShadow(data_shadow_in, data, pom, TEXTURE_OUT(tex_height));
			OUT_FRAG_ALBEDO *= shadow;
		#endif

		// Change depth buffer with POM's depth offset
		#ifdef STATE_PARALLAX_DEPTH_CUTOUT
			OUT_FRAG_DELTA_DEPTH = pom.depth_offset;
		#endif

		// Update base texture UV
		base_uv -= pom.uv_offset;

		// Update detail texture UV
		pom.uv_offset /= var_uv_transform.xy;
		detail_uv -= pom.uv_offset * var_detail_uv_transform.xy;


		// Apply albedo texture
		OUT_FRAG_ALBEDO *= TEXTURE(tex_albedo, base_uv).rgb;
		OUT_FRAG_ALBEDO += TEXTURE(tex_albedo_detail, detail_uv).rgb * var_albedo_detail_visibility;
	#}
}

```
