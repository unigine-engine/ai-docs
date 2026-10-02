# Unigine::InputEventMouseWheel Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls mouse wheel event information.


Events of this type are created by the engine and passed to your handlers. You can also construct one yourself and dispatch it via *[engine.input.sendEvent()()](../../../api/library/controls/class.input_usc.md#sendEvent_InputEvent_void)*, which is what a custom SystemProxy implementation or a device emulator does.


## InputEventMouseWheel Class

### Members

---

## static InputEventMouseWheel ( )

Default constructor.
## InputEventMouseWheel ( long timestamp , ivec2 mouse_pos )

Mouse wheel input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventMouseWheel ( long timestamp , ivec2 mouse_pos , int wheel , int wheel_h )

Mouse wheel input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *int* **wheel** - Delta amount scrolled vertically (positive value - away from the user, negative - towards the user.
- *int* **wheel_h** - Delta amount scrolled horizontally (positive value - to the right, negative - to the left).

## void setWheel ( int wheel )

Sets the delta of the vertical mouse scroll movement.
### Arguments

- *int* **wheel** - The amount scrolled vertically, positive away from the user and negative towards the user.

## int getWheel ( )

Returns the vertical scroll amount carried by this event. Negative values correspond to scrolling downwards, positive ones � upwards. Unlike [Input::MouseWheel](../../../api/library/controls/class.input_usc.md#MouseWheel), which sums up the whole frame, this is the amount of a single event.
### Return value

The amount scrolled vertically, positive away from the user and negative towards the user.
## void setWheelHorizontal ( int horizontal )

Sets the delta of the horizontal mouse scroll movement.
### Arguments

- *int* **horizontal** - The amount scrolled horizontally, positive to the right and negative to the left.

## int getWheelHorizontal ( )

Returns the horizontal scroll amount carried by this event. Negative values correspond to scrolling leftwards, positive ones � rightwards. Unlike [Input::MouseWheelHorizontal](../../../api/library/controls/class.input_usc.md#MouseWheelHorizontal), which sums up the whole frame, this is the amount of a single event.
### Return value

The amount scrolled horizontally, positive to the right and negative to the left.
