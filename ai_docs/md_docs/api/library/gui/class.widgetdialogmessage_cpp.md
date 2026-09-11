# Unigine::WidgetDialogMessage Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetDialog


This class creates a dialog window containing a message text string.


## WidgetDialogMessage Class

### Members

## void setMessageText ( const char * text )

Sets a new text message of the dialog. The default is equal to the dialog title.
### Arguments

- *const char ** **text** - The text message of the dialog

## const char * getMessageText () const

Returns the current text message of the dialog. The default is equal to the dialog title.
### Return value

Current text message of the dialog
## void setMessageHidden ( bool hidden )

Sets a new value indicating if the text message in the widget is hidden or shown.
### Arguments

- *bool* **hidden** - true if the text message is hidden, false if it is shown

## bool isMessageHidden () const

Returns the current value indicating if the text message in the widget is hidden or shown.
### Return value

true if the text message is hidden, false if it is shown
---

## static WidgetDialogMessagePtr create ( const Ptr < Gui > & gui , const char * str = 0 )

Constructor. Creates a message dialog with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the dialog will belong.
- *const char ** **str** - Dialog title. This is an optional parameter.

## static WidgetDialogMessagePtr create ( const char * str = 0 )

Constructor. Creates a message dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Dialog title. This is an optional parameter.

## void setMessageFont ( const char * name )

Sets a font that will be used to display the text message in the widget.
### Arguments

- *const char ** **name** - Font name.

## void setMessageFontColor ( const Math:: vec4 & color )

Sets a color of the font used to display the text message in the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Font color.

## void setMessageFontRich ( int rich )

Sets a value indicating if rich text formatting should be used for the text message in the widget.
### Arguments

- *int* **rich** - Positive number to use rich text formatting, 0 to use plain text formatting.

## void setMessageFontSize ( int size )

Sets a size of the font used to display the text message in the widget.
### Arguments

- *int* **size** - Font size.
