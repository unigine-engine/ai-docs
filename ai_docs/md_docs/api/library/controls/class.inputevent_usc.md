# Unigine::InputEvent Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class handles input event information.


## InputEvent Class

### Members

---

## int getType ( )

Returns the type of the input event.
### Return value

The type of the input event, one of the [INPUT_EVENT](#INPUT_EVENT) values.
## string getTypeName ( )

Returns the name of the input event type.
### Return value

The name of the input event type.
## void setTimestamp ( unsigned int timestamp )

Sets the timestamp of the event.
### Arguments

- *unsigned int* **timestamp** - The timestamp of the event, in milliseconds.

## unsigned int getTimestamp ( )

Returns the timestamp of the event.
### Return value

The timestamp of the event, in milliseconds.
## void setMousePosition ( ivec2 pos )

Sets the mouse position for the event.
### Arguments

- *ivec2* **pos** - The position of the mouse.

## ivec2 getMousePosition ( )

Returns the mouse position for the event.
### Return value

The position of the mouse.
## long getFrame ( )

Returns the engine frame during which the event has been sent from proxy to Input.
### Return value

The engine frame during which the event has been sent from proxy to Input.
