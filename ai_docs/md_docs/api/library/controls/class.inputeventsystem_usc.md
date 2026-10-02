# Unigine::InputEventSystem Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls system events such as changing the input language of the keyboard layout.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventSystem Class

### Members

---

## InputEventSystem ( )

Default constructor.
## InputEventSystem ( unsigned int timestamp , ivec2 mouse_pos )

Default constructor.
### Arguments

- *unsigned int* **timestamp** - Timestamp of the event (time when the event occurred).
- *ivec2* **mouse_pos** - Coordinates of the mouse cursor position along X and Y axes.

## InputEventSystem ( unsigned int timestamp , ivec2 mouse_pos , int action )

Default constructor.
### Arguments

- *unsigned int* **timestamp** - Timestamp of the event (time when the event occurred).
- *ivec2* **mouse_pos** - Coordinates of the mouse cursor position along X and Y axes.
- *int* **action** - action of the system event.

## void setAction ( int action )

Sets the action the event represents. See *[getAction()()](../../...md#getAction_int)*.
### Arguments

- *int* **action** - New action to be set for the system event.

## int getAction ( )

Returns the action the event represents: one of the [ACTION](#ACTION) values. Currently the only system event reported is a change of the keyboard layout.
### Return value

Current system event action.
