# Unigine::WindowEvent Class (CS)


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

### Properties

## 🔒︎ WindowEvent.TYPE Type

The type of the window event. One of the [WINDOW_EVENT_*](#WINDOW_EVENT) values.
## 🔒︎ string TypeName

The name of the window event.
## ullong Timestamp

The timestamp of the event, in milliseconds.
## ullong WinID

The identifier of the window.
## ivec2 MousePosition

The mouse position at the event creation.
## ivec2 Position

The window position at the event creation.
## ivec2 Size

The window size at the event creation.
## EngineWindow Window

The window for which the event has been created.
