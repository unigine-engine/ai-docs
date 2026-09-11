# Unigine.Texture Class (CPP)

**Header:** #include <UnigineTextures.h>


Interface for handling textures.


Textures are stored on GPU.


Unigine provides different filtering modes of texture samples:


1. Point filtering
2. Linear filtering
3. Bilinear filtering
4. Trilinear filtering
5. Anisotropic filtering


They are ordered from the worst visual quality to the best, thus from the least expensive performance cost to the most.


Texture has two sets of flags: sampler and format flags.


#### Sampler Flags


Sampler flags can be changed dynamically at runtime for the [user](../../../content/materials/index.md#user_materials) materials.


- SAMPLER_WRAP_CLAMP_X
- SAMPLER_WRAP_CLAMP_Y
- SAMPLER_WRAP_CLAMP_Z
- SAMPLER_WRAP_BORDER_X
- SAMPLER_WRAP_BORDER_Y
- SAMPLER_WRAP_BORDER_Z
- SAMPLER_WRAP_BORDER_ONE
- SAMPLER_WRAP_BORDER
- SAMPLER_WRAP_MASK
- SAMPLER_FILTER_POINT
- SAMPLER_FILTER_LINEAR
- SAMPLER_FILTER_BILINEAR
- SAMPLER_FILTER_TRILINEAR
- SAMPLER_FILTER_MASK
- SAMPLER_ANISOTROPY_1
- SAMPLER_ANISOTROPY_2
- SAMPLER_ANISOTROPY_4
- SAMPLER_ANISOTROPY_8
- SAMPLER_ANISOTROPY_16
- SAMPLER_ANISOTROPY_MASK
- SAMPLER_DEFAULT_FLAGS
- SAMPLER_FLAGS


#### Format Flags


Format flags changes require texture reinitialization to take effect. The format flags are read-only (editable only for the [base](../../../content/materials/index.md#base_materials) materials).


- FORMAT_SRGB
- FORMAT_SIGNED
- FORMAT_INTEGER
- FORMAT_MIPMAPS
- FORMAT_MASK
- FORMAT_MULTISAMPLE_2
- FORMAT_MULTISAMPLE_4
- FORMAT_MULTISAMPLE_8
- FORMAT_MULTISAMPLE_16
- FORMAT_MULTISAMPLE_MASK
- FORMAT_USAGE_UNORDERED_ACCESS
- FORMAT_USAGE_RENDER
- FORMAT_USAGE_IMMUTABLE
- FORMAT_USAGE_DYNAMIC
- FORMAT_USAGE_STAGING
- FORMAT_USAGE_SHARED
- FORMAT_USAGE_MASK
- FORMAT_FLAGS


#### Data Storage (Levels, Layers, Faces)


A texture's storage contains one or more images with certain dimensions. Each type of texture has a specific arrangement of images in its storage. Textures can have **mipmaps** - smaller versions of the same image used to help in texture sampling and filtering. Each mipmap level has a separate set of images.


Since a texture stores multiple images, it is important to be able to identify a specific image in a texture. Each image in a texture can be uniquely identified by the following numbers, depending on the texture type:


- For textures that can have mipmaps, the **mipmap level** that contains the image.
- For Array Textures, the **array layer** that contains the image.
- For Cubemap Textures, the **face** within that array layer and mipmap level. > **Notice:** For Cubemap Array Textures, the layer and face are combined into layer-faces.


Therefore, a texture can be thought of as a three-dimensional array of images. The first index is the *mipmap level*, the second is the *array layer*, and the third is the *cube map face*. Another way to think of it is that a texture has a number of mipmap levels. Each mipmap can have a number of array layers. And each array layer has a number of faces. **Every image of a texture can therefore be uniquely referenced by the face, layer, and level indices.**


## Texture Class

### Members

## int getAllFlags () const

Returns the current texture flags ([format](#format_flags) and [sampler](#sampler_flags)).
### Return value

Current texture flags, a combination of *[FORMAT_*](#FORMAT_SRGB)* and *[SAMPLER_*](#SAMPLER_WRAP_CLAMP_X)* variables.
## int getFormatFlags () const

Returns the current texture [format flags](#format_flags).
### Return value

Current format flags, a combination of *[FORMAT_*](#FORMAT_SRGB)* variables.
## void setSamplerFlags ( int flags )

Sets a new texture [sampler flags](#sampler_flags).
### Arguments

- *int* **flags** - The sampler flags, a combination of *[SAMPLER_*](#SAMPLER_WRAP_CLAMP_X)* variables.

## int getSamplerFlags () const

Returns the current texture [sampler flags](#sampler_flags).
### Return value

Current sampler flags, a combination of *[SAMPLER_*](#SAMPLER_WRAP_CLAMP_X)* variables.
## int getNumFaces () const

Returns the current number of [faces](#anatomy) in the texture.
### Return value

Current number of [faces](#anatomy) in the texture.
## int getNumLayers () const

Returns the current number of [layers](#anatomy) in the texture.
### Return value

Current number of [layers](#anatomy) in the texture.
## int getNumMipmaps () const

Returns the current The texture [mipmap](#anatomy) count.
### Return value

Current The texture [mipmap](#anatomy) count.
## int getNumChannels () const

Returns the current number of channels.
### Return value

Current number of channels.
## bool isDepthFormat () const

Returns the current value indicating if the texture is depth texture.
### Return value

**true** if the texture is depth texture; otherwise **false**.
## bool isColorFormat () const

Returns the current value indicating if the texture is color texture.
### Return value

**true** if the texture is color texture; otherwise **false**.
## bool isCompressedFormat () const

Returns the current value indicating if the texture is stored in a compressed format (DXT1, DXT3, DXT5, ATI1, ATI2, ZLC1 or ZLC2).
### Return value

**true** if the texture is stored in a compressed format (DXT1, DXT3, DXT5, ATI1, ATI2, ZLC1 or ZLC2); otherwise **false**.
## bool isCombinedFormat () const

Returns the current value indicating if the texture is stored in a combined format (RGB565, RGBA4, RGB5A1, or RGB10A2).
### Return value

**true** if the texture is stored in a combined format (RGB565, RGBA4, RGB5A1, or RGB10A2); otherwise **false**.
## bool isIntegerFormat () const

Returns the current value indicating if the texture is stored in an integer format (unsigned char, unsigned short, or unsigned int).
### Return value

**true** if the texture is stored in an integer format (unsigned char, unsigned short, or unsigned int); otherwise **false**.
## bool isFloatFormat () const

Returns the current value indicating if the texture is stored in a float format (R32F, RG32F or RGBA32F).
### Return value

**true** if the texture is stored in a float format (R32F, RG32F or RGBA32F); otherwise **false**.
## bool isHalfFormat () const

Returns the current value indicating if the texture is stored in a half-float format (R16F, RG16F or RGBA16F).
### Return value

**true** if the texture is stored in a half-float format (R16F, RG16F or RGBA16F); otherwise **false**.
## bool isUShortFormat () const

Returns the current value indicating if the texture is stored in an unsigned short format (R16, RG16 or RGBA16).
### Return value

**true** if the texture is stored in an unsigned short format (R16, RG16 or RGBA16); otherwise **false**.
## bool isUCharFormat () const

Returns the current value indicating if the texture is stored in an unsigned char format (R8, RG8, RGBA8, DXT1, DXT3, DXT5, ATI1 or ATI2).
### Return value

**true** if the texture is stored in an unsigned char format (R8, RG8, RGBA8, DXT1, DXT3, DXT5, ATI1 or ATI2); otherwise **false**.
## bool isUIntFormat () const

Returns the current value indicating if the texture is stored in an unsigned integer format (R32U, RG32U or RGBA32U).
### Return value

**true** if the texture is stored in an unsigned integer format (R32U, RG32U or RGBA32U); otherwise **false**.
## bool isRawFormat () const

Returns the current value indicating if the texture is uncompressed (stored in R8, RG8, RGBA8, R16, RG16, RGBA16, R16F, RG16F, RGBA16F, R32F, RG32F, RGBA32F, RGB565, RGBA4, RGB5A1, RGB10A2, D16, D24S8, D32F, or D32FS8 format).
### Return value

**true** if the texture is uncompressed (stored in R8, RG8, RGBA8, R16, RG16, RGBA16, R16F, RG16F, RGBA16F, R32F, RG32F, RGBA32F, RGB565, RGBA4, RGB5A1, RGB10A2, D16, D24S8, D32F, or D32FS8 format); otherwise **false**.
## int getImageFormat () const

Returns the current image format corresponding to the current texture format.
### Return value

Current Image format identifier (see the [FORMAT_*](../../../api/library/common/class.image_cpp.md#FORMAT_ATI1) variables) or 0 if the specified texture format is unknown.
## const char * getFormatName () const

Returns the current texture format name.
### Return value

Current texture format name.
## int getFormat () const

Returns the current texture format.
### Return value

Current texture format.
## bool isArrayType () const

Returns the current value indicating if the texture is array texture.
### Return value

**true** if the texture type is an array; otherwise **false**.
## bool isCubeType () const

Returns the current value indicating if the texture is cube texture.
### Return value

**true** if the texture type is cube texture; otherwise **false**.
## bool is3DType () const

Returns the current value indicating if the texture is a 3D texture.
### Return value

**true** if the texture type is 3D texture; otherwise **false**.
## bool is2DType () const

Returns the current value indicating if the texture is a 2D texture.
### Return value

**true** if the texture type is 2D texture; otherwise **false**.
## const char * getTypeName () const

Returns the current texture type name.
### Return value

Current texture type name.
## int getType () const

Returns the current texture type.
### Return value

Current texture type.
## void setDebugName ( const char * name )

Sets a new friendly name for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Arguments

- *const char ** **name** - The friendly name of the texture used for GPU debugging (RenderDoc, NVIDIA Nsight).

## const char * getDebugName () const

Returns the current friendly name for GPU debugging (RenderDoc, NVIDIA Nsight). It can be used to help you determine if the corresponding object interface pointer caused the leak. Memory leaks are reported by the [debug software layer](https://docs.microsoft.com/en-us/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers#debug-layer) by outputting a list of object interface pointers along with their friendly names.
### Return value

Current friendly name of the texture used for GPU debugging (RenderDoc, NVIDIA Nsight).
## void setOwnership ( bool ownership )

Sets a new ownership flag that defines if the texture is to be automatically managed by the Engine. If the flag is set the Engine takes care of the texture as if it was created by the Engine, otherwise the user should manage the texture manually (destroy the object, do all necessary memory cleanup).
### Arguments

- *bool* **ownership** - Set **true** to enable automatic managing of the texture and used memory lifetime by the Engine; **false** - to disable it.

## bool isOwnership () const

Returns the current ownership flag that defines if the texture is to be automatically managed by the Engine. If the flag is set the Engine takes care of the texture as if it was created by the Engine, otherwise the user should manage the texture manually (destroy the object, do all necessary memory cleanup).
### Return value

**true** if automatic managing of the texture and used memory lifetime by the Engine is enabled ; otherwise **false**.
## bool isUsageShared () const

Returns the current value indicating if the texture has the [FORMAT_USAGE_SHARED](#FORMAT_USAGE_SHARED) flag enabled.
### Return value

**true** if the [FORMAT_USAGE_SHARED](#FORMAT_USAGE_SHARED) flag for the texture is enabled ; otherwise **false**.
## bool isUsageStaging () const

Returns the current value indicating if the texture has the [FORMAT_USAGE_STAGING](#FORMAT_USAGE_STAGING) flag enabled.
### Return value

**true** if the [FORMAT_USAGE_STAGING](#FORMAT_USAGE_STAGING) flag for the texture is enabled ; otherwise **false**.
## bool isUsageDynamic () const

Returns the current value indicating if the texture has the [FORMAT_USAGE_DYNAMIC](#FORMAT_USAGE_DYNAMIC) flag enabled.
### Return value

**true** if the [FORMAT_USAGE_DYNAMIC](#FORMAT_USAGE_DYNAMIC) flag for the texture is enabled ; otherwise **false**.
## bool isUsageImmutable () const

Returns the current value indicating if the texture has the [FORMAT_USAGE_IMMUTABLE](#FORMAT_USAGE_IMMUTABLE) flag enabled.
### Return value

**true** if the [FORMAT_USAGE_IMMUTABLE](#FORMAT_USAGE_IMMUTABLE) flag for the texture is enabled ; otherwise **false**.
## bool isUsageRender () const

Returns the current value indicating if the texture has the [FORMAT_USAGE_RENDER](#FORMAT_USAGE_RENDER) flag enabled.
### Return value

**true** if the [FORMAT_USAGE_RENDER](#FORMAT_USAGE_RENDER) flag for the texture is enabled ; otherwise **false**.
## bool isUsageUnorderedAccess () const

Returns the current value indicating if the texture has the [FORMAT_USAGE_UNORDERED_ACCESS](#FORMAT_USAGE_UNORDERED_ACCESS) flag enabled.
### Return value

**true** if the [FORMAT_USAGE_UNORDERED_ACCESS](#FORMAT_USAGE_UNORDERED_ACCESS) flag for the texture is enabled ; otherwise **false**.
## size_t getVideoMemoryUsage () const

Returns the current amount of memory occupied by the texture.
### Return value

Current texture size, in bytes.
---

## bool isAnisotropy ( ) const

Checks texture anisotropy.
### Return value

true if the texture filter is anisotropy, otherwise, false.
## bool isValid ( )

Returns a value indicating if the texture is valid (null-pointer check).
### Return value

true if the texture is valid; otherwise, false.
## int getDepth ( int level = 0 ) const

Returns the depth for the given texture mipmap level.
### Arguments

- *int* **level** - Mipmap level number in the range from **0** to the [total number of mipmaps](#getNumMipmaps_int).

### Return value

Texture mipmap level depth.
## int getHeight ( int level = 0 ) const

Returns the height for the specified texture mipmap level.
### Arguments

- *int* **level** - Mipmap level number in the range from **0** to the [total number of mipmaps](#getNumMipmaps_int).

### Return value

Texture mipmap level height.
## bool setImage ( const Ptr < Image > & image )

Sets texture data using the data of the specified source image.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Source image to be used for setting texture data.

### Return value

true if the data was set successfully; otherwise, false.
## bool setImage2D ( const Ptr < Image > & image , int offset_x , int offset_y , int texture_format = -1 )


Sets texture data using the data of the specified 2D or 2D array image.


> **Notice:** The following conditions must be satisfied:
>
>
> - Both texture and image types must be either **2D** or **2D_ARRAY**.
> - Texture resolution must be greater or equal to the image resolution.
> - Image and texture mipmap counts must be equal (the same is for layer counts of 2D arrays).


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Source image to be used for setting texture data.
- *int* **offset_x** - Offset along the X axis (in pixels) starting from which the data of the specified image is to be taken. The following condition must be satisfied: **offset_x < texture_width - image_width**.
- *int* **offset_y** - Offset along the Y axis (in pixels) starting from which the data of the specified image is to be taken. The following condition must be satisfied: **offset_y < texture_height - image_height**.
- *int* **texture_format** - Texture format identifier (see the [FORMAT_*](#FORMAT_ATI1) variables), or -1 - auto-detect.

### Return value

true if the data was set successfully; otherwise, false.
## bool setImageLayer ( const Ptr < Image > & image , int layer , int texture_format = -1 )


Sets the data of the specified layer of the 2D texture array using the data of the specified 2D image.


> **Notice:** The following conditions must be satisfied:
>
>
> - Texture and image must have the same resolution.
> - Image and texture mipmap counts must be equal (the same is for layer counts of 2D arrays).


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Source image to be used for setting the data of the 2D texture array layer.
- *int* **layer** - Number of the 2D texture array layer, for which the data is to be set.
- *int* **texture_format** - Texture format identifier (see the [FORMAT_*](#FORMAT_ATI1) variables), or -1 - auto-detect.

### Return value

true if the data was set successfully; otherwise, false.
## int getMultisample ( ) const

Returns the multisample count.
### Return value

Multisample count.
## int getWidth ( int level = 0 ) const

Returns the width for the specified texture mipmap level.
### Arguments

- *int* **level** - Mipmap level number in the range from **0** to the [total number of mipmaps](#getNumMipmaps_int).

### Return value

Texture mipmap level width.
## void clear ( )

Clears texture.
## bool copy2D ( int dest_x = 0 , int dest_y = 0 , int src_x = 0 , int src_y = 0 , int w = -1 , int h = -1 )

Copies 2D texture.
### Arguments

- *int* **dest_x** - The offset of the source texture along the X-axis.
- *int* **dest_y** - The offset of the source texture along the Y-axis.
- *int* **src_x** - The offset of the destination texture along the X-axis.
- *int* **src_y** - The offset of the destination texture along the Y-axis.
- *int* **w** - The width of the destination texture.
- *int* **h** - The height of the destination texture.

### Return value

true if the texture was copied; otherwise, false.
## bool copyCube ( int face , int dest_x = 0 , int dest_y = 0 , int src_x = 0 , int src_y = 0 , int w = -1 , int h = -1 )

Copies Cube texture.
### Arguments

- *int* **face** - The face of the cube.
- *int* **dest_x** - The offset of the source texture along the X-axis.
- *int* **dest_y** - The offset of the source texture along the Y-axis.
- *int* **src_x** - The offset of the destination texture along the X-axis.
- *int* **src_y** - The offset of the destination texture along the Y-axis.
- *int* **w** - The width of the destination texture.
- *int* **h** - The height of the destination texture.

### Return value

true if the texture was copied; otherwise, false.
## static Ptr < Texture > TexturePtr create ( )

Texture constructor.
### Return value

Pointer to the created texture.
## bool create ( const Ptr < Image > & image , int flags = SAMPLER_FILTER_LINEAR , int skip_mipmaps = 0 , int format = -1 )

Texture constructor. Creates a new texture with the specified parameters.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image pointer.
- *int* **flags** - Texture flags.
- *int* **skip_mipmaps**
- *int* **format** - Texture format.

### Return value

true if the texture was created successfully; otherwise, false.
## bool create2D ( int width , int height , int format , int flags = SAMPLER_FILTER_LINEAR )

Creates 2D texture.
### Arguments

- *int* **width** - Texture width.
- *int* **height** - Texture height.
- *int* **format** - Texture format.
- *int* **flags** - Texture flags.

### Return value

true if the texture was created successfully; otherwise, false.
## bool create2DArray ( int width , int height , int num_layers , int format , int flags = SAMPLER_FILTER_LINEAR )

Creates 2D Array texture.
### Arguments

- *int* **width** - Texture width.
- *int* **height** - Texture height.
- *int* **num_layers** - Texture layers.
- *int* **format** - Texture format.
- *int* **flags** - Texture flags.

### Return value

true if the 2D array texture was created; otherwise, false.
## bool create3D ( int width , int height , int depth , int format , int flags = SAMPLER_FILTER_LINEAR )

Creates 3D texture.
### Arguments

- *int* **width** - Texture width.
- *int* **height** - Texture height.
- *int* **depth** - Texture depth.
- *int* **format** - Texture format.
- *int* **flags** - Texture flags.

### Return value

true if the 3D texture was created; otherwise, false.
## bool createCube ( int width , int height , int format , int flags = SAMPLER_FILTER_LINEAR )

Creates Cube texture.
### Arguments

- *int* **width** - Texture width.
- *int* **height** - Texture height.
- *int* **format** - Texture format.
- *int* **flags** - Texture flags.

### Return value

true if the cubemap texture was created; otherwise, false.
## bool createCubeArray ( int width , int height , int num_layers , int format , int flags = SAMPLER_FILTER_LINEAR )

Creates Cube Array texture.
### Arguments

- *int* **width** - Texture width.
- *int* **height** - Texture height.
- *int* **num_layers** - Texture layers.
- *int* **format** - Texture format.
- *int* **flags** - Texture flags.

### Return value

true if the cubemap texture array was created; otherwise, false.
## bool createMipmaps ( )

Creates mipmaps stack.
### Return value

true if the mipmaps stack was created; otherwise, false.
## void destroy ( )

Destroys texture.
## bool load ( const char * name , int flags = SAMPLER_FILTER_LINEAR )

Loads texture from file.
### Arguments

- *const char ** **name** - File name.
- *int* **flags** - Texture flags.

### Return value

true if the texture was loaded; otherwise, false.
## void render2D ( float x0 = -1.0f , float y0 = -1.0f , float x1 = 1.0f , float y1 = 1.0f )

Renders 2D texture. This function creates 4 vertices (2 polygons) by using 2 X-coordinates and 2 Y-coordinates and sends it to be rendered.
### Arguments

- *float* **x0** - The first X-coordinate.
- *float* **y0** - The first Y-coordinate.
- *float* **x1** - The second X-coordinate.
- *float* **y1** - The second Y-coordinate.

## void render2DArray ( int layer , float x0 = -1.0f , float y0 = -1.0f , float x1 = 1.0f , float y1 = 1.0f )

Renders 2D Array texture. This function creates 4 vertices (2 polygons) of the texture layer by using 2 X-coordinates and 2 Y-coordinates and sends it to be rendered.
### Arguments

- *int* **layer** - The number of layer.
- *float* **x0** - The first X-coordinate.
- *float* **y0** - The first Y-coordinate.
- *float* **x1** - The second X-coordinate.
- *float* **y1** - The second Y-coordinate.

## void render2DScreen ( float x0 = -1.0f , float y0 = -1.0f , float x1 = 1.0f , float y1 = 1.0f )

Renders 2D Screen texture. This function creates 3 vertices (1 polygon) and and sends texture to be rendered inside the polygon to avoid artifacts on the edge of 2 polygons if the anti-aliasing is used.
### Arguments

- *float* **x0** - The first X-coordinate.
- *float* **y0** - The first Y-coordinate.
- *float* **x1** - The second X-coordinate.
- *float* **y1** - The second Y-coordinate.

## void renderCube ( int face , float x0 = -1.0f , float y0 = -1.0f , float x1 = 1.0f , float y1 = 1.0f )

Renders Cube texture. This function creates 4 vertices (2 polygons) of the given face of the cube texture by using 2 X-coordinates and 2 Y-coordinates and sends it to be rendered.
### Arguments

- *int* **face** - The face of the cube.
- *float* **x0** - The first X-coordinate.
- *float* **y0** - The first Y-coordinate.
- *float* **x1** - The second X-coordinate.
- *float* **y1** - The second Y-coordinate.

## void renderCubeArray ( int face , int layer , float x0 = -1.0f , float y0 = -1.0f , float x1 = 1.0f , float y1 = 1.0f )

Renders Cube Array texture. This function creates 4 vertices (2 polygons) of the given face of the cube texture layer by using 2 X-coordinates and 2 Y-coordinates and sends it to be rendered.
### Arguments

- *int* **face** - The face of the cube.
- *int* **layer** - The layer number.
- *float* **x0** - The first X-coordinate.
- *float* **y0** - The first Y-coordinate.
- *float* **x1** - The second X-coordinate.
- *float* **y1** - The second Y-coordinate.

## int formatImageToTexture ( int image_format , int flags )

Returns the texture format corresponding to the specified image format.
### Arguments

- *int* **image_format** - Image format identifier (see the [FORMAT_*](../../../api/library/common/class.image_cpp.md#FORMAT_ATI1) variables) or 0 if the specified texture format is unknown.
- *int* **flags** - Unsigned format flag. 1 to interpret integer image format as unsigned, 0 - as signed.

### Return value

Texture format identifier (see the [FORMAT_*](#FORMAT_ATI1) variables) or 0 if the specified image format is unknown.
## int formatTextureToImage ( int texture_format )

Returns the image format corresponding to the specified texture format.
### Arguments

- *int* **texture_format** - Texture format identifier (see the [FORMAT_*](#FORMAT_ATI1) variables).

### Return value

Image format identifier (see the [FORMAT_*](../../../api/library/common/class.image_cpp.md#FORMAT_ATI1) variables) or 0 if the specified texture format is unknown.
## int typeTextureToImage ( int texture_type )

Returns the image type corresponding to the specified texture type.
### Arguments

- *int* **texture_type** - Texture type identifier (see the [TEXTURE_*](#TEXTURE_2D) variables).

### Return value

Image type identifier (see the [IMAGE_*](../../../api/library/common/class.image_cpp.md#IMAGE_2D) variables) or 0 if the specified texture type is unknown.
## void clearBuffer ( )

Clears all levels of the texture image (fills all its elements with 0-values).
## void clearBuffer ( const Math:: vec4 & color )

Clears all levels of the texture image (fills all its elements with the clecified color values).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color to be used to fill the buffer.

## void swap ( const Ptr < Texture > & texture )

Swaps the data of the current texture with the source texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Source texture.

## bool copy ( const Ptr < Texture > & src )

Copies the data of the source texture to the texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **src** - Source texture.

### Return value

true if the data of the source texture is copied successfully; otherwise, false.
## size_t getVideoMemoryUsage ( int width , int height , int format , int num_mipmaps , int flags , int num_faces , int num_layers , int depth )

Returns the amount of memory occupied by a texture with the specified parameters.
### Arguments

- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **format** - Texture format.
- *int* **num_mipmaps** - Number of mipmaps in the texture.
- *int* **flags** - Texture flags.
- *int* **num_faces** - Number of faces in the texture.
- *int* **num_layers** - Number of layers in the texture.
- *int* **depth** - Texture depth.

### Return value

Texture size, in bytes.
## bool copyRegion ( const Ptr < Texture > & src , const Math:: ivec3 & src_coords , int src_level , const Math:: ivec3 & dest_coords , int dest_level , int width , int height , int depth )

Copies the specified region from the source texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **src** - Source texture from which the data is to be copied.
- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **src_coords** - Coordinates in the source texture starting from which the region's data is to be taken.
- *int* **src_level** - Source texture mipmap level number in the range from **0** to the [total number of mipmaps](#getNumMipmaps_int).
- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **dest_coords** - Coordinates in the texture starting from which the data from the source texture is to be pasted.
- *int* **dest_level** - Target mipmap level number in the range from **0** to the [total number of mipmaps](#getNumMipmaps_int).
- *int* **width** - Width of the region to be copied, in pixels.
- *int* **height** - Height of the region to be copied, in pixels.
- *int* **depth** - Depth of the region to be copied, in pixels.

### Return value

true if the specified region was successfully copied from the source to the destination; otherwise, false.
## bool setBlob ( const Ptr < Blob > & blob ) const

Sets texture data from the specified source blob.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../api/library/common/class.blob_cpp.md)> &* **blob** - Source blob containing texture data.

### Return value

true if the data was set successfully; otherwise, false.
## const char * getTypeName ( int type )

Returns the texture type name by its type index.
### Arguments

- *int* **type** - Texture type index.

### Return value

Texture type name.
## Ptr < ResourceExternalMemory > getResourceExternalMemory ( ) const

Returns the pointer to the resource in video memory. If the [FORMAT_USAGE_SHARED](#FORMAT_USAGE_SHARED) flag is not enabled for the resource, this method returns nullptr.
### Return value

The pointer to the resource in video memory. If the [FORMAT_USAGE_SHARED](#FORMAT_USAGE_SHARED) flag is not enabled for the resource, this method returns nullptr.
