# Unigine::Image Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Interface for handling textures and other images.


This class supports the following formats:


| Format | Extensions | Save | Load |
|---|---|---|---|
| UNIGINE Native | .texture | ![yes](yes.png) | ![](yes.png) |
| JPEG | .jpg, .jpeg, .jpe, .jif, .jfif, .jfi | ![Yes](yes.png) | ![Yes](yes.png) |
| TIFF | .tif, .tiff | ![Yes](yes.png) | ![Yes](yes.png) |
| TGA | .tga | ![Yes](yes.png) | ![Yes](yes.png) |
| PNG | .png | ![Yes](yes.png) | ![Yes](yes.png) |
| EXR | .exr (no B44, B44A, PIX24 compression) | ![Yes](yes.png) | ![No](yes.png) |
| DDS | .dds | ![Yes](yes.png) | ![Yes](yes.png) |
| PSD | .psd | ![Yes](yes.png) | ![Yes](yes.png) |
| SGI | .sgi, .bw, .la, .int, .inta, .rgb, .rgba | ![No](no.png) | ![Yes](yes.png) |
| PPM/PGM | .ppm, .pgm | ![No](no.png) | ![Yes](yes.png) |
| IES | .ies | ![No](no.png) | ![Yes](yes.png) |
| HDR | .hdr | ![No](no.png) | ![Yes](yes.png) |


Textures are stored on GPU, while images - on CPU.


### Data Storage (Levels, Layers, Faces)


An image storage contains one or more sub-images with certain dimensions. Each type of image has a specific arrangement of sub-images in its storage. Images can have **mipmaps** - smaller versions of the same image used to help in sampling and filtering. Each mipmap level has a separate set of sub-images.


Since an image can store multiple sub-images, it is important to be able to identify a specific sub-image in it. Each sub-image can be uniquely identified by the following numbers, depending on the image type:


- For images that can have mipmaps, the **mipmap level**​ that contains the sub-image.
- For Array Images, the **array layer​** that contains the sub-image.
- For Cubemap Images, the **face** within that array layer and mipmap level. > **Notice:** For Cubemap Array Images, the layer and face are combined into layer-faces.


Therefore, an image can be thought of as a three-dimensional array of sub-image. The first index is the *mipmap level*, the second is the *array layer*, and the third is the *cube map face*. Another way to think of it is that an image has a number of mipmap levels. Each mipmap can have a number of array layers. And each array layer has a number of faces. **Every sub-image of an image can therefore be uniquely referenced by the face, layer, and level indices.**


### See Also


- C++ sample
- C# sample


## Image Class

### Members

## int getNumChannels () const

Returns the current number of image channels.
### Return value

Current number of image channels.
## int getType () const

Returns the current numerical code of the image type.
### Return value

Current numerical code of the image type: 0 for a 2D image, 1 for a 3D image, 2 for a cube image, 3 for a 2D Array. See the [Unigine::Image:: Enumeration with IMAGE_* prefixes](#IMAGE_2D).
## const char * getTypeName () const

Returns the current image type name.
### Return value

Current image type name: 2D for a 2D image, 3D for a 3D image, Cube for a cube image, 2D_Array for a 2D Array.
## int getNumMipmaps () const

Returns the current number of [mipmaps](#anatomy) stored with the image.
### Return value

Current number of mipmap levels.
## int getNumLayers () const

Returns the current number of [layers](#anatomy) in the image.
### Return value

Current number of layers.
## int getNumFaces () const

Returns the current number of [faces](#anatomy) in the image.
### Return value

Current number of image faces.
## bool isLoaded () const

Returns the current value indicating whether the image is loaded.
### Return value

**true** if the image is loaded; otherwise **false**.
## int getBlockSize () const

Returns the current compressed image block size.
### Return value

Current block size in bytes.
## int getPixelSize () const

Returns the current uncompressed image pixel size.
### Return value

Current pixel size, in bytes.
## bool isCubeType () const

Returns the current value indicating if the image is cube image.
### Return value

**true** if the image is a cube image; otherwise **false**.
## bool isArrayType () const

Returns the current value indicating if the image is of an array type (see [*_ARRAY](#IMAGE_2D_ARRAY) variables).
### Return value

**true** if the image is of an array type; otherwise **false**.
## bool is3DType () const

Returns the current value indicating if the image is a 3D image.
### Return value

**true** if the image is a 3D image; otherwise **false**.
## bool is2DType () const

Returns the current value indicating if the image is a 2D image.
### Return value

**true** if the image is a 2D image; otherwise **false**.
## int getFormat () const

Returns the current numerical code of the image format.
### Return value

Current Numerical code of the image format. See the [FORMAT_*](#AUTO_FORMAT) variables.
## const char * getFormatName () const

Returns the current image format name.
### Return value

Current Image format name. The following values can be returned: R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F, RGB565, RGBA4, RGB5A1, RGB10A2, DXT1, DXT3, DXT5, ATI1, ATI2.
## int getDepth () const

Returns the current image depth, in pixels.
### Return value

Current image depth, in pixels.
## int getHeight () const

Returns the current image height, in pixels.
### Return value

Current image height, in pixels.
## int getWidth () const

Returns the current image width, in pixels.
### Return value

Current image width, in pixels.
## getPixelsSize () const

Returns the current size of all pixels of the image.
### Return value

Current size of all pixels of the image, in bytes.
## getNumPixels () const

Returns the current number of pixels in the image.
### Return value

Current number of pixels.
## void setFileCompression ( )

Sets a new file compression type used for the image.
### Arguments

- **compression** - The file compression type to be used for the image. One of the *[FILE_COMPRESSION_*](#FILE_COMPRESSION_LZ4_HIGH)* values.

## getFileCompression () const

Returns the current file compression type used for the image.
### Return value

Current file compression type to be used for the image. One of the *[FILE_COMPRESSION_*](#FILE_COMPRESSION_LZ4_HIGH)* values.
---

## static Image ( )

Default constructor. An empty instance with default parameters is created.
## static Image ( string name )

Constructor. Creates an image loading data from the specified file.
### Arguments

- *string* **name** - Image file name.

## int allocData ( int clear = true )

Allocates memory for the image data.
### Arguments

- *int* **clear** - Clear flag: set **1** to fill allocated memory with zero-values; otherwise, set **0**.

### Return value

**1** if memory for the image data is allocated successfully; otherwise, **0**.
## void clearData ( )

Clears all image data.
## void set ( int offset , const dvec4 & value )

Sets a value for a pixel by its offset. Compressed and combined image formats are not supported.
### Arguments

- *int* **offset** - Pixel offset: `offset = image_width * Y + X`, ( 0 , 0) - top left corner of the image.
- *const dvec4 &* **value** - RGBA color of a pixel with the specified ID.

## void get ( int offset , dvec4 & value )

Gets a value for a pixel by its offset and puts it to the target buffer  `value`.
### Arguments

- *int* **offset** - Pixel offset: `offset = image_width * Y + X`, ( 0 , 0) - top left corner of the image.
- *dvec4 &* **value** - Target buffer to receive an RGBA color of a pixel with the specified ID.

## void get8F ( const ivec2 & coord , vec4 & p )

Returns a set of 8-bit float values stored in the specified image pixel and neighboring ones and puts them to the output vector.
### Arguments

- *const ivec2 &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.
- *vec4 &* **p** - Output [vec4](../../../api/library/math/class.vec4_usc.md) vector (P00, P01, P10, P11) to receive 8-bit float values stored in the specified image pixel and neighboring ones: > **Notice:** Values are normalized in the **[0.0f; 1.0f]** range.

  - **P00** - (X, Y)
  - **P01** - (X, Y+1)
  - **P10** - (X+1, Y)
  - **P11** - (X+1, Y+1)

## float get8F ( const ivec2 & coord )

Returns an 8-bit float value stored in the specified pixel of the image.
### Arguments

- *const ivec2 &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.

### Return value

An 8-bit float value stored in the specified pixel of the image normalized in the **[0.0f; 1.0f]** range.
## void get16F ( const ivec2 & coord , vec4 & p )

Returns a set of 16-bit float values stored in the specified image pixel and neighboring ones and puts them to the output vector.
### Arguments

- *const ivec2 &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.
- *vec4 &* **p** - Output [vec4](../../../api/library/math/class.vec4_usc.md) vector (P00, P01, P10, P11) to receive 16-bit float values stored in the specified image pixel and neighboring ones: > **Notice:** Values are normalized in the **[0.0f; 1.0f]** range.

  - **P00** - (X, Y)
  - **P01** - (X, Y+1)
  - **P10** - (X+1, Y)
  - **P11** - (X+1, Y+1)

## float get16F ( const ivec2 & coord )

Returns a 16-bit float value stored in the specified pixel of the image.
### Arguments

- *const ivec2 &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.

### Return value

A 16-bit float value stored in the specified pixel of the image normalized in the **[0.0f; 1.0f]** range.
## void get32F ( const ivec2 & coord , vec4 & p )

Returns a set of 32-bit float values stored in the specified image pixel and neighboring ones and puts them to the output vector.
### Arguments

- *const ivec2 &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.
- *vec4 &* **p** - Output [vec4](../../../api/library/math/class.vec4_usc.md) vector (P00, P01, P10, P11) to receive 32-bit float values stored in the specified image pixel and neighboring ones: > **Notice:** Values are normalized in the **[0.0f; 1.0f]** range.

  - **P00** - (X, Y)
  - **P01** - (X, Y+1)
  - **P10** - (X+1, Y)
  - **P11** - (X+1, Y+1)

## float get32F ( const ivec2 & coord )

Returns a 32-bit float value stored in the specified pixel of the image.
### Arguments

- *const ivec2 &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.

### Return value

A 32-bit float value stored in the specified pixel of the image normalized in the **[0.0f; 1.0f]** range.
## void set2D ( int x , int y , float r , float g , float b , float a , variable color )

Sets a color for a given pixel of a 2D image. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *float* **r** - Red component of a color normalized in range from **0** to **1**.
- *float* **g** - Green component of a color normalized in range from **0** to **1**.
- *float* **b** - Blue component of a color normalized in range from **0** to **1**.
- *float* **a** - Alpha component of a color normalized in range from **0** to **1**.
- *variable* **color** - Color. It can be a vector of 4 float or integer components ([*vec4*](../../../api/library/math/class.vec4_usc.md) or [*ivec4*](../../../api/library/math/class.ivec4_usc.md)) or a scalar (for images with a single channel).

## get2DArray ( int x , int y , int layer )

Returns a color of a given pixel. The image must be a 2D texture array. Compressed formats are not supported.If *float* coordinates are provided, linear interpolation is used to get a color sample.
### Arguments

- *int* **x** - The X coordinate of a pixel. It can be one of the following:

  - [int](../../../code/uniginescript/language/data_types.md#int) in range **[0; width]**
  - [float](../../../code/uniginescript/language/data_types.md#float) in range [0.0f; 1.0f] > **Notice:** If the provided value is outside the range, modulus is used to count pixels from the beginning.
- *int* **y** - Y coordinate of a pixel. Must be of the same type as *x*:

  - [int](../../../code/uniginescript/language/data_types.md#int) in range **[0; height]**
  - [float](../../../code/uniginescript/language/data_types.md#float) in range [0.0f; 1.0f] > **Notice:** If the provided value is outside the range, modulus is used to count pixels from the beginning.
- *int* **layer** - Image layer number.

### Return value

Color. It can be a vector of 4 float or integer components ([*vec4*](../../../api/library/math/class.vec4_usc.md) or [*ivec4*](../../../api/library/math/class.ivec4_usc.md)) or a scalar (for images with a single channel).
## void set3D ( int x , int y , int z , float r , float g , float b , float a )

Sets a color of a given pixel of a 3D image. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **z** - Z integer coordinate of a pixel in range [0; depth].
- *float* **r** - Red component of a color normalized in range from **0** to **1**.
- *float* **g** - Green component of a color normalized in range from **0** to **1**.
- *float* **b** - Blue component of a color normalized in range from **0** to **1**.
- *float* **a** - Alpha component of a color normalized in range from **0** to **1**.

## get3D ( float x , float y , float z )

Returns a color of a given pixel. The image must be of the 2D type. Compressed formats are not supported. If *float* coordinates are provided, linear interpolation is used to get a color sample.
### Arguments

- *float* **x** - X coordinate of a pixel. It can be:

  - [int](../../../code/uniginescript/language/data_types.md#int) in range [0; width].
  - [float](../../../code/uniginescript/language/data_types.md#float) in range [0.0f; 1.0f] > **Notice:** If the provided value is outside the range, modulus is used to count pixels from the beginning.
- *float* **y** - Y coordinate of a pixel. It can be:

  - [int](../../../code/uniginescript/language/data_types.md#int) in range [0; width].
  - [float](../../../code/uniginescript/language/data_types.md#float) in range [0.0f; 1.0f] > **Notice:** If the provided value is outside the range, modulus is used to count pixels from the beginning.
- *float* **z** - Z coordinate of a pixel. It can be:

  - [int](../../../code/uniginescript/language/data_types.md#int) in range [0; width].
  - [float](../../../code/uniginescript/language/data_types.md#float) in range [0.0f; 1.0f] > **Notice:** If the provided value is outside the range, modulus is used to count pixels from the beginning.

### Return value

Color. It can be a vector of 4 float or integer components ([*vec4*](../../../api/library/math/class.vec4_usc.md) or [*ivec4*](../../../api/library/math/class.ivec4_usc.md)) or a scalar (for images with a single channel).
## get3D ( int x , int y , int z )

Returns a color of a given pixel. The image must be of the 3D type. Compressed formats are not supported. If *float* coordinates are provided, linear interpolation is used to get a color sample.
### Arguments

- *int* **x** - X coordinate of a pixel. It can be:

  - [int](../../../code/uniginescript/language/data_types.md#int) in range [0; width].
  - [float](../../../code/uniginescript/language/data_types.md#float) in range [0.0f; 1.0f] > **Notice:** If the provided value is outside the range, modulus is used to count pixels from the beginning.
- *int* **y** - Y coordinate of a pixel. Must be of the same type as *x*:

  - [int](../../../code/uniginescript/language/data_types.md#int) in range [0; height].
  - [float](../../../code/uniginescript/language/data_types.md#float) in range [0.0f; 1.0f] > **Notice:** If the provided value is outside the range, modulus is used to count pixels from the beginning.
- *int* **z** - Z coordinate of a pixel. Must be of the same type as *x*:

  - [int](../../../code/uniginescript/language/data_types.md#int) in range [0; depth].
  - [float](../../../code/uniginescript/language/data_types.md#float) in range [0.0f; 1.0f] > **Notice:** If the provided value is outside the range, modulus is used to count pixels from the beginning.

### Return value

Color. It can be a vector of 4 float or integer components ([*vec4*](../../../api/library/math/class.vec4_usc.md) or [*ivec4*](../../../api/library/math/class.ivec4_usc.md)) or a scalar (for images with a single channel).
## int isCombinedFormat ( )

Returns a value indicating if the image is stored in a combined format (RGB565, RGBA4, RGB5A1 or RGB10A2).
### Return value

**1** if the image is in combined format; otherwise, **0**.
## int isCombinedFormat ( int format )

Returns a value indicating if a given format is a combined format (RGB565, RGBA4, RGB5A1 or RGB10A2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

**1** if the specified format is a combined format; otherwise, **0**.
## int isCompressedFormat ( )

Returns a value indicating if the image is stored in a compressed format (DXT1, DXT3, DXT5, ATI1, ATI2).
### Return value

**1** if the image is in a compressed format; otherwise, **0**.
## int isCompressedFormat ( int format )

Returns a value indicating if a given format is a compressed format (DXT1, DXT3, DXT5, ATI1, ATI2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

**1** if the specified format is a compressed format; otherwise, **0**.
## void setCube ( int x , int y , int face )

Sets a color of a given pixel. The image must be of the Cube type. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; depth].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **face** - Face number in range from 0 to 5.

## getCube ( float x , float y , int face )

Returns a color of a given pixel. The image must be of the Cube type. Compressed formats are not supported.
### Arguments

- *float* **x** - X float coordinate of a pixel in range [0.0f; 1.0f].
- *float* **y** - Y float coordinate of a pixel in range [0.0f; 1.0f].
- *int* **face** - Face number in range from 0 to 5.

### Return value

Pixel color stored in a vec4.
## getCube ( int x , int y , int face , vec3 direction )

Returns a color of a given pixel. The image must be of the Cube type. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **face** - Face number in range from 0 to 5.
- *vec3* **direction** - Direction vector used for color sampling.

### Return value

Pixel color stored in a vec4.
## void setCubeArray ( int x , int y , int face , int layer )

Sets a color of a given pixel. The image must be of the Cube Array type. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Image layer number.

## getCubeArray ( int layer )


Returns the color of a given pixel of the cube array image.


> **Notice:** Compressed formats are not supported.


### Arguments

- *int* **layer** - Image layer number.

### Return value

Pixel color (can be vec4, or ivec4, or a scalar for single-channel images).
## getCubeArray ( int v1 , int v2 , int face , int layer )


Returns the color of a given pixel of the cube array image. Both the first and the second passed arguments mush be either of the float or of the integer type.


> **Notice:** Compressed formats are not supported.


### Arguments

- *int* **v1** - X integer coordinate of a pixel in range [0;width].
- *int* **v2** - Y integer coordinate of a pixel in range [0; height].
- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Image layer number.

### Return value

Pixel color stored in a vec4.
## getCubeArray ( float v1 , float v2 , int face , int layer )

Returns a color of a given pixel. The image must be of the Cube Array type. Compressed formats are not supported.
### Arguments

- *float* **v1** - X integer coordinate of a pixel in range [0;width].
- *float* **v2** - Y integer coordinate of a pixel in range [0;height].
- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Image layer number.

### Return value

Pixel color stored in a vec4.
## int getDepth ( int level = 0 )

Returns the image depth on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Image depth if the image exists (its depth is larger than 0); otherwise, 1.
## int isFloatFormat ( )

Returns a value indicating if the image is stored in a float format (R32F, RG32F, RGB32F or RGBA32F).
### Return value

**1** if the image is in float format; otherwise, **0** is returned.
## int isFloatFormat ( int format )

Returns a value indicating if a given format is a float format (R32F, RG32F, RGB32F or RGBA32F).
### Arguments

- *int* **format** - Image format identifier. See the [IMAGE_FORMAT_*](#AUTO_FORMAT) variables.

### Return value

**1** if the specified format is a float format; otherwise, **0**.
## int getFormat ( int num_channels , int format )

Returns a numerical code of the image format for the specified format and number of channels.
### Arguments

- *int* **num_channels** - Number of channels in the **[1; 4]** range.
- *int* **format** - Numerical code of the image format. See the [IMAGE_FORMAT_*](#AUTO_FORMAT) variables.

### Return value

Numerical code of the image format for the specified number of channels.
## string getFormatName ( int format )

Returns the name of the image format by the given format ID.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

Image format name. The following values can be returned: R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F, RGB565, RGBA4, RGB5A1, RGB10A2, DXT1, DXT3, DXT5, ATI1, ATI2.
## int isHalfFormat ( )

Returns a value indicating if the image is stored in a half-float format (R16F, RG16F, RGB16F or RGBA16F).
### Return value

**1** if the image is in half-float format; otherwise, **0**.
## int isHalfFormat ( int format )

Returns a value indicating if a given format is a half-float format (R16F, RG16F, RGB16F or RGBA16F).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

**1** if the specified format is a half-float format; otherwise, **0**.
## int getHeight ( int level = 0 )

Returns image height on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Image height if the image exists (its height is larger than 0); otherwise, 1.
## int setChannelInt ( int channel , int value )

Sets an integer value for a given image channel. Compressed and combined image formats are not supported.
### Arguments

- *int* **channel** - Channel number in range from **0** to **number of channels - 1**.
- *int* **value** - Value in range from **0** to **255** (8-bit formats) or from **0** to **65535** (16-bit formats).

### Return value

**1** if the value is set successfully; otherwise, **0**.
## int setChannelFloat ( int channel , float value )

Sets a float value for a given image channel. Compressed and combined image formats are not supported.
### Arguments

- *int* **channel** - Channel number in range from **0** to **number of channels - 1**.
- *float* **value** - Value in range from **0.0f** to **1.0f**.

### Return value

**1** if the value is set successfully; otherwise, **0**.
## int swapChannels ( int channel_0 , int channel_1 )

Swaps values of two channels with the specified numbers. Compressed formats are not supported.
### Arguments

- *int* **channel_0** - Number of the first channel in range from **0** to **number of channels - 1**.
- *int* **channel_1** - Number of the second channel in range from **0** to **number of channels - 1**.

### Return value

**1** if the two specified channels were swapped successfully; otherwise, **0**.
## int getOffset ( int level )

Returns the image offset on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps.

### Return value

Image offset, in bytes.
## void getPixels ( )

Copies the image data to a given target [blob](../../../api/library/common/class.blob_usc.md).
### Arguments

## int getPixelsSize ( int format , int w , int h )

Returns the size of all pixels for the image of the specified format and size.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.
- *int* **w** - Image width, in pixels.
- *int* **h** - Image width, in pixels.

### Return value

Size of all pixels of the specified image, in bytes.
## int isRawFormat ( )

Returns a value indicating if the image is uncompressed (stored in R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F, RGB565, RGBA4, RGB5A1 or RGB10A2 format).
### Return value

**1** if the image is uncompressed; otherwise, **0**.
## int isRawFormat ( int format )

Returns a value indicating if a given format is an uncompressed format (R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F, RGB565, RGBA4, RGB5A1 or RGB10A2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

**1** if the specified format is an uncompressed format; otherwise, **0**.
## int getSize ( )

Returns the current image size.
### Return value

Image size, in bytes.
## int getSize ( int level )

Returns the current image size.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps.

### Return value

Image size in bytes.
## int getStride ( int level = 0 )

Returns the image stride on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps.

### Return value

Image stride in bytes.
## int getDepthStride ( int level = 0 )

Returns the image depth stride on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps.

### Return value

Image depth stride in bytes.
## string getTypeName ( int type )

Returns the name of the image type by its identifier.
### Arguments

- *int* **type** - Image type. One of the [IMAGE_*](#IMAGE_2D) types.

### Return value

Image type name: 2D for a 2D image, 3D for a 3D image, Cube for a cube image, 2D_Array for a 2D Array.
## int isUCharFormat ( )

Returns a value indicating if the image is stored in an unsigned char format (R8, RG8, RGB8, RGBA8, DXT1, DXT3, DXT5, ATI1 or ATI2).
### Return value

**1** if the image is in unsigned char format; otherwise, **0**.
## int isUCharFormat ( int format )

Returns a value indicating if a given format is an unsigned char format (R8, RG8, RGB8, RGBA8, DXT1, DXT3, DXT5, ATI1 or ATI2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

**1** if the specified format is an unsigned char format; otherwise, **0**.
## int isUShortFormat ( )

Returns a value indicating if the image is stored in an unsigned short format (R16, RG16, RGB16 or RGBA16).
### Return value

**1** if the image is in unsigned short format; otherwise, **0**.
## int isUShortFormat ( int format )

Returns a value indicating if a given format is an unsigned short format (R16, RG16, RGB16 or RGBA16).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

**1** if the specified format is an unsigned short format; otherwise, **0**.
## int getWidth ( int level = 0 )

Returns the image width on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Image width if the image exists (its width is larger than 0); otherwise, 1.
## int blend ( Image image , int x0 , int y0 , int x1 , int y1 , int width , int height , float scale = 1.0f , int safe = 0 )


Blends the specified image with the current one. Blending takes place within a specified region. If the *safe* flag is set to 1, rendering of the blended images won't be performed outside the destination image boundaries. Compressed, combined, half-float and float formats are not supported. Images of different formats can be blended as follows:


- R8 with R8, RG8;
- RG8 with RG8, RGB8;
- RGB8 with RGB8, RGBA8;
- RGBA8 with RGBA8 only;
- R16 with R16, RG16;
- RG16 with RG16, RGB16;
- RGB16 with RGB16, RGBA16;
- RGBA16 with RGBA16 only;


### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Source image to be blended with the current image.
- *int* **x0** - X coordinate of a position in the current image.
- *int* **y0** - Y coordinate of a position in the current image.
- *int* **x1** - X coordinate of a position in a source image, which is blended with the current image.
- *int* **y1** - Y coordinate of a position in a source image, which is blended with the current image.
- *int* **width** - Width of the blending region.
- *int* **height** - Height of the blending region.
- *float* **scale** - Scale of blending:

  - If blended images are of the same format, the blended image is multiplied by scale value and is added to the destination image.
  - If a source image has one more channel compared to the current one, it will serve as alpha value. This channel value is multiplied by scale and is used to alpha blend the images.
  - The default scale value is 1.0f.
- *int* **safe** - **1** for safe blending with respect to destination image boundaries; otherwise, **0**.

### Return value

Returns **1** if blending is successful; otherwise, **0**.
## int blur ( int radius , float gamma = 1.0f , int level = 0 )

Filters the image using two-pass Gaussian blur. Only the 2D or cube image can be blurred. Compressed and combined image formats are not supported.
### Arguments

- *int* **radius** - Blur filter radius, the number of neighbouring source pixels that are averaged for each blurred destination pixel. For example, if Radius = 2, two pixels from each side are taken and the blurring kernel is **5** x **5** pixels.
- *float* **gamma** - Gamma correction value. If **1** is provided, no gamma correction is applied. This is an optional argument.
- *int* **level** - Mip level for which the blurring effect is applied. This is an optional argument.

### Return value

**1** if the image was successfully blurred or the size of blur filter is 0; otherwise, **0**.
## int sharpen ( float radius , float intensity , float gamma = 1.0f , int sharp_only_lightness = true , int level = 0 )

Sharpens the image. Only the 2D or cube image can be sharpened. Compressed and combined image formats are not supported.
### Arguments

- *float* **radius** - Sharpen filter radius, the number of neighbouring source pixels (or subpixels) that are averaged for each sharpened destination pixel.
- *float* **intensity** - Filter intensity value.
- *float* **gamma** - Gamma correction value. If **1** is provided, no gamma correction is applied. This is an optional argument.
- *int* **sharp_only_lightness** - **1** to adjust sharpness of the lightness value only, **0** to sharpen all HSL values. This is an optional argument.
- *int* **level** - Mip level for which the sharpening effect is applied. This is an optional argument.

### Return value

**1** if the image was successfully sharpened or the size of sharpen filter is 0; otherwise, **0**.
## void clear ( )

Clears all data associated with the image and resets its type, format, size to default. Also the number of image layers and mipmaps is set to 1.
## int combine ( int new_format = -1 )


Converts the image to a combined format. The following conversions are available:


- RGB8 to RGB565
- RGBA8 to RGBA4 if the format is specified as RGBA4; otherwise, RGBA8 is converted to RGB5A1 by default
- RGBA16 to RGB10A2


### Arguments

- *int* **new_format** - Combined format to convert the image into. This is an optional argument. If no format is specified, default conversion will be performed.

### Return value

**1** if the conversion into the combined format is successful; otherwise, **0**.
## int combineMipmaps ( )

Combines the loaded 2D image with the mipmap image. Only one mipmap image can be combined. Compressed image formats cannot be combined.
### Return value

**1** if the image and a mipmap are successfully combined; otherwise, **0**.
## int compare ( Image image , int x0 , int y0 , int x1 , int y1 , int width , int height , int threshold = 0 )

Compares a region of a specified image with a specified region of the current image. Compressed, combined, half-float and float formats are not supported.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Source image to compare the loaded image with.
- *int* **x0** - X coordinate on the loaded image.
- *int* **y0** - Y coordinate on the loaded image.
- *int* **x1** - X coordinate on the source image.
- *int* **y1** - Y coordinate on the source image.
- *int* **width** - Width of a region to compare.
- *int* **height** - Height of a region to compare.
- *int* **threshold** - A threshold to compare.

### Return value

**1** if the regions match; otherwise, **0**.
## int compress ( int new_format = -1 )


Converts the image to a compressed format. The following conversions are available:


- R8 to ATI1
- RG8 to ATI2
- RGB8 to DXT1
- RGBA8 to DXT3, DXT5(by default)
- ZLC1 to ZLC1
- ZLC2 to ZLC2


### Arguments

- *int* **new_format** - Format to compress the image into. This is an optional argument. If no format is specified, default conversion will be performed.

### Return value

**1** if the image is compressed successfully; otherwise, **0**.
## int convertToFormat ( int new_format )

Converts the image to a specified format. Compressed and combined images are automatically decompressed/decombined.
### Arguments

- *int* **new_format** - Target format to convert the image into. See the **[IMAGE_FORMAT_*()](../../...md#AUTO_FORMAT)** variables.

### Return value

**1** if the conversion is successful; otherwise, **0**.
## int convertToType ( int type )


Converts the image to a specified type. The following conversions are possible:


| Source type | Target type | Target dimensions |
|---|---|---|
| 2D (height should be proportional to width) | 3D | width � height � height/width |
| 2D (height should divide by four, width should divide by three) | Cube | width/4 � height/3 |
| 3D | 2D | width � height*depth |
| 3D | 2D texture array | width � height |
| Cube | 2D | width*4 � height*3 |
| Cube | 2D array texture | width � height |
| 2D array texture | 2D | width � height*number of texture layers |


### Arguments

- *int* **type** - Type for conversion. One of the [IMAGE_*](#IMAGE_2D) types.

### Return value

**1** if the conversion is successful; otherwise, **0**.
## void assignFrom ( const Image & src_image )

Copies the data from the specified source image. The size of the image shall be updated according to the size of the source image (unlike the [*resizeFrom()*](#resizeFrom_Image_int_int) method).
### Arguments

- *const [Image](../../../api/library/common/class.image_usc.md) &* **src_image** - Source image.

## bool resizeFrom ( )

Copies the data from the specified source image, resizing the source. The source image shall be resized (enlarged/shrinked) to fit the size of the image.
### Arguments

### Return value

**1** if the data was successfully copied from the source image; otherwise, **0**.
## int copy ( const Image & src_image , int layer )


Copies data from the specified source image according to the specified **layer** parameter. Depending on the image and the source image types the **layer** parameter either defines the index of the layer/face to copy data FROM (source), or the index of the layer/face to copy data TO (destination):


| Image | Source Image | Copy |
|---|---|---|
| Cube | 2D | Specified source 2D image is copied to the face of the cubemap image specified by the layer argument in the **[0; 5]** range: 2D_image **TO** cubemap_face[ ***layer*** ] |
| 2D Array | 2D | Specified source 2D image is copied to the specified layer of the 2D image array: 2D image **TO** 2D_array[ ***layer*** ] |
| Cube Array | Cube | Specified source cubemap image (all 6 faces) is copied to the specified layer of the cubemap image array: cubemap_image **TO** cubemap_array[ ***layer*** ] |
| 2D | Cube | Face of the source cubemap image specified by the layer argument in the **[0; 5]** range is copied to the 2D image: 2D_image **FROM** cubemap_face[ ***layer*** ] |
| 2D | 2D Array | Specified layer of the source 2D image array is copied to the 2D image: 2D image **FROM** 2D_array[ ***layer*** ] |
| Cube | Cube Array | Specified layer of the source сubemap image array is copied to the cubemap image (all 6 faces): cubemap_image **FROM** cubemap_array[ ***layer*** ] |


```cpp
src_image.load(src_image_path);
src_image.convertToFormat(IMAGE_FORMAT_RGB8);// 2D 1024x1024 image

dest_image.create2DArray(1024, 1024, 5, IMAGE_FORMAT_RGB8);
dest_image.copy(src_image, 4); // created 2D image is copied to the 5th layer of the 2D image array

```


### Arguments

- *const [Image](../../../api/library/common/class.image_usc.md) &* **src_image** - Source image.
- *int* **layer** - Zero-based index defining layer/face TO or FROM which the data is to be copied.

### Return value

**1** if the data is copied successfully; otherwise, **0**.
## int copy ( const Image & src_image , int dest_channel , int src_channel )

Copies a given channel from the specified image to the specified image channel.
### Arguments

- *const [Image](../../../api/library/common/class.image_usc.md) &* **src_image** - Source image.
- *int* **dest_channel**
- *int* **src_channel** - Source channel.

### Return value

**1** if the channel is copied successfully from the source image; otherwise, **0**.
## int copy ( const Image & src_image , int x_dst , int y_dst , int x_src , int y_src , int width , int height , int safe = 0 )

Copies a data fragment with specified width, height, and coordinates from the source image.
### Arguments

- *const [Image](../../../api/library/common/class.image_usc.md) &* **src_image** - Source image, from which a fragment is to be copied.
- *int* **x_dst** - X coordinate of a position in the image, to which the data fragment is to be copied.
- *int* **y_dst** - Y coordinate of a position in the image, to which the data fragment is to be copied.
- *int* **x_src** - X coordinate of a position in a source image, starting from which the data fragment is to be copied.
- *int* **y_src** - Y coordinate of a position in a source image, starting from which the data fragment is to be copied.
- *int* **width** - Width of the fragment to be copied from the source image, in pixels.
- *int* **height** - Height of the fragment to be copied from the source image, in pixels.
- *int* **safe** - true for safe copying with respect to destination image boundaries; otherwise, false. > **Notice:** The safe flag doesn't provide safe copying with respect to source image boundaries.

### Return value

**1** if the specified fragment was successfully copied from the source image; otherwise, **0**.
## int copyFast ( const Image & src_image , int x_dst , int y_dst , int x_src , int y_src , int w , int h )

Copies a data fragment with specified width, height, and coordinates from the source image.
### Arguments

- *const [Image](../../../api/library/common/class.image_usc.md) &* **src_image** - Source image, from which a fragment is to be copied.
- *int* **x_dst** - X coordinate of a position in the image, to which the data fragment is to be copied.
- *int* **y_dst** - Y coordinate of a position in the image, to which the data fragment is to be copied.
- *int* **x_src** - X coordinate of a position in a source image, starting from which the data fragment is to be copied.
- *int* **y_src** - Y coordinate of a position in a source image, starting from which the data fragment is to be copied.
- *int* **w** - Width of the fragment to be copied from the source image, in pixels.
- *int* **h** - Height of the fragment to be copied from the source image, in pixels.

### Return value

**1** if the specified fragment was successfully copied from the source image; otherwise, **0**.
## int create2D ( int width , int height , int format , int num_mipmaps = 1 , int clear = 1 , int allocate = 1 )

Creates an empty 2D image filled with black color.
### Arguments

- *int* **width** - Required width, in pixels.
- *int* **height** - Required height, in pixels.
- *int* **format** - Required format. See the [*IMAGE_FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument. If the value is smaller than 1, an assertion is raised.
- *int* **clear** - Positive number to fill the image with black color, **0** not to fill. This optional argument can be set to **0** if new data will fully overwrite the data existing in the memory.
- *int* **allocate** - Positive number to allocate memory for the created image. This value should be always set to **1**.

### Return value

**1** if 2D image is successfully created; otherwise, **0**.
## int create2DArray ( int width , int height , int num_layers , int format , int num_mipmaps = 1 , int clear = 1 , int allocate = 1 )

Creates an empty 2D texture array filled with black color.
### Arguments

- *int* **width** - Required width, in pixels.
- *int* **height** - Required height, in pixels.
- *int* **num_layers** - Number of texture layers.
- *int* **format** - Required format. See the [*IMAGE_FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument. If the value is smaller than 1, an assertion is raised.
- *int* **clear** - Positive number to fill the texture array with black color, **0** not to fill. This optional argument can be set to **0** if new data will fully overwrite the data existing in the memory.
- *int* **allocate** - Positive number to allocate memory for the created image. This value should be always set to **1**.

### Return value

**1** if 2D texture array is successfully created; otherwise, **0**.
## int create3D ( int width , int height , int depth , int format , int num_mipmaps = 1 , int clear = 1 , int allocate = 1 )

Creates an empty 3D image filled with black color.
### Arguments

- *int* **width** - Required width, in pixels.
- *int* **height** - Required height, in pixels.
- *int* **depth** - Required depth.
- *int* **format** - Required format. See the [*IMAGE_FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument. If the value is smaller than 1, an assertion is raised.
- *int* **clear** - Positive number to fill the image with black color, **0** not to fill. This optional argument can be set to **0** if new data will fully overwrite the data existing in the memory.
- *int* **allocate** - Positive number to allocate memory for the created image. This value should be always set to **1**.

### Return value

**1** if 3D image is successfully created; otherwise, **0**.
## void create3DTurbulence ( int size , float scale , int frequency , int seed )

Creates a 3D turbulence image (RGBA8).
### Arguments

- *int* **size** - 3D image size, in pixels. Width, height, and depth are equal.
- *float* **scale** - Scaling factor applied to the displacement amount.
- *int* **frequency** - Base frequency, determines how rapidly the displacement amount changes. Increasing this value creates more turbulence.
- *int* **seed** - Specifies the initial number used for noise generation. Different Seed values produce different random variations and can be useful in changing the result. Keep in mind, that you should use the same Seed value when you want to retain the same variations.

## int createCube ( int width , int height , int format , int num_mipmaps = 1 , int clear = 1 , int allocate = 1 )

Creates the empty cube image filled with black color.
### Arguments

- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.
- *int* **format** - Texture format. See the [*IMAGE_FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument.
- *int* **clear** - **1** to fill the image with black color, **0** is not to fill. This optional argument can be set to **0** if new data will fully overwrite the data existing in the memory.
- *int* **allocate** - **1** to allocate memory for the created image. This value should be always set to **1**.

### Return value

**1** if the cube image is successfully created; otherwise, **0**.
## int createCubeArray ( int width , int height , int num_layers , int format , int num_mipmaps = 1 , int clear = 1 , int allocate = 1 )

Creates the empty cube array image filled with black color.
### Arguments

- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.
- *int* **num_layers** - Number of image layers.
- *int* **format** - Texture format. See the [*IMAGE_FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument.
- *int* **clear** - 1 to fill the image with black color, **0** is not to fill. This optional argument can be set to **0** if new data will fully overwrite the data existing in the memory.
- *int* **allocate** - **1** to allocate memory for the created image. This value should be always set to **1**.

### Return value

**1** if the cube array image is successfully created; otherwise, **0**.
## int createMipmaps ( int filter = FILTER_LINEAR , float gamma = 1.0f )

Generates mipmaps for the image. Mipmaps cannot be created for compressed and combined image formats.
### Arguments

- *int* **filter** - Filter type to be used: linear or point. The default filter is linear. See the [Unigine::Image Enumerations with FILTER_* prefixes](#FILTER_LINEAR).
- *float* **gamma** - Gamma correction value. If **1** is provided, no gamma correction is applied. This is an optional argument.

### Return value

**1** if the mipmaps are generated successfully; otherwise, **0**.
## int createMipmapsCubeGGX ( int quality )

Generates GGX mipmaps on CPU with the specified quality, of course slower and with lower quality than on GPU but it provides the result synchronously (actually this should be the only case, when this method is to be used).
### Arguments

- *int* **quality** - Quality of GGX mipmaps. One of the *[GGX_MIPMAPS_QUALITY](#GGX_MIPMAPS_QUALITY)* values.

### Return value

**1** if the mipmaps are generated successfully; otherwise, **0**.
## int removeMipmaps ( )

Removes mipmaps generated for the image.
### Return value

**1** if mipmaps generated for the image are removed successfully; otherwise, **0**.
## int decombine ( )


Automatically converts the image from the combined format to a correct one. The following conversions are available:


- RGB565 to RGB8
- RGBA4 to RGBA8
- RGB5A1 to RGBA8
- RGB10A2 to RGBA16


### Return value

**1** if the image is successfully converted from the combined format; otherwise, **0**.
## int decombineMipmaps ( )

Decombines the loaded 2D-image and the mipmap images. The number of mipmaps must be larger than 1. Compressed image formats cannot be decombined.
### Return value

**1** if the 2D-image and mipmap image are successfully decombined; otherwise, **0**.
## int decompress ( )


Decompresses the image from the compressed format to a correct one. The following conversions are available:


- DXT1 to RGB8
- DXT1 without alpha data to RGB8
- DXT3 to RGBA8
- DXT5 to RGBA8
- ATI1 to R8
- ATI2 to RG8


### Return value

**1** if the image was successfully decompressed; otherwise, **0**.
## int extrude ( int pixels )

Extrudes contour of the image in the alpha=0 region on the given number of pixels. Only images of the [RGBA8](#FORMAT_RGBA8) and [RGBA16](#FORMAT_RGBA16) formats can be extruded.
### Arguments

- *int* **pixels** - Number of contour pixels.

### Return value

**1** if the image contour is successfully extruded; otherwise, **0**.
## int flipX ( )

Flips the 2D image horizontally. Compressed and combined image formats are not supported.
### Return value

**1** if the image is successfully flipped; otherwise, **0**.
## int flipY ( )

Flips the 2D image vertically. Compressed and combined image formats are not supported.
### Return value

**1** if the image is successfully flipped; otherwise, **0**.
## int hasMipmaps ( )

Returns a value indicating if the source image has mipmaps.
### Return value

**1** if the image has mipmaps; otherwise, **0**.
## int info ( string path )


Retrieves information about the specified image by it's path and stores it into current **Image** instance. The following file formats are supported:


- *.texture
- *.tga
- *.jpg
- *.png
- *.dds
- *.psd
- *.ies
- tif

  - *.tif
  - *.tiff


### Arguments

- *string* **path** - Name of the image file.

### Return value

**1** if the information was successfully retrieved and recognized; otherwise, **0**.
## int invert ( )

Inverts values of all the image channels. Only [R8](#FORMAT_R8), [RG8](#FORMAT_RG8), [RGB8](#FORMAT_RGB8), [RGBA8](#FORMAT_RGBA8), [R16](#FORMAT_R16), [RG16](#FORMAT_RG16), [RGB16](#FORMAT_RGB16), [RGBA16](#FORMAT_RGBA16), [R32F](#FORMAT_R32F), [RG32F](#FORMAT_RG32F), [RGB32F](#FORMAT_RGB32F) and [RGBA32F](#FORMAT_RGBA32F) formats can be inverted.
### Return value

**1** if the image is inverted successfully; otherwise, **0**.
## int load ( string file , int mip_offset )

Loads an image from a specified file. The [following file formats](#intro) are supported.
### Arguments

- *string* **file** - Name of the image file.
- *int* **mip_offset** - Mipmap offset.

### Return value

**1** if the image is loaded successfully; otherwise, **0**.
## int load ( string file )

Loads an image from the specified file. The [following file formats](#intro) are supported.
### Arguments

- *string* **file** - Name of the image file.

### Return value

**1** if the image is loaded successfully; otherwise, **0**.
## int normalize ( )

Creates a three-component normal map out of the image.
### Return value

**1** if normalization was successful; otherwise, **0**.
## int resize ( int new_width , int new_height , int filter = FILTER_LINEAR )

Resizes the image. Only the 2D or cube image can be resized. Compressed and combined image formats cannot be resized.
### Arguments

- *int* **new_width** - New image width.
- *int* **new_height** - New image height.
- *int* **filter** - Filter type to be used: linear or point. The default filter is linear. See the [Unigine::Image Enumerations with FILTER_* prefixes](#FILTER_LINEAR).

### Return value

**1** if the image is resized successfully; otherwise, **0**.
## int rotate ( int angle )

Rotates the image by a given angle (with the step of 90 degrees). Only the 2D or cube image can be rotated. Compressed and combined image formats cannot be rotated.
### Arguments

- *int* **angle** - Angle, that will be multiplied by the step (angle * 90) to set the image rotation degree.

### Return value

**1** if the image is rotated successfully; otherwise, **0**.
## bool save ( )

Saves the image to a file with the specified name. The [following file formats](#intro) are supported.
### Arguments

### Return value

**1** if the image is saved successfully; otherwise, **0**.
## bool save ( float quality )

Saves the image to a specified file. The [following file formats](#intro) are supported.
### Arguments

- *float* **quality** - Quality of JPG compression in range **[0;1]**.

### Return value

**1** if the image is saved successfully; otherwise, **0**.
## int sign ( )

Converts the image from unsigned type to signed char. Only R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, ATI1 and ATI2 formats can be converted.
### Return value

**1** if the image has been converted successfully; otherwise, **0**.
## void swap ( Image image )

Swaps the data of the current image with the source image.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Source image.

## Pixel toPixel ( int format , vec4 color )

Converts a [vec4](../../../api/library/math/class.vec4_usc.md) color vector (R, G, B, A) to Pixel color depending on the specified image format.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.
- *vec4* **color** - Color [vec4](../../../api/library/math/class.vec4_usc.md) vector (R, G, B, A) with components normalized in range [0.0f; 1.0f]

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## vec4 toVec4 ( int format , Pixel p )

Converts Pixel color to a [vec4](../../../api/library/math/class.vec4_usc.md) color vector (R, G, B, A) depending on the specified image format.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.
- *Pixel* **p** - Pixel color represented by a [Pixel structure](#pixel).

### Return value

Color [vec4](../../../api/library/math/class.vec4_usc.md) vector (R, G, B, A). Each component is normalized in range [0.0f; 1.0f]
## int getNumChannels ( int format )

Returns the number of channels for the specified image format.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

Number of channels for the specified image format.
## int getPixelSize ( int format )

Returns the pixel size for the specified image format. Not available for compressed image formats (DXT1, DXT3, DXT5, ATI1, ATI2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

Pixel size for the specified image format.
## int getBlockSize ( int format )

Returns the block size for the specified image format. Available for compressed image formats only (DXT1, DXT3, DXT5, ATI1, ATI2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

Block size for the specified image format.
## int invertChannel ( int channel )

Inverts the values stored in the specified channel. Channels of images of half (*FORMAT_R16F* to *FORMAT_RGBA16F*) and float (*FORMAT_R32F* to *FORMAT_RGBA32F*) formats cannot be inverted.
### Arguments

- *int* **channel** - Number of the channel to be inverted, in the range from 0 to the [total number of channels](#getNumChannels_int).

### Return value

**1** if the specified channel is inverted successfully; otherwise, **0**.
## int getRawFormat ( int format )

Returns the closest RAW format of the uncompressed image.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

Identifier of the uncompressed image (stored in R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F format).
## void calcRange ( dvec2 & range )

Calculates the image range for all available channels in total.
### Arguments

- *dvec2 &* **range** - The vector to store the image range (min and max values).

## void calcRange ( dvec2 & r , dvec2 & g , dvec2 & b , dvec2 & a )

Calculates the image range for each channel separately.
### Arguments

- *dvec2 &* **r** - The vector to store the R channel range (min and max values).
- *dvec2 &* **g** - The vector to store the G channel range (min and max values).
- *dvec2 &* **b** - The vector to store the B channel range (min and max values).
- *dvec2 &* **a** - The vector to store the A channel range (min and max values).

## void changeRange ( const dvec4 & range )


Changes the image range.


> **Notice:** The range of the final image will be clamped, if the set range values exceed the maximum values of the image format.


### Arguments

- *const dvec4 &* **range** - Vector that stores the range values: x and y coordinates of the value specify the original range, z and w specify the new range.

## void changeRange ( const dvec4 & range_r , const dvec4 & range_g , const dvec4 & range_b , const dvec4 & range_a )


Changes the image range for each channel separately.


> **Notice:** The range of the final image will be clamped, if the set range values exceed the maximum values of the image format.


### Arguments

- *const dvec4 &* **range_r** - Vector that stores the range values for the R channel: x and y coordinates of the value specify the original range, z and w specify the new range.
- *const dvec4 &* **range_g** - Vector that stores the range values for the G channel: x and y coordinates of the value specify the original range, z and w specify the new range.
- *const dvec4 &* **range_b** - Vector that stores the range values for the B channel: x and y coordinates of the value specify the original range, z and w specify the new range.
- *const dvec4 &* **range_a** - Vector that stores the range values for the A channel: x and y coordinates of the value specify the original range, z and w specify the new range.

## void normalizeRange ( int per_cahnnel )

Normalizes the image range either per channel or for all channels altogether.
### Arguments

- *int* **per_cahnnel** - **1** if per-channel normalization is required; otherwise, **0**.

## int flipCubemapX ( )

Flips the cubemap image along the X axis.
### Return value

**1** if the cubemap is flipped successfully; otherwise, **0**.
## int flipCubemapY ( )

Flips the cubemap image along the Y axis.
### Return value

**1** if the cubemap is flipped successfully; otherwise, **0**.
## int flipCubemapZ ( )

Flips the cubemap image along the Z axis.
### Return value

**1** if the cubemap is flipped successfully; otherwise, **0**.
## Vector<String> getSupportedLoadExtensions ( )

Returns the list of supported file extensions for loading images.
### Return value

Vector of [supported file extensions](../../../api/library/common/class.image_usc.md#load_cstr_int_int) for loading images.
## int isSupportedLoadExtension ( string extension )

Returns a value indicating if the specified file extension is supported for loading.
### Arguments

- *string* **extension** - File extension to check (without a leading dot).

### Return value

**1** if the file extension is supported for loading; otherwise, **0**.
## int isSupportedLoad ( string path )

Returns a value indicating if the specified file path is supported for loading. This method extracts the file extension from the provided path and checks if loading an image with that extension is supported.
### Arguments

- *string* **path** - File path to check.

### Return value

**1** if the file path is supported for loading; otherwise, **0**.
## Vector<String> getSupportedSaveExtensions ( )

Returns the list of supported file extensions for saving images.
### Return value

Vector of [supported file extensions](../../../api/library/common/class.image_usc.md#save_cstr_int) for saving images.
## int isSupportedSaveExtension ( string extension )

Returns a value indicating if the specified file extension is supported for saving.
### Arguments

- *string* **extension** - File extension to check (without a leading dot).

### Return value

**1** if the file extension is supported for loading; otherwise, **0**.
## int isSupportedSaveExtension ( string extension , SaveImageInfo save_info )

Returns a value indicating if the specified file extension is supported for saving with provided image parameters. This method uses **SaveImageInfo** structure to determine the properties of the image, such as its format, dimensions, depth, layers and mipmaps.
### Arguments

- *string* **extension** - File extension to check (without a leading dot).
- *SaveImageInfo* **save_info** - Structure to store image information.

## int isSupportedSave ( string path )

Returns a value indicating if the specified file path is supported for saving. This method extracts the file extension from the provided path and checks if saving an image with that extension is supported.
### Arguments

- *string* **path** - File path to check.

### Return value

**1** if the file path is supported for saving; otherwise, **0**.
## int getRawFormat ( )

Returns the closest RAW format of the uncompressed image based on the object's current format.
### Return value

Identifier of the uncompressed image (stored in R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F format).
