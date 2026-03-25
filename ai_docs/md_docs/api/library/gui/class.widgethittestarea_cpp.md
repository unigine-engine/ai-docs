# Unigine::WidgetHitTestArea Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class is used to define the widget area in engine-style windows and borderless system windows intersected by a user-controlled cursor. If the hit test area type is "resize", the system automatically changes the cursor shape, if the hit test area is draggable, the window can be dragged by clicking and dragging this area.


In the following example, the system borders of the main window are disabled and 2 custom drag areas are added. The first area is located at the top of the window and the second area is in its center. For demonstration purposes, the background is enabled for both areas.


<details>
<summary>AppSystemLogic.cpp | Close</summary>

`AppSystemLogic.cpp`


```cpp
#include "AppSystemLogic.h"
#include <UnigineWindowManager.h>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

int AppSystemLogic::init()
{

	// borderless main window
	EngineWindowViewportPtr main_window = WindowManager::getMainWindow();
	if (main_window)
	{
		// disable system borders
		main_window->setBordersEnabled(false);

		GuiPtr gui = main_window->getSelfGui();

		// add a drag area similar to title bar
		WidgetVBoxPtr top_drag_container = WidgetVBox::create(gui);
		main_window->addChild(top_drag_container);

		WidgetHitTestAreaPtr top_drag_area = WidgetHitTestArea::create(gui, EngineWindow::HITTEST_DRAGGABLE);
		top_drag_area->setHeight(25);
		top_drag_container->addChild(top_drag_area, Gui::ALIGN_EXPAND);

		top_drag_area->setBackground(1);
		top_drag_area->setBackgroundColor(Math::vec4_red);

		// add an extra drag area
		WidgetHitTestAreaPtr drag_area = WidgetHitTestArea::create(gui, EngineWindow::HITTEST_DRAGGABLE);
		drag_area->setWidth(512);
		drag_area->setHeight(256);
		main_window->addChild(drag_area, Gui::ALIGN_CENTER);

		drag_area->setBackground(1);
		drag_area->setBackgroundColor(Math::vec4_blue);
	}

	return 1;
}

int AppSystemLogic::shutdown()
{
	// removing all event subscriptions
	econnections.disconnectAll();

	return 1;
}


```

</details>


## WidgetHitTestArea Class

### Members

## int getHitTestResult () const

Returns the current hit test area type, one of the **[EngineWindow::HITTEST_*](../../../api/library/gui/class.enginewindow_cpp.md#HITTEST_INVALID)** values.
### Return value

Current hit test area type.
## void setBackgroundColor ( const Math:: vec4 & color )

Sets a new color for the background of the drag area to be used for debug purposes.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The background color.

## Math:: vec4 getBackgroundColor () const

Returns the current color for the background of the drag area to be used for debug purposes.
### Return value

Current background color.
## void setBackground ( int background )

Sets a new flag indicating if background rendering is enabled for the drag area for debug purposes.
### Arguments

- *int* **background** - The flag indicating background rendering status: 1 for enabled, 0 for disabled.

## int getBackground () const

Returns the current flag indicating if background rendering is enabled for the drag area for debug purposes.
### Return value

Current flag indicating background rendering status: 1 for enabled, 0 for disabled.
---

## WidgetHitTestArea ( const Ptr < Gui > & gui , int hit_test )

Constructor. Creates a hit test area widget and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the hit test area widget belongs.
- *int* **hit_test** - Hit test area type, one of the **[EngineWindow::HITTEST_*](../../../api/library/gui/class.enginewindow_cpp.md#HITTEST_INVALID)** values.

## WidgetHitTestArea ( int hit_test )

Constructor. Creates a hit test area widget of the specified type.
### Arguments

- *int* **hit_test** - Hit test area type, one of the **[EngineWindow::HITTEST_*](../../../api/library/gui/class.enginewindow_cpp.md#HITTEST_INVALID)** values.
