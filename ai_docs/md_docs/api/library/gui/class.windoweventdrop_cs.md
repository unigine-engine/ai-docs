# Unigine::WindowEventDrop Class (CS)

**Inherits from:** WindowEvent


This class is used to handle an event of dragging and dropping a text or file into a window.


## WindowEventDrop Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ITEMS_DROP_BEGIN** = 0 | A new set of drops is beginning. |
| **ITEM_DROP** = 1 | Text/plain drag-and-drop event. |
| **ITEMS_DROP_END** = 2 | The current set of drops is now complete. |

### Properties

## WindowEventDrop.ACTION Action

The type of the drop action performed with the window during the event.
## string Path

The absolute path to the dropped file.
### Members

---

## WindowEventDrop ( )

Default constructor.
## WindowEventDrop ( ulong timestamp , ulong win_id )

Window drop event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - The window that was dropped on, if any.

## WindowEventDrop ( ulong timestamp , ulong win_id , ivec2 mouse_pos )

Window drop event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - The window that was dropped on, if any.
- *ivec2* **mouse_pos** - Position of the mouse.

## WindowEventDrop ( ulong timestamp , ulong win_id , ivec2 mouse_pos , ivec2 position , ivec2 size )

Window drop event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - The window that was dropped on, if any.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.

## WindowEventDrop ( ulong timestamp , ulong win_id , ivec2 mouse_pos , ivec2 position , ivec2 size , WindowEventDrop.ACTION action , string item_path )

Window drop event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - The window that was dropped on, if any.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.
- *[WindowEventDrop.ACTION](../../../api/library/gui/class.windoweventdrop_cs.md#ACTION)* **action** - Type of the drop action performed with the window during the event.
- *string* **item_path**
