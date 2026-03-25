# UUSL GBuffer Structure


G-buffer is a series of textures where all the visible information is written: albedo color, normals, lightmap, etc. G-buffer is used for [deferred rendering pipeline](../../principles/render/sequence/index.md).


UUSL has a handy *GBuffer* structure to fill it in the shader's code.


> **Notice:** Since main workflow in UNIGINE is metalness, it has different structure of G-buffer than specular workflow has.


## GBuffer Textures


GBuffer has the following set of textures:


| Texture name | Type | Description |
|---|---|---|
| Albedo | RGBA8 | **RGB** - albedo value. **A** - occlusion value. |
| Shading | RGBA8 | **R** - metalness value. **G** - F0 (specular) value. **B** - translucent value. **A** - microfiber value. |
| Normal | RGBA8 | **RGB** - normal value. **A** - roughness value. |
| Velocity | RG16F | **RG** - pixel displacement value (XY coordinates). |
| Material Mask | R32U | **R** - material mask value. |
| Lightmap | RG11B10F | **RGB** - lightmap value. |
| Geodetic Flat Position | RGBA32F | **RGBA** - lightmap value. |
| Features | RGBA8 | **R** - bevel value. **G** - cavity mask. **B** - convexity mask. |
| Depth Patch | RG32F | **R** - fragment depth. **G** - geometry depth. |


Channels of these textures fill the corresponding fields of the *[GBuffer](#GBuffer)* and *[GBufferSpecular](#GBufferSpecular)* structures.


## GBuffer Structures


## struct GBuffer

The *GBuffer* structure has a set of textures, the channels of which fill in the specified fields.
### Fields

- *float3* **albedo** - Albedo color value.
- *float* **transparent** - Alpha value for Alpha Test and Alpha Blend materials.
- *float* **metalness** - Metalness value.
- *float* **roughness** - Roughness value.
- *float* **f0** - Specular value.
- *float* **microfiber** - Microfiber value.
- *float3* **normal** - Packed GBuffer normal in view space.
- *float* **translucent** - Translucent value.
- *float2* **velocity** - Pixel displacement value (XY coordinates).
- *float3* **lightmap** - **RGB** - lightmap value.
- *float* **occlusion** - Occlusion value.
- *float* **bevel** - Bevel value.
- *float2* **curvature** - Curvature values: R - cavity, G - convexity.
- *int* **material_mask** - Material mask value.
- *float* **depth_patch** - Fragment depth.


## struct GBufferSpecular

The *Specular GBuffer* structure has a set of textures, the channels of which fill in the specified fields. To convert *Specular GBuffer* to *Metalness GBuffer*, use the *[specularToMetalness()](#specularToMetalness_GBufferSpecular)* function.
### Fields

- *float3* **diffuse** - Diffuse surface color.
- *float* **transparent** - Alpha value for Alpha Test and Alpha Blend materials.
- *float3* **specular** - Specular surface color.
- *float* **gloss** - Surface glossiness.
- *float* **microfiber** - Microfiber value.
- *float3* **normal** - Packed GBuffer normal in view space.
- *float* **translucent** - Translucent value.
- *float2* **velocity** - Pixel displacement value (XY coordinates).
- *float3* **lightmap** - **RGB** - lightmap value.
- *float* **occlusion** - Occlusion value.
- *float* **bevel** - Bevel value.
- *float2* **curvature** - Curvature values: R - cavity, G - convexity.
- *int* **material_mask** - Material mask value.
- *float* **depth_patch** - Fragment depth.


## GBuffer Functions


## GBuffer GBufferDefault ( )

Default constructor for GBuffer structure for metalness workflow. It creates an instance with default (not null) values.
### Return value

GBuffer structure with default (not null) values.
## GBufferSpecular GBufferSpecularDefault ( )

Constructor for GBuffferSpecular structure for specular workflow. It creates an instance with default (not null) values.
### Return value

GBufferSpecular structure with default (not null) values.
## GBuffer specularToMetalness ( GBufferSpecular gbuffer )

Converts given specular GBufferSpecular to metalness Gbuffer.
### Arguments

- *GBufferSpecular* **gbuffer** - Specular GBufferSpecular instance to be converted.

### Return value

Metalness Gbuffer instance.
## void setGBuffer ( GBuffer gbuffer )

Sets GBuffer values by using corresponding values of given GBuffer instance.
### Arguments

- *GBuffer* **gbuffer** - GBuffer instance with necessary values to be set.


## void setGBuffer ( GBufferSpecular gbuffer )

Sets GBuffer values by using corresponding values of given GBufferSpecular instance.
Inside this method [*specularToMetalness()*](#specularToMetalness_GBufferSpecular) is called.
### Arguments

- *GBufferSpecular* **gbuffer** - GBufferSpecular instance with necessary values to be set.


## void loadGBufferAlbedo ( inout GBuffer gbuffer , Texture2D TEX_ALBEDO , float2 uv )

Loads albedo texture values (albedo color and occlusion) to GBuffer.
### Arguments

- *inout GBuffer* **gbuffer** - Gbuffer structure. Values will be written in it.
- *[Texture2D](/code/uusl/textures#texture_in_name)* **TEX_ALBEDO** - Albedo texture.
- *float2* **uv** - UV coordinates.


## void loadGBufferShading ( inout GBuffer gbuffer , Texture2D TEX_SHADING , float2 uv )

Loads shading texture values (metalness, f0, translucence, microfiber) to GBuffer.
### Arguments

- *inout GBuffer* **gbuffer** - Gbuffer structure. Values will be written in it.
- *[Texture2D](/code/uusl/textures#texture_in_name)* **TEX_SHADING** - Shading texture.
- *float2* **uv** - UV coordinates.


## void loadGBufferNormal ( inout GBuffer gbuffer , Texture2D TEX_NORMAL , float2 uv )

Loads normal texture values (normal and roughness) to GBuffer.
### Arguments

- *inout GBuffer* **gbuffer** - Gbuffer structure. Values will be written in it.
- *[Texture2D](/code/uusl/textures#texture_in_name)* **TEX_NORMAL** - Normal texture.
- *float2* **uv** - UV coordinates.


## float3 unpackGBufferNormal ( float3 normal )

Returns the normal unit vector into which the RGB normal is unpacked.
### Arguments

- *float3* **normal** - RGB8 normal.

### Return value

Normal unit vector.
## float3 unpackGBufferNormal ( float4 normal )

Returns the normal unit vector into which the RGB normal is unpacked.
### Arguments

- *float4* **normal**

### Return value

Normal unit vector.
## float3 packGBufferNormal ( float3 normal )

Returns the RGB8 vector, into which the normal unit vector is packed.
### Arguments

- *float3* **normal** - Normal unit vector.

### Return value

RGB8 normal.
## void gbufferSRGB ( GBuffer gbuffer )

Apples sRGB correction to albedo and F0.
### Arguments

- *GBuffer* **gbuffer** - GBuffer structure.


## Usage Example


### Defining the GBuffer Structure


To use GBuffer structure in your shader's code, you should define and initialize the GBuffer structure by using its constructors. For metalness worlkflow use *GBufferDefault()* constructor (for specular workflow you should use *GBufferSpecular* structure and *GBufferSpecularDefault()* constructor respectively).


The following example shows the way of creating GBuffer structure for both workflows by using *#ifdef #else #endif* preprocessor statements.


```glsl
/* ... */
	#ifdef METALNESS
		GBuffer gbuffer = GBufferDefault();
		#define GBUFFER gbuffer
	#else
		GBufferSpecular gbuffer_s = GBufferSpecularDefault();
		#define GBUFFER gbuffer_s
	#endif
/* ... */

```


> **Notice:** Defining the **GBUFFER** with *#define* directive is handy to get access to GBuffer structure, no matter what type of the workflow is used.


### Filling the GBuffer Structure


After defining and initializing the GBuffer structure (like in an example above), you can easily fill the GBuffer's fields. You can fill the specific channel of the GBuffer texture.


```glsl
/* ... */
	#ifdef METALNESS
		GBUFFER.albedo		= color.rgb;
		GBUFFER.metalness	= shading.r;
		GBUFFER.roughness	= shading.g;

	#else
		GBUFFER.diffuse		= color.rgb;
		GBUFFER.specular	= shading.rgb;
		GBUFFER.gloss		= shading.a;
		GBUFFER.microfiber	= m_microfiber;

	#endif
/* ... */

```


### Loading Textures to GBuffer Structure


Another way of filling the GBuffer structure is using GBuffer functions for textures loading.


In case of changing GBuffer structure fields, these loading functions will perform the same function, preventing possible errors during migration to another UNIGINE Engine version.


```glsl
// initialize textures
/* ... */
INIT_TEXTURE(1,TEX_NORMAL)
INIT_TEXTURE(2,TEX_ALBEDO)
INIT_TEXTURE(3,TEX_SHADING)
/* ... */

/* ... */
GBuffer gbuffer = GBufferDefault();
loadGBufferAlbedo(gbuffer, TEXTURE_OUT(TEX_ALBEDO),uv);
loadGBufferShading(gbuffer, TEXTURE_OUT(TEX_SHADING),uv);
loadGBufferNormal(gbuffer, TEXTURE_OUT(TEX_NORMAL),uv);
/* ... */

```
