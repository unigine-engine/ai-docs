# Unigine::Input Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The Input class contains functions for simple manual handling of user inputs using a keyboard, a mouse or a gamepad.


This class represents a singleton of the [Engine](../../../api/library/engine/class.engine_usc.md) class and can be accessed via the following way:

```cpp
engine.input
```


### See Also


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

Returns the current number of joysticks.
### Return value

Current number of joysticks.
## int getNumGamePads () const

Returns the current number of all gamepads.
### Return value

Current number of all gamepads.
## int getMouseWheelHorizontal () const

Returns the current horizontal mouse scroll value.
### Return value

Current horizontal mouse scroll value in the [-1;1] range.
## int getMouseWheel () const

Returns the current vertical mouse scroll value.
### Return value

Current mouse scroll value. Negative values correspond to scrolling downwards; positive values correspond to scrolling upwards; the value is zero when the mouse wheel is not scrolled.
## ivec2 getMouseDeltaPosition () const

Returns the current vector containing delta values of the mouse cursor position.
### Return value

Current vector containing screen position change of the mouse pointer along the X and Y axes � the difference between the values in the previous and the current frames.
## void setMousePosition ( ivec2 position )

Sets a new vector containing integer values of the mouse cursor position.
### Arguments

- *ivec2* **position** - The Returns a vector containing the global coordinates of the mouse cursor. In case of a mouse button event, the cursor position at the moment of the processed event is returned. In case of no such event, the mouse position at the beginning of the frame is returned. To get the cursor position during another type of event, get this event (for example [getKeyEvent()](#getKeyEvent_int_InputEventKeyboard)) and get the cursor position stored inside it.

## ivec2 getMousePosition () const

Returns the current vector containing integer values of the mouse cursor position.
### Return value

Current Returns a vector containing the global coordinates of the mouse cursor. In case of a mouse button event, the cursor position at the moment of the processed event is returned. In case of no such event, the mouse position at the beginning of the frame is returned. To get the cursor position during another type of event, get this event (for example [getKeyEvent()](#getKeyEvent_int_InputEventKeyboard)) and get the cursor position stored inside it.
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

Returns the current change in the absolute mouse position (not the screen cursor), dots per inch.
### Return value

Current change in the absolute mouse position (not the screen cursor), dots per inch.
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

Returns a gamepad of the given index.
### Arguments

- *int* **num** - Gamepad index.

### Return value

[InputGamepad](../../../api/library/controls/class.inputgamepad_usc.md) object.
## InputJoystick engine.input. getJoystick ( int num )

Returns a joystick with the given index.
### Arguments

- *int* **num** - Joystick index.

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

- *int* **index** - Touch input index.

### Return value

**1** if the touchscreen is pressed; otherwise, **0**.
## int engine.input. isTouchDown ( int index )

Returns a value indicating if the given touch was pressed during the current frame.
### Arguments

- *int* **index** - Touch input index.

### Return value

**1** if the touchscreen is pressed during the current frame; otherwise, **0**.
## int engine.input. isTouchUp ( int index )

Returns a value indicating if the given touch was released.
### Arguments

- *int* **index** - Touch input index.

### Return value

**1** during the first frame when the touch was released; otherwise, **0**.
## ivec2 engine.input. getTouchPosition ( int index )

Returns a vector containing integer values of touch position.
### Arguments

- *int* **index** - Touch input index.

### Return value

The touch position.
## ivec2 engine.input. getTouchDelta ( int index )

Returns a vector containing screen position change of the touch along the X and Y axes � the difference between the values in the previous and the current frames.
### Arguments

- *int* **index** - Touch input index.

### Return value

The touch position delta.
## InputEventTouch engine.input. getTouchEvent ( int index )

Returns the action cast to the touch event.
### Arguments

- *int* **index** - Touch input index.

### Return value

Touch input event.
## InputEventKeyboard engine.input. getKeyEvent ( int key )

Returns the currently processed keyboard input event.
### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

Keyboard input event, or null if there are no events for the specified key in the current frame.
## string engine.input. getKeyName ( int key )

Returns the specified key name.
### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

Key name.
## int engine.input. getKeyByName ( string name )

Returns the key by its name.
### Arguments

- *string* **name** - Key name.

### Return value

One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.
## InputEventMouseButton engine.input. getMouseButtonEvent ( int button )

Returns the mouse motion input event for the specified button.
### Arguments

- *int* **button** - One of the [INPUT_MOUSE_BUTTON_](#MOUSE_BUTTON_LEFT) codes.

### Return value

Mouse motion input event.
## string engine.input. getMouseButtonName ( int button )

Returns the mouse button name.
### Arguments

- *int* **button** - One of the [INPUT_MOUSE_BUTTON_](#MOUSE_BUTTON_LEFT) codes.

### Return value

Mouse button name.
## int engine.input. getMouseButtonByName ( string name )

Returns the mouse button by its name.
### Arguments

- *string* **name** - Mouse button name.

### Return value

One of the [INPUT_MOUSE_BUTTON_](#MOUSE_BUTTON_LEFT) codes.
## void engine.input. sendEvent ( InputEvent e )

Creates a user event and dispatches it to the Engine.
### Arguments

- *[InputEvent](../../../api/library/controls/class.inputevent_usc.md)* **e** - Input event.

## void engine.input. setEventsFilter ( IntPtr func )

Sets a callback function to be executed on receiving input events. This input event filter enables you to reject certain input events for the Engine and get necessary information on all input events.
### Arguments

- *IntPtr* **func** - Input event callback.

## int engine.input. isModifierEnabled ( int modifier )

Returns the value indicating if the specified modifier is enabled.
### Arguments

- *int* **modifier** - One of the [INPUT_MODIFIER_](#MODIFIER_LEFT_SHIFT) codes.

### Return value

**1** if the modifier is enabled; otherwise, **0**.
## unsigned int engine.input. keyToUnicode ( int key )

Returns the specified key transformed to unicode.
### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

Unicode symbol.
## int engine.input. unicodeToKey ( unsigned int unicode )

Returns the specified key transformed to unicode.
### Arguments

- *unsigned int* **unicode** - Unicode symbol.

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

Clears the custom mouse cursor set via the [setMouseCursorCustom()](#setMouseCursorCustom_Image_int_int_void) method.
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

Returns the absolute mouse position obtained from the OS.
### Return value

The absolute mouse position.
## int engine.input. isKeyText ( int key )

Returns a value indicating if the given key has a corresponding printable symbol (current Num Lock state is taken into account). For example, pressing 2 on the numpad with *Num Lock* enabled produces "2", while with disabled *Num Lock* the same key acts as a down arrow. Keys like *Esc, PrintScreen, BackSpace* do not produce any printable symbol at all.
### Arguments

- *int* **key** - One of the [INPUT_KEY_](#KEY_UNKNOWN) codes.

### Return value

**1** if the key value is a symbol; otherwise, **0**.
## string engine.input. getModifierName ( int modifier )

Returns the name of the key modifier by its scancode.
### Arguments

- *int* **modifier** - Scancode of the modifier.

### Return value

Key name of the modifier.
## int engine.input. getModifierByName ( string name )

Returns the scancode of the key modifier by its name.
### Arguments

- *string* **name** - Key name of the modifier.

### Return value

Scancode of the modifier.
## InputVRDevice engine.input. getVRDevice ( int num )

Returns the VR device by its number.
### Arguments

- *int* **num** - Number of the VR device.

### Return value

VR device.
## void engine.input. setIMETextInputRect ( int position_x , int position_y , int width , int height )

Tells the operating system where the text caret or edit area is located, so that the IME composition and candidate window can be positioned next to it. Has no effect if text input is not currently active.
### Arguments

- *int* **position_x** - Horizontal position of the top-left corner of the text input rectangle, in render pixels relative to the engine window.
- *int* **position_y** - Vertical position of the top-left corner of the text input rectangle, in render pixels relative to the engine window.
- *int* **width** - Width of the text input rectangle, in pixels.
- *int* **height** - Height of the text input rectangle, in pixels.
