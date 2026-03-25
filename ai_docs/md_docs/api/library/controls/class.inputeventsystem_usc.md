# Unigine::InputEventSystem Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls system events such as changing the input language of the keyboard layout.


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

Sets the action for the system event.
### Arguments

- *int* **action** - New action to be set for the system event.

## int getAction ( )

Returns the action of the system event.
### Return value

Current system event action.
