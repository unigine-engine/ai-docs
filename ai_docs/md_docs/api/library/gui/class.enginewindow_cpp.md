# Unigine::EngineWindow Class (CPP)

**Header:** #include <UnigineWindowManager.h>


This base class operates with engine windows: their components, relations with other windows, size, position, visual representation and other features.


When you create [a window viewport](../../../api/library/gui/class.enginewindowviewport_cpp.md) or [a window group](../../../api/library/gui/class.enginewindowgroup_cpp.md), the engine window is created.


The image below demonstrates the window components that can be controlled by the EngineWindow class methods.


![Window components](window_structure.png)


To create the engine window, use one of the *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cpp.md)* or *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cpp.md)* class constructors. For example:


```cpp
// create an engine window of the specified size with the specified name
EngineWindowViewportPtr window = EngineWindowViewport::create("New window", 580, 300);

```


Then, by using methods of the *EngineWindow* class, you can specify the window appearance (for example, set a title, an icon, change opacity, add borders, and so on), and properties (whether the window can be nested, or whether it can become a group), define its style (system or engine), change the window state (whether it is shown/hidden, minimized/maximized, focused, etc.), manage window intersections and events.


### Setting Up Position and Size


In UNIGINE, the window size and position coordinates are measured in both [logical units](../../../principles/dpi/index.md) and pixels:


- The size and position in *units* don't depend on the [DPI scale](#getDpiScale_float) and always remain the same. You can change the window and client area size via **[setSize](../../...md#setSize_ivec2_void)**and **[setClientSize](../../...md#setClientSize_ivec2_void)**, adjust the [minimum](#setMinSize_ivec2_void) and [maximum size](#setMaxSize_ivec2_void) and set the window and client position via the corresponding methods. All of them work with units.
- The size and position in *pixels* are calculated by multiplying the size in units by the current [DPI scale](#getDpiScale_float). You can get it using one of the *RenderSize*-related methods/properties (e.g., **[getRenderSize](../../...md#getRenderSize_ivec2)**, and so on). When the DPI scale is 100%, *1 unit corresponds to 1 pixel*. > **Notice:** DPI scaling is applied only when the `auto_dpi` flag is enabled. You can check the current flag value via the console or by using **[WindowManager::isAutoDpiScaling](../../../api/library/gui/class.windowmanager_cpp.md#isAutoDpiScaling_int)**. >  To determine how the OS handles the DPI scale, specify the *[DPI awareness mode](../../../api/library/gui/class.windowmanager_cpp.md#DPI_AWARENESS)*.


You should consider this information when resizing textures, calculating mouse intersections, etc. The window size and position should be set individually, depending on the situation.


> **Notice:** If necessary, you can convert the size and position coordinates *from units to pixels* and visa versa:
> - Use one of the **[toRenderSize](../../...md#toRenderSize_int_int)**or **[toUnitSize](../../...md#toUnitSize_int_int)**to convert the size.
> - Use **[globalToLocalUnitPosition](../../...md#globalToLocalUnitPosition_ivec2_ivec2)**to transform the coordinates in pixels into units or **[localUnitToGlobalPosition](../../...md#localUnitToGlobalPosition_ivec2_ivec2)**to do the opposite.


In the following example, the positions of the window and client area (in units) change to the mouse cursor when you press the **P** or **C** respectively:


<details>
<summary>AppSystemLogic.cpp</summary>

```cpp
#include <UnigineEngine.h>
#include <UnigineLogic.h>
#include <UnigineWindowManager.h>

using namespace Unigine;
using namespace Math;

EngineWindowViewportPtr system_viewport;

int AppSystemLogic::init()
{

	// create a separate window viewport
	system_viewport = EngineWindowViewport::create("Separate System Viewport", 400, 350);
	// specify an intial position
	system_viewport->setPosition(ivec2(30, 30));

	// render the window viewport
	system_viewport->show();

	return 1;
}

int AppSystemLogic::update()
{

	// change the window position to the mouse cursor when pressing 'P'
	if (Input::isKeyDown(Input::KEY_P))
	{

		if (system_viewport.isDeleted() == false)
			system_viewport->setPosition(mouse_pos);
	}

	// change the client area position to the mouse cursor when pressing 'C'
	if (Input::isKeyDown(Input::KEY_C))
	{
		if (system_viewport.isDeleted() == false)
			system_viewport->setClientPosition(mouse_pos);
	}

	return 1;
}


```

</details>


Check also the  and C++ SIM samples � they print the full information on the window size and DPI.


### Adjusting Visual Representation


The window visual representation includes all available window parameters such as title and title bar, icon, borders, opacity, and window style (the engine or system one).


Here are some window examples:


<details>
<summary>AppSystemLogic.cpp</summary>

```cpp
#include <UnigineEngine.h>
#include <UnigineLogic.h>
#include <UnigineWindowManager.h>

using namespace Unigine;
using namespace Math;

EngineWindowViewportPtr system_viewport;

EngineWindowViewportPtr system_viewport_borderless;
EngineWindowViewportPtr engine_viewport_borderless;
EngineWindowViewportPtr engine_viewport;

int AppSystemLogic::init()
{
	// create a separate system viewport
	system_viewport = EngineWindowViewport::create("Window", 200, 200);
	// specify an intial position
	system_viewport->setPosition(ivec2(30, 30));

	// change the size
	system_viewport->setSize(ivec2(400, 350));

	// render the window viewport
	system_viewport->show();

	// create a separate system viewport with borders and title bar disabled
	system_viewport_borderless = EngineWindowViewport::create(400, 350);
	system_viewport_borderless->setPosition(ivec2(460, 30));
	system_viewport_borderless->setSize(ivec2(400, 350));
	// disable borders
	system_viewport_borderless->setBordersEnabled(false);
	// disable a title bar
	system_viewport_borderless->setTitleBarEnabled(false);
	system_viewport_borderless->show();

	// create a separate engine viewport with no borders
	engine_viewport_borderless = EngineWindowViewport::create("Window", 400, 350);
	engine_viewport_borderless->setPosition(ivec2(460, 30));
	engine_viewport_borderless->setEngineStyle(true);
	engine_viewport_borderless->setSize(ivec2(400, 350));
	// disable borders
	engine_viewport_borderless->setBordersEnabled(false);
	engine_viewport_borderless->show();

	// create a separate engine viewport with borders
	engine_viewport = EngineWindowViewport::create("Window", 400, 350);
	engine_viewport->setPosition(ivec2(460, 30));
	engine_viewport->setEngineStyle(true);
	engine_viewport->setSize(ivec2(400, 350));
	engine_viewport->show();

	return 1;
}


```

</details>


| ![](system_style.jpg) *A system-style window* | ![](borders_bar_disabled.jpg) *A window (either system or engine style),borders and title bar disabled* |
|---|---|
| ![](engine_style_borders_disabled.jpg) *An engine-style window, borders disabled* | ![](engine_style_borders_enabled.jpg) *An engine-style window, borders enabled* |


The *system* and *engine* style windows have the same component layout except the sizing border: in the engine style, it is in the visual part of the window.


The ability to customize the window style makes it possible to create a standard set of window settings for different systems and frameworks.


Check the C++ SIM sample in UNIGINE SDK for more details.


### Setting Up Order


In the following example, the order of the window under the cursor changes when you press the specific button: **T** to make the window appear on top of all other windows, **A** to always render the window above the other windows.


<details>
<summary>AppSystemLogic.cpp</summary>

```cpp
#include "AppSystemLogic.h"
#include <UnigineEngine.h>
#include <UnigineLogic.h>
#include <UnigineWindowManager.h>

using namespace Unigine;
using namespace Math;

EngineWindowPtr current_window;

EngineWindowViewportPtr system_viewport;

EngineWindowViewportPtr system_viewport_borderless;
EngineWindowViewportPtr engine_viewport_borderless;
EngineWindowViewportPtr engine_viewport;

int AppSystemLogic::init()
{
	// create a separate system viewport
	system_viewport = EngineWindowViewport::create("Window", 200, 200);
	// specify an intial position
	system_viewport->setPosition(ivec2(30, 30));

	// change the size
	system_viewport->setSize(ivec2(400, 350));

	// render the window viewport
	system_viewport->show();

	// create a separate system viewport with borders and title bar disabled
	system_viewport_borderless = EngineWindowViewport::create(400, 350);
	system_viewport_borderless->setPosition(ivec2(460, 30));
	system_viewport_borderless->setSize(ivec2(400, 350));
	// disable borders
	system_viewport_borderless->setBordersEnabled(false);
	// disable a title bar
	system_viewport_borderless->setTitleBarEnabled(false);
	system_viewport_borderless->show();

	// create a separate engine viewport with no borders
	engine_viewport_borderless = EngineWindowViewport::create("Window", 400, 350);
	engine_viewport_borderless->setPosition(ivec2(460, 30));
	engine_viewport_borderless->setEngineStyle(true);
	engine_viewport_borderless->setSize(ivec2(400, 350));
	// disable borders
	engine_viewport_borderless->setBordersEnabled(false);
	engine_viewport_borderless->show();

	// create a separate engine viewport with borders
	engine_viewport = EngineWindowViewport::create("Window", 400, 350);
	engine_viewport->setPosition(ivec2(460, 30));
	engine_viewport->setEngineStyle(true);
	engine_viewport->setSize(ivec2(400, 350));
	engine_viewport->show();

	return 1;
}

int AppSystemLogic::update()
{
	// get the current mouse position
	ivec2 mouse_pos = Input::getMousePosition();

	// make the window under the cursor appear on top when pressing 'T'
	if (Input::isKeyDown(Input::KEY_T))
	{
		current_window = WindowManager::getUnderCursorWindow();
		if (current_window.isDeleted() == false)
			current_window->toTop();
	}

	// set the window under the cursor to be always on top when pressing 'A'
	if (Input::isKeyDown(Input::KEY_A))
	{
		current_window = WindowManager::getUnderCursorWindow();
		if (current_window.isDeleted() == false)
			current_window->setAlwaysOnTop(true);
	}

	return 1;
}


```

</details>


Check the sample in UNIGINE SDK for more details.


### Changing Behavior


With the set of behavior-related functions, you can do the following:


- Force the engine to [stop operating](#setHoldEngine_int_void) while the engine window is opened.
- Ignore or allow [using the OS methods for windows closing](#setIgnoreSystemClose_int_void).
- Specify whether the window is [resizable](#setResizable_int_void).
- Specify the sizing border size.
- Control rendering of the engine window - [show, hide, focus, minimize, maximize, restore, or close](#show_void).


Check the and samples in UNIGINE SDK for more details.


### Working with Modal Windows


The following example demonstrates how to create modal windows and add modal children to the main window. Additionally, the main window includes a message that informs the user whether they can close the window or not.


<details>
<summary>AppSystemLogic.cpp</summary>

```cpp
#include "AppSystemLogic.h"
#include <UnigineEngine.h>
#include <UnigineLogic.h>
#include <UnigineWindowManager.h>

using namespace Unigine;
using namespace Math;

WidgetLabelPtr label;
EngineWindowViewportPtr main_window;

int AppSystemLogic::init()
{
	// main window
	main_window = WindowManager::getMainWindow();
	main_window->setSize(ivec2(1600, 900));
	main_window->setPosition(ivec2(30, 30));
	main_window->setCanBeNested(false);
	main_window->setCanCreateGroup(false);

	// add an info label to the main window
	label = WidgetLabel::create("");
	label->setFontOutline(1);
	label->setLifetime(Widget::LIFETIME_WINDOW);
	label->setFontColor(vec4_red);
	main_window->addChild(label, Gui::ALIGN_LEFT);

	// first modal window of the main window
	EngineWindowViewportPtr main_modal_0 = EngineWindowViewport::create("Modal for Main 0", 600, 650);
	main_modal_0->setPosition(ivec2(50, 250));
	main_modal_0->setCanBeNested(false);
	main_modal_0->setCanCreateGroup(false);
	main_modal_0->show();
	main_modal_0->setModal(main_window);

	// second modal window of the main window
	EngineWindowViewportPtr main_modal_1 = EngineWindowViewport::create("Modal for Main 1", 900, 650);
	main_modal_1->setPosition(ivec2(700, 250));
	main_modal_1->setCanBeNested(false);
	main_modal_1->setCanCreateGroup(false);
	main_modal_1->show();
	main_modal_1->setModal(main_window);

	return 1;
}

int AppSystemLogic::update()
{
	String text;

	// check if the modal children of the main window are still opened
	if (main_window->isModalParent())
		text += "You CANNOT close this window. Please close modal children first.\n";
	else
		text += "You CAN close this window.\n";

	// render the info label
	label->setText(text);

	return 1;
}


```

</details>


Check the sample in UNIGINE SDK for more details.


## See Also


- A set of SDK samples (`source/window_manager/`) demonstrating various usage aspects.


## EngineWindow Class

### Enums

## HITTEST

| Name | Description |
|---|---|
| **HITTEST_INVALID** = -1 | The hittest result is invalid. |
| **HITTEST_NORMAL** = 0 | Client area of the window. |
| **HITTEST_DRAGGABLE** = 1 | Area of the window, by clicking onto which the window can be moved. |
| **HITTEST_RESIZE_TOPLEFT** = 2 | Area of the window that can be dragged to resize the window to the top and/or left direction. |
| **HITTEST_RESIZE_TOP** = 3 | Area of the window that can be dragged to resize the window to the top direction. |
| **HITTEST_RESIZE_TOPRIGHT** = 4 | Area of the window that can be dragged to resize the window to the top and/or right direction. |
| **HITTEST_RESIZE_RIGHT** = 5 | Area of the window that can be dragged to resize the window to the right direction. |
| **HITTEST_RESIZE_BOTTOMRIGHT** = 6 | Area of the window that can be dragged to resize the window to the bottom and/or right direction. |
| **HITTEST_RESIZE_BOTTOM** = 7 | Area of the window that can be dragged to resize the window to the bottom direction. |
| **HITTEST_RESIZE_BOTTOMLEFT** = 8 | Area of the window that can be dragged to resize the window to the bottom and/or left direction. |
| **HITTEST_RESIZE_LEFT** = 9 | Area of the window that can be dragged to resize the window to the left direction. |

## FLAGS

| Name | Description |
|---|---|
| **FLAGS_SHOWN** = 1 << 0 | Window is rendered. |
| **FLAGS_FIXED_SIZE** = 1 << 1 | Window size is fixed. |
| **FLAGS_HOLD_ENGINE** = 1 << 2 | Engine can't stop operating while this window is open. |
| **FLAGS_MAIN** = 1 << 3 | Main window. |
| **FLAGS_CONSOLE_USAGE** = 1 << 4 | Usage of the console for the window is enabled. |
| **FLAGS_PROFILER_USAGE** = 1 << 5 | Usage of the profiler for the window is enabled. |
| **FLAGS_VISUALIZER_USAGE** = 1 << 6 | Usage of the visualizer for the window is enabled. |

## AREA

| Name | Description |
|---|---|
| **AREA_NONE** = 0 | None of the areas of the window split into 9 parts is selected. |
| **AREA_TOP_LEFT** = 1 | Top left area of the window split into 9 parts. |
| **AREA_TOP_CENTER** = 2 | Top center area of the window split into 9 parts. |
| **AREA_TOP_RIGHT** = 3 | Top right area of the window split into 9 parts. |
| **AREA_CENTER_LEFT** = 4 | Center left area of the window split into 9 parts. |
| **AREA_CENTER_CENTER** = 5 | Center area of the window split into 9 parts. |
| **AREA_CENTER_RIGHT** = 6 | Center right area of the window split into 9 parts. |
| **AREA_BOTTOM_LEFT** = 7 | Bottom left area of the window split into 9 parts. |
| **AREA_BOTTOM_CENTER** = 8 | Bottom center area of the window split into 9 parts. |
| **AREA_BOTTOM_RIGHT** = 9 | Bottom right area of the window split into 9 parts. |

## TYPE

| Name | Description |
|---|---|
| **ENGINE_WINDOW** = 0 | Engine window. |
| **ENGINE_WINDOW_VIEWPORT** = 1 | Engine viewport window. |
| **ENGINE_WINDOW_GROUP** = 2 | Engine window group. |
| **NUM_ENGINE_WINDOWS** = 3 | Total number of engine windows. |

### Members

## Ptr < Gui > getGui () const

Returns the current parent Gui for a window. If the window is nested, this Gui differs from [SelfGui](#getSelfGui_Gui).
### Return value

Current Gui instance.
## int getDisplayIndex () const

Returns the current number of the display, on which the window is currently displayed. For separate windows, this index is requested from the system proxy; for nested windows, the index is provided based on the location of the client center point.
### Return value

Current number of the display, on which the window is currently displayed.
## bool isNested () const

Returns the current value indicating if this is a nested window or group of windows.
### Return value

**true** if this is a nested window or group of windows; otherwise **false**.
## bool isSeparate () const

Returns the current value indicating if this is a separate window or group of windows.
### Return value

**true** if this is a separate window or group of windows is enabled ; otherwise **false**.
## Ptr < Gui > getSelfGui () const

Returns the current Gui instance for a window. This Gui remains unchanged during the whole lifecycle of the window.
### Return value

Current Gui instance.
## void setPosition ( const Math:: ivec2 & position )

Sets a new position of the [top left corner](#window_structure) of the window in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **position** - The window screen position (coordinates of the top left corner).

## Math:: ivec2 getPosition () const

Returns the current position of the [top left corner](#window_structure) of the window in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Return value

Current window screen position (coordinates of the top left corner).
## void setClientPosition ( const Math:: ivec2 & position )

Sets a new position of the [top left corner](#window_structure) of the client (the window content area without the top bar and borders) in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **position** - The screen position of the client (coordinates of the top left corner).

## Math:: ivec2 getClientPosition () const

Returns the current position of the [top left corner](#window_structure) of the client (the window content area without the top bar and borders) in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Return value

Current screen position of the client (coordinates of the top left corner).
## Math:: ivec2 getClientLocalPosition () const

Returns the current position of the [top left corner](#window_structure) of the client (the window content area without the top bar and borders) relative to the window position in the screen coordinates (pixels).
### Return value

Current screen position of the client (coordinates of the top left corner) relative to the window position in the screen coordinates (pixels).
## void setSize ( const Math:: ivec2 & size )

Sets a new engine [window size](#window_structure) in [logical units](../../../principles/dpi/index.md) (including the sizing border).
> **Notice:** This method is for a separate or parent window, using this method for a nested window is not allowed (when requesting the current value, it will return the value of the global parent group).


### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **size** - The engine [window size](#window_structure) in [logical units](../../../principles/dpi/index.md) (including the sizing border).

## Math:: ivec2 getSize () const

Returns the current engine [window size](#window_structure) in [logical units](../../../principles/dpi/index.md) (including the sizing border).
> **Notice:** This method is for a separate or parent window, using this method for a nested window is not allowed (when requesting the current value, it will return the value of the global parent group).


### Return value

Current engine [window size](#window_structure) in [logical units](../../../principles/dpi/index.md) (including the sizing border).
## void setClientSize ( const Math:: ivec2 & size )

Sets a new size of the window [client (content) area](#window_structure) in [logical units](../../../principles/dpi/index.md).
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **size** - The size of the window client (content) area in logical units

## Math:: ivec2 getClientSize () const

Returns the current size of the window [client (content) area](#window_structure) in [logical units](../../../principles/dpi/index.md).
### Return value

Current size of the window client (content) area in logical units
## void setMinSize ( const Math:: ivec2 & size )

Sets a new minimum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is more than the current maximum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current maximum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return zero values).


### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **size** - The minimum possible size of the window.

## Math:: ivec2 getMinSize () const

Returns the current minimum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is more than the current maximum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current maximum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return zero values).


### Return value

Current minimum possible size of the window.
## void setMaxSize ( const Math:: ivec2 & size )

Sets a new maximum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is less than the current minimum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current minimum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **size** - The maximum possible size of the window.

## Math:: ivec2 getMaxSize () const

Returns the current maximum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is less than the current minimum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current minimum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Return value

Current maximum possible size of the window.
## void setTitle ( const char * title )

Sets a new text of the title for the window. For a separate window, the title is set via system proxy in the title bar only; for a nested window, it is also set in the tab of the parent group.
### Arguments

- *const char ** **title** - The title of the window.

## const char * getTitle () const

Returns the current text of the title for the window. For a separate window, the title is set via system proxy in the title bar only; for a nested window, it is also set in the tab of the parent group.
### Return value

Current title of the window.
## void setOpacity ( float opacity )

Sets a new opacity for the window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will always return 1.0f).


### Arguments

- *float* **opacity** - The opacity for the window.

## float getOpacity () const

Returns the current opacity for the window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will always return 1.0f).


### Return value

Current opacity for the window.
## void setBordersEnabled ( bool enabled )

Sets a new value indicating if the borders are enabled for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


### Arguments

- *bool* **enabled** - Set **true** to enable borders for the window; **false** - to disable it.

## bool isBordersEnabled () const

Returns the current value indicating if the borders are enabled for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


### Return value

**true** if borders for the window is enabled ; otherwise **false**.
## void setBorderSize ( int size )

Sets a new engine window border size.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Arguments

- *int* **size** - The engine window border size.

## int getBorderSize () const

Returns the current engine window border size.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Return value

Current engine window border size.
## void setResizable ( bool resizable )

Sets a new value indicating if the engine window is resizable by the mouse.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


### Arguments

- *bool* **resizable** - Set **true** to enable resizing of the engine window with the mouse; **false** - to disable it.

## bool isResizable () const

Returns the current value indicating if the engine window is resizable by the mouse.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


### Return value

**true** if resizing of the engine window with the mouse is enabled ; otherwise **false**.
## bool isShown () const

Returns the current value indicating if the engine window is rendered.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

**true** if the engine window is rendered; otherwise **false**.
## bool isHidden () const

Returns the current value indicating if the engine window isn't rendered.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

**true** if the engine window isn't rendered; otherwise **false**.
## bool isFocused () const

Returns the current value indicating if the engine window is in focus.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

**true** if the engine window is in focus; otherwise **false**.
## bool isMinimized () const

Returns the current value indicating if the engine window is minimized.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

**true** if the engine window is minimized; otherwise **false**.
## bool isMaximized () const

Returns the current value indicating if the engine window is maximized.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

**true** if the engine window is maximized; otherwise **false**.
## int getOrder () const

Returns the current order of the window. This value allows comparing which window is closer to the viewer (a relatively smaller value).
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

Current order of the window.
## Ptr < EngineWindowGroup > getParentGroup () const

Returns the current group into which the current window is nested, or nullptr if it is a separate window.
### Return value

Current group into which the current window is nested, or nullptr if it is a separate window.
## Ptr < EngineWindowGroup > getGlobalParentGroup () const

Returns the current top group of the hierarchy into which the current window is nested, or nullptr if it is a separate window.
### Return value

Current top group of the hierarchy into which the current window is nested, or nullptr if it is a separate window.
## int getNumDroppedItems () const

Returns the current total number of files and/or folders dropped to the window.
### Return value

Current number of dropped files and/or folders.
## int getNumModalWindows () const

Returns the current total number of modal windows for this window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return 0.


### Return value

Current total number of modal windows.
## Ptr < EngineWindow > getModalParent () const

Returns the current modal parent of the window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return nullptr.


### Return value

Current modal parent of the window.
## bool isModalParent () const

Returns the current value indicating if the window is parent for any modal window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return false.


### Return value

**true** if the window is parent for any modal window; otherwise **false**.
## bool isModal () const

Returns the current value indicating if the window is modal. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return false.


### Return value

**true** if the window is modal; otherwise **false**.
## void setIgnoreSystemClose ( bool close )

Sets a new value indicating if closing the window using the OS methods is ignored (*ALT+F4* or cross in the top-right corner of the window).
### Arguments

- *bool* **close** - Set **true** to enable ignoring OS methods for closing the window; **false** - to disable it.

## bool isIgnoreSystemClose () const

Returns the current value indicating if closing the window using the OS methods is ignored (*ALT+F4* or cross in the top-right corner of the window).
### Return value

**true** if ignoring OS methods for closing the window is enabled ; otherwise **false**.
## void setHoldEngine ( bool engine )

Sets a new value indicating if the engine operation can't be stopped while this window is open.
### Arguments

- *bool* **engine** - Set **true** to enable the engine can't stop operating while this window is open; **false** - to disable it.

## bool isHoldEngine () const

Returns the current value indicating if the engine operation can't be stopped while this window is open.
### Return value

**true** if the engine can't stop operating while this window is open; otherwise **false**.
## unsigned long long getID () const

Returns the current ID of the engine window, which is unchanged during the whole lifecycle of the window.
### Return value

Current ID of the engine window, if the window is external.
## void setAlwaysOnTop ( bool top )

Sets a new value indicating if the window is always rendered above the other windows.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return the value of the global parent group).


### Arguments

- *bool* **top** - Set **true** to enable the window is always on top; **false** - to disable it.

## bool isAlwaysOnTop () const

Returns the current value indicating if the window is always rendered above the other windows.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return the value of the global parent group).


### Return value

**true** if the window is always on top; otherwise **false**.
## bool isHiddenByTab () const

Returns the current value indicating if the window is overlapped by any other tab (either by switching to another tab or resizing this window to have zero client area).
### Return value

**true** if the window is overlapped by any other tab; otherwise **false**.
## void setCanCreateGroup ( bool group )

Sets a new value indicating if the engine window can become a group.
### Arguments

- *bool* **group** - Set **true** to enable usage of the engine window as a group; **false** - to disable it.

## bool isCanCreateGroup () const

Returns the current value indicating if the engine window can become a group.
### Return value

**true** if usage of the engine window as a group is enabled ; otherwise **false**.
## void setCanBeNested ( bool nested )

Sets a new value indicating if the engine window can be used as a nested window.
### Arguments

- *bool* **nested** - Set **true** to enable usage of the engine window as a nested window; **false** - to disable it.

## bool isCanBeNested () const

Returns the current value indicating if the engine window can be used as a nested window.
### Return value

**true** if usage of the engine window as a nested window is enabled ; otherwise **false**.
## bool isSystemFocused () const

Returns the current value indicating if the engine window is currently in focus.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


### Return value

**true** if the engine window is in focus; otherwise **false**.
## void setSizingBorderSize ( int size )

Sets a new [size of the border](#window_examples) in the widget that is manipulated to resize the window.
> **Notice:** - This method should not be applied to a system-style window with enabled borders, as the system settings cannot be changed (for an unmodified system-style window (i.e. with the enabled border size), the system value is applied).
> - This method should not be applied to nested windows (it will return 0).


### Arguments

- *int* **size** - The size of the border in the widget that is manipulated to resize the window, in pixels.

## int getSizingBorderSize () const

Returns the current [size of the border](#window_examples) in the widget that is manipulated to resize the window.
> **Notice:** - This method should not be applied to a system-style window with enabled borders, as the system settings cannot be changed (for an unmodified system-style window (i.e. with the enabled border size), the system value is applied).
> - This method should not be applied to nested windows (it will return 0).


### Return value

Current size of the border in the widget that is manipulated to resize the window, in pixels.
## void setEngineStyle ( bool style )

Sets a new value indicating if the [engine style](#window_examples) or the default system style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


### Arguments

- *bool* **style** - Set **true** to enable the engine style for the engine window; **false** - to disable it.

## bool isEngineStyle () const

Returns the current value indicating if the [engine style](#window_examples) or the default system style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


### Return value

**true** if the engine style for the engine window is enabled ; otherwise **false**.
## void setSystemStyle ( bool style )

Sets a new value indicating if the default [system style](#window_examples) or the engine style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


### Arguments

- *bool* **style** - Set **true** to enable the default system style for the engine window; **false** - to disable it.

## bool isSystemStyle () const

Returns the current value indicating if the default [system style](#window_examples) or the engine style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


### Return value

**true** if the default system style for the engine window is enabled ; otherwise **false**.
## void setTitleBarHeight ( int height )

Sets a new height of the window title bar.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Arguments

- *int* **height** - The engine window title bar height.

## int getTitleBarHeight () const

Returns the current height of the window title bar.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Return value

Current engine window title bar height.
## void setTitleBarEnabled ( bool enabled )

Sets a new value indicating if the title bar is enabled for the engine window.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Arguments

- *bool* **enabled** - Set **true** to enable the title bar for the engine window; **false** - to disable it.

## bool isTitleBarEnabled () const

Returns the current value indicating if the title bar is enabled for the engine window.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


### Return value

**true** if the title bar for the engine window is enabled ; otherwise **false**.
## const char * getTypeName () const

Returns the current name of the engine window type as a string.
### Return value

Current string representation of the engine window type.
## EngineWindow::TYPE getType () const

Returns the current type of the engine window.
### Return value

Current type of the engine window.
## float getDpiScale () const

Returns the current DPI scale applied to the elements inside the window.
### Return value

Current DPI scale applied to the elements inside the window.
## int getDpi () const

Returns the current DPI level for the window.
### Return value

Current DPI level for the window.
## Math:: ivec2 getMaxRenderSize () const

Returns the current maximum window size in pixels.
### Return value

Current maximum window size in pixels.
## Math:: ivec2 getMinRenderSize () const

Returns the current minimum window size in pixels.
### Return value

Current minimum window size in pixels.
## Math:: ivec2 getClientRenderSize () const

Returns the current client area size in pixels.
### Return value

Current client area size in pixels.
## Math:: ivec2 getRenderSize () const

Returns the current engine window frame size in pixels.
### Return value

Current engine window frame size in pixels.
## Event<> getEventUnstack () const

event triggered when the window is unstacked. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Unstack event handler
void unstack_event_handler()
{
	Log::message("\Handling Unstack event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections unstack_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventUnstack().connect(unstack_event_connections, unstack_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventUnstack().connect(unstack_event_connections, []() {
		Log::message("\Handling Unstack event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
unstack_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection unstack_event_connection;

// subscribe to the Unstack event with a handler function keeping the connection
publisher->getEventUnstack().connect(unstack_event_connection, unstack_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
unstack_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
unstack_event_connection.setEnabled(true);

// ...

// remove subscription to the Unstack event via the connection
unstack_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Unstack event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Unstack event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventUnstack().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId unstack_handler_id;

// subscribe to the Unstack event with a lambda handler function and keeping connection ID
unstack_handler_id = publisher->getEventUnstack().connect(e_connections, []() {
		Log::message("\Handling Unstack event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventUnstack().disconnect(unstack_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Unstack events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventUnstack().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventUnstack().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventStack () const

event triggered when the window is stacked. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Stack event handler
void stack_event_handler()
{
	Log::message("\Handling Stack event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections stack_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventStack().connect(stack_event_connections, stack_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventStack().connect(stack_event_connections, []() {
		Log::message("\Handling Stack event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
stack_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection stack_event_connection;

// subscribe to the Stack event with a handler function keeping the connection
publisher->getEventStack().connect(stack_event_connection, stack_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
stack_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
stack_event_connection.setEnabled(true);

// ...

// remove subscription to the Stack event via the connection
stack_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Stack event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Stack event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventStack().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId stack_handler_id;

// subscribe to the Stack event with a lambda handler function and keeping connection ID
stack_handler_id = publisher->getEventStack().connect(e_connections, []() {
		Log::message("\Handling Stack event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventStack().disconnect(stack_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Stack events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventStack().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventStack().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < EngineWindow > &> getEventUnstackMove () const

event triggered when the window is unstacked and moved. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<EngineWindow> & **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the UnstackMove event handler
void unstackmove_event_handler(const Ptr<EngineWindow> & window)
{
	Log::message("\Handling UnstackMove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections unstackmove_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventUnstackMove().connect(unstackmove_event_connections, unstackmove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventUnstackMove().connect(unstackmove_event_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling UnstackMove event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
unstackmove_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection unstackmove_event_connection;

// subscribe to the UnstackMove event with a handler function keeping the connection
publisher->getEventUnstackMove().connect(unstackmove_event_connection, unstackmove_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
unstackmove_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
unstackmove_event_connection.setEnabled(true);

// ...

// remove subscription to the UnstackMove event via the connection
unstackmove_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A UnstackMove event handler implemented as a class member
	void event_handler(const Ptr<EngineWindow> & window)
	{
		Log::message("\Handling UnstackMove event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventUnstackMove().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId unstackmove_handler_id;

// subscribe to the UnstackMove event with a lambda handler function and keeping connection ID
unstackmove_handler_id = publisher->getEventUnstackMove().connect(e_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling UnstackMove event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventUnstackMove().disconnect(unstackmove_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all UnstackMove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventUnstackMove().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventUnstackMove().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const char *> getEventItemDrop () const

event triggered when an item is dropped to the window. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const char * **item**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ItemDrop event handler
void itemdrop_event_handler(const char * item)
{
	Log::message("\Handling ItemDrop event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections itemdrop_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventItemDrop().connect(itemdrop_event_connections, itemdrop_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventItemDrop().connect(itemdrop_event_connections, [](const char * item) {
		Log::message("\Handling ItemDrop event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
itemdrop_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection itemdrop_event_connection;

// subscribe to the ItemDrop event with a handler function keeping the connection
publisher->getEventItemDrop().connect(itemdrop_event_connection, itemdrop_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
itemdrop_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
itemdrop_event_connection.setEnabled(true);

// ...

// remove subscription to the ItemDrop event via the connection
itemdrop_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A ItemDrop event handler implemented as a class member
	void event_handler(const char * item)
	{
		Log::message("\Handling ItemDrop event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventItemDrop().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId itemdrop_handler_id;

// subscribe to the ItemDrop event with a lambda handler function and keeping connection ID
itemdrop_handler_id = publisher->getEventItemDrop().connect(e_connections, [](const char * item) {
		Log::message("\Handling ItemDrop event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventItemDrop().disconnect(itemdrop_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ItemDrop events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventItemDrop().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventItemDrop().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventClose () const

event triggered when the window is closed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Close event handler
void close_event_handler()
{
	Log::message("\Handling Close event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections close_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventClose().connect(close_event_connections, close_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventClose().connect(close_event_connections, []() {
		Log::message("\Handling Close event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
close_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection close_event_connection;

// subscribe to the Close event with a handler function keeping the connection
publisher->getEventClose().connect(close_event_connection, close_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
close_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
close_event_connection.setEnabled(true);

// ...

// remove subscription to the Close event via the connection
close_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Close event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Close event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventClose().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId close_handler_id;

// subscribe to the Close event with a lambda handler function and keeping connection ID
close_handler_id = publisher->getEventClose().connect(e_connections, []() {
		Log::message("\Handling Close event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventClose().disconnect(close_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Close events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventClose().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventClose().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventRestored () const

event triggered when the window is restored. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Restored event handler
void restored_event_handler()
{
	Log::message("\Handling Restored event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections restored_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventRestored().connect(restored_event_connections, restored_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventRestored().connect(restored_event_connections, []() {
		Log::message("\Handling Restored event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
restored_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection restored_event_connection;

// subscribe to the Restored event with a handler function keeping the connection
publisher->getEventRestored().connect(restored_event_connection, restored_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
restored_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
restored_event_connection.setEnabled(true);

// ...

// remove subscription to the Restored event via the connection
restored_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Restored event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Restored event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventRestored().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId restored_handler_id;

// subscribe to the Restored event with a lambda handler function and keeping connection ID
restored_handler_id = publisher->getEventRestored().connect(e_connections, []() {
		Log::message("\Handling Restored event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventRestored().disconnect(restored_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Restored events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventRestored().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventRestored().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventMaximized () const

event triggered when the window is maximized. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Maximized event handler
void maximized_event_handler()
{
	Log::message("\Handling Maximized event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections maximized_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventMaximized().connect(maximized_event_connections, maximized_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventMaximized().connect(maximized_event_connections, []() {
		Log::message("\Handling Maximized event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
maximized_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection maximized_event_connection;

// subscribe to the Maximized event with a handler function keeping the connection
publisher->getEventMaximized().connect(maximized_event_connection, maximized_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
maximized_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
maximized_event_connection.setEnabled(true);

// ...

// remove subscription to the Maximized event via the connection
maximized_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Maximized event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Maximized event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventMaximized().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId maximized_handler_id;

// subscribe to the Maximized event with a lambda handler function and keeping connection ID
maximized_handler_id = publisher->getEventMaximized().connect(e_connections, []() {
		Log::message("\Handling Maximized event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventMaximized().disconnect(maximized_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Maximized events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventMaximized().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventMaximized().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventMinimized () const

event triggered when the window is minimized. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Minimized event handler
void minimized_event_handler()
{
	Log::message("\Handling Minimized event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections minimized_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventMinimized().connect(minimized_event_connections, minimized_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventMinimized().connect(minimized_event_connections, []() {
		Log::message("\Handling Minimized event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
minimized_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection minimized_event_connection;

// subscribe to the Minimized event with a handler function keeping the connection
publisher->getEventMinimized().connect(minimized_event_connection, minimized_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
minimized_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
minimized_event_connection.setEnabled(true);

// ...

// remove subscription to the Minimized event via the connection
minimized_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Minimized event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Minimized event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventMinimized().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId minimized_handler_id;

// subscribe to the Minimized event with a lambda handler function and keeping connection ID
minimized_handler_id = publisher->getEventMinimized().connect(e_connections, []() {
		Log::message("\Handling Minimized event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventMinimized().disconnect(minimized_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Minimized events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventMinimized().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventMinimized().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventHidden () const

event triggered when the window is hidden. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Hidden event handler
void hidden_event_handler()
{
	Log::message("\Handling Hidden event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections hidden_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventHidden().connect(hidden_event_connections, hidden_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventHidden().connect(hidden_event_connections, []() {
		Log::message("\Handling Hidden event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
hidden_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection hidden_event_connection;

// subscribe to the Hidden event with a handler function keeping the connection
publisher->getEventHidden().connect(hidden_event_connection, hidden_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
hidden_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
hidden_event_connection.setEnabled(true);

// ...

// remove subscription to the Hidden event via the connection
hidden_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Hidden event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Hidden event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventHidden().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId hidden_handler_id;

// subscribe to the Hidden event with a lambda handler function and keeping connection ID
hidden_handler_id = publisher->getEventHidden().connect(e_connections, []() {
		Log::message("\Handling Hidden event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventHidden().disconnect(hidden_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Hidden events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventHidden().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventHidden().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventShown () const

event triggered when the window is shown. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Shown event handler
void shown_event_handler()
{
	Log::message("\Handling Shown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections shown_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventShown().connect(shown_event_connections, shown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventShown().connect(shown_event_connections, []() {
		Log::message("\Handling Shown event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
shown_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection shown_event_connection;

// subscribe to the Shown event with a handler function keeping the connection
publisher->getEventShown().connect(shown_event_connection, shown_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
shown_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
shown_event_connection.setEnabled(true);

// ...

// remove subscription to the Shown event via the connection
shown_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Shown event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Shown event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventShown().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId shown_handler_id;

// subscribe to the Shown event with a lambda handler function and keeping connection ID
shown_handler_id = publisher->getEventShown().connect(e_connections, []() {
		Log::message("\Handling Shown event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventShown().disconnect(shown_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Shown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventShown().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventShown().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventMouseLeave () const

event triggered when the mouse leaves the window area. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the MouseLeave event handler
void mouseleave_event_handler()
{
	Log::message("\Handling MouseLeave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mouseleave_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventMouseLeave().connect(mouseleave_event_connections, mouseleave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventMouseLeave().connect(mouseleave_event_connections, []() {
		Log::message("\Handling MouseLeave event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
mouseleave_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection mouseleave_event_connection;

// subscribe to the MouseLeave event with a handler function keeping the connection
publisher->getEventMouseLeave().connect(mouseleave_event_connection, mouseleave_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
mouseleave_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
mouseleave_event_connection.setEnabled(true);

// ...

// remove subscription to the MouseLeave event via the connection
mouseleave_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A MouseLeave event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling MouseLeave event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventMouseLeave().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId mouseleave_handler_id;

// subscribe to the MouseLeave event with a lambda handler function and keeping connection ID
mouseleave_handler_id = publisher->getEventMouseLeave().connect(e_connections, []() {
		Log::message("\Handling MouseLeave event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventMouseLeave().disconnect(mouseleave_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all MouseLeave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventMouseLeave().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventMouseLeave().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventMouseEnter () const

event triggered when the mouse enters the window area. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the MouseEnter event handler
void mouseenter_event_handler()
{
	Log::message("\Handling MouseEnter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mouseenter_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventMouseEnter().connect(mouseenter_event_connections, mouseenter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventMouseEnter().connect(mouseenter_event_connections, []() {
		Log::message("\Handling MouseEnter event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
mouseenter_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection mouseenter_event_connection;

// subscribe to the MouseEnter event with a handler function keeping the connection
publisher->getEventMouseEnter().connect(mouseenter_event_connection, mouseenter_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
mouseenter_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
mouseenter_event_connection.setEnabled(true);

// ...

// remove subscription to the MouseEnter event via the connection
mouseenter_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A MouseEnter event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling MouseEnter event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventMouseEnter().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId mouseenter_handler_id;

// subscribe to the MouseEnter event with a lambda handler function and keeping connection ID
mouseenter_handler_id = publisher->getEventMouseEnter().connect(e_connections, []() {
		Log::message("\Handling MouseEnter event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventMouseEnter().disconnect(mouseenter_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all MouseEnter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventMouseEnter().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventMouseEnter().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventUnfocused () const

event triggered when the window loses the focus. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Unfocused event handler
void unfocused_event_handler()
{
	Log::message("\Handling Unfocused event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections unfocused_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventUnfocused().connect(unfocused_event_connections, unfocused_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventUnfocused().connect(unfocused_event_connections, []() {
		Log::message("\Handling Unfocused event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
unfocused_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection unfocused_event_connection;

// subscribe to the Unfocused event with a handler function keeping the connection
publisher->getEventUnfocused().connect(unfocused_event_connection, unfocused_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
unfocused_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
unfocused_event_connection.setEnabled(true);

// ...

// remove subscription to the Unfocused event via the connection
unfocused_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Unfocused event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Unfocused event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventUnfocused().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId unfocused_handler_id;

// subscribe to the Unfocused event with a lambda handler function and keeping connection ID
unfocused_handler_id = publisher->getEventUnfocused().connect(e_connections, []() {
		Log::message("\Handling Unfocused event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventUnfocused().disconnect(unfocused_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Unfocused events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventUnfocused().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventUnfocused().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventFocused () const

event triggered when the window gains the focus. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Focused event handler
void focused_event_handler()
{
	Log::message("\Handling Focused event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focused_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFocused().connect(focused_event_connections, focused_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFocused().connect(focused_event_connections, []() {
		Log::message("\Handling Focused event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
focused_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection focused_event_connection;

// subscribe to the Focused event with a handler function keeping the connection
publisher->getEventFocused().connect(focused_event_connection, focused_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
focused_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
focused_event_connection.setEnabled(true);

// ...

// remove subscription to the Focused event via the connection
focused_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Focused event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Focused event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFocused().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId focused_handler_id;

// subscribe to the Focused event with a lambda handler function and keeping connection ID
focused_handler_id = publisher->getEventFocused().connect(e_connections, []() {
		Log::message("\Handling Focused event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFocused().disconnect(focused_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Focused events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFocused().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFocused().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Math:: ivec2 &> getEventResized () const

event triggered when the window is resized. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Math::ivec2 & **new_size**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Resized event handler
void resized_event_handler(const Math::ivec2 & new_size)
{
	Log::message("\Handling Resized event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections resized_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventResized().connect(resized_event_connections, resized_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventResized().connect(resized_event_connections, [](const Math::ivec2 & new_size) {
		Log::message("\Handling Resized event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
resized_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection resized_event_connection;

// subscribe to the Resized event with a handler function keeping the connection
publisher->getEventResized().connect(resized_event_connection, resized_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
resized_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
resized_event_connection.setEnabled(true);

// ...

// remove subscription to the Resized event via the connection
resized_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Resized event handler implemented as a class member
	void event_handler(const Math::ivec2 & new_size)
	{
		Log::message("\Handling Resized event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventResized().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId resized_handler_id;

// subscribe to the Resized event with a lambda handler function and keeping connection ID
resized_handler_id = publisher->getEventResized().connect(e_connections, [](const Math::ivec2 & new_size) {
		Log::message("\Handling Resized event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventResized().disconnect(resized_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Resized events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventResized().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventResized().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Math:: ivec2 &> getEventMoved () const

event triggered when the window is moved. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Math::ivec2 & **new_coords**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Moved event handler
void moved_event_handler(const Math::ivec2 & new_coords)
{
	Log::message("\Handling Moved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections moved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventMoved().connect(moved_event_connections, moved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventMoved().connect(moved_event_connections, [](const Math::ivec2 & new_coords) {
		Log::message("\Handling Moved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
moved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection moved_event_connection;

// subscribe to the Moved event with a handler function keeping the connection
publisher->getEventMoved().connect(moved_event_connection, moved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
moved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
moved_event_connection.setEnabled(true);

// ...

// remove subscription to the Moved event via the connection
moved_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Moved event handler implemented as a class member
	void event_handler(const Math::ivec2 & new_coords)
	{
		Log::message("\Handling Moved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventMoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId moved_handler_id;

// subscribe to the Moved event with a lambda handler function and keeping connection ID
moved_handler_id = publisher->getEventMoved().connect(e_connections, [](const Math::ivec2 & new_coords) {
		Log::message("\Handling Moved event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventMoved().disconnect(moved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Moved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventMoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventMoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventFuncSwap () const

event triggered before calling the window swap. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FuncSwap event handler
void funcswap_event_handler()
{
	Log::message("\Handling FuncSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcswap_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFuncSwap().connect(funcswap_event_connections, funcswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFuncSwap().connect(funcswap_event_connections, []() {
		Log::message("\Handling FuncSwap event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
funcswap_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection funcswap_event_connection;

// subscribe to the FuncSwap event with a handler function keeping the connection
publisher->getEventFuncSwap().connect(funcswap_event_connection, funcswap_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
funcswap_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
funcswap_event_connection.setEnabled(true);

// ...

// remove subscription to the FuncSwap event via the connection
funcswap_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A FuncSwap event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling FuncSwap event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFuncSwap().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId funcswap_handler_id;

// subscribe to the FuncSwap event with a lambda handler function and keeping connection ID
funcswap_handler_id = publisher->getEventFuncSwap().connect(e_connections, []() {
		Log::message("\Handling FuncSwap event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFuncSwap().disconnect(funcswap_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FuncSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFuncSwap().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFuncSwap().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventFuncEndRender () const

event triggered after the window rendering has ended. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FuncEndRender event handler
void funcendrender_event_handler()
{
	Log::message("\Handling FuncEndRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcendrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFuncEndRender().connect(funcendrender_event_connections, funcendrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFuncEndRender().connect(funcendrender_event_connections, []() {
		Log::message("\Handling FuncEndRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
funcendrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection funcendrender_event_connection;

// subscribe to the FuncEndRender event with a handler function keeping the connection
publisher->getEventFuncEndRender().connect(funcendrender_event_connection, funcendrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
funcendrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
funcendrender_event_connection.setEnabled(true);

// ...

// remove subscription to the FuncEndRender event via the connection
funcendrender_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A FuncEndRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling FuncEndRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFuncEndRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId funcendrender_handler_id;

// subscribe to the FuncEndRender event with a lambda handler function and keeping connection ID
funcendrender_handler_id = publisher->getEventFuncEndRender().connect(e_connections, []() {
		Log::message("\Handling FuncEndRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFuncEndRender().disconnect(funcendrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FuncEndRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFuncEndRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFuncEndRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Gui > &> getEventFuncEndRenderGui () const

event triggered after the GUI rendering has ended. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Gui> & **gui**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FuncEndRenderGui event handler
void funcendrendergui_event_handler(const Ptr<Gui> & gui)
{
	Log::message("\Handling FuncEndRenderGui event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcendrendergui_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFuncEndRenderGui().connect(funcendrendergui_event_connections, funcendrendergui_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFuncEndRenderGui().connect(funcendrendergui_event_connections, [](const Ptr<Gui> & gui) {
		Log::message("\Handling FuncEndRenderGui event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
funcendrendergui_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection funcendrendergui_event_connection;

// subscribe to the FuncEndRenderGui event with a handler function keeping the connection
publisher->getEventFuncEndRenderGui().connect(funcendrendergui_event_connection, funcendrendergui_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
funcendrendergui_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
funcendrendergui_event_connection.setEnabled(true);

// ...

// remove subscription to the FuncEndRenderGui event via the connection
funcendrendergui_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A FuncEndRenderGui event handler implemented as a class member
	void event_handler(const Ptr<Gui> & gui)
	{
		Log::message("\Handling FuncEndRenderGui event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFuncEndRenderGui().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId funcendrendergui_handler_id;

// subscribe to the FuncEndRenderGui event with a lambda handler function and keeping connection ID
funcendrendergui_handler_id = publisher->getEventFuncEndRenderGui().connect(e_connections, [](const Ptr<Gui> & gui) {
		Log::message("\Handling FuncEndRenderGui event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFuncEndRenderGui().disconnect(funcendrendergui_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FuncEndRenderGui events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFuncEndRenderGui().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFuncEndRenderGui().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Gui > &> getEventFuncBeginRenderGui () const

event triggered when the GUI rendering has begun. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Gui> & **gui**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FuncBeginRenderGui event handler
void funcbeginrendergui_event_handler(const Ptr<Gui> & gui)
{
	Log::message("\Handling FuncBeginRenderGui event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcbeginrendergui_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFuncBeginRenderGui().connect(funcbeginrendergui_event_connections, funcbeginrendergui_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFuncBeginRenderGui().connect(funcbeginrendergui_event_connections, [](const Ptr<Gui> & gui) {
		Log::message("\Handling FuncBeginRenderGui event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
funcbeginrendergui_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection funcbeginrendergui_event_connection;

// subscribe to the FuncBeginRenderGui event with a handler function keeping the connection
publisher->getEventFuncBeginRenderGui().connect(funcbeginrendergui_event_connection, funcbeginrendergui_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
funcbeginrendergui_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
funcbeginrendergui_event_connection.setEnabled(true);

// ...

// remove subscription to the FuncBeginRenderGui event via the connection
funcbeginrendergui_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A FuncBeginRenderGui event handler implemented as a class member
	void event_handler(const Ptr<Gui> & gui)
	{
		Log::message("\Handling FuncBeginRenderGui event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFuncBeginRenderGui().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId funcbeginrendergui_handler_id;

// subscribe to the FuncBeginRenderGui event with a lambda handler function and keeping connection ID
funcbeginrendergui_handler_id = publisher->getEventFuncBeginRenderGui().connect(e_connections, [](const Ptr<Gui> & gui) {
		Log::message("\Handling FuncBeginRenderGui event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFuncBeginRenderGui().disconnect(funcbeginrendergui_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FuncBeginRenderGui events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFuncBeginRenderGui().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFuncBeginRenderGui().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventFuncRender () const

event triggered after the window rendering function. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FuncRender event handler
void funcrender_event_handler()
{
	Log::message("\Handling FuncRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFuncRender().connect(funcrender_event_connections, funcrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFuncRender().connect(funcrender_event_connections, []() {
		Log::message("\Handling FuncRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
funcrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection funcrender_event_connection;

// subscribe to the FuncRender event with a handler function keeping the connection
publisher->getEventFuncRender().connect(funcrender_event_connection, funcrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
funcrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
funcrender_event_connection.setEnabled(true);

// ...

// remove subscription to the FuncRender event via the connection
funcrender_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A FuncRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling FuncRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFuncRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId funcrender_handler_id;

// subscribe to the FuncRender event with a lambda handler function and keeping connection ID
funcrender_handler_id = publisher->getEventFuncRender().connect(e_connections, []() {
		Log::message("\Handling FuncRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFuncRender().disconnect(funcrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FuncRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFuncRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFuncRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventFuncBeginRender () const

event triggered when the window rendering has begun. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FuncBeginRender event handler
void funcbeginrender_event_handler()
{
	Log::message("\Handling FuncBeginRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcbeginrender_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFuncBeginRender().connect(funcbeginrender_event_connections, funcbeginrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFuncBeginRender().connect(funcbeginrender_event_connections, []() {
		Log::message("\Handling FuncBeginRender event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
funcbeginrender_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection funcbeginrender_event_connection;

// subscribe to the FuncBeginRender event with a handler function keeping the connection
publisher->getEventFuncBeginRender().connect(funcbeginrender_event_connection, funcbeginrender_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
funcbeginrender_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
funcbeginrender_event_connection.setEnabled(true);

// ...

// remove subscription to the FuncBeginRender event via the connection
funcbeginrender_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A FuncBeginRender event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling FuncBeginRender event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFuncBeginRender().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId funcbeginrender_handler_id;

// subscribe to the FuncBeginRender event with a lambda handler function and keeping connection ID
funcbeginrender_handler_id = publisher->getEventFuncBeginRender().connect(e_connections, []() {
		Log::message("\Handling FuncBeginRender event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFuncBeginRender().disconnect(funcbeginrender_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FuncBeginRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFuncBeginRender().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFuncBeginRender().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventFuncUpdate () const

event triggered after the window update. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FuncUpdate event handler
void funcupdate_event_handler()
{
	Log::message("\Handling FuncUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFuncUpdate().connect(funcupdate_event_connections, funcupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFuncUpdate().connect(funcupdate_event_connections, []() {
		Log::message("\Handling FuncUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
funcupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection funcupdate_event_connection;

// subscribe to the FuncUpdate event with a handler function keeping the connection
publisher->getEventFuncUpdate().connect(funcupdate_event_connection, funcupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
funcupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
funcupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the FuncUpdate event via the connection
funcupdate_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A FuncUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling FuncUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFuncUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId funcupdate_handler_id;

// subscribe to the FuncUpdate event with a lambda handler function and keeping connection ID
funcupdate_handler_id = publisher->getEventFuncUpdate().connect(e_connections, []() {
		Log::message("\Handling FuncUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFuncUpdate().disconnect(funcupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FuncUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFuncUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFuncUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < WindowEvent > &> getEventWindowEvent () const

event triggered on the window event. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<WindowEvent> & **event**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the WindowEvent event handler
void windowevent_event_handler(const Ptr<WindowEvent> & event)
{
	Log::message("\Handling WindowEvent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowevent_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventWindowEvent().connect(windowevent_event_connections, windowevent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventWindowEvent().connect(windowevent_event_connections, [](const Ptr<WindowEvent> & event) {
		Log::message("\Handling WindowEvent event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
windowevent_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection windowevent_event_connection;

// subscribe to the WindowEvent event with a handler function keeping the connection
publisher->getEventWindowEvent().connect(windowevent_event_connection, windowevent_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
windowevent_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
windowevent_event_connection.setEnabled(true);

// ...

// remove subscription to the WindowEvent event via the connection
windowevent_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A WindowEvent event handler implemented as a class member
	void event_handler(const Ptr<WindowEvent> & event)
	{
		Log::message("\Handling WindowEvent event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventWindowEvent().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId windowevent_handler_id;

// subscribe to the WindowEvent event with a lambda handler function and keeping connection ID
windowevent_handler_id = publisher->getEventWindowEvent().connect(e_connections, [](const Ptr<WindowEvent> & event) {
		Log::message("\Handling WindowEvent event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventWindowEvent().disconnect(windowevent_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all WindowEvent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventWindowEvent().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventWindowEvent().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## void moveToCenter ( )

Positions the window so that the client center coincides with the center of the current display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void setMinAndMaxSize ( const Math:: ivec2 & min_size , const Math:: ivec2 & max_size )

Sets the minimum and maximum possible window size when resizing the window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **min_size** - The minimum possible size of the window.
- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **max_size** - The maximum possible size of the window.

## int setIcon ( const Ptr < Image > & image )

Sets the icon for the window.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - The icon for the window.

### Return value

1 if the specified icon is successfully set for the window, otherwise 0.
## int getIcon ( Ptr < Image > & image ) const

Gets the icon for the engine window and puts it to the specified target Image.
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Target image for the window icon.

### Return value

1 if the icon for the window is returned successfully, otherwise 0.
## void show ( )

Enables rendering of the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void hide ( )

Disables rendering of the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void setFocus ( )

Sets the focus to the window.
## void setSystemFocus ( )

Sets the focus to the engine window.
> **Notice:** This method is applied to a separate or parent window, for nested windows use [setFocus()](#setFocus_void).


## void minimize ( )

Minimizes the engine window to an iconic representation.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void maximize ( )

Makes the engine window as large as possible.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void restore ( )

Restores the size and position of the minimized or maximized engine window via the system proxy.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## EngineWindow::HITTEST getHitTestResult ( const Math:: ivec2 & global_pos )

Returns a value indicating in which area of the engine window the mouse is located.
> **Notice:** This method is used for interaction with system windows only, i.e. it cannot be used for nested windows.


### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **global_pos** - Global coordinates of the hit-test point.

### Return value

Value indicating the window area, one of the [HITTEST_*](#HITTEST) values.
## const char * getHitTestResultName ( EngineWindow::HITTEST hit_test ) const

Returns the string representation of the hit test result value.
### Arguments

- *[EngineWindow::HITTEST](../../../api/library/gui/class.enginewindow_cpp.md#HITTEST)* **hit_test** - Value indicating the window area, one of the [HITTEST_*](#HITTEST) values.

### Return value

The string representation of the hit test result value (e.g., HITTEST_RESIZE_RIGHT is RESIZE RIGHT).
## void toTop ( )

Makes the window appear on top of all other windows.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## bool isGlobalChildOf ( const Ptr < EngineWindowGroup > & group )

Returns the value specifying if the current window is a part of a hierarchy of the specified window.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cpp.md)> &* **group** - Window to be checked.

### Return value

true if the current window is globally a child of the specified one, otherwise false.
## void updateGuiHierarchy ( )

Updates the hierarchy for all widgets � the widgets are arranged, expanded to the required sizes and then their positions are updated. Updating the hierarchy may be required, for example, for getting the screen position immediately after the widget has been added to the hierarchy. For a separate window, the hierarchy in [self gui](#getSelfGui_Gui) is updated; for a nested window, the hierarchy in [self gui](#getSelfGui_Gui) of the global parent group is updated.
## const char * getDroppedItem ( int index ) const

Returns the absolute path to the file or folder dropped to the window.
### Arguments

- *int* **index** - Index of the dropped file or folder.

### Return value

Absolute path to the dropped file or folder.
## void screenshot ( const char * path )

Creates a screenshot after the rendering stage is completed.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *const char ** **path** - Path to save the screenshot.

## void setModal ( const Ptr < EngineWindow > & parent_window )

Sets the current window modal to the specified parent window. Both the parent and the child windows must be separate. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, a nested window can't be a parent for a modal window.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **parent_window** - Parent window.

## void addModalWindow ( const Ptr < EngineWindow > & window )

Adds the argument window as modal to the current window. Both the parent and the child windows must be separate. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, a nested window can't be a parent for a modal window.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - Window to be added as modal.

## void removeModalWindow ( const Ptr < EngineWindow > & window )

Removes the argument modal window from this window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, a nested window can't be a parent for a modal window.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - Engine window.

## Ptr < EngineWindow > getModalWindow ( int index ) const

Returns the modal window for this window by its index. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return nullptr.


### Arguments

- *int* **index** - Index of the modal window.

### Return value

Modal window.
## void unstack ( )

Removes the current window from a parent group.
## void close ( )

Deletes the window if this window is not a [modal parent](#getModalParent_EngineWindow) or a member of a [fixed group](../../../api/library/gui/class.enginewindowgroup_cpp.md#isFixed_int). If a window is a member of a fixed group, it cannot be closed (i.e. deleted).
## bool getIntersection ( const Math:: ivec2 & global_mouse_pos ) const

Returns the value indicating if the mouse is hovering over the window.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

true if the mouse hovers over the current window, otherwise false.
## bool getClientIntersection ( const Math:: ivec2 & global_mouse_pos ) const

Returns the value indicating if the mouse is hovering over the client area of the window.
```cpp
//checks if the mouse is hovering over the main window
WindowManager::getMainWindow()->getClientIntersection(Input::getMousePosition());


```


### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

true if the mouse hovers over the client area of the window, otherwise false.
## EngineWindow::AREA getClient9Area ( const Math:: ivec2 & global_mouse_pos ) const

Returns the area over which the mouse hovers, one of the nine areas into which the window is segmented.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

One of the nine segments the screen area is split into.
## const char * get9AreaName ( EngineWindow::AREA area ) const

Returns the name of the screen segment as a string.
### Arguments

- *[EngineWindow::AREA](../../../api/library/gui/class.enginewindow_cpp.md#AREA)* **area** - One of the nine segments the screen area is split into.

### Return value

The string representation of the segment value (e.g., AREA_TOP_LEFT is TOP LEFT).
## Math:: ivec2 globalToLocalUnitPosition ( const Math:: ivec2 & global_pos ) const

Transforms the global screen coordinates in pixels into [logical units](../../../principles/dpi/index.md) relative to the window client area.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **global_pos** - The position in global coordinates.

### Return value

The coordinates in [logical units](../../../principles/dpi/index.md) relative to the window client area.
## Math:: ivec2 localUnitToGlobalPosition ( const Math:: ivec2 & unit_pos ) const

Transforms the position in [logical units](../../../principles/dpi/index.md) relative to the window client area into the global screen coordinates in pixels.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **unit_pos** - The coordinates in [logical units](../../../principles/dpi/index.md) relative to the window client area.

### Return value

The position in global coordinates.
## int toRenderSize ( int unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *int* **unit_size** - Size in [logical units](../../../principles/dpi/index.md).

### Return value

Size in pixels.
## int toUnitSize ( int render_size )

Transforms the pixel value to the unit value.
### Arguments

- *int* **render_size** - Size in pixels.

### Return value

Size in [logical units](../../../principles/dpi/index.md).
## Math:: ivec2 toRenderSize ( const Math:: ivec2 & unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **unit_size** - Size in [logical units](../../../principles/dpi/index.md).

### Return value

Size in pixels.
## Math:: ivec2 toUnitSize ( const Math:: ivec2 & render_size )

Transforms the pixel value to the unit value.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **render_size** - Size in pixels.

### Return value

Size in [logical units](../../../principles/dpi/index.md).
