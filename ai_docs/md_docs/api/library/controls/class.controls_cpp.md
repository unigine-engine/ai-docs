# Unigine::Controls Class (CPP)

**Header:** #include <UnigineControls.h>


> **Notice:** This class is deprecated. Use *[Input](../../../api/library/controls/class.input_cpp.md)* class instead.


## Controls Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **CONTROLS_APP** = 0 | [ControlsApp](../../../api/library/controls/class.controlsapp_cpp.md) instance. |
| **CONTROLS_DUMMY** = 1 | [ControlsDummy](../../../api/library/controls/class.controlsdummy_cpp.md) instance. |

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

## static ControlsPtr create ( int type )

Creates a smart pointer to Controls.
### Arguments

- *int* **type** - Type of the controls to be created.

## void setState ( int state , int value )

Toggles the state of the given control on or off.
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).
- *int* **value** - State value: positive value to "press" the control; 0 to release it.

## int getState ( int state ) const

Returns the state of a given control (pressed or unpressed).
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

**1** if the control is pressed; otherwise, **0**.
## int getStateByName ( const char * name ) const

Returns the state of a given control (pressed or unpressed) by the control state name.
### Arguments

- *const char ** **name** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

**1** if the control is pressed; otherwise, **0**.
## const char * getStateName ( int state ) const

Returns the name of a given control state as a string.
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

Name of the control state.
## int clearState ( int state )

Returns a control state and clears it to **0** (not pressed). This function allows to handle control only once even if it is kept pressed over several frames.
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

State of the given control: 1 if the control is pressed; otherwise, 0.
## bool saveState ( const Ptr < Stream > & stream ) const

Saves controls settings into the stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int)* methods:


```cpp
// Get the instance of default engine controls and set its state
controls = Engine::getControls();
controls->setMouseDX(5.0f);

// save state
BlobPtr blob_state = Blob::create();
controls->saveState(blob_state);

// change state
controls->setMouseDX(1.0f);

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
controls->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true if the controls settings are saved successfully; otherwise, false.
## bool restoreState ( const Ptr < Stream > & stream )

Restores controls settings from the stream.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```cpp
// Get the instance of default engine controls and set its state
controls = Engine::getControls();
controls->setMouseDX(5.0f);

// save state
BlobPtr blob_state = Blob::create();
controls->saveState(blob_state);

// change state
controls->setMouseDX(1.0f);

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
controls->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true if the controls settings are restored successfully; otherwise, false.
