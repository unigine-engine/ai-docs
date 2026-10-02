# Unigine::InputEvent Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class handles input event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEvent Class

### Members

---

## int getType ( )

Returns the type of the event � one of the [TYPE](#TYPE) values. Use it to find out which subclass the event can be cast to.
### Return value

The type of the input event, one of the [INPUT_EVENT](#INPUT_EVENT) values.
## string getTypeName ( )

Returns the name of the event class as a string, InputEventMouseButton for example. Intended for logging and debugging.
### Return value

The name of the input event type.
## void setTimestamp ( long timestamp )

Sets the timestamp of the event.
### Arguments

- *long* **timestamp** - The timestamp of the event, in milliseconds.

## long getTimestamp ( )

Returns the moment the event was received, in milliseconds. The value originates from the input backend, so use it to order events and to measure intervals between them rather than as an absolute time.
### Return value

The timestamp of the event, in milliseconds.
## void setMousePosition ( ivec2 pos )

Sets the mouse position for the event.
### Arguments

- *ivec2* **pos** - The position of the mouse.

## ivec2 getMousePosition ( )

Returns the mouse cursor position at the moment the event was received, in global (desktop) coordinates. Every input event carries it, including the events that have nothing to do with the mouse.
### Return value

The position of the mouse.
## long getFrame ( )

Returns the engine frame during which the event has been sent from proxy to Input.
### Return value

The engine frame during which the event has been sent from proxy to Input.
