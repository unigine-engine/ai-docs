# Unigine::WidgetDialogImage Class (CS)

**Inherits from:** WidgetDialog


This class creates dialog window with an image preview of adjustable scale.


## WidgetDialogImage Class

### Properties

## string Texture

The name of the image whose preview and properties are displayed in the dialog.
### Members

---

## WidgetDialogImage ( Gui gui , string str = 0 )

Constructor. Creates an image dialog with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the dialog will belong.
- *string* **str** - Dialog title. This is an optional parameter.

## WidgetDialogImage ( string str = 0 )

Constructor. Creates an image dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Dialog title. This is an optional parameter.

## void SetImage ( Image image )

Sets the image, preview and properties of which should be displayed in the dialog.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to be set.

## Image GetImage ( )

Returns the image, preview and properties of which should be displayed in the dialog.
### Return value

Image, preview and properties of which are displayed in the dialog.
