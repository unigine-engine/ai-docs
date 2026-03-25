# Unigine::WindowEvent Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The class to process window events. It allows getting the type, time of creation, position, size and id of the window for which the event has been created.


## WindowEvent Class

### Members

---

## int getType ( )

Returns the type of the window event.
### Return value

Type of the window event, one of the [WINDOW_EVENT_WINDOW_EVENT](#WINDOW_EVENT) values.
## string getTypeName ( )

Returns the name of the window event.
### Return value

The name of the window event.
## void setTimestamp ( long timestamp )

Sets a timestamp of the event.
### Arguments

- *long* **timestamp** - Timestamp of the event, in milliseconds.

## long getTimestamp ( )

Returns the timestamp of the event.
### Return value

The timestamp of the event, in milliseconds.
## void setWinID ( long winid )

Sets the identifier of the window.
### Arguments

- *long* **winid** - Identifier of the window.

## long getWinID ( )

Returns the identifier of the window.
### Return value

The identifier of the window.
## void setMousePosition ( ivec2 position )

Sets the position of the mouse at the event creation.
### Arguments

- *ivec2* **position** - Position of the mouse at the event creation.

## ivec2 getMousePosition ( )

Returns the mouse position at the event creation.
### Return value

The position of the mouse at the event creation.
## void setPosition ( ivec2 position )

Sets the window position at the event creation.
### Arguments

- *ivec2* **position** - Position of the window at the event creation.

## ivec2 getPosition ( )

Returns the window position at the event creation.
### Return value

The position of the window at the event creation.
## void setSize ( ivec2 size )

Sets the window size at the event creation.
### Arguments

- *ivec2* **size** - Size of the window at the event creation.

## ivec2 getSize ( )

Returns the window size at the event creation.
### Return value

The size of the window at the event creation.
## void setWindow ( EngineWindow window )

Sets the window for which the event has been created.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - Window for which the event has been created.

## EngineWindow getWindow ( )

Returns the window for which the event has been created.
### Return value

The window for which the event has been created.
