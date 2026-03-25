# Options


Fixed *options* of the material, their list cannot be changed. They are used to set custom values for common material options. The type of *ULON* node is *Option*.


The syntax is the following:


```cpp
Option option_name = value(s)

```


## Preprocessor Auto Generation for Shaders


You can access options in the shader using the following defines:


- `GET_OPTION_<`option name in uppercase> — available for all types of options.


| Option name | Option's define | Possible values |
|---|---|---|
| Transparent | GET_OPTION_TRANSPARENT | 0 — opaque (*default*) 1 — alpha test 2 — blend 3 — water |
| Order | GET_OPTION_ORDER | -128..127 0 — default order |
| Depth mask | GET_OPTION_DEPTH_MASK | 0 or 1 |
| Depth test | GET_OPTION_DEPTH_TEST | 0 or 1 |
| Two sided | GET_OPTION_TWO_SIDED | 0 or 1 |
| Cast shadow | GET_OPTION_CAST_PROJ_OMNI_SHADOW | 0 or 1 |
| Cast world shadow | GET_OPTION_CAST_WORLD_SHADOW | 0 or 1 |
| Overlap | GET_OPTION_OVERLAP | 0 or 1 |


- `OPTION_<`option name in uppercase> — defined only if an option has a positive value.


| Option name | Option's define | Additional define(s) |
|---|---|---|
| Transparent | OPTION_TRANSPARENT | 0 — OPAQUE 1 — ALPHA_TEST 2 — TRANSPARENT_BLEND 3 — TRANSPARENT_WATER |
| Order | OPTION_ORDER | — |
| Depth mask | OPTION_DEPTH_MASK | — |
| Depth test | OPTION_DEPTH_TEST | — |
| Two sided | OPTION_TWO_SIDED | 1 — TWO_SIDED |
| Cast shadow | OPTION_CAST_PROJ_OMNI_SHADOW | — |
| Cast world shadow | OPTION_CAST_WORLD_SHADOW | — |
| Overlap | OPTION_OVERLAP | 1 — OVERLAP_RENDER |


For various **blend** modes the *[source](#blend_src)* and *[destination](#blend_dest)* defines are generated:


```cpp
BLEND_SRC_FUNC_<source blend option name in uppercase>
BLEND_DEST_FUNC_<destination blend option name in uppercase>

// Examples
BLEND_SRC_FUNC_SRC_ALPHA
BLEND_DEST_FUNC_ONE_MINUS_SRC_ALPHA

```


## Usage Examples


```cpp
BaseMaterial
{
	Option depth_test  = false
	Option transparent = 2
	Option blend_src	= src_alpha
	Option blend_dest	= one_minus_src_alpha
}

```


## Arguments


> **Notice:** The argument names and values are case-sensitive.


### editable


***Boolean***


A flag indicating if option can be changed in the *[Parameters](../../../../editor2/materials_settings/index.md)* window or via [API](../../../../api/library/rendering/class.material_cpp.md).


Available values:


- false — unchangeable
- true — changeable (by default)


### hidden


***Boolean***


A flag indicating if option is displayed in the *[Parameters](../../../../editor2/materials_settings/index.md)* window.


Available values:


- false — displayed (by default)
- true — hidden


## Types of Options


### blend_src


***String***


A node that allows you to set a [blending](../../../../principles/render/blending/index.md) option value (only for transparent objects and decals). It is a source image representing polygon color.


Available values:


- zero — *RGBA* components of the source/destination image color are multiplied by zero.
- one — *RGBA* components of the source/destination image color are multiplied by one.
- src_color — *RGBA* components of the source/destination image color are multiplied by the mR, mG, mB, mA components (per component).
- one_minus_src_color — *RGBA* components of the source/destination image color are multiplied by the 1 - mR, 1 - mG, 1 - mB, 1 - mA components (per component).
- src_alpha — *RGBA* components of the source/destination image color are multiplied by the mA component.
- one_minus_src_alpha — *RGBA* components of the source/destination image color are multiplied by the 1 - mA component.
- dest_color — *RGBA* components of the source/destination image color are multiplied by the bR, bG, bB, bA components (per component).
- one_minus_dest_color — *RGBA* components of the source/destination image color are multiplied by the 1 - bR, 1 - bG, 1 - bB, 1 - bA components (per component).
- dest_alpha — *RGBA* components of the source/destination image color are multiplied by the bA component.
- one_minus_dest_alpha — *RGBA* components of the source/destination image color are multiplied by the 1 - bA component.


mR, mG, mB, mA are normalized Red, Blue, Green and Alpha material image channels;


bR, bG, bB, bA are normalized Red, Blue, Green and Alpha background image channels.


### blend_dest


***String***


A node that allows you to set a [blending](../../../../principles/render/blending/index.md) option value (only for transparent objects and decals). It is a destination image representing screen buffer color.


Available values:


- zero — *RGBA* components of the source/destination image color are multiplied by zero.
- one — *RGBA* components of the source/destination image color are multiplied by one.
- src_color — *RGBA* components of the source/destination image color are multiplied by the mR, mG, mB, mA components (per component).
- one_minus_src_color — *RGBA* components of the source/destination image color are multiplied by the 1 - mR, 1 - mG, 1 - mB, 1 - mA components (per component).
- src_alpha — *RGBA* components of the source/destination image color are multiplied by the mA component.
- one_minus_src_alpha — *RGBA* components of the source/destination image color are multiplied by the 1 - mA component.
- dest_color — *RGBA* components of the source/destination image color are multiplied by the bR, bG, bB, bA components (per component).
- one_minus_dest_color — *RGBA* components of the source/destination image color are multiplied by the 1 - bR, 1 - bG, 1 - bB, 1 - bA components (per component).
- dest_alpha — *RGBA* components of the source/destination image color are multiplied by the bA component.
- one_minus_dest_alpha — *RGBA* components of the source/destination image color are multiplied by the 1 - bA component.


mR, mG, mB, mA are normalized Red, Blue, Green and Alpha material image channels;


bR, bG, bB, bA are normalized Red, Blue, Green and Alpha background image channels.


### order


***Char***


[Rendering order](../../../../editor2/materials_settings/index.md#order) of the material. Specifies the priority of the material rendering (only for *[Object](../../../../api/library/objects/class.object_cpp.md)* and *[Decal](../../../../api/library/decals/class.decal_cpp.md)*).


Available values:


- -128 .. 127. The default value is 0. The higher the rendering order, the lower the rendering priority (the material with the -128 order will be rendered first).


### shadow_mask


***Integer***


A *[shadow](../../../../editor2/materials_settings/index.md#shadow_mask)* mask used to control shadows cast by an object lit by light sources (only for *[Object](../../../../api/library/objects/class.object_cpp.md)* and *[Decal](../../../../api/library/decals/class.decal_cpp.md)*).


Available values:


- Integer number, representing a mask. The default value is ~0.


### viewport_mask


***Integer***


A *[viewport](../../../../editor2/materials_settings/index.md#viewport_mask)* mask (only for *[Object](../../../../api/library/objects/class.object_cpp.md)* and *[Decal](../../../../api/library/decals/class.decal_cpp.md)*).


Available values:


- Integer number, representing a mask. The default value is ~0.


### depth_mask


***Boolean***


A flag indicating if writing in the [depth buffer](../../../../editor2/materials_settings/index.md#depth_write) is enabled for a material (only for *[Object](../../../../api/library/objects/class.object_cpp.md)*).


Available values:


- false — not used
- true — used (by default)


### depth_test


***Boolean***


A flag indicating if the *[Depth Test](../../../../editor2/materials_settings/index.md#depth_test)* option is enabled for a material (only for *[Object](../../../../api/library/objects/class.object_cpp.md)*).


Available values:


- false — disabled
- true — enabled (by default)


### two_sided


***Boolean***


A flag indicating if the *[Two Sided](../../../../editor2/materials_settings/index.md#two_sided)* option is enabled for a material (only for *[Object](../../../../api/library/objects/class.object_cpp.md)*).


Available values:


- false — disabled (by default)
- true — enabled


### cast_shadow


***Boolean***


A flag indicating if the *[Cast Proj and Omni Shadow](../../../../editor2/materials_settings/index.md#cast_shadow)* option is enabled for a material (only for *[Object](../../../../api/library/objects/class.object_cpp.md)*).


Available values:


- false — disabled
- true — enabled (by default)


### cast_world_shadow


***Boolean***


A flag indicating if the *[Cast World shadow](../../../../editor2/materials_settings/index.md#cast_world_shadow)* option is enabled for a material (only for *[Object](../../../../api/library/objects/class.object_cpp.md)*).


Available values:


- false — disabled
- true — enabled (by default)


### transparent


Indicates how and when an object with this material will be rendered (only for *[Object](../../../../api/library/objects/class.object_cpp.md)*). A lower value gives a higher priority in the rendering queue.


Available values:


**Integer**


- 0 = `TRANSPARENT_NONE` — opaque geometry that renders in deferred pass into GBuffer
- 1 = `TRANSPARENT_ALPHA_TEST` — opaque geometry with enabled alpha test that renders in the deferred pass into *GBuffer*
- 2 = `TRANSPARENT_BLEND` — transparent geometry that renders in forward passes
- 3 = `TRANSPARENT_WATER` — water objects that renders in the deferred pass


or a **String**


- none = TRANSPARENT_NONE
- alpha_test = TRANSPARENT_ALPHA_TEST
- blend = TRANSPARENT_BLEND
- water = TRANSPARENT_WATER


### overlap


***Boolean***


A flag indicating if the *[Overlap](../../../../editor2/materials_settings/index.md#overlap)* option is enabled for a material (only for *[Object](../../../../api/library/objects/class.object_cpp.md)*). This can be used for UI elements.


Available values:


- false — disabled (by default)
- true — enabled
