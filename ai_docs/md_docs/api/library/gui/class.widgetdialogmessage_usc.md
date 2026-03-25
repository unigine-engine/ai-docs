# Unigine::WidgetDialogMessage Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetDialog


This class creates a dialog window containing a message text string.


## WidgetDialogMessage Class

### Members

---

## static WidgetDialogMessage ( Gui gui , string str = 0 )

Constructor. Creates a message dialog with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the dialog will belong.
- *string* **str** - Dialog title. This is an optional parameter.

## static WidgetDialogMessage ( string str = 0 )

Constructor. Creates a message dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Dialog title. This is an optional parameter.

## void setMessageFont ( string name )

Sets a font that will be used to display the message.
### Arguments

- *string* **name** - Font name.

## void setMessageFontColor ( vec4 color )

Sets a color of the font used to display the message.
### Arguments

- *vec4* **color** - Font color.

## void setMessageFontRich ( int rich )

Sets a value indicating if rich text formatting should be used.
### Arguments

- *int* **rich** - Positive number to use rich text formatting, 0 to use plain text formatting.

## void setMessageFontSize ( int size )

Sets a size of the font used to display the message.
### Arguments

- *int* **size** - Font size.

## void setMessageHidden ( int hidden )

Hides or shows the text message in the widget.
### Arguments

- *int* **hidden** - **1** to hide the text message, **0** to show it.

## int isMessageHidden ( )

Returns a value indicating if a text message in the widget is hidden or shown.
### Return value

**1** if the text message is hidden; otherwise, **0**.
## void setMessageText ( string text )

Sets a message of the dialog.
### Arguments

- *string* **text** - Text message.

## string getMessageText ( )

Returns the message of the dialog. The default is equal to dialog title.
### Return value

Text message.
