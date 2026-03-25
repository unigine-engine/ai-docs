# Unigine.Ffp Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


Interface for fixed function pipeline.


Ffp class in Unigine differs from the classic OpenGL FFP implementation. For example, Unigine [Visualizer](../../../code/console/index.md#visualizer) and [Texture Buffers for Debugging](../../../code/console/index.md#render_show_textures) are implemented by using Ffp. Ffp uses already implemented D3D12 and Vulkan shader programs (without creating materials, etc.) to render.


This interface enables to render basic geometric primitives. For example, it can be used to draw a project watermark.


### See Also


- C++ API sample located in the folder **<UnigineSDK>/source/samples/Api/Systems/Ffp**
- C# API sample located in the folder **<UnigineSDK>/source/csharp/samples/Api/Systems/Ffp**


## Ffp Class

### Members

---

## void addIndices ( )

Adds the specified array of indices to Ffp.
### Arguments

## void addVertex ( )

Adds the specified vertex array to Ffp.
### Arguments

## void setTextureSample ( int sample )

Sets a new texture sample flag.
### Arguments

- *int* **sample** - Texture sample flag to be set, one of the *[TEXTURE_SAMPLE_*](#TEXTURE_SAMPLE_2D)* values.

## int getTextureSample ( )

Returns the current texture sample flag.
### Return value

Current texture sample flag used, one of the *[TEXTURE_SAMPLE_*](#TEXTURE_SAMPLE_2D)* values.
