# Unigine::WidgetDialog Class (CS)

**Inherits from:** WidgetWindow


This class creates a [dialog window](../../../code/gui/ui/ui_containers.md#dialog).

The object of this class looks as follows:


![](../../../code/gui/ui/widgets/dialog.png)


### See Also


- C++ sample
- C# Component sample


## WidgetDialog Class

### Properties

## string CloseText

The caption of the Close button. The default is empty.
## string CancelText

The caption of the Cancel button. The default is Cancel.
## string OkText

The caption of the OK button. The default is OK.
## 🔒︎ bool IsOkClicked

The value indicating if the OK button is clicked.
## 🔒︎ int Result

The value indicating which button has been clicked: 1 if the OK button is clicked; -1 if the Cancel button is clicked; 0 if the Close button is clicked.
## 🔒︎ bool IsDone

The value indicating if the dialog window is closed.
### Members

---

## WidgetDialog ( Gui gui , string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a dialog window with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the dialog will belong.
- *string* **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between widgets in the window and between them and the window border. This is an optional parameter.

## WidgetDialog ( string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a dialog window with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between widgets in the window and between them and the window border. This is an optional parameter.

## WidgetButton GetCancelButton ( )

Returns the button that cancels an action.
### Return value

Cancel button.
## int IsCancelClicked ( )

Returns a value indicating if the Cancel button is clicked.
### Return value

1 if the Cancel button is clicked; otherwise, 0.
## WidgetButton GetCloseButton ( )

Returns the button that closes an action.
### Return value

Close button.
## int IsCloseClicked ( )

Returns a value indicating if the Close button is clicked.
### Return value

1 if the Close button is clicked; otherwise, 0.
## WidgetButton GetOkButton ( )

Returns the button that approves an action.
### Return value

OK button.
