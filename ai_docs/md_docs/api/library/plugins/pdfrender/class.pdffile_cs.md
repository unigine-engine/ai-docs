# Unigine::Plugins::PDFRender::PDFFile Class (CS)


## PDFFile Class

### Enums

## RENDER_FLAG

| Name | Description |
|---|---|
| **ANNOT** = 0x01 | Enable rendering of annotations. |
| **LCD_TEXT** = 0x02 | Enable text rendering optimized for LCD displays. > **Notice:** This flag takes effect only if text antialiasing is enabled. |
| **NO_NATIVETEXT** = 0x04 | Disable native text output on platforms where it is available. |
| **GRAYSCALE** = 0x08 | Render the output in grayscale. |
| **NO_SMOOTHTEXT** = 0x1000 | Disable antialiasing for text. > **Notice:** This flag also disables LCD text optimization. |
| **NO_SMOOTHIMAGE** = 0x2000 | Disable antialiasing for images. |
| **NO_SMOOTHPATH** = 0x4000 | Disable antialiasing for paths. |

### Properties

## 🔒︎ bool IsValid

The value indicating if the PDF file is loaded.
## 🔒︎ int PageCount

The PDF document total page number.
### Members

---

## float GetPageHeight ( int pageIndex )

Returns the height of the specified PDF page, in units. One unit is 1/72 inch (around 0.3528 mm).
### Arguments

- *int* **pageIndex** - target page index.

### Return value

Page height, in units. One unit is 1/72 inch (around 0.3528 mm).
## float GetPageWidth ( int pageIndex )

Returns the width of the specified PDF page, in units. One unit is 1/72 inch (around 0.3528 mm).
### Arguments

- *int* **pageIndex** - target page index.

### Return value

Page width, in units. One unit is 1/72 inch (around 0.3528 mm).
## Image RenderPage ( int pageIndex , int width , int height , int render_flags = 0 )

Renders the specified PDF page into a new *[Image](../../../../api/library/common/class.image_cs.md)* object with the given width, height and [render flags](#RENDER_FLAG).
### Arguments

- *int* **pageIndex** - target page index.
- *int* **width** - target image width, in units. One unit is 1/72 inch (around 0.3528 mm).
- *int* **height** - target image height, in units. One unit is 1/72 inch (around 0.3528 mm).
- *int* **render_flags** - a [render flag](#RENDER_FLAG).

### Return value

Image containing the rendered PDF page data.
