# Unigine::Input Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The Input class contains functions for simple manual handling of user inputs using a keyboard, a mouse or a gamepad.


This class represents a singleton of the [Engine](../../../api/library/engine/class.engine_usc.md) class and can be accessed via the following way:

```cpp
engine.input
```


### See Also


- The [Input System](../../...md) article
- A set of C++ samples (`<SAMPLES_PROJECT_PATH>/source/input_controls/`)
- A set of C# Component samples (`<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/input_controls/`)


### Usage Examples


The following example shows a way to move and rotate a node by using the Input class:

```cpp
int update() {
	float move_speed = 1.0f;
	float turn_speed = 5.0f;

	if (engine.console.isActive())
		return;

	vec3 direction = node.getWorldDirection(AXIS_Y);
	if (engine.input.isKeyPressed(INPUT_KEY_UP) || engine.input.isKeyPressed(INPUT_KEY_W))
	{
		node.setWorldPosition(node.getWorldPosition() + direction * move_speed * engine.game.getIFps());
	}

	if (engine.input.isKeyPressed(INPUT_KEY_DOWN) || engine.input.isKeyPressed(INPUT_KEY_S))
	{
		node.setWorldPosition(node.getWorldPosition() - direction * move_speed * engine.game.getIFps());
	}

	if (engine.input.isKeyPressed(INPUT_KEY_LEFT) || engine.input.isKeyPressed(INPUT_KEY_A))
	{
		node.rotate(0.0f, 0.0f, turn_speed * engine.game.getIFps());
	}

	if (engine.input.isKeyPressed(INPUT_KEY_RIGHT) || engine.input.isKeyPressed(INPUT_KEY_D))
	{
		node.rotate(0.0f, 0.0f, -turn_speed * engine.game.getIFps());
	}

	return 1;
}

```


## Input Class

### Members

## void setIMEEnabled ( int imeenabled )

Sets a new value indicating if the system IME (Input Method Editor, used for composed text input such as CJK) is enabled. When enabled, the OS can open its composition and candidate window, and the engine receives *[text editing](../../../api/library/controls/class.inputeventtextediting_usc.md)* (preedit) events while the user composes text. Disabled by default.
### Arguments

- *int* **imeenabled** - The IME text composition

## int isIMEEnabled () const

Returns the current value indicating if the system IME (Input Method Editor, used for composed text input such as CJK) is enabled. When enabled, the OS can open its composition and candidate window, and the engine receives *[text editing](../../../api/library/controls/class.inputeventtextediting_usc.md)* (preedit) events while the user composes text. Disabled by default.
### Return value

Current IME text composition
## int getNumJoysticks () const

Returns the current number of joystick slots. A slot is created for every joystick that has been connected at least once and is never removed, so this value does not decrease when a joystick is unplugged. Use *[engine.inputjoystick.isAvailable()()](../../../api/library/controls/class.inputjoystick_usc.md#isAvailable_int)* to check whether a slot currently has a joystick behind it.
### Return value

Current number of joystick slots.
## int getNumGamePads () const

Returns the current number of gamepad slots. A slot is created for every gamepad that has been connected at least once and is never removed, so this value does not decrease when a gamepad is unplugged. Use *[engine.inputgamepad.isAvailable()()](../../../api/library/controls/class.inputgamepad_usc.md#isAvailable_int)* to check whether a slot currently has a gamepad behind it.
### Return value

Current number of gamepad slots.
## int getMouseWheelHorizontal () const

Returns the current horizontal mouse scroll value. Negative values correspond to scrolling leftwards; positive values correspond to scrolling rightwards; the value is zero when the wheel is not scrolled horizontally. All horizontal scroll events received during the frame are summed up, so the magnitude is not limited to 1.
### Return value

Current horizontal mouse scroll value.
## int getMouseWheel () const

Returns the current mouse scroll value. Negative values correspond to scrolling downwards; positive values correspond to scrolling upwards; the value is zero when the mouse wheel is not scrolled. All scroll events received during the frame are summed up.
### Return value

Current vertical mouse scroll value.
## ivec2 getMouseDeltaPosition () const

Returns the current vector containing screen position change of the mouse pointer along the X and Y axes � the difference between the values in the previous and the current frames.
### Return value

Current vector containing delta values of the mouse cursor position.
## void setMousePosition ( ivec2 position )

Sets a new global coordinates of the mouse cursor. While a mouse button event is being processed, the cursor position at the moment of that event is returned; otherwise, the position at the beginning of the frame is returned. To get the cursor position during another type of event, get this event (for example *[getKeyEvent()()](../../...md#getKeyEvent_int_InputEventKeyboard)*) and read the position stored inside it. Use *[getForceMousePosition()()](../../...md#getForceMousePosition_ivec2)* to query the current position from the OS instead of this frame-bound value.
### Arguments

- *ivec2* **position** - The global coordinates of the mouse cursor.

## ivec2 getMousePosition () const

Returns the current global coordinates of the mouse cursor. While a mouse button event is being processed, the cursor position at the moment of that event is returned; otherwise, the position at the beginning of the frame is returned. To get the cursor position during another type of event, get this event (for example *[getKeyEvent()()](../../...md#getKeyEvent_int_InputEventKeyboard)*) and read the position stored inside it. Use *[getForceMousePosition()()](../../...md#getForceMousePosition_ivec2)* to query the current position from the OS instead of this frame-bound value.
### Return value

Current global coordinates of the mouse cursor.
## void setMouseHandle ( int handle )

Sets a new mouse behavior mode, one of the [MOUSE_HANDLE](#MOUSE_HANDLE) values.
### Arguments

- *int* **handle** - The mouse behavior mode, one of the [MOUSE_HANDLE](#MOUSE_HANDLE) values.

## int getMouseHandle () const

Returns the current mouse behavior mode, one of the [MOUSE_HANDLE](#MOUSE_HANDLE) values.
### Return value

Current mouse behavior mode, one of the [MOUSE_HANDLE](#MOUSE_HANDLE) values.
## void setMouseCursorNeedUpdate ( int update )

Sets a new value indicating that changes were made to the cursor (it was shown, hidden, changed to system, or anything else) and it has to be updated. Suppose the cursor was modified, for example, by the *Interface* plugin. After closing the plugin's window the cursor shall not return to its previous state because SDL doesn't even know about the changes. You can use this flag to signalize, that mouse cursor must be updated.
### Arguments

- *int* **update** - The changes were made to the cursor (it was shown, hidden, changed to system, or anything else) and it has to be updated

## int isMouseCursorNeedUpdate () const

Returns the current value indicating that changes were made to the cursor (it was shown, hidden, changed to system, or anything else) and it has to be updated. Suppose the cursor was modified, for example, by the *Interface* plugin. After closing the plugin's window the cursor shall not return to its previous state because SDL doesn't even know about the changes. You can use this flag to signalize, that mouse cursor must be updated.
### Return value

Current changes were made to the cursor (it was shown, hidden, changed to system, or anything else) and it has to be updated
## void setMouseCursorSystem ( int system )

Sets a new value indicating if the OS mouse pointer is displayed.
### Arguments

- *int* **system** - The value indicating if the OS mouse pointer is displayed

## int isMouseCursorSystem () const

Returns the current value indicating if the OS mouse pointer is displayed.
### Return value

Current value indicating if the OS mouse pointer is displayed
## void setMouseCursorHide ( int hide )

Sets a new value indicating if the mouse cursor is hidden in the current frame.
### Arguments

- *int* **hide** - The value indicating if the mouse cursor is hidden in the current frame

## int isMouseCursorHide () const

Returns the current value indicating if the mouse cursor is hidden in the current frame.
### Return value

Current value indicating if the mouse cursor is hidden in the current frame
## void setMouseGrab ( int grab )

Sets a new value indicating if the mouse pointer is bound to the application window (can't leave it).
### Arguments

- *int* **grab** - The value indicating if the mouse pointer is bound to the application window

## int isMouseGrab () const

Returns the current value indicating if the mouse pointer is bound to the application window (can't leave it).
### Return value

Current value indicating if the mouse pointer is bound to the application window
## void setClipboard ( )

Sets a new contents of the system clipboard.
### Arguments

- **clipboard** - The contents of the system clipboard.

## const char * getClipboard () const

Returns the current contents of the system clipboard.
### Return value

Current contents of the system clipboard.
## bool isEmptyClipboard () const

Returns the current value indicating if the clipboard is empty.
### Return value

**true** if the clipboard is empty; otherwise **false**.
## getMouseDeltaRaw () const

Returns the current raw mouse movement for the current frame, as reported by the device. Unlike [MouseDeltaPosition](#MouseDeltaPosition), which tracks the screen cursor, this value comes from the raw input of the OS: it is not affected by pointer acceleration or desktop sensitivity settings and is not limited by the screen borders. For a mouse reporting relative motion the units are device counts, whose size depends on the mouse DPI; for a device reporting absolute coordinates the units are screen pixels. All raw motion events received during the frame are summed up.
### Return value

Current raw mouse movement for the current frame, as reported by the device (not the screen cursor movement).
## getVRControllerTreadmill () const

Returns the current treadmill VR controller.
### Return value

Current treadmill VR controller.
## getVRControllerRight () const

Returns the current right-hand VR controller.
### Return value

Current right-hand VR controller.
## getVRControllerLeft () const

Returns the current left-hand VR controller.
### Return value

Current left-hand VR controller.
## getVRHead () const

Returns the current head VR controller.
### Return value

Current head VR controller.
## int getNumVRDevices () const

Returns the current number of all VR devices.
### Return value

Current number of all VR devices.
## static getEventImmediateInput () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventJoyPovMotion () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventJoyAxisMotion () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventJoyButtonUp () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventJoyButtonDown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventJoyDisconnected () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventJoyConnected () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventVrDeviceAxisMotion () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventVrDeviceButtonTouchUp () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventVrDeviceButtonTouchDown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventVrDeviceButtonUp () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventVrDeviceButtonDown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventVrDeviceDisconnected () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventVrDeviceConnected () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int, int, int> getEventGamepadTouchMotion () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int, int, int> getEventGamepadTouchUp () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int, int, int> getEventGamepadTouchDown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventGamepadAxisMotion () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventGamepadButtonUp () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventGamepadButtonDown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventGamepadDisconnected () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventGamepadConnected () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventTouchMotion () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventTouchUp () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventTouchDown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventTextPress () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventKeyRepeat () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventKeyUp () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventKeyDown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventMouseMotion () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventMouseWheelHorizontal () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventMouseWheel () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventMouseUp () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventMouseDown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventTextEditing () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## InputGamePad engine.input. getGamePad ( int num )

Returns the gamepad in the given slot. A newly connected gamepad reuses the lowest free slot, so the same index can refer to a different device after a reconnection.
### Arguments

- *int* **num** - Gamepad slot index, from 0 to [NumGamePads](#NumGamePads)�- 1. The index is not checked: a value outside this range results in undefined behavior.

### Return value

[InputGamepad](../../../api/library/controls/class.inputgamepad_usc.md) object.
## InputJoystick engine.input. getJoystick ( int num )

Returns the joystick in the given slot. A newly connected joystick reuses the lowest free slot, so the same index can refer to a different device after a reconnection.
### Arguments

- *int* **num** - Joystick slot index, from 0 to [NumJoysticks](#NumJoysticks)�- 1. The index is not checked: a value outside this range results in undefined behavior.

### Return value

[InputJoystick](../../../api/library/controls/class.inputjoystick_usc.md) object.
## int engine.input. isKeyPressed ( int key )

Returns a value indicating if the given key is pressed. Check this value to perform continuous actions.
```cpp
if (engine.input.isKeyPressed(INPUT_KEY_ENTER)) {
	log.message("enter key is held down\n");
}

```


### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

**1** if the key is pressed; otherwise, **0**.
## int engine.input. isKeyDown ( int key )

Returns a value indicating if the given key was pressed during the current frame. Check this value to perform one-time actions on pressing a key.
```cpp
if (engine.input.isKeyDown(INPUT_KEY_KEY_SPACE)) {
	log.message("space key was pressed\n");
}

```


### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

1 during the first frame when the key was pressed, 0 for the following ones until it is released and pressed again.
## int engine.input. isKeyUp ( int key )

Returns a value indicating if the given key was released during the current frame. Check this value to perform one-time actions on releasing a key.
```cpp
if (engine.input.isKeyUp(INPUT_KEY_F)) {
	log.message("f key was released\n");
}

```


### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

**1** during the first frame when the key was released; otherwise, **0**.
## int engine.input. isMouseButtonPressed ( int button )

Returns a value indicating if the given mouse button is pressed. Check this value to perform continuous actions.
```cpp
if (engine.input.isMouseButtonPressed(INPUT_MOUSE_BUTTON_LEFT)) {
	log.message("left mouse button is held down\n");
}

```


### Arguments

- *int* **button** - One of the [INPUT_MOUSE_BUTTON_](#MOUSE_BUTTON_LEFT) codes.

### Return value

1 if the mouse button is pressed; otherwise, 0.
## int engine.input. isMouseButtonDown ( int button )

Returns a value indicating if the given mouse button was pressed during the current frame. Check this value to perform one-time actions on pressing a mouse button.
```cpp
if (engine.input.isMouseButtonDown(INPUT_MOUSE_BUTTON_LEFT)) {
	log.message("left mouse button was pressed\n");
}

```


### Arguments

- *int* **button** - One of the [INPUT_MOUSE_BUTTON_](#MOUSE_BUTTON_LEFT) codes.

### Return value

1 during the first frame when the mouse button was released; otherwise, 0.
## int engine.input. isMouseButtonUp ( int button )

Returns a value indicating if the given mouse button was released during the current frame. Check this value to perform one-time actions on releasing a mouse button.
```cpp
if (engine.input.isMouseButtonUp(INPUT_MOUSE_BUTTON_LEFT)) {
	log.message("left mouse button was released\n");
}

```


### Arguments

- *int* **button** - One of the [INPUT_MOUSE_BUTTON_](#MOUSE_BUTTON_LEFT) codes.

### Return value

1 during the first frame when the mouse button was released; otherwise, 0.
## int engine.input. isTouchPressed ( int index )

Returns a value indicating if the touchscreen is pressed by the finger.
### Arguments

- *int* **index** - Touch input index, from 0 to [NUM_TOUCHES](#NUM_TOUCHES)�- 1. The index is not checked: a value outside this range results in undefined behavior.

### Return value

**1** if the touchscreen is pressed; otherwise, **0**.
## int engine.input. isTouchDown ( int index )

Returns a value indicating if the given touch was pressed during the current frame.
### Arguments

- *int* **index** - Touch input index, from 0 to [NUM_TOUCHES](#NUM_TOUCHES)�- 1. The index is not checked: a value outside this range results in undefined behavior.

### Return value

**1** if the touchscreen is pressed during the current frame; otherwise, **0**.
## int engine.input. isTouchUp ( int index )

Returns a value indicating if the given touch ended during the current frame. It is true for one frame only, in the same way as *[isTouchDown()()](../../...md#isTouchDown_int_int)* reports the beginning of a touch.
### Arguments

- *int* **index** - Touch input index, from 0 to [NUM_TOUCHES](#NUM_TOUCHES)�- 1. The index is not checked: a value outside this range results in undefined behavior.

### Return value

**1** during the first frame when the touch was released; otherwise, **0**.
## ivec2 engine.input. getTouchPosition ( int index )

Returns the position of the given touch in global (desktop) coordinates, as of the touch event processed in the current frame.
### Arguments

- *int* **index** - Touch input index, from 0 to [NUM_TOUCHES](#NUM_TOUCHES)�- 1. The index is not checked: a value outside this range results in undefined behavior.

### Return value

The touch position.
## ivec2 engine.input. getTouchDelta ( int index )

Returns a vector containing screen position change of the touch along the X and Y axes � the difference between the values in the previous and the current frames.
### Arguments

- *int* **index** - Touch input index, from 0 to [NUM_TOUCHES](#NUM_TOUCHES)�- 1. The index is not checked: a value outside this range results in undefined behavior.

### Return value

The touch position delta.
## InputEventTouch engine.input. getTouchEvent ( int index )

Returns the touch input event currently being processed for the given touch index. One event is taken from the queue per frame; use *[getTouchEvents()()](../../...md#getTouchEvents_int_VECInputEventTouch_int)* to get all events received for this touch.
### Arguments

- *int* **index** - Touch input index, from 0 to [NUM_TOUCHES](#NUM_TOUCHES)�- 1. The index is not checked: a value outside this range results in undefined behavior.

### Return value

Touch input event, or null if there are no events for the specified touch in the current frame.
## InputEventKeyboard engine.input. getKeyEvent ( int key )

Returns the keyboard event currently being processed for the given key. One event is taken from the queue per frame; use *[getKeyEvents()()](../../...md#getKeyEvents_int_VECInputEventKeyboard_int)* to get all events received for this key.
### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

Keyboard input event, or null if there are no events for the specified key in the current frame.
## string engine.input. getKeyName ( int key )

Returns the name of the given key, ESC or LEFT_SHIFT for example. The names are the constant names without the prefix (KEY_ESC gives ESC) and do not depend on the keyboard layout; for the layout-dependent label use *[getKeyLocalName()()](../../...md#getKeyLocalName_int_cstr)*.
### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

Key name.
## int engine.input. getKeyByName ( string name )

Returns the key with the given name � the reverse of *[getKeyName()()](../../...md#getKeyName_int_cstr)*. [KEY_UNKNOWN](#KEY_UNKNOWN) is returned if no key has this name.
### Arguments

- *string* **name** - Key name.

### Return value

One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.
## InputEventMouseButton engine.input. getMouseButtonEvent ( int button )

Returns the mouse button event currently being processed for the given button. One event is taken from the queue per frame; use *[getMouseButtonEvents()()](../../...md#getMouseButtonEvents_int_VECInputEventMouseButton_int)* to get all events received for this button.
### Arguments

- *int* **button** - One of the [INPUT_MOUSE_BUTTON_](#MOUSE_BUTTON_LEFT) codes.

### Return value

Mouse button input event, or null if there are no events for the specified button in the current frame.
## string engine.input. getMouseButtonName ( int button )

Returns the name of the given mouse button, LEFT or AUX_0 for example.
### Arguments

- *int* **button** - One of the [INPUT_MOUSE_BUTTON_](#MOUSE_BUTTON_LEFT) codes.

### Return value

Mouse button name.
## int engine.input. getMouseButtonByName ( string name )

Returns the mouse button with the given name � the reverse of *[getMouseButtonName()()](../../...md#getMouseButtonName_int_cstr)*. [MOUSE_BUTTON_UNKNOWN](#MOUSE_BUTTON_UNKNOWN) is returned if no button has this name.
### Arguments

- *string* **name** - Mouse button name.

### Return value

One of the [INPUT_MOUSE_BUTTON_](#MOUSE_BUTTON_LEFT) codes.
## void engine.input. sendEvent ( InputEvent e )

Dispatches an input event to the Engine. The Engine takes ownership of the event: it is deleted automatically after it leaves the events buffer, which stores the last 60 frames. Do not keep or reuse the object after this call, and do not send back an event obtained from *[getEventsBuffer()()](../../...md#getEventsBuffer_int_VECInputEvent_int)* - copy the data you need and build a new event instead.
### Arguments

- *[InputEvent](../../../api/library/controls/class.inputevent_usc.md)* **e** - Input event.

## void engine.input. setEventsFilter ( IntPtr func )

Sets a callback function to be executed on receiving input events. This input event filter enables you to reject certain input events for the Engine and get necessary information on all input events.
### Arguments

- *IntPtr* **func** - Input event callback.

## int engine.input. isModifierEnabled ( int modifier )

Returns a value indicating if the given modifier is currently active � a modifier key held down, or a lock such as Caps Lock switched on. The state is queried from the OS.
### Arguments

- *int* **modifier** - One of the [INPUT_MODIFIER_](#MODIFIER_LEFT_SHIFT) codes.

### Return value

**1** if the modifier is enabled; otherwise, **0**.
## unsigned int engine.input. keyToUnicode ( int key )

Returns the Unicode character produced by the given key on the current keyboard layout. 0 is returned if the key has no printable symbol � *[isKeyText()()](../../...md#isKeyText_int_int)* is a shortcut for this check.
### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

Unicode character code, or 0 if the key has no printable symbol.
## int engine.input. unicodeToKey ( unsigned int unicode )

Returns the key that produces the given Unicode character on the current keyboard layout � the inverse of *[keyToUnicode()()](../../...md#keyToUnicode_int_uint)*. KEY_UNKNOWN is returned if the character is 0 or cannot be produced by the current layout. Keys whose symbol is not consistent across platforms (Esc, Print Screen, Backspace, Tab, Enter, Menu, numpad - and +) also resolve to KEY_UNKNOWN.
### Arguments

- *unsigned int* **unicode** - Unicode character code.

### Return value

One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.
## void engine.input. setMouseCursorSkinCustom ( Image image )

Sets a custom image to be used for the mouse cursor.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image containing pointer shapes to be set for the mouse cursor (e.g., select, move, resize, etc.).

## void engine.input. setMouseCursorSkinSystem ( )

Sets the current OS cursor skin (pointer shapes like select, move, resize, etc.).
## void engine.input. setMouseCursorSkinDefault ( )

Sets the default Engine cursor skin (pointer shapes like select, move, resize, etc.).
## void engine.input. setMouseCursorCustom ( Image image , int x = 0 , int y = 0 )

Sets a custom image for the OS mouse cursor. The image must be of the square size and *RGBA8* format.
```cpp
engine.app.setMouseCursorCustom(new Image("textures/my_cursor.png"));
// show the OS mouse pointer
engine.input.setMouseCursorSystem(1);

```


### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Cursor image to be set.
- *int* **x** - X coordinate of the cursor's hot spot.
- *int* **y** - Y coordinate of the cursor's hot spot.

## void engine.input. clearMouseCursorCustom ( )

Clears the custom mouse cursor set via the *[setMouseCursorCustom()()](../../...md#setMouseCursorCustom_Image_int_int_void)* method.
## void engine.input. updateMouseCursor ( )

Updates the mouse cursor. This method should be called after making changes to the mouse cursor to apply them all together. After calling this method the cursor shall be updated in the next frame.
## string engine.input. getKeyLocalName ( int key )

Returns the name for the specified key taken from the currently selected keyboard layout.
> **Notice:** The returned value is affected by the modifier such as Shift.


### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

Localized name for the specified key.
## ivec2 engine.input. getForceMousePosition ( )

Returns the mouse cursor position queried from the OS at the moment of the call. Unlike [MousePosition](#MousePosition), which is captured once at the beginning of the frame and reflects the position stored in the processed input event, this value is always up to date.
### Return value

Current mouse cursor position in global (desktop) coordinates.
## int engine.input. isKeyText ( int key )

Returns a value indicating if the given key has a corresponding printable symbol (current Num Lock state is taken into account). For example, pressing 2 on the numpad with *Num Lock* enabled produces "2", while with disabled *Num Lock* the same key acts as a down arrow. Keys like *Esc, PrintScreen, BackSpace* do not produce any printable symbol at all.
### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

**1** if the key value is a symbol; otherwise, **0**.
## string engine.input. getModifierName ( int modifier )

Returns the name of the given modifier, LEFT_SHIFT or CAPS_LOCK for example.
### Arguments

- *int* **modifier** - Scancode of the modifier.

### Return value

Key name of the modifier.
## int engine.input. getModifierByName ( string name )

Returns the modifier with the given name � the reverse of *[getModifierName()()](../../...md#getModifierName_int_cstr)*. [MODIFIER_NONE](#MODIFIER_NONE) is returned if no modifier has this name.
### Arguments

- *string* **name** - Key name of the modifier.

### Return value

Scancode of the modifier.
## InputVRDevice engine.input. getVRDevice ( int num )

Returns the VR device in the given slot. A slot is created for every VR device that has been connected at least once and is never removed, so the same index keeps referring to the same device.
### Arguments

- *int* **num** - VR device slot index, from 0 to [NumVRDevices](#NumVRDevices)�- 1. The index is not checked: a value outside this range results in undefined behavior.

### Return value

VR device.
## void engine.input. setIMETextInputRect ( int position_x , int position_y , int width , int height )

Tells the operating system where the text caret or edit area is located, so that the IME composition and candidate window can be positioned next to it. Has no effect if text input is not currently active.
### Arguments

- *int* **position_x** - Horizontal position of the top-left corner of the text input rectangle, in render pixels relative to the engine window.
- *int* **position_y** - Vertical position of the top-left corner of the text input rectangle, in render pixels relative to the engine window.
- *int* **width** - Width of the text input rectangle, in pixels.
- *int* **height** - Height of the text input rectangle, in pixels.
