# Unigine::WidgetEditLine Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates an editable single-line [text field](../../../code/gui/ui/ui_widgets.md#editline) containing a text string.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/editline.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetEditLine Class

### Members

## void setText ( string text )

Sets a new text for the text field.
### Arguments

- *string* **text** - The contents of the text field.

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

Sets a new validator associated with the text field. The default is [VALIDATOR_ANY](../../../api/library/gui/class.gui_usc.md#VALIDATOR_ANY).
### Arguments

- *int* **validator** - The validator, one of the [*GUI_VALIDATOR_**](../../../api/library/gui/class.gui_usc.md) pre-defined variables.

## int getValidator () const

Returns the current validator associated with the text field. The default is [VALIDATOR_ANY](../../../api/library/gui/class.gui_usc.md#VALIDATOR_ANY).
### Return value

Current validator, one of the [*GUI_VALIDATOR_**](../../../api/library/gui/class.gui_usc.md) pre-defined variables.
## void setPassword ( int password )

Sets a new value indicating if the text field is a password field (all entered characters are displayed as dots).
### Arguments

- *int* **password** - The display of the text field contents as a password field (masked input)

## int isPassword () const

Returns the current value indicating if the text field is a password field (all entered characters are displayed as dots).
### Return value

Current display of the text field contents as a password field (masked input)
## void setEditable ( int editable )

Sets a new
### Arguments

- *int* **editable** - The editing of the text field contents

## int isEditable () const

Returns the current
### Return value

Current editing of the text field contents
## void setBorderColor ( vec4 color )

Sets a new border color for the widget.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getBorderColor () const

Returns the current border color for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setSelectionColor ( vec4 color )

Sets a new color used to highlight the selection for the widget.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getSelectionColor () const

Returns the current color used to highlight the selection for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setBackgroundColor ( vec4 color )

Sets a new background color for the widget.
### Arguments

- *vec4* **color** - The four-component vector specifying the color in the RGBA format.

## vec4 getBackgroundColor () const

Returns the current background color for the widget.
### Return value

Current four-component vector specifying the color in the RGBA format.
## void setStyleTextureBorder ( )

Sets a new path to the texture to be used as a border of the widget.
### Arguments

- **border** - The path to the texture to be used as a border of the widget.

## const char * getStyleTextureBorder () const

Returns the current path to the texture to be used as a border of the widget.
### Return value

Current path to the texture to be used as a border of the widget.
## void setStyleTextureBackground ( )

Sets a new path to the texture to be used as a background of the widget.
### Arguments

- **background** - The path to the texture to be used as a background of the widget.

## const char * getStyleTextureBackground () const

Returns the current path to the texture to be used as a background of the widget.
### Return value

Current path to the texture to be used as a background of the widget.
## void setStyleTextureSelection ( )

Sets a new path to the texture to be used as a background for the selected text.
### Arguments

- **selection** - The path to the texture to be used as a background for the selected text.

## const char * getStyleTextureSelection () const

Returns the current path to the texture to be used as a background for the selected text.
### Return value

Current path to the texture to be used as a background for the selected text.
## void setCursorMode ( int mode )

Sets a new cursor movement and hit-test mode for this text field, one of the *Gui::CURSOR_MODE_** values. With *CURSOR_MODE_AUTO* (default) the mode is inherited from the **[getGlobalCursorMode()()](../../../api/library/gui/class.gui_usc.md#getGlobalCursorMode_int)** property of the GUI. The visual mode moves the caret and selection in on-screen order, which is natural for bidirectional text; the logical mode follows the stored character sequence.
### Arguments

- *int* **mode** - The cursor movement mode of the text field

## int getCursorMode () const

Returns the current cursor movement and hit-test mode for this text field, one of the *Gui::CURSOR_MODE_** values. With *CURSOR_MODE_AUTO* (default) the mode is inherited from the **[getGlobalCursorMode()()](../../../api/library/gui/class.gui_usc.md#getGlobalCursorMode_int)** property of the GUI. The visual mode moves the caret and selection in on-screen order, which is natural for bidirectional text; the logical mode follows the stored character sequence.
### Return value

Current cursor movement mode of the text field
---

## static WidgetEditLine ( Gui gui , string str = 0 )

Constructor. Creates a text field and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the text field will belong.
- *string* **str** - Initial value. This is an optional parameter.

## static WidgetEditLine ( string str = 0 )

Constructor. Creates a text field and adds it to the Engine GUI.
### Arguments

- *string* **str** - Initial value. This is an optional parameter.

## String getSelectionText ( )

Returns currently selected text.
### Return value

Currently selected text.
## void clearSelectionText ( )

Deletes currently selected text.
