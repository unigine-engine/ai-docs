# Unigine::WindowEvent Class (CPP)

**Header:** #include <UnigineWindowManager.h>


The class to process window events. It allows getting the type, time of creation, position, size and id of the window for which the event has been created.


## WindowEvent Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **WINDOW_EVENT** = 0 | Window state change. |
| **WINDOW_EVENT_GENERIC** = 1 | Event of window transformation (such as moving, resizing, collapsing, etc.). |
| **WINDOW_EVENT_DROP** = 2 | Event of dragging and dropping a file or folder into a window. |
| **WINDOW_EVENT_DPI** = 3 | Event of changing the DPI level. |
| **NUM_WINDOW_EVENTS** = 4 | Event counter. |

### Members

---

## WindowEvent::TYPE getType ( ) const

Returns the type of the window event.
### Return value

Type of the window event, one of the [TYPE.WINDOW_EVENT](#TYPE) values.
## const char * getTypeName ( ) const

Returns the name of the window event.
### Return value

The name of the window event.
## void setTimestamp ( unsigned long long timestamp )

Sets a timestamp of the event.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event, in milliseconds.

## unsigned long long getTimestamp ( ) const

Returns the timestamp of the event.
### Return value

The timestamp of the event, in milliseconds.
## void setWinID ( unsigned long long winid )

Sets the identifier of the window.
### Arguments

- *unsigned long long* **winid** - Identifier of the window.

## unsigned long long getWinID ( ) const

Returns the identifier of the window.
### Return value

The identifier of the window.
## void setMousePosition ( const Math:: ivec2 & position )

Sets the position of the mouse at the event creation.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **position** - Position of the mouse at the event creation.

## Math:: ivec2 getMousePosition ( ) const

Returns the mouse position at the event creation.
### Return value

The position of the mouse at the event creation.
## void setPosition ( const Math:: ivec2 & position )

Sets the window position at the event creation.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **position** - Position of the window at the event creation.

## Math:: ivec2 getPosition ( ) const

Returns the window position at the event creation.
### Return value

The position of the window at the event creation.
## void setSize ( const Math:: ivec2 & size )

Sets the window size at the event creation.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **size** - Size of the window at the event creation.

## Math:: ivec2 getSize ( ) const

Returns the window size at the event creation.
### Return value

The size of the window at the event creation.
## void setWindow ( const Ptr < EngineWindow > & window )

Sets the window for which the event has been created.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - Window for which the event has been created.

## Ptr < EngineWindow > getWindow ( ) const

Returns the window for which the event has been created.
### Return value

The window for which the event has been created.
