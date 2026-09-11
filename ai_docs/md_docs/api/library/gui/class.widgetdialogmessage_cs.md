# Unigine::WidgetDialogMessage Class (CS)

**Inherits from:** WidgetDialog


This class creates a dialog window containing a message text string.


## WidgetDialogMessage Class

### Properties

## string MessageText

The text message of the dialog. The default is equal to the dialog title.
## bool MessageHidden

The value indicating if the text message in the widget is hidden or shown.
### Members

---

## WidgetDialogMessage ( Gui gui , string str = 0 )

Constructor. Creates a message dialog with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the dialog will belong.
- *string* **str** - Dialog title. This is an optional parameter.

## WidgetDialogMessage ( string str = 0 )

Constructor. Creates a message dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Dialog title. This is an optional parameter.

## void SetMessageFont ( string name )

Sets a font that will be used to display the text message in the widget.
### Arguments

- *string* **name** - Font name.

## void SetMessageFontColor ( vec4 color )

Sets a color of the font used to display the text message in the widget.
### Arguments

- *vec4* **color** - Font color.

## void SetMessageFontRich ( int rich )

Sets a value indicating if rich text formatting should be used for the text message in the widget.
### Arguments

- *int* **rich** - Positive number to use rich text formatting, 0 to use plain text formatting.

## void SetMessageFontSize ( int size )

Sets a size of the font used to display the text message in the widget.
### Arguments

- *int* **size** - Font size.
