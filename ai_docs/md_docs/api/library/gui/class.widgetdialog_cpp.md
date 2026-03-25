# Unigine::WidgetDialog Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetWindow


This class creates a [dialog window](../../../code/gui/ui/ui_containers.md#dialog).

The object of this class looks as follows:


![](../../../code/gui/ui/widgets/dialog.png)


### See Also


- C++ sample
- C# Component sample


## WidgetDialog Class

### Members

---

## static WidgetDialogPtr create ( const Ptr < Gui > & gui , const char * str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a dialog window with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the dialog will belong.
- *const char ** **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between widgets in the window and between them and the window border. This is an optional parameter.

## static WidgetDialogPtr create ( const char * str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a dialog window with given parameters and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between widgets in the window and between them and the window border. This is an optional parameter.

## Ptr < WidgetButton > getCancelButton ( ) const

Returns the button that cancels an action.
### Return value

Cancel button.
## int isCancelClicked ( ) const

Returns a value indicating if the Cancel button is clicked.
### Return value

1 if the Cancel button is clicked; otherwise, 0.
## void setCancelText ( const char * text )

Sets a caption of the Cancel button.
### Arguments

- *const char ** **text** - Cancel button caption.

## const char * getCancelText ( ) const

Returns the caption of the Cancel button. The default is Cancel.
### Return value

Cancel button caption.
## Ptr < WidgetButton > getCloseButton ( ) const

Returns the button that closes an action.
### Return value

Close button.
## int isCloseClicked ( ) const

Returns a value indicating if the Close button is clicked.
### Return value

1 if the Close button is clicked; otherwise, 0.
## void setCloseText ( const char * text )

Sets a caption of the Close button.
### Arguments

- *const char ** **text** - Close button caption.

## const char * getCloseText ( ) const

Returns the caption of the Close button. The default is empty.
### Return value

Close button caption.
## bool isDone ( ) const

Returns a value indicating if the dialog window is closed.
### Return value

**1** if the dialog window is closed; otherwise, **0**.
## Ptr < WidgetButton > getOkButton ( ) const

Returns the button that approves an action.
### Return value

OK button.
## bool isOkClicked ( ) const

Returns a value indicating if the OK button is clicked.
### Return value

true if the OK button is clicked; otherwise, false.
## void setOkText ( const char * text )

Sets a caption of the OK button.
### Arguments

- *const char ** **text** - OK button caption.

## const char * getOkText ( ) const

Returns the caption of the OK button. The default is OK.
### Return value

OK button caption.
## int getResult ( ) const

Returns a value indicating which button has been clicked.
### Return value

1 if the OK button is clicked; -1 if the Cancel button is clicked; 0 if the Close button is clicked.
