# Unigine::InputEventMouseMotion Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls mouse motion event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventMouseMotion Class

### Members

---

## InputEventMouseMotion ( )

Default constructor.
## InputEventMouseMotion ( long timestamp , ivec2 mouse_pos , ivec2 delta )

Mouse motion input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **delta** - Delta of the mouse position from the previous event.

## InputEventMouseMotion ( long timestamp , ivec2 mouse_pos )

Mouse motion input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## void setDelta ( ivec2 delta )

Sets the delta of the mouse position from the previous event.
### Arguments

- *ivec2* **delta** - Delta of the mouse position from the previous event.

## ivec2 getDelta ( )

Returns the raw movement reported by the mouse for this event. The value comes from the raw input of the OS, so it is not affected by pointer acceleration or desktop sensitivity settings and is not limited by the screen borders. [Input::MouseDeltaRaw](../../../api/library/controls/class.input_usc.md#MouseDeltaRaw) is the sum of these values over the frame.
### Return value

Delta of the mouse position from the previous event.
