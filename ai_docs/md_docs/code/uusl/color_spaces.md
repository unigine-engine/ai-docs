# Color Model Functions


This documentation article contains information functions of the UUSL. This information can be used as the reference document for writing shaders.


To start using common UUSL functionality, include the `core/materials/shaders/api/color_spaces.h` file.


```glsl
#include <core/materials/shaders/api/color_spaces.h>
```


## Color Model Functions


## float3 hueToRgb ( float hue )

Converts Hue color value to RGB (Red, Green, Blue) color values.
### Arguments

- *float* **hue** - Hue color value.

### Return value

RGB (Red, Green, Blue) color values.
## float3 rgbToHcv ( float3 rgb )

Converts RGB (Red, Green, Blue) color values to HCV (Hue, Chroma, Value) color values.
### Arguments

- *float3* **rgb** - RGB (Red, Green, Blue) color values.

### Return value

HCV (Hue, Chroma, Value) color values.
## float3 rgbToHsv ( float3 rgb )

Converts RGB (Red, Green, Blue) color values to HSV (Hue, Saturation, Value) color values.
### Arguments

- *float3* **rgb** - RGB (Red, Green, Blue) color values.

### Return value

HSV (Hue, Saturation, Value).
## float3 hsvToRgb ( float3 hsv )

Converts HSV (Hue, Saturation, Value) color values to RGB (Red, Green, Blue) color values.
### Arguments

- *float3* **hsv** - HSV (Hue, Saturation, Value).

### Return value

RGB (Red, Green, Blue) color values.
## float3 rgbToHcy ( float3 rgb )

Converts RGB (Red, Green, Blue) color values to HCY (Hue, Chroma, Luma) color values.
### Arguments

- *float3* **rgb** - RGB (Red, Green, Blue) color values.

### Return value

HCY (Hue, Chroma, Luma) color values.
## float3 hcyToRgb ( float3 hcy )

Converts HCY (Hue, Chroma, Luma) to RGB (Red, Green, Blue) color values.
### Arguments

- *float3* **hcy** - HCY (Hue, Chroma, Luma) color values.

### Return value

RGB (Red, Green, Blue) color values.
## float3 rgbToHcl ( float3 rgb )

Converts RGB (Red, Green, Blue) color values to HCL (Hue, Chroma, Luminance) color values.
### Arguments

- *float3* **rgb** - RGB (Red, Green, Blue) color values.

### Return value

HCL (Hue, Chroma, Luminance) color values.
## float3 hclToRgb ( float3 hcl )

Converts HCL (Hue, Chroma, Luminance) to RGB (Red, Green, Blue) color values.
### Arguments

- *float3* **hcl** - HCL (Hue, Chroma, Luminance) color values.

### Return value

RGB (Red, Green, Blue) color values.
## float3 rgbToHsl ( float3 rgb )

Converts RGB (Red, Green, Blue) color values to HSL (Hue, Saturation, Lightness) color values.
### Arguments

- *float3* **rgb** - RGB (Red, Green, Blue) color values.

### Return value

HSL (Hue, Saturation, Lightness) color values.
## float3 hslToRgb ( float3 hsl )

Converts HSL (Hue, Saturation, Lightness) to RGB (Red, Green, Blue) color values.
### Arguments

- *float3* **hsl** - HSL (Hue, Saturation, Lightness) color values.

### Return value

RGB (Red, Green, Blue) color values.
## float3 rgbToYuv ( float3 rgb )

Converts RGB (Red, Green, Blue) color values to YUV (Luminance, Delta Blue, Delta Red) color values.
### Arguments

- *float3* **rgb** - RGB (Red, Green, Blue) color values.

### Return value

YUV (Luminance, Delta Blue, Delta Red) color values.
## float3 yuvToRgb ( float3 yuv )

Converts YUV (Luminance, Delta Blue, Delta Red) to RGB (Red, Green, Blue) color values.
### Arguments

- *float3* **yuv** - YUV (Luminance, Delta Blue, Delta Red) color values.

### Return value

RGB (Red, Green, Blue) color values.
## float3 rgbToYcbcr ( float3 rgb )

Converts RGB (Red, Green, Blue) color values to YCbCr (Luma, Chrominance Blue, Chrominance Red) color values.
### Arguments

- *float3* **rgb** - RGB (Red, Green, Blue) color values.

### Return value

YCbCr (Luma, Chrominance Blue, Chrominance Red) color values.
## float3 ycbcrToRgb ( float3 ycc )

Converts YCbCr (Luma, Chrominance Blue, Chrominance Red) to RGB (Red, Green, Blue) color values.
### Arguments

- *float3* **ycc** - YCbCr (Luma, Chrominance Blue, Chrominance Red) color values.

### Return value

RGB (Red, Green, Blue) color values.
## float3 rgbToYcgco ( float3 rgb )

Converts RGB (Red, Green, Blue) color values to YCgCo (Luma, Chrominance Green, Chrominance Orange) color values.
### Arguments

- *float3* **rgb** - RGB (Red, Green, Blue) color values.

### Return value

YCgCo (Luma, Chrominance Green, Chrominance Orange) color values.
## float3 ycgcoToRgb ( float3 ycc )

Converts YCgCo (Luma, Chrominance Green, Chrominance Orange) color values to RGB (Red, Green, Blue) color values.
### Arguments

- *float3* **ycc** - YCgCo (Luma, Chrominance Green, Chrominance Orange) color values.

### Return value

RGB (Red, Green, Blue) color values.
