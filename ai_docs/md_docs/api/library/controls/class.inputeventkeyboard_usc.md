# Unigine::InputEventKeyboard Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls keyboard event information.


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

Sets the action to be performed by the keyboard.
### Arguments

- *int* **action** - Action performed by the keyboard.

## int getAction ( )

Returns the action performed by the mouse button.
### Return value

Action performed by the keyboard.
## void setKey ( int key )

Sets the keyboard key language-dependent value.
### Arguments

- *int* **key** - Virtual keyboard key value (dependent on the keyboard language).

## int getKey ( )

Returns the keyboard key language-dependent value.
### Return value

Virtual keyboard key value (dependent on the keyboard language).
