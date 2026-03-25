# Unigine::WindowEventDpi Class (CPP)

**Header:** #include <UnigineWindowManager.h>

**Inherits from:** WindowEvent


## WindowEventDpi Class

### Enums

## ACTION

| Name | Description |
|---|---|
| **ACTION_DPI_CHANGED** = 0 | DPI level has been changed. |
| **ACTION_SIZE_SCALED** = 1 | Window size has been scaled. |

### Members

---

## WindowEventDpi ( )

Default constructor.
## WindowEventDpi ( unsigned long long timestamp , unsigned long long win_id )

Window DPI event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - The window for which DPI is set.

## WindowEventDpi ( unsigned long long timestamp , unsigned long long win_id , const Math:: ivec2 & mouse_pos )

Window DPI event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - The window for which DPI is set.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.

## WindowEventDpi ( unsigned long long timestamp , unsigned long long win_id , const Math:: ivec2 & mouse_pos , const Math:: ivec2 & position , const Math:: ivec2 & size )

Window DPI event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - The window for which DPI is set.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **position** - Position of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **size** - Size of the window.

## WindowEventDpi ( unsigned long long timestamp , unsigned long long win_id , const Math:: ivec2 & mouse_pos , const Math:: ivec2 & position , const Math:: ivec2 & size , WindowEventDrop::ACTION action , int dpi )

Window DPI event constructor.
### Arguments

- *unsigned long long* **timestamp** - Timestamp of the event.
- *unsigned long long* **win_id** - The window for which DPI is set.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **mouse_pos** - Position of the mouse.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **position** - Position of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **size** - Size of the window.
- *[WindowEventDrop::ACTION](../../../api/library/gui/class.windoweventdrop_cpp.md#ACTION)* **action** - Type of the DPI action performed with the window during the event.
- *int* **dpi** - The DPI level.

## void setAction ( WindowEventDpi::ACTION action )

Sets the type of the DPI action performed with the window during the event.
### Arguments

- *[WindowEventDpi::ACTION](../../../api/library/gui/class.windoweventdpi_cpp.md#ACTION)* **action** - Type of the DPI action performed with the window during the event.

## WindowEventDpi::ACTION getAction ( ) const

Returns the type of the DPI action performed with the window during the event.
### Return value

The type of the DPI action performed with the window during the event.
## void setDpi ( int dpi )

Sets the DPI level.
### Arguments

- *int* **dpi** - The DPI level.

## int getDpi ( ) const

Returns the current DPI level.
### Return value

The DPI level.
