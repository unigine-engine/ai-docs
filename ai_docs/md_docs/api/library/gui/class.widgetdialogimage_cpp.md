# Unigine::WidgetDialogImage Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetDialog


This class creates dialog window with an image preview of adjustable scale.


## WidgetDialogImage Class

### Members

---

## static WidgetDialogImagePtr create ( const Ptr < Gui > & gui , const char * str = 0 )

Constructor. Creates an image dialog with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the dialog will belong.
- *const char ** **str** - Dialog title. This is an optional parameter.

## static WidgetDialogImagePtr create ( const char * str = 0 )

Constructor. Creates an image dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Dialog title. This is an optional parameter.

## void setImage ( const Ptr < Image > & image )

Sets the image, preview and properties of which should be displayed in the dialog.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image to be set.

## Ptr < Image > getImage ( ) const

Returns the image, preview and properties of which should be displayed in the dialog.
### Return value

Image, preview and properties of which are displayed in the dialog.
## void setTexture ( const char * texture )

Sets a name of the image, preview and properties of which should be displayed in the dialog.
### Arguments

- *const char ** **texture** - Path to an image file.

## const char * getTexture ( ) const

Returns a name of the image, preview and properties of which should be displayed in the dialog.
### Return value

Path to the image file.
