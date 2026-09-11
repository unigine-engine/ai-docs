# Unigine::WindowEventGeneric Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WindowEvent


This class is used to get the type of the window event.


## WindowEventGeneric Class

### Members

## void setAction ( int action )

Sets a new type of the generic action performed with the window during the event.
### Arguments

- *int* **action** - The type of the generic action performed with the window during the event

## int getAction () const

Returns the current type of the generic action performed with the window during the event.
### Return value

Current type of the generic action performed with the window during the event
---

## WindowEventGeneric ( )

Default constructor.
## WindowEventGeneric ( long timestamp , long win_id )

Generic window event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - Identifier of the window.

## WindowEventGeneric ( long timestamp , long win_id , ivec2 mouse_pos )

Generic window event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - Identifier of the window.
- *ivec2* **mouse_pos** - Mouse position.

## WindowEventGeneric ( long timestamp , long win_id , ivec2 mouse_pos , ivec2 position , ivec2 size )

Generic window event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - Identifier of the window.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.

## WindowEventGeneric ( long timestamp , long win_id , ivec2 mouse_pos , ivec2 position , ivec2 size , int action )

Generic window event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - Identifier of the window.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.
- *int* **action** - Type of the generic action performed with the window during the event.
