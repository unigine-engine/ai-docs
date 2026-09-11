# Unigine::WindowEventGeneric Class (CPP)

**Header:** #include <UnigineWindowManager.h>

**Inherits from:** WindowEvent


This class is used to get the type of the window event.


## WindowEventGeneric Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_RESIZED** = 0 | Window has been resized. This event is always preceded by [ACTION_SIZE_CHANGED](#ACTION_SIZE_CHANGED). |
| **ACTION_MOVED** = 1 | Window has been moved. |
| **ACTION_SIZE_CHANGED** = 2 | Window size has changed either as a result of an API call or through the system or user changing the window size. This event is followed by [ACTION_RESIZED](#ACTION_RESIZED) if the size was changed by an external event, i.e. the user or the window manager. |
| **ACTION_FOCUS_GAINED** = 3 | Window has gained keyboard focus. |
| **ACTION_FOCUS_LOST** = 4 | Window has lost keyboard focus. |
| **ACTION_MOUSE_ENTER** = 5 | Window has gained mouse focus. |
| **ACTION_MOUSE_LEAVE** = 6 | Window has lost mouse focus. |
| **ACTION_SHOWN** = 7 | Window has been shown. |
| **ACTION_HIDDEN** = 8 | Window has been hidden. |
| **ACTION_MINIMIZED** = 9 | Window has been minimized. |
| **ACTION_MAXIMIZED** = 10 | Window has been maximized. |
| **ACTION_RESTORED** = 11 | Window has been restored to normal size and position. |
| **ACTION_CLOSE** = 12 | The window manager requests the window to be closed. |
| **ACTION_UNSTACK_MOVE** = 13 | Window has been unstacked and pulled out of the group. |

### Members

## void setAction ( WindowEventGeneric::ACTION action )

Sets a new type of the generic action performed with the window during the event.
### Arguments

- *[WindowEventGeneric::ACTION](../../../api/library/gui/class.windoweventgeneric_cpp.md#ACTION)* **action** - The type of the generic action performed with the window during the event

## WindowEventGeneric::ACTION getAction () const

Returns the current type of the generic action performed with the window during the event.
### Return value

Current type of the generic action performed with the window during the event
---

## WindowEventGeneric ( )

Default constructor.
## WindowEventGeneric ( unsigned long long timestamp , unsigned long long win_id )

Generic window event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - Identifier of the window.

## WindowEventGeneric ( unsigned long long timestamp , unsigned long long win_id , const Math:: ivec2 & mouse_pos )

Generic window event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - Identifier of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Mouse position.

## WindowEventGeneric ( unsigned long long timestamp , unsigned long long win_id , const Math:: ivec2 & mouse_pos , const Math:: ivec2 & position , const Math:: ivec2 & size )

Generic window event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - Identifier of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **position** - Position of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **size** - Size of the window.

## WindowEventGeneric ( unsigned long long timestamp , unsigned long long win_id , const Math:: ivec2 & mouse_pos , const Math:: ivec2 & position , const Math:: ivec2 & size , WindowEventGeneric::ACTION action )

Generic window event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - Identifier of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **position** - Position of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **size** - Size of the window.
- *[WindowEventGeneric::ACTION](../../../api/library/gui/class.windoweventgeneric_cpp.md#ACTION)* **action** - Type of the generic action performed with the window during the event.
