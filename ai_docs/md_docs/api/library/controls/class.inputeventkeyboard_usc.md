# Unigine::InputEventKeyboard Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls keyboard event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventKeyboard Class

### Members

---

## InputEventKeyboard ( )

Default constructor.
## InputEventKeyboard ( long timestamp , ivec2 mouse_pos , int action , int key )

Keyboard input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **action** - Action performed.
- *int* **key** - Virtual keyboard key value (dependent on the language).

## InputEventKeyboard ( long timestamp , ivec2 mouse_pos )

Keyboard input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## void setAction ( int action )

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - Action performed by the keyboard.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values � the key was pressed, auto-repeated while held, or released.
### Return value

Action performed by the keyboard.
## void setKey ( int key )

Sets the keyboard key language-dependent value.
### Arguments

- *int* **key** - Virtual keyboard key value (dependent on the keyboard language).

## int getKey ( )

Returns the key the event refers to � one of the [Input::KEY](../../../api/library/controls/class.input_usc.md#KEY) values. The code depends on the keyboard layout currently selected in the system.
### Return value

Virtual keyboard key value (dependent on the keyboard language).
