# Unigine::WindowEventDrop Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WindowEvent


This class is used to handle an event of dragging and dropping a text or file into a window.


## WindowEventDrop Class

### Members

## void setAction ( int action )

Sets a new type of the drop action performed with the window during the event.
### Arguments

- *int* **action** - The type of the drop action performed with the window during the event

## int getAction () const

Returns the current type of the drop action performed with the window during the event.
### Return value

Current type of the drop action performed with the window during the event
## void setPath ( string path )

Sets a new absolute path to the dropped file.
### Arguments

- *string* **path** - The absolute path to the dropped file

## const char * getPath () const

Returns the current absolute path to the dropped file.
### Return value

Current absolute path to the dropped file
---

## WindowEventDrop ( )

Default constructor.
## WindowEventDrop ( long timestamp , long win_id )

Window drop event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - The window that was dropped on, if any.

## WindowEventDrop ( long timestamp , long win_id , ivec2 mouse_pos )

Window drop event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - The window that was dropped on, if any.
- *ivec2* **mouse_pos** - Position of the mouse.

## WindowEventDrop ( long timestamp , long win_id , ivec2 mouse_pos , ivec2 position , ivec2 size )

Window drop event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - The window that was dropped on, if any.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.

## WindowEventDrop ( long timestamp , long win_id , ivec2 mouse_pos , ivec2 position , ivec2 size , int action , string item_path )

Window drop event constructor.
### Arguments

- *long* **timestamp** - Timestamp of the event.
- *long* **win_id** - The window that was dropped on, if any.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.
- *int* **action** - Type of the drop action performed with the window during the event.
- *string* **item_path**
