# Unigine::WindowEvent Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The class to process window events. It allows getting the type, time of creation, position, size and id of the window for which the event has been created.


## WindowEvent Class

### Members

## int getType () const

Returns the current type of the window event. One of the [WINDOW_EVENT_*](#WINDOW_EVENT) values.
### Return value

Current type of the window event
## const char * getTypeName () const

Returns the current name of the window event.
### Return value

Current name of the window event
## void setTimestamp ( long timestamp )

Sets a new timestamp of the event, in milliseconds.
### Arguments

- *long* **timestamp** - The timestamp of the event

## long getTimestamp () const

Returns the current timestamp of the event, in milliseconds.
### Return value

Current timestamp of the event
## void setWinID ( long id )

Sets a new identifier of the window.
### Arguments

- *long* **id** - The identifier of the window

## long getWinID () const

Returns the current identifier of the window.
### Return value

Current identifier of the window
## void setMousePosition ( ivec2 position )

Sets a new mouse position at the event creation.
### Arguments

- *ivec2* **position** - The mouse position at the event creation

## ivec2 getMousePosition () const

Returns the current mouse position at the event creation.
### Return value

Current mouse position at the event creation
## void setPosition ( ivec2 position )

Sets a new window position at the event creation.
### Arguments

- *ivec2* **position** - The window position at the event creation

## ivec2 getPosition () const

Returns the current window position at the event creation.
### Return value

Current window position at the event creation
## void setSize ( ivec2 size )

Sets a new window size at the event creation.
### Arguments

- *ivec2* **size** - The window size at the event creation

## ivec2 getSize () const

Returns the current window size at the event creation.
### Return value

Current window size at the event creation
## void setWindow ( EngineWindow window )

Sets a new window for which the event has been created.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_usc.md)* **window** - The window for which the event has been created

## EngineWindow getWindow () const

Returns the current window for which the event has been created.
### Return value

Current window for which the event has been created
