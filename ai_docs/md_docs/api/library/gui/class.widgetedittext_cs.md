# Unigine::WidgetEditText Class (CS)

**Inherits from:** Widget


This class creates a simple editable multi-line [text area](../../../code/gui/ui/ui_widgets.md#edittext) containing text strings.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/edittext.png)


> **Notice:** Word [wrapping](../../../api/library/gui/class.widget_cs.md#setFontWrap_int_void) and [rich text](../../../api/library/gui/class.widget_cs.md#setFontRich_int_void) options are not supported for this class.


#### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


## WidgetEditText Class

### Properties

## string Text

The contents of the text field.
## 🔒︎ int NumLines

The number of lines in the text field.
## 🔒︎ int SelectionLine

The number of the line where selection starts.
## 🔒︎ int SelectionPosition

The cursor position in the line where selection starts.
## 🔒︎ int CursorLine

The number of the current line.
## 🔒︎ int CursorPosition

The cursor position in the current line.
## vec4 NumberColor

The color used for numbers.
## vec4 SelectionColor

The color used to highlight the selection for the widget.
## vec4 BackgroundColor

The background color for the widget.
## int Background

The value indicating if a background texture is rendered for the text field. The default is 1.
## bool Editable

The value indicating if the contents of the text field can be edited. The default is value is true.
## 🔒︎ int CursorPositionX

The value of the text cursor position X coordinate.
## 🔒︎ int CursorPositionY

The value of the text cursor position Y coordinate.
## 🔒︎ int CursorWidth

The text cursor width.
## bool UseScrollWheelEnabled

The value indicating if the currently selected line is changed (the cursor moves up or down) when scrolling the mouse wheel.
## string StyleTextureBackground

The path to the texture to be used as a background of the widget.
## string StyleTextureSelection

The path to the texture to be used as a background for the selected text.
## Gui.CursorMode CursorMode

The cursor movement and hit-test mode for this text editor, one of the *Gui::CURSOR_MODE_** values. With *CURSOR_MODE_AUTO* (default) the mode is inherited from the **[GlobalCursorMode](../../../api/library/gui/class.gui_cs.md#getGlobalCursorMode_int)** property of the GUI. The visual mode moves the caret and selection in on-screen order per line, which is natural for bidirectional text; the logical mode follows the stored character sequence.
### Members

---

## WidgetEditText ( Gui gui , string str = 0 )

Constructor. Creates a multiline text field and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the text field will belong.
- *string* **str** - Initial value. This is an optional parameter.

## WidgetEditText ( string str = 0 )

Constructor. Creates a multiline text field and adds it to the Engine GUI.
### Arguments

- *string* **str** - Initial value. This is an optional parameter.

## void SetCursor ( int position , int line )

Sets the cursor to a given position in a given line.
### Arguments

- *int* **position** - Position number.
- *int* **line** - Line number.

## void SetLineText ( int line , string str )

Sets new contents for a given line.
### Arguments

- *int* **line** - Line number.
- *string* **str** - Text.

## string GetLineText ( int line )

Returns the text contained in a given line.
### Arguments

- *int* **line** - Line number.

### Return value

Text contained in the line.
## void SetSelection ( int position , int line )

Sets a line and a position from which a new selection will start.
### Arguments

- *int* **position** - Position number.
- *int* **line** - Line number.

## string GetSelectionText ( )

Returns the currently selected text.
### Return value

Currently selected text.
## void SetTokenColor ( string token , vec4 color )

Sets a color for a given token. The token will be highlighted with the provided color.
### Arguments

- *string* **token** - Token (i.e. keyword, identifier, etc).
- *vec4* **color** - Color.

## vec4 GetTokenColor ( string token )

Returns a color, which is used to highlight a given token.
### Arguments

- *string* **token** - Token.

### Return value

Color of the current token.
## void SetTokensColor ( string tokens , vec4 color )

Sets a color to given tokens. Each token will be highlighted with the provided color.
### Arguments

- *string* **tokens** - Comma-separated list of tokens (i.e. keywords, identifiers, etc).
- *vec4* **color** - Color.

## int AddLine ( string str = 0 )

Adds a new line to the widget.
### Arguments

- *string* **str** - Text to add. This is an optional argument.

### Return value

Number of the added line.
## void ClearSelectionText ( )

Deletes the currently selected text.
## void RemoveLine ( int line )

Deletes a given line.
### Arguments

- *int* **line** - Line number.

## int GetLineWidth ( int line , int end = -1 )

Returns the text line width (space taken by symbols).
### Arguments

- *int* **line** - The line index from 0 to the [total number of lines](#getNumLines_int).
- *int* **end** - The index of the last symbol up to which the line width is returned. If set to -1, the whole set of symbols in the line is taken.

### Return value

The text line width, in pixels.
