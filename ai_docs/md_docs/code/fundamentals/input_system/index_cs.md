# Input System (CS)


The **Input System** gives you access to every input device through a single class - keyboard, mouse, gamepads, joysticks, VR controllers, and touch devices. It also gives access to the system clipboard.


It lets you do the following:


- Poll the current state of a device - whether a key is pressed, where the cursor is, and how far a trigger is pressed.
- Subscribe to input events and react to them as they arrive.
- Filter incoming events before the Engine processes them.
- Send your own events to simulate input.


This covers everything from a simple "WASD + mouse" control scheme to custom processing of the raw events of every connected device.


## Input Events


Devices do not send input to your code directly. Every device reports input by creating an **input event** - an object derived from **[InputEvent](../../../api/library/controls/class.inputevent_cs.md)**, such as **InputEventKeyboard** or **InputEventMouseButton**. Your own code can create the same events.


All events enter the Input System through a single method - **[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)**. Devices call it internally, and you can call it yourself to [simulate input](#custom_events). It can be called from any thread.


No matter where an event comes from, it follows the same path:


![The path an input event takes from a device to your code](input_pipeline.svg)

*Immediate Input bypasses the events buffer and can be triggered in any thread*


1. An event enters the system through **Input.SendEvent()**.
2. The Engine checks the [input focus](#focus). While input is out of focus and [background update](../../../code/console/index.md#background_update) is disabled, events are discarded - except gamepad and joystick connection events, which are always accepted.
3. The Engine discards redundant mouse and keyboard events: a mouse press when the button is already pressed, and a mouse or key release when the control is not pressed. Key presses always pass through, which is what makes auto-repeat work. Events from other devices are not checked for this.
4. The [events filter](#events_filter) can reject or modify the event.
5. The [Immediate Input](#immediate_input) event is triggered right away.
6. The event is stored in the [events buffer](#events_buffer). For the left mouse button, the Engine also generates an extra *MOUSE_BUTTON_DCLICK* event when two clicks fall within 400 milliseconds and 4 pixels of each other. These two thresholds are fixed and cannot be changed. Process the event in the same way as an event of any other mouse button.
7. On the next Engine update, the events buffer is processed on the [main thread](../../../code/fundamentals/thread_system/index.md#thread_main): device states are updated and input events are triggered.
8. Your code polls the states and handles the events.


The Engine performs this whole sequence automatically. However, you can step in when you want to [filter events](#events_filter), [react with minimal latency](#immediate_input), or [simulate input](#custom_events).


## Input Focus


Input events are processed only while input is **in focus**.


By default, input is in focus while at least one application window is focused. If input loses focus and [background update](../../../code/console/index.md#background_update) is disabled, all incoming events are discarded. Gamepad and joystick connection events are the exception: connecting and disconnecting a device skips the focus check and is always accepted.


Input also loses focus while a system dialog is open. Such a dialog is modal: it takes over the input until the user closes it. This applies to the following dialogs:


- A message, warning, or error dialog - **[WindowManager.DialogMessage()](../../../api/library/gui/class.windowmanager_cs.md#dialogMessage_cstr_cstr_int)**, **[WindowManager.DialogWarning()](../../../api/library/gui/class.windowmanager_cs.md#dialogWarning_cstr_cstr_int)**, **[WindowManager.DialogError()](../../../api/library/gui/class.windowmanager_cs.md#dialogError_cstr_cstr_int)**.
- A system dialog - **[WindowManager.ShowSystemDialog()](../../../api/library/gui/class.windowmanager_cs.md#showSystemDialog_SystemDialog_int)**.
- A file or folder dialog - **[WindowManager.DialogOpenFile()](../../../api/library/gui/class.windowmanager_cs.md#dialogOpenFile_cstr_cstr_cstr)**, **[WindowManager.DialogOpenFiles()](../../../api/library/gui/class.windowmanager_cs.md#dialogOpenFiles_cstr_cstr_VECString)**, **[WindowManager.DialogOpenFolder()](../../../api/library/gui/class.windowmanager_cs.md#dialogOpenFolder_cstr_cstr)**, **[WindowManager.DialogSaveFile()](../../../api/library/gui/class.windowmanager_cs.md#dialogSaveFile_cstr_cstr_cstr)**.


These calls block until the dialog is closed. Input regains focus afterwards, if it was in focus before the dialog opened.


When input loses focus, the Engine generates release events for everything currently held down: mouse buttons, keys, gamepad buttons and touches, joystick buttons, and VR buttons. Both the devices and your code receive these events, so no control remains pressed while the application runs in the background.


When input regains focus, the cursor position is read from the system again, and mouse deltas and wheel values are reset to zero. This prevents a large jump in the mouse delta in the first frame after the application regains focus.


> **Notice:** If you implement your own *[CustomSystemProxy](../../../api/library/engine/class.customsystemproxy_cs.md)*, you can define your own focus conditions for the Input System.


## From Events to Device State


Events that pass the checks are stored in a buffer and processed during the next Engine update. The effect of an event on the device state depends on the event type.


| How it is applied | Events |
|---|---|
| **One event per [frame](../../../code/fundamentals/execution_sequence/main_loop.md).** The Engine keeps a separate queue for each individual control and takes one event from it every frame. | - Key press and release - Mouse button press and release - Touch down and up - Gamepad button press and release, touchpad finger down and up - Joystick button press and release, POV hat motion - VR button press and release, VR button touch |
| **Summed over the frame.** All values received during the frame are summed. | - Mouse motion delta - Mouse wheel - Touch delta - Gamepad touchpad delta |
| **Last value only.** The device state keeps the last event of the frame. | - Gamepad, joystick, and VR axes - Gamepad accelerometer and gyroscope - Touch position and pressure |
| **Not stored as state.** The Engine sends these events to subscribers only; there is no state to read afterwards. | - Text input and text editing - Key auto-repeat - Device connection and disconnection |


![Events of one frame becoming device state](input_events_buffer.svg)

*Events of one frame for a mouse button and for mouse motion: four presses and releases become four frames of state, while three motion values become one*


The per-control queue exists to prevent lost input. Suppose the user presses and releases a key within a single frame. Without the queue, the frame would only see the final state - key released - and the press would be lost. Applying the press in one frame and the release in the next preserves both.


Buffered input matters whenever fast and precise user actions have to be recognized. A typical example is a quick-time event, where the user must press a specific sequence of keys quickly and accurately.


### Update Order


Buffer processing happens automatically once per frame, before your application logic is updated. The sequence is as follows:


1. The events buffer is updated. The history shifts by one frame, and the events collected since the last update become the events of the current frame.
2. Device states are updated, each kind of event in its own way: queued events are taken one per frame, motion values are summed, and axes keep the last value of the frame.
3. All input events are triggered, except for [Immediate Input](#immediate_input), which has already been triggered.


Devices are updated in a fixed order: touch devices, mouse, keyboard, gamepads, joysticks, and VR devices. GUI input is updated next, and then the events are triggered in the same device order.


After this stage, your code can poll the current state of every device and handle the events it has subscribed to.


### Reading the Buffer Directly


The events buffer stores the history of the **last 60 frames**. Use **[Input.GetEventsBuffer()](../../../api/library/controls/class.input_cs.md#getEventsBuffer_int_VECInputEvent_int)** to get all events of a given frame, where 0 is the current frame and 1 is the previous one. For frames beyond the history depth, the method returns nothing.


Two more methods work with a single key:


- **[Input.GetKeyEvent()](../../../api/library/controls/class.input_cs.md#getKeyEvent_int_InputEventKeyboard)** returns the event applied to the key in the current frame.
- **[Input.GetKeyEvents()](../../../api/library/controls/class.input_cs.md#getKeyEvents_int_VECInputEventKeyboard_int)** returns the whole queue still pending for the key - the events that will be applied in the upcoming frames.


## Reading Device States


In most cases, you need only the current state of a device. Read it from your per-frame update:


```csharp
private void Update()
{
	// movement: true for as long as the key is held
	float moveX = 0.0f;
	float moveY = 0.0f;

	if (Input.IsKeyPressed(Input.KEY.W)) moveY += 1.0f;
	if (Input.IsKeyPressed(Input.KEY.S)) moveY -= 1.0f;
	if (Input.IsKeyPressed(Input.KEY.A)) moveX -= 1.0f;
	if (Input.IsKeyPressed(Input.KEY.D)) moveX += 1.0f;

	// looking around: how far the mouse moved since the previous frame
	ivec2 look = Input.MouseDeltaRaw;

	// a single shot on the frame the button goes down
	if (Input.IsMouseButtonDown(Input.MOUSE_BUTTON.LEFT))
		Log.Message("fire\n");
}

```


[Keys](../../../api/library/controls/class.input_cs.md#isKeyDown_int_int), [mouse buttons](../../../api/library/controls/class.input_cs.md#isMouseButtonDown_int_int), [touches](../../../api/library/controls/class.input_cs.md#isTouchDown_int_int), [gamepad buttons](../../../api/library/controls/class.inputgamepad_cs.md#isButtonDown_int_int), [joystick buttons](../../../api/library/controls/class.inputjoystick_cs.md#isButtonDown_uint_int), and [VR buttons](../../../vr_development/vr_input_cs.md) are all read with the same three methods:


| Method | Returns *true* |
|---|---|
| **Is*Down()** | On the frame the control was pressed. |
| **Is*Pressed()** | Every frame while the control is held. |
| **Is*Up()** | On the frame the control was released. |


> **Notice:** A very short tap is never lost, even if it happens entirely within one frame - see [From Events to Device State](#events_buffer).


Key codes identify the physical position of a key, not the character printed on it - see [Keyboard](#keyboard).


Positions, deltas, and axis values differ from device to device - see the chapters below.


Modifiers have their own check. **[Input.IsModifierEnabled()](../../../api/library/controls/class.input_cs.md#isModifierEnabled_int_int)** reads the state from the operating system, so it also covers the lock keys and is not affected by the [events filter](#events_filter):


```csharp
if (Input.IsModifierEnabled(Input.MODIFIER.ANY_CTRL) && Input.IsKeyDown(Input.KEY.S))
	Save();

```


Besides *ANY_* variants, there are left and right modifiers, as well as *NUM_LOCK, CAPS_LOCK, SCROLL_LOCK*, and *ALT_GR*.


## Handling Input Events


Polling answers the question "What is happening right now?" Events answer "What just happened?" Subscribe to them the same way as to any other [event in UNIGINE](../../../code/fundamentals/events/index_cs.md):


```csharp
private EventConnections connections = new EventConnections();

private void Init()
{
	Input.EventKeyDown.Connect(connections, (Input.KEY key) =>
	{
		Log.Message($"key down: {Input.GetKeyName(key)}\n");
	});

	Input.EventGamepadConnected.Connect(connections, (int num) =>
	{
		Log.Message($"gamepad {num} connected\n");
	});
}

```


Use polling for continuous actions such as movement or aiming, and use events for single reactions such as interface clicks, keyboard shortcuts, text input, and devices being connected or disconnected.


The available events are:


| Device | Events |
|---|---|
| Keyboard | **[EventKeyDown](../../../api/library/controls/class.input_cs.md#EventKeyDown)**, **[EventKeyUp](../../../api/library/controls/class.input_cs.md#EventKeyUp)**, **[EventKeyRepeat](../../../api/library/controls/class.input_cs.md#EventKeyRepeat)** |
| Text Input | **[EventTextPress](../../../api/library/controls/class.input_cs.md#EventTextPress)**, **[EventTextEditing](../../../api/library/controls/class.input_cs.md#EventTextEditing)** |
| Mouse | **[EventMouseDown](../../../api/library/controls/class.input_cs.md#EventMouseDown)**, **[EventMouseUp](../../../api/library/controls/class.input_cs.md#EventMouseUp)**, **[EventMouseMotion](../../../api/library/controls/class.input_cs.md#EventMouseMotion)**, **[EventMouseWheel](../../../api/library/controls/class.input_cs.md#EventMouseWheel)**, **[EventMouseWheelHorizontal](../../../api/library/controls/class.input_cs.md#EventMouseWheelHorizontal)** |
| Touch Devices | **[EventTouchDown](../../../api/library/controls/class.input_cs.md#EventTouchDown)**, **[EventTouchUp](../../../api/library/controls/class.input_cs.md#EventTouchUp)**, **[EventTouchMotion](../../../api/library/controls/class.input_cs.md#EventTouchMotion)** |
| Gamepads | **[EventGamepadConnected](../../../api/library/controls/class.input_cs.md#EventGamepadConnected)**, **[EventGamepadDisconnected](../../../api/library/controls/class.input_cs.md#EventGamepadDisconnected)**, **[EventGamepadButtonDown](../../../api/library/controls/class.input_cs.md#EventGamepadButtonDown)**, **[EventGamepadButtonUp](../../../api/library/controls/class.input_cs.md#EventGamepadButtonUp)**, **[EventGamepadAxisMotion](../../../api/library/controls/class.input_cs.md#EventGamepadAxisMotion)**, and the gamepad touchpad events |
| Joysticks | **[EventJoyConnected](../../../api/library/controls/class.input_cs.md#EventJoyConnected)**, **[EventJoyDisconnected](../../../api/library/controls/class.input_cs.md#EventJoyDisconnected)**, **[EventJoyButtonDown](../../../api/library/controls/class.input_cs.md#EventJoyButtonDown)**, **[EventJoyButtonUp](../../../api/library/controls/class.input_cs.md#EventJoyButtonUp)**, **[EventJoyAxisMotion](../../../api/library/controls/class.input_cs.md#EventJoyAxisMotion)**, **[EventJoyPovMotion](../../../api/library/controls/class.input_cs.md#EventJoyPovMotion)** |
| VR Devices | Connection, button, button touch, and axis events - see [VR Input System](../../../vr_development/vr_input_cs.md) |
| Any Device | *[Immediate Input](../../../api/library/controls/class.input_cs.md#EventImmediateInput)* - see [Immediate Input Event](#immediate_input) |


All of these, except Immediate Input, are triggered on the main thread during the Engine update.


## Keyboard


The main difficulty with keyboard input is that keyboard layouts differ from country to country. UNIGINE solves it by working with the **physical position** of a key rather than with the character printed on it. Key codes are bound to the QWERTY layout. If you set up movement on *WASD*, a user with an AZERTY keyboard will use *ZQSD* - the keys in the same physical place, under the same fingers.


When you do need the character rather than the position, use these methods:


| Method | Returns |
|---|---|
| **[Input.GetKeyName()](../../../api/library/controls/class.input_cs.md#getKeyName_int_cstr)** | The name of the key code itself, such as *W*. Does not depend on the layout. |
| **[Input.KeyToUnicode()](../../../api/library/controls/class.input_cs.md#keyToUnicode_int_uint)** | The Unicode character the key produces on the current layout. |
| **[Input.GetKeyLocalName()](../../../api/library/controls/class.input_cs.md#getKeyLocalName_int_cstr)** | A readable name for the key on the current layout. Falls back to the key code name when the key has no printable character - for example, a NumPad key with NumLock off. |
| **[Input.GetKeyByName()](../../../api/library/controls/class.input_cs.md#getKeyByName_cstr_int)**, **[Input.UnicodeToKey()](../../../api/library/controls/class.input_cs.md#unicodeToKey_uint_int)** | The reverse conversions, from a name or a character back to a key code. |


Use **[Input.GetKeyLocalName()](../../../api/library/controls/class.input_cs.md#getKeyLocalName_int_cstr)** when you show key bindings in the interface, so that users see the key as it is labeled on their own keyboard.


Some keys appear twice on the keyboard. For these, the *[KEY_ANY_](../../../api/library/controls/class.input_cs.md#KEY)* codes respond to either one. Use them when it makes no difference which of the two the user pressed. Note that *KEY_ANY_CTRL* and the other key codes go through the input pipeline, while *MODIFIER_ANY_CTRL* and the other [modifiers](#polling) are read from the operating system.


## Text Input


Reading keys is not enough for entering text. A key code identifies the key that was pressed, not the character that the key produces. The character depends on the keyboard layout and on the active modifiers. For languages such as Chinese or Japanese it also depends on an IME - a system component that composes one character from several keystrokes.


For text, subscribe to **[Input.EventTextPress](../../../api/library/controls/class.input_cs.md#EventTextPress)**. It delivers ready Unicode characters:


```csharp
Input.EventTextPress.Connect(connections, (uint unicode) =>
{
	// append the character to the text field
});

```


An IME composes a character over several keystrokes, and the partially composed text has to be shown to the user. That intermediate text is passed by **[Input.EventTextEditing](../../../api/library/controls/class.input_cs.md#EventTextEditing)**, which provides three values: the text that is being composed, the cursor position in that text, and the length of the text.


In the built-in [widgets](../../../code/gui/ui/ui_widgets.md) for text input the IME works on its own, and you do not have to write anything for it. You control it yourself only when you handle text input on your own, for example in a custom widget.


In that case, switch the IME on with **[Input.IMEEnabled](../../../api/library/controls/class.input_cs.md#IMEEnabled)** while your text field is focused and switch it off afterwards, so that it does not intercept keys during normal gameplay. Use **[Input.SetIMETextInputRect()](../../../api/library/controls/class.input_cs.md#setIMETextInputRect_int_int_int_int_void)** to tell the system where the field is on screen, so that the list of suggested characters appears next to it.


**[Input.IsKeyText()](../../../api/library/controls/class.input_cs.md#isKeyText_int_int)** tells whether a key produces a printable character at all. For NumPad keys, the answer depends on whether NumLock is enabled.


## Clipboard


The Input System also gives access to the system clipboard, which is what makes copy and paste work in your text fields:


```csharp
// copy
Input.Clipboard = "text to copy";

// paste
if (!Input.IsEmptyClipboard)
{
	string text = Input.Clipboard;
}

```


The clipboard is shared with the rest of the system, so the text can come from or go to any other application.


## Mouse


Mouse buttons are read with the same three methods as any other control - see [Reading Device States](#polling). Besides the usual buttons, there is *MOUSE_BUTTON_DCLICK*, a virtual button the Engine reports on a [double click](#input_events).


The cursor position is available from **[Input.MousePosition](../../../api/library/controls/class.input_cs.md#MousePosition)**, in global desktop coordinates. It is captured once at the start of the frame, so it does not change while the frame is being processed. When you need the position the system has right now, use **[Input.GetForceMousePosition()](../../../api/library/controls/class.input_cs.md#getForceMousePosition_ivec2)** instead. **[Input.MouseWheel](../../../api/library/controls/class.input_cs.md#MouseWheel)** and **[Input.MouseWheelHorizontal](../../../api/library/controls/class.input_cs.md#MouseWheelHorizontal)** report how far the wheel turned during the frame.


### Two Kinds of Movement


You can measure mouse movement in two ways. These two values are not interchangeable:


- **[Input.MouseDeltaPosition](../../../api/library/controls/class.input_cs.md#MouseDeltaPosition)** is the difference between cursor positions in two frames. It includes everything the operating system applies to the pointer, such as the sensitivity setting and the acceleration, and it stops at the screen edges.
- **[Input.MouseDeltaRaw](../../../api/library/controls/class.input_cs.md#MouseDeltaRaw)** is the movement reported by the device itself, with no system processing applied.


![The same mouse movement measured as cursor movement and as device movement](input_mouse_delta.svg)

*The mouse moves the same amount in both frames. The system sensitivity makes the cursor cover more ground - until it reaches the screen edge and stops*


Use **[Input.MouseDeltaPosition](../../../api/library/controls/class.input_cs.md#MouseDeltaPosition)** when the user is pointing at something on screen, and **[Input.MouseDeltaRaw](../../../api/library/controls/class.input_cs.md#MouseDeltaRaw)** when the user is controlling a camera. The user may change the system sensitivity at any time, and camera speed should not change with it. The raw delta guarantees that.


### Cursor Behavior


In a 3D application, the cursor usually has to be locked or hidden. Two settings cover this:


- **[Input.MouseGrab](../../../api/library/controls/class.input_cs.md#MouseGrab)** confines the cursor to the window. The mouse keeps reporting movement, but the cursor never leaves the window, so the user can turn the camera without limit.
- **[Input.MouseCursorHide](../../../api/library/controls/class.input_cs.md#MouseCursorHide)** hides the cursor without affecting its position.


Both together are the usual setup for a first-person camera, often with a crosshair drawn at the center of the screen. By default, however, you do not control them: the Engine manages the cursor itself. It captures the cursor when the user clicks in the viewport and releases it when the user presses *Esc* or opens the [console](../../../code/console/index.md), and it does so every frame, overwriting both settings. While the Engine manages a confined cursor, it also re-centers it every frame.


**[Input.MouseHandle](../../../api/library/controls/class.input_cs.md#MouseHandle)** selects who is in charge:


- *MOUSE_HANDLE_GRAB* - the default described above.
- *MOUSE_HANDLE_SOFT* - the cursor is hidden after a second without movement and shown again as soon as the mouse moves.
- *MOUSE_HANDLE_USER* - the cursor is left entirely to your code.


Switching to *MOUSE_HANDLE_USER* stops the Engine from touching the cursor, and two things become your job:


- The switch itself releases the cursor. Set **[Input.MouseGrab](../../../api/library/controls/class.input_cs.md#MouseGrab)** again if you need it confined.
- Nothing re-centers the cursor any more. Do it with **[Input.MousePosition](../../../api/library/controls/class.input_cs.md#MousePosition)**.


For replacing the cursor image and other appearance settings, see [Customizing Mouse Cursor and Behavior](../../../code/usage/mouse_customization/index_cs.md).


## Gamepads


Gamepads can be connected and disconnected while the application is running. The Engine gives every gamepad it has seen a fixed **slot**: **[Input.NumGamePads](../../../api/library/controls/class.input_cs.md#NumGamePads)** returns the number of slots, and **[Input.GetGamePad()](../../../api/library/controls/class.input_cs.md#getGamePad_int_InputGamePad)** returns the gamepad in a given slot.


Slots are never removed. Unplugging a gamepad does not decrease **[Input.NumGamePads](../../../api/library/controls/class.input_cs.md#NumGamePads)**, and a newly connected gamepad reuses the lowest free slot, so the same slot can later refer to a different gamepad. Always check **[InputGamePad.IsAvailable](../../../api/library/controls/class.inputgamepad_cs.md#isAvailable_int)** before you read a gamepad: it is the only way to tell whether the slot currently has hardware behind it.


![How gamepad slots are assigned and reused](input_gamepad_slots.svg)

*A slot is never removed: unplugging a gamepad does not lower the counter, and the next one connected takes the free slot*


Gamepad connection events are the only input the Engine accepts while input is [out of focus](#focus) and [background update](../../../code/console/index.md#background_update) is disabled. They are still processed only when the Engine updates again, so the slots catch up as soon as the application regains focus.


```csharp
InputGamePad pad = Input.GetGamePad(0);
if (pad != null && pad.IsAvailable)
{
	vec2 move = pad.AxesLeft;
	vec2 look = pad.AxesRight;
	float gas = pad.TriggerRight;

	if (pad.IsButtonDown(Input.GAMEPAD_BUTTON.A))
		Log.Message("jump\n");
}

```


Buttons follow a common layout - *A, B, X, Y*, shoulders, thumbsticks, D-pad, *START, BACK, GUIDE*, and *TOUCHPAD* - regardless of the gamepad model. The model of the connected gamepad is reported by **[InputGamePad.ModelType](../../../api/library/controls/class.inputgamepad_cs.md#ModelType)**, so you can show button prompts that match the device the user is holding.


### Dead Zone and Smoothing


A thumbstick that nobody is touching rarely reports exactly zero. Without a dead zone, the character drifts slowly even when the user is not touching the gamepad.


The Input System has no built-in dead zone. Compare the axis value against your own threshold:


```csharp
const float DEAD_ZONE = 0.15f;

vec2 move = pad.AxesLeft;

if (MathLib.Abs(move.x) < DEAD_ZONE) move.x = 0.0f;
if (MathLib.Abs(move.y) < DEAD_ZONE) move.y = 0.0f;

```


What the Engine does provide is **smoothing**. **[InputGamePad.Filter](../../../api/library/controls/class.inputgamepad_cs.md#setFilter_float_void)** sets the weight with which the value of the previous frame is blended into the current one. 0 means no smoothing and the axes react instantly; larger values make them react more slowly. The same weight is applied to both thumbsticks and both triggers.


> **Notice:** The Engine applies the smoothing once per frame with a fixed weight, so the result depends on the frame rate.


### Vibration, Light, and Sensors


**[InputGamePad.SetVibration()](../../../api/library/controls/class.inputgamepad_cs.md#setVibration_float_float_float_void)** starts vibration with separate intensity for the low-frequency and high-frequency motors, and a duration in milliseconds.


Some gamepads also have a light bar and motion sensors. These are optional, so check for support before use: **[InputGamePad.IsLightSupported](../../../api/library/controls/class.inputgamepad_cs.md#IsLightSupported)** before **[InputGamePad.SetLightColor()](../../../api/library/controls/class.inputgamepad_cs.md#setLightColor_vec3_void)**, **[InputGamePad.IsAccelerationSupported](../../../api/library/controls/class.inputgamepad_cs.md#IsAccelerationSupported)** before **[InputGamePad.Acceleration](../../../api/library/controls/class.inputgamepad_cs.md#Acceleration)**, and **[InputGamePad.IsAngularVelocitySupported](../../../api/library/controls/class.inputgamepad_cs.md#IsAngularVelocitySupported)** before **[InputGamePad.AngularVelocity](../../../api/library/controls/class.inputgamepad_cs.md#AngularVelocity)**.


A gamepad may also have a touchpad. Touchpads are counted by **[InputGamePad.NumTouches](../../../api/library/controls/class.inputgamepad_cs.md#NumTouches)**, and the fingers on a given touchpad by **[InputGamePad.GetNumTouchFingers()](../../../api/library/controls/class.inputgamepad_cs.md#getNumTouchFingers_int_int)**. A finger is addressed by a pair of indices - the touchpad and the finger on it - and reports its [position](../../../api/library/controls/class.inputgamepad_cs.md#getTouchPosition_int_int_vec2), [movement](../../../api/library/controls/class.inputgamepad_cs.md#getTouchDelta_int_int_vec2), and [pressure](../../../api/library/controls/class.inputgamepad_cs.md#getTouchPressure_int_int_float).


## Joysticks


A joystick can be a flight stick, a wheel, a throttle quadrant, or a similar device. Use **[Input.GetJoystick()](../../../api/library/controls/class.input_cs.md#getJoystick_int_InputJoystick)** to get a joystick by slot and **[Input.NumJoysticks](../../../api/library/controls/class.input_cs.md#NumJoysticks)** to get the number of slots. Slots work the same way as for [gamepads](#gamepads), so check **[InputJoystick.IsAvailable](../../../api/library/controls/class.inputjoystick_cs.md#isAvailable_int)** before you read a joystick.


Unlike a gamepad, a joystick has no fixed set of controls. Request the number of controls from the device: **[InputJoystick.NumAxes](../../../api/library/controls/class.inputjoystick_cs.md#getNumAxes_int)**, **[InputJoystick.NumButtons](../../../api/library/controls/class.inputjoystick_cs.md#getNumButtons_int)**, and **[InputJoystick.NumPovs](../../../api/library/controls/class.inputjoystick_cs.md#getNumPovs_int)**. Each control also reports its own name - **[InputJoystick.GetAxisName()](../../../api/library/controls/class.inputjoystick_cs.md#getAxisName_uint_cstr)**, **[InputJoystick.GetButtonName()](../../../api/library/controls/class.inputjoystick_cs.md#getButtonName_uint_cstr)**, and **[InputJoystick.GetPovName()](../../../api/library/controls/class.inputjoystick_cs.md#getPovName_uint_cstr)** - and this is the name to show in the bindings screen.


A POV hat is the small eight-way switch on top of a stick. Although its motion has eight directions, a hat behaves like a button, not like an axis: its events are queued one per frame.


### Force Feedback


Joysticks can push back. Waveform effects follow a fixed shape over time: constant force, ramps, sine, square, triangle, and sawtooth waves. The spring, friction, damper, and inertia effects instead react to how the user moves the device.


![The force each waveform effect applies over time](input_ffb_waveforms.svg)

*The force each waveform effect applies over time, against the zero line*


Force feedback works on both Windows and Linux. What is available depends on the device rather than on the Engine: a device works on Linux if its manufacturer supports Linux, and each device implements its own subset of the effects. Check before you play an effect:


```csharp
InputJoystick joystick = Input.GetJoystick(0);

if (joystick != null && joystick.IsAvailable
	&& joystick.IsForceFeedbackEffectSupported(Input.JOYSTICK_FORCE_FEEDBACK_EFFECT.JOYSTICK_FORCE_FEEDBACK_SPRING))
{
	joystick.PlayForceFeedbackEffectSpring(0.5f);
}

```


An effect runs until it ends or until it is [stopped explicitly](../../../api/library/controls/class.inputjoystick_cs.md#stopForceFeedbackEffect_int_void).


See more details of force feedback in the [related article](../../../code/fundamentals/input_system/force_feedback.md).


## Touch Devices


Touches are addressed by index, so several fingers can be tracked at once. The Engine assigns an index to a finger when it touches the surface and frees the index when the finger is lifted.


Each touch has the same three states as a button - **[Input.IsTouchDown()](../../../api/library/controls/class.input_cs.md#isTouchDown_int_int)**, **[Input.IsTouchPressed()](../../../api/library/controls/class.input_cs.md#isTouchPressed_int_int)**, **[Input.IsTouchUp()](../../../api/library/controls/class.input_cs.md#isTouchUp_int_int)** - plus a position and a movement delta, read with **[Input.GetTouchPosition()](../../../api/library/controls/class.input_cs.md#getTouchPosition_int_ivec2)** and **[Input.GetTouchDelta()](../../../api/library/controls/class.input_cs.md#getTouchDelta_int_ivec2)**.


Do not store a touch index between gestures: once a finger is lifted, the same index can be given to a different finger.


## VR Devices


VR controllers, trackers, and head-mounted displays go through the same [pipeline](#pipeline) as every other device, and their buttons and axes are read the same way. Everything specific to VR - tracking, transforms, haptics, and the button layout of each controller model - is covered in a separate article.


See [VR Input System](../../../vr_development/vr_input_cs.md).


## Building a Control Scheme


The Input System reports what the hardware is doing. Turning that into actions your application understands is the job of your own code.


### Rebindable Controls


Do not compare against a hard-coded key. Store a key code per action, read that code every frame, and let the user change it.


Three methods make the bindings storable and presentable:


- **[Input.GetKeyName()](../../../api/library/controls/class.input_cs.md#getKeyName_int_cstr)** turns a key code into a name that does not depend on the layout - save this in your settings file.
- **[Input.GetKeyByName()](../../../api/library/controls/class.input_cs.md#getKeyByName_cstr_int)** turns the name back into a key code when you load the settings.
- **[Input.GetKeyLocalName()](../../../api/library/controls/class.input_cs.md#getKeyLocalName_int_cstr)** gives the label printed on the user's own keyboard - show this in the bindings screen.


```csharp
Input.KEY jumpKey = Input.KEY.SPACE;

// when you save the settings: store a layout-independent name, for example "SPACE"
string name = Input.GetKeyName(jumpKey);

// when you load the settings: turn the stored name back into a key code
jumpKey = Input.GetKeyByName(name);

// in the bindings screen: show the label printed on this keyboard
Log.Message($"jump key: {Input.GetKeyLocalName(jumpKey)}\n");

// in your update: read the binding instead of a hard-coded key
if (Input.IsKeyDown(jumpKey))
	Jump();

```


To let the user assign a new key, subscribe to **[EventKeyDown](../../../api/library/controls/class.input_cs.md#EventKeyDown)** while the bindings screen is waiting for input, and take the key the event reports.


Joysticks have no fixed set of controls, so store a control index instead of a key code, and ask the device for the label: **[InputJoystick.GetAxisName()](../../../api/library/controls/class.inputjoystick_cs.md#getAxisName_uint_cstr)**, **[InputJoystick.GetButtonName()](../../../api/library/controls/class.inputjoystick_cs.md#getButtonName_uint_cstr)**, and **[InputJoystick.GetPovName()](../../../api/library/controls/class.inputjoystick_cs.md#getPovName_uint_cstr)**.


### Input and Widgets


Widgets do not consume input. The Engine updates device states before it updates the interface, so a click on an interface button reaches your world logic in the same frame: the weapon shoots while the user is clicking a menu button.


Check **[Gui.GetUnderCursorWidget()](../../../api/library/gui/class.gui_cs.md#getUnderCursorWidget_Widget)** on the [current](../../../api/library/gui/class.gui_cs.md#getCurrent_Gui) Gui before you act on a click. It returns the widget the cursor is hovering over, and nothing when the cursor is over no widget at all.


## Intercepting and Simulating Input


Use the features in this chapter when the standard processing is not enough. They let you receive every event before the Engine receives it, react to input with the smallest possible delay, and send input that no real device produced.


### Events Filter


You can set an events filter - a function that is called for every incoming event before the Engine processes it. The return value determines what happens to the event:


- 0 - pass the event to the Engine.
- 1 - reject the event.


There is a **single filter for the whole Input System**. Setting a new one via **[Input.SetEventsFilter()](../../../api/library/controls/class.input_cs.md#setEventsFilter_int_ptr_void)** replaces the previous one, so all your rules must be implemented in a single function.


The following filter rejects all events from the *Space* key, so that they never reach the Engine:


```csharp
private int EventFilter(InputEvent e)
{
	if (e.Type == InputEvent.TYPE.INPUT_EVENT_KEYBOARD)
	{
		InputEventKeyboard keyEvent = e as InputEventKeyboard;
		if (keyEvent.Key == Input.KEY.SPACE)
			return 1;
	}

	return 0;
}

private void Init()
{
	Input.SetEventsFilter(EventFilter);
}

```


A filter is useful in the following cases:


- **Dropping unwanted events**. See the example above.
- **Changing event data**. Events have setters, so you can swap mouse buttons for left-handed users, remap a key, or scale a mouse delta before the Engine sees it.
- **Resolving conflicts between devices**. When several devices are connected and report the same action, the filter is the place to give priority to one of them.
- **Protecting against event bursts**. See [Performance and Common Mistakes](#performance).


The filter below does not reject anything - it swaps the left and right mouse buttons for left-handed users. The event is passed on with 0, and the Engine sees only the modified version of it:


```csharp
private int SwapMouseButtons(InputEvent e)
{
	if (e.Type == InputEvent.TYPE.INPUT_EVENT_MOUSE_BUTTON)
	{
		InputEventMouseButton buttonEvent = e as InputEventMouseButton;

		if (buttonEvent.Button == Input.MOUSE_BUTTON.LEFT)
			buttonEvent.Button = Input.MOUSE_BUTTON.RIGHT;
		else if (buttonEvent.Button == Input.MOUSE_BUTTON.RIGHT)
			buttonEvent.Button = Input.MOUSE_BUTTON.LEFT;
	}

	return 0;
}

```


> **Warning:** The filter is called on the thread that sent the event, which is not necessarily the main thread. Keep it short and thread-safe, and see [Thread Safety in API](../../../code/fundamentals/thread_safety/index.md) for what you may call from it.


### Immediate Input Event


The *[Immediate Input](../../../api/library/controls/class.input_cs.md#EventImmediateInput)* event is the fastest way to learn about new input. It is triggered as soon as the event passes the filter, before it reaches the events buffer.


```csharp
private EventConnections connections = new EventConnections();

private void OnImmediateInput(InputEvent e)
{
	if (e.Type == InputEvent.TYPE.INPUT_EVENT_KEYBOARD)
	{
		InputEventKeyboard keyEvent = e as InputEventKeyboard;
		Log.Message($"keyboard event: {Input.GetKeyName(keyEvent.Key)} {keyEvent.Action}\n");
	}
}

private void Init()
{
	Input.EventImmediateInput.Connect(connections, OnImmediateInput);
}

```


Two things follow from the position of this event in the [pipeline](#pipeline):


- The filter still applies. Rejected events never reach the handler.
- The handler runs on the thread that sent the event. There is no guarantee that this is the main thread.


Use this event for low-latency tasks such as writing your own buffering system or logging raw input. For regular application logic, poll device states or use the ordinary input events instead - they are delivered on the main thread.


### Sending Custom Events


You can create input events yourself and send them to the Engine via **[Input.SendEvent()](../../../api/library/controls/class.input_cs.md#sendEvent_InputEvent_void)**. This is useful for automated testing, replaying recorded sessions, remote control, and virtual input devices.


The example below simulates pressing a key:


```csharp
private void SimulateKeyInput(Input.KEY key)
{
	InputEventKeyboard keyDown = new InputEventKeyboard();
	keyDown.Action = InputEventKeyboard.ACTION.DOWN;
	keyDown.Key = key;

	InputEventKeyboard keyUp = new InputEventKeyboard();
	keyUp.Action = InputEventKeyboard.ACTION.UP;
	keyUp.Key = key;

	Input.SendEvent(keyDown);
	Input.SendEvent(keyUp);
}

```


Events you send follow exactly the same path as events from real devices - focus check, filter, Immediate Input, buffer. Because of this, the Engine discards them while input is out of focus and background update is disabled.


Once you pass an event to **Input.SendEvent()**, the Engine owns it and deletes it when it leaves the 60-frame history. Do not keep or reuse the object afterwards. The events you get from **[Input.GetEventsBuffer()](../../../api/library/controls/class.input_cs.md#getEventsBuffer_int_VECInputEvent_int)** belong to the Engine as well.


> **Warning:** Never send back an event that came from **[Input.GetEventsBuffer()](../../../api/library/controls/class.input_cs.md#getEventsBuffer_int_VECInputEvent_int)**. The Engine already owns that object and deletes it on its own. If you send it again, the Engine deletes the same object twice, which corrupts memory and usually crashes the application.
>
>
> To record and replay a session, copy what you need from each event - its type, timestamp, and key, button, or position - into your own data. Create new events when you replay the recording.


## Performance and Common Mistakes


**Frame rate and input values.**


- **Multiply by the frame duration**, *[Game::getIFps()](../../../api/library/engine/class.game_cs.md#IFps)*. Axes of gamepads and joysticks hold an absolute position that does not depend on the frame rate. Without the multiplication, a stick moves the character faster on a machine with a higher frame rate.
- **Do not multiply.** Mouse deltas and the wheel are [summed over the frame](#events_buffer). A slower frame collects more movement, so these values already account for the frame duration. Multiplying them again makes the mouse feel slower on a low frame rate.


**Event bursts after a frame rate drop.** Press and release events are taken from the [per-control queue](#events_buffer) one per frame. If the frame rate drops while the user keeps clicking, the queues grow. No event is lost, but once the frame rate returns to normal, the accumulated events are applied one per frame and the application performs many actions in a short time. If this behavior is a problem for your application, handle it in the [events filter](#events_filter) - for example, check the current frame rate and discard the excess events.


**Work done in the filter.** The filter runs for every single event, including high-frequency mouse motion. Heavy logic here directly increases input latency.


## See Also


- [Input Class](../../../api/library/controls/class.input_cs.md) - the full API reference.
- [VR Input System](../../../vr_development/vr_input_cs.md) - controllers, trackers, and headsets.
- [Customizing Mouse Cursor and Behavior](../../../code/usage/mouse_customization/index_cs.md) - cursor images and appearance.
- [Event Handling](../../../code/fundamentals/events/index_cs.md) - how subscription works in UNIGINE.
- [Thread Safety in API](../../../code/fundamentals/thread_safety/index.md) - what you may call from the events filter and the Immediate Input handler.
- [Input Handling](../../../sdk/api_samples/cpp/input_controls.md) - a runnable sample from the SDK.
