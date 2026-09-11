# Unigine::UserInterface Class (CPP)

**Header:** #include <UnigineUserInterface.h>


The class is used to work with widgets that are created by loading a UI file.


### Usage Examples


The examples below show:

- Loading a UserInterface from the `*.ui` file and accessing the widgets it stores.
- Adding callbacks to these widgets.
- Managing the UserInterface lifetime.


#### Managing Lifetime by the World


The UserInterface is created on loading the world. When you reload or exit the world, or close the Engine window, the UserInterface is deleted.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
#include "AppWorldLogic.h"
#include <UnigineWidgets.h>

#include <UnigineUserInterface.h>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econn;

void on_group_remove(const WidgetPtr &group)
{
	Log::message("world group removed\n");
}

int AppWorldLogic::init()
{

	// world user interface
	UserInterfacePtr ui = UserInterface::create(Gui::getCurrent(), "user_interface.ui");
	ui->setLifetime(Widget::LIFETIME_WORLD);

	auto main_group = checked_ptr_cast<WidgetGroupBox>(ui->getWidget(ui->findWidget("main_group")));
	main_group->setText("World User Interface");
	main_group->getEventRemove().connect(econn, on_group_remove);
	WindowManager::getMainWindow()->addChild(main_group, Gui::ALIGN_EXPAND);

	return 1;
}

int AppWorldLogic::shutdown()
{
	// removing all event subscriptions
	econn.disconnectAll();

	return 1;
}


```

</details>


#### Managing Lifetime by the Window


The UserInterface is created in a separate window. When you close the window, the UserInterface is deleted as its lifetime is managed by this window. The console shows whether the window and UserInterface are deleted or not, whether the remove event is fired, and the message from the remove event handler (if it is).


After closing, the window can be re-created by pressing **T**.


<details>
<summary>AppSystemLogic.cpp | Close</summary>

`AppSystemLogic.cpp`


```cpp
#include "AppSystemLogic.h"
#include <UnigineWidgets.h>

#include <UnigineUserInterface.h>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

EngineWindowViewportPtr window;

UserInterfacePtr ui;
WidgetGroupBoxPtr main_group;

bool group_remove_handler = false;

void on_window_group_remove()
{
	Log::message("window group removed\n");
	group_remove_handler = true;
}

void create_window()
{

	window = EngineWindowViewport::create("Test", 512, 256, EngineWindow::FLAGS_SHOWN);

	// window user interface
	ui = UserInterface::create(window->getGui(), "user_interface.ui");
	ui->setLifetime(Widget::LIFETIME_WINDOW);

	main_group = checked_ptr_cast<WidgetGroupBox>(ui->getWidget(engine_ui->findWidget("main_group")));
	main_group->setText("Window User Interface");
	main_group->getEventRemove().connect(econnections, on_window_group_remove);
	window->addChild(main_group, Gui::ALIGN_EXPAND);

}

int AppSystemLogic::init()
{

	create_window();

	return 1;
}

int AppSystemLogic::update()
{

	if (Input::isKeyDown(Input::KEY_T) && window.isDeleted())
		create_window();

	Log::message("window deleted: %d, group deleted: %d, ui deleted: %d, group remove handler %d\n",
		window.isDeleted(), main_group.isDeleted(), ui.isDeleted(), group_remove_handler);


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


#### Managing Lifetime by the Engine


The lifetime of the UserInterface is managed by the Engine, so it is deleted on Engine shutdown. A [Gui](../../../api/library/gui/class.gui_cpp.md) instance is set manually via the *[setGui()](#setGui_Gui_void)* method.


The console shows whether the window and UserInterface are deleted or not, whether the remove event is fired, and the message from the remove event handler (if it is). After closing, the window can be re-created by pressing **T**.


<details>
<summary>AppSystemLogic.cpp | Close</summary>

`AppSystemLogic.cpp`


```cpp
#include "AppSystemLogic.h"
#include <UnigineWidgets.h>

#include <UnigineUserInterface.h>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

EngineWindowViewportPtr engine_window;

UserInterfacePtr engine_ui;
WidgetGroupBoxPtr engine_main_group;

bool engine_group_remove_handler = false;

void on_engine_group_remove(const WidgetPtr &group)
{
	Log::message("engine group removed\n");
	engine_group_remove_handler = true;
}

void create_engine_window()
{

	engine_window = EngineWindowViewport::create("Test", 512, 256, EngineWindow::FLAGS_SHOWN);

	engine_ui->setGui(engine_window->getGui());
	engine_window->addChild(engine_main_group, Gui::ALIGN_EXPAND);

}

int AppSystemLogic::init()
{

	// engine user interface
	engine_ui = UserInterface::create(Gui::getCurrent(), "user_interface.ui");
	engine_ui->setLifetime(Widget::LIFETIME_ENGINE);

	engine_main_group = checked_ptr_cast<WidgetGroupBox>(engine_ui->getWidget(ui->findWidget("main_group")));
	engine_main_group->setText("Engine User Interface");
	engine_main_group->getEventRemove().connect(econnections, on_engine_group_remove);

	create_engine_window();

	return 1;
}

int AppSystemLogic::update()
{

	if (Input::isKeyDown(Input::KEY_T) && engine_window.isDeleted())
		create_engine_window();

	Log::message("engine window deleted: %d,engine group deleted: %d, engine ui deleted: %d, engine group remove handler %d\n",
		engine_window.isDeleted(), engine_main_group.isDeleted(), engine_ui.isDeleted(), engine_group_remove_handler);

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


### See Also


- C++ sample
- C# Component sample


## UserInterface Class

### Enums

## EVENT_TYPE

| Name | Description |
|---|---|
| **EVENT_SHOW** = 0 |  |
| **EVENT_HIDE** = 1 |  |
| **EVENT_FOCUS_IN** = 2 |  |
| **EVENT_FOCUS_OUT** = 3 |  |
| **EVENT_CHANGED** = 4 |  |
| **EVENT_CLICKED** = 5 |  |
| **EVENT_DOUBLE_CLICKED** = 6 |  |
| **EVENT_PRESSED** = 7 |  |
| **EVENT_RELEASED** = 8 |  |
| **EVENT_KEY_PRESSED** = 9 |  |
| **EVENT_TEXT_PRESSED** = 10 |  |
| **EVENT_ENTER** = 11 |  |
| **EVENT_LEAVE** = 12 |  |
| **EVENT_DRAG_MOVE** = 13 |  |
| **EVENT_DRAG_DROP** = 14 |  |
| **EVENT_REMOVE** = 15 |  |
| **NUM_EVENTS** = 16 |  |

### Members

## int getNumWidgets () const

Returns the current number of associated widgets.
### Return value

Current number of associated widgets
## void setGui ( const Ptr < Gui >& gui )

Sets a new *[Gui](../../../api/library/gui/class.gui_cpp.md)* instance used for the UserInterface.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)>&* **gui** - The Gui instance used for the UserInterface

## Ptr < Gui > getGui () const

Returns the current *[Gui](../../../api/library/gui/class.gui_cpp.md)* instance used for the UserInterface.
### Return value

Current Gui instance used for the UserInterface
## void setLifetime ( Widget::LIFETIME lifetime )

Sets a new lifetime management type for the UserInterface. By default, the [LIFETIME_ENGINE](../../../api/library/gui/class.widget_cpp.md#LIFETIME) type is used.
> **Notice:** Lifetime of each UserInterface in the hierarchy is defined by its root. Thus, a lifetime management type set for a child UserInterface that differs from the one set for the root is ignored.

### Arguments

- *[Widget::LIFETIME](../../../api/library/gui/class.widget_cpp.md#LIFETIME)* **lifetime** - The lifetime management type for the UserInterface

## Widget::LIFETIME getLifetime () const

Returns the current lifetime management type for the UserInterface. By default, the [LIFETIME_ENGINE](../../../api/library/gui/class.widget_cpp.md#LIFETIME) type is used.
> **Notice:** Lifetime of each UserInterface in the hierarchy is defined by its root. Thus, a lifetime management type set for a child UserInterface that differs from the one set for the root is ignored.

### Return value

Current lifetime management type for the UserInterface
---

## static UserInterfacePtr create ( const Ptr < Gui > & gui , const char * name , const char * prefix = 0 )

UserInterface constructor.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - GUI smart pointer.
- *const char ** **name** - User interface name.
- *const char ** **prefix** - Names prefix.

## int getCallback ( int num , int callback ) const

Returns the number of a given callback function.
### Arguments

- *int* **num** - Widget number.
- *int* **callback** - Callback type number. One of the callbacks defined in the [Gui class](../../../api/library/gui/class.gui_cpp.md) (for example, CLICK, SHOW, HIDE, etc).

### Return value

Callback number.
## const char * getCallbackInstanceData ( int num , Gui::CALLBACK_INDEX callback ) const

Returns the callback instance data.
### Arguments

- *int* **num** - Widget number.
- *[Gui::CALLBACK_INDEX](../../../api/library/gui/class.gui_cpp.md#CALLBACK_INDEX)* **callback** - Callback type number. One of the callbacks defined in the [Gui class](../../../api/library/gui/class.gui_cpp.md) (for example, CLICK, SHOW, HIDE, etc).

### Return value

Callback instance data.
## const char * getCallbackName ( int num , Gui::CALLBACK_INDEX callback ) const

Returns the name of a given callback function.
### Arguments

- *int* **num** - Widget number.
- *[Gui::CALLBACK_INDEX](../../../api/library/gui/class.gui_cpp.md#CALLBACK_INDEX)* **callback** - Callback type number. One of the callbacks defined in the [Gui class](../../../api/library/gui/class.gui_cpp.md) (for example, CLICK, SHOW, HIDE, etc).

### Return value

Callback function name.
## const char * getCallbackStringData ( int num , Gui::CALLBACK_INDEX callback ) const

Returns the callback string data.
### Arguments

- *int* **num** - Widget number.
- *[Gui::CALLBACK_INDEX](../../../api/library/gui/class.gui_cpp.md#CALLBACK_INDEX)* **callback** - Callback type number. One of the callbacks defined in the [Gui class](../../../api/library/gui/class.gui_cpp.md) (for example, CLICK, SHOW, HIDE, etc).

### Return value

Callback string data.
## const char * getCallbackVariableData ( int num , Gui::CALLBACK_INDEX callback ) const

Returns the callback variable data.
### Arguments

- *int* **num** - Widget number.
- *[Gui::CALLBACK_INDEX](../../../api/library/gui/class.gui_cpp.md#CALLBACK_INDEX)* **callback** - Callback type number. One of the callbacks defined in the [Gui class](../../../api/library/gui/class.gui_cpp.md) (for example, CLICK, SHOW, HIDE, etc).

### Return value

Callback variable data.
## Ptr < Widget > getCallbackWidgetData ( int num , Gui::CALLBACK_INDEX callback ) const

Returns the callback widget data.
### Arguments

- *int* **num** - Widget number.
- *[Gui::CALLBACK_INDEX](../../../api/library/gui/class.gui_cpp.md#CALLBACK_INDEX)* **callback** - Callback type number. One of the callbacks defined in the [Gui class](../../../api/library/gui/class.gui_cpp.md) (for example, CLICK, SHOW, HIDE, etc).

### Return value

Widget data.
## int getNumCallbacks ( int num ) const

Returns the total number of callbacks for a given widget.
### Arguments

- *int* **num** - Widget number.

### Return value

Number of callbacks.
## Ptr < Widget > getWidget ( int num ) const

Returns a widget with the given ID.
### Arguments

- *int* **num** - Widget number.

### Return value

Pointer to the widget with the given number.
## Ptr < Widget > getWidgetByName ( const char * name ) const

Returns a widget with the given name.
### Arguments

- *const char ** **name** - Widget name.

### Return value

Widget with the given ID.
## int getWidgetExport ( int num ) const

Returns a value indicating if a given widget is exported into a script.
### Arguments

- *int* **num** - Widget number.

### Return value

Returns 1 if the widget is exported; otherwise, 0.
## const char * getWidgetName ( int num ) const

Returns widget name by its number.
### Arguments

- *int* **num** - Widget number.

### Return value

Widget name.
## const char * getWidgetNext ( int num ) const

Returns the name of the widget, which will be focused next.
### Arguments

- *int* **num** - Current widget number.

### Return value

Next Widget name.
## int findWidget ( const char * name ) const

Searches a widget by its name.
### Arguments

- *const char ** **name** - Widget name.

### Return value

Returns the number of the widget if exists; otherwise, -1.
## void updateWidgets ( ) const

Updates all widgets belonging to the user interface. This function should be called, for example, after change of the interface language.
