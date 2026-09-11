# Unigine::WindowEventDrop Class (CPP)

**Header:** #include <UnigineWindowManager.h>

**Inherits from:** WindowEvent


This class is used to handle an event of dragging and dropping a text or file into a window.


## WindowEventDrop Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_ITEMS_DROP_BEGIN** = 0 | A new set of drops is beginning. |
| **ACTION_ITEM_DROP** = 1 | Text/plain drag-and-drop event. |
| **ACTION_ITEMS_DROP_END** = 2 | The current set of drops is now complete. |

### Members

## void setAction ( WindowEventDrop::ACTION action )

Sets a new type of the drop action performed with the window during the event.
### Arguments

- *[WindowEventDrop::ACTION](../../../api/library/gui/class.windoweventdrop_cpp.md#ACTION)* **action** - The type of the drop action performed with the window during the event

## WindowEventDrop::ACTION getAction () const

Returns the current type of the drop action performed with the window during the event.
### Return value

Current type of the drop action performed with the window during the event
## void setPath ( const char * path )

Sets a new absolute path to the dropped file.
### Arguments

- *const char ** **path** - The absolute path to the dropped file

## const char * getPath () const

Returns the current absolute path to the dropped file.
### Return value

Current absolute path to the dropped file
---

## WindowEventDrop ( )

Default constructor.
## WindowEventDrop ( unsigned long long timestamp , unsigned long long win_id )

Window drop event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - The window that was dropped on, if any.

## WindowEventDrop ( unsigned long long timestamp , unsigned long long win_id , const Math:: ivec2 & mouse_pos )

Window drop event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - The window that was dropped on, if any.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## WindowEventDrop ( unsigned long long timestamp , unsigned long long win_id , const Math:: ivec2 & mouse_pos , const Math:: ivec2 & position , const Math:: ivec2 & size )

Window drop event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - The window that was dropped on, if any.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **position** - Position of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **size** - Size of the window.

## WindowEventDrop ( unsigned long long timestamp , unsigned long long win_id , const Math:: ivec2 & mouse_pos , const Math:: ivec2 & position , const Math:: ivec2 & size , WindowEventDrop::ACTION action , const char * item_path )

Window drop event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - The window that was dropped on, if any.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **position** - Position of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **size** - Size of the window.
- *[WindowEventDrop::ACTION](../../../api/library/gui/class.windoweventdrop_cpp.md#ACTION)* **action** - Type of the drop action performed with the window during the event.
- *const char ** **item_path**
