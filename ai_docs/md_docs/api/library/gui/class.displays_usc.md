# Unigine::Displays Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The *Displays* class allows getting information about connected displays such as the number of screen displays and the index of the main one, their position and size in pixels. It provides access to the name and current dpi. This class also allows obtaining the total number of available modes for displays and getting the resolution and refresh rate by the mode index.


## Displays Class

### Members

## int getMain () const

Returns the current index of the main system display.
### Return value

Current index of the main system display
## int getDefaultSystemDPI () const

Returns the current default system dots/pixels-per-inch value.
### Return value

Current default system dots/pixels-per-inch value
## int getNum () const

Returns the current number of available video displays.
### Return value

Current number of available video displays
## int getCurrent () const

Returns the current index of the display that is currently under the cursor.
### Return value

Current index of the display that is currently under the cursor
---

## ivec2 getPosition ( int display_index )

Returns the display position by its index.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display position.
## ivec2 getResolution ( int display_index )

Returns the display resolution by its index.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display resolution.
## int getDPI ( int display_index )

Returns the display DPI by its index.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display DPI.
## int getNumModes ( int display_index )

Returns the total number of available display modes.
### Arguments

- *int* **display_index** - Display index.

### Return value

Number of available display modes.
## ivec2 getModeResolution ( int display_index , int mode_index )

Returns the resolution of the selected display mode for the selected display.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).

### Return value

Resolution.
## int getModeRefreshRate ( int display_index , int mode_index )

Returns the refresh rate of the specified display mode.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).

### Return value

Refresh rate of the specified display mode.
## string getName ( int display_index )

Returns the system name of the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

System name of the display.
## int getRefreshRate ( int display_index )

Returns the current refresh rate of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Refresh rate of the specified display.
## int getCurrentMode ( int display_index )

Returns the current display mode for the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).
## int getDesktopMode ( int display_index )

Returns information about the desktop's display mode. There's a difference between this function and [getCurrentMode()](#getCurrentMode_int_int) when the application runs fullscreen and has changed the resolution. In such a case, this function will return the previous native display mode, and not the current display mode.
### Arguments

- *int* **display_index** - Display index.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).
## int getOrientation ( int display_index )

Returns the display orientation.
### Arguments

- *int* **display_index** - Display index.

### Return value

Orientation, one of the [DISPLAYS_ORIENTATION_*](#ORIENTATION_UNKNOWN) values.
## int getUniqueID ( int display_index )

Returns the unique ID for the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display unique ID.
## int findMode ( int display_index , ivec2 resolution )

Returns the index of the display mode by the display index and resolution.
### Arguments

- *int* **display_index** - Display index.
- *ivec2* **resolution** - Display resolution.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int), or -1 if the mode is not found.
## int findMode ( int display_index , ivec2 resolution , int refresh_rate )

Returns the index of the display mode by the display index, resolution, and refresh rate.
### Arguments

- *int* **display_index** - Display index.
- *ivec2* **resolution** - Display resolution.
- *int* **refresh_rate** - Refresh rate.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int), or -1 if the mode is not found.
## int getByPoint ( ivec2 point )

Returns the index of the display that is located at the specified point. For example, you can submit the mouse coordinates as the argument to obtain the index of the display over which the cursor is hovering.
### Arguments

- *ivec2* **point** - The point position in global coordinates.

### Return value

The index of the display located at the specified point.
