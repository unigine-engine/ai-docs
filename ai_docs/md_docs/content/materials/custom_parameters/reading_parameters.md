# Reading Parameters


Every read starts from a [Surface ID](../../../content/materials/custom_parameters/ids_and_buffers.md#ids), and there are two ways to get one:


- **From a buffer** - a post-effect, or any other pass running over the finished frame, reads the ID at the pixel it is shading.
- **From the draw call** - a material drawing a surface does not have to sample anything: the renderer supplies the ID of that surface directly.


One lookup by that ID returns the whole block: the values [declared](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#declare) for the surface, and the built-in fields the engine adds to it - the node, surface and instance numbers that identify the surface, the feature bits, and the Material ID. Looking that ID up the same way returns the values of the material.


Both a custom shader and a [material graph](../../../content/materials/graph/index.md) can perform that lookup, and this article describes each of them.


## In a Shader


The declared parameters are generated into a **SurfaceParameters** structure (and a **MaterialParameters** one), whose fields carry the names they were declared with. Alongside them each structure holds the built-ins the engine keeps there - the Material ID of the surface, the node, surface and instance numbers that identify it, the classic [material mask](../../../principles/bit_masking/index.md#material_mask) of the material, and the feature bits of each. *[Structures and Constants](../../../code/uusl/custom_parameters.md#types)* lists them field by field.


The feature bits record which rendering features are enabled for the surface or the material at that pixel, so an effect can include or skip those pixels instead of guessing. Each bit has a reader of its own, with overloads that take the bits, the whole block, an ID or pixel coordinates, so a check can start from whatever is at hand: **isSsaoBit(coord)** reads the Scene Buffer on its own, and **isSsaoBit(surface_id)** goes from the surface to the material behind it. These are exactly the extra output ports the [graph nodes](#shader_graph) expose.


The structures and the getters come with `core/materials/shaders/render/common.h`, the header that a [custom material](../../../content/materials/custom.md) includes anyway, so nothing has to be added for them. A post-effect pass that reads a parameter looks like this in full:


```glsl
#include <core/materials/shaders/render/common.h>

STRUCT_FRAG_BEGIN
	INIT_COLOR(float4)
STRUCT_FRAG_END

MAIN_FRAG_BEGIN(FRAGMENT_IN)

	SurfaceParameters params = getSceneSurfaceParameters(int2(IN_POSITION.xy));

	float gamma = 0.0f;
	if (isValidSurfaceParameters(params))
		gamma = params.gamma_offset;

	OUT_COLOR = float4(gamma, gamma, gamma, 1.0f);

MAIN_FRAG_END

```


Pixel coordinates come from **IN_POSITION.xy**, cast to int2. The surrounding shader API is described in [UUSL: GBuffer](../../../code/uusl/gbuffer.md), and [Custom Materials](../../../content/materials/custom.md) shows how to write the material this pass belongs to.


A getter hands over the whole structure, not one field of it: there is no shader-side way to fetch a single parameter, and no reason to look for one - reading five of them off **params** costs the same as reading one. The API setters and getters work the other way round, a value at a time.


The values of the material are reached from the same block, without sampling anything a second time, because the surface block carries the Material ID of its own material. *[Reading Both Blocks at One Pixel](../../../code/uusl/custom_parameters.md#usage)* writes that pair out in full.


Each buffer has its own set of getters. They all take pixel coordinates, so the buffer is read at the pixel asked for:


| Buffer | Getters |
|---|---|
| Opaque geometry | [getOpaque**SurfaceID**()](../../../code/uusl/custom_parameters.md#getOpaqueSurfaceID_int2), [getOpaque**SurfaceParameters**()](../../../code/uusl/custom_parameters.md#getOpaqueSurfaceParameters_int2), [getOpaqueSurface**MaterialID**()](../../../code/uusl/custom_parameters.md#getOpaqueSurfaceMaterialID_int2), [getOpaque**MaterialParameters**()](../../../code/uusl/custom_parameters.md#getOpaqueMaterialParameters_int2), [getOpaque**MaterialMask**()](../../../code/uusl/custom_parameters.md#getOpaqueMaterialMask_int2) |
| Transparent geometry | [getTransparent**SurfaceID**()](../../../code/uusl/custom_parameters.md#getTransparentSurfaceID_int2), [getTransparent**SurfaceParameters**()](../../../code/uusl/custom_parameters.md#getTransparentSurfaceParameters_int2), [getTransparentSurface**MaterialID**()](../../../code/uusl/custom_parameters.md#getTransparentSurfaceMaterialID_int2), [getTransparent**MaterialParameters**()](../../../code/uusl/custom_parameters.md#getTransparentMaterialParameters_int2), [getTransparent**MaterialMask**()](../../../code/uusl/custom_parameters.md#getTransparentMaterialMask_int2) |
| Decals | [getDecal**SurfaceID**()](../../../code/uusl/custom_parameters.md#getDecalSurfaceID_int2), [getDecal**SurfaceParameters**()](../../../code/uusl/custom_parameters.md#getDecalSurfaceParameters_int2), [getDecalSurface**MaterialID**()](../../../code/uusl/custom_parameters.md#getDecalSurfaceMaterialID_int2), [getDecal**MaterialParameters**()](../../../code/uusl/custom_parameters.md#getDecalMaterialParameters_int2), [getDecal**MaterialMask**()](../../../code/uusl/custom_parameters.md#getDecalMaterialMask_int2) |
| Water | [getWater**SurfaceID**()](../../../code/uusl/custom_parameters.md#getWaterSurfaceID_int2), [getWater**SurfaceParameters**()](../../../code/uusl/custom_parameters.md#getWaterSurfaceParameters_int2), [getWaterSurface**MaterialID**()](../../../code/uusl/custom_parameters.md#getWaterSurfaceMaterialID_int2), [getWater**MaterialParameters**()](../../../code/uusl/custom_parameters.md#getWaterMaterialParameters_int2) |
| The composed scene | [getScene**SurfaceID**()](../../../code/uusl/custom_parameters.md#getSceneSurfaceID_int2), [getScene**SurfaceParameters**()](../../../code/uusl/custom_parameters.md#getSceneSurfaceParameters_int2), [getSceneSurface**MaterialID**()](../../../code/uusl/custom_parameters.md#getSceneSurfaceMaterialID_int2), [getScene**MaterialParameters**()](../../../code/uusl/custom_parameters.md#getSceneMaterialParameters_int2), [getScene**MaterialMask**()](../../../code/uusl/custom_parameters.md#getSceneMaterialMask_int2) |


Water is the one buffer without a material mask getter - the row above is not missing an entry.


Two more getters take an ID instead of pixel coordinates, for code that already has one: [**getSurfaceParameters()**](../../../code/uusl/custom_parameters.md#getSurfaceParameters_SurfaceID) and [**getMaterialParameters()**](../../../code/uusl/custom_parameters.md#getMaterialParameters_MaterialID). The Opaque and Scene Buffers can additionally be read by UV, through [**getOpaqueSurfaceIDUV()**](../../../code/uusl/custom_parameters.md#getOpaqueSurfaceIDUV_float2) and [**getSceneSurfaceIDUV()**](../../../code/uusl/custom_parameters.md#getSceneSurfaceIDUV_float2); the other buffers have no UV variant.


> **Notice:** In the engine API, **getSurfaceParameters()** and **getMaterialParameters()** return the [layout](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#declare), the declaration itself, rather than a block of values. See *[UUSL Surface and Material Parameters](../../../code/uusl/custom_parameters.md)*.


Whether the Transparent and Water Buffers exist at all depends on [multilayered Surface ID](../../../content/materials/custom_parameters/ids_and_buffers.md#modes), so a shader that reads them can ask [**isTransparentSurfaceIDAvailable()**](../../../code/uusl/custom_parameters.md#isTransparentSurfaceIDAvailable) or [**isWaterSurfaceIDAvailable()**](../../../code/uusl/custom_parameters.md#isWaterSurfaceIDAvailable) first. [**isDecalSurfaceIDAvailable()**](../../../code/uusl/custom_parameters.md#isDecalSurfaceIDAvailable) and [**isSceneSurfaceIDAvailable()**](../../../code/uusl/custom_parameters.md#isSceneSurfaceIDAvailable) exist for symmetry and always return true.


Such a check answers about the configuration, not about this frame. A buffer can exist and still receive nothing: the mode is on, but the frame holds no transparent surface, or no decal has *Write Surface ID* enabled. Such a buffer reads **SURFACE_ID_NONE** at every pixel, exactly as a buffer that does not exist does. Both cases give back a block of zeros, so the check to write per pixel is [**isValidSurfaceParameters()**](../../../code/uusl/custom_parameters.md#isValidSurfaceParameters_SurfaceParameters); the availability check only saves the sampling.


Every function named above is described argument by argument in *[UUSL Surface and Material Parameters](../../../code/uusl/custom_parameters.md)*, which also covers the *[defines](../../../code/uusl/custom_parameters.md#defines)* the renderer generates the structures through - what a shader has to guard on if it must compile whether or not the project declares anything, and how it can tell at compile time which buffers the current configuration provides.


## In Material Graph


The same data is available in [Material Editor](../../../content/materials/graph/index.md) as a family of nodes:


- *[Surface Parameters](../../../content/materials/graph/node_library/input/surface_parameters.md)* and *[Material Parameters](../../../content/materials/graph/node_library/input/material_parameters.md)* - read the block that belongs to the pixel being shaded. The buffer is chosen in the *Type* property of the node.
- *[Material Parameters by ID](../../../content/materials/graph/node_library/input/material_parameters_by_id.md)* - the same for a material, but the ID comes from an input port instead of a buffer.
- *[Current Surface Parameters](../../../content/materials/graph/node_library/input/current_surface_parameters.md)* - the block of the surface being shaded, taken from the ID the renderer supplies with the draw call. It is the one node unavailable in a post-effect graph, which has no current surface.
- *[Surface ID Rendering Mode](../../../content/materials/graph/node_library/input/surface_id_rendering_mode.md)* - four boolean outputs for a graph that has to adapt to the buffers the current configuration provides.


Besides the declared parameters, every one of these nodes exposes the built-ins of the block as ports of its own - *Node ID*, *Surface*, *Instance* and *Material ID* on a surface node, *Material Mask* on a material one, and on each the [feature bits](#shader_uusl) of that block. The pages above show each node and list them port by port.
