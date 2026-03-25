# Unigine::WidgetDialogColor Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetDialog


This class creates a dialog with clickable color field, RGB value sliders, color parameters and a predefined palette. There are two color formats available:

- Standard format, which represents colors as four-component vectors.
- Web format, which allows these variants: *RRGGBB*, *RRGGBBAA*, *#RRGGBB*, *#RRGGBBAA*.


## WidgetDialogColor Class

### Members

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

## void setColor ( const Math:: vec4 & color )

Selects a given color.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color.

## Math:: vec4 getColor ( ) const

Returns the currently selected color.
### Return value

Current color.
## void setPaletteColors ( const char * colors )

Fills the palette with given colors.
### Arguments

- *const char ** **colors** - A list of colors in the Web format separated with semicolons.

## const char * getPaletteColors ( ) const

Returns the current palette colors.
### Return value

List of colors in the Web format separated with semicolons.
## void setWebColor ( const char * color )

Selects a color in the web format.
### Arguments

- *const char ** **color** - Color in the web format.

## const char * getWebColor ( ) const

Returns the currently selected color in the web format.
### Return value

Current color.
