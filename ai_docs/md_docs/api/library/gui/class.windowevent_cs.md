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

The type of the window event, one of the [TYPE](#TYPE) values.
## 🔒︎ string TypeName

The name of the window event.
## ulong Timestamp

The timestamp of the event, in milliseconds.
## ulong WinID

The identifier of the window.
## ivec2 MousePosition

The position of the mouse at the event creation.
## ivec2 Position

The position of the window at the event creation.
## ivec2 Size

The size of the window at the event creation.
## EngineWindow Window

The window for which the event has been created.
### Members

---
