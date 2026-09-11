# Unigine.RenderTarget Class (CS)


A container to which an image is rendered (a [framebuffer](https://en.wikipedia.org/wiki/Framebuffer) abstraction).


## RenderTarget Class

### Properties

## 🔒︎ bool IsCompleted

The value indicating if the render target is completed.
## 🔒︎ bool IsEnabled

The value indicating if the render target is enabled.
### Members

---

## RenderTarget ( )

Constructor. Creates a new render target.
## void Destroy ( )

Destroys the render target.
## void Enable ( )

Enables the render target.
## void EnableCompute ( )

Enables the render target with the use of compute shader output.
## void Disable ( )

Disables the render target.
## void Flush ( )

Flushes the render target.
## Texture GetColorTexture ( int slot )

Returns a color texture by the specified slot.
### Arguments

- *int* **slot** - Texture slot.

### Return value

Color texture if it exists, otherwise NULL.
## void BindColorTexture ( int slot , Texture texture )

Binds all layers and faces (if supported by the texture type) of a texture on the 0 mip level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Color texture to be bound.

## void BindColorTexture2D ( int slot , Texture texture , int mip = 0 )

Binds the specified slot of a 2D texture on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - 2D color texture to be bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindColorTexture2DArray ( int slot , Texture texture , int layer = -1 , int mip = 0 )

Binds the specified slot and layer of a 2D texture array on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - 2D color texture array to be bound.
- *int* **layer** - Number of the 2D texture array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindColorTextureCube ( int slot , Texture texture , int face = -1 , int mip = 0 )

Binds the specified slot and face of a texture cube on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Color texture cube to be bound.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindColorTextureCubeArray ( int slot , Texture texture , int layer = -1 , int face = -1 , int mip = 0 )

Binds the specified layer and face of a texture cube array on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Color cube array texture to be bound.
- *int* **layer** - Number of the texture cube array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindColorTexture3D ( int slot , Texture texture , int depth = -1 , int mip = 0 )

Binds the specified depth layer of a 3D texture on the specified mipmap level to the specified slot as render target.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - 3D Color texture to be bound.
- *int* **depth** - 3D texture depth layer. With the default value of -1, all depth layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void UnbindColorTexture ( int slot )

Unbinds a render target texture from the specified slot.
### Arguments

- *int* **slot** - Texture slot.

## void UnbindColorTextures ( )

Unbinds all render target textures from a render target.
## Texture GetDepthTexture ( )

Returns the depth texture.
### Return value

Depth texture if it exists, otherwise NULL.
## void BindDepthTexture ( Texture texture )

Binds all layers and faces (if supported by the texture type) of a texture on the 0 mip level to the specified slot as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Depth texture to be bound.

## void BindDepthTextureReadOnly ( Texture texture )

Binds a depth texture as a read-only depth render target (such as depth test), and at the same time allows using this texture as a shader resource in the shader.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Depth texture to be bound.

## void BindDepthTexture2D ( Texture texture , int mip = 0 )

Binds a 2D depth texture on the specified mipmap level as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - 2D depth texture to be bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindDepthTexture2DArray ( Texture texture , int layer = -1 , int mip = 0 )

Binds the specified layer of a depth texture on the specified mipmap level as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - 2D depth texture array to be bound.
- *int* **layer** - Number of the 2D depth texture array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindDepthTextureCube ( Texture texture , int face = -1 , int mip = 0 )

Binds the specified face of a depth texture cube on the specified mipmap level as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Depth texture cube to be bound.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindDepthTextureCubeArray ( Texture texture , int layer = -1 , int face = -1 , int mip = 0 )

Binds the specified layer and face of a depth texture cube array on the specified mipmap level as depth target.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Depth texture cube array to be bound.
- *int* **layer** - Number of the texture cube array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void UnbindDepthTexture ( )

Unbinds a depth texture from a depth target.
## Texture GetUnorderedAccessTexture ( int slot )

Returns an unordered access texture by the specified slot.
### Arguments

- *int* **slot** - Texture slot.

### Return value

Unordered access texture if it exists, otherwise NULL.
## void BindUnorderedAccessTexture ( int slot , Texture texture , bool writeonly = false , bool atomic = false )

Binds all layers and faces (if supported by the texture type) of a texture on the 0 mip level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Unordered access texture to be bound.
- *bool* **writeonly** - Access flag. true to use the texture for writing only, otherwise false.
- *bool* **atomic** - Set true to bind the texture with the *GL_32UI* format; otherwise � false. This flag is to be set for Vulkan only.

## void BindUnorderedAccessTexture2D ( int slot , Texture texture , bool writeonly = false , bool atomic = false , int mip = 0 )

Binds a 2D texture on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Unordered access 2D texture to be bound.
- *bool* **writeonly** - Access flag. true to use the texture for writing only, otherwise false.
- *bool* **atomic** - Set true to bind the texture with the *GL_32UI* format; otherwise � false. This flag is to be set for Vulkan only.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindUnorderedAccessTexture2DArray ( int slot , Texture texture , bool writeonly = false , bool atomic = false , int layer = -1 , int mip = 0 )

Binds the specified layer of a 2D texture array on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Unordered access 2D texture array to be bound.
- *bool* **writeonly** - Access flag. true to use the texture for writing only, otherwise false.
- *bool* **atomic** - Set true to bind the texture with the *GL_32UI* format; otherwise � false. This flag is to be set for Vulkan only.
- *int* **layer** - Number of the 2D texture array layer. With the default value of -1, all layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindUnorderedAccessTextureCube ( int slot , Texture texture , bool writeonly = false , bool atomic = false , int face = -1 , int mip = 0 )

Binds the specified face of a texture cube on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Unordered access texture cube to be bound.
- *bool* **writeonly** - Access flag. true to use the texture for writing only, otherwise false.
- *bool* **atomic** - Set true to bind the texture with the *GL_32UI* format; otherwise � false. This flag is to be set for Vulkan only.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindUnorderedAccessTextureCubeArray ( int slot , Texture texture , bool writeonly = false , bool atomic = false , int layer = -1 , int face = -1 , int mip = 0 )

Binds the specified layer and face of a texture cube on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Unordered access texture cube array to be bound.
- *bool* **writeonly** - Access flag. true to use the texture for writing only, otherwise false.
- *bool* **atomic** - Set true to bind the texture with the *GL_32UI* format; otherwise � false. This flag is to be set for Vulkan only.
- *int* **layer** - Number of the texture cube array layer.
- *int* **face** - The face of the cube. With the default value of -1, all faces of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void BindUnorderedAccessTexture3D ( int slot , Texture texture , bool writeonly = false , bool atomic = false , int depth = -1 , int mip = 0 )

Binds the specified layer of a 3D texture on the specified mipmap level to the specified slot for unordered access.
### Arguments

- *int* **slot** - Texture slot.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Unordered access 3D texture to be bound.
- *bool* **writeonly** - Access flag. true to use the texture for writing only, otherwise false.
- *bool* **atomic** - Set true to bind the texture with the *GL_32UI* format; otherwise � false. This flag is to be set for Vulkan only.
- *int* **depth** - 3D texture depth layer. With the default value of -1, all depth layers of the texture on a specified mip level are bound.
- *int* **mip** - Mipmap level number in the range from **0** to the [total number of mipmaps](../../../api/library/rendering/class.texture_cs.md#getNumMipmaps_int).

## void UnbindUnorderedAccessTexture ( int slot )

Unbinds an unordered access texture from the specified slot.
### Arguments

- *int* **slot** - Texture slot.

## void UnbindUnorderedAccessTextures ( )

Unbinds all unordered access textures for unordered access resources.
## StructuredBuffer GetStructuredBuffer ( int slot )

Returns a structured buffer by the specified slot.
### Arguments

- *int* **slot** - Texture slot.

### Return value

[Structured buffer](../../../api/library/rendering/class.structuredbuffer_cs.md) if it exists, otherwise NULL.
## void BindStructuredBuffer ( int slot , StructuredBuffer buffer )

Binds a structured buffer to a device by the specified slot.
### Arguments

- *int* **slot** - Texture slot.
- *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* **buffer** - [Structured buffer](../../../api/library/rendering/class.structuredbuffer_cs.md) to be bound.

## void UnbindStructuredBuffer ( int slot )

Unbinds a structured buffer for unordered access resources.
### Arguments

- *int* **slot** - Texture slot.

## void UnbindStructuredBuffers ( )

Unbinds all structured buffers for unordered access resources.
## void UnbindAll ( )

Unbinds all color, depth, and unordered access textures as well as structured buffers.
