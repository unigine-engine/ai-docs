# Unigine::WindowEventDpi Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WindowEvent


## WindowEventDpi Class

### Members

## void setAction ( int action )

Sets a new type of the DPI action performed with the window during the event.
### Arguments

- *int* **action** - The type of the DPI action performed with the window during the event

## int getAction () const

Returns the current type of the DPI action performed with the window during the event.
### Return value

Current type of the DPI action performed with the window during the event
## void setDpi ( int dpi )

Sets a new DPI level.
### Arguments

- *int* **dpi** - The DPI level

## int getDpi () const

Returns the current DPI level.
### Return value

Current DPI level
---

## WindowEventDpi ( )

Default constructor.
## WindowEventDpi ( long timestamp , long win_id )

Window DPI event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - The window for which DPI is set.

## WindowEventDpi ( long timestamp , long win_id , ivec2 mouse_pos )

Window DPI event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - The window for which DPI is set.
- *ivec2* **mouse_pos** - Position of the mouse.

## WindowEventDpi ( long timestamp , long win_id , ivec2 mouse_pos , ivec2 position , ivec2 size )

Window DPI event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - The window for which DPI is set.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.

## WindowEventDpi ( long timestamp , long win_id , ivec2 mouse_pos , ivec2 position , ivec2 size , int action , int dpi )

Window DPI event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - The window for which DPI is set.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.
- *int* **action** - Type of the DPI action performed with the window during the event.
- *int* **dpi** - The DPI level.
