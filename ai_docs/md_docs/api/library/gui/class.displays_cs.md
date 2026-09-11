# Unigine::Displays Class (CS)

> **Notice:** This class is a singleton.


The *Displays* class allows getting information about connected displays such as the number of screen displays and the index of the main one, their position and size in pixels. It provides access to the name and current dpi. This class also allows obtaining the total number of available modes for displays and getting the resolution and refresh rate by the mode index.


<details>
<summary>DisplayClass.cs | Close</summary>

`DisplayClass.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class DisplaysClass : Component
{
	EngineWindowViewport window_0;
	int current_display;

	private void Init()
	{
		// get the main window
		window_0 = WindowManager.MainWindow;
		// set its position and size
		window_0.Position = new ivec2(60, 60);
		window_0.Size = new ivec2(960, 600);
		// render the window
		window_0.Show();

		// get the current display
		current_display = Displays.Current;
		// show the information on the current display in the main window
		ShowDisplayInfo(current_display);

	}

	private void Update()
	{
		// check if the cursor has been moved to another display
		if (current_display != Displays.Current)
		{
			// remove the information on the previous display
			for (int i = 0; i < window_0.NumChildren; i++) window_0.RemoveChild(window_0.GetChild(i));
			// show the information on the display that is currently under cursor
			ShowDisplayInfo(current_display);
		}

	}

	private void ShowDisplayInfo(int i)
	{
		ivec2 resolution;

		if (i == Displays.Main) window_0.AddChild(new WidgetLabel(window_0.SelfGui, String.Format("Main display")));
		// the display name
		window_0.AddChild(new WidgetLabel(window_0.SelfGui, String.Format("The display name: {0} \n", Displays.GetName(i))));
		// the display resolution
		resolution = Displays.GetResolution(i);
		window_0.AddChild(new WidgetLabel(window_0.SelfGui, String.Format("The display resolution: {0} {1}", resolution.x, resolution.y)));
		// the display dpi
		window_0.AddChild(new WidgetLabel(window_0.SelfGui, String.Format("The display DPI:{0} \n", Displays.GetDPI(i))));
		// the number of modes of the display
		window_0.AddChild(new WidgetLabel(window_0.SelfGui, String.Format("The num display modes: {0}", Displays.GetNumModes(i))));
		// the current mode of the display
		window_0.AddChild(new WidgetLabel(window_0.SelfGui, String.Format("The current display mode: {0} ", Displays.GetCurrentMode(i))));

	}
}

```

</details>


## Displays Class

### Enums

## ORIENTATION

| Name | Description |
|---|---|
| **UNKNOWN** = -1 | Another undefined type of orientation. |
| **LANDSCAPE** = 0 | Landscape orientation. |
| **LANDSCAPE_FLIPPED** = 1 | Landscape orientation turned upside down. |
| **PORTRAIT** = 2 | Portrait orientation. |
| **PORTRAIT_FLIPPED** = 3 | Portrait orientation turned upside down. |

### Properties

## 🔒︎ int Main

The index of the main system display.
## 🔒︎ int DefaultSystemDPI

The default system dots/pixels-per-inch value.
## 🔒︎ int Num

The number of available video displays.
## 🔒︎ int Current

The index of the display that is currently under the cursor.
### Members

---

## ivec2 GetPosition ( int display_index )

Returns the display position by its index.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display position.
## ivec2 GetResolution ( int display_index )

Returns the display resolution by its index.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display resolution.
## int GetDPI ( int display_index )

Returns the display DPI by its index.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display DPI.
## int GetNumModes ( int display_index )

Returns the total number of available display modes.
### Arguments

- *int* **display_index** - Display index.

### Return value

Number of available display modes.
## ivec2 GetModeResolution ( int display_index , int mode_index )

Returns the resolution of the selected display mode for the selected display.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).

### Return value

Resolution.
## int GetModeRefreshRate ( int display_index , int mode_index )

Returns the refresh rate of the specified display mode.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).

### Return value

Refresh rate of the specified display mode.
## string GetName ( int display_index )

Returns the system name of the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

System name of the display.
## int GetRefreshRate ( int display_index )

Returns the current refresh rate of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Refresh rate of the specified display.
## int GetCurrentMode ( int display_index )

Returns the current display mode for the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).
## int GetDesktopMode ( int display_index )

Returns information about the desktop's display mode. There's a difference between this function and [getCurrentMode()](#getCurrentMode_int_int) when the application runs fullscreen and has changed the resolution. In such a case, this function will return the previous native display mode, and not the current display mode.
### Arguments

- *int* **display_index** - Display index.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).
## Displays.ORIENTATION GetOrientation ( int display_index )

Returns the display orientation.
### Arguments

- *int* **display_index** - Display index.

### Return value

Orientation, one of the [ORIENTATION](#ORIENTATION) values.
## int GetUniqueID ( int display_index )

Returns the unique ID for the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display unique ID.
## int FindDisplay ( string name )

Returns the display index by its name.
### Arguments

- *string* **name** - Display name.

### Return value

Display index.
## int FindDisplay ( int unique_id )

Returns the display index by its unique ID.
### Arguments

- *int* **unique_id** - Display unique ID.

### Return value

Display index, or -1 if the display is not found.
## int FindMode ( int display_index , ivec2 resolution )

Returns the index of the display mode by the display index and resolution.
### Arguments

- *int* **display_index** - Display index.
- *ivec2* **resolution** - Display resolution.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int), or -1 if the mode is not found.
## int FindMode ( int display_index , ivec2 resolution , int refresh_rate )

Returns the index of the display mode by the display index, resolution, and refresh rate.
### Arguments

- *int* **display_index** - Display index.
- *ivec2* **resolution** - Display resolution.
- *int* **refresh_rate** - Refresh rate.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int), or -1 if the mode is not found.
## int GetByPoint ( ivec2 point )

Returns the index of the display that is located at the specified point. For example, you can submit the mouse coordinates as the argument to obtain the index of the display over which the cursor is hovering.
### Arguments

- *ivec2* **point** - The point position in global coordinates.

### Return value

The index of the display located at the specified point.
