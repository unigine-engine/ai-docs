# Unigine.ImageConverter Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to define the convertation parameters required for the image at the [import](../../../editor2/assets_workflow/texture_import.md).


## ImageConverter Class

### Members

## void setType ( int type )

Sets a new numerical code of the image type.
### Arguments

- *int* **type** - The numerical code of the image type: 0 for a 2D image, 1 for a 3D image, 2 for a cube image, 3 for a 2D Array. See the [Unigine::Image:: Enumeration with IMAGE_* prefixes](../../../api/library/common/class.image_usc.md#IMAGE_2D).

## int getType () const

Returns the current numerical code of the image type.
### Return value

Current numerical code of the image type: 0 for a 2D image, 1 for a 3D image, 2 for a cube image, 3 for a 2D Array. See the [Unigine::Image:: Enumeration with IMAGE_* prefixes](../../../api/library/common/class.image_usc.md#IMAGE_2D).
## void setFormat ( int format )

Sets a new numerical code of the image format.
### Arguments

- *int* **format** - The numerical code of the image format. See the [FORMAT_*](../../../api/library/common/class.image_usc.md#FORMAT_ATI1) variables.

## int getFormat () const

Returns the current numerical code of the image format.
### Return value

Current numerical code of the image format. See the [FORMAT_*](../../../api/library/common/class.image_usc.md#FORMAT_ATI1) variables.
## void setResolutionMode ( )

Sets a new resolution mode to be used for the image.
### Arguments

- **mode** - The resolution mode to be used for the image. One of the *[RESOLUTION_MODE](#RESOLUTION_MODE_AUTO)* values.

## getResolutionMode () const

Returns the current resolution mode to be used for the image.
### Return value

Current The resolution mode to be used for the image. One of the *[RESOLUTION_MODE](#RESOLUTION_MODE_AUTO)* values.
## void setResizeFilter ( )

Sets a new resize filter to be used for the image.
### Arguments

- **filter** - The resize filter to be used for the image. One of the *[RESIZE_FILTER](#RESIZE_FILTER_POINT)* values.

## getResizeFilter () const

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
## void setFileCompression ( )

Sets a new image file compression type.
### Arguments

- **compression** - The file compression type to be used for the image. One of the *[FILE_COMPRESSION_*](../../../api/library/common/class.image_usc.md#FILE_COMPRESSION_LZ4_HIGH)* values.

## getFileCompression () const

Returns the current image file compression type.
### Return value

Current file compression type to be used for the image. One of the *[FILE_COMPRESSION_*](../../../api/library/common/class.image_usc.md#FILE_COMPRESSION_LZ4_HIGH)* values.
## void setCompressionQuality ( )

Sets a new image file compression quality.
### Arguments

- **quality** - The compression quality to be used for the image. One of the *[COMPRESSION_QUALITY_*](#COMPRESSION_QUALITY_LOW)* values.

## getCompressionQuality () const

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
## void setMipmapsMode ( )

Sets a new filtering type for the image mipmaps.
### Arguments

- **mode** - The mipmaps mode to be used. One of the *[MIPMAPS_MODE_*](#MIPMAPS_MODE_DISABLE)* values.

## getMipmapsMode () const

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
## void setGGXMipmapsQuality ( )

Sets a new quality for mipmaps generated for cubemap images using the GGX BRDF microfacet model. The value is applied when the [mipmap mode is set](#setMipmapsMode_int_void) to [GGX](#MIPMAPS_MODE_GGX).
### Arguments

- **quality** - The quality of the GGX mipmaps for the cubemap image. One of the **[IMAGE_GGX_MIPMAPS_QUALITY()](../../../api/library/common/class.image_usc.md#GGX_MIPMAPS_QUALITY)** values.

## getGGXMipmapsQuality () const

Returns the current quality for mipmaps generated for cubemap images using the GGX BRDF microfacet model. The value is applied when the [mipmap mode is set](#setMipmapsMode_int_void) to [GGX](#MIPMAPS_MODE_GGX).
### Return value

Current quality of the GGX mipmaps for the cubemap image. One of the **[IMAGE_GGX_MIPMAPS_QUALITY()](../../../api/library/common/class.image_usc.md#GGX_MIPMAPS_QUALITY)** values.
## void setRangeMode ( )

Sets a new range mode to be applied at the image conversion.
### Arguments

- **mode** - The range mode to be applied at the image conversion. One of the *[RANGE_MODE_*](#RANGE_MODE_DISABLE)* values.

## getRangeMode () const

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
## void setRange ( int channel , dvec4 value )


Sets the range to be applied at the image conversion.


> **Notice:** The range of the final image will be clamped, if the set range values exceed the maximum values of the image conversion format.


### Arguments

- *int* **channel** - Number of the channel to be inverted, in the range from 0 to the total number of channels.
- *dvec4* **value** - Range values: x and y coordinates of the value specify the original range, z and w specify the range to which the image will be converted.

## dvec4 getRange ( int channel )

Returns the range to be applied at the image conversion.
### Arguments

- *int* **channel** - Number of the channel to be inverted, in the range from 0 to the total number of channels.

### Return value

Range values: x and y coordinates of the value specify the original range, z and w specify the range to which the image will be converted.
## int getInvertChannel ( int channel )

Returns the value indicating if the channel needs to be inverted.
### Arguments

- *int* **channel** - The number of the channel to be inverted, in the range from 0 to the total number of channels.

### Return value

**1** if the channel needs to be inverted; otherwise, **0**.
## void setInvertChannel ( int channel , int value )

Inverts the values stored in the specified channel. Channels of images of half (*FORMAT_R16F* to *FORMAT_RGBA16F*) and float (*FORMAT_R32F* to *FORMAT_RGBA32F*) formats cannot be inverted.
### Arguments

- *int* **channel** - The number of the channel to be inverted, in the range from 0 to the total number of channels.
- *int* **value** - **1** if the channel needs to be inverted; otherwise, **0**.

## void reset ( )

Sets the converter to the default values.
## void copy ( ImageConverter & converter )

Copies data from the specified source converter.
### Arguments

- *[ImageConverter](../../../api/library/common/class.imageconverter_usc.md) &* **converter** - The source converter.

## ImageConverter clone ( )

Creates a clone of the specified source converter.
### Return value

The converter to be cloned.
## int load ( string path )

Loads the image converter settings on the disk using the specified path.
### Arguments

- *string* **path** - The path to the file with the image converter settings.

### Return value

**1** if the image converter settings are loaded successfully; otherwise, **0**.
## int save ( string path )

Saves image converter settings on the disk to the specified location.
### Arguments

- *string* **path** - The path to the file to store the image converter settings.

### Return value

**1** if the image converter settings are saved successfully; otherwise, **0**.
## void updateParameters ( Image image )

Validates the parameters of the image converter for the specified image. This method allows checking the resulting parameters before converting the image.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - The image to be converted.

## int runCPU ( Image & image )

Runs the image converter on CPU.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md) &* **image** - The image to be converted.

### Return value

**1** if the image has been converted successfully; otherwise, **0**.
## int adaptForSaving ( Image image , string extension )

Attempts to adapt the converter for saving the given image using one of the [supported file extensions](../../../api/library/common/class.image_usc.md#intro).
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to be saved.
- *string* **extension** - Target file extension.

### Return value

true if the image is valid and suitable format and type could be determined and set for saving; otherwise false.
