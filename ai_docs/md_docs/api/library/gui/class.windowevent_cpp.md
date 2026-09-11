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

## WindowEvent::TYPE getType () const

Returns the current type of the window event. One of the [WINDOW_EVENT_*](#WINDOW_EVENT) values.
### Return value

Current type of the window event
## const char * getTypeName () const

Returns the current name of the window event.
### Return value

Current name of the window event
## void setTimestamp ( unsigned long long timestamp )

Sets a new timestamp of the event, in milliseconds.
### Arguments

- *unsigned long long* **timestamp** - The timestamp of the event

## unsigned long long getTimestamp () const

Returns the current timestamp of the event, in milliseconds.
### Return value

Current timestamp of the event
## void setWinID ( unsigned long long id )

Sets a new identifier of the window.
### Arguments

- *unsigned long long* **id** - The identifier of the window

## unsigned long long getWinID () const

Returns the current identifier of the window.
### Return value

Current identifier of the window
## void setMousePosition ( const Math:: ivec2 & position )

Sets a new mouse position at the event creation.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **position** - The mouse position at the event creation

## Math:: ivec2 getMousePosition () const

Returns the current mouse position at the event creation.
### Return value

Current mouse position at the event creation
## void setPosition ( const Math:: ivec2 & position )

Sets a new window position at the event creation.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **position** - The window position at the event creation

## Math:: ivec2 getPosition () const

Returns the current window position at the event creation.
### Return value

Current window position at the event creation
## void setSize ( const Math:: ivec2 & size )

Sets a new window size at the event creation.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **size** - The window size at the event creation

## Math:: ivec2 getSize () const

Returns the current window size at the event creation.
### Return value

Current window size at the event creation
## void setWindow ( const Ptr < EngineWindow >& window )

Sets a new window for which the event has been created.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)>&* **window** - The window for which the event has been created

## Ptr < EngineWindow > getWindow () const

Returns the current window for which the event has been created.
### Return value

Current window for which the event has been created
