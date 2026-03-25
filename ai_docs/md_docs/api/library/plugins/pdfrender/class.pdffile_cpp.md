# Unigine::Plugins::PDFRender::PDFFile Class (CPP)

**Header:** #include <plugins/Unigine/PDFRender/UniginePDFRender.h>


## PDFFile Class

### Enums

## RENDER_FLAG

| Name | Description |
|---|---|
| **RENDER_FLAG_ANNOT** = 0x01 | Enable rendering of annotations. |
| **RENDER_FLAG_LCD_TEXT** = 0x02 | Enable text rendering optimized for LCD displays. > **Notice:** This flag takes effect only if text antialiasing is enabled. |
| **RENDER_FLAG_NO_NATIVETEXT** = 0x04 | Disable native text output on platforms where it is available. |
| **RENDER_FLAG_GRAYSCALE** = 0x08 | Render the output in grayscale. |
| **RENDER_FLAG_NO_SMOOTHTEXT** = 0x1000 | Disable antialiasing for text. > **Notice:** This flag also disables LCD text optimization. |
| **RENDER_FLAG_NO_SMOOTHIMAGE** = 0x2000 | Disable antialiasing for images. |
| **RENDER_FLAG_NO_SMOOTHPATH** = 0x4000 | Disable antialiasing for paths. |

### Members

## bool isValid () const

Returns the current value indicating if the PDF file is loaded.
### Return value

**true** if the PDF file is loaded; otherwise **false**.
## int getPageCount () const

Returns the current PDF document total page number.
### Return value

Current PDF document total page number.
---

## float getPageHeight ( int pageIndex ) const

Returns the height of the specified PDF page, in units. One unit is 1/72 inch (around 0.3528 mm).
### Arguments

- *int* **pageIndex** - target page index.

### Return value

Page height, in units. One unit is 1/72 inch (around 0.3528 mm).
## float getPageWidth ( int pageIndex ) const

Returns the width of the specified PDF page, in units. One unit is 1/72 inch (around 0.3528 mm).
### Arguments

- *int* **pageIndex** - target page index.

### Return value

Page width, in units. One unit is 1/72 inch (around 0.3528 mm).
## Ptr < Image > renderPage ( int pageIndex , int width , int height , int render_flags = 0 ) const

Renders the specified PDF page into a new *[Image](../../../../api/library/common/class.image_cpp.md)* object with the given width, height and [render flags](#RENDER_FLAG).
### Arguments

- *int* **pageIndex** - target page index.
- *int* **width** - target image width, in units. One unit is 1/72 inch (around 0.3528 mm).
- *int* **height** - target image height, in units. One unit is 1/72 inch (around 0.3528 mm).
- *int* **render_flags** - a [render flag](#RENDER_FLAG).

### Return value

Image containing the rendered PDF page data.
