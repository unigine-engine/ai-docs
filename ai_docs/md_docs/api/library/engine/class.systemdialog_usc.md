# Unigine.SystemDialog Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to create and manage system dialogs displaying informational, warning, and error messages.


## SystemDialog Class

### Members

---

## SystemDialog ( )

Constructor.
## void setType ( int type )

Sets the type of the system dialog.
### Arguments

- *int* **type** - Dialog type to be set: one of the [SYSTEM_DIALOG_TYPE_*](#TYPE_ERROR) values.

## int getType ( )

Returns the current type of the system dialog.
### Return value

Dialog type to be set: one of the [SYSTEM_DIALOG_TYPE_*](#TYPE_ERROR) values.
## void setTitle ( string title )

Sets a new title for the system dialog.
### Arguments

- *string* **title** - Dialog title to be set.

## string getTitle ( )

Returns the current title of the system dialog.
### Return value

Current dialog title.
## void setMessage ( string message )

Sets a new message of the system dialog.
### Arguments

- *string* **message** - Dialog message to be set.

## string getMessage ( )

Returns the current message of the system dialog.
### Return value

Current dialog message.
## void setDefaultButtonReturn ( int val )

Sets a default button to be pressed by default when the user hits the *Return* key on the keyboard.
### Arguments

- *int* **val** - Number of the button to be set, in the range from 0 to the [total number of buttons](#getNumButtons_int).

## int getDefaultButtonReturn ( )

Returns the current default button to be pressed by default when the user hits the *Return* key on the keyboard.
### Return value

Number of the button, in the range from 0 to the [total number of buttons](#getNumButtons_int).
## void setDefaultButtonEscape ( int escape )

Sets a default button to be pressed by default when the user hits the *Escape* key on the keyboard.
### Arguments

- *int* **escape** - Number of the button to be set, in the range from 0 to the [total number of buttons](#getNumButtons_int).

## int getDefaultButtonEscape ( )

Returns the current default button to be pressed by default when the user hits the *Escape* key on the keyboard.
### Return value

Number of the button, in the range from 0 to the [total number of buttons](#getNumButtons_int).
## int getNumButtons ( )

Returns the total number of buttons of the system dialog.
### Return value

Total number of dialog buttons.
## int addButton ( )

Adds a new button to the system dialog.
### Return value

Number of the new added button.
## int addButton ( string name )

Adds a new button to the system dialog.
### Arguments

- *string* **name** - Name of the button to be added.

### Return value

Number of the new added button.
## void removeButton ( int num )

Removes the button with the specified number from the system dialog.
### Arguments

- *int* **num** - Number of the button to be removed, in the range from 0 to the [total number of buttons](#getNumButtons_int).

## void swapButtons ( int num_0 , int num_1 )

Swaps two buttons with the specified numbers.
### Arguments

- *int* **num_0** - Number of the first button, in the range from 0 to the [total number of buttons](#getNumButtons_int).
- *int* **num_1** - Number of the second button, in the range from 0 to the [total number of buttons](#getNumButtons_int).

## string getButtonName ( int num )

Returns the name of the button by its number.
### Arguments

- *int* **num** - Number of the button, in the range from 0 to the [total number of buttons](#getNumButtons_int).

### Return value

Name of the button with the specified number.
## void setButtonName ( int num , string name )

Sets as new name for the button with the specified number.
### Arguments

- *int* **num** - Number of the button to be renamed, in the range from 0 to the [total number of buttons](#getNumButtons_int).
- *string* **name** - New name to be set for the button with the specified number.
