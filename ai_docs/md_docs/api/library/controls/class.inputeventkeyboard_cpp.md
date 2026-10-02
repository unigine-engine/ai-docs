# Unigine::InputEventKeyboard Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls keyboard event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[Input::sendEvent()](../../../api/library/controls/class.input_cpp.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


### See Also


- C++ sample
- C# Component sample


## InputEventKeyboard Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DOWN** = 0 | Keyboard button is held down. |
| **ACTION_REPEAT** = 1 | Keyboard button has been pressed repeatedly. |
| **ACTION_UP** = 2 | Keyboard button has been released. |

### Members

---

## InputEventKeyboard ( )

Default constructor.
## InputEventKeyboard ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos , InputEventKeyboard::ACTION action , Input::KEY key )

Keyboard input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *[InputEventKeyboard::ACTION](../../../api/library/controls/class.inputeventkeyboard_cpp.md#ACTION)* **action** - Action performed.
- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - Virtual keyboard key value (dependent on the language).

## InputEventKeyboard ( unsigned long long timestamp , const Math:: ivec2 & mouse_pos )

Keyboard input event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## void setAction ( InputEventKeyboard::ACTION action )

Sets the action the event represents. See *[getAction()](../../...md#getAction_int)*.
### Arguments

- *[InputEventKeyboard::ACTION](../../../api/library/controls/class.inputeventkeyboard_cpp.md#ACTION)* **action** - Action performed by the keyboard.

## InputEventKeyboard::ACTION getAction ( ) const

Returns the action the event represents: one of the [ACTION](#ACTION) values � the key was pressed, auto-repeated while held, or released.
### Return value

Action performed by the keyboard.
## void setKey ( Input::KEY key )

Sets the keyboard key language-dependent value.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - Virtual keyboard key value (dependent on the keyboard language).

## Input::KEY getKey ( ) const

Returns the key the event refers to � one of the [Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY) values. The code depends on the keyboard layout currently selected in the system.
### Return value

Virtual keyboard key value (dependent on the keyboard language).
