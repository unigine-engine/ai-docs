# Unigine::Plugins::PDFRender::PDFFile Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## PDFFile Class

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

## float getPageHeight ( int pageIndex )

Returns the height of the specified PDF page, in units. One unit is 1/72 inch (around 0.3528 mm).
### Arguments

- *int* **pageIndex** - target page index.

### Return value

Page height, in units. One unit is 1/72 inch (around 0.3528 mm).
## float getPageWidth ( int pageIndex )

Returns the width of the specified PDF page, in units. One unit is 1/72 inch (around 0.3528 mm).
### Arguments

- *int* **pageIndex** - target page index.

### Return value

Page width, in units. One unit is 1/72 inch (around 0.3528 mm).
## Image renderPage ( int pageIndex , int width , int height , int render_flags = 0 )

Renders the specified PDF page into a new *[Image](../../../../api/library/common/class.image_usc.md)* object with the given width, height and [render flags](#RENDER_FLAG).
### Arguments

- *int* **pageIndex** - target page index.
- *int* **width** - target image width, in units. One unit is 1/72 inch (around 0.3528 mm).
- *int* **height** - target image height, in units. One unit is 1/72 inch (around 0.3528 mm).
- *int* **render_flags** - a [render flag](#RENDER_FLAG).

### Return value

Image containing the rendered PDF page data.
