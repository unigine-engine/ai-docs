# Unigine::WidgetEditLine Class (CS)

**Inherits from:** Widget


This class creates an editable single-line [text field](../../../code/gui/ui/ui_widgets.md#editline) containing a text string.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/editline.png)


#### See Also


- C++ sample
- C# Component sample


## WidgetEditLine Class

### Properties

## string Text

The text for the text field.
## int Selection

The position from which the selection starts.
## int Cursor

The cursor position in the text field.
## int Capacity

The maximum length of a string entered into the text field.
## int Background

The value indicating if a background texture is rendered for the text field.
## int Validator

The validator associated with the text field. The default is [VALIDATOR_ANY](../../../api/library/gui/class.gui_cs.md#VALIDATOR_ANY).
## bool Password

The value indicating if the text field is a password field (all entered characters are displayed as dots).
## bool Editable

The value indicating if the contents of the text field can be edited.
## vec4 BorderColor

The border color for the widget.
## vec4 SelectionColor

The color used to highlight the selection for the widget.
## vec4 BackgroundColor

The background color for the widget.
## string StyleTextureBorder

The path to the texture to be used as a border of the widget.
## string StyleTextureBackground

The path to the texture to be used as a background of the widget.
## string StyleTextureSelection

The path to the texture to be used as a background for the selected text.
## Gui.CursorMode CursorMode

The cursor movement and hit-test mode for this text field, one of the *Gui::CURSOR_MODE_** values. With *CURSOR_MODE_AUTO* (default) the mode is inherited from the **[GlobalCursorMode](../../../api/library/gui/class.gui_cs.md#getGlobalCursorMode_int)** property of the GUI. The visual mode moves the caret and selection in on-screen order, which is natural for bidirectional text; the logical mode follows the stored character sequence.
### Members

---

## WidgetEditLine ( Gui gui , string str = 0 )

Constructor. Creates a text field and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the text field will belong.
- *string* **str** - Initial value. This is an optional parameter.

## WidgetEditLine ( string str = 0 )

Constructor. Creates a text field and adds it to the Engine GUI.
### Arguments

- *string* **str** - Initial value. This is an optional parameter.

## string GetSelectionText ( )

Returns currently selected text.
### Return value

Currently selected text.
## void ClearSelectionText ( )

Deletes currently selected text.
