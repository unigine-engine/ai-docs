# Unigine.SystemDialog Class (CS)


This class is used to create and manage system dialogs displaying informational, warning, and error messages.


## SystemDialog Class

### Properties

## int Type

The Dialog type to be set: one of the [TYPE_*](#TYPE_ERROR) values.
## string Title

The Current dialog title.
## string Message

The Current dialog message.
## int DefaultButtonReturn

The Number of the button, in the range from 0 to the [total number of buttons](#getNumButtons_int).
## int DefaultButtonEscape

The Number of the button, in the range from 0 to the [total number of buttons](#getNumButtons_int).
## 🔒︎ int NumButtons

The Total number of dialog buttons.
### Members

---

## SystemDialog ( )

Constructor.
## int AddButton ( )

Adds a new button to the system dialog.
### Return value

Number of the new added button.
## int AddButton ( string name )

Adds a new button to the system dialog.
### Arguments

- *string* **name** - Name of the button to be added.

### Return value

Number of the new added button.
## void RemoveButton ( int num )

Removes the button with the specified number from the system dialog.
### Arguments

- *int* **num** - Number of the button to be removed, in the range from 0 to the [total number of buttons](#getNumButtons_int).

## void SwapButtons ( int num_0 , int num_1 )

Swaps two buttons with the specified numbers.
### Arguments

- *int* **num_0** - Number of the first button, in the range from 0 to the [total number of buttons](#getNumButtons_int).
- *int* **num_1** - Number of the second button, in the range from 0 to the [total number of buttons](#getNumButtons_int).

## string GetButtonName ( int num )

Returns the name of the button by its number.
### Arguments

- *int* **num** - Number of the button, in the range from 0 to the [total number of buttons](#getNumButtons_int).

### Return value

Name of the button with the specified number.
## void SetButtonName ( int num , string name )

Sets as new name for the button with the specified number.
### Arguments

- *int* **num** - Number of the button to be renamed, in the range from 0 to the [total number of buttons](#getNumButtons_int).
- *string* **name** - New name to be set for the button with the specified number.
