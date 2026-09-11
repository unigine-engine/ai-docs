# Unigine.RenderTarget Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


A container to which an image is rendered (a [framebuffer](https://en.wikipedia.org/wiki/Framebuffer) abstraction).


## RenderTarget Class

### Members

## int isCompleted () const

Returns the current value indicating if the render target is completed.
### Return value

Current render target is completed
## int isEnabled () const

Returns the current value indicating if the render target is enabled.
### Return value

Current render target is enabled
---

## static RenderTarget ( )

Constructor. Creates a new render target.
## void destroy ( )

Destroys the render target.
## void enable ( )

Enables the render target.
## void enableCompute ( )

Enables the render target with the use of compute shader output.
## void disable ( )

Disables the render target.
## void flush ( )

Flushes the render target.
## Texture getColorTexture ( int slot )

Returns a color texture by the specified slot.
### Arguments

- *int* **slot** - Texture slot.

### Return value

Color texture if it exists, otherwise NULL.
## void bindColorTexture ( int slot , Texture texture )

Binds all layers and faces (if supported by the texture type) of a texture on the 0 mip level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Color texture to be bound.

## void bindColorTexture2D ( int slot , Texture texture , int mip = 0 )

Binds the specified slot of a 2D texture on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - 2D color texture to be bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindColorTexture2DArray ( int slot , Texture texture , int layer = -1 , int mip = 0 )

Binds the specified slot and layer of a 2D texture array on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - 2D color texture array to be bound.
- *int* **layer** - Number of the 2D texture array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindColorTextureCube ( int slot , Texture texture , int face = -1 , int mip = 0 )

Binds the specified slot and face of a texture cube on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Color texture cube to be bound.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindColorTextureCubeArray ( int slot , Texture texture , int layer = -1 , int face = -1 , int mip = 0 )

Binds the specified layer and face of a texture cube array on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Color cube array texture to be bound.
- *int* **layer** - Number of the texture cube array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindColorTexture3D ( int slot , Texture texture , int depth = -1 , int mip = 0 )

Binds the specified depth layer of a 3D texture on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - 3D Color texture to be bound.
- *int* **depth** - 3D texture depth layer. With the default value of -1, all depth layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void unbindColorTexture ( int slot )

Unbinds a render target texture from the specified slot.
### Arguments

- *int* **slot** - Texture slot.

## void unbindColorTextures ( )

Unbinds all render target textures from a render target.
## Texture getDepthTexture ( )

Returns the depth texture.
### Return value

Depth texture if it exists, otherwise NULL.
## void bindDepthTexture ( Texture texture )

Binds all layers and faces (if supported by the texture type) of a texture on the 0 mip level to the specified slot as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Depth texture to be bound.

## void bindDepthTextureReadOnly ( Texture texture )

Binds a depth texture as a read-only depth render target (such as depth test), and at the same time allows using this texture as a shader resource in the shader.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Depth texture to be bound.

## void bindDepthTexture2D ( Texture texture , int mip = 0 )

Binds a 2D depth texture on the specified mipmap level as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - 2D depth texture to be bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindDepthTexture2DArray ( Texture texture , int layer = -1 , int mip = 0 )

Binds the specified layer of a depth texture on the specified mipmap level as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - 2D depth texture array to be bound.
- *int* **layer** - Number of the 2D depth texture array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindDepthTextureCube ( Texture texture , int face = -1 , int mip = 0 )

Binds the specified face of a depth texture cube on the specified mipmap level as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Depth texture cube to be bound.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindDepthTextureCubeArray ( Texture texture , int layer = -1 , int face = -1 , int mip = 0 )

Binds the specified layer and face of a depth texture cube array on the specified mipmap level as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Depth texture cube array to be bound.
- *int* **layer** - Number of the texture cube array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void unbindDepthTexture ( )

Unbinds a depth texture from a depth target.
## Texture getUnorderedAccessTexture ( int slot )

Returns an unordered access texture by the specified slot.
### Arguments

- *int* **slot** - Texture slot.

### Return value

Unordered access texture if it exists, otherwise NULL.
## void bindUnorderedAccessTexture ( int slot , Texture texture , int writeonly = false , int atomic = false )

Binds all layers and faces (if supported by the texture type) of a texture on the 0 mip level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Unordered access texture to be bound.
- *int* **writeonly** - Access flag. **1** to use the texture for writing only, otherwise **0**.
- *int* **atomic** - Set **1** to bind the texture with the *GL_32UI* format; otherwise � **0**. This flag is to be set for Vulkan only.

## void bindUnorderedAccessTexture2D ( int slot , Texture texture , int writeonly = false , int atomic = false , int mip = 0 )

Binds a 2D texture on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Unordered access 2D texture to be bound.
- *int* **writeonly** - Access flag. **1** to use the texture for writing only, otherwise **0**.
- *int* **atomic** - Set **1** to bind the texture with the *GL_32UI* format; otherwise � **0**. This flag is to be set for Vulkan only.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindUnorderedAccessTexture2DArray ( int slot , Texture texture , int writeonly = false , int atomic = false , int layer = -1 , int mip = 0 )

Binds the specified layer of a 2D texture array on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Unordered access 2D texture array to be bound.
- *int* **writeonly** - Access flag. **1** to use the texture for writing only, otherwise **0**.
- *int* **atomic** - Set **1** to bind the texture with the *GL_32UI* format; otherwise � **0**. This flag is to be set for Vulkan only.
- *int* **layer** - Number of the 2D texture array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindUnorderedAccessTextureCube ( int slot , Texture texture , int writeonly = false , int atomic = false , int face = -1 , int mip = 0 )

Binds the specified face of a texture cube on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Unordered access texture cube to be bound.
- *int* **writeonly** - Access flag. **1** to use the texture for writing only, otherwise **0**.
- *int* **atomic** - Set **1** to bind the texture with the *GL_32UI* format; otherwise � **0**. This flag is to be set for Vulkan only.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindUnorderedAccessTextureCubeArray ( int slot , Texture texture , int writeonly = false , int atomic = false , int layer = -1 , int face = -1 , int mip = 0 )

Binds the specified layer and face of a texture cube on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Unordered access texture cube array to be bound.
- *int* **writeonly** - Access flag. **1** to use the texture for writing only, otherwise **0**.
- *int* **atomic** - Set **1** to bind the texture with the *GL_32UI* format; otherwise � **0**. This flag is to be set for Vulkan only.
- *int* **layer** - Number of the texture cube array layer.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void bindUnorderedAccessTexture3D ( int slot , Texture texture , int writeonly = false , int atomic = false , int depth = -1 , int mip = 0 )

Binds the specified layer of a 3D texture on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Unordered access 3D texture to be bound.
- *int* **writeonly** - Access flag. **1** to use the texture for writing only, otherwise **0**.
- *int* **atomic** - Set **1** to bind the texture with the *GL_32UI* format; otherwise � **0**. This flag is to be set for Vulkan only.
- *int* **depth** - 3D texture depth layer. With the default value of -1, all depth layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_usc.md#getNumMipmaps_int).

## void unbindUnorderedAccessTexture ( int slot )

Unbinds an unordered access texture from the specified slot.
### Arguments

- *int* **slot** - Texture slot.

## void unbindUnorderedAccessTextures ( )

Unbinds all unordered access textures for unordered access resources.
## StructuredBuffer getStructuredBuffer ( int slot )

Returns a structured buffer by the specified slot.
### Arguments

- *int* **slot** - Texture slot.

### Return value

[Structured buffer](../../../api/library/rendering/class.structuredbuffer_usc.md) if it exists, otherwise NULL.
## void bindStructuredBuffer ( int slot , StructuredBuffer buffer )

Binds a structured buffer to a device by the specified slot.
### Arguments

- *int* **slot** - Texture slot.
- *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_usc.md)* **buffer** - [Structured buffer](../../../api/library/rendering/class.structuredbuffer_usc.md) to be bound.

## void unbindStructuredBuffer ( int slot )

Unbinds a structured buffer for unordered access resources.
### Arguments

- *int* **slot** - Texture slot.

## void unbindStructuredBuffers ( )

Unbinds all structured buffers for unordered access resources.
## void unbindAll ( )

Unbinds all color, depth, and unordered access textures as well as structured buffers.
