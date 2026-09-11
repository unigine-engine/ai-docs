# Unigine::Controls Class (CS)


> **Notice:** This class is deprecated. Use *[Input](../../../api/library/controls/class.input_cs.md)* class instead.


## Controls Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **CONTROLS_APP** = 0 | [ControlsApp](../../../api/library/controls/class.controlsapp_cs.md) instance. |
| **CONTROLS_DUMMY** = 1 | [ControlsDummy](../../../api/library/controls/class.controlsdummy_cs.md) instance. |

### Properties

## float MouseDY

The screen position change of the mouse pointer along the y axis during the previous frame.
## float MouseDX

The screen position change of the mouse pointer along the x axis during the previous frame.
## 🔒︎ string TypeName

The type name of input controls.
## 🔒︎ Controls.TYPE Type

The type of input controls.
### Members

---

## Controls ( int type )

Creates a smart pointer to Controls.
### Arguments

- *int* **type** - Type of the controls to be created.

## void SetState ( int state , int value )

Toggles the state of the given control on or off.
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).
- *int* **value** - Positive value to "press" the corresponding control; **0** to release it.

## int GetState ( int state )

Returns the state of a given control (pressed or unpressed).
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

**1** if the control is pressed; otherwise, **0**.
## int GetStateByName ( string name )

Returns the state of a given control (pressed or unpressed) by the control state name.
### Arguments

- *string* **name** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

**1** if the control is pressed; otherwise, **0**.
## string GetStateName ( int state )

Returns the name of a given control state as a string.
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

Name of the control state.
## int ClearState ( int state )

Returns a control state and clears it to **0** (not pressed). This function allows to handle control only once even if it is kept pressed over several frames.
### Arguments

- *int* **state** - Control state (one of *[CONTROLS_STATE_*](#STATE_AUX_0)* variables).

### Return value

State of the given control: 1 if the control is pressed; otherwise, 0.
## bool SaveState ( Stream stream )

Saves controls settings into the stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int)* methods:


```csharp
// Get the instance of default engine controls and set its state
Controls controls = new engine.Controls();
controls.MouseDX = 5.0f;

// save state
Blob blob_state = new Blob();
controls.SaveState(blob_state);

// change the node state
controls.MouseDX = 1.0f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
controls.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - The stream to save controls data.

### Return value

true if the controls settings are saved successfully; otherwise, false.
## bool RestoreState ( Stream stream )

Restores controls settings from the stream.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```csharp
// Get the instance of default engine controls and set its state
Controls controls = new engine.Controls();
controls.MouseDX = 5.0f;

// save state
Blob blob_state = new Blob();
controls.SaveState(blob_state);

// change the node state
controls.MouseDX = 1.0f;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
controls.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - The stream to save controls data.

### Return value

true if the controls settings are restored successfully; otherwise, false.
