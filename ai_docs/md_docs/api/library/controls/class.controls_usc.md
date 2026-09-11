# Unigine::Controls Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


> **Notice:** This class is deprecated. Use *[Input](../../../api/library/controls/class.input_usc.md)* class instead.


## Controls Class

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
## const char * getTypeName () const

Returns the current type name of input controls.
### Return value

Current type name of input controls.
## getType () const

Returns the current type of input controls.
### Return value

Current Controls type (one of *CONTROLS_** variables):
1. *[CONTROLS_APP](#CONTROLS_APP)* = 0
2. *[CONTROLS_DUMMY](#CONTROLS_DUMMY)*


---

## void engine.controls. setState ( int state , int value )

Toggles the state of the given control on or off.
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).
- *int* **value** - Positive value to "press" the corresponding control; **0** to release it.

## int engine.controls. getState ( int state )

Returns the state of a given control (pressed or unpressed).
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

**1** if the control is pressed; otherwise, **0**.
## int engine.controls. getStateByName ( string name )

Returns the state of a given control (pressed or unpressed) by the control state name.
### Arguments

- *string* **name** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

**1** if the control is pressed; otherwise, **0**.
## string engine.controls. getStateName ( int state )

Returns the name of a given control state as a string.
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

Name of the control state.
## int engine.controls. clearState ( int state )

Returns a control state and clears it to **0** (not pressed). This function allows to handle control only once even if it is kept pressed over several frames.
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

State of the given control: 1 if the control is pressed; otherwise, 0.
## int engine.controls. saveState ( Stream stream )

Saves controls settings into the stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int)* methods:


```cpp
// Get the instance of default engine controls and set its state
Controls controls = engine.getControls();
controls.setMouseDX(5.0f);

// save state
Blob blob_state = new Blob();
controls.saveState(blob_state);

// change state
controls.setMouseDX(1.0f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
controls.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - The stream to save controls data.

### Return value

**1** if the controls settings are saved successfully; otherwise, **0**.
## int engine.controls. restoreState ( Stream stream )

Restores controls settings from the stream.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```cpp
// Get the instance of default engine controls and set its state
Controls controls = engine.getControls();
controls.setMouseDX(5.0f);

// save state
Blob blob_state = new Blob();
controls.saveState(blob_state);

// change state
controls.setMouseDX(1.0f);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
controls.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - The stream to save controls data.

### Return value

**1** if the controls settings are restored successfully; otherwise, **0**.
