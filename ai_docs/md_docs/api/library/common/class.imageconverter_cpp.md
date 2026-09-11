# Unigine.ImageConverter Class (CPP)

**Header:** #include <UnigineImage.h>


This class is used to define the convertation parameters required for the image at the [import](../../../editor2/assets_workflow/texture_import.md).


## ImageConverter Class

### Enums

## MIPMAPS_MODE

| Name | Description |
|---|---|
| **MIPMAPS_MODE_DISABLE** = 0 | Mipmaps are not generated. |
| **MIPMAPS_MODE_POINT** = 1 | Point filtering method is used at mipmap generation. |
| **MIPMAPS_MODE_LINEAR** = 2 | Linear filtering method is used at mipmap generation. |
| **MIPMAPS_MODE_BLUR** = 3 | Blurring is applied at mipmap generation. |
| **MIPMAPS_MODE_SHARPEN** = 4 | Sharpening is applied at mipmap generation. |
| **MIPMAPS_MODE_COMBINED** = 5 | Combination of the loaded 2D image with the most detailed mipmap image. |
| **MIPMAPS_MODE_GGX** = 6 | Generation of mipmaps for cubemap images ([IMAGE_CUBE](../../../api/library/common/class.image_cpp.md#IMAGE_CUBE) or [IMAGE_CUBE_ARRAY](../../../api/library/common/class.image_cpp.md#IMAGE_CUBE_ARRAY)) using GGX BRDF microfacet model. |

## RESOLUTION_MODE

| Name | Description |
|---|---|
| **RESOLUTION_MODE_AUTO** = 0 | Resolution set by the converter depending on the image format (for example, the 2D image is converted to 2D array / 3D image). |
| **RESOLUTION_MODE_ORIGINAL** = 1 | Resolution of the original image. |
| **RESOLUTION_MODE_MANUAL** = 2 | Resolution set manually in the converter. |

## COMPRESSION_QUALITY

| Name | Description |
|---|---|
| **COMPRESSION_QUALITY_LOW** = 0 | Low quality of compression. |
| **COMPRESSION_QUALITY_HIGH** = 1 | High quality of compression. |

## RESIZE_FILTER

| Name | Description |
|---|---|
| **RESIZE_FILTER_POINT** = 0 | Point filtering method used for resizing. |
| **RESIZE_FILTER_LINEAR** = 1 | Linear filtering method used for resizing. |
| **RESIZE_FILTER_MIN** = 2 | Minimum filtering method used for resizing. |

## RANGE_MODE

| Name | Description |
|---|---|
| **RANGE_MODE_DISABLE** = 0 | Image values are not normalized. |
| **RANGE_MODE_NORMALIZE** = 1 | Values in all channels of the image are normalized altogeter to the values from 0 to 1 (i.e. overall brightness of the image). Recommended to be used for colors. |
| **RANGE_MODE_NORMALIZE_PER_CHANNEL** = 2 | Normalization to the values from 0 to 1 is performed for each channel of the image separately. |
| **RANGE_MODE_MANUAL** = 3 | Normalization to manually set values is performed. |

### Members

## void setType ( int type )

Sets a new numerical code of the image type.
### Arguments

- *int* **type** - The numerical code of the image type: 0 for a 2D image, 1 for a 3D image, 2 for a cube image, 3 for a 2D Array. See the [Unigine::Image:: Enumeration with IMAGE_* prefixes](../../../api/library/common/class.image_cpp.md#IMAGE_2D).

## int getType () const

Returns the current numerical code of the image type.
### Return value

Current numerical code of the image type: 0 for a 2D image, 1 for a 3D image, 2 for a cube image, 3 for a 2D Array. See the [Unigine::Image:: Enumeration with IMAGE_* prefixes](../../../api/library/common/class.image_cpp.md#IMAGE_2D).
## void setFormat ( int format )

Sets a new numerical code of the image format.
### Arguments

- *int* **format** - The numerical code of the image format. See the [FORMAT_*](../../../api/library/common/class.image_cpp.md#FORMAT_ATI1) variables.

## int getFormat () const

Returns the current numerical code of the image format.
### Return value

Current numerical code of the image format. See the [FORMAT_*](../../../api/library/common/class.image_cpp.md#FORMAT_ATI1) variables.
## void setResolutionMode ( ImageConverter::RESOLUTION_MODE mode )

Sets a new resolution mode to be used for the image.
### Arguments

- *[ImageConverter::RESOLUTION_MODE](../../../api/library/common/class.imageconverter_cpp.md#RESOLUTION_MODE)* **mode** - The resolution mode to be used for the image. One of the *[RESOLUTION_MODE](#RESOLUTION_MODE_AUTO)* values.

## ImageConverter::RESOLUTION_MODE getResolutionMode () const

Returns the current resolution mode to be used for the image.
### Return value

Current The resolution mode to be used for the image. One of the *[RESOLUTION_MODE](#RESOLUTION_MODE_AUTO)* values.
## void setResizeFilter ( ImageConverter::RESIZE_FILTER filter )

Sets a new resize filter to be used for the image.
### Arguments

- *[ImageConverter::RESIZE_FILTER](../../../api/library/common/class.imageconverter_cpp.md#RESIZE_FILTER)* **filter** - The resize filter to be used for the image. One of the *[RESIZE_FILTER](#RESIZE_FILTER_POINT)* values.

## ImageConverter::RESIZE_FILTER getResizeFilter () const

Returns the current resize filter to be used for the image.
### Return value

Current The resize filter to be used for the image. One of the *[RESIZE_FILTER](#RESIZE_FILTER_POINT)* values.
## void setWidth ( int width )

Sets a new image width, in pixels.
### Arguments

- *int* **width** - The image width, in pixels.

## int getWidth () const

Returns the current image width, in pixels.
### Return value

Current image width, in pixels.
## void setHeight ( int height )

Sets a new image height, in pixels.
### Arguments

- *int* **height** - The image height, in pixels.

## int getHeight () const

Returns the current image height, in pixels.
### Return value

Current image height, in pixels.
## void setDepth ( int depth )

Sets a new image depth, in pixels.
### Arguments

- *int* **depth** - The image depth, in pixels.

## int getDepth () const

Returns the current image depth, in pixels.
### Return value

Current image depth, in pixels.
## void setFileCompression ( Image::FILE_COMPRESSION compression )

Sets a new image file compression type.
### Arguments

- *[Image::FILE_COMPRESSION](../../../api/library/common/class.image_cpp.md#FILE_COMPRESSION)* **compression** - The file compression type to be used for the image. One of the *[FILE_COMPRESSION_*](../../../api/library/common/class.image_cpp.md#FILE_COMPRESSION_LZ4_HIGH)* values.

## Image::FILE_COMPRESSION getFileCompression () const

Returns the current image file compression type.
### Return value

Current file compression type to be used for the image. One of the *[FILE_COMPRESSION_*](../../../api/library/common/class.image_cpp.md#FILE_COMPRESSION_LZ4_HIGH)* values.
## void setCompressionQuality ( ImageConverter::COMPRESSION_QUALITY quality )

Sets a new image file compression quality.
### Arguments

- *[ImageConverter::COMPRESSION_QUALITY](../../../api/library/common/class.imageconverter_cpp.md#COMPRESSION_QUALITY)* **quality** - The compression quality to be used for the image. One of the *[COMPRESSION_QUALITY_*](#COMPRESSION_QUALITY_LOW)* values.

## ImageConverter::COMPRESSION_QUALITY getCompressionQuality () const

Returns the current image file compression quality.
### Return value

Current compression quality to be used for the image. One of the *[COMPRESSION_QUALITY_*](#COMPRESSION_QUALITY_LOW)* values.
## void setGPUCompression ( bool gpucompression )

Sets a new value specifying if GPU compression is used at converting the image.
### Arguments

- *bool* **gpucompression** - Set **true** to enable image compression on GPU; **false** - to disable it.

## bool isGPUCompression () const

Returns the current value specifying if GPU compression is used at converting the image.
### Return value

**true** if image compression on GPU is enabled ; otherwise **false**.
## void setMipmapsMode ( ImageConverter::MIPMAPS_MODE mode )

Sets a new filtering type for the image mipmaps.
### Arguments

- *[ImageConverter::MIPMAPS_MODE](../../../api/library/common/class.imageconverter_cpp.md#MIPMAPS_MODE)* **mode** - The mipmaps mode to be used. One of the *[MIPMAPS_MODE_*](#MIPMAPS_MODE_DISABLE)* values.

## ImageConverter::MIPMAPS_MODE getMipmapsMode () const

Returns the current filtering type for the image mipmaps.
### Return value

Current mipmaps mode to be used. One of the *[MIPMAPS_MODE_*](#MIPMAPS_MODE_DISABLE)* values.
## void setMipmapsGamma ( float gamma )

Sets a new gamma correction value used for the mipmaps.
### Arguments

- *float* **gamma** - The gamma correction value used for the mipmaps.

## float getMipmapsGamma () const

Returns the current gamma correction value used for the mipmaps.
### Return value

Current gamma correction value used for the mipmaps.
## void setMipmapsFilterRadius ( float radius )

Sets a new radius used for the mipmaps filtering.
### Arguments

- *float* **radius** - The filter radius value.

## float getMipmapsFilterRadius () const

Returns the current radius used for the mipmaps filtering.
### Return value

Current filter radius value.
## void setMipmapsFilterIntensity ( float intensity )

Sets a new filter intensity value used for the mipmaps.
### Arguments

- *float* **intensity** - The filter intensity value used for the mipmaps.

## float getMipmapsFilterIntensity () const

Returns the current filter intensity value used for the mipmaps.
### Return value

Current filter intensity value used for the mipmaps.
## void setMipmapsSharpOnlyLightness ( bool lightness )

Sets a new value specifying if sharpness is applied to the HSL lightness value of the mipmap only.
### Arguments

- *bool* **lightness** - true to adjust sharpness of the lightness value only, **false** to sharpen all HSL values.

## bool isMipmapsSharpOnlyLightness () const

Returns the current value specifying if sharpness is applied to the HSL lightness value of the mipmap only.
### Return value

true to adjust sharpness of the lightness value only, **false** to sharpen all HSL values.
## void setGGXMipmapsQuality ( Image::GGX_MIPMAPS_QUALITY quality )

Sets a new quality for mipmaps generated for cubemap images using the GGX BRDF microfacet model. The value is applied when the [mipmap mode is set](#setMipmapsMode_int_void) to [GGX](#MIPMAPS_MODE_GGX).
### Arguments

- *[Image::GGX_MIPMAPS_QUALITY](../../../api/library/common/class.image_cpp.md#GGX_MIPMAPS_QUALITY)* **quality** - The quality of the GGX mipmaps for the cubemap image. One of the **[Image::GGX_MIPMAPS_QUALITY](../../../api/library/common/class.image_cpp.md#GGX_MIPMAPS_QUALITY)** values.

## Image::GGX_MIPMAPS_QUALITY getGGXMipmapsQuality () const

Returns the current quality for mipmaps generated for cubemap images using the GGX BRDF microfacet model. The value is applied when the [mipmap mode is set](#setMipmapsMode_int_void) to [GGX](#MIPMAPS_MODE_GGX).
### Return value

Current quality of the GGX mipmaps for the cubemap image. One of the **[Image::GGX_MIPMAPS_QUALITY](../../../api/library/common/class.image_cpp.md#GGX_MIPMAPS_QUALITY)** values.
## void setRangeMode ( ImageConverter::RANGE_MODE mode )

Sets a new range mode to be applied at the image conversion.
### Arguments

- *[ImageConverter::RANGE_MODE](../../../api/library/common/class.imageconverter_cpp.md#RANGE_MODE)* **mode** - The range mode to be applied at the image conversion. One of the *[RANGE_MODE_*](#RANGE_MODE_DISABLE)* values.

## ImageConverter::RANGE_MODE getRangeMode () const

Returns the current range mode to be applied at the image conversion.
### Return value

Current range mode to be applied at the image conversion. One of the *[RANGE_MODE_*](#RANGE_MODE_DISABLE)* values.
## void setFlipX ( bool x )

Sets a new value specifying if the image is to be flipped horizontally.
### Arguments

- *bool* **x** - Set **true** to enable horizontal flipping of the image; **false** - to disable it.

## bool isFlipX () const

Returns the current value specifying if the image is to be flipped horizontally.
### Return value

**true** if horizontal flipping of the image is enabled ; otherwise **false**.
## void setFlipY ( bool y )

Sets a new value specifying if the image is to be flipped vertically.
### Arguments

- *bool* **y** - Set **true** to enable vertical flipping of the image; **false** - to disable it.

## bool isFlipY () const

Returns the current value specifying if the image is to be flipped vertically.
### Return value

**true** if vertical flipping of the image is enabled ; otherwise **false**.
## void setBlur ( int blur )

Sets a new amount of blur in pixels.
### Arguments

- *int* **blur** - The amount of blur in pixels.

## int getBlur () const

Returns the current amount of blur in pixels.
### Return value

Current amount of blur in pixels.
## void setRotate ( int rotate )

Sets a new image rotation angle.
### Arguments

- *int* **rotate** - The rotation angle, clock-wise.

## int getRotate () const

Returns the current image rotation angle.
### Return value

Current rotation angle, clock-wise.
---

## ImageConverter ( )

Default constructor. An empty instance with default parameters is created.
## ImageConverter ( const Ptr < ImageConverter > & imageconverter )

Constructor. Creates an image converter by copying a given source image converter.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ImageConverter](../../../api/library/common/class.imageconverter_cpp.md)> &* **imageconverter** - Source image converter.

## void setRange ( int channel , const Math:: dvec4 & value )


Sets the range to be applied at the image conversion.


> **Notice:** The range of the final image will be clamped, if the set range values exceed the maximum values of the image conversion format.


### Arguments

- *int* **channel** - Number of the channel to be inverted, in the range from 0 to the total number of channels.
- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Range values: x and y coordinates of the value specify the original range, z and w specify the range to which the image will be converted.

## Math:: dvec4 getRange ( int channel ) const

Returns the range to be applied at the image conversion.
### Arguments

- *int* **channel** - Number of the channel to be inverted, in the range from 0 to the total number of channels.

### Return value

Range values: x and y coordinates of the value specify the original range, z and w specify the range to which the image will be converted.
## bool getInvertChannel ( int channel )

Returns the value indicating if the channel needs to be inverted.
### Arguments

- *int* **channel** - The number of the channel to be inverted, in the range from 0 to the total number of channels.

### Return value

**true** if the channel needs to be inverted; otherwise, **false**.
## void setInvertChannel ( int channel , bool value )

Inverts the values stored in the specified channel. Channels of images of half (*FORMAT_R16F* to *FORMAT_RGBA16F*) and float (*FORMAT_R32F* to *FORMAT_RGBA32F*) formats cannot be inverted.
### Arguments

- *int* **channel** - The number of the channel to be inverted, in the range from 0 to the total number of channels.
- *bool* **value** - **true** if the channel needs to be inverted; otherwise, **false**.

## void reset ( )

Sets the converter to the default values.
## void copy ( Ptr < ImageConverter > & converter ) const

Copies data from the specified source converter.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ImageConverter](../../../api/library/common/class.imageconverter_cpp.md)> &* **converter** - The source converter.

## Ptr < ImageConverter > clone ( ) const

Creates a clone of the specified source converter.
### Return value

The converter to be cloned.
## bool load ( const char * path )

Loads the image converter settings on the disk using the specified path.
### Arguments

- *const char ** **path** - The path to the file with the image converter settings.

### Return value

**true** if the image converter settings are loaded successfully; otherwise, **false**.
## void load ( const Ptr < Json > & json )

Loads the `.json` object with the image converter settings.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Json](../../../api/library/common/class.json_cpp.md)> &* **json** - The object with the image converter settings.

## bool save ( const char * path ) const

Saves image converter settings on the disk to the specified location.
### Arguments

- *const char ** **path** - The path to the file to store the image converter settings.

### Return value

**true** if the image converter settings are saved successfully; otherwise, **false**.
## void save ( const Ptr < Json > & json ) const

Saves image converter settings to the specified `.json` object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Json](../../../api/library/common/class.json_cpp.md)> &* **json** - The object with the image converter settings.

## void updateParameters ( const Ptr < Image > & image )

Validates the parameters of the image converter for the specified image. This method allows checking the resulting parameters before converting the image.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - The image to be converted.

## bool runCPU ( Ptr < Image > & image )

Runs the image converter on CPU.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - The image to be converted.

### Return value

true if the image has been converted successfully; otherwise, false.
## bool run ( CallbackBase1 < Ptr < Image >> * on_converted , const Ptr < Image > & image )

Runs the image converter.
### Arguments

- *[CallbackBase1](../../../api/library/common/callbacks/class.callbackbase1_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)>> ** **on_converted** - Callback to be fired after image conversion.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to be converted.

### Return value

true if the image has been converted successfully; otherwise, false.
## bool adaptForSaving ( const Ptr < Image > & image , const char * extension )

Attempts to adapt the converter for saving the given image using one of the [supported file extensions](../../../api/library/common/class.image_cpp.md#intro).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to be saved.
- *const char ** **extension** - Target file extension.

### Return value

true if the image is valid and suitable format and type could be determined and set for saving; otherwise false.
