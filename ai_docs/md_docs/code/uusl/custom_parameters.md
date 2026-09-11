# UUSL Surface and Material Parameters


This article is the shader-side reference for [custom parameters of surfaces and materials](../../content/materials/custom_parameters/index.md): the structures the declared parameters are generated into, the functions that read them out of the Surface ID Buffers, and the defines the renderer supplies along with them.


Everything below comes with `core/materials/shaders/api/common.h`:


```glsl
#include <core/materials/shaders/api/common.h>
```


A [custom material](../../content/materials/custom.md) includes `core/materials/shaders/render/common.h`, which pulls that header in, so nothing has to be added for it there.


> **Notice:** **getSurfaceParameters()** and **getMaterialParameters()** mean one thing here and another in the engine API. In a shader they return a block of values for one ID. As *[*Render::getSurfaceParameters()*](../../api/library/rendering/class.render_cpp.md#SurfaceParameters)* and *[*Materials::getMaterialParameters()*](../../api/library/rendering/class.materials_cpp.md#MaterialParameters)* they return the [layout](../../content/materials/custom_parameters/declaring_and_setting_cpp.md#declare) - the declaration itself.


## Defines


The declarations are not something a shader includes - the renderer turns them into defines and compiles every shader against them. Which defines are there therefore depends on what the project declares and on how the renderer is configured, and a shader can adapt to that at compile time.


| Define | What it holds |
|---|---|
| SURFACE_PARAMETERS_STRUCT_BODY | The generated body of the **SurfaceParameters** structure - the built-in fields, then one field per declared surface parameter, named exactly as it was declared and typed as it was declared |
| MATERIAL_PARAMETERS_STRUCT_BODY | The same for **MaterialParameters** |
| SURFACE_PARAMETERS_STRUCT_SIZE | Size of one surface block in bytes - the same number the API reports as *[*getStructureSize()*](../../api/library/common/class.customparameterlayout_cpp.md#StructureSize)* |
| MATERIAL_PARAMETERS_STRUCT_SIZE | The same for one material block |
| SURFACE_ID_MULTILAYERED | Defined while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on, and absent otherwise. Nothing is stored in it - what matters is whether it is there |


The two structure bodies are what the **SurfaceParameters** and **MaterialParameters** types are built from, and every function returning either of them is declared inside an **#ifdef** on them. A shader that has to compile in a configuration where they may be missing should guard its reads the same way:


```glsl
#ifdef SURFACE_PARAMETERS_STRUCT_BODY
	SurfaceParameters params = getSceneSurfaceParameters(int2(IN_POSITION.xy));
	// ...
#endif

```


> **Notice:** Declaring nothing does not remove the structure. The block always carries its built-in fields, so **SURFACE_PARAMETERS_STRUCT_BODY** is there even for a project that has declared no parameters at all - the structure simply holds the built-ins and nothing else.


**SURFACE_ID_MULTILAYERED** is what the per-stage getters are compiled against. Without it **getTransparentSurfaceID()** and **getWaterSurfaceID()** compile down to **SURFACE_ID_NONE**, the matching parameter getters return a block of zeros, and **isTransparentSurfaceIDAvailable()** and **isWaterSurfaceIDAvailable()** return false. A graph does the same check through the *[Surface ID Rendering Mode](../../content/materials/graph/node_library/input/surface_id_rendering_mode.md)* node.


> **Warning:** A declaration changes the generated structures, so shaders compiled against the old ones cannot read a newly declared parameter until the materials are reloaded. In *UnigineEditor* the *Save* button does that; from code it takes *[*Materials::reloadMaterials()*](../../api/library/rendering/class.materials_cpp.md#reloadMaterials_void)*.


## Structures and Constants


### SurfaceID and MaterialID


An ID is not a bare number but a small structure, so that the same three questions can be asked of it wherever it comes from:


| Member | What it answers |
|---|---|
| id | The number itself, as a uint |
| isValid() | A real surface or material, rather than one of the reserved values |
| isEmpty() | Nothing was written at that pixel |
| isSky() | The pixel is the sky |


The same three are available as free functions - [isValidSurfaceID()](#ref_ids) and its neighbours - for code that reads better that way.


The reserved values are constants of their own, and the two sets are separate: a constant of one should not be used with the other, even where the numbers currently coincide.


| Constant | Value | Meaning |
|---|---|---|
| SURFACE_ID_NONE / MATERIAL_ID_NONE | 0u | No surface or material, or none allocated |
| SURFACE_ID_SKY / MATERIAL_ID_SKY | 1u | The sky |
| SURFACE_ID_RESERVED_NUM / MATERIAL_ID_RESERVED_NUM | 2u | The first number a real surface or material can get; everything below it is reserved |


The same constants are available from the API, as *[*Render::SURFACE_ID*](../../api/library/rendering/class.render_cpp.md#SURFACE_ID)* and *[*Material::MATERIAL_ID*](../../api/library/rendering/class.material_cpp.md#MATERIAL_ID)*.


### SurfaceParameters and MaterialParameters


These two are generated from the declarations, so the parameters of the project appear in them as ordinary fields under the names they were declared with. Alongside them each structure carries the built-ins the engine keeps there.


The built-in fields of **SurfaceParameters**:


| Field | What it is |
|---|---|
| unigine_material_id | **MaterialID** of the material assigned to the surface - the link between the two blocks |
| unigine_feature_bits | **SurfaceFeatureBits**, which carries the lightmap bit |
| unigine_node_id | int identifying the node the surface belongs to |
| unigine_surface | int - the number of the surface within that node |
| unigine_instance | int - the number of the instance, for geometry drawn instanced |


And of **MaterialParameters**:


| Field | What it is |
|---|---|
| unigine_material_mask | uint - the classic [material mask](../../principles/bit_masking/index.md#material_mask) |
| unigine_feature_bits | **MaterialFeatureBits**, which carries the rendering-feature bits |


Those three numbers - node, surface and instance - are the reverse lookup from a pixel back to the object that owns it, and unlike a [Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#ids) they hold for as long as the world stays loaded.


> **Notice:** A block may also end in generated padding fields whose names start with an underscore, such as **_surface_tail_pad0**. They round the structure up to its stride and hold nothing. This is why a declared parameter [may not start with an underscore](../../content/materials/custom_parameters/declaring_and_setting_cpp.md#declare_names).


### Feature Bits


Feature bits record which rendering features are enabled at that pixel, so an effect can include or skip those pixels instead of guessing. They come in two structures - **SurfaceFeatureBits**, carrying the lightmap bit alone, and **MaterialFeatureBits**, carrying the rest:


- **isScreenSpaceShadowsBit()**, **isShorelineWetnessBit()**, **isMotionBlurBit()**, **isSsaoBit()**, **isSsrBit()**, **isSssBit()** and **isDofBit()** on the material bits;
- **isLightmapBit()** on the surface ones.


Each of them is also a free function with overloads for the bits, a whole block, an ID or pixel coordinates, so a check can start from whatever is at hand - see [Feature Bits](#ref_bits). The engine's own depth of field and motion blur judge a pixel this way. In a [material graph](../../content/materials/graph/index.md) the same bits are extra output ports of the parameter nodes.


## Reading Both Blocks at One Pixel


A pass that needs the values of the surface and of its material does not sample anything twice. One buffer read gives the surface block, and the material block follows from the Material ID that block already carries - which is what the **getMaterialParameters(SurfaceParameters)** overload is for.


A sensor view is the usual case: what a substance is like is stored on the material, and how this particular object deviates from it on the surface, as [Choosing Where a Value Belongs](../../content/materials/custom_parameters/index.md#choosing) describes. The pass adds the two up:


```glsl
#include <core/materials/shaders/api/common.h>

STRUCT_FRAG_BEGIN
	INIT_COLOR(float4)
STRUCT_FRAG_END

MAIN_FRAG_BEGIN(FRAGMENT_IN)

	int2 coord = int2(IN_POSITION.xy);

	// one buffer read: the surface drawn at this pixel
	SurfaceParameters surface = getSceneSurfaceParameters(coord);

	float gamma = 0.0f;
	if (isValidSurfaceParameters(surface))
	{
		// no second buffer read: the block carries the Material ID of its own material
		MaterialParameters material = getMaterialParameters(surface);

		// the substance answers, the object corrects
		gamma = material.radar_gamma_db + surface.gamma_offset;

		// the built-ins are in the same block, already read
		if (surface.unigine_node_id == selected_node)
			gamma += highlight_boost;
	}

	OUT_COLOR = float4(gamma, gamma, gamma, 1.0f);

MAIN_FRAG_END

```


Both blocks are kept in local variables and read from as often as needed. A getter always returns the whole structure, so fetching five values off **surface** costs exactly what fetching one does, and calling **getSceneSurfaceParameters()** again for another parameter would only repeat work already done. The API setters and getters work the other way round, a value at a time.


**isValidSurfaceParameters()** is the check to write per pixel. It rejects the block of zeros that comes back where nothing was written - a pixel of the sky, or a buffer that exists but received nothing this frame - and an availability check does not replace it, since that one answers about the configuration rather than about this pixel.


> **Notice:** Reading through the Scene Buffer works whatever the [Multilayered](../../content/materials/custom_parameters/ids_and_buffers.md#modes) setting is, which is why it is the default choice. The per-stage buffers are for a pass that has to read one pixel layer by layer - the Transparent Buffer giving the windscreen, the Opaque one the driver behind it.


The same pair of reads is available in a [material graph](../../content/materials/graph/index.md) as the *[Surface Parameters](../../content/materials/graph/node_library/input/surface_parameters.md)* and *[Material Parameters](../../content/materials/graph/node_library/input/material_parameters.md)* nodes - see [In Material Graph](../../content/materials/custom_parameters/reading_parameters.md#shader_graph).


## Reading a Surface ID from a Buffer


Every one of these takes the coordinates of a pixel and answers with the Surface ID written there. Which buffers exist depends on the [Multilayered](../../content/materials/custom_parameters/ids_and_buffers.md#modes) setting.


## SurfaceID getOpaqueSurfaceID ( int2 coord )

Reads the **Opaque Buffer** - the Surface ID plane of the G-buffer, which opaque geometry always writes - at the given pixel.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Surface ID written at that pixel, or **SURFACE_ID_NONE** if nothing was written there.
## SurfaceID getTransparentSurfaceID ( int2 coord )


Reads the **Transparent Buffer** - the buffer alpha-blend geometry and particles write into - at the given pixel.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on. Without it there is no such buffer, and the function returns **SURFACE_ID_NONE** at every pixel.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Surface ID written at that pixel, or **SURFACE_ID_NONE** if nothing was written there.
## SurfaceID getDecalSurfaceID ( int2 coord )

Reads the **Decal Buffer** - the buffer decals write into - at the given pixel.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Surface ID written at that pixel, or **SURFACE_ID_NONE** if nothing was written there.
## SurfaceID getWaterSurfaceID ( int2 coord )


Reads the **Water Buffer** - the buffer water writes into - at the given pixel.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on. Without it there is no such buffer, and the function returns **SURFACE_ID_NONE** at every pixel.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Surface ID written at that pixel, or **SURFACE_ID_NONE** if nothing was written there.
## SurfaceID getSceneSurfaceID ( int2 coord )

Reads the **Scene Buffer** - every category composited into one - at the given pixel.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Surface ID written at that pixel, or **SURFACE_ID_NONE** if nothing was written there.
## SurfaceID getOpaqueSurfaceIDUV ( float2 uv )

The same as **getOpaqueSurfaceID()**, addressed by texture coordinates instead of pixel ones, for a pass that does not run at the resolution of the buffer. Only the Opaque and the Scene Buffers have this variant.
### Arguments

- *float2* **uv** - Texture coordinates of the pixel, in the 0 to 1 range.

### Return value

Surface ID written at that pixel, or **SURFACE_ID_NONE** if nothing was written there.
## SurfaceID getSceneSurfaceIDUV ( float2 uv )

The same as **getSceneSurfaceID()**, addressed by texture coordinates instead of pixel ones, for a pass that does not run at the resolution of the buffer. Only the Opaque and the Scene Buffers have this variant.
### Arguments

- *float2* **uv** - Texture coordinates of the pixel, in the 0 to 1 range.

### Return value

Surface ID written at that pixel, or **SURFACE_ID_NONE** if nothing was written there.
## bool isTransparentSurfaceIDAvailable ( )


Reports whether transparent geometry has a Surface ID Buffer of its own in the current configuration.


An availability check answers about the configuration, not about this frame. A buffer that exists but received nothing reads **SURFACE_ID_NONE** everywhere, so per-pixel code still has to check the block it gets with **isValidSurfaceParameters()**.


### Return value

true while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on, false otherwise.
## bool isDecalSurfaceIDAvailable ( )


Decals read and write the Surface ID in the same pass, so they cannot share a target with the geometry underneath and always get a buffer of their own. The function exists for symmetry with the other stages.


An availability check answers about the configuration, not about this frame. A buffer that exists but received nothing reads **SURFACE_ID_NONE** everywhere, so per-pixel code still has to check the block it gets with **isValidSurfaceParameters()**.


### Return value

Always true.
## bool isWaterSurfaceIDAvailable ( )


Reports whether water has a Surface ID Buffer of its own in the current configuration.


An availability check answers about the configuration, not about this frame. A buffer that exists but received nothing reads **SURFACE_ID_NONE** everywhere, so per-pixel code still has to check the block it gets with **isValidSurfaceParameters()**.


### Return value

true while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on, false otherwise.
## bool isSceneSurfaceIDAvailable ( )


The Scene Buffer exists in either mode. The function exists for symmetry with the other stages.


An availability check answers about the configuration, not about this frame. A buffer that exists but received nothing reads **SURFACE_ID_NONE** everywhere, so per-pixel code still has to check the block it gets with **isValidSurfaceParameters()**.


### Return value

Always true.
## Checking an ID


The free-function form of the checks the [ID structures](#types_ids) carry as members.


## bool isValidSurfaceID ( SurfaceID surface_id )

Checks that the ID is not one of the reserved values, that is, that it is at least **SURFACE_ID_RESERVED_NUM**.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if the ID belongs to a real surface.
## bool isEmptySurfaceID ( SurfaceID surface_id )

Checks whether the ID means "nothing here" - no surface was drawn at the pixel, or none was allocated.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if the ID is **SURFACE_ID_NONE**.
## bool isSkySurfaceID ( SurfaceID surface_id )

Checks whether the pixel is the sky.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if the ID is **SURFACE_ID_SKY**.
## bool isValidMaterialID ( MaterialID material_id )

Checks that the ID is not one of the reserved values, that is, that it is at least **MATERIAL_ID_RESERVED_NUM**.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if the ID belongs to a real material.
## bool isEmptyMaterialID ( MaterialID material_id )

Checks whether the ID means "nothing here" - no material was drawn at the pixel, or none was allocated.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if the ID is **MATERIAL_ID_NONE**.
## bool isSkyMaterialID ( MaterialID material_id )

Checks whether the pixel is the sky.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if the ID is **MATERIAL_ID_SKY**.
## SurfaceID toSurfaceID ( uint id )

Wraps a raw number into the ID type, for code that has an ID as a plain uint.
### Arguments

- *uint* **id** - Raw number to wrap.

### Return value

The number wrapped into a **SurfaceID**.
## MaterialID toMaterialID ( uint id )

Wraps a raw number into the ID type, for code that has an ID as a plain uint.
### Arguments

- *uint* **id** - Raw number to wrap.

### Return value

The number wrapped into a **MaterialID**.
## Reading Surface Parameters


A block can be looked up by an ID that is already at hand, or read straight out of a buffer at a pixel.


## SurfaceParameters getSurfaceParameters ( SurfaceID surface_id )

Looks the surface parameter block up by an ID that is already at hand, without sampling any buffer.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

The whole block of that surface: every declared parameter, plus the built-in fields.
## SurfaceParameters getOpaqueSurfaceParameters ( int2 coord )

Reads the **Opaque Buffer** at the given pixel and returns the parameter block of the surface found there. The same as **getSurfaceParameters(getOpaqueSurfaceID(coord))**.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the surface drawn at that pixel, or a block of zeros if no ID was written there.
## SurfaceParameters getTransparentSurfaceParameters ( int2 coord )


Reads the **Transparent Buffer** at the given pixel and returns the parameter block of the surface found there. The same as **getSurfaceParameters(getTransparentSurfaceID(coord))**.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on. Without it the function returns a block filled with zeros, which **isValidSurfaceParameters()** rejects.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the surface drawn at that pixel, or a block of zeros if no ID was written there.
## SurfaceParameters getDecalSurfaceParameters ( int2 coord )

Reads the **Decal Buffer** at the given pixel and returns the parameter block of the surface found there. The same as **getSurfaceParameters(getDecalSurfaceID(coord))**.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the surface drawn at that pixel, or a block of zeros if no ID was written there.
## SurfaceParameters getWaterSurfaceParameters ( int2 coord )


Reads the **Water Buffer** at the given pixel and returns the parameter block of the surface found there. The same as **getSurfaceParameters(getWaterSurfaceID(coord))**.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on. Without it the function returns a block filled with zeros, which **isValidSurfaceParameters()** rejects.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the surface drawn at that pixel, or a block of zeros if no ID was written there.
## SurfaceParameters getSceneSurfaceParameters ( int2 coord )

Reads the **Scene Buffer** at the given pixel and returns the parameter block of the surface found there. The same as **getSurfaceParameters(getSceneSurfaceID(coord))**.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the surface drawn at that pixel, or a block of zeros if no ID was written there.
## bool isValidSurfaceParameters ( SurfaceParameters params )

Tells a block that was actually read from a real surface apart from the block of zeros a buffer with nothing in it gives back. This is the check to write per pixel, before any value of the block is used.
### Arguments

- *SurfaceParameters* **params** - Surface parameter block that has already been read.

### Return value

true if the block belongs to a real surface.
## MaterialID getSurfaceMaterialID ( SurfaceID surface_id )

Goes from a surface to the material assigned to it. Every surface block carries the ID of its material, which is what makes reading both blocks at one pixel a single extra lookup.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

Material ID stored in the block of that surface.
## MaterialID getOpaqueSurfaceMaterialID ( int2 coord )

Reads the **Opaque Buffer** at the given pixel and returns the Material ID stored in the surface block found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Material ID of the surface drawn at that pixel.
## MaterialID getTransparentSurfaceMaterialID ( int2 coord )

Reads the **Transparent Buffer** at the given pixel and returns the Material ID stored in the surface block found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Material ID of the surface drawn at that pixel.
## MaterialID getDecalSurfaceMaterialID ( int2 coord )

Reads the **Decal Buffer** at the given pixel and returns the Material ID stored in the surface block found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Material ID of the surface drawn at that pixel.
## MaterialID getWaterSurfaceMaterialID ( int2 coord )

Reads the **Water Buffer** at the given pixel and returns the Material ID stored in the surface block found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Material ID of the surface drawn at that pixel.
## MaterialID getSceneSurfaceMaterialID ( int2 coord )

Reads the **Scene Buffer** at the given pixel and returns the Material ID stored in the surface block found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

Material ID of the surface drawn at that pixel.
## Reading Material Parameters


The same set for materials, plus the overload that takes a surface block and follows the Material ID inside it.


## MaterialParameters getMaterialParameters ( MaterialID material_id )

Looks the material parameter block up by an ID that is already at hand.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

The whole block of that material: every declared parameter, plus the built-in fields.
## MaterialParameters getMaterialParameters ( SurfaceParameters params )


Takes a surface block that has already been read and returns the block of its material, using the Material ID stored inside it.


This is the overload to use when a pass needs both blocks at one pixel: the buffer is sampled once for the surface block, and the material block follows from it without sampling anything again. See [Reading Both Blocks at One Pixel](#usage).


### Arguments

- *SurfaceParameters* **params** - Surface parameter block that has already been read.

### Return value

The block of the material the surface is made of.
## MaterialParameters getOpaqueMaterialParameters ( int2 coord )

Reads the **Opaque Buffer** at the given pixel, follows the Material ID of the surface found there, and returns the block of that material.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the material drawn at that pixel, or a block of zeros if no ID was written there.
## MaterialParameters getTransparentMaterialParameters ( int2 coord )


Reads the **Transparent Buffer** at the given pixel, follows the Material ID of the surface found there, and returns the block of that material.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on. Without it the function returns a block filled with zeros.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the material drawn at that pixel, or a block of zeros if no ID was written there.
## MaterialParameters getDecalMaterialParameters ( int2 coord )

Reads the **Decal Buffer** at the given pixel, follows the Material ID of the surface found there, and returns the block of that material.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the material drawn at that pixel, or a block of zeros if no ID was written there.
## MaterialParameters getWaterMaterialParameters ( int2 coord )


Reads the **Water Buffer** at the given pixel, follows the Material ID of the surface found there, and returns the block of that material.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on. Without it the function returns a block filled with zeros.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the material drawn at that pixel, or a block of zeros if no ID was written there.
## MaterialParameters getSceneMaterialParameters ( int2 coord )

Reads the **Scene Buffer** at the given pixel, follows the Material ID of the surface found there, and returns the block of that material.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The block of the material drawn at that pixel, or a block of zeros if no ID was written there.
## uint getOpaqueMaterialMask ( int2 coord )

A shortcut for the **unigine_material_mask** field of the material block read through the **Opaque Buffer**. Water has no variant of this function.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The classic [material mask](../../principles/bit_masking/index.md#material_mask) of the material drawn at that pixel.
## uint getTransparentMaterialMask ( int2 coord )

A shortcut for the **unigine_material_mask** field of the material block read through the **Transparent Buffer**. Water has no variant of this function.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The classic [material mask](../../principles/bit_masking/index.md#material_mask) of the material drawn at that pixel.
## uint getDecalMaterialMask ( int2 coord )

A shortcut for the **unigine_material_mask** field of the material block read through the **Decal Buffer**. Water has no variant of this function.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The classic [material mask](../../principles/bit_masking/index.md#material_mask) of the material drawn at that pixel.
## uint getSceneMaterialMask ( int2 coord )

A shortcut for the **unigine_material_mask** field of the material block read through the **Scene Buffer**. Water has no variant of this function.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

The classic [material mask](../../principles/bit_masking/index.md#material_mask) of the material drawn at that pixel.
## Feature Bits


Each bit has a reader with overloads for the bits, a whole block, an ID or pixel coordinates, so a check can start from whatever is at hand. The variants with a stage in the name read that stage's buffer instead of the Scene one.


## bool isLightmapBit ( SurfaceFeatureBits feature_bits )

Checks the lightmap bit of feature bits taken from a surface block. It is the only bit the surface block carries; all the others belong to the material one.
### Arguments

- *SurfaceFeatureBits* **feature_bits** - Feature bits taken from a surface parameter block.

### Return value

true if the surface uses a lightmap.
## bool isLightmapBit ( SurfaceParameters params )

The same check on a surface block that has already been read.
### Arguments

- *SurfaceParameters* **params** - Surface parameter block that has already been read.

### Return value

true if the surface uses a lightmap.
## bool isLightmapBit ( SurfaceID surface_id )

The same check, reading the block of the given Surface ID first.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if the surface uses a lightmap.
## bool isOpaqueLightmapBit ( int2 coord )

The same check, reading the Opaque Buffer at the given pixel first.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if the surface drawn at that pixel uses a lightmap.
## bool isScreenSpaceShadowsBit ( MaterialFeatureBits feature_bits )

Checks the screen-space shadows bit of feature bits taken from a material block.
### Arguments

- *MaterialFeatureBits* **feature_bits** - Feature bits taken from a material parameter block.

### Return value

true if screen-space shadows is enabled for that material.
## bool isShorelineWetnessBit ( MaterialFeatureBits feature_bits )

Checks the shoreline wetness bit of feature bits taken from a material block.
### Arguments

- *MaterialFeatureBits* **feature_bits** - Feature bits taken from a material parameter block.

### Return value

true if shoreline wetness is enabled for that material.
## bool isMotionBlurBit ( MaterialFeatureBits feature_bits )

Checks the motion blur bit of feature bits taken from a material block.
### Arguments

- *MaterialFeatureBits* **feature_bits** - Feature bits taken from a material parameter block.

### Return value

true if motion blur is enabled for that material.
## bool isSsaoBit ( MaterialFeatureBits feature_bits )

Checks the SSAO bit of feature bits taken from a material block.
### Arguments

- *MaterialFeatureBits* **feature_bits** - Feature bits taken from a material parameter block.

### Return value

true if SSAO is enabled for that material.
## bool isSsrBit ( MaterialFeatureBits feature_bits )

Checks the SSR bit of feature bits taken from a material block.
### Arguments

- *MaterialFeatureBits* **feature_bits** - Feature bits taken from a material parameter block.

### Return value

true if SSR is enabled for that material.
## bool isSssBit ( MaterialFeatureBits feature_bits )

Checks the subsurface scattering bit of feature bits taken from a material block.
### Arguments

- *MaterialFeatureBits* **feature_bits** - Feature bits taken from a material parameter block.

### Return value

true if subsurface scattering is enabled for that material.
## bool isDofBit ( MaterialFeatureBits feature_bits )

Checks the depth of field bit of feature bits taken from a material block.
### Arguments

- *MaterialFeatureBits* **feature_bits** - Feature bits taken from a material parameter block.

### Return value

true if depth of field is enabled for that material.
## bool isScreenSpaceShadowsBit ( MaterialParameters params )

Checks the screen-space shadows bit of a material block that has already been read.
### Arguments

- *MaterialParameters* **params** - Material parameter block that has already been read.

### Return value

true if screen-space shadows is enabled for that material.
## bool isShorelineWetnessBit ( MaterialParameters params )

Checks the shoreline wetness bit of a material block that has already been read.
### Arguments

- *MaterialParameters* **params** - Material parameter block that has already been read.

### Return value

true if shoreline wetness is enabled for that material.
## bool isMotionBlurBit ( MaterialParameters params )

Checks the motion blur bit of a material block that has already been read.
### Arguments

- *MaterialParameters* **params** - Material parameter block that has already been read.

### Return value

true if motion blur is enabled for that material.
## bool isSsaoBit ( MaterialParameters params )

Checks the SSAO bit of a material block that has already been read.
### Arguments

- *MaterialParameters* **params** - Material parameter block that has already been read.

### Return value

true if SSAO is enabled for that material.
## bool isSsrBit ( MaterialParameters params )

Checks the SSR bit of a material block that has already been read.
### Arguments

- *MaterialParameters* **params** - Material parameter block that has already been read.

### Return value

true if SSR is enabled for that material.
## bool isSssBit ( MaterialParameters params )

Checks the subsurface scattering bit of a material block that has already been read.
### Arguments

- *MaterialParameters* **params** - Material parameter block that has already been read.

### Return value

true if subsurface scattering is enabled for that material.
## bool isDofBit ( MaterialParameters params )

Checks the depth of field bit of a material block that has already been read.
### Arguments

- *MaterialParameters* **params** - Material parameter block that has already been read.

### Return value

true if depth of field is enabled for that material.
## bool isScreenSpaceShadowsBit ( MaterialID material_id )

Reads the block of the given Material ID and checks the screen-space shadows bit in it.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if screen-space shadows is enabled for that material.
## bool isShorelineWetnessBit ( MaterialID material_id )

Reads the block of the given Material ID and checks the shoreline wetness bit in it.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if shoreline wetness is enabled for that material.
## bool isMotionBlurBit ( MaterialID material_id )

Reads the block of the given Material ID and checks the motion blur bit in it.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if motion blur is enabled for that material.
## bool isSsaoBit ( MaterialID material_id )

Reads the block of the given Material ID and checks the SSAO bit in it.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if SSAO is enabled for that material.
## bool isSsrBit ( MaterialID material_id )

Reads the block of the given Material ID and checks the SSR bit in it.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if SSR is enabled for that material.
## bool isSssBit ( MaterialID material_id )

Reads the block of the given Material ID and checks the subsurface scattering bit in it.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if subsurface scattering is enabled for that material.
## bool isDofBit ( MaterialID material_id )

Reads the block of the given Material ID and checks the depth of field bit in it.
### Arguments

- *MaterialID* **material_id** - Material ID to look the block up by.

### Return value

true if depth of field is enabled for that material.
## bool isScreenSpaceShadowsBit ( SurfaceID surface_id )

Goes from a Surface ID to the material behind it and checks the screen-space shadows bit in the material block.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if screen-space shadows is enabled for the material of that surface.
## bool isShorelineWetnessBit ( SurfaceID surface_id )

Goes from a Surface ID to the material behind it and checks the shoreline wetness bit in the material block.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if shoreline wetness is enabled for the material of that surface.
## bool isMotionBlurBit ( SurfaceID surface_id )

Goes from a Surface ID to the material behind it and checks the motion blur bit in the material block.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if motion blur is enabled for the material of that surface.
## bool isSsaoBit ( SurfaceID surface_id )

Goes from a Surface ID to the material behind it and checks the SSAO bit in the material block.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if SSAO is enabled for the material of that surface.
## bool isSsrBit ( SurfaceID surface_id )

Goes from a Surface ID to the material behind it and checks the SSR bit in the material block.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if SSR is enabled for the material of that surface.
## bool isSssBit ( SurfaceID surface_id )

Goes from a Surface ID to the material behind it and checks the subsurface scattering bit in the material block.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if subsurface scattering is enabled for the material of that surface.
## bool isDofBit ( SurfaceID surface_id )

Goes from a Surface ID to the material behind it and checks the depth of field bit in the material block.
### Arguments

- *SurfaceID* **surface_id** - Surface ID to look the block up by.

### Return value

true if depth of field is enabled for the material of that surface.
## bool isScreenSpaceShadowsBit ( int2 coord )

Reads the Scene Buffer at the given pixel on its own and checks the screen-space shadows bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if screen-space shadows is enabled for the material drawn at that pixel.
## bool isShorelineWetnessBit ( int2 coord )

Reads the Scene Buffer at the given pixel on its own and checks the shoreline wetness bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if shoreline wetness is enabled for the material drawn at that pixel.
## bool isMotionBlurBit ( int2 coord )

Reads the Scene Buffer at the given pixel on its own and checks the motion blur bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if motion blur is enabled for the material drawn at that pixel.
## bool isSsaoBit ( int2 coord )

Reads the Scene Buffer at the given pixel on its own and checks the SSAO bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if SSAO is enabled for the material drawn at that pixel.
## bool isSsrBit ( int2 coord )

Reads the Scene Buffer at the given pixel on its own and checks the SSR bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if SSR is enabled for the material drawn at that pixel.
## bool isSssBit ( int2 coord )

Reads the Scene Buffer at the given pixel on its own and checks the subsurface scattering bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if subsurface scattering is enabled for the material drawn at that pixel.
## bool isDofBit ( int2 coord )

Reads the Scene Buffer at the given pixel on its own and checks the depth of field bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if depth of field is enabled for the material drawn at that pixel.
## bool isSsrBitUV ( float2 uv )

The same as **isSsrBit(coord)**, addressed by texture coordinates, for a pass that does not run at the resolution of the buffer. SSR is the only bit with this variant.
### Arguments

- *float2* **uv** - Texture coordinates of the pixel, in the 0 to 1 range.

### Return value

true if SSR is enabled for the material drawn at that pixel.
## bool isOpaqueScreenSpaceShadowsBit ( int2 coord )

Reads the **Opaque Buffer** at the given pixel instead of the Scene Buffer, and checks the screen-space shadows bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if screen-space shadows is enabled for the material drawn at that pixel.
## bool isOpaqueShorelineWetnessBit ( int2 coord )

Reads the **Opaque Buffer** at the given pixel instead of the Scene Buffer, and checks the shoreline wetness bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if shoreline wetness is enabled for the material drawn at that pixel.
## bool isOpaqueMotionBlurBit ( int2 coord )

Reads the **Opaque Buffer** at the given pixel instead of the Scene Buffer, and checks the motion blur bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if motion blur is enabled for the material drawn at that pixel.
## bool isOpaqueSsaoBit ( int2 coord )

Reads the **Opaque Buffer** at the given pixel instead of the Scene Buffer, and checks the SSAO bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if SSAO is enabled for the material drawn at that pixel.
## bool isOpaqueSsrBit ( int2 coord )

Reads the **Opaque Buffer** at the given pixel instead of the Scene Buffer, and checks the SSR bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if SSR is enabled for the material drawn at that pixel.
## bool isOpaqueSssBit ( int2 coord )

Reads the **Opaque Buffer** at the given pixel instead of the Scene Buffer, and checks the subsurface scattering bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if subsurface scattering is enabled for the material drawn at that pixel.
## bool isOpaqueDofBit ( int2 coord )

Reads the **Opaque Buffer** at the given pixel instead of the Scene Buffer, and checks the depth of field bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if depth of field is enabled for the material drawn at that pixel.
## bool isTransparentScreenSpaceShadowsBit ( int2 coord )


Reads the **Transparent Buffer** at the given pixel instead of the Scene Buffer, and checks the screen-space shadows bit of the material found there.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if screen-space shadows is enabled for the material drawn at that pixel.
## bool isTransparentShorelineWetnessBit ( int2 coord )


Reads the **Transparent Buffer** at the given pixel instead of the Scene Buffer, and checks the shoreline wetness bit of the material found there.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if shoreline wetness is enabled for the material drawn at that pixel.
## bool isTransparentMotionBlurBit ( int2 coord )


Reads the **Transparent Buffer** at the given pixel instead of the Scene Buffer, and checks the motion blur bit of the material found there.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if motion blur is enabled for the material drawn at that pixel.
## bool isTransparentSsaoBit ( int2 coord )


Reads the **Transparent Buffer** at the given pixel instead of the Scene Buffer, and checks the SSAO bit of the material found there.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if SSAO is enabled for the material drawn at that pixel.
## bool isTransparentSsrBit ( int2 coord )


Reads the **Transparent Buffer** at the given pixel instead of the Scene Buffer, and checks the SSR bit of the material found there.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if SSR is enabled for the material drawn at that pixel.
## bool isTransparentSssBit ( int2 coord )


Reads the **Transparent Buffer** at the given pixel instead of the Scene Buffer, and checks the subsurface scattering bit of the material found there.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if subsurface scattering is enabled for the material drawn at that pixel.
## bool isTransparentDofBit ( int2 coord )


Reads the **Transparent Buffer** at the given pixel instead of the Scene Buffer, and checks the depth of field bit of the material found there.


Available only while [multilayered Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#modes) is on.


### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if depth of field is enabled for the material drawn at that pixel.
## bool isDecalScreenSpaceShadowsBit ( int2 coord )

Reads the **Decal Buffer** at the given pixel instead of the Scene Buffer, and checks the screen-space shadows bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if screen-space shadows is enabled for the material drawn at that pixel.
## bool isDecalShorelineWetnessBit ( int2 coord )

Reads the **Decal Buffer** at the given pixel instead of the Scene Buffer, and checks the shoreline wetness bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if shoreline wetness is enabled for the material drawn at that pixel.
## bool isDecalMotionBlurBit ( int2 coord )

Reads the **Decal Buffer** at the given pixel instead of the Scene Buffer, and checks the motion blur bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if motion blur is enabled for the material drawn at that pixel.
## bool isDecalSsaoBit ( int2 coord )

Reads the **Decal Buffer** at the given pixel instead of the Scene Buffer, and checks the SSAO bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if SSAO is enabled for the material drawn at that pixel.
## bool isDecalSsrBit ( int2 coord )

Reads the **Decal Buffer** at the given pixel instead of the Scene Buffer, and checks the SSR bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if SSR is enabled for the material drawn at that pixel.
## bool isDecalSssBit ( int2 coord )

Reads the **Decal Buffer** at the given pixel instead of the Scene Buffer, and checks the subsurface scattering bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if subsurface scattering is enabled for the material drawn at that pixel.
## bool isDecalDofBit ( int2 coord )

Reads the **Decal Buffer** at the given pixel instead of the Scene Buffer, and checks the depth of field bit of the material found there.
### Arguments

- *int2* **coord** - Coordinates of the pixel to sample the buffer at - **IN_POSITION.xy** cast to int2 in a post-effect.

### Return value

true if depth of field is enabled for the material drawn at that pixel.
