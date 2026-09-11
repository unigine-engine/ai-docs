# Unigine::WidgetDialogColor Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetDialog


This class creates a dialog with clickable color field, RGB value sliders, color parameters and a predefined palette. There are two color formats available:

- Standard format, which represents colors as four-component vectors.
- Web format, which allows these variants: *RRGGBB*, *RRGGBBAA*, *#RRGGBB*, *#RRGGBBAA*.


## WidgetDialogColor Class

### Members

## void setPaletteColors ( const char * colors )

Sets a new palette colors of the dialog, as a list of colors in the web format separated with semicolons.
### Arguments

- *const char ** **colors** - The palette colors of the dialog, as a list of colors in the web format separated with semicolons

## const char * getPaletteColors () const

Returns the current palette colors of the dialog, as a list of colors in the web format separated with semicolons.
### Return value

Current palette colors of the dialog, as a list of colors in the web format separated with semicolons
## void setWebColor ( const char * color )

Sets a new color selected in the dialog, in the web (hexadecimal) format.
### Arguments

- *const char ** **color** - The color selected in the dialog, in the web (hexadecimal) format

## const char * getWebColor () const

Returns the current color selected in the dialog, in the web (hexadecimal) format.
### Return value

Current color selected in the dialog, in the web (hexadecimal) format
## void setColor ( const Math:: vec4 & color )

Sets a new color selected in the dialog.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color selected in the dialog

## Math:: vec4 getColor () const

Returns the current color selected in the dialog.
### Return value

Current color selected in the dialog
---

## static WidgetDialogColorPtr create ( const Ptr < Gui > & gui , const char * str = 0 )

Constructor. Creates a color picker dialog with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the dialog will belong.
- *const char ** **str** - Dialog title. This is an optional parameter.

## static WidgetDialogColorPtr create ( const char * str = 0 )

Constructor. Creates a color picker dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Dialog title. This is an optional parameter.
