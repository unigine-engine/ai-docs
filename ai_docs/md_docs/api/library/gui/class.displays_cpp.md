# Unigine::Displays Class (CPP)

**Header:** #include <UnigineDisplays.h>

> **Notice:** This class is a singleton.


The *Displays* class allows getting information about connected displays such as the number of screen displays and the index of the main one, their position and size in pixels. It provides access to the name and current dpi. This class also allows obtaining the total number of available modes for displays and getting the resolution and refresh rate by the mode index.


<details>
<summary>AppSystemLogic.h | Close</summary>

`AppSystemLogic.h`


```cpp
#include <UnigineLogic.h>

class AppSystemLogic : public Unigine::SystemLogic
{
public:
	AppSystemLogic();
	~AppSystemLogic() override;

	int init() override;

	int update() override;
	int postUpdate() override;

	int shutdown() override;

	int showDisplayInfo(int current_display);

};


```

</details>


<details>
<summary>AppSystemLogic.cpp | Close</summary>

`AppSystemLogic.cpp`


```cpp
#include "AppSystemLogic.h"
#include <UnigineDisplays.h>

using namespace Unigine;
using namespace Math;

EngineWindowViewportPtr window_0;
int current_display;

int AppSystemLogic::init()
{

	// get the main window
	window_0 = WindowManager::getMainWindow();
	// set its position and size
	window_0->setPosition(Math::ivec2(60, 60));
	window_0->setSize(Math::ivec2(960, 600));
	// render the window
	window_0->show();

	// get the current display
	current_display = Displays::getCurrent();
	// show the information on the current display in the main window
	showDisplayInfo(current_display);

	return 1;
}

int AppSystemLogic::update()
{
	// check if the cursor has been moved to another display
	if (current_display != Displays::getCurrent())
	{
		// remove the information on the previous display
		for (int i = 0; i < window_0->getNumChildren(); i++) window_0->removeChild(window_0->getChild(i));
		// show the information on the display that is currently under cursor
		showDisplayInfo(current_display);
	}

	return 1;
}

int AppSystemLogic::showDisplayInfo(int i)
{
	ivec2 resolution;

	if (i == Displays::getMain()) window_0->addChild(WidgetLabel::create(window_0->getSelfGui(), String::format("Main display")));
	// the display name
	window_0->addChild(WidgetLabel::create(window_0->getSelfGui(), String::format("The display name: %s \n", Displays::getName(i))));
	// the display resolution
	resolution = Displays::getResolution(i);
	window_0->addChild(WidgetLabel::create(window_0->getSelfGui(), String::format("The display resolution: %d %d", resolution.x, resolution.y)));
	// the display dpi
	window_0->addChild(WidgetLabel::create(window_0->getSelfGui(), String::format("The display DPI: %d \n", Displays::getDPI(i))));
	// the number of modes of the display
	window_0->addChild(WidgetLabel::create(window_0->getSelfGui(), String::format("The num display modes: %d \n", Displays::getNumModes(i))));
	// the current mode of the display
	window_0->addChild(WidgetLabel::create(window_0->getSelfGui(), String::format("The current display mode: %d", Displays::getCurrentMode(i))));

	return 1;
}


```

</details>


## Displays Class

### Enums

## ORIENTATION

| Name | Description |
|---|---|
| **ORIENTATION_UNKNOWN** = -1 | Another undefined type of orientation. |
| **ORIENTATION_LANDSCAPE** = 0 | Landscape orientation. |
| **ORIENTATION_LANDSCAPE_FLIPPED** = 1 | Landscape orientation turned upside down. |
| **ORIENTATION_PORTRAIT** = 2 | Portrait orientation. |
| **ORIENTATION_PORTRAIT_FLIPPED** = 3 | Portrait orientation turned upside down. |

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

## Math:: ivec2 getPosition ( int display_index ) const

Returns the display position by its index.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display position.
## Math:: ivec2 getResolution ( int display_index ) const

Returns the display resolution by its index.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display resolution.
## int getDPI ( int display_index ) const

Returns the display DPI by its index.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display DPI.
## int getNumModes ( int display_index ) const

Returns the total number of available display modes.
### Arguments

- *int* **display_index** - Display index.

### Return value

Number of available display modes.
## Math:: ivec2 getModeResolution ( int display_index , int mode_index ) const

Returns the resolution of the selected display mode for the selected display.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).

### Return value

Resolution.
## int getModeRefreshRate ( int display_index , int mode_index ) const

Returns the refresh rate of the specified display mode.
### Arguments

- *int* **display_index** - Display index.
- *int* **mode_index** - Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).

### Return value

Refresh rate of the specified display mode.
## const char * getName ( int display_index ) const

Returns the system name of the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

System name of the display.
## int getRefreshRate ( int display_index ) const

Returns the current refresh rate of the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Refresh rate of the specified display.
## int getCurrentMode ( int display_index ) const

Returns the current display mode for the specified display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).
## int getDesktopMode ( int display_index ) const

Returns information about the desktop's display mode. There's a difference between this function and [getCurrentMode()](#getCurrentMode_int_int) when the application runs fullscreen and has changed the resolution. In such a case, this function will return the previous native display mode, and not the current display mode.
### Arguments

- *int* **display_index** - Display index.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int).
## Displays::ORIENTATION getOrientation ( int display_index ) const

Returns the display orientation.
### Arguments

- *int* **display_index** - Display index.

### Return value

Orientation, one of the [ORIENTATION_*](#ORIENTATION_UNKNOWN) values.
## int getUniqueID ( int display_index ) const

Returns the unique ID for the display.
### Arguments

- *int* **display_index** - Display index.

### Return value

Display unique ID.
## int findDisplay ( const char * name ) const

Returns the display index by its name.
### Arguments

- *const char ** **name** - Display name.

### Return value

Display index.
## int findDisplay ( int unique_id ) const

Returns the display index by its unique ID.
### Arguments

- *int* **unique_id** - Display unique ID.

### Return value

Display index, or -1 if the display is not found.
## int findMode ( int display_index , const Math:: ivec2 & resolution ) const

Returns the index of the display mode by the display index and resolution.
### Arguments

- *int* **display_index** - Display index.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Display resolution.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int), or -1 if the mode is not found.
## int findMode ( int display_index , const Math:: ivec2 & resolution , int refresh_rate ) const

Returns the index of the display mode by the display index, resolution, and refresh rate.
### Arguments

- *int* **display_index** - Display index.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Display resolution.
- *int* **refresh_rate** - Refresh rate.

### Return value

Index of the display mode from 0 to the [total number of available display modes](#getNumModes_int_int), or -1 if the mode is not found.
## int getByPoint ( const Math:: ivec2 & point ) const

Returns the index of the display that is located at the specified point. For example, you can submit the mouse coordinates as the argument to obtain the index of the display over which the cursor is hovering.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **point** - The point position in global coordinates.

### Return value

The index of the display located at the specified point.
