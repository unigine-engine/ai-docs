# Unigine::InputEventText Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** InputEvent


This class controls text event information.


## InputEventText Class

### Members

---

## InputEventText ( )

Default constructor.
## InputEventText ( long timestamp , ivec2 mouse_pos )

Text input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.

## InputEventText ( long timestamp , ivec2 mouse_pos , unsigned int unicode )

Text input event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *ivec2* **mouse_pos** - Position of the mouse.
- *unsigned int* **unicode** - Unicode symbol.

## void setUnicode ( unsigned int unicode )

Sets the input symbol.
### Arguments

- *unsigned int* **unicode** - Unicode symbol.

## unsigned int getUnicode ( )

Returns the input symbol.
### Return value

Unicode symbol.
