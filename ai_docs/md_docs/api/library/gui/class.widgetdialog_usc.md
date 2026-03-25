# Unigine::WidgetDialog Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

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

## static WidgetDialog ( Gui gui , string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a dialog window with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the dialog will belong.
- *string* **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between widgets in the window and between them and the window border. This is an optional parameter.

## static WidgetDialog ( string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a dialog window with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between widgets in the window and between them and the window border. This is an optional parameter.

## WidgetButton getCancelButton ( )

Returns the button that cancels an action.
### Return value

Cancel button.
## int isCancelClicked ( )

Returns a value indicating if the Cancel button is clicked.
### Return value

1 if the Cancel button is clicked; otherwise, 0.
## void setCancelText ( string text )

Sets a caption of the Cancel button.
### Arguments

- *string* **text** - Cancel button caption.

## string getCancelText ( )

Returns the caption of the Cancel button. The default is Cancel.
### Return value

Cancel button caption.
## WidgetButton getCloseButton ( )

Returns the button that closes an action.
### Return value

Close button.
## int isCloseClicked ( )

Returns a value indicating if the Close button is clicked.
### Return value

1 if the Close button is clicked; otherwise, 0.
## void setCloseText ( string text )

Sets a caption of the Close button.
### Arguments

- *string* **text** - Close button caption.

## string getCloseText ( )

Returns the caption of the Close button. The default is empty.
### Return value

Close button caption.
## int isDone ( )

Returns a value indicating if the dialog window is closed.
### Return value

**1** if the dialog window is closed; otherwise, **0**.
## WidgetButton getOkButton ( )

Returns the button that approves an action.
### Return value

OK button.
## int isOkClicked ( )

Returns a value indicating if the OK button is clicked.
### Return value

**1** if the OK button is clicked; otherwise, **0**.
## void setOkText ( string text )

Sets a caption of the OK button.
### Arguments

- *string* **text** - OK button caption.

## string getOkText ( )

Returns the caption of the OK button. The default is OK.
### Return value

OK button caption.
## int getResult ( )

Returns a value indicating which button has been clicked.
### Return value

1 if the OK button is clicked; -1 if the Cancel button is clicked; 0 if the Close button is clicked.
