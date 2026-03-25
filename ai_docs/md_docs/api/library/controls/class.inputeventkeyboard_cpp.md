# Unigine::InputEventKeyboard Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls keyboard event information.


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

Sets the action to be performed by the keyboard.
### Arguments

- *[InputEventKeyboard::ACTION](../../../api/library/controls/class.inputeventkeyboard_cpp.md#ACTION)* **action** - Action performed by the keyboard.

## InputEventKeyboard::ACTION getAction ( ) const

Returns the action performed by the mouse button.
### Return value

Action performed by the keyboard.
## void setKey ( Input::KEY key )

Sets the keyboard key language-dependent value.
### Arguments

- *[Input::KEY](../../../api/library/controls/class.input_cpp.md#KEY)* **key** - Virtual keyboard key value (dependent on the keyboard language).

## Input::KEY getKey ( ) const

Returns the keyboard key language-dependent value.
### Return value

Virtual keyboard key value (dependent on the keyboard language).
