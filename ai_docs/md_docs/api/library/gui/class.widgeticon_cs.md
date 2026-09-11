# Unigine::WidgetIcon Class (CS)

**Inherits from:** Widget


This class creates a toggleable [icon](../../../code/gui/ui/ui_widgets.md#icon) with two states - pressed or not.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/icon.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetIcon Class

### Properties

## string Text

The floating text placed over the icon.
## int TextAlign

The alignment flag set for the floating text over the icon. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_cs.md) variables. The default is *ALIGN_CENTER*.
## string Texture

The path to the icon image.
## bool Toggled

The value indicating if the icon serving as a toggle button is pressed.
## bool Toggleable

The value indicating if the icon is a toggle button or a simple button. The default is 0.
### Members

---

## WidgetIcon ( Gui gui , string str = 0 , int width = 0 , int height = 0 )

Constructor. Creates an icon of the specified size using a given texture and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new icon will belong.
- *string* **str** - The path to a texture file.
- *int* **width** - Icon width.
- *int* **height** - Icon height.

## WidgetIcon ( string str = 0 , int width = 0 , int height = 0 )

Constructor. Creates an icon of the specified size using a given texture and adds it to the Engine GUI.
### Arguments

- *string* **str** - The path to a texture file.
- *int* **width** - Icon width.
- *int* **height** - Icon height.

## void SetImage ( Image image )

Sets an icon image.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to set.

## Image GetImage ( )

Returns the icon image.
### Return value

Icon image.
