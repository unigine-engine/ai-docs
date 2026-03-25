# Unigine::WidgetDialogImage Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetDialog


This class creates dialog window with an image preview of adjustable scale.


## WidgetDialogImage Class

### Members

---

## static WidgetDialogImage ( Gui gui , string str = 0 )

Constructor. Creates an image dialog with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the dialog will belong.
- *string* **str** - Dialog title. This is an optional parameter.

## static WidgetDialogImage ( string str = 0 )

Constructor. Creates an image dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Dialog title. This is an optional parameter.

## void setImage ( Image image )

Sets the image, preview and properties of which should be displayed in the dialog.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to be set.

## Image getImage ( )

Returns the image, preview and properties of which should be displayed in the dialog.
### Return value

Image, preview and properties of which are displayed in the dialog.
## void setTexture ( string texture )

Sets a name of the image, preview and properties of which should be displayed in the dialog.
### Arguments

- *string* **texture** - Path to the image file.

## string getTexture ( )

Returns a name of the image, preview and properties of which should be displayed in the dialog.
### Return value

Path to the image file.
