# Unigine::ControlsApp Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This class is deprecated. Use *[Input](../../../api/library/controls/class.input_usc.md)* class instead.


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

Sets a new value indicating which type of mouse data is used to control the camera � raw ([Input::getMouseDeltaRaw()](../../../api/library/controls/class.input_usc.md#getMouseDeltaRaw_ivec2)) or processed by the OS ([Input::getMouseDeltaPosition()](../../../api/library/controls/class.input_usc.md#getMouseDeltaPosition_ivec2)).
### Arguments

- *bool* **input** - Set **true** to enable mode using raw mouse data to control the camera; **false** - to disable it.

## bool isMouseRawInput () const

Returns the current value indicating which type of mouse data is used to control the camera � raw ([Input::getMouseDeltaRaw()](../../../api/library/controls/class.input_usc.md#getMouseDeltaRaw_ivec2)) or processed by the OS ([Input::getMouseDeltaPosition()](../../../api/library/controls/class.input_usc.md#getMouseDeltaPosition_ivec2)).
### Return value

**true** if mode using raw mouse data to control the camera is enabled ; otherwise **false**.
## void setMouseEnabled ( int enabled )

Sets a new value indicating if the mouse is enabled.
### Arguments

- *int* **enabled** - The the mouse

## int isMouseEnabled () const

Returns the current value indicating if the mouse is enabled.
### Return value

Current the mouse
## void setAlwaysRun ( int run = 0 )

Sets a new value indicating if the player is running by default. If the player is in this mode, the *Run* control will switch them to walking. A positive integer enables this mode, 0 disables it.
### Arguments

- *int* **run** - The positive integer to make the player run by default; otherwise, **0**.

## int getAlwaysRun () const

Returns the current value indicating if the player is running by default. If the player is in this mode, the *Run* control will switch them to walking. A positive integer enables this mode, 0 disables it.
### Return value

Current positive integer to make the player run by default; otherwise, **0**.
## void setEnabled ( int enabled )

Sets a new value indicating if input handling for current application window is enabled.
### Arguments

- *int* **enabled** - The input handling for current application window

## int isEnabled () const

Returns the current value indicating if input handling for current application window is enabled.
### Return value

Current input handling for current application window
## void setMouseHandle ( int handle )

Sets a new mouse behavior mode.
### Arguments

- *int* **handle** - The mouse behavior mode, one of the [MOUSE_HANDLE_*](../../../api/library/controls/class.input_usc.md#MOUSE_HANDLE_GRAB) values.

## int getMouseHandle () const

Returns the current mouse behavior mode.
### Return value

Current mouse behavior mode, one of the [MOUSE_HANDLE_*](../../../api/library/controls/class.input_usc.md#MOUSE_HANDLE_GRAB) values.
## void setAutosave ( int autosave )

Sets a new value indicating if current controls configuration settings are automatically saved to the corresponding controls config file (`configs/default.controls` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
### Arguments

- *int* **autosave** - The automatic saving of current controls configuration settings

## int isAutosave () const

Returns the current value indicating if current controls configuration settings are automatically saved to the corresponding controls config file (`configs/default.controls` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
### Return value

Current automatic saving of current controls configuration settings
## void setPath ( string path )

Sets a new path to the [controls configuration file](../../../code/configuration_file_usc.md#controls) (default: `configs/default.controls`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
### Arguments

- *string* **path** - The path to the controls configuration file.

## const char * getPath () const

Returns the current path to the [controls configuration file](../../../code/configuration_file_usc.md#controls) (default: `configs/default.controls`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
### Return value

Current path to the controls configuration file.
---

## void setState ( int state , int value )

Updates the state of a given control (sets the control on or off).
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).
- *int* **value** - State value: positive value to "press" the control; 0 to release it.

## int getState ( int state )

Returns the state of a given control.
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).

### Return value

State value: positive value means the control is "pressed"; 0 means the control is released.
## void setStateMouseButton ( int state , int button )

Sets a mouse button that switches a given state on and off. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).
- *int* **button** - Button that toggles the state, one of the [INPUT_MOUSE_BUTTON_](../../../api/library/controls/class.input_usc.md#MOUSE_BUTTON_LEFT) codes.

## int getStateMouseButton ( int state )

Returns a mouse button that switches a given state on and off. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).

### Return value

Button that toggles the state, one of the [INPUT_MOUSE_BUTTON_](../../../api/library/controls/class.input_usc.md#MOUSE_BUTTON_LEFT) codes.
## int isStateMouseButton ( int button )

Returns a value indicating if the given button assigned to the state.
### Arguments

- *int* **button** - Button that toggles the state, one of the [INPUT_MOUSE_BUTTON_](../../../api/library/controls/class.input_usc.md#MOUSE_BUTTON_LEFT) codes.

### Return value

**1** if the given button is assigned; otherwise, **0**.
## void getStateEvent ( int state )

Lets the user assign a key or a mouse button to a given state.
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).

## int isStateEvent ( )

Returns a value indicating if a key or a mouse button is successfully assigned to a state.
### Return value

**1** if a key or a mouse button is already assigned; otherwise, **0**.
## void setStateKey ( int state , int key )

Sets a key that toggles a given state on and off. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).
- *int* **key** - Key that switches the state, one of the [INPUT_KEY_](../../../api/library/controls/class.input_usc.md#KEY_UNKNOWN) codes.

## int getStateKey ( int state )

Returns a key that toggles a given state on and off. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).

### Return value

Key that switches the state, one of the [INPUT_KEY_](../../../api/library/controls/class.input_usc.md#KEY_UNKNOWN) codes.
## int isStateKey ( int key )

Checks if a given key already acts as an application control. This is useful to avoid collisions between application controls and hot keys.
### Arguments

- *int* **key** - Key that switches the state, one of the [INPUT_KEY_](../../../api/library/controls/class.input_usc.md#KEY_UNKNOWN) codes.

### Return value

**1** if the key is assigned to a state; otherwise, **0**.
## String getStateName ( int state )

Returns the name of the given control state.
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).

### Return value

Name of the given control state.
## String getStateInfo ( int state )

Returns the information about the given control state.
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).

### Return value

String containing information about the given control state.
## int clearState ( int state )

Returns a control state and clears it to 0 (control is not pressed).
### Arguments

- *int* **state** - State (one of *[CONTROLS_STATE_*](../../../api/library/controls/class.controls_usc.md#STATE_FORWARD)* variables).

### Return value

**1** if the control is pressed; otherwise, **0**.
## void setRemoveGrabKey ( int key )

Sets a new key to be used to switch off the [grab mode](../../../api/library/controls/class.input_usc.md#setMouseGrab_int_void) of the mouse pointer (mouse pointer is bound to the application window). See [this example](../../../code/usage/mouse_customization/index_usc.md#defines) for more information on mouse pointer modes and customization.
### Arguments

- *int* **key** - Key to be used to switch off the [grab mode](../../../api/library/controls/class.input_usc.md#setMouseGrab_int_void) of the mouse pointer, one of the [INPUT_KEY_](../../../api/library/controls/class.input_usc.md#KEY_UNKNOWN) codes.

## int getRemoveGrabKey ( )

Returns the key currently used to switch off the [grab mode](../../../api/library/controls/class.input_usc.md#setMouseGrab_int_void) of the mouse pointer (mouse pointer is bound to the application window). See [this example](../../../code/usage/mouse_customization/index_usc.md#defines) for more information on mouse pointer modes and customization.
### Return value

Key used to switch off the [grab mode](../../../api/library/controls/class.input_usc.md#setMouseGrab_int_void) of the mouse pointer, one of the [INPUT_KEY_](../../../api/library/controls/class.input_usc.md#KEY_UNKNOWN) codes.
## int load ( )

***Console*:**`controls_config_load`Loads controls configuration settings from a [controls configuration file](../../../code/configuration_file_usc.md) (`configs/default.controls` by default).
To change the path to the controls configuration file use the [*setPath()*](#setPath_cstr_void) method.

### Return value

1 if controls configuration settings are successfully loaded from a file; otherwise, 0.
## int save ( )

***Console*:**`controls_config_save`Saves controls configuration settings to a [controls configuration file](../../../code/configuration_file_usc.md) (`configs/default.controls` by default).
To change the path to the controls configuration file use the [*setPath()*](#setPath_cstr_void) method.

### Return value

1 if controls configuration settings are successfully saved to a file; otherwise, 0.
