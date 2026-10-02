# Unigine::ControlsApp Class (CS)


> **Notice:** This class is deprecated. Use *[Input](../../../api/library/controls/class.input_cs.md)* class instead.


## ControlsApp Class

### Properties

## float MouseDY

The screen position change of the mouse pointer along the y axis during the previous frame.
## float MouseDX

The screen position change of the mouse pointer along the x axis during the previous frame.
## float MouseSensitivity

The mouse sensitivity used to increase or decrease the speed of mouse movement.
## bool MouseInverse

The value indicating if back-and-forth movements of the mouse (by y-axis) are inverted: when the mouse is moved upward, the camera looks downwards, and when the mouse is moved downwards, the camera looks upwards. this mode is available only to control the camera.
## bool MouseRawInput

The value indicating which type of mouse data is used to control the camera � raw (*[Input.MouseDeltaRaw](../../../api/library/controls/class.input_cs.md#getMouseDeltaRaw_ivec2)*) or processed by the OS (*[Input.MouseDeltaPosition](../../../api/library/controls/class.input_cs.md#getMouseDeltaPosition_ivec2)*).
## bool MouseEnabled

The value indicating if the mouse is enabled.
## int AlwaysRun

The value indicating if the player is running by default. If the player is in this mode, the *Run* control will switch them to walking. A positive integer enables this mode, 0 disables it.
## bool Enabled

The value indicating if input handling for current application window is enabled.
## Input.MOUSE_HANDLE MouseHandle

The mouse behavior mode.
## bool Autosave

The value indicating if current controls configuration settings are automatically saved to the corresponding controls config file (`configs/default.controls` by default) on loading, closing, and saving the world, as well as on the Engine shutdown.
## string Path

The path to the [controls configuration file](../../../code/configuration_file_cs.md#controls) (default: `configs/default.controls`). The path can be specified as an absolute path or relative to the *[*-data_path*](../../../code/command_line.md#data_path)* or *<project_name>* folder if the *[*-project_name*](../../../code/command_line.md#project_name)* is set.
## Input.KEY RemoveGrabKey

The key used to switch off the [grab mode](../../../api/library/controls/class.input_cs.md#setMouseGrab_int_void) of the mouse pointer (mouse pointer is bound to the application window). See [this example](../../../code/usage/mouse_customization/index_cs.md#defines) for more information on mouse pointer modes and customization.
### Members

---

## void SetState ( int state , int value )

Sets the value of the given control state. Any positive value means the control is "pressed", 0 releases it.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).
- *int* **value** - State value: positive value to "press" the control; 0 to release it.

## int GetState ( int state )

Returns the value of the given control state: a positive value while the control is "pressed", 0 when it is released.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).

### Return value

State value: positive value means the control is "pressed"; 0 means the control is released.
## void SetStateMouseButton ( int state , Input.MOUSE_BUTTON button )

Assigns a mouse button to the given control state: from now on the state is switched on while the button is held. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).
- *[Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON)* **button** - Button that toggles the state, one of the [Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON) enum values.

## Input.MOUSE_BUTTON GetStateMouseButton ( int state )

Returns the mouse button assigned to the given control state, or [MOUSE_BUTTON_UNKNOWN](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON_UNKNOWN) if the state has no mouse button assigned. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).

### Return value

Button that toggles the state, one of the [Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON) enum values.
## int IsStateMouseButton ( Input.MOUSE_BUTTON button )

Returns a value indicating if the given mouse button is assigned to any control state. The method scans all states, it does not take a state number.
### Arguments

- *[Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON)* **button** - Button that toggles the state, one of the [Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON) enum values.

### Return value

**1** if the given button is assigned; otherwise, **0**.
## void GetStateEvent ( int state )

Starts capturing a binding for the given control state: the next key or mouse button the user presses is assigned to it, and the current value of the state is reset. Poll *[IsStateEvent()](../../...md#isStateEvent_int)* to find out when the capture is over.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).

## int IsStateEvent ( )

Returns a value indicating if a key or a mouse button is successfully assigned to a state.
### Return value

**1** if a key or a mouse button is already assigned; otherwise, **0**.
## void SetStateKey ( int state , Input.KEY key )

Assigns a key to the given control state: from now on the state is switched on while the key is held. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).
- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - Key that switches the state, one of the [Input.KEY](../../../api/library/controls/class.input_cs.md#KEY) enum values.

## Input.KEY GetStateKey ( int state )

Returns the key assigned to the given control state, or [KEY_UNKNOWN](../../../api/library/controls/class.input_cs.md#KEY_UNKNOWN) if the state has no key assigned. This parameter is stored in the following configuration file: **[*.controls](../../../code/configuration_file_cpp.md#controls)**.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).

### Return value

Key that switches the state, one of the [Input.KEY](../../../api/library/controls/class.input_cs.md#KEY) enum values.
## int IsStateKey ( Input.KEY key )

Checks if a given key already acts as an application control. This is useful to avoid collisions between application controls and hot keys.
### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - Key that switches the state, one of the [Input.KEY](../../../api/library/controls/class.input_cs.md#KEY) enum values.

### Return value

**1** if the key is assigned to a state; otherwise, **0**.
## string GetStateName ( int state )

Returns the name of the given control state, FORWARD or MOVE_LEFT for example. These names identify the states in the controls configuration file.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).

### Return value

Name of the given control state.
## string GetStateInfo ( int state )

Returns the bindings of the given control state as a string meant to be shown to the user: key W, key W or mouse LEFT, or empty when nothing is assigned to the state.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).

### Return value

String containing information about the given control state.
## int ClearState ( int state )

Returns the current value of the given control state and resets the state to 0. 0 is returned if the state number is out of range.
### Arguments

- *int* **state** - State (one of *[STATE_*](../../../api/library/controls/class.controls_cs.md#STATE_FORWARD)* variables).

### Return value

**1** if the control is pressed; otherwise, **0**.
## int Load ( )

***Console*:**`controls_config_load`Loads controls configuration settings from a [controls configuration file](../../../code/configuration_file_cs.md) (`configs/default.controls` by default).
To change the path to the controls configuration file use the [*setPath()*](#setPath_cstr_void) method.

### Return value

1 if controls configuration settings are successfully loaded from a file; otherwise, 0.
## int Save ( )

***Console*:**`controls_config_save`Saves controls configuration settings to a [controls configuration file](../../../code/configuration_file_cs.md) (`configs/default.controls` by default).
To change the path to the controls configuration file use the [*setPath()*](#setPath_cstr_void) method.

### Return value

1 if controls configuration settings are successfully saved to a file; otherwise, 0.
