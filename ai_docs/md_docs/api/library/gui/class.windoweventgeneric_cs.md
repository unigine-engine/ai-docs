# Unigine::WindowEventGeneric Class (CS)

**Inherits from:** WindowEvent


This class is used to get the type of the window event.


## WindowEventGeneric Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **RESIZED** = 0 | Window has been resized. This event is always preceded by [ACTION.SIZE_CHANGED](#ACTION_SIZE_CHANGED). |
| **MOVED** = 1 | Window has been moved. |
| **SIZE_CHANGED** = 2 | Window size has changed either as a result of an API call or through the system or user changing the window size. This event is followed by [ACTION.RESIZED](#ACTION_RESIZED) if the size was changed by an external event, i.e. the user or the window manager. |
| **FOCUS_GAINED** = 3 | Window has gained keyboard focus. |
| **FOCUS_LOST** = 4 | Window has lost keyboard focus. |
| **MOUSE_ENTER** = 5 | Window has gained mouse focus. |
| **MOUSE_LEAVE** = 6 | Window has lost mouse focus. |
| **SHOWN** = 7 | Window has been shown. |
| **HIDDEN** = 8 | Window has been hidden. |
| **MINIMIZED** = 9 | Window has been minimized. |
| **MAXIMIZED** = 10 | Window has been maximized. |
| **RESTORED** = 11 | Window has been restored to normal size and position. |
| **CLOSE** = 12 | The window manager requests the window to be closed. |
| **UNSTACK_MOVE** = 13 | Window has been unstacked and pulled out of the group. |

### Properties

## WindowEventGeneric.ACTION Action

The type of the generic action performed with the window during the event.
### Members

---

## WindowEventGeneric ( )

Default constructor.
## WindowEventGeneric ( ulong timestamp , ulong win_id )

Generic window event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - Identifier of the window.

## WindowEventGeneric ( ulong timestamp , ulong win_id , ivec2 mouse_pos )

Generic window event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - Identifier of the window.
- *ivec2* **mouse_pos** - Mouse position.

## WindowEventGeneric ( ulong timestamp , ulong win_id , ivec2 mouse_pos , ivec2 position , ivec2 size )

Generic window event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - Identifier of the window.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.

## WindowEventGeneric ( ulong timestamp , ulong win_id , ivec2 mouse_pos , ivec2 position , ivec2 size , WindowEventGeneric.ACTION action )

Generic window event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - Identifier of the window.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.
- *[WindowEventGeneric.ACTION](../../../api/library/gui/class.windoweventgeneric_cs.md#ACTION)* **action** - Type of the generic action performed with the window during the event.
