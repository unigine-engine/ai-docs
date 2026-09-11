# Unigine::ControlsApp Class (CPP)

**Header:** #include <UnigineControls.h>


> **Notice:** This class is deprecated. Use *[Input](../../../api/library/controls/class.input_cpp.md)* class instead.


## ControlsApp Class

### Members

## void setMouseDY ( float dy )

Sets a new screen position change of the mouse pointer along the y axis during the previous frame.
### Arguments

- *float* **dy** - The screen position change of the mouse pointer along the y axis during the previous frame.

## float getMouseDY () const

Returns the current screen position change of the mouse pointer along the y axis during the previous frame.
### Return value

Current screen position change of the mouse pointer along the y axis during the previous frame.
## void setMouseDX ( float dx )

Sets a new screen position change of the mouse pointer along the x axis during the previous frame.
### Arguments

- *float* **dx** - The screen position change of the mouse pointer along the x axis during the previous frame.

## float getMouseDX () const

Returns the current screen position change of the mouse pointer along the x axis during the previous frame.
### Return value

Current screen position change of the mouse pointer along the x axis during the previous frame.
## void setMouseSensitivity ( float sensitivity )

Sets a new mouse sensitivity used to increase or decrease the speed of mouse movement.
### Arguments

- *float* **sensitivity** - The mouse sensitivity used to increase or decrease the speed of mouse movement.

## float getMouseSensitivity () const

Returns the current mouse sensitivity used to increase or decrease the speed of mouse movement.
### Return value

Current mouse sensitivity used to increase or decrease the speed of mouse movement.
## void setMouseInverse ( bool inverse )

Sets a new value indicating if back-and-forth movements of the mouse (by y-axis) are inverted: when the mouse is moved upward, the camera looks downwards, and when the mouse is moved downwards, the camera looks upwards. this mode is available only to control the camera.
### Arguments

- *bool* **inverse** - Set **true** to enable the inverted state of the mouse; **false** - to disable it.

## bool isMouseInverse () const

Returns the current value indicating if back-and-forth movements of the mouse (by y-axis) are inverted: when the mouse is moved upward, the camera looks downwards, and when the mouse is moved downwards, the camera looks upwards. this mode is available only to control the camera.
### Return value

**true** if the inverted state of the mouse is enabled ; otherwise **false**.
## void setMouseRawInput ( bool input )

Sets a new value indicating which type of mouse data is used to control the camera � raw ([Input::getMouseDeltaRaw()](../../../api/library/controls/class.input_cpp.md#getMouseDeltaRaw_ivec2)) or processed by the OS ([Input::getMouseDeltaPosition()](../../../api/library/controls/class.input_cpp.md#getMouseDeltaPosition_ivec2)).
### Arguments

- *bool* **input** - Set **true** to enable mode using raw mouse data to control the camera; **false** - to disable it.

## bool isMouseRawInput () const

Returns the current value indicating which type of mouse data is used to control the camera � raw ([Input::getMouseDeltaRaw()](../../../api/library/controls/class.input_cpp.md#getMouseDeltaRaw_ivec2)) or processed by the OS ([Input::getMouseDeltaPosition()](../../../api/library/controls/class.input_cpp.md#getMouseDeltaPosition_ivec2)).
### Return value

**true** if mode using raw mouse data to control the camera is enabled ; otherwise **false**.
## void setMouseEnabled ( bool enabled )

Sets a new value indicating if the mouse is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable the mouse; **false** - to disable it.

## bool isMouseEnabled () const

Returns the current value indicating if the mouse is enabled.
### Return value

**true** if the mouse is enabled ; otherwise **false**.
## void setAlwaysRun ( int run = 0 )

Sets a new value indicating if the player is running by default. If the player is in this mode, the *Run* control will switch them to walking. A positive integer enables this mode, 0 disables it.
### Arguments

- *int* **run** - The positive integer to make the player run by default; otherwise, **0**.

## int getAlwaysRun () const

Returns the current value indicating if the player is running by default. If the player is in this mode, the *Run* control will switch them to walking. A positive integer enables this mode, 0 disables it.
### Return value

Current positive integer to make the player run by default; otherwise, **0**.
## void setEnabled ( bool enabled )

Sets a new value indicating if input handling for current application window is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable input handling for current application window; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if input handling for current application window is enabled.
### Return value

**true** if input handling for current application window is enabled ; otherwise **false**.
## void setMouseHandle ( Input::MOUSE_HANDLE handle )

Sets a new mouse behavior mode.
### Arguments

- *[Input::MOUSE_HANDLE](../../../api/library/controls/class.input_cpp.md#MOUSE_HANDLE)* **handle** - The mouse behavior mode, one of the [MOUSE_HANDLE_*](../../../api/library/controls/class.input_cpp.md#MOUSE_HANDLE) values.

## Input::MOUSE_HANDLE getMouseHandle () const

Returns the current mouse behavior mode.
### Return value

Current mouse behavior mode, one of the [MOUSE_HANDLE_*](../../../api/library/controls/class.input_cpp.md#MOUSE_HANDLE) values.
## void setAutosave ( bool autosave )

Sets a new value indicating if current controls configuration settings are automatically saved to the corresponding controls config file (`configs/default.controls` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
### Arguments

- *bool* **autosave** - Set **true** to enable automatic saving of current controls configuration settings; **false** - to disable it.

## bool isAutosave () const

Returns the current value indicating if current controls configuration settings are automatically saved to the corresponding controls config file (`configs/default.controls` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
### Return value

**true** if automatic saving of current controls configuration settings is enabled ; otherwise **false**.
## void setPath ( const char * path )

Sets a new path to the [controls configuration file](../../../code/configuration_file_cpp.md#controls) (default: `configs/default.controls`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
### Arguments

- *const char ** **path** - The path to the controls configuration file.

## const char * getPath () const

Returns the current path to the [controls configuration file](../../../code/configuration_file_cpp.md#controls) (default: `configs/default.controls`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
### Return value

Current path to the controls configuration file.
---

## void setState ( int state , int value )

Updates the state of a given control (sets the control on or off).
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.
- *int* **value** - State value: positive value to "press" the control; 0 to release it.

## int getState ( int state )

Returns the state of a given control.
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.

### Return value

State value: positive value means the control is "pressed"; 0 means the control is released.
## void setStateMouseButton ( int state , Input::MOUSE_BUTTON button )

Sets a mouse button that switches a given state on and off. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.
- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - Button that toggles the state, one of the preset [MOUSE_BUTTON_](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON) codes.

## Input::MOUSE_BUTTON getStateMouseButton ( int state )

Returns a mouse button that switches a given state on and off. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.

### Return value

Button that toggles the state, one of the preset [MOUSE_BUTTON_](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON) codes.
## int isStateMouseButton ( Input::MOUSE_BUTTON button )

Returns a value indicating if the given button assigned to the state.
### Arguments

- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - Button that toggles the state, one of the preset [MOUSE_BUTTON_](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON) codes.

### Return value

**1** if the given button is assigned; otherwise, **0**.
## void getStateEvent ( int state )

Lets the user assign a key or a mouse button to a given state.
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.

## int isStateEvent ( )

Returns a value indicating if a key or a mouse button is successfully assigned to a state.
### Return value

**1** if a key or a mouse button is already assigned; otherwise, **0**.
## void setStateKey ( int state , Input::KEY key )

Sets a key that toggles a given state on and off. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.
- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - Key that switches the state, one of the preset [KEY_](../../../api/library/controls/class.input_cpp.md#KEY) codes.

## Input::KEY getStateKey ( int state )

Returns a key that toggles a given state on and off. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.

### Return value

Key that switches the state, one of the preset [KEY_](../../../api/library/controls/class.input_cpp.md#KEY) codes.
## int isStateKey ( Input::KEY key )

Checks if a given key already acts as an application control. This is useful to avoid collisions between application controls and hot keys.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - Key that switches the state, one of the preset [KEY_](../../../api/library/controls/class.input_cpp.md#KEY) codes.

### Return value

**1** if the key is assigned to a state; otherwise, **0**.
## String getStateName ( int state )

Returns the name of the given control state.
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.

### Return value

Name of the given control state.
## String getStateInfo ( int state ) const

Returns the information about the given control state.
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.

### Return value

String containing information about the given control state.
## int clearState ( int state )

Returns a control state and clears it to 0 (control is not pressed).
### Arguments

- *int* **state** - Control state number. Possible values are in range [ [STATE_FORWARD](../../../api/library/controls/class.controls_cpp.md#STATE_FORWARD);NUM_STATES]. For full list of available controls see Unigine::Controls:: Enumeration at the end of the article.

### Return value

**1** if the control is pressed; otherwise, **0**.
## void setRemoveGrabKey ( Input::KEY key )

Sets a new key to be used to switch off the [grab mode](../../../api/library/controls/class.input_cpp.md#setMouseGrab_int_void) of the mouse pointer (mouse pointer is bound to the application window). See [this example](../../../code/usage/mouse_customization/index_cpp.md#defines) for more information on mouse pointer modes and customization.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - Key to be used to switch off the [grab mode](../../../api/library/controls/class.input_cpp.md#setMouseGrab_int_void) of the mouse pointer, one of the preset [KEY_](../../../api/library/controls/class.input_cpp.md#KEY) codes.

## Input::KEY getRemoveGrabKey ( ) const

Returns the key currently used to switch off the [grab mode](../../../api/library/controls/class.input_cpp.md#setMouseGrab_int_void) of the mouse pointer (mouse pointer is bound to the application window). See [this example](../../../code/usage/mouse_customization/index_cpp.md#defines) for more information on mouse pointer modes and customization.
### Return value

Key used to switch off the [grab mode](../../../api/library/controls/class.input_cpp.md#setMouseGrab_int_void) of the mouse pointer, one of the preset [KEY_](../../../api/library/controls/class.input_cpp.md#KEY) codes.
## int load ( )

***Console*:**`controls_config_load`Loads controls configuration settings from a [controls configuration file](../../../code/configuration_file_cpp.md) (`configs/default.controls` by default).
To change the path to the controls configuration file use the [*setPath()*](#setPath_cstr_void) method.

### Return value

1 if controls configuration settings are successfully loaded from a file; otherwise, 0.
## int save ( ) const

***Console*:**`controls_config_save`Saves controls configuration settings to a [controls configuration file](../../../code/configuration_file_cpp.md) (`configs/default.controls` by default).
To change the path to the controls configuration file use the [*setPath()*](#setPath_cstr_void) method.

### Return value

1 if controls configuration settings are successfully saved to a file; otherwise, 0.
