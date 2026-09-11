# Unigine::WidgetEditText Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a simple editable multi-line [text area](../../../code/gui/ui/ui_widgets.md#edittext) containing text strings.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/edittext.png)


> **Notice:** Word [wrapping](../../../api/library/gui/class.widget_cpp.md#setFontWrap_int_void) and [rich text](../../../api/library/gui/class.widget_cpp.md#setFontRich_int_void) options are not supported for this class.


#### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


## WidgetEditText Class

### Members

## void setText ( const char * text )

Sets a new contents of the text field.
### Arguments

- *const char ** **text** - The text contained in the text field.

## const char * getText () const

Returns the current contents of the text field.
### Return value

Current text contained in the text field.
## int getNumLines () const

Returns the current number of lines in the text field.
### Return value

Current number of lines.
## int getSelectionLine () const

Returns the current number of the line where selection starts.
### Return value

Current line number.
## int getSelectionPosition () const

Returns the current cursor position in the line where selection starts.
### Return value

Current position number.
## int getCursorLine () const

Returns the current number of the current line.
### Return value

Current line number.
## int getCursorPosition () const

Returns the current cursor position in the current line.
### Return value

Current position number.
## void setNumberColor ( const Math:: vec4 & color )

Sets a new color used for numbers.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getNumberColor () const

Returns the current color used for numbers.
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
## void setBackground ( int background )

Sets a new value indicating if a background texture is rendered for the text field. The default is 1.
### Arguments

- *int* **background** - The value indicating if a background texture is rendered for the text field

## int getBackground () const

Returns the current value indicating if a background texture is rendered for the text field. The default is 1.
### Return value

Current value indicating if a background texture is rendered for the text field
## void setEditable ( bool editable )

Sets a new value indicating if the contents of the text field can be edited. The default is value is true.
### Arguments

- *bool* **editable** - Set **true** to enable editing of the text field contents; **false** - to disable it.

## bool isEditable () const

Returns the current value indicating if the contents of the text field can be edited. The default is value is true.
### Return value

**true** if editing of the text field contents is enabled ; otherwise **false**.
## int getCursorPositionX () const

Returns the current value of the text cursor position X coordinate.
### Return value

Current value of the text cursor position X coordinate, in pixels.
## int getCursorPositionY () const

Returns the current value of the text cursor position Y coordinate.
### Return value

Current value of the text cursor position Y coordinate, in pixels.
## int getCursorWidth () const

Returns the current text cursor width.
### Return value

Current text cursor width, in pixels.
## void setUseScrollWheelEnabled ( bool enabled )

Sets a new value indicating if the currently selected line is changed (the cursor moves up or down) when scrolling the mouse wheel.
### Arguments

- *bool* **enabled** - Set **true** to enable changing the line on scrolling; **false** - to disable it.

## bool isUseScrollWheelEnabled () const

Returns the current value indicating if the currently selected line is changed (the cursor moves up or down) when scrolling the mouse wheel.
### Return value

**true** if changing the line on scrolling is enabled ; otherwise **false**.
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

Sets a new cursor movement and hit-test mode for this text editor, one of the *Gui::CURSOR_MODE_** values. With *CURSOR_MODE_AUTO* (default) the mode is inherited from the **[getGlobalCursorMode()](../../../api/library/gui/class.gui_cpp.md#getGlobalCursorMode_int)** property of the GUI. The visual mode moves the caret and selection in on-screen order per line, which is natural for bidirectional text; the logical mode follows the stored character sequence.
### Arguments

- *[Gui::CursorMode](../../../api/library/gui/class.gui_cpp.md#CursorMode)* **mode** - The cursor movement mode of the text editor

## Gui::CursorMode getCursorMode () const

Returns the current cursor movement and hit-test mode for this text editor, one of the *Gui::CURSOR_MODE_** values. With *CURSOR_MODE_AUTO* (default) the mode is inherited from the **[getGlobalCursorMode()](../../../api/library/gui/class.gui_cpp.md#getGlobalCursorMode_int)** property of the GUI. The visual mode moves the caret and selection in on-screen order per line, which is natural for bidirectional text; the logical mode follows the stored character sequence.
### Return value

Current cursor movement mode of the text editor
---

## static WidgetEditTextPtr create ( const Ptr < Gui > & gui , const char * str = 0 )

Constructor. Creates a multiline text field and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the text field will belong.
- *const char ** **str** - Initial value. This is an optional parameter.

## static WidgetEditTextPtr create ( const char * str = 0 )

Constructor. Creates a multiline text field and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Initial value. This is an optional parameter.

## void setCursor ( int position , int line )

Sets the cursor to a given position in a given line.
### Arguments

- *int* **position** - Position number.
- *int* **line** - Line number.

## void setLineText ( int line , const char * str )

Sets new contents for a given line.
### Arguments

- *int* **line** - Line number.
- *const char ** **str** - Text.

## String getLineText ( int line ) const

Returns the text contained in a given line.
### Arguments

- *int* **line** - Line number.

### Return value

Text contained in the line.
## void setSelection ( int position , int line )

Sets a line and a position from which a new selection will start.
### Arguments

- *int* **position** - Position number.
- *int* **line** - Line number.

## String getSelectionText ( ) const

Returns the currently selected text.
### Return value

Currently selected text.
## void setTokenColor ( const char * token , const Math:: vec4 & color )

Sets a color for a given token. The token will be highlighted with the provided color.
### Arguments

- *const char ** **token** - Token (i.e. keyword, identifier, etc).
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color.

## Math:: vec4 getTokenColor ( const char * token ) const

Returns a color, which is used to highlight a given token.
### Arguments

- *const char ** **token** - Token (i.e. keyword, identifier, etc).

### Return value

Color of the current token.
## void setTokensColor ( const char * tokens , const Math:: vec4 & color )

Sets a color to given tokens. Each token will be highlighted with the provided color.
### Arguments

- *const char ** **tokens** - Comma-separated list of tokens (i.e. keywords, identifiers, etc).
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color.

## int addLine ( const char * str = 0 )

Adds a new line to the widget.
### Arguments

- *const char ** **str** - Text to add. This is an optional argument.

### Return value

Number of the added line.
## void clearSelectionText ( )

Deletes the currently selected text.
## void removeLine ( int line )

Deletes a given line.
### Arguments

- *int* **line** - Line number.

## int getLineWidth ( int line , int end = -1 ) const

Returns the text line width (space taken by symbols).
### Arguments

- *int* **line** - The line index from 0 to the [total number of lines](#getNumLines_int).
- *int* **end** - The index of the last symbol up to which the line width is returned. If set to -1, the whole set of symbols in the line is taken.

### Return value

The text line width, in pixels.
