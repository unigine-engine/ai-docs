# Unigine::Input Class (CS)

> **Notice:** This class is a singleton.


The Input class contains functions for simple manual handling of user inputs using a keyboard, a mouse or a gamepad.


### See Also


- A set of C++ samples (`<SAMPLES_PROJECT_PATH>/source/input_controls/`)
- A set of C# Component samples (`<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/input_controls/`)


### Usage Examples


The following example shows a way to move and rotate a node by using the Input class:


```csharp
private Node box = null;

private const float moveSpeed = 1.0f;
private const float turnSpeed = 30.0f;

private void Init()
{

	box = Primitives.CreateBox(vec3.ONE);

}

private void Update()
{

	if (Unigine.Console.Active)
		return;

	if (Input.IsKeyPressed(Input.KEY.UP) || Input.IsKeyPressed(Input.KEY.W))
		box.Translate(vec3.FORWARD * moveSpeed * Game.IFps);

	if (Input.IsKeyPressed(Input.KEY.DOWN) || Input.IsKeyPressed(Input.KEY.S))
		box.Translate(vec3.BACK * moveSpeed * Game.IFps);

	if (Input.IsKeyPressed(Input.KEY.LEFT) || Input.IsKeyPressed(Input.KEY.A))
		box.Rotate(0.0f, 0.0f, turnSpeed * Game.IFps);

	if (Input.IsKeyPressed(Input.KEY.RIGHT) || Input.IsKeyPressed(Input.KEY.D))
		box.Rotate(0.0f, 0.0f, -turnSpeed * Game.IFps);

}

```


The following code demonstrates how to receive an event that changed the button state to [IsKeyDown](#isKeyDown_int_int), [IsKeyUp](#isKeyUp_int_int). Such code can also be used for the mouse and touch buttons.


```csharp
private void Update()
{

	if (Input.IsKeyDown(Input.KEY.T) || Input.IsKeyUp(Input.KEY.T))
		{
			InputEventKeyboard e = Input.GetKeyEvent(Input.KEY.T);
			Unigine.Console.MessageLine($"{Input.GetKeyName(e.Key)} {e.Action} time = {e.Timestamp} frame = {e.Frame}");
		}
}

```


The following code illustrates receiving the immediate input � the user receives the event notification immediately after filtering:


```csharp
private void Init()
{

	Input.EventImmediateInput.Connect(OnImmediateInput);

}

private void OnImmediateInput(InputEvent e)
{
	switch (e.Type)
	{
		case InputEvent.TYPE.INPUT_EVENT_KEYBOARD:
		{
			InputEventKeyboard k = e as InputEventKeyboard;
			Unigine.Console.MessageLine($"keyboard event: {Input.GetKeyName(k.Key)} {k.Action}");
			break;
		}

		case InputEvent.TYPE.INPUT_EVENT_MOUSE_BUTTON:
		{
			InputEventMouseButton m = e as InputEventMouseButton;
			Unigine.Console.MessageLine($"mouse button event: {Input.GetMouseButtonName(m.Button)} {m.Action}");
			break;
		}

		default: break;
	}
}

```


The following code illustrates how the event filter works. Pressing the "W" button and mouse movements will be declined, i.e. these events won't be taken as input:


```csharp
private void Init()
{

	Input.SetEventsFilter(EventFilter);

}

private int EventFilter(InputEvent e)
{
	switch (e.Type)
	{
		case InputEvent.TYPE.INPUT_EVENT_KEYBOARD:
		{
			// skip 'W' key repeat events
			InputEventKeyboard k = e as InputEventKeyboard;
			if (k.Key == Input.KEY.W && k.Action == InputEventKeyboard.ACTION.REPEAT)
				return 1;
			break;
		}

		case InputEvent.TYPE.INPUT_EVENT_MOUSE_MOTION:
		{
			// skip all mouse motion events
			return 1;
		}

		default: break;
	}

	return 0;
}

```


The following code is an example of input events creation. We'll imitate the input of the `show_profiler 1` console command as if it were an event from the keyboard.


```csharp
enum STATE
{
	OPEN_CONSOLE = 0,
	TYPING_COMMAND,
	APPLY_COMMAND,
	FINISH,
}

private STATE state = STATE.OPEN_CONSOLE;

void emulate_key_input(Input.KEY key)
{
	InputEventKeyboard key_down = new InputEventKeyboard();
	key_down.Action =  InputEventKeyboard.ACTION.DOWN;
	key_down.Key = key;

	InputEventKeyboard key_repeat = new InputEventKeyboard();
	key_repeat.Action = InputEventKeyboard.ACTION.REPEAT;
	key_repeat.Key = key;

	InputEventKeyboard key_up = new InputEventKeyboard();
	key_up.Action = InputEventKeyboard.ACTION.UP;
	key_up.Key = key;

	Input.SendEvent(key_down);
	Input.SendEvent(key_repeat);
	Input.SendEvent(key_up);
}

void emulate_text_input(String text)
{
	int size = text.Length;
	for (int i = 0; i < size; i++)
	{
		InputEventText text_input = new InputEventText();
		text_input.Unicode = text[i];
		Input.SendEvent(text_input);
	}
}

private void Update()
{

	switch (state)
	{
		case STATE.OPEN_CONSOLE:
		{
			emulate_key_input(Input.KEY.BACK_QUOTE);
			state = STATE.TYPING_COMMAND;
			break;
		}

		case STATE.TYPING_COMMAND:
		{
			emulate_text_input("show_profiler 1");
			state = STATE.APPLY_COMMAND;
			break;
		}

		case STATE.APPLY_COMMAND:
		{
			emulate_key_input(Input.KEY.ENTER);
			state = STATE.FINISH;
			break;
		}

		default: break;
	}
}

```


The following code demonstrates how to obtain various button names using the [GetKeyName()](#getKeyName_int_cstr), [KeyToUnicode()](#keyToUnicode_int_uint), and [GetKeyLocalName()](#getKeyLocalName_int_cstr) methods:


```csharp
/*...*/
using System.Linq;
using System.Text;

/*...*/

	private void Init()
	{

		Unigine.Console.Onscreen = true;

	}

	private void Update()
	{

		var printInfo = (string state, Input.KEY key) =>
		{
			uint unicode = Input.KeyToUnicode(key);
			string unicodeName = Encoding.Unicode.GetString(BitConverter.GetBytes(unicode));
			unicodeName = unicodeName.TrimEnd('\0');
			Unigine.Console.Message($"{state}: (key='{Input.GetKeyName(key)}', unicode='{unicodeName}', local_name='{Input.GetKeyLocalName(key)}') ");
		};

		printInfo("Up", Input.KEY.W);
		printInfo("Jump", Input.KEY.SPACE);
		printInfo("Run", Input.KEY.RIGHT_SHIFT);
		Unigine.Console.Message("\n");
	}

```


## Input Class

### Enums

## MOUSE_HANDLE

| Name | Description |
|---|---|
| **GRAB** = 0 | The mouse is grabbed when clicked (the cursor disappears and camera movement is controlled by the mouse). |
| **SOFT** = 1 | The mouse cursor disappears after being idle for a short time period. |
| **USER** = 2 | The mouse is not handled by the system (allows input handling by some custom module). |

## MOUSE_BUTTON

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Unknown mouse button. |
| **LEFT** = 1 | Left mouse button. |
| **MIDDLE** = 2 | Middle mouse button. |
| **RIGHT** = 3 | Right mouse button. |
| **DCLICK** = 4 | Left mouse button double click. |
| **AUX_0** = 5 | Auxiliary mouse button. |
| **AUX_1** = 6 | Auxiliary mouse button. |
| **AUX_2** = 7 | Auxiliary mouse button. |
| **AUX_3** = 8 | Auxiliary mouse button. |
| **MOUSE_NUM_BUTTONS** = 9 | Number of mouse buttons. |

## MODIFIER

| Name | Description |
|---|---|
| **LEFT_SHIFT** = 0 | Left *Shift* key used as modifier. |
| **RIGHT_SHIFT** = 1 | Right *Shift* key used as modifier. |
| **LEFT_CTRL** = 2 | Left *Ctrl* key used as modifier. |
| **RIGHT_CTRL** = 3 | Right *Ctrl* key used as modifier. |
| **LEFT_ALT** = 4 | Left *Alt* key used as modifier. |
| **RIGHT_ALT** = 5 | Right *Alt* key used as modifier. |
| **LEFT_CMD** = 6 | Left Command key used as modifier. |
| **RIGHT_CMD** = 7 | Right Command key used as modifier. |
| **NUM_LOCK** = 8 | *Num Lock* key used as modifier. |
| **CAPS_LOCK** = 9 | *Caps Lock* key used as modifier. |
| **SCROLL_LOCK** = 10 | *Scroll Lock* key used as modifier. |
| **ALT_GR** = 11 | *Alt Gr* key used as modifier. |
| **ANY_SHIFT** = 12 | Any *Shift* key used as modifier. |
| **ANY_CTRL** = 13 | Any *Ctrl* key used as modifier. |
| **ANY_ALT** = 14 | Any *Alt* key used as modifier. |
| **ANY_CMD** = 15 | Any Command key used as modifier. |
| **NONE** = 16 | No modifier is specified. |
| **NUM_MODIFIERS** = 17 | Total number of modifiers. |

## KEY

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Unknown key |
| **ESC** = 1 | *Escape* key |
| **F1** = 2 | **F1** key |
| **F2** = 3 | **F2** key |
| **F3** = 4 | **F3** key |
| **F4** = 5 | **F4** key |
| **F5** = 6 | **F5** key |
| **F6** = 7 | **F6** key |
| **F7** = 8 | **F7** key |
| **F8** = 9 | **F8** key |
| **F9** = 10 | **F9** key |
| **F10** = 11 | **F10** key |
| **F11** = 12 | **F11** key |
| **F12** = 13 | **F12** key |
| **PRINTSCREEN** = 14 | *Print Screen* key |
| **SCROLL_LOCK** = 15 | *Scroll Lock* key |
| **PAUSE** = 16 | *Pause* key |
| **BACK_QUOTE** = 17 | Back quote key |
| **DIGIT_1** = 18 | The **1** key of the alphanumeric keyboard |
| **DIGIT_2** = 19 | The **2** key of the alphanumeric keyboard |
| **DIGIT_3** = 20 | The **3** key of the alphanumeric keyboard |
| **DIGIT_4** = 21 | The **4** key of the alphanumeric keyboard |
| **DIGIT_5** = 22 | The **5** key of the alphanumeric keyboard |
| **DIGIT_6** = 23 | The **6** key of the alphanumeric keyboard |
| **DIGIT_7** = 24 | The **7** key of the alphanumeric keyboard |
| **DIGIT_8** = 25 | The **8** key of the alphanumeric keyboard |
| **DIGIT_9** = 26 | The **9** key of the alphanumeric keyboard |
| **DIGIT_0** = 27 | The **0** key of the alphanumeric keyboard |
| **MINUS** = 28 | Minus key |
| **EQUALS** = 29 | Equals key |
| **BACKSPACE** = 30 | Backspace key |
| **TAB** = 31 | *Tab* key |
| **Q** = 32 | *Q* key |
| **W** = 33 | *W* key |
| **E** = 34 | *E* key |
| **R** = 35 | *R* key |
| **T** = 36 | *T* key |
| **Y** = 37 | *Y* key |
| **U** = 38 | *U* key |
| **I** = 39 | *I* key |
| **O** = 40 | *O* key |
| **P** = 41 | *P* key |
| **LEFT_BRACKET** = 42 | Left square bracket key |
| **RIGHT_BRACKET** = 43 | Right square bracket key |
| **ENTER** = 44 | *Enter* key |
| **CAPS_LOCK** = 45 | *Caps Lock* key |
| **A** = 46 | *A* key |
| **S** = 47 | *S* key |
| **D** = 48 | *D* key |
| **F** = 49 | *F* key |
| **G** = 50 | *G* key |
| **H** = 51 | *H* key |
| **J** = 52 | *J* key |
| **K** = 53 | *K* key |
| **L** = 54 | *L* key |
| **SEMICOLON** = 55 | Semicolon key |
| **QUOTE** = 56 | Quote key |
| **BACK_SLASH** = 57 | Backward slash key |
| **LEFT_SHIFT** = 58 | Left *Shift* key |
| **LESS** = 59 | Less than key |
| **Z** = 60 | **Z** key |
| **X** = 61 | **X** key |
| **C** = 62 | **C** key |
| **V** = 63 | **V** key |
| **B** = 64 | **B** key |
| **N** = 65 | **N** key |
| **M** = 66 | **M** key |
| **COMMA** = 67 | Comma key |
| **DOT** = 68 | Dot key |
| **SLASH** = 69 | Slash key |
| **RIGHT_SHIFT** = 70 | Right *Shift* key |
| **LEFT_CTRL** = 71 | Left *Ctrl* key |
| **LEFT_CMD** = 72 | Left Command key |
| **LEFT_ALT** = 73 | Left *Alt* key |
| **SPACE** = 74 | Space key |
| **RIGHT_ALT** = 75 | Right *Alt* key |
| **RIGHT_CMD** = 76 | Right Command key |
| **MENU** = 77 | Menu key |
| **RIGHT_CTRL** = 78 | Right *Ctrl* key |
| **INSERT** = 79 | *Insert* key |
| **DELETE** = 80 | *Delete* key |
| **HOME** = 81 | *Home* key |
| **END** = 82 | *End* key |
| **PGUP** = 83 | Page Up key |
| **PGDOWN** = 84 | Page down |
| **UP** = 85 | Up arrow key |
| **LEFT** = 86 | Left arrow key |
| **DOWN** = 87 | Down arrow key |
| **RIGHT** = 88 | Right arrow key |
| **NUM_LOCK** = 89 | *Num Lock* key |
| **NUMPAD_DIVIDE** = 90 | Divide key of the numeric keypad |
| **NUMPAD_MULTIPLY** = 91 | Multiply key of the numeric keypad |
| **NUMPAD_MINUS** = 92 | Minus key of the numeric keypad |
| **NUMPAD_DIGIT_7** = 93 | The **7** key of the numeric keypad |
| **NUMPAD_DIGIT_8** = 94 | The **8** key of the numeric keypad |
| **NUMPAD_DIGIT_9** = 95 | The **9** key of the numeric keypad |
| **NUMPAD_PLUS** = 96 | Plus key of the numeric keypad |
| **NUMPAD_DIGIT_4** = 97 | The **4** key of the numeric keypad |
| **NUMPAD_DIGIT_5** = 98 | The **5** key of the numeric keypad |
| **NUMPAD_DIGIT_6** = 99 | The **6** key of the numeric keypad |
| **NUMPAD_DIGIT_1** = 100 | The **1** key of the numeric keypad |
| **NUMPAD_DIGIT_2** = 101 | The **2** key of the numeric keypad |
| **NUMPAD_DIGIT_3** = 102 | The **3** key of the numeric keypad |
| **NUMPAD_ENTER** = 103 | *Enter* key of the numeric keypad |
| **NUMPAD_DIGIT_0** = 104 | The **0** key of the numeric keypad |
| **NUMPAD_DOT** = 105 | Dot key of the numeric keypad |
| **ANY_SHIFT** = 106 | Any *Shift* key |
| **ANY_CTRL** = 107 | Any *Ctrl* key |
| **ANY_ALT** = 108 | Any *Alt* key |
| **ANY_CMD** = 109 | Any Command key |
| **ANY_UP** = 110 | Any up arrow key |
| **ANY_LEFT** = 111 | Any left arrow key |
| **ANY_DOWN** = 112 | Any down arrow key |
| **ANY_RIGHT** = 113 | Any right arrow key |
| **ANY_ENTER** = 114 | Any up arrow key |
| **ANY_DELETE** = 115 | Any *Delete* key |
| **ANY_INSERT** = 116 | Any *Insert* key |
| **ANY_HOME** = 117 | Any *Home* key |
| **ANY_END** = 118 | Any *End* key |
| **ANY_PGUP** = 119 | Any Page Up key |
| **ANY_PGDOWN** = 120 | Any Page Down key |
| **ANY_DIGIT_1** = 121 | The **1** key of either alphanumeric keyboard or numeric keypad |
| **ANY_DIGIT_2** = 122 | The **2** key of either alphanumeric keyboard or numeric keypad |
| **ANY_DIGIT_3** = 123 | The **3** key of either alphanumeric keyboard or numeric keypad |
| **ANY_DIGIT_4** = 124 | The **4** key of either alphanumeric keyboard or numeric keypad |
| **ANY_DIGIT_5** = 125 | The **5** key of either alphanumeric keyboard or numeric keypad |
| **ANY_DIGIT_6** = 126 | The **6** key of either alphanumeric keyboard or numeric keypad |
| **ANY_DIGIT_7** = 127 | The **7** key of either alphanumeric keyboard or numeric keypad |
| **ANY_DIGIT_8** = 128 | The **8** key of either alphanumeric keyboard or numeric keypad |
| **ANY_DIGIT_9** = 129 | The **9** key of either alphanumeric keyboard or numeric keypad |
| **ANY_DIGIT_0** = 130 | The **0** key of either alphanumeric keyboard or numeric keypad |
| **ANY_MINUS** = 131 | Any minus key |
| **ANY_EQUALS** = 132 | Any Equals key |
| **ANY_DOT** = 133 | Any dot key |
| **NUM_KEYS** = 134 | Number of keys. |

## DEVICE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Unknown device. |
| **GAME_CONTROLLER** = 1 | Game controller device. |
| **WHEEL** = 2 | Wheel device. |
| **ARCADE_STICK** = 3 | Arcade stick device. |
| **FLIGHT_STICK** = 4 | Flight stick device. |
| **DANCE_PAD** = 5 | Dance pad device. |
| **GUITAR** = 6 | Guitar. |
| **DRUM_KIT** = 7 | Drum kit. |
| **VR** = 8 | VR device. |

## GAMEPAD_BUTTON

Buttons of the gamepad.
| Name | Description |
|---|---|
| **A** = 0 | Button A of the gamepad. |
| **B** = 1 | Button B of the gamepad. |
| **X** = 2 | Button X of the gamepad. |
| **Y** = 3 | Button Y of the gamepad. |
| **BACK** = 4 | Button "Back" of the gamepad. |
| **START** = 5 | Button "Start" of the gamepad. |
| **DPAD_UP** = 6 | Button "Up" of the gamepad. |
| **DPAD_DOWN** = 7 | Button "Down" of the gamepad. |
| **DPAD_LEFT** = 8 | Button "Left" of the gamepad. |
| **DPAD_RIGHT** = 9 | Button "Right" of the gamepad. |
| **THUMB_LEFT** = 10 | Left thumbstick button of the gamepad. |
| **THUMB_RIGHT** = 11 | Right thumbstick button of the gamepad. |
| **SHOULDER_LEFT** = 12 | Left shoulder (bumper) button of the gamepad. |
| **SHOULDER_RIGHT** = 13 | Right shoulder (bumper) button of the gamepad. |
| **GUIDE** = 14 | Button "Guide" of the gamepad. |
| **MISC1** = 15 | The miscellaneous button of the gamepad. |
| **TOUCHPAD** = 16 | Touchpad of the gamepad. |
| **NUM_GAMEPAD_BUTTONS** = 17 | Number of buttons on a gamepad. |

## GAMEPAD_AXIS

| Name | Description |
|---|---|
| **LEFT_X** = 0 | X axis of the left stick of the gamepad. |
| **LEFT_Y** = 1 | Y axis of the left stick of the gamepad. |
| **RIGHT_X** = 2 | X axis of the right stick of the gamepad. |
| **RIGHT_Y** = 3 | Y axis of the right stick of the gamepad. |
| **LEFT_TRIGGER** = 4 | Left trigger of the gamepad. |
| **RIGHT_TRIGGER** = 5 | Right trigger of the gamepad. |
| **NUM_GAMEPAD_AXES** = 6 | Number of axes on a gamepad. |

## JOYSTICK_POV

POV (Point-of-View) switch or DPad states.
| Name | Description |
|---|---|
| **NOT_PRESSED** = 0 | POV (Point-of-View) hat switch or D-Pad (directional pad) button is not pressed. |
| **UP** = 1 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in up position. |
| **UP_RIGHT** = 2 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in right-up position. |
| **RIGHT** = 3 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in right position. |
| **DOWN_RIGHT** = 4 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in down-right position. |
| **DOWN** = 5 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in down position. |
| **DOWN_LEFT** = 6 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in down-left position. |
| **LEFT** = 7 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in left position. |
| **UP_LEFT** = 8 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in left-up position. |

## VR_BUTTON

| Name | Description |
|---|---|
| **SYSTEM** = 0 | System button. |
| **START** = 1 | Start button. |
| **HOME** = 2 | Home button. |
| **END** = 3 | End button. |
| **SELECT** = 4 | Select button. |
| **VOLUME_UP** = 5 | Volume Up button. |
| **VOLUME_DOWN** = 6 | Volume Up button. |
| **MUTE_MIC** = 7 | Mute Microphone button. |
| **PLAY_PAUSE** = 8 | Play/Pause button. |
| **MENU** = 9 | Menu button. |
| **VIEW** = 10 | View button. |
| **BACK** = 11 | Back button. |
| **X** = 12 | X button reserved for the controller. |
| **Y** = 13 | Y button reserved for the controller. |
| **SHOULDER** = 14 | Shoulder button reserved for the controller. |
| **GRIP** = 15 | Grip button reserved for the controller. |
| **AXIS_0** = 16 | The axis reserved for the controller. |
| **AXIS_1** = 17 | The axis reserved for the controller. |
| **AXIS_2** = 18 | The axis reserved for the controller. |
| **AXIS_3** = 19 | The axis reserved for the controller. |
| **AXIS_4** = 20 | The axis reserved for the controller. |
| **AXIS_5** = 21 | The axis reserved for the controller. |
| **AXIS_6** = 22 | The axis reserved for the controller. |
| **AXIS_7** = 23 | The axis reserved for the controller. |
| **AXIS_8** = 24 | The axis reserved for the controller. |
| **AXIS_9** = 25 | The axis reserved for the controller. |
| **AXIS_10** = 26 | The axis reserved for the controller. |
| **AXIS_11** = 27 | The axis reserved for the controller. |
| **AXIS_12** = 28 | The axis reserved for the controller. |
| **AXIS_13** = 29 | The axis reserved for the controller. |
| **AXIS_14** = 30 | The axis reserved for the controller. |
| **AXIS_15** = 31 | The axis reserved for the controller. |
| **DPAD_UP** = 32 | Sensor panel up button. |
| **DPAD_DOWN** = 33 | Sensor panel down button. |
| **DPAD_LEFT** = 34 | Sensor panel left button. |
| **DPAD_RIGHT** = 35 | Sensor panel right button. |
| **DPAD_CENTER** = 36 | Sensor panel center button. |
| **THUMBREST** = 37 | Thumb rest, a place for the user to rest their thumb. |
| **THUMB_RESTING_SURFACES** = 38 | Thumb resting surfaces � any surfaces that a thumb may naturally rest on. This may include, but is not limited to, face buttons, thumbstick, and thumbrest. |
| **PROXIMITY_SENSOR** = 39 | Proximity sensor. |
| **APPLICATION** = 40 | Application menu button. |
| **NUM_VR_BUTTONS** = 41 | Total number of VR buttons and axes. |

## JOYSTICK_FORCE_FEEDBACK_EFFECT

| Name | Description |
|---|---|
| **JOYSTICK_FORCE_FEEDBACK_CONSTANT** = 0 | Steady force in a single direction. |
| **JOYSTICK_FORCE_FEEDBACK_RAMP** = 1 | Force that steadily increases or decreases in magnitude. |
| **JOYSTICK_FORCE_FEEDBACK_SINEWAVE** = 2 | Force pulsates periodically according to the sinusoidal wave pattern. |
| **JOYSTICK_FORCE_FEEDBACK_SQUAREWAVE** = 3 | Force pulsates periodically according to the square wave pattern. |
| **JOYSTICK_FORCE_FEEDBACK_TRIANGLEWAVE** = 4 | Force pulsates periodically according to the triangle wave pattern. |
| **JOYSTICK_FORCE_FEEDBACK_SAWTOOTHUPWAVE** = 5 | Force pulsates periodically according to the up (regular) sawtooth wave pattern. |
| **JOYSTICK_FORCE_FEEDBACK_SAWTOOTHDOWNWAVE** = 6 | Force pulsates periodically according to the down (reverse) sawtooth wave pattern. |
| **JOYSTICK_FORCE_FEEDBACK_SPRING** = 7 | Force increases in proportion to the distance of the axis from a defined neutral point. |
| **JOYSTICK_FORCE_FEEDBACK_FRICTION** = 8 | Force is applied when the axis is moved and depends on the defined friction coefficient. |
| **JOYSTICK_FORCE_FEEDBACK_DAMPER** = 9 | Force increases in proportion to the velocity with which the user moves the axis. |
| **JOYSTICK_FORCE_FEEDBACK_INERTIA** = 10 | Force increases in proportion to the acceleration of the axis. |
| **NUM_JOYSTICK_FORCE_FEEDBACKS** = 11 | Total number of joystick force feedbacks. |

### Properties

## bool IMEEnabled

The value indicating if the system IME (Input Method Editor, used for composed text input such as CJK) is enabled. When enabled, the OS can open its composition and candidate window, and the engine receives *[text editing](../../../api/library/controls/class.inputeventtextediting_cs.md)* (preedit) events while the user composes text. Disabled by default.
## 🔒︎ int NumJoysticks

The number of joysticks.
## 🔒︎ int NumGamePads

The number of all gamepads.
## 🔒︎ int MouseWheelHorizontal

The horizontal mouse scroll value.
## 🔒︎ int MouseWheel

The vertical mouse scroll value.
## 🔒︎ ivec2 MouseDeltaPosition

The vector containing delta values of the mouse cursor position.
## ivec2 MousePosition

The vector containing integer values of the mouse cursor position.
## Input.MOUSE_HANDLE MouseHandle

The mouse behavior mode, one of the [MOUSE_HANDLE](#MOUSE_HANDLE) values.
## bool MouseCursorNeedUpdate

The value indicating that changes were made to the cursor (it was shown, hidden, changed to system, or anything else) and it has to be updated. Suppose the cursor was modified, for example, by the *Interface* plugin. After closing the plugin's window the cursor shall not return to its previous state because SDL doesn't even know about the changes. You can use this flag to signalize, that mouse cursor must be updated.
## bool MouseCursorSystem

The value indicating if the OS mouse pointer is displayed.
## bool MouseCursorHide

The value indicating if the mouse cursor is hidden in the current frame.
## bool MouseGrab

The value indicating if the mouse pointer is bound to the application window (can't leave it).
## string Clipboard

The contents of the system clipboard.
## 🔒︎ bool IsEmptyClipboard

The value indicating if the clipboard is empty.
## 🔒︎ ivec2 MouseDeltaRaw

The change in the absolute mouse position (not the screen cursor), dots per inch.
## 🔒︎ InputVRController VRControllerTreadmill

The treadmill VR controller.
## 🔒︎ InputVRController VRControllerRight

The right-hand VR controller.
## 🔒︎ InputVRController VRControllerLeft

The left-hand VR controller.
## 🔒︎ InputVRHead VRHead

The head VR controller.
## 🔒︎ int NumVRDevices

The number of all VR devices.
## 🔒︎ Event< InputEvent > EventImmediateInput

The event triggered immediately at input as received from proxy before being processed by the engine. This event can be triggered in different threads depending on the proxy implementation. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(InputEvent **event**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ImmediateInput event handler
void immediateinput_event_handler(InputEvent event)
{
	Log.Message("\Handling ImmediateInput event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections immediateinput_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventImmediateInput.Connect(immediateinput_event_connections, immediateinput_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventImmediateInput.Connect(immediateinput_event_connections, (InputEvent event) => {
		Log.Message("Handling ImmediateInput event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
immediateinput_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ImmediateInput event with a handler function
Input.EventImmediateInput.Connect(immediateinput_event_handler);

// remove subscription to the ImmediateInput event later by the handler function
Input.EventImmediateInput.Disconnect(immediateinput_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection immediateinput_event_connection;

// subscribe to the ImmediateInput event with a lambda handler function and keeping the connection
immediateinput_event_connection = Input.EventImmediateInput.Connect((InputEvent event) => {
		Log.Message("Handling ImmediateInput event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
immediateinput_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
immediateinput_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
immediateinput_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ImmediateInput events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventImmediateInput.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventImmediateInput.Enabled = true;

```

</details>

## 🔒︎ Event<int, int> EventJoyPovMotion

The event triggered when a joystick POV state value is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **joystick_id**, int **pov_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the JoyPovMotion event handler
void joypovmotion_event_handler(int joystick_id,  int pov_index)
{
	Log.Message("\Handling JoyPovMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joypovmotion_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventJoyPovMotion.Connect(joypovmotion_event_connections, joypovmotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventJoyPovMotion.Connect(joypovmotion_event_connections, (int joystick_id,  int pov_index) => {
		Log.Message("Handling JoyPovMotion event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
joypovmotion_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the JoyPovMotion event with a handler function
Input.EventJoyPovMotion.Connect(joypovmotion_event_handler);

// remove subscription to the JoyPovMotion event later by the handler function
Input.EventJoyPovMotion.Disconnect(joypovmotion_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection joypovmotion_event_connection;

// subscribe to the JoyPovMotion event with a lambda handler function and keeping the connection
joypovmotion_event_connection = Input.EventJoyPovMotion.Connect((int joystick_id,  int pov_index) => {
		Log.Message("Handling JoyPovMotion event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
joypovmotion_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
joypovmotion_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
joypovmotion_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring JoyPovMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventJoyPovMotion.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventJoyPovMotion.Enabled = true;

```

</details>

## 🔒︎ Event<int, int> EventJoyAxisMotion

The event triggered when a joystick axis state value is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **joystick_id**, int **axis**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the JoyAxisMotion event handler
void joyaxismotion_event_handler(int joystick_id,  int axis)
{
	Log.Message("\Handling JoyAxisMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joyaxismotion_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventJoyAxisMotion.Connect(joyaxismotion_event_connections, joyaxismotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventJoyAxisMotion.Connect(joyaxismotion_event_connections, (int joystick_id,  int axis) => {
		Log.Message("Handling JoyAxisMotion event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
joyaxismotion_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the JoyAxisMotion event with a handler function
Input.EventJoyAxisMotion.Connect(joyaxismotion_event_handler);

// remove subscription to the JoyAxisMotion event later by the handler function
Input.EventJoyAxisMotion.Disconnect(joyaxismotion_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection joyaxismotion_event_connection;

// subscribe to the JoyAxisMotion event with a lambda handler function and keeping the connection
joyaxismotion_event_connection = Input.EventJoyAxisMotion.Connect((int joystick_id,  int axis) => {
		Log.Message("Handling JoyAxisMotion event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
joyaxismotion_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
joyaxismotion_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
joyaxismotion_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring JoyAxisMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventJoyAxisMotion.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventJoyAxisMotion.Enabled = true;

```

</details>

## 🔒︎ Event<int, int> EventJoyButtonUp

The event triggered when a joystick button is released. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **joystick_id**, int **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the JoyButtonUp event handler
void joybuttonup_event_handler(int joystick_id,  int button)
{
	Log.Message("\Handling JoyButtonUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joybuttonup_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventJoyButtonUp.Connect(joybuttonup_event_connections, joybuttonup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventJoyButtonUp.Connect(joybuttonup_event_connections, (int joystick_id,  int button) => {
		Log.Message("Handling JoyButtonUp event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
joybuttonup_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the JoyButtonUp event with a handler function
Input.EventJoyButtonUp.Connect(joybuttonup_event_handler);

// remove subscription to the JoyButtonUp event later by the handler function
Input.EventJoyButtonUp.Disconnect(joybuttonup_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection joybuttonup_event_connection;

// subscribe to the JoyButtonUp event with a lambda handler function and keeping the connection
joybuttonup_event_connection = Input.EventJoyButtonUp.Connect((int joystick_id,  int button) => {
		Log.Message("Handling JoyButtonUp event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
joybuttonup_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
joybuttonup_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
joybuttonup_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring JoyButtonUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventJoyButtonUp.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventJoyButtonUp.Enabled = true;

```

</details>

## 🔒︎ Event<int, int> EventJoyButtonDown

The event triggered when a joystick button is pressed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **joystick_id**, int **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the JoyButtonDown event handler
void joybuttondown_event_handler(int joystick_id,  int button)
{
	Log.Message("\Handling JoyButtonDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joybuttondown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventJoyButtonDown.Connect(joybuttondown_event_connections, joybuttondown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventJoyButtonDown.Connect(joybuttondown_event_connections, (int joystick_id,  int button) => {
		Log.Message("Handling JoyButtonDown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
joybuttondown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the JoyButtonDown event with a handler function
Input.EventJoyButtonDown.Connect(joybuttondown_event_handler);

// remove subscription to the JoyButtonDown event later by the handler function
Input.EventJoyButtonDown.Disconnect(joybuttondown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection joybuttondown_event_connection;

// subscribe to the JoyButtonDown event with a lambda handler function and keeping the connection
joybuttondown_event_connection = Input.EventJoyButtonDown.Connect((int joystick_id,  int button) => {
		Log.Message("Handling JoyButtonDown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
joybuttondown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
joybuttondown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
joybuttondown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring JoyButtonDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventJoyButtonDown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventJoyButtonDown.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventJoyDisconnected

The event triggered when a joystick is disconnected. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **joystick_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the JoyDisconnected event handler
void joydisconnected_event_handler(int joystick_id)
{
	Log.Message("\Handling JoyDisconnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joydisconnected_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventJoyDisconnected.Connect(joydisconnected_event_connections, joydisconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventJoyDisconnected.Connect(joydisconnected_event_connections, (int joystick_id) => {
		Log.Message("Handling JoyDisconnected event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
joydisconnected_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the JoyDisconnected event with a handler function
Input.EventJoyDisconnected.Connect(joydisconnected_event_handler);

// remove subscription to the JoyDisconnected event later by the handler function
Input.EventJoyDisconnected.Disconnect(joydisconnected_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection joydisconnected_event_connection;

// subscribe to the JoyDisconnected event with a lambda handler function and keeping the connection
joydisconnected_event_connection = Input.EventJoyDisconnected.Connect((int joystick_id) => {
		Log.Message("Handling JoyDisconnected event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
joydisconnected_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
joydisconnected_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
joydisconnected_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring JoyDisconnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventJoyDisconnected.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventJoyDisconnected.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventJoyConnected

The event triggered when a joystick is connected. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **joystick_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the JoyConnected event handler
void joyconnected_event_handler(int joystick_id)
{
	Log.Message("\Handling JoyConnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joyconnected_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventJoyConnected.Connect(joyconnected_event_connections, joyconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventJoyConnected.Connect(joyconnected_event_connections, (int joystick_id) => {
		Log.Message("Handling JoyConnected event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
joyconnected_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the JoyConnected event with a handler function
Input.EventJoyConnected.Connect(joyconnected_event_handler);

// remove subscription to the JoyConnected event later by the handler function
Input.EventJoyConnected.Disconnect(joyconnected_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection joyconnected_event_connection;

// subscribe to the JoyConnected event with a lambda handler function and keeping the connection
joyconnected_event_connection = Input.EventJoyConnected.Connect((int joystick_id) => {
		Log.Message("Handling JoyConnected event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
joyconnected_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
joyconnected_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
joyconnected_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring JoyConnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventJoyConnected.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventJoyConnected.Enabled = true;

```

</details>

## 🔒︎ Event<int, int> EventVrDeviceAxisMotion

The event triggered when a VR device axis state value is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**, int **axis**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the VrDeviceAxisMotion event handler
void vrdeviceaxismotion_event_handler(int device_id,  int axis)
{
	Log.Message("\Handling VrDeviceAxisMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdeviceaxismotion_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventVrDeviceAxisMotion.Connect(vrdeviceaxismotion_event_connections, vrdeviceaxismotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventVrDeviceAxisMotion.Connect(vrdeviceaxismotion_event_connections, (int device_id,  int axis) => {
		Log.Message("Handling VrDeviceAxisMotion event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
vrdeviceaxismotion_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the VrDeviceAxisMotion event with a handler function
Input.EventVrDeviceAxisMotion.Connect(vrdeviceaxismotion_event_handler);

// remove subscription to the VrDeviceAxisMotion event later by the handler function
Input.EventVrDeviceAxisMotion.Disconnect(vrdeviceaxismotion_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection vrdeviceaxismotion_event_connection;

// subscribe to the VrDeviceAxisMotion event with a lambda handler function and keeping the connection
vrdeviceaxismotion_event_connection = Input.EventVrDeviceAxisMotion.Connect((int device_id,  int axis) => {
		Log.Message("Handling VrDeviceAxisMotion event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
vrdeviceaxismotion_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
vrdeviceaxismotion_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
vrdeviceaxismotion_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring VrDeviceAxisMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventVrDeviceAxisMotion.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventVrDeviceAxisMotion.Enabled = true;

```

</details>

## 🔒︎ Event<int, Input.VR_BUTTON > EventVrDeviceButtonTouchUp

The event triggered when a finger is withdrawn from a VR device button. If the finger is releasing a button that has been pressed, this event is triggered along with [EventVrDeviceButtonUp](#EventVrDeviceButtonUp). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**, Input.VR_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the VrDeviceButtonTouchUp event handler
void vrdevicebuttontouchup_event_handler(int device_id,  Input.VR_BUTTON button)
{
	Log.Message("\Handling VrDeviceButtonTouchUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicebuttontouchup_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventVrDeviceButtonTouchUp.Connect(vrdevicebuttontouchup_event_connections, vrdevicebuttontouchup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventVrDeviceButtonTouchUp.Connect(vrdevicebuttontouchup_event_connections, (int device_id,  Input.VR_BUTTON button) => {
		Log.Message("Handling VrDeviceButtonTouchUp event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
vrdevicebuttontouchup_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the VrDeviceButtonTouchUp event with a handler function
Input.EventVrDeviceButtonTouchUp.Connect(vrdevicebuttontouchup_event_handler);

// remove subscription to the VrDeviceButtonTouchUp event later by the handler function
Input.EventVrDeviceButtonTouchUp.Disconnect(vrdevicebuttontouchup_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection vrdevicebuttontouchup_event_connection;

// subscribe to the VrDeviceButtonTouchUp event with a lambda handler function and keeping the connection
vrdevicebuttontouchup_event_connection = Input.EventVrDeviceButtonTouchUp.Connect((int device_id,  Input.VR_BUTTON button) => {
		Log.Message("Handling VrDeviceButtonTouchUp event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
vrdevicebuttontouchup_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
vrdevicebuttontouchup_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
vrdevicebuttontouchup_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring VrDeviceButtonTouchUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventVrDeviceButtonTouchUp.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventVrDeviceButtonTouchUp.Enabled = true;

```

</details>

## 🔒︎ Event<int, Input.VR_BUTTON > EventVrDeviceButtonTouchDown

The event triggered when a VR device button is touched. If the button has been touched and pressed, [EventVrDeviceButtonDown](#EventVrDeviceButtonDown) is triggered along with this event. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**, Input.VR_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the VrDeviceButtonTouchDown event handler
void vrdevicebuttontouchdown_event_handler(int device_id,  Input.VR_BUTTON button)
{
	Log.Message("\Handling VrDeviceButtonTouchDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicebuttontouchdown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventVrDeviceButtonTouchDown.Connect(vrdevicebuttontouchdown_event_connections, vrdevicebuttontouchdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventVrDeviceButtonTouchDown.Connect(vrdevicebuttontouchdown_event_connections, (int device_id,  Input.VR_BUTTON button) => {
		Log.Message("Handling VrDeviceButtonTouchDown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
vrdevicebuttontouchdown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the VrDeviceButtonTouchDown event with a handler function
Input.EventVrDeviceButtonTouchDown.Connect(vrdevicebuttontouchdown_event_handler);

// remove subscription to the VrDeviceButtonTouchDown event later by the handler function
Input.EventVrDeviceButtonTouchDown.Disconnect(vrdevicebuttontouchdown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection vrdevicebuttontouchdown_event_connection;

// subscribe to the VrDeviceButtonTouchDown event with a lambda handler function and keeping the connection
vrdevicebuttontouchdown_event_connection = Input.EventVrDeviceButtonTouchDown.Connect((int device_id,  Input.VR_BUTTON button) => {
		Log.Message("Handling VrDeviceButtonTouchDown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
vrdevicebuttontouchdown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
vrdevicebuttontouchdown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
vrdevicebuttontouchdown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring VrDeviceButtonTouchDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventVrDeviceButtonTouchDown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventVrDeviceButtonTouchDown.Enabled = true;

```

</details>

## 🔒︎ Event<int, Input.VR_BUTTON > EventVrDeviceButtonUp

The event triggered when a VR device button is released. If the finger is withdrawn from the button that has been pressed, [EventVrDeviceButtonTouchUp](#EventVrDeviceButtonTouchUp) is triggered along with this event. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**, Input.VR_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the VrDeviceButtonUp event handler
void vrdevicebuttonup_event_handler(int device_id,  Input.VR_BUTTON button)
{
	Log.Message("\Handling VrDeviceButtonUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicebuttonup_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventVrDeviceButtonUp.Connect(vrdevicebuttonup_event_connections, vrdevicebuttonup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventVrDeviceButtonUp.Connect(vrdevicebuttonup_event_connections, (int device_id,  Input.VR_BUTTON button) => {
		Log.Message("Handling VrDeviceButtonUp event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
vrdevicebuttonup_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the VrDeviceButtonUp event with a handler function
Input.EventVrDeviceButtonUp.Connect(vrdevicebuttonup_event_handler);

// remove subscription to the VrDeviceButtonUp event later by the handler function
Input.EventVrDeviceButtonUp.Disconnect(vrdevicebuttonup_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection vrdevicebuttonup_event_connection;

// subscribe to the VrDeviceButtonUp event with a lambda handler function and keeping the connection
vrdevicebuttonup_event_connection = Input.EventVrDeviceButtonUp.Connect((int device_id,  Input.VR_BUTTON button) => {
		Log.Message("Handling VrDeviceButtonUp event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
vrdevicebuttonup_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
vrdevicebuttonup_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
vrdevicebuttonup_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring VrDeviceButtonUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventVrDeviceButtonUp.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventVrDeviceButtonUp.Enabled = true;

```

</details>

## 🔒︎ Event<int, Input.VR_BUTTON > EventVrDeviceButtonDown

The event triggered when a VR device button is pressed. If the button has not previously been touched, [EventVrDeviceButtonTouchDown](#EventVrDeviceButtonTouchDown) is triggered along with this event. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**, Input.VR_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the VrDeviceButtonDown event handler
void vrdevicebuttondown_event_handler(int device_id,  Input.VR_BUTTON button)
{
	Log.Message("\Handling VrDeviceButtonDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicebuttondown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventVrDeviceButtonDown.Connect(vrdevicebuttondown_event_connections, vrdevicebuttondown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventVrDeviceButtonDown.Connect(vrdevicebuttondown_event_connections, (int device_id,  Input.VR_BUTTON button) => {
		Log.Message("Handling VrDeviceButtonDown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
vrdevicebuttondown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the VrDeviceButtonDown event with a handler function
Input.EventVrDeviceButtonDown.Connect(vrdevicebuttondown_event_handler);

// remove subscription to the VrDeviceButtonDown event later by the handler function
Input.EventVrDeviceButtonDown.Disconnect(vrdevicebuttondown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection vrdevicebuttondown_event_connection;

// subscribe to the VrDeviceButtonDown event with a lambda handler function and keeping the connection
vrdevicebuttondown_event_connection = Input.EventVrDeviceButtonDown.Connect((int device_id,  Input.VR_BUTTON button) => {
		Log.Message("Handling VrDeviceButtonDown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
vrdevicebuttondown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
vrdevicebuttondown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
vrdevicebuttondown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring VrDeviceButtonDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventVrDeviceButtonDown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventVrDeviceButtonDown.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventVrDeviceDisconnected

The event triggered when a VR device is disconnected. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the VrDeviceDisconnected event handler
void vrdevicedisconnected_event_handler(int device_id)
{
	Log.Message("\Handling VrDeviceDisconnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicedisconnected_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventVrDeviceDisconnected.Connect(vrdevicedisconnected_event_connections, vrdevicedisconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventVrDeviceDisconnected.Connect(vrdevicedisconnected_event_connections, (int device_id) => {
		Log.Message("Handling VrDeviceDisconnected event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
vrdevicedisconnected_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the VrDeviceDisconnected event with a handler function
Input.EventVrDeviceDisconnected.Connect(vrdevicedisconnected_event_handler);

// remove subscription to the VrDeviceDisconnected event later by the handler function
Input.EventVrDeviceDisconnected.Disconnect(vrdevicedisconnected_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection vrdevicedisconnected_event_connection;

// subscribe to the VrDeviceDisconnected event with a lambda handler function and keeping the connection
vrdevicedisconnected_event_connection = Input.EventVrDeviceDisconnected.Connect((int device_id) => {
		Log.Message("Handling VrDeviceDisconnected event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
vrdevicedisconnected_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
vrdevicedisconnected_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
vrdevicedisconnected_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring VrDeviceDisconnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventVrDeviceDisconnected.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventVrDeviceDisconnected.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventVrDeviceConnected

The event triggered when a VR device is connected. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the VrDeviceConnected event handler
void vrdeviceconnected_event_handler(int device_id)
{
	Log.Message("\Handling VrDeviceConnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdeviceconnected_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventVrDeviceConnected.Connect(vrdeviceconnected_event_connections, vrdeviceconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventVrDeviceConnected.Connect(vrdeviceconnected_event_connections, (int device_id) => {
		Log.Message("Handling VrDeviceConnected event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
vrdeviceconnected_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the VrDeviceConnected event with a handler function
Input.EventVrDeviceConnected.Connect(vrdeviceconnected_event_handler);

// remove subscription to the VrDeviceConnected event later by the handler function
Input.EventVrDeviceConnected.Disconnect(vrdeviceconnected_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection vrdeviceconnected_event_connection;

// subscribe to the VrDeviceConnected event with a lambda handler function and keeping the connection
vrdeviceconnected_event_connection = Input.EventVrDeviceConnected.Connect((int device_id) => {
		Log.Message("Handling VrDeviceConnected event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
vrdeviceconnected_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
vrdeviceconnected_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
vrdeviceconnected_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring VrDeviceConnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventVrDeviceConnected.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventVrDeviceConnected.Enabled = true;

```

</details>

## 🔒︎ Event<int, int, int> EventGamepadTouchMotion

The event triggered when the finger touching the gamepad touch panel moves across it. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**, int **touch_id**, int **finger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the GamepadTouchMotion event handler
void gamepadtouchmotion_event_handler(int gamepad_id,  int touch_id,  int finger)
{
	Log.Message("\Handling GamepadTouchMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadtouchmotion_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventGamepadTouchMotion.Connect(gamepadtouchmotion_event_connections, gamepadtouchmotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventGamepadTouchMotion.Connect(gamepadtouchmotion_event_connections, (int gamepad_id,  int touch_id,  int finger) => {
		Log.Message("Handling GamepadTouchMotion event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
gamepadtouchmotion_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the GamepadTouchMotion event with a handler function
Input.EventGamepadTouchMotion.Connect(gamepadtouchmotion_event_handler);

// remove subscription to the GamepadTouchMotion event later by the handler function
Input.EventGamepadTouchMotion.Disconnect(gamepadtouchmotion_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection gamepadtouchmotion_event_connection;

// subscribe to the GamepadTouchMotion event with a lambda handler function and keeping the connection
gamepadtouchmotion_event_connection = Input.EventGamepadTouchMotion.Connect((int gamepad_id,  int touch_id,  int finger) => {
		Log.Message("Handling GamepadTouchMotion event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
gamepadtouchmotion_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
gamepadtouchmotion_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
gamepadtouchmotion_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring GamepadTouchMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventGamepadTouchMotion.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventGamepadTouchMotion.Enabled = true;

```

</details>

## 🔒︎ Event<int, int, int> EventGamepadTouchUp

The event triggered when the touch is withdrawn from the gamepad touch panel. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**, int **touch_id**, int **finger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the GamepadTouchUp event handler
void gamepadtouchup_event_handler(int gamepad_id,  int touch_id,  int finger)
{
	Log.Message("\Handling GamepadTouchUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadtouchup_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventGamepadTouchUp.Connect(gamepadtouchup_event_connections, gamepadtouchup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventGamepadTouchUp.Connect(gamepadtouchup_event_connections, (int gamepad_id,  int touch_id,  int finger) => {
		Log.Message("Handling GamepadTouchUp event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
gamepadtouchup_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the GamepadTouchUp event with a handler function
Input.EventGamepadTouchUp.Connect(gamepadtouchup_event_handler);

// remove subscription to the GamepadTouchUp event later by the handler function
Input.EventGamepadTouchUp.Disconnect(gamepadtouchup_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection gamepadtouchup_event_connection;

// subscribe to the GamepadTouchUp event with a lambda handler function and keeping the connection
gamepadtouchup_event_connection = Input.EventGamepadTouchUp.Connect((int gamepad_id,  int touch_id,  int finger) => {
		Log.Message("Handling GamepadTouchUp event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
gamepadtouchup_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
gamepadtouchup_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
gamepadtouchup_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring GamepadTouchUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventGamepadTouchUp.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventGamepadTouchUp.Enabled = true;

```

</details>

## 🔒︎ Event<int, int, int> EventGamepadTouchDown

The event triggered when the gamepad touch panel is touched. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**, int **touch_id**, int **finger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the GamepadTouchDown event handler
void gamepadtouchdown_event_handler(int gamepad_id,  int touch_id,  int finger)
{
	Log.Message("\Handling GamepadTouchDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadtouchdown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventGamepadTouchDown.Connect(gamepadtouchdown_event_connections, gamepadtouchdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventGamepadTouchDown.Connect(gamepadtouchdown_event_connections, (int gamepad_id,  int touch_id,  int finger) => {
		Log.Message("Handling GamepadTouchDown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
gamepadtouchdown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the GamepadTouchDown event with a handler function
Input.EventGamepadTouchDown.Connect(gamepadtouchdown_event_handler);

// remove subscription to the GamepadTouchDown event later by the handler function
Input.EventGamepadTouchDown.Disconnect(gamepadtouchdown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection gamepadtouchdown_event_connection;

// subscribe to the GamepadTouchDown event with a lambda handler function and keeping the connection
gamepadtouchdown_event_connection = Input.EventGamepadTouchDown.Connect((int gamepad_id,  int touch_id,  int finger) => {
		Log.Message("Handling GamepadTouchDown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
gamepadtouchdown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
gamepadtouchdown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
gamepadtouchdown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring GamepadTouchDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventGamepadTouchDown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventGamepadTouchDown.Enabled = true;

```

</details>

## 🔒︎ Event<int, Input.GAMEPAD_AXIS > EventGamepadAxisMotion

The event triggered when a gamepad axis state value is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**, Input.GAMEPAD_AXIS **axis**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the GamepadAxisMotion event handler
void gamepadaxismotion_event_handler(int gamepad_id,  Input.GAMEPAD_AXIS axis)
{
	Log.Message("\Handling GamepadAxisMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadaxismotion_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventGamepadAxisMotion.Connect(gamepadaxismotion_event_connections, gamepadaxismotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventGamepadAxisMotion.Connect(gamepadaxismotion_event_connections, (int gamepad_id,  Input.GAMEPAD_AXIS axis) => {
		Log.Message("Handling GamepadAxisMotion event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
gamepadaxismotion_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the GamepadAxisMotion event with a handler function
Input.EventGamepadAxisMotion.Connect(gamepadaxismotion_event_handler);

// remove subscription to the GamepadAxisMotion event later by the handler function
Input.EventGamepadAxisMotion.Disconnect(gamepadaxismotion_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection gamepadaxismotion_event_connection;

// subscribe to the GamepadAxisMotion event with a lambda handler function and keeping the connection
gamepadaxismotion_event_connection = Input.EventGamepadAxisMotion.Connect((int gamepad_id,  Input.GAMEPAD_AXIS axis) => {
		Log.Message("Handling GamepadAxisMotion event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
gamepadaxismotion_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
gamepadaxismotion_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
gamepadaxismotion_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring GamepadAxisMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventGamepadAxisMotion.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventGamepadAxisMotion.Enabled = true;

```

</details>

## 🔒︎ Event<int, Input.GAMEPAD_BUTTON > EventGamepadButtonUp

The event triggered when a gamepad button is released. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**, Input.GAMEPAD_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the GamepadButtonUp event handler
void gamepadbuttonup_event_handler(int gamepad_id,  Input.GAMEPAD_BUTTON button)
{
	Log.Message("\Handling GamepadButtonUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadbuttonup_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventGamepadButtonUp.Connect(gamepadbuttonup_event_connections, gamepadbuttonup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventGamepadButtonUp.Connect(gamepadbuttonup_event_connections, (int gamepad_id,  Input.GAMEPAD_BUTTON button) => {
		Log.Message("Handling GamepadButtonUp event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
gamepadbuttonup_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the GamepadButtonUp event with a handler function
Input.EventGamepadButtonUp.Connect(gamepadbuttonup_event_handler);

// remove subscription to the GamepadButtonUp event later by the handler function
Input.EventGamepadButtonUp.Disconnect(gamepadbuttonup_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection gamepadbuttonup_event_connection;

// subscribe to the GamepadButtonUp event with a lambda handler function and keeping the connection
gamepadbuttonup_event_connection = Input.EventGamepadButtonUp.Connect((int gamepad_id,  Input.GAMEPAD_BUTTON button) => {
		Log.Message("Handling GamepadButtonUp event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
gamepadbuttonup_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
gamepadbuttonup_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
gamepadbuttonup_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring GamepadButtonUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventGamepadButtonUp.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventGamepadButtonUp.Enabled = true;

```

</details>

## 🔒︎ Event<int, Input.GAMEPAD_BUTTON > EventGamepadButtonDown

The event triggered when a gamepad button is pressed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**, Input.GAMEPAD_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the GamepadButtonDown event handler
void gamepadbuttondown_event_handler(int gamepad_id,  Input.GAMEPAD_BUTTON button)
{
	Log.Message("\Handling GamepadButtonDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadbuttondown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventGamepadButtonDown.Connect(gamepadbuttondown_event_connections, gamepadbuttondown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventGamepadButtonDown.Connect(gamepadbuttondown_event_connections, (int gamepad_id,  Input.GAMEPAD_BUTTON button) => {
		Log.Message("Handling GamepadButtonDown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
gamepadbuttondown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the GamepadButtonDown event with a handler function
Input.EventGamepadButtonDown.Connect(gamepadbuttondown_event_handler);

// remove subscription to the GamepadButtonDown event later by the handler function
Input.EventGamepadButtonDown.Disconnect(gamepadbuttondown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection gamepadbuttondown_event_connection;

// subscribe to the GamepadButtonDown event with a lambda handler function and keeping the connection
gamepadbuttondown_event_connection = Input.EventGamepadButtonDown.Connect((int gamepad_id,  Input.GAMEPAD_BUTTON button) => {
		Log.Message("Handling GamepadButtonDown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
gamepadbuttondown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
gamepadbuttondown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
gamepadbuttondown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring GamepadButtonDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventGamepadButtonDown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventGamepadButtonDown.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventGamepadDisconnected

The event triggered when a gamepad is disconnected. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the GamepadDisconnected event handler
void gamepaddisconnected_event_handler(int gamepad_id)
{
	Log.Message("\Handling GamepadDisconnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepaddisconnected_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventGamepadDisconnected.Connect(gamepaddisconnected_event_connections, gamepaddisconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventGamepadDisconnected.Connect(gamepaddisconnected_event_connections, (int gamepad_id) => {
		Log.Message("Handling GamepadDisconnected event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
gamepaddisconnected_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the GamepadDisconnected event with a handler function
Input.EventGamepadDisconnected.Connect(gamepaddisconnected_event_handler);

// remove subscription to the GamepadDisconnected event later by the handler function
Input.EventGamepadDisconnected.Disconnect(gamepaddisconnected_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection gamepaddisconnected_event_connection;

// subscribe to the GamepadDisconnected event with a lambda handler function and keeping the connection
gamepaddisconnected_event_connection = Input.EventGamepadDisconnected.Connect((int gamepad_id) => {
		Log.Message("Handling GamepadDisconnected event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
gamepaddisconnected_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
gamepaddisconnected_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
gamepaddisconnected_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring GamepadDisconnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventGamepadDisconnected.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventGamepadDisconnected.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventGamepadConnected

The event triggered when a gamepad is connected. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the GamepadConnected event handler
void gamepadconnected_event_handler(int gamepad_id)
{
	Log.Message("\Handling GamepadConnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadconnected_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventGamepadConnected.Connect(gamepadconnected_event_connections, gamepadconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventGamepadConnected.Connect(gamepadconnected_event_connections, (int gamepad_id) => {
		Log.Message("Handling GamepadConnected event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
gamepadconnected_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the GamepadConnected event with a handler function
Input.EventGamepadConnected.Connect(gamepadconnected_event_handler);

// remove subscription to the GamepadConnected event later by the handler function
Input.EventGamepadConnected.Disconnect(gamepadconnected_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection gamepadconnected_event_connection;

// subscribe to the GamepadConnected event with a lambda handler function and keeping the connection
gamepadconnected_event_connection = Input.EventGamepadConnected.Connect((int gamepad_id) => {
		Log.Message("Handling GamepadConnected event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
gamepadconnected_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
gamepadconnected_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
gamepadconnected_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring GamepadConnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventGamepadConnected.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventGamepadConnected.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventTouchMotion

The event triggered when the touch is moved. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **touch_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TouchMotion event handler
void touchmotion_event_handler(int touch_id)
{
	Log.Message("\Handling TouchMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections touchmotion_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventTouchMotion.Connect(touchmotion_event_connections, touchmotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventTouchMotion.Connect(touchmotion_event_connections, (int touch_id) => {
		Log.Message("Handling TouchMotion event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
touchmotion_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TouchMotion event with a handler function
Input.EventTouchMotion.Connect(touchmotion_event_handler);

// remove subscription to the TouchMotion event later by the handler function
Input.EventTouchMotion.Disconnect(touchmotion_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection touchmotion_event_connection;

// subscribe to the TouchMotion event with a lambda handler function and keeping the connection
touchmotion_event_connection = Input.EventTouchMotion.Connect((int touch_id) => {
		Log.Message("Handling TouchMotion event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
touchmotion_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
touchmotion_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
touchmotion_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TouchMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventTouchMotion.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventTouchMotion.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventTouchUp

The event triggered when the touch is released. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **touch_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TouchUp event handler
void touchup_event_handler(int touch_id)
{
	Log.Message("\Handling TouchUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections touchup_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventTouchUp.Connect(touchup_event_connections, touchup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventTouchUp.Connect(touchup_event_connections, (int touch_id) => {
		Log.Message("Handling TouchUp event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
touchup_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TouchUp event with a handler function
Input.EventTouchUp.Connect(touchup_event_handler);

// remove subscription to the TouchUp event later by the handler function
Input.EventTouchUp.Disconnect(touchup_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection touchup_event_connection;

// subscribe to the TouchUp event with a lambda handler function and keeping the connection
touchup_event_connection = Input.EventTouchUp.Connect((int touch_id) => {
		Log.Message("Handling TouchUp event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
touchup_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
touchup_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
touchup_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TouchUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventTouchUp.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventTouchUp.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventTouchDown

The event triggered when the touch is pressed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **touch_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TouchDown event handler
void touchdown_event_handler(int touch_id)
{
	Log.Message("\Handling TouchDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections touchdown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventTouchDown.Connect(touchdown_event_connections, touchdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventTouchDown.Connect(touchdown_event_connections, (int touch_id) => {
		Log.Message("Handling TouchDown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
touchdown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TouchDown event with a handler function
Input.EventTouchDown.Connect(touchdown_event_handler);

// remove subscription to the TouchDown event later by the handler function
Input.EventTouchDown.Disconnect(touchdown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection touchdown_event_connection;

// subscribe to the TouchDown event with a lambda handler function and keeping the connection
touchdown_event_connection = Input.EventTouchDown.Connect((int touch_id) => {
		Log.Message("Handling TouchDown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
touchdown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
touchdown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
touchdown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TouchDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventTouchDown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventTouchDown.Enabled = true;

```

</details>

## 🔒︎ Event<uint> EventTextPress

The event triggered when the key that has a corresponding printable symbol is pressed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(uint **unicode**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TextPress event handler
void textpress_event_handler(uint unicode)
{
	Log.Message("\Handling TextPress event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections textpress_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventTextPress.Connect(textpress_event_connections, textpress_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventTextPress.Connect(textpress_event_connections, (uint unicode) => {
		Log.Message("Handling TextPress event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
textpress_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TextPress event with a handler function
Input.EventTextPress.Connect(textpress_event_handler);

// remove subscription to the TextPress event later by the handler function
Input.EventTextPress.Disconnect(textpress_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection textpress_event_connection;

// subscribe to the TextPress event with a lambda handler function and keeping the connection
textpress_event_connection = Input.EventTextPress.Connect((uint unicode) => {
		Log.Message("Handling TextPress event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
textpress_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
textpress_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
textpress_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TextPress events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventTextPress.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventTextPress.Enabled = true;

```

</details>

## 🔒︎ Event<uint> EventKeyRepeat

The event triggered when the key is pressed repeatedly. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(uint **unicode**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the KeyRepeat event handler
void keyrepeat_event_handler(uint unicode)
{
	Log.Message("\Handling KeyRepeat event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections keyrepeat_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventKeyRepeat.Connect(keyrepeat_event_connections, keyrepeat_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventKeyRepeat.Connect(keyrepeat_event_connections, (uint unicode) => {
		Log.Message("Handling KeyRepeat event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
keyrepeat_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the KeyRepeat event with a handler function
Input.EventKeyRepeat.Connect(keyrepeat_event_handler);

// remove subscription to the KeyRepeat event later by the handler function
Input.EventKeyRepeat.Disconnect(keyrepeat_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection keyrepeat_event_connection;

// subscribe to the KeyRepeat event with a lambda handler function and keeping the connection
keyrepeat_event_connection = Input.EventKeyRepeat.Connect((uint unicode) => {
		Log.Message("Handling KeyRepeat event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
keyrepeat_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
keyrepeat_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
keyrepeat_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring KeyRepeat events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventKeyRepeat.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventKeyRepeat.Enabled = true;

```

</details>

## 🔒︎ Event< Input.KEY > EventKeyUp

The event triggered when the key is released. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Input.KEY **key**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the KeyUp event handler
void keyup_event_handler(Input.KEY key)
{
	Log.Message("\Handling KeyUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections keyup_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventKeyUp.Connect(keyup_event_connections, keyup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventKeyUp.Connect(keyup_event_connections, (Input.KEY key) => {
		Log.Message("Handling KeyUp event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
keyup_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the KeyUp event with a handler function
Input.EventKeyUp.Connect(keyup_event_handler);

// remove subscription to the KeyUp event later by the handler function
Input.EventKeyUp.Disconnect(keyup_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection keyup_event_connection;

// subscribe to the KeyUp event with a lambda handler function and keeping the connection
keyup_event_connection = Input.EventKeyUp.Connect((Input.KEY key) => {
		Log.Message("Handling KeyUp event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
keyup_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
keyup_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
keyup_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring KeyUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventKeyUp.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventKeyUp.Enabled = true;

```

</details>

## 🔒︎ Event< Input.KEY > EventKeyDown

The event triggered when the key is pressed and held. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Input.KEY **key**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the KeyDown event handler
void keydown_event_handler(Input.KEY key)
{
	Log.Message("\Handling KeyDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections keydown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventKeyDown.Connect(keydown_event_connections, keydown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventKeyDown.Connect(keydown_event_connections, (Input.KEY key) => {
		Log.Message("Handling KeyDown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
keydown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the KeyDown event with a handler function
Input.EventKeyDown.Connect(keydown_event_handler);

// remove subscription to the KeyDown event later by the handler function
Input.EventKeyDown.Disconnect(keydown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection keydown_event_connection;

// subscribe to the KeyDown event with a lambda handler function and keeping the connection
keydown_event_connection = Input.EventKeyDown.Connect((Input.KEY key) => {
		Log.Message("Handling KeyDown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
keydown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
keydown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
keydown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring KeyDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventKeyDown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventKeyDown.Enabled = true;

```

</details>

## 🔒︎ Event<int, int> EventMouseMotion

The event triggered when the mouse is moved. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **coord_x**, int **coord_y**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the MouseMotion event handler
void mousemotion_event_handler(int coord_x, int coord_y)
{
	Log.Message("\Handling MouseMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mousemotion_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventMouseMotion.Connect(mousemotion_event_connections, mousemotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventMouseMotion.Connect(mousemotion_event_connections, (int coord_x, int coord_y) => {
		Log.Message("Handling MouseMotion event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
mousemotion_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the MouseMotion event with a handler function
Input.EventMouseMotion.Connect(mousemotion_event_handler);

// remove subscription to the MouseMotion event later by the handler function
Input.EventMouseMotion.Disconnect(mousemotion_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection mousemotion_event_connection;

// subscribe to the MouseMotion event with a lambda handler function and keeping the connection
mousemotion_event_connection = Input.EventMouseMotion.Connect((int coord_x, int coord_y) => {
		Log.Message("Handling MouseMotion event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
mousemotion_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
mousemotion_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
mousemotion_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring MouseMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventMouseMotion.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventMouseMotion.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventMouseWheelHorizontal

The event triggered when the mouse wheel is moved horizontally. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **delta_horizontal**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the MouseWheelHorizontal event handler
void mousewheelhorizontal_event_handler(int delta_horizontal)
{
	Log.Message("\Handling MouseWheelHorizontal event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mousewheelhorizontal_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventMouseWheelHorizontal.Connect(mousewheelhorizontal_event_connections, mousewheelhorizontal_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventMouseWheelHorizontal.Connect(mousewheelhorizontal_event_connections, (int delta_horizontal) => {
		Log.Message("Handling MouseWheelHorizontal event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
mousewheelhorizontal_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the MouseWheelHorizontal event with a handler function
Input.EventMouseWheelHorizontal.Connect(mousewheelhorizontal_event_handler);

// remove subscription to the MouseWheelHorizontal event later by the handler function
Input.EventMouseWheelHorizontal.Disconnect(mousewheelhorizontal_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection mousewheelhorizontal_event_connection;

// subscribe to the MouseWheelHorizontal event with a lambda handler function and keeping the connection
mousewheelhorizontal_event_connection = Input.EventMouseWheelHorizontal.Connect((int delta_horizontal) => {
		Log.Message("Handling MouseWheelHorizontal event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
mousewheelhorizontal_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
mousewheelhorizontal_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
mousewheelhorizontal_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring MouseWheelHorizontal events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventMouseWheelHorizontal.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventMouseWheelHorizontal.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventMouseWheel

The event triggered when the mouse scroll wheel is moved. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **delta_vertical**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the MouseWheel event handler
void mousewheel_event_handler(int delta_vertical)
{
	Log.Message("\Handling MouseWheel event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mousewheel_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventMouseWheel.Connect(mousewheel_event_connections, mousewheel_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventMouseWheel.Connect(mousewheel_event_connections, (int delta_vertical) => {
		Log.Message("Handling MouseWheel event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
mousewheel_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the MouseWheel event with a handler function
Input.EventMouseWheel.Connect(mousewheel_event_handler);

// remove subscription to the MouseWheel event later by the handler function
Input.EventMouseWheel.Disconnect(mousewheel_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection mousewheel_event_connection;

// subscribe to the MouseWheel event with a lambda handler function and keeping the connection
mousewheel_event_connection = Input.EventMouseWheel.Connect((int delta_vertical) => {
		Log.Message("Handling MouseWheel event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
mousewheel_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
mousewheel_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
mousewheel_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring MouseWheel events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventMouseWheel.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventMouseWheel.Enabled = true;

```

</details>

## 🔒︎ Event< Input.MOUSE_BUTTON > EventMouseUp

The event triggered when the mouse button is released. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Input.MOUSE_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the MouseUp event handler
void mouseup_event_handler(Input.MOUSE_BUTTON button)
{
	Log.Message("\Handling MouseUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mouseup_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventMouseUp.Connect(mouseup_event_connections, mouseup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventMouseUp.Connect(mouseup_event_connections, (Input.MOUSE_BUTTON button) => {
		Log.Message("Handling MouseUp event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
mouseup_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the MouseUp event with a handler function
Input.EventMouseUp.Connect(mouseup_event_handler);

// remove subscription to the MouseUp event later by the handler function
Input.EventMouseUp.Disconnect(mouseup_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection mouseup_event_connection;

// subscribe to the MouseUp event with a lambda handler function and keeping the connection
mouseup_event_connection = Input.EventMouseUp.Connect((Input.MOUSE_BUTTON button) => {
		Log.Message("Handling MouseUp event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
mouseup_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
mouseup_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
mouseup_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring MouseUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventMouseUp.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventMouseUp.Enabled = true;

```

</details>

## 🔒︎ Event< Input.MOUSE_BUTTON > EventMouseDown

The event triggered when the mouse button is pressed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Input.MOUSE_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the MouseDown event handler
void mousedown_event_handler(Input.MOUSE_BUTTON button)
{
	Log.Message("\Handling MouseDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mousedown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventMouseDown.Connect(mousedown_event_connections, mousedown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventMouseDown.Connect(mousedown_event_connections, (Input.MOUSE_BUTTON button) => {
		Log.Message("Handling MouseDown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
mousedown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the MouseDown event with a handler function
Input.EventMouseDown.Connect(mousedown_event_handler);

// remove subscription to the MouseDown event later by the handler function
Input.EventMouseDown.Disconnect(mousedown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection mousedown_event_connection;

// subscribe to the MouseDown event with a lambda handler function and keeping the connection
mousedown_event_connection = Input.EventMouseDown.Connect((Input.MOUSE_BUTTON button) => {
		Log.Message("Handling MouseDown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
mousedown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
mousedown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
mousedown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring MouseDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventMouseDown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventMouseDown.Enabled = true;

```

</details>

## 🔒︎ Event<string, int, int> EventTextEditing

The event triggered while the user is composing text via an IME (Input Method Editor). The handler receives the current UTF-8 composition (preedit) text, the cursor position within it, and the length of the selected portion (both in codepoints). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience.

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **text**, int **cursor**, int **length**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TextEditing event handler
void textediting_event_handler(string text, int cursor, int length)
{
	Log.Message("\Handling TextEditing event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections textediting_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input.EventTextEditing.Connect(textediting_event_connections, textediting_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input.EventTextEditing.Connect(textediting_event_connections, (string text, int cursor, int length) => {
		Log.Message("Handling TextEditing event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
textediting_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TextEditing event with a handler function
Input.EventTextEditing.Connect(textediting_event_handler);

// remove subscription to the TextEditing event later by the handler function
Input.EventTextEditing.Disconnect(textediting_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection textediting_event_connection;

// subscribe to the TextEditing event with a lambda handler function and keeping the connection
textediting_event_connection = Input.EventTextEditing.Connect((string text, int cursor, int length) => {
		Log.Message("Handling TextEditing event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
textediting_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
textediting_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
textediting_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TextEditing events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input.EventTextEditing.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Input.EventTextEditing.Enabled = true;

```

</details>

### Members

---

## InputGamePad GetGamePad ( int num )

Returns a gamepad of the given index.
### Arguments

- *int* **num** - Gamepad index.

### Return value

[InputGamepad](../../../api/library/controls/class.inputgamepad_cs.md) object.
## InputJoystick GetJoystick ( int num )

Returns a joystick with the given index.
### Arguments

- *int* **num** - Joystick index.

### Return value

[InputJoystick](../../../api/library/controls/class.inputjoystick_cs.md) object.
## bool IsKeyPressed ( Input.KEY key )

Returns a value indicating if the given key is pressed. Check this value to perform continuous actions.
```csharp
if (Input.IsKeyPressed(Input.KEY.ENTER)) {
	Log.Message("the Enter key is held down\n");
}

```


### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the [Input.KEY](#KEY) enum values.

### Return value

true if the key is pressed; otherwise, false.
## bool IsKeyDown ( Input.KEY key )

Returns a value indicating if the given key was pressed during the current frame. Check this value to perform one-time actions on pressing a key.
```csharp
if (Input.IsKeyDown(Input.KEY.SPACE)) {
	Log.Message("the Space key was pressed\n");
}

```


### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the [Input.KEY](#KEY) enum values.

### Return value

True during the first frame when the key was pressed, false for the following ones until it is released and pressed again.
## bool IsKeyUp ( Input.KEY key )

Returns a value indicating if the given key was released during the current frame. Check this value to perform one-time actions on releasing a key.
```csharp
if (Input.IsKeyUp(Input.KEY.F)) {
	Log.Message("the F key was released\n");
}

```


### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the [Input.KEY](#KEY) enum values.

### Return value

true during the first frame when the key was released; otherwise, false.
## bool IsMouseButtonPressed ( Input.MOUSE_BUTTON button )

Returns a value indicating if the given mouse button is pressed. Check this value to perform continuous actions.
```csharp
if (Input.IsMouseButtonPressed(Input.MOUSE_BUTTON.LEFT)) {
	Log.Message("the left mouse button is held down\n");
}

```


### Arguments

- *[Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON)* **button** - One of the [Input.MOUSE_BUTTON](#MOUSE_BUTTON) enum values.

### Return value

True if the mouse button is pressed; otherwise, false.
## bool IsMouseButtonDown ( Input.MOUSE_BUTTON button )

Returns a value indicating if the given mouse button was pressed during the current frame. Check this value to perform one-time actions on pressing a mouse button.
```csharp
if (Input.IsMouseButtonDown(Input.MOUSE_BUTTON.LEFT)) {
	Log.Message("the left mouse button was pressed\n");
}

```


### Arguments

- *[Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON)* **button** - One of the [Input.MOUSE_BUTTON](#MOUSE_BUTTON) enum values.

### Return value

True during the first frame when the mouse button was released; otherwise, false.
## bool IsMouseButtonUp ( Input.MOUSE_BUTTON button )

Returns a value indicating if the given mouse button was released during the current frame. Check this value to perform one-time actions on releasing a mouse button.
```csharp
if (Input.IsMouseButtonUp(Input.MOUSE_BUTTON.LEFT)) {
	Log.Message("left mouse button was released\n");
}

```


### Arguments

- *[Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON)* **button** - One of the [Input.MOUSE_BUTTON](#MOUSE_BUTTON) enum values.

### Return value

True during the first frame when the mouse button was released; otherwise, false.
## bool IsTouchPressed ( int index )

Returns a value indicating if the touchscreen is pressed by the finger.
### Arguments

- *int* **index** - Touch input index.

### Return value

true if the touchscreen is pressed; otherwise, false.
## bool IsTouchDown ( int index )

Returns a value indicating if the given touch was pressed during the current frame.
### Arguments

- *int* **index** - Touch input index.

### Return value

true if the touchscreen is pressed during the current frame; otherwise, false.
## bool IsTouchUp ( int index )

Returns a value indicating if the given touch was released.
### Arguments

- *int* **index** - Touch input index.

### Return value

true during the first frame when the touch was released; otherwise, false.
## ivec2 GetTouchPosition ( int index )

Returns a vector containing integer values of touch position.
### Arguments

- *int* **index** - Touch input index.

### Return value

The touch position.
## ivec2 GetTouchDelta ( int index )

Returns a vector containing screen position change of the touch along the X and Y axes � the difference between the values in the previous and the current frames.
### Arguments

- *int* **index** - Touch input index.

### Return value

The touch position delta.
## InputEventTouch GetTouchEvent ( int index )

Returns the action cast to the touch event.
### Arguments

- *int* **index** - Touch input index.

### Return value

Touch input event.
## int GetTouchEvents ( int index , InputEventTouch [] OUT_events )

Returns the actions cast to the touch event.
### Arguments

- *int* **index** - Touch input index.
- *[InputEventTouch](../../../api/library/controls/class.inputeventtouch_cs.md)[]* **OUT_events** - The buffer with touch input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of touch input events.
## InputEventKeyboard GetKeyEvent ( Input.KEY key )

Returns the currently processed keyboard input event.
### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the [Input.KEY](#KEY) enum values.

### Return value

Keyboard input event, or null if there are no events for the specified key in the current frame.
## int GetKeyEvents ( Input.KEY key , InputEventKeyboard [] OUT_events )

Returns the buffer with events for the specified key.
### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the [Input.KEY](#KEY) enum values.
- *[InputEventKeyboard](../../../api/library/controls/class.inputeventkeyboard_cs.md)[]* **OUT_events** - The buffer with input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## string GetKeyName ( Input.KEY key )

Returns the specified key name.
### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the [Input.KEY](#KEY) enum values.

### Return value

Key name.
## Input.KEY GetKeyByName ( string name )

Returns the key by its name.
### Arguments

- *string* **name** - Key name.

### Return value

One of the [Input.KEY](#KEY) enum values.
## InputEventMouseButton GetMouseButtonEvent ( Input.MOUSE_BUTTON button )

Returns the mouse motion input event for the specified button.
### Arguments

- *[Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON)* **button** - One of the [Input.MOUSE_BUTTON](#MOUSE_BUTTON) enum values.

### Return value

Mouse motion input event.
## string GetMouseButtonName ( Input.MOUSE_BUTTON button )

Returns the mouse button name.
### Arguments

- *[Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON)* **button** - One of the [Input.MOUSE_BUTTON](#MOUSE_BUTTON) enum values.

### Return value

Mouse button name.
## Input.MOUSE_BUTTON GetMouseButtonByName ( string name )

Returns the mouse button by its name.
### Arguments

- *string* **name** - Mouse button name.

### Return value

One of the [Input.MOUSE_BUTTON](#MOUSE_BUTTON) enum values.
## int GetEventsBuffer ( int frame , InputEvent [] OUT_events )

Returns the buffer with the input events for the specified frame.
### Arguments

- *int* **frame** - Number of frame for which the buffer of input events is to be obtained. Input events are stored for the last 60 frames. 0 is the current frame, 1 is the previous frame, etc.
- *[InputEvent](../../../api/library/controls/class.inputevent_cs.md)[]* **OUT_events** - The buffer with input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SendEvent ( InputEvent e )

Creates a user event and dispatches it to the Engine.
### Arguments

- *[InputEvent](../../../api/library/controls/class.inputevent_cs.md)* **e** - Input event.

## void SetEventsFilter ( IntPtr func )

Sets a callback function to be executed on receiving input events. This input event filter enables you to reject certain input events for the Engine and get necessary information on all input events.
### Arguments

- *IntPtr* **func** - Input event callback.

## bool IsModifierEnabled ( Input.MODIFIER modifier )

Returns the value indicating if the specified modifier is enabled.
### Arguments

- *[Input.MODIFIER](../../../api/library/controls/class.input_cs.md#MODIFIER)* **modifier** - One of the [MODIFIER.](#MODIFIER_LEFT_SHIFT) enum values.

### Return value

true if the modifier is enabled; otherwise, false.
## uint KeyToUnicode ( Input.KEY key )

Returns the specified key transformed to unicode.
### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the [Input.KEY](#KEY) enum values.

### Return value

Unicode symbol.
## Input.KEY UnicodeToKey ( uint unicode )

Returns the specified key transformed to unicode.
### Arguments

- *uint* **unicode** - Unicode symbol.

### Return value

One of the [Input.KEY](#KEY) enum values.
## void SetMouseCursorSkinCustom ( Image image )

Sets a custom image to be used for the mouse cursor.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image containing pointer shapes to be set for the mouse cursor (e.g., select, move, resize, etc.).

## void SetMouseCursorSkinSystem ( )

Sets the current OS cursor skin (pointer shapes like select, move, resize, etc.).
## void SetMouseCursorSkinDefault ( )

Sets the default Engine cursor skin (pointer shapes like select, move, resize, etc.).
## void SetMouseCursorCustom ( Image image , int x = 0 , int y = 0 )

Sets a custom image for the OS mouse cursor. The image must be of the square size and *RGBA8* format.
```csharp
// create an instance of the Image class
Image cursor = new Image("textures/my_cursor.png");
// set the image as the mouse cursor
Input.SetMouseCursorCustom(cursor);
// show the OS mouse pointer
Input.MouseCursorSystem = true;

```


### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Cursor image to be set.
- *int* **x** - X coordinate of the cursor's hot spot.
- *int* **y** - Y coordinate of the cursor's hot spot.

## void ClearMouseCursorCustom ( )

Clears the custom mouse cursor set via the [setMouseCursorCustom()](#setMouseCursorCustom_Image_int_int_void) method.
## void UpdateMouseCursor ( )

Updates the mouse cursor. This method should be called after making changes to the mouse cursor to apply them all together. After calling this method the cursor shall be updated in the next frame.
## string GetKeyLocalName ( Input.KEY key )

Returns the name for the specified key taken from the currently selected keyboard layout.
> **Notice:** The returned value is affected by the modifier such as Shift.


### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the [Input.KEY](#KEY) enum values.

### Return value

Localized name for the specified key.
## int GetMouseButtonEvents ( Input.MOUSE_BUTTON button , InputEventMouseButton [] OUT_events )

Returns the number of input events for the specified mouse button and puts the events to the specified output buffer.
### Arguments

- *[Input.MOUSE_BUTTON](../../../api/library/controls/class.input_cs.md#MOUSE_BUTTON)* **button** - One of the [Input.MOUSE_BUTTON](#MOUSE_BUTTON) enum values.
- *[InputEventMouseButton](../../../api/library/controls/class.inputeventmousebutton_cs.md)[]* **OUT_events** - Buffer with input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified mouse button.
## ivec2 GetForceMousePosition ( )

Returns the absolute mouse position obtained from the OS.
### Return value

The absolute mouse position.
## bool IsKeyText ( Input.KEY key )

Returns a value indicating if the given key has a corresponding printable symbol (current Num Lock state is taken into account). For example, pressing 2 on the numpad with *Num Lock* enabled produces "2", while with disabled *Num Lock* the same key acts as a down arrow. Keys like *Esc, PrintScreen, BackSpace* do not produce any printable symbol at all.
### Arguments

- *[Input.KEY](../../../api/library/controls/class.input_cs.md#KEY)* **key** - One of the [Input.KEY](#KEY) enum values.

### Return value

true if the key value is a symbol; otherwise, false.
## string GetModifierName ( Input.MODIFIER modifier )

Returns the name of the key modifier by its scancode.
### Arguments

- *[Input.MODIFIER](../../../api/library/controls/class.input_cs.md#MODIFIER)* **modifier** - Scancode of the modifier.

### Return value

Key name of the modifier.
## Input.MODIFIER GetModifierByName ( string name )

Returns the scancode of the key modifier by its name.
### Arguments

- *string* **name** - Key name of the modifier.

### Return value

Scancode of the modifier.
## InputVRDevice GetVRDevice ( int num )

Returns the VR device by its number.
### Arguments

- *int* **num** - Number of the VR device.

### Return value

VR device.
## void SetIMETextInputRect ( int position_x , int position_y , int width , int height )

Tells the operating system where the text caret or edit area is located, so that the IME composition and candidate window can be positioned next to it. Has no effect if text input is not currently active.
### Arguments

- *int* **position_x** - Horizontal position of the top-left corner of the text input rectangle, in render pixels relative to the engine window.
- *int* **position_y** - Vertical position of the top-left corner of the text input rectangle, in render pixels relative to the engine window.
- *int* **width** - Width of the text input rectangle, in pixels.
- *int* **height** - Height of the text input rectangle, in pixels.
