# Unigine::InputEventSystem Class (CPP)

**Header:** #include <UnigineInput.h>

**Inherits from:** InputEvent


This class controls system events such as changing the input language of the keyboard layout.


## InputEventSystem Class

### Enums

## ACTION

System event actions.
| Name | Description |
|---|---|
| **ACTION_KEYBOARD_LAYOUT_CHANGED** = 0 | Keyboard layout has changed. |

### Members

---

## InputEventSystem ( )

Default constructor.
## InputEventSystem ( unsigned int timestamp , const Math:: ivec2 & mouse_pos )

Default constructor.
### Arguments

- *unsigned int* **timestamp** - Timestamp of the event (time when the event occurred).
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Coordinates of the mouse cursor position along X and Y axes.

## InputEventSystem ( unsigned int timestamp , const Math:: ivec2 & mouse_pos , InputEventSystem::ACTION action )

Default constructor.
### Arguments

- *unsigned int* **timestamp** - Timestamp of the event (time when the event occurred).
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Coordinates of the mouse cursor position along X and Y axes.
- *[InputEventSystem::ACTION](../../../api/library/controls/class.inputeventsystem_cpp.md#ACTION)* **action** - action of the system event.

## void setAction ( InputEventSystem::ACTION action )

Sets the action for the system event.
### Arguments

- *[InputEventSystem::ACTION](../../../api/library/controls/class.inputeventsystem_cpp.md#ACTION)* **action** - New action to be set for the system event.

## InputEventSystem::ACTION getAction ( ) const

Returns the action of the system event.
### Return value

Current system event action.
