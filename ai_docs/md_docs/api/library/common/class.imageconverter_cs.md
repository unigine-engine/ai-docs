# Unigine.ImageConverter Class (CS)


This class is used to define the convertation parameters required for the image at the [import](../../../editor2/assets_workflow/texture_import.md).


## ImageConverter Class

### Enums

## MIPMAPS_MODE

| Name | Description |
|---|---|
| **DISABLE** = 0 | Mipmaps are not generated. |
| **POINT** = 1 | Point filtering method is used at mipmap generation. |
| **LINEAR** = 2 | Linear filtering method is used at mipmap generation. |
| **BLUR** = 3 | Blurring is applied at mipmap generation. |
| **SHARPEN** = 4 | Sharpening is applied at mipmap generation. |
| **COMBINED** = 5 | Combination of the loaded 2D image with the most detailed mipmap image. |
| **GGX** = 6 | Generation of mipmaps for cubemap images ([IMAGE_CUBE](../../../api/library/common/class.image_cs.md#IMAGE_CUBE) or [IMAGE_CUBE_ARRAY](../../../api/library/common/class.image_cs.md#IMAGE_CUBE_ARRAY)) using GGX BRDF microfacet model. |

## RESOLUTION_MODE

| Name | Description |
|---|---|
| **AUTO** = 0 | Resolution set by the converter depending on the image format (for example, the 2D image is converted to 2D array / 3D image). |
| **ORIGINAL** = 1 | Resolution of the original image. |
| **MANUAL** = 2 | Resolution set manually in the converter. |

## COMPRESSION_QUALITY

| Name | Description |
|---|---|
| **LOW** = 0 | Low quality of compression. |
| **HIGH** = 1 | High quality of compression. |

## RESIZE_FILTER

| Name | Description |
|---|---|
| **POINT** = 0 | Point filtering method used for resizing. |
| **LINEAR** = 1 | Linear filtering method used for resizing. |
| **MIN** = 2 | Minimum filtering method used for resizing. |

## RANGE_MODE

| Name | Description |
|---|---|
| **DISABLE** = 0 | Image values are not normalized. |
| **NORMALIZE** = 1 | Values in all channels of the image are normalized altogeter to the values from 0 to 1 (i.e. overall brightness of the image). Recommended to be used for colors. |
| **NORMALIZE_PER_CHANNEL** = 2 | Normalization to the values from 0 to 1 is performed for each channel of the image separately. |
| **MANUAL** = 3 | Normalization to manually set values is performed. |

### Properties

## int Type

The numerical code of the image type.
## int Format

The numerical code of the image format.
## ImageConverter.RESOLUTION_MODE ResolutionMode

The resolution mode to be used for the image.
## ImageConverter.RESIZE_FILTER ResizeFilter

The resize filter to be used for the image.
## int Width

The image width, in pixels.
## int Height

The image height, in pixels.
## int Depth

The image depth, in pixels.
## Image.FILE_COMPRESSION FileCompression

The image file compression type.
## ImageConverter.COMPRESSION_QUALITY CompressionQuality

The image file compression quality.
## bool GPUCompression

The value specifying if GPU compression is used at converting the image.
## ImageConverter.MIPMAPS_MODE MipmapsMode

The filtering type for the image mipmaps.
## float MipmapsGamma

The gamma correction value used for the mipmaps.
## float MipmapsFilterRadius

The radius used for the mipmaps filtering.
## float MipmapsFilterIntensity

The filter intensity value used for the mipmaps.
## bool MipmapsSharpOnlyLightness

The value specifying if sharpness is applied to the HSL lightness value of the mipmap only.
## Image.GGX_MIPMAPS_QUALITY GGXMipmapsQuality

The quality for mipmaps generated for cubemap images using the GGX BRDF microfacet model. The value is applied when the [mipmap mode is set](#setMipmapsMode_int_void) to [GGX](#MIPMAPS_MODE_GGX).
## ImageConverter.RANGE_MODE RangeMode

The range mode to be applied at the image conversion.
## bool FlipX

The value specifying if the image is to be flipped horizontally.
## bool FlipY

The value specifying if the image is to be flipped vertically.
## int Blur

The amount of blur in pixels.
## int Rotate

The image rotation angle.
### Members

---

## ImageConverter ( )

Default constructor. An empty instance with default parameters is created.
## ImageConverter ( ImageConverter imageconverter )

Constructor. Creates an image converter by copying a given source image converter.
### Arguments

- *[ImageConverter](../../../api/library/common/class.imageconverter_cs.md)* **imageconverter** - Source image converter.

## void SetRange ( int channel , dvec4 value )


Sets the range to be applied at the image conversion.


> **Notice:** The range of the final image will be clamped, if the set range values exceed the maximum values of the image conversion format.


### Arguments

- *int* **channel** - Number of the channel to be inverted, in the range from 0 to the total number of channels.
- *dvec4* **value** - Range values: x and y coordinates of the value specify the original range, z and w specify the range to which the image will be converted.

## dvec4 GetRange ( int channel )

Returns the range to be applied at the image conversion.
### Arguments

- *int* **channel** - Number of the channel to be inverted, in the range from 0 to the total number of channels.

### Return value

Range values: x and y coordinates of the value specify the original range, z and w specify the range to which the image will be converted.
## bool GetInvertChannel ( int channel )

Returns the value indicating if the channel needs to be inverted.
### Arguments

- *int* **channel** - The number of the channel to be inverted, in the range from 0 to the total number of channels.

### Return value

**true** if the channel needs to be inverted; otherwise, **false**.
## void SetInvertChannel ( int channel , bool value )

Inverts the values stored in the specified channel. Channels of images of half (*FORMAT_R16F* to *FORMAT_RGBA16F*) and float (*FORMAT_R32F* to *FORMAT_RGBA32F*) formats cannot be inverted.
### Arguments

- *int* **channel** - The number of the channel to be inverted, in the range from 0 to the total number of channels.
- *bool* **value** - **true** if the channel needs to be inverted; otherwise, **false**.

## void Reset ( )

Sets the converter to the default values.
## void Copy ( ImageConverter converter )

Copies data from the specified source converter.
### Arguments

- *[ImageConverter](../../../api/library/common/class.imageconverter_cs.md)* **converter** - The source converter.

## ImageConverter Clone ( )

Creates a clone of the specified source converter.
### Return value

The converter to be cloned.
## bool Load ( string path )

Loads the image converter settings on the disk using the specified path.
### Arguments

- *string* **path** - The path to the file with the image converter settings.

### Return value

**true** if the image converter settings are loaded successfully; otherwise, **false**.
## void Load ( Json json )

Loads the `.json` object with the image converter settings.
### Arguments

- *[Json](../../../api/library/common/class.json_cs.md)* **json** - The object with the image converter settings.

## bool Save ( string path )

Saves image converter settings on the disk to the specified location.
### Arguments

- *string* **path** - The path to the file to store the image converter settings.

### Return value

**true** if the image converter settings are saved successfully; otherwise, **false**.
## void Save ( Json json )

Saves image converter settings to the specified `.json` object.
### Arguments

- *[Json](../../../api/library/common/class.json_cs.md)* **json** - The object with the image converter settings.

## void UpdateParameters ( Image image )

Validates the parameters of the image converter for the specified image. This method allows checking the resulting parameters before converting the image.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - The image to be converted.

## bool RunCPU ( Image image )

Runs the image converter on CPU.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - The image to be converted.

### Return value

true if the image has been converted successfully; otherwise, false.
## bool Run ( Converted on_converted , Image image )

Runs the image converter.
### Arguments

- *Converted* **on_converted** - Callback to be fired after image conversion.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to be converted.

### Return value

true if the image has been converted successfully; otherwise, false.
## bool AdaptForSaving ( Image image , string extension )

Attempts to adapt the converter for saving the given image using one of the [supported file extensions](../../../api/library/common/class.image_cs.md#intro).
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to be saved.
- *string* **extension** - Target file extension.

### Return value

true if the image is valid and suitable format and type could be determined and set for saving; otherwise false.
