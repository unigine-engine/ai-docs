# Unigine::WidgetEditLine Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates an editable single-line [text field](../../../code/gui/ui/ui_widgets.md#editline) containing a text string.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/editline.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetEditLine Class

### Members

## void setText ( const char * text )

Sets a new text for the text field.
### Arguments

- *const char ** **text** - The contents of the text field.

## const char * getText () const

Returns the current text for the text field.
### Return value

Current contents of the text field.
## void setSelection ( int selection )

Sets a new position from which the selection starts.
### Arguments

- *int* **selection** - The position from which the selection starts.

## int getSelection () const

Returns the current position from which the selection starts.
### Return value

Current position from which the selection starts.
## void setCursor ( int cursor )

Sets a new cursor position in the text field.
### Arguments

- *int* **cursor** - The cursor position. The set value is saturated in the range from 0 to text field capacity.

## int getCursor () const

Returns the current cursor position in the text field.
### Return value

Current cursor position. The set value is saturated in the range from 0 to text field capacity.
## void setCapacity ( int capacity )

Sets a new maximum length of a string entered into the text field.
### Arguments

- *int* **capacity** - The maximum number of characters. The default is 1024.

## int getCapacity () const

Returns the current maximum length of a string entered into the text field.
### Return value

Current maximum number of characters. The default is 1024.
## void setBackground ( int background )

Sets a new value indicating if a background texture is rendered for the text field.
### Arguments

- *int* **background** - The positive number if a background texture is rendered; otherwise, 0. The default is 1.

## int getBackground () const

Returns the current value indicating if a background texture is rendered for the text field.
### Return value

Current positive number if a background texture is rendered; otherwise, 0. The default is 1.
## void setValidator ( int validator )

Sets a new validator associated with the text field. The default is [VALIDATOR_ANY](../../../api/library/gui/class.gui_cpp.md#VALIDATOR_ANY).
### Arguments

- *int* **validator** - The validator, one of the Gui:: Enumeration with [VALIDATOR_*](../../../api/library/gui/class.gui_cpp.md#VALIDATOR_ANY) prefixes.

## int getValidator () const

Returns the current validator associated with the text field. The default is [VALIDATOR_ANY](../../../api/library/gui/class.gui_cpp.md#VALIDATOR_ANY).
### Return value

Current validator, one of the Gui:: Enumeration with [VALIDATOR_*](../../../api/library/gui/class.gui_cpp.md#VALIDATOR_ANY) prefixes.
## void setPassword ( bool password )

Sets a new value indicating if the text field is a password field (all entered characters are displayed as dots).
### Arguments

- *bool* **password** - Set **true** to enable display of the text field contents as a password field (masked input); **false** - to disable it.

## bool isPassword () const

Returns the current value indicating if the text field is a password field (all entered characters are displayed as dots).
### Return value

**true** if display of the text field contents as a password field (masked input) is enabled ; otherwise **false**.
## void setEditable ( bool editable )

Sets a new value indicating if the contents of the text field can be edited.
### Arguments

- *bool* **editable** - Set **true** to enable editing of the text field contents; **false** - to disable it.

## bool isEditable () const

Returns the current value indicating if the contents of the text field can be edited.
### Return value

**true** if editing of the text field contents is enabled ; otherwise **false**.
## void setBorderColor ( const Math:: vec4 & color )

Sets a new border color for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBorderColor () const

Returns the current border color for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setSelectionColor ( const Math:: vec4 & color )

Sets a new color used to highlight the selection for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getSelectionColor () const

Returns the current color used to highlight the selection for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setBackgroundColor ( const Math:: vec4 & color )

Sets a new background color for the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getBackgroundColor () const

Returns the current background color for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setStyleTextureBorder ( const char * border )

Sets a new path to the texture to be used as a border of the widget.
### Arguments

- *const char ** **border** - The path to the texture to be used as a border of the widget.

## const char * getStyleTextureBorder () const

Returns the current path to the texture to be used as a border of the widget.
### Return value

Current path to the texture to be used as a border of the widget.
## void setStyleTextureBackground ( const char * background )

Sets a new path to the texture to be used as a background of the widget.
### Arguments

- *const char ** **background** - The path to the texture to be used as a background of the widget.

## const char * getStyleTextureBackground () const

Returns the current path to the texture to be used as a background of the widget.
### Return value

Current path to the texture to be used as a background of the widget.
## void setStyleTextureSelection ( const char * selection )

Sets a new path to the texture to be used as a background for the selected text.
### Arguments

- *const char ** **selection** - The path to the texture to be used as a background for the selected text.

## const char * getStyleTextureSelection () const

Returns the current path to the texture to be used as a background for the selected text.
### Return value

Current path to the texture to be used as a background for the selected text.
## void setCursorMode ( Gui::CursorMode mode )

Sets a new cursor movement and hit-test mode for this text field, one of the *Gui::CURSOR_MODE_** values. With *CURSOR_MODE_AUTO* (default) the mode is inherited from the **[getGlobalCursorMode()](../../../api/library/gui/class.gui_cpp.md#getGlobalCursorMode_int)** property of the GUI. The visual mode moves the caret and selection in on-screen order, which is natural for bidirectional text; the logical mode follows the stored character sequence.
### Arguments

- *[Gui::CursorMode](../../../api/library/gui/class.gui_cpp.md#CursorMode)* **mode** - The cursor movement mode of the text field

## Gui::CursorMode getCursorMode () const

Returns the current cursor movement and hit-test mode for this text field, one of the *Gui::CURSOR_MODE_** values. With *CURSOR_MODE_AUTO* (default) the mode is inherited from the **[getGlobalCursorMode()](../../../api/library/gui/class.gui_cpp.md#getGlobalCursorMode_int)** property of the GUI. The visual mode moves the caret and selection in on-screen order, which is natural for bidirectional text; the logical mode follows the stored character sequence.
### Return value

Current cursor movement mode of the text field
---

## static WidgetEditLinePtr create ( const Ptr < Gui > & gui , const char * str = 0 )

Constructor. Creates a text field and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the text field will belong.
- *const char ** **str** - Initial value. This is an optional parameter.

## static WidgetEditLinePtr create ( const char * str = 0 )

Constructor. Creates a text field and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Initial value. This is an optional parameter.

## String getSelectionText ( ) const

Returns currently selected text.
### Return value

Currently selected text.
## void clearSelectionText ( )

Deletes currently selected text.
