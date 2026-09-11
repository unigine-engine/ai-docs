# Unigine::Input Class (CPP)

**Header:** #include <UnigineInput.h>

> **Notice:** This class is a singleton.


The Input class contains functions for simple manual handling of user inputs using a keyboard, a mouse or a gamepad.


### See Also


- A set of C++ samples (`<SAMPLES_PROJECT_PATH>/source/input_controls/`)
- A set of C# Component samples (`<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/input_controls/`)


### Usage Examples


The following example shows a way to move and rotate a node by using the Input class:


```cpp
#include "AppWorldLogic.h"
#include <UnigineInput.h>

#include <UnigineConsole.h>

#include <UnigineGame.h>
#include <UniginePrimitives.h>

using namespace Unigine;

using namespace Math;

NodePtr box;

float move_speed = 1.0f;
float turn_speed = 30.0f;

int AppWorldLogic::init()
{

	box = Primitives::createBox(vec3_one);

	return 1;
}

int AppWorldLogic::update()
{

	if (Console::isActive())
		return 1;

	if (Input::isKeyPressed(Input::KEY_UP) || Input::isKeyPressed(Input::KEY_W))
		box->translate(Vec3_forward * move_speed * Game::getIFps());

	if (Input::isKeyPressed(Input::KEY_DOWN) || Input::isKeyPressed(Input::KEY_S))
		box->translate(Vec3_back * move_speed * Game::getIFps());

	if (Input::isKeyPressed(Input::KEY_LEFT) || Input::isKeyPressed(Input::KEY_A))
		box->rotate(0.0f, 0.0f, turn_speed * Game::getIFps());

	if (Input::isKeyPressed(Input::KEY_RIGHT) || Input::isKeyPressed(Input::KEY_D))
		box->rotate(0.0f, 0.0f, -turn_speed * Game::getIFps());

	return 1;
}

```


The following code demonstrates how to receive an event that changed the button state to [isKeyDown()](#isKeyDown_int_int), [isKeyUp()](#isKeyUp_int_int). Such code can also be used for the mouse and touch buttons.


```cpp
#include "AppWorldLogic.h"
#include <UnigineInput.h>

#include <UnigineConsole.h>

using namespace Unigine;

int AppWorldLogic::update()
{

	if (Input::isKeyDown(Input::KEY_T) || Input::isKeyUp(Input::KEY_T))
	{
		InputEventKeyboardPtr e = Input::getKeyEvent(Input::KEY_T);
		Console::messageLine("%s %d time = %lld frame = %lld", Input::getKeyName(e->getKey()), e->getAction(), e->getTimestamp(), e->getFrame());
	}

	return 1;
}

```


The following code illustrates receiving the immediate input � the user receives the event notification immediately after filtering:


```cpp
#include "AppWorldLogic.h"
#include <UnigineInput.h>

#include <UnigineConsole.h>

using namespace Unigine;

int AppWorldLogic::init()
{

	Input::getEventImmediateInput().connect(on_immediate_input);

	return 1;
}

```


The following code illustrates how the event filter works. Pressing the "W" button and mouse movements will be declined, i.e. these events won't be taken as input:


```cpp
#include "AppWorldLogic.h"
#include <UnigineInput.h>

using namespace Unigine;

int event_filter(InputEventPtr& e)
{
	switch (e->getType())
	{
	case InputEvent::INPUT_EVENT_KEYBOARD:
	{
		// skip 'W' key repeat events
		InputEventKeyboardPtr k = checked_ptr_cast<InputEventKeyboard>(e);
		if (k->getKey() == Input::KEY_W && k->getAction() == InputEventKeyboard::ACTION_REPEAT)
			return 1;
		break;
	}

	case InputEvent::INPUT_EVENT_MOUSE_MOTION:
	{
		// skip all mouse motion events
		return 1;
	}

	default: break;
	}

	return 0;
}

int AppWorldLogic::init()
{

	Input::setEventsFilter(event_filter);

	return 1;
}

```


The following code is an example of input events creation. We'll imitate the input of the `show_profiler 1` console command as if it were an event from the keyboard.


```cpp
#include "AppWorldLogic.h"
#include <UnigineInput.h>

using namespace Unigine;

enum
{
	STATE_OPEN_CONSOLE = 0,
	STATE_TYPING_COMMAND,
	STATE_APPLY_COMMAND,
	STATE_FINISH,
};

int state = STATE_OPEN_CONSOLE;

void emulate_key_input(Input::KEY key)
{
	InputEventKeyboardPtr key_down = InputEventKeyboard::create();
	key_down->setAction(InputEventKeyboard::ACTION_DOWN);
	key_down->setKey(key);

	InputEventKeyboardPtr key_repeat = InputEventKeyboard::create();
	key_repeat->setAction(InputEventKeyboard::ACTION_REPEAT);
	key_repeat->setKey(key);

	InputEventKeyboardPtr key_up = InputEventKeyboard::create();
	key_up->setAction(InputEventKeyboard::ACTION_UP);
	key_up->setKey(key);

	Input::sendEvent(key_down);
	Input::sendEvent(key_repeat);
	Input::sendEvent(key_up);
}

void emulate_text_input(const char *text)
{
	int size = strlen(text);
	for (int i = 0; i < size; i++)
	{
		InputEventTextPtr text_input = InputEventText::create();
		text_input->setUnicode(text[i]);
		Input::sendEvent(text_input);
	}
}

int AppWorldLogic::update()
{

	switch (state)
	{
		case STATE_OPEN_CONSOLE:
		{
			emulate_key_input(Input::KEY_BACK_QUOTE);
			state = STATE_TYPING_COMMAND;
			break;
		}

		case STATE_TYPING_COMMAND:
		{
			emulate_text_input("show_profiler 1");
			state = STATE_APPLY_COMMAND;
			break;
		}

		case STATE_APPLY_COMMAND:
		{
			emulate_key_input(Input::KEY_ENTER);
			state = STATE_FINISH;
			break;
		}

		default: break;
	}

	return 1;
}

```


The following code demonstrates how to obtain various button names using the [getKeyName()](#getKeyName_int_cstr), [keyToUnicode()](#keyToUnicode_int_uint), and [getKeyLocalName()](#getKeyLocalName_int_cstr) methods:


```cpp
#include "AppWorldLogic.h"
#include <UnigineInput.h>

#include <UnigineConsole.h>

using namespace Unigine;

int AppWorldLogic::init()
{

	Console::setOnscreen(true);

	return 1;
}

int AppWorldLogic::update()
{

	auto print_info = [](const char* state, Input::KEY key)
	{
		unsigned int unicode = Input::keyToUnicode(key);
		Console::message("%s: (key='%s', unicode='%s', local_name='%s') ",
			state,
			Input::getKeyName(key),
			String::unicodeToUtf8(unicode).get(),
			Input::getKeyLocalName(key));
	};

	print_info("Up", Input::KEY_W);
	print_info("Jump", Input::KEY_SPACE);
	print_info("Run", Input::KEY_RIGHT_SHIFT);
	Console::message("\n");

	return 1;
}

```


## Input Class

### Enums

## MOUSE_HANDLE

| Name | Description |
|---|---|
| **MOUSE_HANDLE_GRAB** = 0 | The mouse is grabbed when clicked (the cursor disappears and camera movement is controlled by the mouse). |
| **MOUSE_HANDLE_SOFT** = 1 | The mouse cursor disappears after being idle for a short time period. |
| **MOUSE_HANDLE_USER** = 2 | The mouse is not handled by the system (allows input handling by some custom module). |

## MOUSE_BUTTON

| Name | Description |
|---|---|
| **MOUSE_BUTTON_UNKNOWN** = 0 | Unknown mouse button. |
| **MOUSE_BUTTON_LEFT** = 1 | Left mouse button. |
| **MOUSE_BUTTON_MIDDLE** = 2 | Middle mouse button. |
| **MOUSE_BUTTON_RIGHT** = 3 | Right mouse button. |
| **MOUSE_BUTTON_DCLICK** = 4 | Left mouse button double click. |
| **MOUSE_BUTTON_AUX_0** = 5 | Auxiliary mouse button. |
| **MOUSE_BUTTON_AUX_1** = 6 | Auxiliary mouse button. |
| **MOUSE_BUTTON_AUX_2** = 7 | Auxiliary mouse button. |
| **MOUSE_BUTTON_AUX_3** = 8 | Auxiliary mouse button. |
| **MOUSE_NUM_BUTTONS** = 9 | Number of mouse buttons. |

## MODIFIER

| Name | Description |
|---|---|
| **MODIFIER_LEFT_SHIFT** = 0 | Left *Shift* key used as modifier. |
| **MODIFIER_RIGHT_SHIFT** = 1 | Right *Shift* key used as modifier. |
| **MODIFIER_LEFT_CTRL** = 2 | Left *Ctrl* key used as modifier. |
| **MODIFIER_RIGHT_CTRL** = 3 | Right *Ctrl* key used as modifier. |
| **MODIFIER_LEFT_ALT** = 4 | Left *Alt* key used as modifier. |
| **MODIFIER_RIGHT_ALT** = 5 | Right *Alt* key used as modifier. |
| **MODIFIER_LEFT_CMD** = 6 | Left Command key used as modifier. |
| **MODIFIER_RIGHT_CMD** = 7 | Right Command key used as modifier. |
| **MODIFIER_NUM_LOCK** = 8 | *Num Lock* key used as modifier. |
| **MODIFIER_CAPS_LOCK** = 9 | *Caps Lock* key used as modifier. |
| **MODIFIER_SCROLL_LOCK** = 10 | *Scroll Lock* key used as modifier. |
| **MODIFIER_ALT_GR** = 11 | *Alt Gr* key used as modifier. |
| **MODIFIER_ANY_SHIFT** = 12 | Any *Shift* key used as modifier. |
| **MODIFIER_ANY_CTRL** = 13 | Any *Ctrl* key used as modifier. |
| **MODIFIER_ANY_ALT** = 14 | Any *Alt* key used as modifier. |
| **MODIFIER_ANY_CMD** = 15 | Any Command key used as modifier. |
| **MODIFIER_NONE** = 16 | No modifier is specified. |
| **NUM_MODIFIERS** = 17 | Total number of modifiers. |

## KEY

| Name | Description |
|---|---|
| **KEY_UNKNOWN** = 0 | Unknown key |
| **KEY_ESC** = 1 | *Escape* key |
| **KEY_F1** = 2 | **F1** key |
| **KEY_F2** = 3 | **F2** key |
| **KEY_F3** = 4 | **F3** key |
| **KEY_F4** = 5 | **F4** key |
| **KEY_F5** = 6 | **F5** key |
| **KEY_F6** = 7 | **F6** key |
| **KEY_F7** = 8 | **F7** key |
| **KEY_F8** = 9 | **F8** key |
| **KEY_F9** = 10 | **F9** key |
| **KEY_F10** = 11 | **F10** key |
| **KEY_F11** = 12 | **F11** key |
| **KEY_F12** = 13 | **F12** key |
| **KEY_PRINTSCREEN** = 14 | *Print Screen* key |
| **KEY_SCROLL_LOCK** = 15 | *Scroll Lock* key |
| **KEY_PAUSE** = 16 | *Pause* key |
| **KEY_BACK_QUOTE** = 17 | Back quote key |
| **KEY_DIGIT_1** = 18 | The **1** key of the alphanumeric keyboard |
| **KEY_DIGIT_2** = 19 | The **2** key of the alphanumeric keyboard |
| **KEY_DIGIT_3** = 20 | The **3** key of the alphanumeric keyboard |
| **KEY_DIGIT_4** = 21 | The **4** key of the alphanumeric keyboard |
| **KEY_DIGIT_5** = 22 | The **5** key of the alphanumeric keyboard |
| **KEY_DIGIT_6** = 23 | The **6** key of the alphanumeric keyboard |
| **KEY_DIGIT_7** = 24 | The **7** key of the alphanumeric keyboard |
| **KEY_DIGIT_8** = 25 | The **8** key of the alphanumeric keyboard |
| **KEY_DIGIT_9** = 26 | The **9** key of the alphanumeric keyboard |
| **KEY_DIGIT_0** = 27 | The **0** key of the alphanumeric keyboard |
| **KEY_MINUS** = 28 | Minus key |
| **KEY_EQUALS** = 29 | Equals key |
| **KEY_BACKSPACE** = 30 | Backspace key |
| **KEY_TAB** = 31 | *Tab* key |
| **KEY_Q** = 32 | *Q* key |
| **KEY_W** = 33 | *W* key |
| **KEY_E** = 34 | *E* key |
| **KEY_R** = 35 | *R* key |
| **KEY_T** = 36 | *T* key |
| **KEY_Y** = 37 | *Y* key |
| **KEY_U** = 38 | *U* key |
| **KEY_I** = 39 | *I* key |
| **KEY_O** = 40 | *O* key |
| **KEY_P** = 41 | *P* key |
| **KEY_LEFT_BRACKET** = 42 | Left square bracket key |
| **KEY_RIGHT_BRACKET** = 43 | Right square bracket key |
| **KEY_ENTER** = 44 | *Enter* key |
| **KEY_CAPS_LOCK** = 45 | *Caps Lock* key |
| **KEY_A** = 46 | *A* key |
| **KEY_S** = 47 | *S* key |
| **KEY_D** = 48 | *D* key |
| **KEY_F** = 49 | *F* key |
| **KEY_G** = 50 | *G* key |
| **KEY_H** = 51 | *H* key |
| **KEY_J** = 52 | *J* key |
| **KEY_K** = 53 | *K* key |
| **KEY_L** = 54 | *L* key |
| **KEY_SEMICOLON** = 55 | Semicolon key |
| **KEY_QUOTE** = 56 | Quote key |
| **KEY_BACK_SLASH** = 57 | Backward slash key |
| **KEY_LEFT_SHIFT** = 58 | Left *Shift* key |
| **KEY_LESS** = 59 | Less than key |
| **KEY_Z** = 60 | **Z** key |
| **KEY_X** = 61 | **X** key |
| **KEY_C** = 62 | **C** key |
| **KEY_V** = 63 | **V** key |
| **KEY_B** = 64 | **B** key |
| **KEY_N** = 65 | **N** key |
| **KEY_M** = 66 | **M** key |
| **KEY_COMMA** = 67 | Comma key |
| **KEY_DOT** = 68 | Dot key |
| **KEY_SLASH** = 69 | Slash key |
| **KEY_RIGHT_SHIFT** = 70 | Right *Shift* key |
| **KEY_LEFT_CTRL** = 71 | Left *Ctrl* key |
| **KEY_LEFT_CMD** = 72 | Left Command key |
| **KEY_LEFT_ALT** = 73 | Left *Alt* key |
| **KEY_SPACE** = 74 | Space key |
| **KEY_RIGHT_ALT** = 75 | Right *Alt* key |
| **KEY_RIGHT_CMD** = 76 | Right Command key |
| **KEY_MENU** = 77 | Menu key |
| **KEY_RIGHT_CTRL** = 78 | Right *Ctrl* key |
| **KEY_INSERT** = 79 | *Insert* key |
| **KEY_DELETE** = 80 | *Delete* key |
| **KEY_HOME** = 81 | *Home* key |
| **KEY_END** = 82 | *End* key |
| **KEY_PGUP** = 83 | Page Up key |
| **KEY_PGDOWN** = 84 | Page down |
| **KEY_UP** = 85 | Up arrow key |
| **KEY_LEFT** = 86 | Left arrow key |
| **KEY_DOWN** = 87 | Down arrow key |
| **KEY_RIGHT** = 88 | Right arrow key |
| **KEY_NUM_LOCK** = 89 | *Num Lock* key |
| **KEY_NUMPAD_DIVIDE** = 90 | Divide key of the numeric keypad |
| **KEY_NUMPAD_MULTIPLY** = 91 | Multiply key of the numeric keypad |
| **KEY_NUMPAD_MINUS** = 92 | Minus key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_7** = 93 | The **7** key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_8** = 94 | The **8** key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_9** = 95 | The **9** key of the numeric keypad |
| **KEY_NUMPAD_PLUS** = 96 | Plus key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_4** = 97 | The **4** key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_5** = 98 | The **5** key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_6** = 99 | The **6** key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_1** = 100 | The **1** key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_2** = 101 | The **2** key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_3** = 102 | The **3** key of the numeric keypad |
| **KEY_NUMPAD_ENTER** = 103 | *Enter* key of the numeric keypad |
| **KEY_NUMPAD_DIGIT_0** = 104 | The **0** key of the numeric keypad |
| **KEY_NUMPAD_DOT** = 105 | Dot key of the numeric keypad |
| **KEY_ANY_SHIFT** = 106 | Any *Shift* key |
| **KEY_ANY_CTRL** = 107 | Any *Ctrl* key |
| **KEY_ANY_ALT** = 108 | Any *Alt* key |
| **KEY_ANY_CMD** = 109 | Any Command key |
| **KEY_ANY_UP** = 110 | Any up arrow key |
| **KEY_ANY_LEFT** = 111 | Any left arrow key |
| **KEY_ANY_DOWN** = 112 | Any down arrow key |
| **KEY_ANY_RIGHT** = 113 | Any right arrow key |
| **KEY_ANY_ENTER** = 114 | Any up arrow key |
| **KEY_ANY_DELETE** = 115 | Any *Delete* key |
| **KEY_ANY_INSERT** = 116 | Any *Insert* key |
| **KEY_ANY_HOME** = 117 | Any *Home* key |
| **KEY_ANY_END** = 118 | Any *End* key |
| **KEY_ANY_PGUP** = 119 | Any Page Up key |
| **KEY_ANY_PGDOWN** = 120 | Any Page Down key |
| **KEY_ANY_DIGIT_1** = 121 | The **1** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_DIGIT_2** = 122 | The **2** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_DIGIT_3** = 123 | The **3** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_DIGIT_4** = 124 | The **4** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_DIGIT_5** = 125 | The **5** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_DIGIT_6** = 126 | The **6** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_DIGIT_7** = 127 | The **7** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_DIGIT_8** = 128 | The **8** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_DIGIT_9** = 129 | The **9** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_DIGIT_0** = 130 | The **0** key of either alphanumeric keyboard or numeric keypad |
| **KEY_ANY_MINUS** = 131 | Any minus key |
| **KEY_ANY_EQUALS** = 132 | Any Equals key |
| **KEY_ANY_DOT** = 133 | Any dot key |
| **NUM_KEYS** = 134 | Number of keys. |

## DEVICE

| Name | Description |
|---|---|
| **DEVICE_UNKNOWN** = 0 | Unknown device. |
| **DEVICE_GAME_CONTROLLER** = 1 | Game controller device. |
| **DEVICE_WHEEL** = 2 | Wheel device. |
| **DEVICE_ARCADE_STICK** = 3 | Arcade stick device. |
| **DEVICE_FLIGHT_STICK** = 4 | Flight stick device. |
| **DEVICE_DANCE_PAD** = 5 | Dance pad device. |
| **DEVICE_GUITAR** = 6 | Guitar. |
| **DEVICE_DRUM_KIT** = 7 | Drum kit. |
| **DEVICE_VR** = 8 | VR device. |

## GAMEPAD_BUTTON

Buttons of the gamepad.
| Name | Description |
|---|---|
| **GAMEPAD_BUTTON_A** = 0 | Button A of the gamepad. |
| **GAMEPAD_BUTTON_B** = 1 | Button B of the gamepad. |
| **GAMEPAD_BUTTON_X** = 2 | Button X of the gamepad. |
| **GAMEPAD_BUTTON_Y** = 3 | Button Y of the gamepad. |
| **GAMEPAD_BUTTON_BACK** = 4 | Button "Back" of the gamepad. |
| **GAMEPAD_BUTTON_START** = 5 | Button "Start" of the gamepad. |
| **GAMEPAD_BUTTON_DPAD_UP** = 6 | Button "Up" of the gamepad. |
| **GAMEPAD_BUTTON_DPAD_DOWN** = 7 | Button "Down" of the gamepad. |
| **GAMEPAD_BUTTON_DPAD_LEFT** = 8 | Button "Left" of the gamepad. |
| **GAMEPAD_BUTTON_DPAD_RIGHT** = 9 | Button "Right" of the gamepad. |
| **GAMEPAD_BUTTON_THUMB_LEFT** = 10 | Left thumbstick button of the gamepad. |
| **GAMEPAD_BUTTON_THUMB_RIGHT** = 11 | Right thumbstick button of the gamepad. |
| **GAMEPAD_BUTTON_SHOULDER_LEFT** = 12 | Left shoulder (bumper) button of the gamepad. |
| **GAMEPAD_BUTTON_SHOULDER_RIGHT** = 13 | Right shoulder (bumper) button of the gamepad. |
| **GAMEPAD_BUTTON_GUIDE** = 14 | Button "Guide" of the gamepad. |
| **GAMEPAD_BUTTON_MISC1** = 15 | The miscellaneous button of the gamepad. |
| **GAMEPAD_BUTTON_TOUCHPAD** = 16 | Touchpad of the gamepad. |
| **NUM_GAMEPAD_BUTTONS** = 17 | Number of buttons on a gamepad. |

## GAMEPAD_AXIS

| Name | Description |
|---|---|
| **GAMEPAD_AXIS_LEFT_X** = 0 | X axis of the left stick of the gamepad. |
| **GAMEPAD_AXIS_LEFT_Y** = 1 | Y axis of the left stick of the gamepad. |
| **GAMEPAD_AXIS_RIGHT_X** = 2 | X axis of the right stick of the gamepad. |
| **GAMEPAD_AXIS_RIGHT_Y** = 3 | Y axis of the right stick of the gamepad. |
| **GAMEPAD_AXIS_LEFT_TRIGGER** = 4 | Left trigger of the gamepad. |
| **GAMEPAD_AXIS_RIGHT_TRIGGER** = 5 | Right trigger of the gamepad. |
| **NUM_GAMEPAD_AXES** = 6 | Number of axes on a gamepad. |

## JOYSTICK_POV

POV (Point-of-View) switch or DPad states.
| Name | Description |
|---|---|
| **JOYSTICK_POV_NOT_PRESSED** = 0 | POV (Point-of-View) hat switch or D-Pad (directional pad) button is not pressed. |
| **JOYSTICK_POV_UP** = 1 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in up position. |
| **JOYSTICK_POV_UP_RIGHT** = 2 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in right-up position. |
| **JOYSTICK_POV_RIGHT** = 3 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in right position. |
| **JOYSTICK_POV_DOWN_RIGHT** = 4 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in down-right position. |
| **JOYSTICK_POV_DOWN** = 5 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in down position. |
| **JOYSTICK_POV_DOWN_LEFT** = 6 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in down-left position. |
| **JOYSTICK_POV_LEFT** = 7 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in left position. |
| **JOYSTICK_POV_UP_LEFT** = 8 | POV (Point-of-View) hat switch or D-Pad (directional pad) is in left-up position. |

## VR_BUTTON

| Name | Description |
|---|---|
| **VR_BUTTON_SYSTEM** = 0 | System button. |
| **VR_BUTTON_START** = 1 | Start button. |
| **VR_BUTTON_HOME** = 2 | Home button. |
| **VR_BUTTON_END** = 3 | End button. |
| **VR_BUTTON_SELECT** = 4 | Select button. |
| **VR_BUTTON_VOLUME_UP** = 5 | Volume Up button. |
| **VR_BUTTON_VOLUME_DOWN** = 6 | Volume Up button. |
| **VR_BUTTON_MUTE_MIC** = 7 | Mute Microphone button. |
| **VR_BUTTON_PLAY_PAUSE** = 8 | Play/Pause button. |
| **VR_BUTTON_MENU** = 9 | Menu button. |
| **VR_BUTTON_VIEW** = 10 | View button. |
| **VR_BUTTON_BACK** = 11 | Back button. |
| **VR_BUTTON_X** = 12 | X button reserved for the controller. |
| **VR_BUTTON_Y** = 13 | Y button reserved for the controller. |
| **VR_BUTTON_SHOULDER** = 14 | Shoulder button reserved for the controller. |
| **VR_BUTTON_GRIP** = 15 | Grip button reserved for the controller. |
| **VR_BUTTON_AXIS_0** = 16 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_1** = 17 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_2** = 18 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_3** = 19 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_4** = 20 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_5** = 21 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_6** = 22 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_7** = 23 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_8** = 24 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_9** = 25 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_10** = 26 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_11** = 27 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_12** = 28 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_13** = 29 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_14** = 30 | The axis reserved for the controller. |
| **VR_BUTTON_AXIS_15** = 31 | The axis reserved for the controller. |
| **VR_BUTTON_DPAD_UP** = 32 | Sensor panel up button. |
| **VR_BUTTON_DPAD_DOWN** = 33 | Sensor panel down button. |
| **VR_BUTTON_DPAD_LEFT** = 34 | Sensor panel left button. |
| **VR_BUTTON_DPAD_RIGHT** = 35 | Sensor panel right button. |
| **VR_BUTTON_DPAD_CENTER** = 36 | Sensor panel center button. |
| **VR_BUTTON_THUMBREST** = 37 | Thumb rest, a place for the user to rest their thumb. |
| **VR_BUTTON_THUMB_RESTING_SURFACES** = 38 | Thumb resting surfaces � any surfaces that a thumb may naturally rest on. This may include, but is not limited to, face buttons, thumbstick, and thumbrest. |
| **VR_BUTTON_PROXIMITY_SENSOR** = 39 | Proximity sensor. |
| **VR_BUTTON_APPLICATION** = 40 | Application menu button. |
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

### Members

## void setIMEEnabled ( bool imeenabled )

Sets a new value indicating if the system IME (Input Method Editor, used for composed text input such as CJK) is enabled. When enabled, the OS can open its composition and candidate window, and the engine receives *[text editing](../../../api/library/controls/class.inputeventtextediting_cpp.md)* (preedit) events while the user composes text. Disabled by default.
### Arguments

- *bool* **imeenabled** - Set **true** to enable IME text composition; **false** - to disable it.

## bool isIMEEnabled () const

Returns the current value indicating if the system IME (Input Method Editor, used for composed text input such as CJK) is enabled. When enabled, the OS can open its composition and candidate window, and the engine receives *[text editing](../../../api/library/controls/class.inputeventtextediting_cpp.md)* (preedit) events while the user composes text. Disabled by default.
### Return value

**true** if IME text composition is enabled ; otherwise **false**.
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
## Math:: ivec2 getMouseDeltaPosition () const

Returns the current vector containing delta values of the mouse cursor position.
### Return value

Current vector containing screen position change of the mouse pointer along the X and Y axes � the difference between the values in the previous and the current frames.
## void setMousePosition ( const Math:: ivec2 & position )

Sets a new vector containing integer values of the mouse cursor position.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **position** - The Returns a vector containing the global coordinates of the mouse cursor. In case of a mouse button event, the cursor position at the moment of the processed event is returned. In case of no such event, the mouse position at the beginning of the frame is returned. To get the cursor position during another type of event, get this event (for example [getKeyEvent()](#getKeyEvent_int_InputEventKeyboard)) and get the cursor position stored inside it.

## Math:: ivec2 getMousePosition () const

Returns the current vector containing integer values of the mouse cursor position.
### Return value

Current Returns a vector containing the global coordinates of the mouse cursor. In case of a mouse button event, the cursor position at the moment of the processed event is returned. In case of no such event, the mouse position at the beginning of the frame is returned. To get the cursor position during another type of event, get this event (for example [getKeyEvent()](#getKeyEvent_int_InputEventKeyboard)) and get the cursor position stored inside it.
## void setMouseHandle ( Input::MOUSE_HANDLE handle )

Sets a new mouse behavior mode, one of the [MOUSE_HANDLE](#MOUSE_HANDLE) values.
### Arguments

- *[Input::MOUSE_HANDLE](../../../api/library/controls/class.input_cpp.md#MOUSE_HANDLE)* **handle** - The mouse behavior mode, one of the [MOUSE_HANDLE](#MOUSE_HANDLE) values.

## Input::MOUSE_HANDLE getMouseHandle () const

Returns the current mouse behavior mode, one of the [MOUSE_HANDLE](#MOUSE_HANDLE) values.
### Return value

Current mouse behavior mode, one of the [MOUSE_HANDLE](#MOUSE_HANDLE) values.
## void setMouseCursorNeedUpdate ( bool update )

Sets a new value indicating that changes were made to the cursor (it was shown, hidden, changed to system, or anything else) and it has to be updated. Suppose the cursor was modified, for example, by the *Interface* plugin. After closing the plugin's window the cursor shall not return to its previous state because SDL doesn't even know about the changes. You can use this flag to signalize, that mouse cursor must be updated.
### Arguments

- *bool* **update** - Set **true** to enable changes were made to the cursor (it was shown, hidden, changed to system, or anything else) and it has to be updated; **false** - to disable it.

## bool isMouseCursorNeedUpdate () const

Returns the current value indicating that changes were made to the cursor (it was shown, hidden, changed to system, or anything else) and it has to be updated. Suppose the cursor was modified, for example, by the *Interface* plugin. After closing the plugin's window the cursor shall not return to its previous state because SDL doesn't even know about the changes. You can use this flag to signalize, that mouse cursor must be updated.
### Return value

**true** if changes were made to the cursor (it was shown, hidden, changed to system, or anything else) and it has to be updated; otherwise **false**.
## void setMouseCursorSystem ( bool system )

Sets a new value indicating if the OS mouse pointer is displayed.
### Arguments

- *bool* **system** - Set **true** to enable value indicating if the OS mouse pointer is displayed; **false** - to disable it.

## bool isMouseCursorSystem () const

Returns the current value indicating if the OS mouse pointer is displayed.
### Return value

**true** if value indicating if the OS mouse pointer is displayed; otherwise **false**.
## void setMouseCursorHide ( bool hide )

Sets a new value indicating if the mouse cursor is hidden in the current frame.
### Arguments

- *bool* **hide** - Set **true** to enable value indicating if the mouse cursor is hidden in the current frame; **false** - to disable it.

## bool isMouseCursorHide () const

Returns the current value indicating if the mouse cursor is hidden in the current frame.
### Return value

**true** if value indicating if the mouse cursor is hidden in the current frame; otherwise **false**.
## void setMouseGrab ( bool grab )

Sets a new value indicating if the mouse pointer is bound to the application window (can't leave it).
### Arguments

- *bool* **grab** - Set **true** to enable value indicating if the mouse pointer is bound to the application window; **false** - to disable it.

## bool isMouseGrab () const

Returns the current value indicating if the mouse pointer is bound to the application window (can't leave it).
### Return value

**true** if value indicating if the mouse pointer is bound to the application window; otherwise **false**.
## void setClipboard ( const char * clipboard )

Sets a new contents of the system clipboard.
### Arguments

- *const char ** **clipboard** - The contents of the system clipboard.

## const char * getClipboard () const

Returns the current contents of the system clipboard.
### Return value

Current contents of the system clipboard.
## bool isEmptyClipboard () const

Returns the current value indicating if the clipboard is empty.
### Return value

**true** if the clipboard is empty; otherwise **false**.
## Math:: ivec2 getMouseDeltaRaw () const

Returns the current change in the absolute mouse position (not the screen cursor), dots per inch.
### Return value

Current change in the absolute mouse position (not the screen cursor), dots per inch.
## Ptr < InputVRController > getVRControllerTreadmill () const

Returns the current treadmill VR controller.
### Return value

Current treadmill VR controller.
## Ptr < InputVRController > getVRControllerRight () const

Returns the current right-hand VR controller.
### Return value

Current right-hand VR controller.
## Ptr < InputVRController > getVRControllerLeft () const

Returns the current left-hand VR controller.
### Return value

Current left-hand VR controller.
## Ptr < InputVRHead > getVRHead () const

Returns the current head VR controller.
### Return value

Current head VR controller.
## int getNumVRDevices () const

Returns the current number of all VR devices.
### Return value

Current number of all VR devices.
## static Event<const Ptr < InputEvent > &> getEventImmediateInput () const

event triggered immediately at input as received from proxy before being processed by the engine. This event can be triggered in different threads depending on the proxy implementation. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<InputEvent> & **event**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ImmediateInput event handler
void immediateinput_event_handler(const Ptr<InputEvent> & event)
{
	Log::message("\Handling ImmediateInput event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections immediateinput_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventImmediateInput().connect(immediateinput_event_connections, immediateinput_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventImmediateInput().connect(immediateinput_event_connections, [](const Ptr<InputEvent> & event) {
		Log::message("\Handling ImmediateInput event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
immediateinput_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection immediateinput_event_connection;

// subscribe to the ImmediateInput event with a handler function keeping the connection
Input::getEventImmediateInput().connect(immediateinput_event_connection, immediateinput_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
immediateinput_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
immediateinput_event_connection.setEnabled(true);

// ...

// remove subscription to the ImmediateInput event via the connection
immediateinput_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A ImmediateInput event handler implemented as a class member
	void event_handler(const Ptr<InputEvent> & event)
	{
		Log::message("\Handling ImmediateInput event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventImmediateInput().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId immediateinput_handler_id;

// subscribe to the ImmediateInput event with a lambda handler function and keeping connection ID
immediateinput_handler_id = Input::getEventImmediateInput().connect(e_connections, [](const Ptr<InputEvent> & event) {
		Log::message("\Handling ImmediateInput event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventImmediateInput().disconnect(immediateinput_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ImmediateInput events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventImmediateInput().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventImmediateInput().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventJoyPovMotion () const

event triggered when a joystick POV state value is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int **joystick_id**, int **pov_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the JoyPovMotion event handler
void joypovmotion_event_handler(int joystick_id,  int pov_index)
{
	Log::message("\Handling JoyPovMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joypovmotion_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventJoyPovMotion().connect(joypovmotion_event_connections, joypovmotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventJoyPovMotion().connect(joypovmotion_event_connections, [](int joystick_id,  int pov_index) {
		Log::message("\Handling JoyPovMotion event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
joypovmotion_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection joypovmotion_event_connection;

// subscribe to the JoyPovMotion event with a handler function keeping the connection
Input::getEventJoyPovMotion().connect(joypovmotion_event_connection, joypovmotion_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
joypovmotion_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
joypovmotion_event_connection.setEnabled(true);

// ...

// remove subscription to the JoyPovMotion event via the connection
joypovmotion_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A JoyPovMotion event handler implemented as a class member
	void event_handler(int joystick_id,  int pov_index)
	{
		Log::message("\Handling JoyPovMotion event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventJoyPovMotion().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId joypovmotion_handler_id;

// subscribe to the JoyPovMotion event with a lambda handler function and keeping connection ID
joypovmotion_handler_id = Input::getEventJoyPovMotion().connect(e_connections, [](int joystick_id,  int pov_index) {
		Log::message("\Handling JoyPovMotion event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventJoyPovMotion().disconnect(joypovmotion_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all JoyPovMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventJoyPovMotion().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventJoyPovMotion().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventJoyAxisMotion () const

event triggered when a joystick axis state value is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**joystick_id**, int **axis**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the JoyAxisMotion event handler
void joyaxismotion_event_handler(joystick_id,  int axis)
{
	Log::message("\Handling JoyAxisMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joyaxismotion_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventJoyAxisMotion().connect(joyaxismotion_event_connections, joyaxismotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventJoyAxisMotion().connect(joyaxismotion_event_connections, [](joystick_id,  int axis) {
		Log::message("\Handling JoyAxisMotion event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
joyaxismotion_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection joyaxismotion_event_connection;

// subscribe to the JoyAxisMotion event with a handler function keeping the connection
Input::getEventJoyAxisMotion().connect(joyaxismotion_event_connection, joyaxismotion_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
joyaxismotion_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
joyaxismotion_event_connection.setEnabled(true);

// ...

// remove subscription to the JoyAxisMotion event via the connection
joyaxismotion_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A JoyAxisMotion event handler implemented as a class member
	void event_handler(joystick_id,  int axis)
	{
		Log::message("\Handling JoyAxisMotion event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventJoyAxisMotion().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId joyaxismotion_handler_id;

// subscribe to the JoyAxisMotion event with a lambda handler function and keeping connection ID
joyaxismotion_handler_id = Input::getEventJoyAxisMotion().connect(e_connections, [](joystick_id,  int axis) {
		Log::message("\Handling JoyAxisMotion event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventJoyAxisMotion().disconnect(joyaxismotion_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all JoyAxisMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventJoyAxisMotion().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventJoyAxisMotion().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventJoyButtonUp () const

event triggered when a joystick button is released. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**joystick_id**, int **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the JoyButtonUp event handler
void joybuttonup_event_handler(joystick_id,  int button)
{
	Log::message("\Handling JoyButtonUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joybuttonup_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventJoyButtonUp().connect(joybuttonup_event_connections, joybuttonup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventJoyButtonUp().connect(joybuttonup_event_connections, [](joystick_id,  int button) {
		Log::message("\Handling JoyButtonUp event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
joybuttonup_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection joybuttonup_event_connection;

// subscribe to the JoyButtonUp event with a handler function keeping the connection
Input::getEventJoyButtonUp().connect(joybuttonup_event_connection, joybuttonup_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
joybuttonup_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
joybuttonup_event_connection.setEnabled(true);

// ...

// remove subscription to the JoyButtonUp event via the connection
joybuttonup_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A JoyButtonUp event handler implemented as a class member
	void event_handler(joystick_id,  int button)
	{
		Log::message("\Handling JoyButtonUp event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventJoyButtonUp().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId joybuttonup_handler_id;

// subscribe to the JoyButtonUp event with a lambda handler function and keeping connection ID
joybuttonup_handler_id = Input::getEventJoyButtonUp().connect(e_connections, [](joystick_id,  int button) {
		Log::message("\Handling JoyButtonUp event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventJoyButtonUp().disconnect(joybuttonup_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all JoyButtonUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventJoyButtonUp().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventJoyButtonUp().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventJoyButtonDown () const

event triggered when a joystick button is pressed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**joystick_id**, int **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the JoyButtonDown event handler
void joybuttondown_event_handler(joystick_id,  int button)
{
	Log::message("\Handling JoyButtonDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joybuttondown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventJoyButtonDown().connect(joybuttondown_event_connections, joybuttondown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventJoyButtonDown().connect(joybuttondown_event_connections, [](joystick_id,  int button) {
		Log::message("\Handling JoyButtonDown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
joybuttondown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection joybuttondown_event_connection;

// subscribe to the JoyButtonDown event with a handler function keeping the connection
Input::getEventJoyButtonDown().connect(joybuttondown_event_connection, joybuttondown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
joybuttondown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
joybuttondown_event_connection.setEnabled(true);

// ...

// remove subscription to the JoyButtonDown event via the connection
joybuttondown_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A JoyButtonDown event handler implemented as a class member
	void event_handler(joystick_id,  int button)
	{
		Log::message("\Handling JoyButtonDown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventJoyButtonDown().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId joybuttondown_handler_id;

// subscribe to the JoyButtonDown event with a lambda handler function and keeping connection ID
joybuttondown_handler_id = Input::getEventJoyButtonDown().connect(e_connections, [](joystick_id,  int button) {
		Log::message("\Handling JoyButtonDown event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventJoyButtonDown().disconnect(joybuttondown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all JoyButtonDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventJoyButtonDown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventJoyButtonDown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventJoyDisconnected () const

event triggered when a joystick is disconnected. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**joystick_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the JoyDisconnected event handler
void joydisconnected_event_handler(joystick_id)
{
	Log::message("\Handling JoyDisconnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joydisconnected_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventJoyDisconnected().connect(joydisconnected_event_connections, joydisconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventJoyDisconnected().connect(joydisconnected_event_connections, [](joystick_id) {
		Log::message("\Handling JoyDisconnected event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
joydisconnected_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection joydisconnected_event_connection;

// subscribe to the JoyDisconnected event with a handler function keeping the connection
Input::getEventJoyDisconnected().connect(joydisconnected_event_connection, joydisconnected_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
joydisconnected_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
joydisconnected_event_connection.setEnabled(true);

// ...

// remove subscription to the JoyDisconnected event via the connection
joydisconnected_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A JoyDisconnected event handler implemented as a class member
	void event_handler(joystick_id)
	{
		Log::message("\Handling JoyDisconnected event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventJoyDisconnected().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId joydisconnected_handler_id;

// subscribe to the JoyDisconnected event with a lambda handler function and keeping connection ID
joydisconnected_handler_id = Input::getEventJoyDisconnected().connect(e_connections, [](joystick_id) {
		Log::message("\Handling JoyDisconnected event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventJoyDisconnected().disconnect(joydisconnected_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all JoyDisconnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventJoyDisconnected().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventJoyDisconnected().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventJoyConnected () const

event triggered when a joystick is connected. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**joystick_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the JoyConnected event handler
void joyconnected_event_handler(joystick_id)
{
	Log::message("\Handling JoyConnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections joyconnected_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventJoyConnected().connect(joyconnected_event_connections, joyconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventJoyConnected().connect(joyconnected_event_connections, [](joystick_id) {
		Log::message("\Handling JoyConnected event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
joyconnected_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection joyconnected_event_connection;

// subscribe to the JoyConnected event with a handler function keeping the connection
Input::getEventJoyConnected().connect(joyconnected_event_connection, joyconnected_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
joyconnected_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
joyconnected_event_connection.setEnabled(true);

// ...

// remove subscription to the JoyConnected event via the connection
joyconnected_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A JoyConnected event handler implemented as a class member
	void event_handler(joystick_id)
	{
		Log::message("\Handling JoyConnected event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventJoyConnected().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId joyconnected_handler_id;

// subscribe to the JoyConnected event with a lambda handler function and keeping connection ID
joyconnected_handler_id = Input::getEventJoyConnected().connect(e_connections, [](joystick_id) {
		Log::message("\Handling JoyConnected event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventJoyConnected().disconnect(joyconnected_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all JoyConnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventJoyConnected().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventJoyConnected().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventVrDeviceAxisMotion () const

event triggered when a VR device axis state value is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**device_id**, int **axis**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the VrDeviceAxisMotion event handler
void vrdeviceaxismotion_event_handler(device_id,  int axis)
{
	Log::message("\Handling VrDeviceAxisMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdeviceaxismotion_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventVrDeviceAxisMotion().connect(vrdeviceaxismotion_event_connections, vrdeviceaxismotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventVrDeviceAxisMotion().connect(vrdeviceaxismotion_event_connections, [](device_id,  int axis) {
		Log::message("\Handling VrDeviceAxisMotion event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
vrdeviceaxismotion_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection vrdeviceaxismotion_event_connection;

// subscribe to the VrDeviceAxisMotion event with a handler function keeping the connection
Input::getEventVrDeviceAxisMotion().connect(vrdeviceaxismotion_event_connection, vrdeviceaxismotion_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
vrdeviceaxismotion_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
vrdeviceaxismotion_event_connection.setEnabled(true);

// ...

// remove subscription to the VrDeviceAxisMotion event via the connection
vrdeviceaxismotion_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A VrDeviceAxisMotion event handler implemented as a class member
	void event_handler(device_id,  int axis)
	{
		Log::message("\Handling VrDeviceAxisMotion event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventVrDeviceAxisMotion().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId vrdeviceaxismotion_handler_id;

// subscribe to the VrDeviceAxisMotion event with a lambda handler function and keeping connection ID
vrdeviceaxismotion_handler_id = Input::getEventVrDeviceAxisMotion().connect(e_connections, [](device_id,  int axis) {
		Log::message("\Handling VrDeviceAxisMotion event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventVrDeviceAxisMotion().disconnect(vrdeviceaxismotion_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all VrDeviceAxisMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventVrDeviceAxisMotion().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventVrDeviceAxisMotion().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, Input::VR_BUTTON > getEventVrDeviceButtonTouchUp () const

event triggered when a finger is withdrawn from a VR device button. If the finger is releasing a button that has been pressed, this event is triggered along with [EventVrDeviceButtonUp](#EventVrDeviceButtonUp). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**, Input::VR_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the VrDeviceButtonTouchUp event handler
void vrdevicebuttontouchup_event_handler(int device_id,  Input::VR_BUTTON button)
{
	Log::message("\Handling VrDeviceButtonTouchUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicebuttontouchup_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventVrDeviceButtonTouchUp().connect(vrdevicebuttontouchup_event_connections, vrdevicebuttontouchup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventVrDeviceButtonTouchUp().connect(vrdevicebuttontouchup_event_connections, [](int device_id,  Input::VR_BUTTON button) {
		Log::message("\Handling VrDeviceButtonTouchUp event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
vrdevicebuttontouchup_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection vrdevicebuttontouchup_event_connection;

// subscribe to the VrDeviceButtonTouchUp event with a handler function keeping the connection
Input::getEventVrDeviceButtonTouchUp().connect(vrdevicebuttontouchup_event_connection, vrdevicebuttontouchup_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
vrdevicebuttontouchup_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
vrdevicebuttontouchup_event_connection.setEnabled(true);

// ...

// remove subscription to the VrDeviceButtonTouchUp event via the connection
vrdevicebuttontouchup_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A VrDeviceButtonTouchUp event handler implemented as a class member
	void event_handler(int device_id,  Input::VR_BUTTON button)
	{
		Log::message("\Handling VrDeviceButtonTouchUp event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventVrDeviceButtonTouchUp().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId vrdevicebuttontouchup_handler_id;

// subscribe to the VrDeviceButtonTouchUp event with a lambda handler function and keeping connection ID
vrdevicebuttontouchup_handler_id = Input::getEventVrDeviceButtonTouchUp().connect(e_connections, [](int device_id,  Input::VR_BUTTON button) {
		Log::message("\Handling VrDeviceButtonTouchUp event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventVrDeviceButtonTouchUp().disconnect(vrdevicebuttontouchup_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all VrDeviceButtonTouchUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventVrDeviceButtonTouchUp().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventVrDeviceButtonTouchUp().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, Input::VR_BUTTON > getEventVrDeviceButtonTouchDown () const

event triggered when a VR device button is touched. If the button has been touched and pressed, [EventVrDeviceButtonDown](#EventVrDeviceButtonDown) is triggered along with this event. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**, Input::VR_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the VrDeviceButtonTouchDown event handler
void vrdevicebuttontouchdown_event_handler(int device_id,  Input::VR_BUTTON button)
{
	Log::message("\Handling VrDeviceButtonTouchDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicebuttontouchdown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventVrDeviceButtonTouchDown().connect(vrdevicebuttontouchdown_event_connections, vrdevicebuttontouchdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventVrDeviceButtonTouchDown().connect(vrdevicebuttontouchdown_event_connections, [](int device_id,  Input::VR_BUTTON button) {
		Log::message("\Handling VrDeviceButtonTouchDown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
vrdevicebuttontouchdown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection vrdevicebuttontouchdown_event_connection;

// subscribe to the VrDeviceButtonTouchDown event with a handler function keeping the connection
Input::getEventVrDeviceButtonTouchDown().connect(vrdevicebuttontouchdown_event_connection, vrdevicebuttontouchdown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
vrdevicebuttontouchdown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
vrdevicebuttontouchdown_event_connection.setEnabled(true);

// ...

// remove subscription to the VrDeviceButtonTouchDown event via the connection
vrdevicebuttontouchdown_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A VrDeviceButtonTouchDown event handler implemented as a class member
	void event_handler(int device_id,  Input::VR_BUTTON button)
	{
		Log::message("\Handling VrDeviceButtonTouchDown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventVrDeviceButtonTouchDown().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId vrdevicebuttontouchdown_handler_id;

// subscribe to the VrDeviceButtonTouchDown event with a lambda handler function and keeping connection ID
vrdevicebuttontouchdown_handler_id = Input::getEventVrDeviceButtonTouchDown().connect(e_connections, [](int device_id,  Input::VR_BUTTON button) {
		Log::message("\Handling VrDeviceButtonTouchDown event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventVrDeviceButtonTouchDown().disconnect(vrdevicebuttontouchdown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all VrDeviceButtonTouchDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventVrDeviceButtonTouchDown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventVrDeviceButtonTouchDown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, Input::VR_BUTTON > getEventVrDeviceButtonUp () const

event triggered when a VR device button is released. If the finger is withdrawn from the button that has been pressed, [EventVrDeviceButtonTouchUp](#EventVrDeviceButtonTouchUp) is triggered along with this event. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**, Input::VR_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the VrDeviceButtonUp event handler
void vrdevicebuttonup_event_handler(int device_id,  Input::VR_BUTTON button)
{
	Log::message("\Handling VrDeviceButtonUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicebuttonup_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventVrDeviceButtonUp().connect(vrdevicebuttonup_event_connections, vrdevicebuttonup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventVrDeviceButtonUp().connect(vrdevicebuttonup_event_connections, [](int device_id,  Input::VR_BUTTON button) {
		Log::message("\Handling VrDeviceButtonUp event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
vrdevicebuttonup_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection vrdevicebuttonup_event_connection;

// subscribe to the VrDeviceButtonUp event with a handler function keeping the connection
Input::getEventVrDeviceButtonUp().connect(vrdevicebuttonup_event_connection, vrdevicebuttonup_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
vrdevicebuttonup_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
vrdevicebuttonup_event_connection.setEnabled(true);

// ...

// remove subscription to the VrDeviceButtonUp event via the connection
vrdevicebuttonup_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A VrDeviceButtonUp event handler implemented as a class member
	void event_handler(int device_id,  Input::VR_BUTTON button)
	{
		Log::message("\Handling VrDeviceButtonUp event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventVrDeviceButtonUp().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId vrdevicebuttonup_handler_id;

// subscribe to the VrDeviceButtonUp event with a lambda handler function and keeping connection ID
vrdevicebuttonup_handler_id = Input::getEventVrDeviceButtonUp().connect(e_connections, [](int device_id,  Input::VR_BUTTON button) {
		Log::message("\Handling VrDeviceButtonUp event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventVrDeviceButtonUp().disconnect(vrdevicebuttonup_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all VrDeviceButtonUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventVrDeviceButtonUp().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventVrDeviceButtonUp().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, Input::VR_BUTTON > getEventVrDeviceButtonDown () const

event triggered when a VR device button is pressed. If the button has not previously been touched, [EventVrDeviceButtonTouchDown](#EventVrDeviceButtonTouchDown) is triggered along with this event. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int **device_id**, Input::VR_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the VrDeviceButtonDown event handler
void vrdevicebuttondown_event_handler(int device_id,  Input::VR_BUTTON button)
{
	Log::message("\Handling VrDeviceButtonDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicebuttondown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventVrDeviceButtonDown().connect(vrdevicebuttondown_event_connections, vrdevicebuttondown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventVrDeviceButtonDown().connect(vrdevicebuttondown_event_connections, [](int device_id,  Input::VR_BUTTON button) {
		Log::message("\Handling VrDeviceButtonDown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
vrdevicebuttondown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection vrdevicebuttondown_event_connection;

// subscribe to the VrDeviceButtonDown event with a handler function keeping the connection
Input::getEventVrDeviceButtonDown().connect(vrdevicebuttondown_event_connection, vrdevicebuttondown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
vrdevicebuttondown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
vrdevicebuttondown_event_connection.setEnabled(true);

// ...

// remove subscription to the VrDeviceButtonDown event via the connection
vrdevicebuttondown_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A VrDeviceButtonDown event handler implemented as a class member
	void event_handler(int device_id,  Input::VR_BUTTON button)
	{
		Log::message("\Handling VrDeviceButtonDown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventVrDeviceButtonDown().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId vrdevicebuttondown_handler_id;

// subscribe to the VrDeviceButtonDown event with a lambda handler function and keeping connection ID
vrdevicebuttondown_handler_id = Input::getEventVrDeviceButtonDown().connect(e_connections, [](int device_id,  Input::VR_BUTTON button) {
		Log::message("\Handling VrDeviceButtonDown event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventVrDeviceButtonDown().disconnect(vrdevicebuttondown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all VrDeviceButtonDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventVrDeviceButtonDown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventVrDeviceButtonDown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventVrDeviceDisconnected () const

event triggered when a VR device is disconnected. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**device_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the VrDeviceDisconnected event handler
void vrdevicedisconnected_event_handler(device_id)
{
	Log::message("\Handling VrDeviceDisconnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdevicedisconnected_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventVrDeviceDisconnected().connect(vrdevicedisconnected_event_connections, vrdevicedisconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventVrDeviceDisconnected().connect(vrdevicedisconnected_event_connections, [](device_id) {
		Log::message("\Handling VrDeviceDisconnected event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
vrdevicedisconnected_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection vrdevicedisconnected_event_connection;

// subscribe to the VrDeviceDisconnected event with a handler function keeping the connection
Input::getEventVrDeviceDisconnected().connect(vrdevicedisconnected_event_connection, vrdevicedisconnected_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
vrdevicedisconnected_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
vrdevicedisconnected_event_connection.setEnabled(true);

// ...

// remove subscription to the VrDeviceDisconnected event via the connection
vrdevicedisconnected_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A VrDeviceDisconnected event handler implemented as a class member
	void event_handler(device_id)
	{
		Log::message("\Handling VrDeviceDisconnected event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventVrDeviceDisconnected().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId vrdevicedisconnected_handler_id;

// subscribe to the VrDeviceDisconnected event with a lambda handler function and keeping connection ID
vrdevicedisconnected_handler_id = Input::getEventVrDeviceDisconnected().connect(e_connections, [](device_id) {
		Log::message("\Handling VrDeviceDisconnected event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventVrDeviceDisconnected().disconnect(vrdevicedisconnected_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all VrDeviceDisconnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventVrDeviceDisconnected().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventVrDeviceDisconnected().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventVrDeviceConnected () const

event triggered when a VR device is connected. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**device_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the VrDeviceConnected event handler
void vrdeviceconnected_event_handler(device_id)
{
	Log::message("\Handling VrDeviceConnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections vrdeviceconnected_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventVrDeviceConnected().connect(vrdeviceconnected_event_connections, vrdeviceconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventVrDeviceConnected().connect(vrdeviceconnected_event_connections, [](device_id) {
		Log::message("\Handling VrDeviceConnected event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
vrdeviceconnected_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection vrdeviceconnected_event_connection;

// subscribe to the VrDeviceConnected event with a handler function keeping the connection
Input::getEventVrDeviceConnected().connect(vrdeviceconnected_event_connection, vrdeviceconnected_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
vrdeviceconnected_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
vrdeviceconnected_event_connection.setEnabled(true);

// ...

// remove subscription to the VrDeviceConnected event via the connection
vrdeviceconnected_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A VrDeviceConnected event handler implemented as a class member
	void event_handler(device_id)
	{
		Log::message("\Handling VrDeviceConnected event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventVrDeviceConnected().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId vrdeviceconnected_handler_id;

// subscribe to the VrDeviceConnected event with a lambda handler function and keeping connection ID
vrdeviceconnected_handler_id = Input::getEventVrDeviceConnected().connect(e_connections, [](device_id) {
		Log::message("\Handling VrDeviceConnected event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventVrDeviceConnected().disconnect(vrdeviceconnected_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all VrDeviceConnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventVrDeviceConnected().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventVrDeviceConnected().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, int, int> getEventGamepadTouchMotion () const

event triggered when the finger touching the gamepad touch panel moves across it. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**gamepad_id**, int **touch_id**, int **finger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the GamepadTouchMotion event handler
void gamepadtouchmotion_event_handler(gamepad_id,  int touch_id,  int finger)
{
	Log::message("\Handling GamepadTouchMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadtouchmotion_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventGamepadTouchMotion().connect(gamepadtouchmotion_event_connections, gamepadtouchmotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventGamepadTouchMotion().connect(gamepadtouchmotion_event_connections, [](gamepad_id,  int touch_id,  int finger) {
		Log::message("\Handling GamepadTouchMotion event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
gamepadtouchmotion_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection gamepadtouchmotion_event_connection;

// subscribe to the GamepadTouchMotion event with a handler function keeping the connection
Input::getEventGamepadTouchMotion().connect(gamepadtouchmotion_event_connection, gamepadtouchmotion_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
gamepadtouchmotion_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
gamepadtouchmotion_event_connection.setEnabled(true);

// ...

// remove subscription to the GamepadTouchMotion event via the connection
gamepadtouchmotion_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A GamepadTouchMotion event handler implemented as a class member
	void event_handler(gamepad_id,  int touch_id,  int finger)
	{
		Log::message("\Handling GamepadTouchMotion event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventGamepadTouchMotion().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId gamepadtouchmotion_handler_id;

// subscribe to the GamepadTouchMotion event with a lambda handler function and keeping connection ID
gamepadtouchmotion_handler_id = Input::getEventGamepadTouchMotion().connect(e_connections, [](gamepad_id,  int touch_id,  int finger) {
		Log::message("\Handling GamepadTouchMotion event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventGamepadTouchMotion().disconnect(gamepadtouchmotion_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all GamepadTouchMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventGamepadTouchMotion().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventGamepadTouchMotion().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, int, int> getEventGamepadTouchUp () const

event triggered when the touch is withdrawn from the gamepad touch panel. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**gamepad_id**, int **touch_id**, int **finger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the GamepadTouchUp event handler
void gamepadtouchup_event_handler(gamepad_id,  int touch_id,  int finger)
{
	Log::message("\Handling GamepadTouchUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadtouchup_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventGamepadTouchUp().connect(gamepadtouchup_event_connections, gamepadtouchup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventGamepadTouchUp().connect(gamepadtouchup_event_connections, [](gamepad_id,  int touch_id,  int finger) {
		Log::message("\Handling GamepadTouchUp event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
gamepadtouchup_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection gamepadtouchup_event_connection;

// subscribe to the GamepadTouchUp event with a handler function keeping the connection
Input::getEventGamepadTouchUp().connect(gamepadtouchup_event_connection, gamepadtouchup_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
gamepadtouchup_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
gamepadtouchup_event_connection.setEnabled(true);

// ...

// remove subscription to the GamepadTouchUp event via the connection
gamepadtouchup_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A GamepadTouchUp event handler implemented as a class member
	void event_handler(gamepad_id,  int touch_id,  int finger)
	{
		Log::message("\Handling GamepadTouchUp event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventGamepadTouchUp().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId gamepadtouchup_handler_id;

// subscribe to the GamepadTouchUp event with a lambda handler function and keeping connection ID
gamepadtouchup_handler_id = Input::getEventGamepadTouchUp().connect(e_connections, [](gamepad_id,  int touch_id,  int finger) {
		Log::message("\Handling GamepadTouchUp event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventGamepadTouchUp().disconnect(gamepadtouchup_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all GamepadTouchUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventGamepadTouchUp().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventGamepadTouchUp().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, int, int> getEventGamepadTouchDown () const

event triggered when the gamepad touch panel is touched. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**gamepad_id**, int **touch_id**, int **finger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the GamepadTouchDown event handler
void gamepadtouchdown_event_handler(gamepad_id,  int touch_id,  int finger)
{
	Log::message("\Handling GamepadTouchDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadtouchdown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventGamepadTouchDown().connect(gamepadtouchdown_event_connections, gamepadtouchdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventGamepadTouchDown().connect(gamepadtouchdown_event_connections, [](gamepad_id,  int touch_id,  int finger) {
		Log::message("\Handling GamepadTouchDown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
gamepadtouchdown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection gamepadtouchdown_event_connection;

// subscribe to the GamepadTouchDown event with a handler function keeping the connection
Input::getEventGamepadTouchDown().connect(gamepadtouchdown_event_connection, gamepadtouchdown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
gamepadtouchdown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
gamepadtouchdown_event_connection.setEnabled(true);

// ...

// remove subscription to the GamepadTouchDown event via the connection
gamepadtouchdown_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A GamepadTouchDown event handler implemented as a class member
	void event_handler(gamepad_id,  int touch_id,  int finger)
	{
		Log::message("\Handling GamepadTouchDown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventGamepadTouchDown().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId gamepadtouchdown_handler_id;

// subscribe to the GamepadTouchDown event with a lambda handler function and keeping connection ID
gamepadtouchdown_handler_id = Input::getEventGamepadTouchDown().connect(e_connections, [](gamepad_id,  int touch_id,  int finger) {
		Log::message("\Handling GamepadTouchDown event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventGamepadTouchDown().disconnect(gamepadtouchdown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all GamepadTouchDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventGamepadTouchDown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventGamepadTouchDown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, Input::GAMEPAD_AXIS > getEventGamepadAxisMotion () const

event triggered when a gamepad axis state value is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**, Input::GAMEPAD_AXIS **axis**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the GamepadAxisMotion event handler
void gamepadaxismotion_event_handler(int gamepad_id,  Input::GAMEPAD_AXIS axis)
{
	Log::message("\Handling GamepadAxisMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadaxismotion_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventGamepadAxisMotion().connect(gamepadaxismotion_event_connections, gamepadaxismotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventGamepadAxisMotion().connect(gamepadaxismotion_event_connections, [](int gamepad_id,  Input::GAMEPAD_AXIS axis) {
		Log::message("\Handling GamepadAxisMotion event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
gamepadaxismotion_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection gamepadaxismotion_event_connection;

// subscribe to the GamepadAxisMotion event with a handler function keeping the connection
Input::getEventGamepadAxisMotion().connect(gamepadaxismotion_event_connection, gamepadaxismotion_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
gamepadaxismotion_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
gamepadaxismotion_event_connection.setEnabled(true);

// ...

// remove subscription to the GamepadAxisMotion event via the connection
gamepadaxismotion_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A GamepadAxisMotion event handler implemented as a class member
	void event_handler(int gamepad_id,  Input::GAMEPAD_AXIS axis)
	{
		Log::message("\Handling GamepadAxisMotion event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventGamepadAxisMotion().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId gamepadaxismotion_handler_id;

// subscribe to the GamepadAxisMotion event with a lambda handler function and keeping connection ID
gamepadaxismotion_handler_id = Input::getEventGamepadAxisMotion().connect(e_connections, [](int gamepad_id,  Input::GAMEPAD_AXIS axis) {
		Log::message("\Handling GamepadAxisMotion event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventGamepadAxisMotion().disconnect(gamepadaxismotion_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all GamepadAxisMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventGamepadAxisMotion().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventGamepadAxisMotion().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, Input::GAMEPAD_BUTTON > getEventGamepadButtonUp () const

event triggered when a gamepad button is released. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**, Input::GAMEPAD_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the GamepadButtonUp event handler
void gamepadbuttonup_event_handler(int gamepad_id,  Input::GAMEPAD_BUTTON button)
{
	Log::message("\Handling GamepadButtonUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadbuttonup_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventGamepadButtonUp().connect(gamepadbuttonup_event_connections, gamepadbuttonup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventGamepadButtonUp().connect(gamepadbuttonup_event_connections, [](int gamepad_id,  Input::GAMEPAD_BUTTON button) {
		Log::message("\Handling GamepadButtonUp event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
gamepadbuttonup_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection gamepadbuttonup_event_connection;

// subscribe to the GamepadButtonUp event with a handler function keeping the connection
Input::getEventGamepadButtonUp().connect(gamepadbuttonup_event_connection, gamepadbuttonup_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
gamepadbuttonup_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
gamepadbuttonup_event_connection.setEnabled(true);

// ...

// remove subscription to the GamepadButtonUp event via the connection
gamepadbuttonup_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A GamepadButtonUp event handler implemented as a class member
	void event_handler(int gamepad_id,  Input::GAMEPAD_BUTTON button)
	{
		Log::message("\Handling GamepadButtonUp event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventGamepadButtonUp().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId gamepadbuttonup_handler_id;

// subscribe to the GamepadButtonUp event with a lambda handler function and keeping connection ID
gamepadbuttonup_handler_id = Input::getEventGamepadButtonUp().connect(e_connections, [](int gamepad_id,  Input::GAMEPAD_BUTTON button) {
		Log::message("\Handling GamepadButtonUp event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventGamepadButtonUp().disconnect(gamepadbuttonup_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all GamepadButtonUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventGamepadButtonUp().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventGamepadButtonUp().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, Input::GAMEPAD_BUTTON > getEventGamepadButtonDown () const

event triggered when a gamepad button is pressed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int **gamepad_id**, Input::GAMEPAD_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the GamepadButtonDown event handler
void gamepadbuttondown_event_handler(int gamepad_id,  Input::GAMEPAD_BUTTON button)
{
	Log::message("\Handling GamepadButtonDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadbuttondown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventGamepadButtonDown().connect(gamepadbuttondown_event_connections, gamepadbuttondown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventGamepadButtonDown().connect(gamepadbuttondown_event_connections, [](int gamepad_id,  Input::GAMEPAD_BUTTON button) {
		Log::message("\Handling GamepadButtonDown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
gamepadbuttondown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection gamepadbuttondown_event_connection;

// subscribe to the GamepadButtonDown event with a handler function keeping the connection
Input::getEventGamepadButtonDown().connect(gamepadbuttondown_event_connection, gamepadbuttondown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
gamepadbuttondown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
gamepadbuttondown_event_connection.setEnabled(true);

// ...

// remove subscription to the GamepadButtonDown event via the connection
gamepadbuttondown_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A GamepadButtonDown event handler implemented as a class member
	void event_handler(int gamepad_id,  Input::GAMEPAD_BUTTON button)
	{
		Log::message("\Handling GamepadButtonDown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventGamepadButtonDown().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId gamepadbuttondown_handler_id;

// subscribe to the GamepadButtonDown event with a lambda handler function and keeping connection ID
gamepadbuttondown_handler_id = Input::getEventGamepadButtonDown().connect(e_connections, [](int gamepad_id,  Input::GAMEPAD_BUTTON button) {
		Log::message("\Handling GamepadButtonDown event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventGamepadButtonDown().disconnect(gamepadbuttondown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all GamepadButtonDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventGamepadButtonDown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventGamepadButtonDown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventGamepadDisconnected () const

event triggered when a gamepad is disconnected. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**gamepad_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the GamepadDisconnected event handler
void gamepaddisconnected_event_handler(gamepad_id)
{
	Log::message("\Handling GamepadDisconnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepaddisconnected_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventGamepadDisconnected().connect(gamepaddisconnected_event_connections, gamepaddisconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventGamepadDisconnected().connect(gamepaddisconnected_event_connections, [](gamepad_id) {
		Log::message("\Handling GamepadDisconnected event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
gamepaddisconnected_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection gamepaddisconnected_event_connection;

// subscribe to the GamepadDisconnected event with a handler function keeping the connection
Input::getEventGamepadDisconnected().connect(gamepaddisconnected_event_connection, gamepaddisconnected_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
gamepaddisconnected_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
gamepaddisconnected_event_connection.setEnabled(true);

// ...

// remove subscription to the GamepadDisconnected event via the connection
gamepaddisconnected_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A GamepadDisconnected event handler implemented as a class member
	void event_handler(gamepad_id)
	{
		Log::message("\Handling GamepadDisconnected event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventGamepadDisconnected().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId gamepaddisconnected_handler_id;

// subscribe to the GamepadDisconnected event with a lambda handler function and keeping connection ID
gamepaddisconnected_handler_id = Input::getEventGamepadDisconnected().connect(e_connections, [](gamepad_id) {
		Log::message("\Handling GamepadDisconnected event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventGamepadDisconnected().disconnect(gamepaddisconnected_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all GamepadDisconnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventGamepadDisconnected().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventGamepadDisconnected().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventGamepadConnected () const

event triggered when a gamepad is connected. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**gamepad_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the GamepadConnected event handler
void gamepadconnected_event_handler(gamepad_id)
{
	Log::message("\Handling GamepadConnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gamepadconnected_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventGamepadConnected().connect(gamepadconnected_event_connections, gamepadconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventGamepadConnected().connect(gamepadconnected_event_connections, [](gamepad_id) {
		Log::message("\Handling GamepadConnected event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
gamepadconnected_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection gamepadconnected_event_connection;

// subscribe to the GamepadConnected event with a handler function keeping the connection
Input::getEventGamepadConnected().connect(gamepadconnected_event_connection, gamepadconnected_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
gamepadconnected_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
gamepadconnected_event_connection.setEnabled(true);

// ...

// remove subscription to the GamepadConnected event via the connection
gamepadconnected_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A GamepadConnected event handler implemented as a class member
	void event_handler(gamepad_id)
	{
		Log::message("\Handling GamepadConnected event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventGamepadConnected().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId gamepadconnected_handler_id;

// subscribe to the GamepadConnected event with a lambda handler function and keeping connection ID
gamepadconnected_handler_id = Input::getEventGamepadConnected().connect(e_connections, [](gamepad_id) {
		Log::message("\Handling GamepadConnected event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventGamepadConnected().disconnect(gamepadconnected_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all GamepadConnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventGamepadConnected().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventGamepadConnected().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventTouchMotion () const

event triggered when the touch is moved. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**touch_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TouchMotion event handler
void touchmotion_event_handler(touch_id)
{
	Log::message("\Handling TouchMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections touchmotion_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventTouchMotion().connect(touchmotion_event_connections, touchmotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventTouchMotion().connect(touchmotion_event_connections, [](touch_id) {
		Log::message("\Handling TouchMotion event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
touchmotion_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection touchmotion_event_connection;

// subscribe to the TouchMotion event with a handler function keeping the connection
Input::getEventTouchMotion().connect(touchmotion_event_connection, touchmotion_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
touchmotion_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
touchmotion_event_connection.setEnabled(true);

// ...

// remove subscription to the TouchMotion event via the connection
touchmotion_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A TouchMotion event handler implemented as a class member
	void event_handler(touch_id)
	{
		Log::message("\Handling TouchMotion event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventTouchMotion().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId touchmotion_handler_id;

// subscribe to the TouchMotion event with a lambda handler function and keeping connection ID
touchmotion_handler_id = Input::getEventTouchMotion().connect(e_connections, [](touch_id) {
		Log::message("\Handling TouchMotion event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventTouchMotion().disconnect(touchmotion_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TouchMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventTouchMotion().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventTouchMotion().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventTouchUp () const

event triggered when the touch is released. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**touch_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TouchUp event handler
void touchup_event_handler(touch_id)
{
	Log::message("\Handling TouchUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections touchup_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventTouchUp().connect(touchup_event_connections, touchup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventTouchUp().connect(touchup_event_connections, [](touch_id) {
		Log::message("\Handling TouchUp event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
touchup_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection touchup_event_connection;

// subscribe to the TouchUp event with a handler function keeping the connection
Input::getEventTouchUp().connect(touchup_event_connection, touchup_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
touchup_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
touchup_event_connection.setEnabled(true);

// ...

// remove subscription to the TouchUp event via the connection
touchup_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A TouchUp event handler implemented as a class member
	void event_handler(touch_id)
	{
		Log::message("\Handling TouchUp event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventTouchUp().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId touchup_handler_id;

// subscribe to the TouchUp event with a lambda handler function and keeping connection ID
touchup_handler_id = Input::getEventTouchUp().connect(e_connections, [](touch_id) {
		Log::message("\Handling TouchUp event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventTouchUp().disconnect(touchup_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TouchUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventTouchUp().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventTouchUp().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventTouchDown () const

event triggered when the touch is pressed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**touch_id**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TouchDown event handler
void touchdown_event_handler(touch_id)
{
	Log::message("\Handling TouchDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections touchdown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventTouchDown().connect(touchdown_event_connections, touchdown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventTouchDown().connect(touchdown_event_connections, [](touch_id) {
		Log::message("\Handling TouchDown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
touchdown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection touchdown_event_connection;

// subscribe to the TouchDown event with a handler function keeping the connection
Input::getEventTouchDown().connect(touchdown_event_connection, touchdown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
touchdown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
touchdown_event_connection.setEnabled(true);

// ...

// remove subscription to the TouchDown event via the connection
touchdown_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A TouchDown event handler implemented as a class member
	void event_handler(touch_id)
	{
		Log::message("\Handling TouchDown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventTouchDown().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId touchdown_handler_id;

// subscribe to the TouchDown event with a lambda handler function and keeping connection ID
touchdown_handler_id = Input::getEventTouchDown().connect(e_connections, [](touch_id) {
		Log::message("\Handling TouchDown event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventTouchDown().disconnect(touchdown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TouchDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventTouchDown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventTouchDown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<unsigned int> getEventTextPress () const

event triggered when the key that has a corresponding printable symbol is pressed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(unsigned int **unicode**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TextPress event handler
void textpress_event_handler(unsigned int unicode)
{
	Log::message("\Handling TextPress event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections textpress_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventTextPress().connect(textpress_event_connections, textpress_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventTextPress().connect(textpress_event_connections, [](unsigned int unicode) {
		Log::message("\Handling TextPress event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
textpress_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection textpress_event_connection;

// subscribe to the TextPress event with a handler function keeping the connection
Input::getEventTextPress().connect(textpress_event_connection, textpress_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
textpress_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
textpress_event_connection.setEnabled(true);

// ...

// remove subscription to the TextPress event via the connection
textpress_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A TextPress event handler implemented as a class member
	void event_handler(unsigned int unicode)
	{
		Log::message("\Handling TextPress event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventTextPress().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId textpress_handler_id;

// subscribe to the TextPress event with a lambda handler function and keeping connection ID
textpress_handler_id = Input::getEventTextPress().connect(e_connections, [](unsigned int unicode) {
		Log::message("\Handling TextPress event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventTextPress().disconnect(textpress_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TextPress events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventTextPress().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventTextPress().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<unsigned int> getEventKeyRepeat () const

event triggered when the key is pressed repeatedly. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(unsigned int **unicode**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the KeyRepeat event handler
void keyrepeat_event_handler(unsigned int unicode)
{
	Log::message("\Handling KeyRepeat event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections keyrepeat_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventKeyRepeat().connect(keyrepeat_event_connections, keyrepeat_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventKeyRepeat().connect(keyrepeat_event_connections, [](unsigned int unicode) {
		Log::message("\Handling KeyRepeat event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
keyrepeat_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection keyrepeat_event_connection;

// subscribe to the KeyRepeat event with a handler function keeping the connection
Input::getEventKeyRepeat().connect(keyrepeat_event_connection, keyrepeat_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
keyrepeat_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
keyrepeat_event_connection.setEnabled(true);

// ...

// remove subscription to the KeyRepeat event via the connection
keyrepeat_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A KeyRepeat event handler implemented as a class member
	void event_handler(unsigned int unicode)
	{
		Log::message("\Handling KeyRepeat event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventKeyRepeat().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId keyrepeat_handler_id;

// subscribe to the KeyRepeat event with a lambda handler function and keeping connection ID
keyrepeat_handler_id = Input::getEventKeyRepeat().connect(e_connections, [](unsigned int unicode) {
		Log::message("\Handling KeyRepeat event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventKeyRepeat().disconnect(keyrepeat_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all KeyRepeat events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventKeyRepeat().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventKeyRepeat().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event< Input::KEY > getEventKeyUp () const

event triggered when the key is released. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(Input::KEY **key**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the KeyUp event handler
void keyup_event_handler(Input::KEY key)
{
	Log::message("\Handling KeyUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections keyup_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventKeyUp().connect(keyup_event_connections, keyup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventKeyUp().connect(keyup_event_connections, [](Input::KEY key) {
		Log::message("\Handling KeyUp event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
keyup_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection keyup_event_connection;

// subscribe to the KeyUp event with a handler function keeping the connection
Input::getEventKeyUp().connect(keyup_event_connection, keyup_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
keyup_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
keyup_event_connection.setEnabled(true);

// ...

// remove subscription to the KeyUp event via the connection
keyup_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A KeyUp event handler implemented as a class member
	void event_handler(Input::KEY key)
	{
		Log::message("\Handling KeyUp event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventKeyUp().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId keyup_handler_id;

// subscribe to the KeyUp event with a lambda handler function and keeping connection ID
keyup_handler_id = Input::getEventKeyUp().connect(e_connections, [](Input::KEY key) {
		Log::message("\Handling KeyUp event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventKeyUp().disconnect(keyup_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all KeyUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventKeyUp().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventKeyUp().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event< Input::KEY > getEventKeyDown () const

event triggered when the key is pressed and held. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(Input::KEY **key**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the KeyDown event handler
void keydown_event_handler(Input::KEY key)
{
	Log::message("\Handling KeyDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections keydown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventKeyDown().connect(keydown_event_connections, keydown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventKeyDown().connect(keydown_event_connections, [](Input::KEY key) {
		Log::message("\Handling KeyDown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
keydown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection keydown_event_connection;

// subscribe to the KeyDown event with a handler function keeping the connection
Input::getEventKeyDown().connect(keydown_event_connection, keydown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
keydown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
keydown_event_connection.setEnabled(true);

// ...

// remove subscription to the KeyDown event via the connection
keydown_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A KeyDown event handler implemented as a class member
	void event_handler(Input::KEY key)
	{
		Log::message("\Handling KeyDown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventKeyDown().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId keydown_handler_id;

// subscribe to the KeyDown event with a lambda handler function and keeping connection ID
keydown_handler_id = Input::getEventKeyDown().connect(e_connections, [](Input::KEY key) {
		Log::message("\Handling KeyDown event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventKeyDown().disconnect(keydown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all KeyDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventKeyDown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventKeyDown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int, int> getEventMouseMotion () const

event triggered when the mouse is moved. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**coord_x**, int **coord_y**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the MouseMotion event handler
void mousemotion_event_handler(coord_x, int coord_y)
{
	Log::message("\Handling MouseMotion event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mousemotion_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventMouseMotion().connect(mousemotion_event_connections, mousemotion_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventMouseMotion().connect(mousemotion_event_connections, [](coord_x, int coord_y) {
		Log::message("\Handling MouseMotion event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
mousemotion_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection mousemotion_event_connection;

// subscribe to the MouseMotion event with a handler function keeping the connection
Input::getEventMouseMotion().connect(mousemotion_event_connection, mousemotion_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
mousemotion_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
mousemotion_event_connection.setEnabled(true);

// ...

// remove subscription to the MouseMotion event via the connection
mousemotion_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A MouseMotion event handler implemented as a class member
	void event_handler(coord_x, int coord_y)
	{
		Log::message("\Handling MouseMotion event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventMouseMotion().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId mousemotion_handler_id;

// subscribe to the MouseMotion event with a lambda handler function and keeping connection ID
mousemotion_handler_id = Input::getEventMouseMotion().connect(e_connections, [](coord_x, int coord_y) {
		Log::message("\Handling MouseMotion event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventMouseMotion().disconnect(mousemotion_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all MouseMotion events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventMouseMotion().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventMouseMotion().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventMouseWheelHorizontal () const

event triggered when the mouse wheel is moved horizontally. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**delta_horizontal**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the MouseWheelHorizontal event handler
void mousewheelhorizontal_event_handler(delta_horizontal)
{
	Log::message("\Handling MouseWheelHorizontal event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mousewheelhorizontal_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventMouseWheelHorizontal().connect(mousewheelhorizontal_event_connections, mousewheelhorizontal_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventMouseWheelHorizontal().connect(mousewheelhorizontal_event_connections, [](delta_horizontal) {
		Log::message("\Handling MouseWheelHorizontal event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
mousewheelhorizontal_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection mousewheelhorizontal_event_connection;

// subscribe to the MouseWheelHorizontal event with a handler function keeping the connection
Input::getEventMouseWheelHorizontal().connect(mousewheelhorizontal_event_connection, mousewheelhorizontal_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
mousewheelhorizontal_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
mousewheelhorizontal_event_connection.setEnabled(true);

// ...

// remove subscription to the MouseWheelHorizontal event via the connection
mousewheelhorizontal_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A MouseWheelHorizontal event handler implemented as a class member
	void event_handler(delta_horizontal)
	{
		Log::message("\Handling MouseWheelHorizontal event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventMouseWheelHorizontal().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId mousewheelhorizontal_handler_id;

// subscribe to the MouseWheelHorizontal event with a lambda handler function and keeping connection ID
mousewheelhorizontal_handler_id = Input::getEventMouseWheelHorizontal().connect(e_connections, [](delta_horizontal) {
		Log::message("\Handling MouseWheelHorizontal event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventMouseWheelHorizontal().disconnect(mousewheelhorizontal_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all MouseWheelHorizontal events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventMouseWheelHorizontal().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventMouseWheelHorizontal().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<int> getEventMouseWheel () const

event triggered when the mouse scroll wheel is moved. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**delta_vertical**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the MouseWheel event handler
void mousewheel_event_handler(delta_vertical)
{
	Log::message("\Handling MouseWheel event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mousewheel_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventMouseWheel().connect(mousewheel_event_connections, mousewheel_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventMouseWheel().connect(mousewheel_event_connections, [](delta_vertical) {
		Log::message("\Handling MouseWheel event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
mousewheel_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection mousewheel_event_connection;

// subscribe to the MouseWheel event with a handler function keeping the connection
Input::getEventMouseWheel().connect(mousewheel_event_connection, mousewheel_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
mousewheel_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
mousewheel_event_connection.setEnabled(true);

// ...

// remove subscription to the MouseWheel event via the connection
mousewheel_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A MouseWheel event handler implemented as a class member
	void event_handler(delta_vertical)
	{
		Log::message("\Handling MouseWheel event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventMouseWheel().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId mousewheel_handler_id;

// subscribe to the MouseWheel event with a lambda handler function and keeping connection ID
mousewheel_handler_id = Input::getEventMouseWheel().connect(e_connections, [](delta_vertical) {
		Log::message("\Handling MouseWheel event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventMouseWheel().disconnect(mousewheel_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all MouseWheel events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventMouseWheel().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventMouseWheel().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event< Input::MOUSE_BUTTON > getEventMouseUp () const

event triggered when the mouse button is released. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(Input::MOUSE_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the MouseUp event handler
void mouseup_event_handler(Input::MOUSE_BUTTON button)
{
	Log::message("\Handling MouseUp event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mouseup_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventMouseUp().connect(mouseup_event_connections, mouseup_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventMouseUp().connect(mouseup_event_connections, [](Input::MOUSE_BUTTON button) {
		Log::message("\Handling MouseUp event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
mouseup_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection mouseup_event_connection;

// subscribe to the MouseUp event with a handler function keeping the connection
Input::getEventMouseUp().connect(mouseup_event_connection, mouseup_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
mouseup_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
mouseup_event_connection.setEnabled(true);

// ...

// remove subscription to the MouseUp event via the connection
mouseup_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A MouseUp event handler implemented as a class member
	void event_handler(Input::MOUSE_BUTTON button)
	{
		Log::message("\Handling MouseUp event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventMouseUp().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId mouseup_handler_id;

// subscribe to the MouseUp event with a lambda handler function and keeping connection ID
mouseup_handler_id = Input::getEventMouseUp().connect(e_connections, [](Input::MOUSE_BUTTON button) {
		Log::message("\Handling MouseUp event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventMouseUp().disconnect(mouseup_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all MouseUp events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventMouseUp().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventMouseUp().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event< Input::MOUSE_BUTTON > getEventMouseDown () const

event triggered when the mouse button is pressed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(Input::MOUSE_BUTTON **button**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the MouseDown event handler
void mousedown_event_handler(Input::MOUSE_BUTTON button)
{
	Log::message("\Handling MouseDown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mousedown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventMouseDown().connect(mousedown_event_connections, mousedown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventMouseDown().connect(mousedown_event_connections, [](Input::MOUSE_BUTTON button) {
		Log::message("\Handling MouseDown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
mousedown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection mousedown_event_connection;

// subscribe to the MouseDown event with a handler function keeping the connection
Input::getEventMouseDown().connect(mousedown_event_connection, mousedown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
mousedown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
mousedown_event_connection.setEnabled(true);

// ...

// remove subscription to the MouseDown event via the connection
mousedown_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A MouseDown event handler implemented as a class member
	void event_handler(Input::MOUSE_BUTTON button)
	{
		Log::message("\Handling MouseDown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventMouseDown().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId mousedown_handler_id;

// subscribe to the MouseDown event with a lambda handler function and keeping connection ID
mousedown_handler_id = Input::getEventMouseDown().connect(e_connections, [](Input::MOUSE_BUTTON button) {
		Log::message("\Handling MouseDown event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventMouseDown().disconnect(mousedown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all MouseDown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventMouseDown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventMouseDown().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const char *, int, int> getEventTextEditing () const

event triggered while the user is composing text via an IME (Input Method Editor). The handler receives the current UTF-8 composition (preedit) text, the cursor position within it, and the length of the selected portion (both in codepoints). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience.

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **text**, int **cursor**, int **length**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TextEditing event handler
void textediting_event_handler(const char * text, int cursor, int length)
{
	Log::message("\Handling TextEditing event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections textediting_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Input::getEventTextEditing().connect(textediting_event_connections, textediting_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Input::getEventTextEditing().connect(textediting_event_connections, [](const char * text, int cursor, int length) {
		Log::message("\Handling TextEditing event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
textediting_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection textediting_event_connection;

// subscribe to the TextEditing event with a handler function keeping the connection
Input::getEventTextEditing().connect(textediting_event_connection, textediting_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
textediting_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
textediting_event_connection.setEnabled(true);

// ...

// remove subscription to the TextEditing event via the connection
textediting_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A TextEditing event handler implemented as a class member
	void event_handler(const char * text, int cursor, int length)
	{
		Log::message("\Handling TextEditing event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Input::getEventTextEditing().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId textediting_handler_id;

// subscribe to the TextEditing event with a lambda handler function and keeping connection ID
textediting_handler_id = Input::getEventTextEditing().connect(e_connections, [](const char * text, int cursor, int length) {
		Log::message("\Handling TextEditing event (lambda).\n");
	}
);

// remove the subscription later using the ID
Input::getEventTextEditing().disconnect(textediting_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TextEditing events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Input::getEventTextEditing().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Input::getEventTextEditing().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## Ptr < InputGamePad > getGamePad ( int num ) const

Returns a gamepad of the given index.
### Arguments

- *int* **num** - Gamepad index.

### Return value

[InputGamepad](../../../api/library/controls/class.inputgamepad_cpp.md) object.
## Ptr < InputJoystick > getJoystick ( int num ) const

Returns a joystick with the given index.
### Arguments

- *int* **num** - Joystick index.

### Return value

[InputJoystick](../../../api/library/controls/class.inputjoystick_cpp.md) object.
## bool isKeyPressed ( Input::KEY key ) const

Returns a value indicating if the given key is pressed. Check this value to perform continuous actions.
```cpp
if (Input::isKeyPressed(Input::KEY_ENTER)) {
	Log::message("the Enter key is held down\n");
}

```


### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the preset [KEY_](#KEY) codes.

### Return value

true if the key is pressed; otherwise, false.
## bool isKeyDown ( Input::KEY key ) const

Returns a value indicating if the given key was pressed during the current frame. Check this value to perform one-time actions on pressing a key.
```cpp
if (Input::isKeyDown(Input::KEY_SPACE)) {
	Log::message("the Space key was pressed\n");
}

```


### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the preset [KEY_](#KEY) codes.

### Return value

1 during the first frame when the key was pressed, 0 for the following ones until it is released and pressed again.
## bool isKeyUp ( Input::KEY key ) const

Returns a value indicating if the given key was released during the current frame. Check this value to perform one-time actions on releasing a key.
```cpp
if (Input::isKeyUp(Input::KEY_F)) {
	Log::message("the F key was released\n");
}

```


### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the preset [KEY_](#KEY) codes.

### Return value

true during the first frame when the key was released; otherwise, false.
## bool isMouseButtonPressed ( Input::MOUSE_BUTTON button ) const

Returns a value indicating if the given mouse button is pressed. Check this value to perform continuous actions.
```cpp
if (Input::isMouseButtonPressed(Input::MOUSE_BUTTON_LEFT)) {
	Log::message("the left mouse button is held down\n");
}

```


### Arguments

- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - One of the preset [MOUSE_BUTTON_](#MOUSE_BUTTON) codes.

### Return value

1 if the mouse button is pressed; otherwise, 0.
## bool isMouseButtonDown ( Input::MOUSE_BUTTON button ) const

Returns a value indicating if the given mouse button was pressed during the current frame. Check this value to perform one-time actions on pressing a mouse button.
```cpp
if (Input::isMouseButtonDown(Input::MOUSE_BUTTON_LEFT)) {
	Log::message("the left mouse button was pressed\n");
}

```


### Arguments

- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - One of the preset [MOUSE_BUTTON_](#MOUSE_BUTTON) codes.

### Return value

1 during the first frame when the mouse button was released; otherwise, 0.
## bool isMouseButtonUp ( Input::MOUSE_BUTTON button ) const

Returns a value indicating if the given mouse button was released during the current frame. Check this value to perform one-time actions on releasing a mouse button.
```cpp
if (Input::isMouseButtonUp(Input::MOUSE_BUTTON_LEFT)) {
	Log::message("the left mouse button was released\n");
}

```


### Arguments

- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - One of the preset [MOUSE_BUTTON_](#MOUSE_BUTTON) codes.

### Return value

1 during the first frame when the mouse button was released; otherwise, 0.
## bool isTouchPressed ( int index ) const

Returns a value indicating if the touchscreen is pressed by the finger.
### Arguments

- *int* **index** - Touch input index.

### Return value

true if the touchscreen is pressed; otherwise, false.
## bool isTouchDown ( int index ) const

Returns a value indicating if the given touch was pressed during the current frame.
### Arguments

- *int* **index** - Touch input index.

### Return value

true if the touchscreen is pressed during the current frame; otherwise, false.
## bool isTouchUp ( int index ) const

Returns a value indicating if the given touch was released.
### Arguments

- *int* **index** - Touch input index.

### Return value

true during the first frame when the touch was released; otherwise, false.
## Math:: ivec2 getTouchPosition ( int index ) const

Returns a vector containing integer values of touch position.
### Arguments

- *int* **index** - Touch input index.

### Return value

The touch position.
## Math:: ivec2 getTouchDelta ( int index ) const

Returns a vector containing screen position change of the touch along the X and Y axes � the difference between the values in the previous and the current frames.
### Arguments

- *int* **index** - Touch input index.

### Return value

The touch position delta.
## Ptr < InputEventTouch > getTouchEvent ( int index )

Returns the action cast to the touch event.
### Arguments

- *int* **index** - Touch input index.

### Return value

Touch input event.
## int getTouchEvents ( int index , Vector < Ptr < InputEventTouch >> & OUT_events )

Returns the actions cast to the touch event.
### Arguments

- *int* **index** - Touch input index.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEventTouch](../../../api/library/controls/class.inputeventtouch_cpp.md)>> &* **OUT_events** - The buffer with touch input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of touch input events.
## Ptr < InputEventKeyboard > getKeyEvent ( Input::KEY key )

Returns the currently processed keyboard input event.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the preset [KEY_](#KEY) codes.

### Return value

Keyboard input event, or nullptr if there are no events for the specified key in the current frame.
## int getKeyEvents ( Input::KEY key , Vector < Ptr < InputEventKeyboard >> & OUT_events )

Returns the buffer with events for the specified key.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the preset [KEY_](#KEY) codes.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEventKeyboard](../../../api/library/controls/class.inputeventkeyboard_cpp.md)>> &* **OUT_events** - The buffer with input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## const char * getKeyName ( Input::KEY key ) const

Returns the specified key name.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the preset [KEY_](#KEY) codes.

### Return value

Key name.
## Input::KEY getKeyByName ( const char * name ) const

Returns the key by its name.
### Arguments

- *const char ** **name** - Key name.

### Return value

One of the preset [KEY_](#KEY) codes.
## Ptr < InputEventMouseButton > getMouseButtonEvent ( Input::MOUSE_BUTTON button )

Returns the mouse motion input event for the specified button.
### Arguments

- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - One of the preset [MOUSE_BUTTON_](#MOUSE_BUTTON) codes.

### Return value

Mouse motion input event.
## const char * getMouseButtonName ( Input::MOUSE_BUTTON button ) const

Returns the mouse button name.
### Arguments

- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - One of the preset [MOUSE_BUTTON_](#MOUSE_BUTTON) codes.

### Return value

Mouse button name.
## Input::MOUSE_BUTTON getMouseButtonByName ( const char * name ) const

Returns the mouse button by its name.
### Arguments

- *const char ** **name** - Mouse button name.

### Return value

One of the preset [MOUSE_BUTTON_](#MOUSE_BUTTON) codes.
## int getEventsBuffer ( int frame , Vector < Ptr < InputEvent >> & OUT_events ) const

Returns the buffer with the input events for the specified frame.
### Arguments

- *int* **frame** - Number of frame for which the buffer of input events is to be obtained. Input events are stored for the last 60 frames. 0 is the current frame, 1 is the previous frame, etc.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEvent](../../../api/library/controls/class.inputevent_cpp.md)>> &* **OUT_events** - The buffer with input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void sendEvent ( const Ptr < InputEvent > & e )

Creates a user event and dispatches it to the Engine.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEvent](../../../api/library/controls/class.inputevent_cpp.md)> &* **e** - Input event.

## void setEventsFilter ( int (*)(const Ptr < InputEvent > &) func )

Sets a callback function to be executed on receiving input events. This input event filter enables you to reject certain input events for the Engine and get necessary information on all input events.
### Arguments

- *int (*)(const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEvent](../../../api/library/controls/class.inputevent_cpp.md)> &)* **func** - Input event callback.

## bool isModifierEnabled ( Input::MODIFIER modifier ) const

Returns the value indicating if the specified modifier is enabled.
### Arguments

- *[Input::MODIFIER](../../../api/library/controls/class.input_cpp.md#MODIFIER)* **modifier** - One of the preset [MODIFIER_](#MODIFIER_LEFT_SHIFT) codes.

### Return value

true if the modifier is enabled; otherwise, false.
## unsigned int keyToUnicode ( Input::KEY key ) const

Returns the specified key transformed to unicode.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the preset [KEY_](#KEY) codes.

### Return value

Unicode symbol.
## Input::KEY unicodeToKey ( unsigned int unicode ) const

Returns the specified key transformed to unicode.
### Arguments

- *unsigned int* **unicode** - Unicode symbol.

### Return value

One of the preset [KEY_](#KEY) codes.
## void setMouseCursorSkinCustom ( const Ptr < Image > & image )

Sets a custom image to be used for the mouse cursor.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image containing pointer shapes to be set for the mouse cursor (e.g., select, move, resize, etc.).

## void setMouseCursorSkinSystem ( )

Sets the current OS cursor skin (pointer shapes like select, move, resize, etc.).
## void setMouseCursorSkinDefault ( )

Sets the default Engine cursor skin (pointer shapes like select, move, resize, etc.).
## void setMouseCursorCustom ( const Ptr < Image > & image , int x = 0 , int y = 0 )

Sets a custom image for the OS mouse cursor. The image must be of the square size and *RGBA8* format.
```cpp
// create an instance of the Image class
ImagePtr cursor = Image::create("textures/my_cursor.png");
// set the image as the mouse cursor
Input::setMouseCursorCustom(cursor);
// show the OS mouse pointer
Input::setMouseCursorSystem(1);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Cursor image to be set.
- *int* **x** - X coordinate of the cursor's hot spot.
- *int* **y** - Y coordinate of the cursor's hot spot.

## void clearMouseCursorCustom ( )

Clears the custom mouse cursor set via the [setMouseCursorCustom()](#setMouseCursorCustom_Image_int_int_void) method.
## void updateMouseCursor ( )

Updates the mouse cursor. This method should be called after making changes to the mouse cursor to apply them all together. After calling this method the cursor shall be updated in the next frame.
## const char * getKeyLocalName ( Input::KEY key ) const

Returns the name for the specified key taken from the currently selected keyboard layout.
> **Notice:** The returned value is affected by the modifier such as Shift.


### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the preset [KEY_](#KEY) codes.

### Return value

Localized name for the specified key.
## int getMouseButtonEvents ( Input::MOUSE_BUTTON button , Vector < Ptr < InputEventMouseButton >> & OUT_events )

Returns the number of input events for the specified mouse button and puts the events to the specified output buffer.
### Arguments

- *[Input::MOUSE_BUTTON](../../../api/library/controls/class.input_cpp.md#MOUSE_BUTTON)* **button** - One of the preset [MOUSE_BUTTON_](#MOUSE_BUTTON) codes.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEventMouseButton](../../../api/library/controls/class.inputeventmousebutton_cpp.md)>> &* **OUT_events** - Buffer with input events. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of input events for the specified mouse button.
## Math:: ivec2 getForceMousePosition ( )

Returns the absolute mouse position obtained from the OS.
### Return value

The absolute mouse position.
## bool isKeyText ( Input::KEY key ) const

Returns a value indicating if the given key has a corresponding printable symbol (current Num Lock state is taken into account). For example, pressing 2 on the numpad with *Num Lock* enabled produces "2", while with disabled *Num Lock* the same key acts as a down arrow. Keys like *Esc, PrintScreen, BackSpace* do not produce any printable symbol at all.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - One of the preset [KEY_](#KEY) codes.

### Return value

true if the key value is a symbol; otherwise, false.
## const char * getModifierName ( Input::MODIFIER modifier ) const

Returns the name of the key modifier by its scancode.
### Arguments

- *[Input::MODIFIER](../../../api/library/controls/class.input_cpp.md#MODIFIER)* **modifier** - Scancode of the modifier.

### Return value

Key name of the modifier.
## Input::MODIFIER getModifierByName ( const char * name ) const

Returns the scancode of the key modifier by its name.
### Arguments

- *const char ** **name** - Key name of the modifier.

### Return value

Scancode of the modifier.
## Ptr < InputVRDevice > getVRDevice ( int num ) const

Returns the VR device by its number.
### Arguments

- *int* **num** - Number of the VR device.

### Return value

VR device.
## void setIMETextInputRect ( int position_x , int position_y , int width , int height )

Tells the operating system where the text caret or edit area is located, so that the IME composition and candidate window can be positioned next to it. Has no effect if text input is not currently active.
### Arguments

- *int* **position_x** - Horizontal position of the top-left corner of the text input rectangle, in render pixels relative to the engine window.
- *int* **position_y** - Vertical position of the top-left corner of the text input rectangle, in render pixels relative to the engine window.
- *int* **width** - Width of the text input rectangle, in pixels.
- *int* **height** - Height of the text input rectangle, in pixels.
