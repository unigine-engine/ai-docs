# Unigine::Image Class (CPP)

**Header:** #include <UnigineImage.h>


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


### Pixels


The color of each pixel of an image is represented by the **Pixel** structure. Depending on the **image format**, values are written either to the **integer** view (Pixel.i) or the **float** view (Pixel.f) of the structure.


The **Pixel** type is implemented as a union structure where ***Pixel.i*** and ***Pixel.f*** overlap in memory. Writing to one view overrides the memory of the other. This means that only the correct accessor should be used depending on the format (see table below).


| Image type | Image format | Accessor | Valid Range in Pixel (per channel, via accessor) |
|---|---|---|---|
| **8-bit unsigned formats** | [R8](#FORMAT_R8), [RG8](#FORMAT_RG8), [RGB8](#FORMAT_RGB8), [RGBA8](#FORMAT_RGBA8) | ***Pixel.i*** | Pixel color components are in range from **0** to **255**. |
| **16-bit unsigned formats** | [R16](#FORMAT_R16), [RG16](#FORMAT_RG16), [RGB16](#FORMAT_RGB16), [RGBA16](#FORMAT_RGBA16) | ***Pixel.i*** | Pixel color components are in range from **0** to **65535**. |
| **16-bit float formats** | [R16F](#FORMAT_R16F), [RG16F](#FORMAT_RG16F), [RGB16F](#FORMAT_RGB16F), [RGBA16F](#FORMAT_RGBA16F) | ***Pixel.i*** | Pixel color components are in range from **0** to **65535**. |
| **32-bit float formats** | [R32F](#FORMAT_R32F), [RG32F](#FORMAT_RG32F), [RGB32F](#FORMAT_RGB32F), [RGBA32F](#FORMAT_RGBA32F) | ***Pixel.f*** | Full 32-bit float value range. |

 Best Practice
***Pixel.i*** and ***Pixel.f*** store the raw memory representation of color channels for all formats (int or float), with values potentially clipped to the representable range and alpha defaulting to 1.0. For example, for **16-bit float formats**, ***Pixel.i*** stores the raw half-float bits, which correspond to -HALF_MAX ... +HALF_MAX when converted to float.


- Use *[toPixel()](../../...md#toPixel_vec4_Pixel)* to convert color values to a Pixel. ```cpp Math::vec4 color(0.5f, 0.5f, 0.0f, 1.0f); Image::Pixel pixel = image->toPixel(color); image->set2D(x, y, pixel); ```
- Use *[toVec4()](../../...md#toVec4_Pixel_vec4)* to read pixels as normalized float values. ```cpp Image::Pixel pixel = image->get2D(x, y); Math::vec4 color = image->toVec4(pixel); ```


In this case, the image format is determined automatically and type conversion is performed correctly.


#### Usage Example


This sample component demonstrates how to:


- Create an image.
- Set color information for each pixel of the image using the [Pixel](#pixel) structure.
- Save the image to a file.
- Get current image format.
- Convert the image to another format.
- Use the created image as an albedo texture for a material assigned to an object.
- Get color information for each pixel of the image using the [Pixel](#pixel) structure.


[Create](../../../principles/component_system/component_system_cpp/index.md#workflow) a new class named **ImageClass** and copy **.h** and **.cpp** files into respective files of a class. Then [assign](../../../principles/component_system/component_system_cpp/index.md#workflow) a property generated for your component to any desired node of the *Object* type, to see its albedo texture replaced by a new created image.


<details>
<summary>ImageClass.h | Close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>
class ImageClass :
	public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(ImageClass, Unigine::ComponentBase);
	COMPONENT_INIT(init);

private:
	void init();

};


```

</details>


<details>
<summary>ImageClass.cpp | Close</summary>

```cpp
#include "ImageClass.h"
REGISTER_COMPONENT(ImageClass);

using namespace Unigine;

void ImageClass::init()
{
	// image size parameters
	const int ASPECT_RATIO = 1;
	const int width = 256;
	const int height = width / ASPECT_RATIO;

	ImagePtr image = Image::create();

	// creating an image of the specified size
	image->create2D(width, height, Image::FORMAT_RGBA8);

	// declaring a pixel to store color information
	Image::Pixel pixel;

	for (int x = 0; x < width; x++)
		for (int y = 0; y < height; y++)
		{
			// setting pixel components
			pixel.i.r = x;
			pixel.i.g = 0;
			pixel.i.b = 0;
			pixel.i.a = 195;

			// setting the color of the image pixel at (x,y)
			image->set2D(x, y, pixel);
		}

	// if a node is an object, we set our image as an albedo texture for its material
	if (getNode()->isObject()) {
		ObjectPtr obj = checked_ptr_cast<Object>(getNode());
		MaterialPtr material = obj->getMaterial(0)->inherit();

		// setting our image as an albedo texture of the material
		material->setTextureImage(material->findTexture("albedo"), image);
		obj->setMaterial(material, 0);
	}
	else {
		Log::message("\nNode is not an object!");
	}

	// saving our image to a *.DDS file
	image->save("myimage.dds");

	// printing current image format to the console
	Log::message("\nImage format: %s", image->getFormatName());

	// converting our image to the 32-bit float format
	image->convertToFormat(Image::FORMAT_RGBA32F);

	// printing image format after conversion to the console
	Log::message("\nImage format after conversion: %s", image->getFormatName());

	// saving a converted image to a *.DDS file
	image->save("myimage_converted.dds");

	// getting the first pixel for each row of the image and printing its color value to the console
	for (int x = 0; x < width; x++)
	{
		pixel = image->get2D(x, 0);
		Log::message("\nPixel(%d, 0) color = (%f,%f,%f,%f)", x, pixel.f.r, pixel.f.g, pixel.f.b, pixel.f.a);
	}

	// clearing the image
	image->clear();
}

```

</details>


### See Also


- C++ sample
- C# sample


## Image Class

### Enums

## FILE_COMPRESSION

| Name | Description |
|---|---|
| **FILE_COMPRESSION_DISABLE** = 0 | Image data is uncompressed. |
| **FILE_COMPRESSION_ZLC_LOW** = 1 | Fast compression used for images stored in the system memory (based on zlib library). |
| **FILE_COMPRESSION_ZLC_HIGH** = 2 | Compression used for images stored in the system memory (based on zlib library). It is used when a smaller file size is required, compared to [ZLC LOW](#FILE_COMPRESSION_ZLC_LOW) (compression is slower). |
| **FILE_COMPRESSION_LZ4_LOW** = 3 | LZ4 lossless data compression algorithm that is focused on compression and decompression speed. It belongs to the LZ77 family of byte-oriented compression schemes (greater file size, faster comression). |
| **FILE_COMPRESSION_LZ4_HIGH** = 4 | LZ4 lossless data compression algorithm that is focused on compression and decompression speed. It belongs to the LZ77 family of byte-oriented compression schemes (smaller file size, slower comression). |

## FILTER

| Name | Description |
|---|---|
| **FILTER_POINT** = 0 | A point mipmap filter. |
| **FILTER_LINEAR** = 1 | A linear mipmap filter. |
| **FILTER_MIN** = 2 | A minimum mipmap filter. |
| **FILTER_BLUR** = 3 | A blurring mipmap filter. |
| **FILTER_SHARPEN** = 4 | A sharpening mipmap filter. |

## GGX_MIPMAPS_QUALITY

Quality of GGX mipmaps.
| Name | Description |
|---|---|
| **GGX_MIPMAPS_QUALITY_LOW** = 0 | Low quality of GGX mipmaps. |
| **GGX_MIPMAPS_QUALITY_MEDIUM** = 1 | Medium quality of GGX mipmaps. |
| **GGX_MIPMAPS_QUALITY_HIGH** = 2 | High quality of GGX mipmaps. |
| **GGX_MIPMAPS_QUALITY_ULTRA** = 3 | Ultra quality of GGX mipmaps. |

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
## size_t getPixelsSize () const

Returns the current size of all pixels of the image.
### Return value

Current size of all pixels of the image, in bytes.
## size_t getNumPixels () const

Returns the current number of pixels in the image.
### Return value

Current number of pixels.
## void setFileCompression ( Image::FILE_COMPRESSION compression )

Sets a new file compression type used for the image.
### Arguments

- *[Image::FILE_COMPRESSION](../../../api/library/common/class.image_cpp.md#FILE_COMPRESSION)* **compression** - The file compression type to be used for the image. One of the *[FILE_COMPRESSION_*](#FILE_COMPRESSION_LZ4_HIGH)* values.

## Image::FILE_COMPRESSION getFileCompression () const

Returns the current file compression type used for the image.
### Return value

Current file compression type to be used for the image. One of the *[FILE_COMPRESSION_*](#FILE_COMPRESSION_LZ4_HIGH)* values.
---

## static ImagePtr create ( )

Default constructor. An empty instance with default parameters is created.
## static ImagePtr create ( const char * name )

Constructor. Creates an image loading data from the specified file.
### Arguments

- *const char ** **name** - Image file name.

## static ImagePtr create ( const Ptr < Image > & image )

Constructor. Creates an image by copying a given source image.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Source image.

## bool allocData ( bool clear = true )

Allocates memory for the image data.
### Arguments

- *bool* **clear** - Clear flag: set **true** to fill allocated memory with zero-values; otherwise, set **false**.

### Return value

**true** if memory for the image data is allocated successfully; otherwise, **false**.
## void clearData ( )

Clears all image data.
## void set ( size_t offset , const Math:: dvec4 & value )

Sets a value for a pixel by its offset. Compressed and combined image formats are not supported.
The code below sets the specified color value for all image pixels:


```cpp
void image_set_pixel_color(ImagePtr& image, const Math::dvec4& value)
{
	// getting image size
	int width = image->getWidth();
	int height = image->getHeight();

	// running through all image pixels of the specified channel in a loop
	for (int y = 0; y < height; y++)
	{
		for (int x = 0; x < width; x++)
		{
			// composing pixel offset from its coords; (0, 0) - top-left corner
			int offset = x + y * width;

			// setting a value for a pixel by its offset
			image->set(offset, value);
		}
	}
}

```


### Arguments

- *size_t* **offset** - Pixel offset: `offset = image_width * Y + X`, ( 0 , 0) - top left corner of the image.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - RGBA color of a pixel with the specified ID.

## void get ( size_t offset , Math:: dvec4 & value ) const

Gets a value for a pixel by its offset and puts it to the target buffer  `value`.
### Arguments

- *size_t* **offset** - Pixel offset: `offset = image_width * Y + X`, ( 0 , 0) - top left corner of the image.
- *Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Target buffer to receive an RGBA color of a pixel with the specified ID.

## Math:: vec4 get ( const Math::ivec2& coord , int offset ) const

Returns image data for the specified pixel coordinates and mipmap offset as a four-component vector.
### Arguments

- *const  Math::ivec2&* **coord** - Pixel coordinates (X, Y) - X in range [0; width], Y in range [0; height].
- *int* **offset** - Mipmap offset value.

### Return value

A [vec4](../../../api/library/math/class.vec4_cpp.md) vector (R, G, B, A) containing image data for the specified pixel coordinates, with components normalized in the **[0.0f; 1.0f]** range.
## void get ( const Math::ivec2& coord , int offset , Math:: vec4 & p00 , Math:: vec4 & p01 , Math:: vec4 & p10 , Math:: vec4 & p11 ) const

Returns image data for the specified pixel coordinates and mipmap offset (along with neighboring pixels) as a set of four-component vectors.
### Arguments

- *const  Math::ivec2&* **coord** - Pixel coordinates (X, Y) - X in range [0; width], Y in range [0; height].
- *int* **offset** - Mipmap offset value.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **p00** - A [vec4](../../../api/library/math/class.vec4_cpp.md) vector (R, G, B, A) containing image data for the specified pixel coordinates (X, Y), with components normalized in the **[0.0f; 1.0f]** range.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **p01** - A [vec4](../../../api/library/math/class.vec4_cpp.md) vector (R, G, B, A) containing image data for the neighboring pixel coordinates (X, Y+1), with components normalized in the **[0.0f; 1.0f]** range.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **p10** - A [vec4](../../../api/library/math/class.vec4_cpp.md) vector (R, G, B, A) containing image data for the neighboring pixel coordinates (X+1, Y), with components normalized in the **[0.0f; 1.0f]** range.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **p11** - A [vec4](../../../api/library/math/class.vec4_cpp.md) vector (R, G, B, A) containing image data for the neighboring pixel coordinates (X+1, Y+1), with components normalized in the **[0.0f; 1.0f]** range.

## void get8F ( const Math:: ivec2 & coord , Math:: vec4 & p ) const

Returns a set of 8-bit float values stored in the specified image pixel and neighboring ones and puts them to the output vector.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **p** - Output [vec4](../../../api/library/math/class.vec4_cpp.md) vector (P00, P01, P10, P11) to receive 8-bit float values stored in the specified image pixel and neighboring ones: > **Notice:** Values are normalized in the **[0.0f; 1.0f]** range.

  - **P00** - (X, Y)
  - **P01** - (X, Y+1)
  - **P10** - (X+1, Y)
  - **P11** - (X+1, Y+1)

## float get8F ( const Math:: ivec2 & coord ) const

Returns an 8-bit float value stored in the specified pixel of the image.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.

### Return value

An 8-bit float value stored in the specified pixel of the image normalized in the **[0.0f; 1.0f]** range.
## void get16F ( const Math:: ivec2 & coord , Math:: vec4 & p ) const

Returns a set of 16-bit float values stored in the specified image pixel and neighboring ones and puts them to the output vector.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **p** - Output [vec4](../../../api/library/math/class.vec4_cpp.md) vector (P00, P01, P10, P11) to receive 16-bit float values stored in the specified image pixel and neighboring ones: > **Notice:** Values are normalized in the **[0.0f; 1.0f]** range.

  - **P00** - (X, Y)
  - **P01** - (X, Y+1)
  - **P10** - (X+1, Y)
  - **P11** - (X+1, Y+1)

## float get16F ( const Math:: ivec2 & coord ) const

Returns a 16-bit float value stored in the specified pixel of the image.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.

### Return value

A 16-bit float value stored in the specified pixel of the image normalized in the **[0.0f; 1.0f]** range.
## void get32F ( const Math:: ivec2 & coord , Math:: vec4 & p ) const

Returns a set of 32-bit float values stored in the specified image pixel and neighboring ones and puts them to the output vector.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.
- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **p** - Output [vec4](../../../api/library/math/class.vec4_cpp.md) vector (P00, P01, P10, P11) to receive 32-bit float values stored in the specified image pixel and neighboring ones: > **Notice:** Values are normalized in the **[0.0f; 1.0f]** range.

  - **P00** - (X, Y)
  - **P01** - (X, Y+1)
  - **P10** - (X+1, Y)
  - **P11** - (X+1, Y+1)

## float get32F ( const Math:: ivec2 & coord ) const

Returns a 32-bit float value stored in the specified pixel of the image.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Pixel coordinates (X, Y) - X in the [0; width] range, Y in the [0; height] range.

### Return value

A 32-bit float value stored in the specified pixel of the image normalized in the **[0.0f; 1.0f]** range.
## void set2D ( int x , int y , const Image::Pixel& p )

Sets a color for a given pixel of a 2D image. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

## void set2D ( const Math::ivec2& coord , const Image::Pixel& p )

Sets a color for a given pixel of a 2D image. Compressed formats are not supported.
### Arguments

- *const  Math::ivec2&* **coord** - Integer coordinates of a pixel in the following ranges: X - [0; width], Y - [0; height].
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

## Image::Pixel get2D ( int x , int y ) const

Returns a color of a given pixel of a 2D image. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get2D ( float x , float y ) const

Returns a color of a given pixel of a 2D image. Linear interpolation is used to get a color sample. Compressed formats are not supported.
### Arguments

- *float* **x** - X float coordinate of a pixel in range [0.0f; 1.0f].
- *float* **y** - Y float coordinate of a pixel in range [0.0f; 1.0f].

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get2D ( float x , float y , const Image::Pixel& skip_pixel ) const


Returns a color of a given pixel of a 2D image. Linear interpolation is used to get a color sample. Compressed formats are not supported.


> **Notice:** If at least one of four interpolated pixels is equal to **skip_pixel**, the method will return **skip_pixel**.


### Arguments

- *float* **x** - X float coordinate of a pixel in range [0.0f; 1.0f].
- *float* **y** - Y float coordinate of a pixel in range [0.0f; 1.0f].
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **skip_pixel** - Skip pixel color represented by a [Pixel structure](#pixel).

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get2D ( const Math::ivec2& coord ) const

Returns a color of a given pixel of a 2D image. Compressed formats are not supported.
### Arguments

- *const  Math::ivec2&* **coord** - Integer coordinates of a pixel in the following ranges: X - [0; width], Y - [0; height].

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get2D ( const Math::vec2& uv ) const

Returns a color of a given pixel of a 2D image. Linear interpolation is used to get a color sample. Compressed formats are not supported.
### Arguments

- *const  Math::vec2&* **uv** - Float coordinates of a pixel in range [0.0f; 1.0f].

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get2D ( const Math::vec2& uv , const Image::Pixel& skip_pixel ) const


Returns a color of a given pixel of a 2D image. Linear interpolation is used to get a color sample. Compressed formats are not supported.


> **Notice:** If at least one of four interpolated pixels is equal to **skip_pixel**, the method will return **skip_pixel**.


### Arguments

- *const  Math::vec2&* **uv** - Float coordinates of a pixel in range [0.0f; 1.0f].
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **skip_pixel** - Skip pixel color represented by a [Pixel structure](#pixel).

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## void set2DArray ( int x , int y , int layer , const Image::Pixel& p )

Sets a color of a given pixel. The image must be a 2D image array. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **layer** - Image layer number.
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

## void set2DArray ( const Math::ivec2& coord , int layer , const Image::Pixel& p )

Sets a color of a given pixel. The image must be a 2D texture array. Compressed formats are not supported.
### Arguments

- *const  Math::ivec2&* **coord** - Coordinates of a pixel.
- *int* **layer** - Image layer number.
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

## Image::Pixel get2DArray ( int x , int y , int layer ) const

Returns a color of a given pixel. The image must be a 2D texture array. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **layer** - Image layer number.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get2DArray ( float x , float y , int layer ) const

Returns a color of a given pixel. The image must be a 2D image array. Compressed formats are not supported. Linear interpolation is used to get a color sample.
### Arguments

- *float* **x** - X float coordinate of a pixel in range [0.0f; 1.0f].
- *float* **y** - Y float coordinate of a pixel in range [0.0f; 1.0f].
- *int* **layer** - Image layer number.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get2DArray ( const Math::ivec2& coord , int layer ) const

Returns a color of a given pixel. The image must be a 2D texture array. Compressed formats are not supported.
### Arguments

- *const  Math::ivec2&* **coord** - Coordinates of a pixel.
- *int* **layer** - Image layer number.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get2DArray ( const Math::vec2& uv , int layer ) const

Returns a color of a given pixel. The image must be a 2D texture array. Compressed formats are not supported.
### Arguments

- *const  Math::vec2&* **uv** - UV coordinates of a pixel.
- *int* **layer** - Image layer number.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## void set3D ( int x , int y , int z , const Image::Pixel& p )

Sets a color of a given pixel of a 3D image. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **z** - Z integer coordinate of a pixel in range [0; depth].
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

## void set3D ( const Math::ivec3& coord , const Image::Pixel& p )

Sets a color of a given pixel of a 3D image. Compressed formats are not supported.
### Arguments

- *const  Math::ivec3&* **coord** - Integer coordinates of a pixel in the following ranges: X - [0; width], Y - [0; height], Z - [0; depth].
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

## Image::Pixel get3D ( float x , float y , float z ) const

Returns a color of a given pixel of a 3D image. Linear interpolation is used to get a color sample. Compressed formats are not supported.
### Arguments

- *float* **x** - X float coordinate of a pixel in range [0.0f; 1.0f].
- *float* **y** - Y float coordinate of a pixel in range [0.0f; 1.0f].
- *float* **z** - Z float coordinate of a pixel in range [0.0f; 1.0f].

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get3D ( int x , int y , int z ) const

Returns a color of a given pixel of a 3D image. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **z** - Z integer coordinate of a pixel in range [0; depth].

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get3D ( const Math::ivec3& coord ) const

Returns a color of a given pixel of a 3D image. Compressed formats are not supported.
### Arguments

- *const  Math::ivec3&* **coord** - Integer coordinates of a pixel in the following ranges: X - [0; width], Y - [0; height], Z - [0; depth].

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get3D ( const Math::vec3& uvw ) const

Returns a color of a given pixel of a 3D image. Linear interpolation is used to get a color sample. Compressed formats are not supported.
### Arguments

- *const  Math::vec3&* **uvw** - Float coordinates of a pixel in range [0.0f; 1.0f].

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel get3DSmooth ( float x , float y , float z ) const


Returns a color of a given pixel obtained using linear interpolation. Compressed formats are not supported.


> **Notice:** This method returns pixel color with float components in the range [0.0f, 1.0f] regardless of the image format.


### Arguments

- *float* **x** - X float coordinate of a pixel in range [0.0f; 1.0f].
- *float* **y** - Y float coordinate of a pixel in range [0.0f; 1.0f].
- *float* **z** - Z float coordinate of a pixel in range [0.0f; 1.0f].

### Return value

Pixel color represented by a [Pixel structure](#pixel) with float components in the range [0.0f, 1.0f].
## Image::Pixel get3DSmooth ( const Math::vec3& uvw ) const


Returns a color of a given pixel obtained using linear interpolation. Compressed formats are not supported.


> **Notice:** This method returns pixel color with float components in the range [0.0f, 1.0f] regardless of the image format.


### Arguments

- *const  Math::vec3&* **uvw** - Float coordinates of a pixel in the range [0.0f; 1.0f].

### Return value

Pixel color represented by a [Pixel structure](#pixel) with float components in the range [0.0f, 1.0f].
## bool isCombinedFormat ( ) const

Returns a value indicating if the image is stored in a combined format (RGB565, RGBA4, RGB5A1 or RGB10A2).
### Return value

true if the image is in combined format; otherwise, false.
## bool isCombinedFormat ( int format )

Returns a value indicating if a given format is a combined format (RGB565, RGBA4, RGB5A1 or RGB10A2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

true if the specified format is a combined format; otherwise, false.
## bool isCompressedFormat ( ) const

Returns a value indicating if the image is stored in a compressed format (DXT1, DXT3, DXT5, ATI1, ATI2).
### Return value

true if the image is in a compressed format; otherwise, false.
## bool isCompressedFormat ( int format )

Returns a value indicating if a given format is a compressed format (DXT1, DXT3, DXT5, ATI1, ATI2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

true if the specified format is a compressed format; otherwise, false.
## void setCube ( int x , int y , int face , const Image::Pixel& p )

Sets a color of a given pixel. The image must be of the Cube type. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; depth].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **face** - Face number in range from 0 to 5.
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

## Image::Pixel getCube ( const Math::vec3& direction ) const

Returns a color of a given pixel. The image must be of the Cube type. Compressed formats are not supported.
### Arguments

- *const  Math::vec3&* **direction** - Cube direction vector used for color sampling.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel getCube ( float x , float y , int face ) const

Returns a color of a given pixel. The image must be of the Cube type. Compressed formats are not supported.
### Arguments

- *float* **x** - X float coordinate of a pixel in range [0.0f; 1.0f].
- *float* **y** - Y float coordinate of a pixel in range [0.0f; 1.0f].
- *int* **face** - Face number in range from 0 to 5.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel getCube ( int x , int y , int face ) const

Returns a color of a given pixel. The image must be of the Cube type. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **face** - Face number in range from 0 to 5.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel getCube ( const Math::ivec2& coord , int face ) const

Returns a color of a given pixel. The image must be of the Cube type. Compressed formats are not supported.
### Arguments

- *const  Math::ivec2&* **coord** - Coordinates of a pixel.
- *int* **face** - Face number in range from 0 to 5.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel getCube ( const Math::vec2& uv , int face ) const

Returns a color of a given pixel. The image must be of the Cube type. Compressed formats are not supported.
### Arguments

- *const  Math::vec2&* **uv** - UV coordinates of a pixel.
- *int* **face** - Face number in range from 0 to 5.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## void setCubeArray ( int x , int y , int face , int layer , const Image::Pixel& p )

Sets a color of a given pixel. The image must be of the Cube Array type. Compressed formats are not supported.
### Arguments

- *int* **x** - X integer coordinate of a pixel in range [0; width].
- *int* **y** - Y integer coordinate of a pixel in range [0; height].
- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Image layer number.
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

## void setCubeArray ( const Math::ivec2& coord , int face , int layer , const Image::Pixel& p )

Sets a color of a given pixel. The image must be of the Cube Array type. Compressed formats are not supported.
### Arguments

- *const  Math::ivec2&* **coord** - Coordinates of a pixel.
- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Image layer number.
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

## Image::Pixel getCubeArray ( const Math::vec3& direction , int layer ) const


Returns the color of a given pixel of the cube array image.


> **Notice:** Compressed formats are not supported.


### Arguments

- *const  Math::vec3&* **direction** - Cube direction vector used for color sampling.
- *int* **layer** - Image layer number.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel getCubeArray ( int v1 , int v2 , int face , int layer ) const

Returns a color of a given pixel. The image must be of the Cube Array type. Compressed formats are not supported.
### Arguments

- *int* **v1** - X integer coordinate of a pixel in range [0;width].
- *int* **v2** - Y integer coordinate of a pixel in range [0; height].
- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Image layer number.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel getCubeArray ( float v1 , float v2 , int face , int layer ) const

Returns a color of a given pixel. The image must be of the Cube Array type. Compressed formats are not supported.
### Arguments

- *float* **v1** - X integer coordinate of a pixel in range [0;width].
- *float* **v2** - Y integer coordinate of a pixel in range [0;height].
- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Image layer number.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel getCubeArray ( const Math::ivec2& coord , int face , int layer ) const

Returns a color of a given pixel. The image must be of the Cube Array type. Compressed formats are not supported.
### Arguments

- *const  Math::ivec2&* **coord** - Coordinates of a pixel.
- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Image layer number.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel getCubeArray ( const Math::vec2& uv , int face , int layer ) const

Returns a color of a given pixel. The image must be of the Cube Array type. Compressed formats are not supported.
### Arguments

- *const  Math::vec2&* **uv** - UV coordinates of a pixel.
- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Image layer number.

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## int getDepth ( int level = 0 ) const

Returns the image depth on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Image depth if the image exists (its depth is larger than 0); otherwise, 1.
## bool isFloatFormat ( ) const

Returns a value indicating if the image is stored in a float format (R32F, RG32F, RGB32F or RGBA32F).
### Return value

true if the image is in float format; otherwise, false is returned.
## bool isFloatFormat ( int format )

Returns a value indicating if a given format is a float format (R32F, RG32F, RGB32F or RGBA32F).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

true if the specified format is a float format; otherwise, false.
## int getFormat ( int num_channels , int format )

Returns a numerical code of the image format for the specified format and number of channels.
### Arguments

- *int* **num_channels** - Number of channels in the **[1; 4]** range.
- *int* **format** - Numerical code of the image format. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

Numerical code of the image format for the specified number of channels.
## const char * getFormatName ( int format )

Returns the name of the image format by the given format ID.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

Image format name. The following values can be returned: R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F, RGB565, RGBA4, RGB5A1, RGB10A2, DXT1, DXT3, DXT5, ATI1, ATI2.
## bool isHalfFormat ( ) const

Returns a value indicating if the image is stored in a half-float format (R16F, RG16F, RGB16F or RGBA16F).
### Return value

true if the image is in half-float format; otherwise, false.
## bool isHalfFormat ( int format )

Returns a value indicating if a given format is a half-float format (R16F, RG16F, RGB16F or RGBA16F).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

true if the specified format is a half-float format; otherwise, false.
## int getHeight ( int level = 0 ) const

Returns image height on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Image height if the image exists (its height is larger than 0); otherwise, 1.
## bool setChannelInt ( int channel , int value )

Sets an integer value for a given image channel. Compressed and combined image formats are not supported.
### Arguments

- *int* **channel** - Channel number in range from **0** to **number of channels - 1**.
- *int* **value** - Value in range from **0** to **255** (8-bit formats) or from **0** to **65535** (16-bit formats).

### Return value

**true** if the value is set successfully; otherwise, **false**.
## bool setChannelFloat ( int channel , float value )

Sets a float value for a given image channel. Compressed and combined image formats are not supported.
### Arguments

- *int* **channel** - Channel number in range from **0** to **number of channels - 1**.
- *float* **value** - Value in range from **0.0f** to **1.0f**.

### Return value

**true** if the value is set successfully; otherwise, **false**.
## bool swapChannels ( int channel_0 , int channel_1 )

Swaps values of two channels with the specified numbers. Compressed formats are not supported.
### Arguments

- *int* **channel_0** - Number of the first channel in range from **0** to **number of channels - 1**.
- *int* **channel_1** - Number of the second channel in range from **0** to **number of channels - 1**.

### Return value

**true** if the two specified channels were swapped successfully; otherwise, **false**.
## size_t getOffset ( int level ) const

Returns the image offset on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps.

### Return value

Image offset, in bytes.
## void setPixels ( unsigned char * OUT_pixels )


Sets image pixels to be taken from the specified source array.


> **Notice:** This method simply performs pointer assignment (without copying data), therefore, it is fast. But make sure the source is not accidentally modified or deleted when its lifetime expires or otherwise.


### Arguments

- *unsigned char ** **OUT_pixels** - Source array. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool setPixels ( const Ptr < Blob > & blob )

Sets image pixels by copying data (not just a pointer assignment) from a given source [blob](../../../api/library/common/class.blob_cpp.md).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../api/library/common/class.blob_cpp.md)> &* **blob** - Source blob containing image data to be copied.

### Return value

true if image data is set successfully; otherwise, false.
## unsigned char * getPixels ( ) const

Returns the pointer to the array of pixels.
The code below fills the specified channel of the image with the specified value:


```cpp
// int channel - number of the target channel to write the specified value
// unsigned char value   - color value
void image_fill_channel(ImagePtr& image, int channel, unsigned char value)
{
	// getting image pixels to a buffer
	unsigned char *data = image->getPixels();

	// getting image size and number of channels
	int channel_num = image->getNumChannels();
	int width = image->getWidth();
	int height = image->getHeight();

	// running through all image pixels of the specified channel in a loop
	for (int y = 0; y < height; y++)
	{
		for (int x = 0; x < width; x++)
		{
			// composing pixel id from its coords and channel number; (0, 0) - top-left corner
			int id = (x + y * width) * channel_num + channel;

			// setting a value for a pixel by its id
			data[id] = value;
		}
	}
}

```


### Return value

Pointer to the array of pixels.
## void getPixels ( const Ptr < Blob > & blob ) const

Copies the image data to a given target [blob](../../../api/library/common/class.blob_cpp.md).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../api/library/common/class.blob_cpp.md)> &* **blob** - Target blob.

## unsigned char * getPixels2D ( int level = 0 ) const

Returns the pointer to the array of pixels with the given mipmap level for the 2D image.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Pointer to the array of pixels.
## unsigned char * getPixels2DArray ( int layer , int level = 0 ) const

Returns the pointer to the array of pixels with the given mipmap level and image layer for the 2D Array image.
### Arguments

- *int* **layer** - Number of the image layer.
- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Pointer to the array of pixels.
## unsigned char * getPixels3D ( int level = 0 ) const

Returns the pointer to the array of pixels with the given mipmap level for the 3D image.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Pointer to the array of pixels.
## unsigned char * getPixelsCube ( int face , int level = 0 ) const

Returns the pointer to the array of pixels with the given mipmap level for the cube image.
### Arguments

- *int* **face** - Face number in range from 0 to 5.
- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Pointer to the array of pixels.
## unsigned char * getPixelsCubeArray ( int face , int layer , int level = 0 ) const

Returns the pointer to the array of pixels with the given mipmap level and image layer for the Cube Array image.
### Arguments

- *int* **face** - Face number in range from 0 to 5.
- *int* **layer** - Number of the image layer.
- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Pointer to the array of pixels.
## size_t getPixelsSize ( int format , int w , int h )

Returns the size of all pixels for the image of the specified format and size.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.
- *int* **w** - Image width, in pixels.
- *int* **h** - Image width, in pixels.

### Return value

Size of all pixels of the specified image, in bytes.
## bool isRawFormat ( ) const

Returns a value indicating if the image is uncompressed (stored in R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F, RGB565, RGBA4, RGB5A1 or RGB10A2 format).
### Return value

true if the image is uncompressed; otherwise, false.
## bool isRawFormat ( int format )

Returns a value indicating if a given format is an uncompressed format (R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F, RGB565, RGBA4, RGB5A1 or RGB10A2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

true if the specified format is an uncompressed format; otherwise, false.
## size_t getSize ( ) const

Returns the current image size.
### Return value

Image size, in bytes.
## size_t getSize ( int level ) const

Returns the current image size.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps.

### Return value

Image size in bytes.
## size_t getStride ( int level = 0 ) const

Returns the image stride on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps.

### Return value

Image stride in bytes.
## size_t getDepthStride ( int level = 0 ) const

Returns the image depth stride on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps.

### Return value

Image depth stride in bytes.
## const char * getTypeName ( int type )

Returns the name of the image type by its identifier.
### Arguments

- *int* **type** - Image type. One of the [IMAGE_*](#IMAGE_2D) types.

### Return value

Image type name: 2D for a 2D image, 3D for a 3D image, Cube for a cube image, 2D_Array for a 2D Array.
## bool isUCharFormat ( ) const

Returns a value indicating if the image is stored in an unsigned char format (R8, RG8, RGB8, RGBA8, DXT1, DXT3, DXT5, ATI1 or ATI2).
### Return value

true if the image is in unsigned char format; otherwise, false.
## bool isUCharFormat ( int format )

Returns a value indicating if a given format is an unsigned char format (R8, RG8, RGB8, RGBA8, DXT1, DXT3, DXT5, ATI1 or ATI2).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

true if the specified format is an unsigned char format; otherwise, false.
## bool isUShortFormat ( ) const

Returns a value indicating if the image is stored in an unsigned short format (R16, RG16, RGB16 or RGBA16).
### Return value

true if the image is in unsigned short format; otherwise, false.
## bool isUShortFormat ( int format )

Returns a value indicating if a given format is an unsigned short format (R16, RG16, RGB16 or RGBA16).
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

true if the specified format is an unsigned short format; otherwise, false.
## int getWidth ( int level = 0 ) const

Returns the image width on a given mipmap level.
### Arguments

- *int* **level** - Mipmap level in range from 0 to the total number of mipmaps. This is an optional argument.

### Return value

Image width if the image exists (its width is larger than 0); otherwise, 1.
## bool blend ( const Ptr < Image > & image , int x0 , int y0 , int x1 , int y1 , int width , int height , float scale = 1.0f , bool safe = 0 )


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

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Source image to be blended with the current image.
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
- *bool* **safe** - true for safe blending with respect to destination image boundaries; otherwise, false.

### Return value

Returns **1** if blending is successful; otherwise, **0**.
## bool blur ( int radius , float gamma = 1.0f , int level = 0 )

Filters the image using two-pass Gaussian blur. Only the 2D or cube image can be blurred. Compressed and combined image formats are not supported.
### Arguments

- *int* **radius** - Blur filter radius, the number of neighbouring source pixels that are averaged for each blurred destination pixel. For example, if Radius = 2, two pixels from each side are taken and the blurring kernel is **5** x **5** pixels.
- *float* **gamma** - Gamma correction value. If **1** is provided, no gamma correction is applied. This is an optional argument.
- *int* **level** - Mip level for which the blurring effect is applied. This is an optional argument.

### Return value

**true** if the image was successfully blurred or the size of blur filter is 0; otherwise, **false**.
## bool sharpen ( float radius , float intensity , float gamma = 1.0f , bool sharp_only_lightness = true , int level = 0 )

Sharpens the image. Only the 2D or cube image can be sharpened. Compressed and combined image formats are not supported.
### Arguments

- *float* **radius** - Sharpen filter radius, the number of neighbouring source pixels (or subpixels) that are averaged for each sharpened destination pixel.
- *float* **intensity** - Filter intensity value.
- *float* **gamma** - Gamma correction value. If **1** is provided, no gamma correction is applied. This is an optional argument.
- *bool* **sharp_only_lightness** - true to adjust sharpness of the lightness value only, **false** to sharpen all HSL values. This is an optional argument.
- *int* **level** - Mip level for which the sharpening effect is applied. This is an optional argument.

### Return value

**true** if the image was successfully sharpened or the size of sharpen filter is 0; otherwise, **false**.
## void clear ( )

Clears all data associated with the image and resets its type, format, size to default. Also the number of image layers and mipmaps is set to 1.
## bool combine ( int new_format = -1 )


Converts the image to a combined format. The following conversions are available:


- RGB8 to RGB565
- RGBA8 to RGBA4 if the format is specified as RGBA4; otherwise, RGBA8 is converted to RGB5A1 by default
- RGBA16 to RGB10A2


### Arguments

- *int* **new_format** - Combined format to convert the image into. This is an optional argument. If no format is specified, default conversion will be performed.

### Return value

true if the conversion into the combined format is successful; otherwise, false.
## bool combineMipmaps ( )

Combines the loaded 2D image with the mipmap image. Only one mipmap image can be combined. Compressed image formats cannot be combined.
### Return value

true if the image and a mipmap are successfully combined; otherwise, false.
## bool compare ( const Ptr < Image > & image , int x0 , int y0 , int x1 , int y1 , int width , int height , int threshold = 0 )

Compares a region of a specified image with a specified region of the current image. Compressed, combined, half-float and float formats are not supported.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Source image to compare the loaded image with.
- *int* **x0** - X coordinate on the loaded image.
- *int* **y0** - Y coordinate on the loaded image.
- *int* **x1** - X coordinate on the source image.
- *int* **y1** - Y coordinate on the source image.
- *int* **width** - Width of a region to compare.
- *int* **height** - Height of a region to compare.
- *int* **threshold** - A threshold to compare.

### Return value

true if the regions match; otherwise, false.
## bool compress ( int new_format = -1 )


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

true if the image is compressed successfully; otherwise, false.
## bool convertToFormat ( int new_format )

Converts the image to a specified format. Compressed and combined images are automatically decompressed/decombined.
### Arguments

- *int* **new_format** - Target format to convert the image into. See the **[FORMAT_*](../../...md#AUTO_FORMAT)** variables.

### Return value

true if the conversion is successful; otherwise, false.
## bool convertToType ( int type )


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

true if the conversion is successful; otherwise, false.
## void assignFrom ( const Ptr < Image > & src_image )

Copies the data from the specified source image. The size of the image shall be updated according to the size of the source image (unlike the [*resizeFrom()*](#resizeFrom_Image_int_int) method).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **src_image** - Source image.

## bool resizeFrom ( const Ptr < Image > & src_image , Image::FILTER filter = FILTER_LINEAR )

Copies the data from the specified source image, resizing the source. The source image shall be resized (enlarged/shrinked) to fit the size of the image.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **src_image** - Source image.
- *[Image::FILTER](../../../api/library/common/class.image_cpp.md#FILTER)* **filter** - Filter type to be used: linear or point. The default filter is linear. See the [Unigine::Image Enumerations with FILTER_* prefixes](#FILTER_LINEAR).

### Return value

**true** if the data was successfully copied from the source image; otherwise, **false**.
## bool copy ( const Ptr < Image > & src_image , int layer )


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
src_image->load(src_image_path);
src_image->convertToFormat(Image::FORMAT_RGB8);// 2D 1024x1024 image

dest_image->create2DArray(1024, 1024, 5, Image::FORMAT_RGB8);
dest_image->copy(src_image, 4); // created 2D image is copied to the 5th layer of the 2D image array

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **src_image** - Source image.
- *int* **layer** - Zero-based index defining layer/face TO or FROM which the data is to be copied.

### Return value

true if the data is copied successfully; otherwise, false.
## bool copy ( const Ptr < Image > & src_image , int dest_channel , int src_channel )

Copies a given channel from the specified image to the specified image channel.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **src_image** - Source image.
- *int* **dest_channel** - Destination channel.
- *int* **src_channel** - Source channel.

### Return value

**true** if the channel is copied successfully from the source image; otherwise, **false**.
## bool copy ( const Ptr < Image > & src_image , int x_dst , int y_dst , int x_src , int y_src , int width , int height , bool safe = 0 )

Copies a data fragment with specified width, height, and coordinates from the source image.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **src_image** - Source image, from which a fragment is to be copied.
- *int* **x_dst** - X coordinate of a position in the image, to which the data fragment is to be copied.
- *int* **y_dst** - Y coordinate of a position in the image, to which the data fragment is to be copied.
- *int* **x_src** - X coordinate of a position in a source image, starting from which the data fragment is to be copied.
- *int* **y_src** - Y coordinate of a position in a source image, starting from which the data fragment is to be copied.
- *int* **width** - Width of the fragment to be copied from the source image, in pixels.
- *int* **height** - Height of the fragment to be copied from the source image, in pixels.
- *bool* **safe** - true for safe copying with respect to destination image boundaries; otherwise, false. > **Notice:** The safe flag doesn't provide safe copying with respect to source image boundaries.

### Return value

**true** if the specified fragment was successfully copied from the source image; otherwise, **false**.
## bool copyFast ( const Ptr < Image > & src_image , size_t x_dst , size_t y_dst , size_t x_src , size_t y_src , size_t w , size_t h )

Copies a data fragment with specified width, height, and coordinates from the source image.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **src_image** - Source image, from which a fragment is to be copied.
- *size_t* **x_dst** - X coordinate of a position in the image, to which the data fragment is to be copied.
- *size_t* **y_dst** - Y coordinate of a position in the image, to which the data fragment is to be copied.
- *size_t* **x_src** - X coordinate of a position in a source image, starting from which the data fragment is to be copied.
- *size_t* **y_src** - Y coordinate of a position in a source image, starting from which the data fragment is to be copied.
- *size_t* **w** - Width of the fragment to be copied from the source image, in pixels.
- *size_t* **h** - Height of the fragment to be copied from the source image, in pixels.

### Return value

**true** if the specified fragment was successfully copied from the source image; otherwise, **false**.
## bool create2D ( int width , int height , int format , int num_mipmaps = 1 , bool clear = 1 , bool allocate = 1 )

Creates an empty 2D image filled with black color.
### Arguments

- *int* **width** - Required width, in pixels.
- *int* **height** - Required height, in pixels.
- *int* **format** - Required format. See the [*FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument. If the value is smaller than 1, an assertion is raised.
- *bool* **clear** - Positive number to fill the image with black color, **0** not to fill. This optional argument can be set to **0** if new data will fully overwrite the data existing in the memory.
- *bool* **allocate** - Positive number to allocate memory for the created image. This value should be always set to **1**.

### Return value

**true** if 2D image is successfully created; otherwise, **false**.
## bool create2DArray ( int width , int height , int num_layers , int format , int num_mipmaps = 1 , bool clear = 1 , bool allocate = 1 )

Creates an empty 2D texture array filled with black color.
### Arguments

- *int* **width** - Required width, in pixels.
- *int* **height** - Required height, in pixels.
- *int* **num_layers** - Number of texture layers.
- *int* **format** - Required format. See the [*FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument. If the value is smaller than 1, an assertion is raised.
- *bool* **clear** - Positive number to fill the texture array with black color, **0** not to fill. This optional argument can be set to **0** if new data will fully overwrite the data existing in the memory.
- *bool* **allocate** - Positive number to allocate memory for the created image. This value should be always set to **1**.

### Return value

**true** if 2D texture array is successfully created; otherwise, **false**.
## bool create3D ( int width , int height , int depth , int format , int num_mipmaps = 1 , bool clear = 1 , bool allocate = 1 )

Creates an empty 3D image filled with black color.
### Arguments

- *int* **width** - Required width, in pixels.
- *int* **height** - Required height, in pixels.
- *int* **depth** - Required depth.
- *int* **format** - Required format. See the [*IMAGE_FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument. If the value is smaller than 1, an assertion is raised.
- *bool* **clear** - Positive number to fill the image with black color, **0** not to fill. This optional argument can be set to **0** if new data will fully overwrite the data existing in the memory.
- *bool* **allocate** - Positive number to allocate memory for the created image. This value should be always set to **1**.

### Return value

**true** if 3D image is successfully created; otherwise, **false**.
## void create3DTurbulence ( int size , float scale , int frequency , int seed )

Creates a 3D turbulence image (RGBA8).
### Arguments

- *int* **size** - 3D image size, in pixels. Width, height, and depth are equal.
- *float* **scale** - Scaling factor applied to the displacement amount.
- *int* **frequency** - Base frequency, determines how rapidly the displacement amount changes. Increasing this value creates more turbulence.
- *int* **seed** - Specifies the initial number used for noise generation. Different Seed values produce different random variations and can be useful in changing the result. Keep in mind, that you should use the same Seed value when you want to retain the same variations.

## bool createCube ( int width , int height , int format , int num_mipmaps = 1 , bool clear = 1 , bool allocate = 1 )

Creates the empty cube image filled with black color.
### Arguments

- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.
- *int* **format** - Texture format. See the [*FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument.
- *bool* **clear** - true to fill the image with black color, false is not to fill. This optional argument can be set to false if new data will fully overwrite the data existing in the memory.
- *bool* **allocate** - true to allocate memory for the created image. This value should be always set to true.

### Return value

true if the cube image is successfully created; otherwise, false.
## bool createCubeArray ( int width , int height , int num_layers , int format , int num_mipmaps = 1 , bool clear = 1 , bool allocate = 1 )

Creates the empty cube array image filled with black color.
### Arguments

- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.
- *int* **num_layers** - Number of image layers.
- *int* **format** - Texture format. See the [*FORMAT_**](#AUTO_FORMAT) variables.
- *int* **num_mipmaps** - Number of mipmaps to create. This is an optional argument.
- *bool* **clear** - 1 to fill the image with black color, false is not to fill. This optional argument can be set to false if new data will fully overwrite the data existing in the memory.
- *bool* **allocate** - true to allocate memory for the created image. This value should be always set to true.

### Return value

true if the cube array image is successfully created; otherwise, false.
## bool createMipmaps ( Image::FILTER filter = FILTER_LINEAR , float gamma = 1.0f )

Generates mipmaps for the image. Mipmaps cannot be created for compressed and combined image formats.
### Arguments

- *[Image::FILTER](../../../api/library/common/class.image_cpp.md#FILTER)* **filter** - Filter type to be used: linear or point. The default filter is linear. See the [Unigine::Image Enumerations with FILTER_* prefixes](#FILTER_LINEAR).
- *float* **gamma** - Gamma correction value. If **1** is provided, no gamma correction is applied. This is an optional argument.

### Return value

true if the mipmaps are generated successfully; otherwise, false.
## bool createMipmapsCubeGGX ( Image::GGX_MIPMAPS_QUALITY quality )

Generates GGX mipmaps on CPU with the specified quality, of course slower and with lower quality than on GPU but it provides the result synchronously (actually this should be the only case, when this method is to be used).
### Arguments

- *[Image::GGX_MIPMAPS_QUALITY](../../../api/library/common/class.image_cpp.md#GGX_MIPMAPS_QUALITY)* **quality** - Quality of GGX mipmaps. One of the *[GGX_MIPMAPS_QUALITY](#GGX_MIPMAPS_QUALITY)* values.

### Return value

true if the mipmaps are generated successfully; otherwise, false.
## bool removeMipmaps ( )

Removes mipmaps generated for the image.
### Return value

true if mipmaps generated for the image are removed successfully; otherwise, false.
## bool decombine ( )


Automatically converts the image from the combined format to a correct one. The following conversions are available:


- RGB565 to RGB8
- RGBA4 to RGBA8
- RGB5A1 to RGBA8
- RGB10A2 to RGBA16


### Return value

true if the image is successfully converted from the combined format; otherwise, false.
## bool decombineMipmaps ( )

Decombines the loaded 2D-image and the mipmap images. The number of mipmaps must be larger than 1. Compressed image formats cannot be decombined.
### Return value

true if the 2D-image and mipmap image are successfully decombined; otherwise, false.
## bool decompress ( )


Decompresses the image from the compressed format to a correct one. The following conversions are available:


- DXT1 to RGB8
- DXT1 without alpha data to RGB8
- DXT3 to RGBA8
- DXT5 to RGBA8
- ATI1 to R8
- ATI2 to RG8


### Return value

true if the image was successfully decompressed; otherwise, false.
## bool extrude ( int pixels )

Extrudes contour of the image in the alpha=0 region on the given number of pixels. Only images of the [RGBA8](#FORMAT_RGBA8) and [RGBA16](#FORMAT_RGBA16) formats can be extruded.
### Arguments

- *int* **pixels** - Number of contour pixels.

### Return value

true if the image contour is successfully extruded; otherwise, false.
## bool flipX ( )

Flips the 2D image horizontally. Compressed and combined image formats are not supported.
### Return value

true if the image is successfully flipped; otherwise, false.
## bool flipY ( )

Flips the 2D image vertically. Compressed and combined image formats are not supported.
### Return value

true if the image is successfully flipped; otherwise, false.
## bool hasMipmaps ( ) const

Returns a value indicating if the source image has mipmaps.
### Return value

true if the image has mipmaps; otherwise, false.
## bool info ( const char * path )


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

- *const char ** **path** - Name of the image file.

### Return value

true if the information was successfully retrieved and recognized; otherwise, false.
## bool invert ( )

Inverts values of all the image channels. Only [R8](#FORMAT_R8), [RG8](#FORMAT_RG8), [RGB8](#FORMAT_RGB8), [RGBA8](#FORMAT_RGBA8), [R16](#FORMAT_R16), [RG16](#FORMAT_RG16), [RGB16](#FORMAT_RGB16), [RGBA16](#FORMAT_RGBA16), [R32F](#FORMAT_R32F), [RG32F](#FORMAT_RG32F), [RGB32F](#FORMAT_RGB32F) and [RGBA32F](#FORMAT_RGBA32F) formats can be inverted.
### Return value

**true** if the image is inverted successfully; otherwise, **false**.
## bool load ( const char * file , int mip_offset )

Loads an image from a specified file. The [following file formats](#intro) are supported.
### Arguments

- *const char ** **file** - Name of the image file.
- *int* **mip_offset** - Mipmap offset value for the loaded image.

### Return value

**true** if the image is loaded successfully; otherwise, **false**.
## bool load ( const char * file )

Loads an image from the specified file. The [following file formats](#intro) are supported.
### Arguments

- *const char ** **file** - Name of the image file.

### Return value

**true** if the image is loaded successfully; otherwise, **false**.
## bool load ( const Ptr < Stream > & stream )

Loads an image from a specified stream. The [following file formats](#intro) are supported.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

**true** if the image is loaded successfully; otherwise, **false**.
## bool load ( const unsigned char * data , int size )

Loads the image from raw data.
### Arguments

- *const unsigned char ** **data** - Set of raw data.
- *int* **size** - Raw data size, in bytes.

### Return value

**true** if the image is loaded successfully; otherwise, **false**.
## bool normalize ( )

Creates a three-component normal map out of the image.
### Return value

**true** if normalization was successful; otherwise, **false**.
## bool resize ( int new_width , int new_height , Image::FILTER filter = FILTER_LINEAR )

Resizes the image. Only the 2D or cube image can be resized. Compressed and combined image formats cannot be resized.
### Arguments

- *int* **new_width** - New image width.
- *int* **new_height** - New image height.
- *[Image::FILTER](../../../api/library/common/class.image_cpp.md#FILTER)* **filter** - Filter type to be used: linear or point. The default filter is linear. See the [Unigine::Image Enumerations with FILTER_* prefixes](#FILTER_LINEAR).

### Return value

**true** if the image is resized successfully; otherwise, **false**.
## bool rotate ( int angle )

Rotates the image by a given angle (with the step of 90 degrees). Only the 2D or cube image can be rotated. Compressed and combined image formats cannot be rotated.
### Arguments

- *int* **angle** - Angle, that will be multiplied by the step (angle * 90) to set the image rotation degree.

### Return value

**true** if the image is rotated successfully; otherwise, **false**.
## bool save ( const char * file ) const

Saves the image to a file with the specified name. The [following file formats](#intro) are supported.
### Arguments

- *const char ** **file** - Name of the file to save image data to.

### Return value

**true** if the image is saved successfully; otherwise, **false**.
## bool save ( const char * file , float quality ) const

Saves the image to a specified file. The [following file formats](#intro) are supported.
### Arguments

- *const char ** **file** - Name of a file with extension into which data will be saved.
- *float* **quality** - Quality of JPG compression in range **[0;1]**.

### Return value

**true** if the image is saved successfully; otherwise, **false**.
## bool save ( const Ptr < Stream > & stream ) const

Saves the image data (either compressed or uncompressed) to the specified stream. Current image [compression](#setFileCompression_int_void) is to be used.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Pointer to the stream.

### Return value

**true** if the image is successfully saved to the specified stream; otherwise, **false**.
## bool sign ( )

Converts the image from unsigned type to signed char. Only R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, ATI1 and ATI2 formats can be converted.
### Return value

true if the image has been converted successfully; otherwise, false.
## void swap ( const Ptr < Image > & image )

Swaps the data of the current image with the source image.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Source image.

## Image::Pixel toPixel ( const Math::vec4& color )

Converts a [vec4](../../../api/library/math/class.vec4_cpp.md) color vector (R, G, B, A) to Pixel color.
### Arguments

- *const  Math::vec4&* **color** - Color [vec4](../../../api/library/math/class.vec4_cpp.md) vector (R, G, B, A) with components normalized in range [0.0f; 1.0f]

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Image::Pixel toPixel ( int format , const Math::vec4& color )

Converts a [vec4](../../../api/library/math/class.vec4_cpp.md) color vector (R, G, B, A) to Pixel color depending on the specified image format.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.
- *const  Math::vec4&* **color** - Color [vec4](../../../api/library/math/class.vec4_cpp.md) vector (R, G, B, A) with components normalized in range [0.0f; 1.0f]

### Return value

Pixel color represented by a [Pixel structure](#pixel).
## Math:: vec4 toVec4 ( const Image::Pixel& pixel )

Converts Pixel color to a [vec4](../../../api/library/math/class.vec4_cpp.md) color vector (R, G, B, A).
### Arguments

- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **pixel** - Pixel color represented by a [Pixel structure](#pixel).

### Return value

Color [vec4](../../../api/library/math/class.vec4_cpp.md) vector (R, G, B, A). Each component is normalized in range [0.0f; 1.0f]
## Math:: vec4 toVec4 ( int format , const Image::Pixel& p )

Converts Pixel color to a [vec4](../../../api/library/math/class.vec4_cpp.md) color vector (R, G, B, A) depending on the specified image format.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.
- *const [Image::Pixel&](../../../api/library/common/class.image_cpp.md#Pixel&)* **p** - Pixel color represented by a [Pixel structure](#pixel).

### Return value

Color [vec4](../../../api/library/math/class.vec4_cpp.md) vector (R, G, B, A). Each component is normalized in range [0.0f; 1.0f]
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
## bool invertChannel ( unsigned char channel )

Inverts the values stored in the specified channel. Channels of images of half (*FORMAT_R16F* to *FORMAT_RGBA16F*) and float (*FORMAT_R32F* to *FORMAT_RGBA32F*) formats cannot be inverted.
### Arguments

- *unsigned char* **channel** - Number of the channel to be inverted, in the range from 0 to the [total number of channels](#getNumChannels_int).

### Return value

**true** if the specified channel is inverted successfully; otherwise, **false**.
## bool saveDDS ( const Ptr < Stream > & stream ) const

Saves the DDS image to a specified stream.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

**true** if the DDS image is saved successfully; otherwise, **false**.
## bool loadDDS ( const Ptr < Stream > & stream )

Loads a DDS image from a specified stream.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

**true** if the DDS image is loaded successfully; otherwise, **false**.
## int getRawFormat ( int format )

Returns the closest RAW format of the uncompressed image.
### Arguments

- *int* **format** - Image format identifier. See the [FORMAT_*](#AUTO_FORMAT) variables.

### Return value

Identifier of the uncompressed image (stored in R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F format).
## void calcRange ( Math:: dvec2 & range )

Calculates the image range for all available channels in total.
### Arguments

- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **range** - The vector to store the image range (min and max values).

## void calcRange ( Math:: dvec2 & r , Math:: dvec2 & g , Math:: dvec2 & b , Math:: dvec2 & a )

Calculates the image range for each channel separately.
### Arguments

- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **r** - The vector to store the R channel range (min and max values).
- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **g** - The vector to store the G channel range (min and max values).
- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **b** - The vector to store the B channel range (min and max values).
- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **a** - The vector to store the A channel range (min and max values).

## void changeRange ( const Math:: dvec4 & range )


Changes the image range.


> **Notice:** The range of the final image will be clamped, if the set range values exceed the maximum values of the image format.


### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **range** - Vector that stores the range values: x and y coordinates of the value specify the original range, z and w specify the new range.

## void changeRange ( const Math:: dvec4 & range_r , const Math:: dvec4 & range_g , const Math:: dvec4 & range_b , const Math:: dvec4 & range_a )


Changes the image range for each channel separately.


> **Notice:** The range of the final image will be clamped, if the set range values exceed the maximum values of the image format.


### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **range_r** - Vector that stores the range values for the R channel: x and y coordinates of the value specify the original range, z and w specify the new range.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **range_g** - Vector that stores the range values for the G channel: x and y coordinates of the value specify the original range, z and w specify the new range.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **range_b** - Vector that stores the range values for the B channel: x and y coordinates of the value specify the original range, z and w specify the new range.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **range_a** - Vector that stores the range values for the A channel: x and y coordinates of the value specify the original range, z and w specify the new range.

## void normalizeRange ( bool per_cahnnel )

Normalizes the image range either per channel or for all channels altogether.
### Arguments

- *bool* **per_cahnnel** - **true** if per-channel normalization is required; otherwise, **false**.

## bool flipCubemapX ( )

Flips the cubemap image along the X axis.
### Return value

**true** if the cubemap is flipped successfully; otherwise, **false**.
## bool flipCubemapY ( )

Flips the cubemap image along the Y axis.
### Return value

**true** if the cubemap is flipped successfully; otherwise, **false**.
## bool flipCubemapZ ( )

Flips the cubemap image along the Z axis.
### Return value

**true** if the cubemap is flipped successfully; otherwise, **false**.
## Vector < String > getSupportedLoadExtensions ( )

Returns the list of supported file extensions for loading images.
### Return value

Vector of [supported file extensions](../../../api/library/common/class.image_cpp.md#load_cstr_int_int) for loading images.
## bool isSupportedLoadExtension ( const char * extension )

Returns a value indicating if the specified file extension is supported for loading.
### Arguments

- *const char ** **extension** - File extension to check (without a leading dot).

### Return value

true if the file extension is supported for loading; otherwise, false.
## bool isSupportedLoad ( const char * path )

Returns a value indicating if the specified file path is supported for loading. This method extracts the file extension from the provided path and checks if loading an image with that extension is supported.
### Arguments

- *const char ** **path** - File path to check.

### Return value

true if the file path is supported for loading; otherwise, false.
## Vector < String > getSupportedSaveExtensions ( )

Returns the list of supported file extensions for saving images.
### Return value

Vector of [supported file extensions](../../../api/library/common/class.image_cpp.md#save_cstr_int) for saving images.
## bool isSupportedSaveExtension ( const char * extension )

Returns a value indicating if the specified file extension is supported for saving.
### Arguments

- *const char ** **extension** - File extension to check (without a leading dot).

### Return value

true if the file extension is supported for loading; otherwise, false.
## bool isSupportedSaveExtension ( const char * extension , const Image::SaveImageInfo & save_info )

Returns a value indicating if the specified file extension is supported for saving with provided image parameters. This method uses **SaveImageInfo** structure to determine the properties of the image, such as its format, dimensions, depth, layers and mipmaps.
### Arguments

- *const char ** **extension** - File extension to check (without a leading dot).
- *const [Image::SaveImageInfo](../../../api/library/common/class.image_cpp.md#SaveImageInfo) &* **save_info** - Structure to store image information.

## bool isSupportedSave ( const char * path )

Returns a value indicating if the specified file path is supported for saving. This method extracts the file extension from the provided path and checks if saving an image with that extension is supported.
### Arguments

- *const char ** **path** - File path to check.

### Return value

true if the file path is supported for saving; otherwise, false.
## int getRawFormat ( ) const

Returns the closest RAW format of the uncompressed image based on the object's current format.
### Return value

Identifier of the uncompressed image (stored in R8, RG8, RGB8, RGBA8, R16, RG16, RGB16, RGBA16, R16F, RG16F, RGB16F, RGBA16F, R32F, RG32F, RGB32F, RGBA32F format).
