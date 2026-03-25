# Unigine::WindowEventDpi Class (CS)

**Inherits from:** WindowEvent


## WindowEventDpi Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **DPI_CHANGED** = 0 | DPI level has been changed. |
| **SIZE_SCALED** = 1 | Window size has been scaled. |

### Properties

## WindowEventDpi.ACTION Action

The type of the DPI action performed with the window during the event.
## int Dpi

The DPI level.
### Members

---

## WindowEventDpi ( )

Default constructor.
## WindowEventDpi ( ulong timestamp , ulong win_id )

Window DPI event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - The window for which DPI is set.

## WindowEventDpi ( ulong timestamp , ulong win_id , ivec2 mouse_pos )

Window DPI event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - The window for which DPI is set.
- *ivec2* **mouse_pos** - Position of the mouse.

## WindowEventDpi ( ulong timestamp , ulong win_id , ivec2 mouse_pos , ivec2 position , ivec2 size )

Window DPI event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - The window for which DPI is set.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.

## WindowEventDpi ( ulong timestamp , ulong win_id , ivec2 mouse_pos , ivec2 position , ivec2 size , WindowEventDrop.ACTION action , int dpi )

Window DPI event constructor.
### Arguments

- *ulong* **timestamp** - Timestamp of the event.
- *ulong* **win_id** - The window for which DPI is set.
- *ivec2* **mouse_pos** - Position of the mouse.
- *ivec2* **position** - Position of the window.
- *ivec2* **size** - Size of the window.
- *[WindowEventDrop.ACTION](../../../api/library/gui/class.windoweventdrop_cs.md#ACTION)* **action** - Type of the DPI action performed with the window during the event.
- *int* **dpi** - The DPI level.
