# Unigine::WindowManager Class (CPP)

**Header:** #include <UnigineWindowManager.h>

> **Notice:** This class is a singleton.


The class to manage windows enabling you to access any window of the appllication, group or stack windows, create various dialogs and so on.


### Accessing Windows


An application window can be accessed via the *[getWindow()](#getWindow_int_EngineWindow)* function. There are also some functions (like *[getMainWindow()](#getMainWindow_EngineWindowViewport)*) that allow accessing the specific windows (a focused window, a fullscreen window, the main application window, and so on). That's how you get an *[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)* class instance (or its child) that you can use to set screen size/resolution, position on the screen, decoration etc.


```cpp
// get the main window
EngineWindowPtr main_window = WindowManager::getMainWindow();
// change position and size(resolution) of the main window
if (main_window)
{
	main_window->setPosition(Math::ivec2(1020, 60));
	main_window->setSize(Math::ivec2(305, 670));
}


```


### Grouping Windows


The engine windows created via the *[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)* class can be grouped. There are three types of the **window groups**:


- Vertical
- Horizontal
- Group of tabs


The number of windows in the group is unlimited.


The WindowManager class provides two main functions for grouping windows:


- *[stack()](#stack_EngineWindow_EngineWindow_int_int_int_EngineWindowGroup)* creates a group of two windows.
- *[stackGroups()](#stackGroups_EngineWindowGroup_EngineWindowGroup_int_EngineWindowGroup)* creates a group of two window groups.


```cpp
// create separate windows
EngineWindowViewportPtr horizontal_1 = EngineWindowViewport::create("Horizontal 1", 512, 256);
EngineWindowViewportPtr horizontal_2 = EngineWindowViewport::create("Horizontal 2", 512, 256);
EngineWindowViewportPtr horizontal_3 = EngineWindowViewport::create("Horizontal 3", 512, 256);
EngineWindowViewportPtr horizontal_4 = EngineWindowViewport::create("Horizontal 4", 512, 256);

// create 2 horizontal window groups
EngineWindowGroupPtr horizontal_group_1 = WindowManager::stack(horizontal_1, horizontal_2, EngineWindowGroup::GROUP_TYPE_HORIZONTAL);
EngineWindowGroupPtr horizontal_group_2 = WindowManager::stack(horizontal_3, horizontal_4, EngineWindowGroup::GROUP_TYPE_HORIZONTAL);
// create a vertical group of 2 horizontal groups
EngineWindowGroupPtr vertical_group = WindowManager::stackGroups(horizontal_group_1, horizontal_group_2, EngineWindowGroup::GROUP_TYPE_VERTICAL);
// specify position, size, title of the verical window group
vertical_group->setPosition(Math::ivec2(50, 60));
vertical_group->setSize(Math::ivec2(565, 310));
vertical_group->setTitle("Vertical Group");
// render the window group
vertical_group->show();


```


Each window or window group has a [state](../../../api/library/gui/class.enginewindow_cpp.md#TYPE), so it changes after stacking.


![](window_manager_stacking.png)


There are also functions based on the *stack()* function that should be used in specific cases to avoid additional checking of arguments:


- *[stackToParentGroup()](#stackToParentGroup_EngineWindow_EngineWindow_int_int_EngineWindowGroup)* stacks the second window to the parent group of the first window. In the result, both windows passed as arguments will be on the same level in the group hierarchy.
- *[stackWindows()](#stackWindows_EngineWindowViewport_EngineWindowViewport_int_EngineWindowGroup)* creates a group of the separate/nested windows. The windows are stacked in the default order.
- *[stack()](#stack_EngineWindow_EngineWindow_int_int_int_EngineWindowGroup)* stacks the window to the other window. If the first argument is the separate window, a new window group is returned. If the first argument is the nested window, the window is added to its group.
- *[stackToGroup()](#stackToGroup_EngineWindowGroup_EngineWindow_int_int_EngineWindowGroup)* stacks the window or window group to another window group.


Follow the links to see the code examples.


For ungrouping, the *[unstack()](#unstack_EngineWindow_void)* function is used: it removes the window or the window group from the parent group.


### Creating Dialog Windows


To create a dialog window, use the corresponding functions of the class. For example:


```cpp
// event handler function
int AppSystemLogic::onButtonClicked(const WidgetPtr &sender_widget, int buttons)
{
	// show the message dialog
	WindowManager::dialogMessage("Message", "The button has been pressed.");

	return 1;

}

int AppSystemLogic::init()
{

	// create a window with widgets in the client area
	auto create_window = [](const char *name)
	{
		EngineWindowViewportPtr window = EngineWindowViewport::create(name, 512, 256);

		window->addChild(WidgetLabel::create(window->getSelfGui(), String::format("This is a %s.", name)), Gui::ALIGN_TOP);
		window->addChild(WidgetButton::create(window->getSelfGui(), name), Gui::ALIGN_CENTER);

		return window;

	};

	{
		// create a window
		EngineWindowViewportPtr window = create_window("Window");
		// get the child widget of the window
		WidgetPtr button = window->getChild(1);
		// subscribe to the Clicked event
		button->getEventClicked().connect(this, &AppSystemLogic::onButtonClicked);
		// show the window
		window->setPosition(Math::ivec2(50, 60));
		window->show();
	}

	return 1;
}


```


### See Also


- A set of SDK samples (`source/window_manager/`) demonstrating various usage aspects.


## WindowManager Class

### Enums

## DPI_AWARENESS

| Name | Description |
|---|---|
| **DPI_AWARENESS_CUSTOM** = -1 | The DPI awareness is set not on the engine side. For example, when the application is integrated via CustomSystemProxy, the user sets the required mode. |
| **DPI_AWARENESS_UNAWARE** = CUSTOM + 1 | Scaling is not taken into account. Windows are displayed with the default DPI level of 96 (100%). The operating system will stretch the raster part of the window and it will look blurry. |
| **DPI_AWARENESS_SYSTEM_AWARE** = UNAWARE + 1 | The DPI level of the main system display is obtained. Only with this DPI level the image is displayed clearly. Displays with another DPI level of changing of the DPI value on the main system display while running the application will cause the image blurring. |
| **DPI_AWARENESS_PER_MONITOR_AWARE** = SYSTEM_AWARE + 1 | Windows get the DPI level from each display individually. > **Notice:** Not available on Linux. |

### Members

## Ptr < EngineWindowViewport > getMainWindow () const

Returns the current window viewport that is set as the main window by default.
> **Notice:** There may be several windows that are set as main, or no main windows at all.


### Return value

Current engine window viewport.
## int getNumWindows () const

Returns the current number of windows.
### Return value

Current number of windows.
## bool isFullscreenMode () const

Returns the current value indicating if the window is the fullscreen state, or in the window mode.
### Return value

**true** if the window is the fullscreen state; otherwise **false**.
## bool isMultipleWindowsSupported () const

Returns the current value indicating if the engine can create more than one window.
### Return value

**true** if multiple windows are supported; otherwise **false**.
## Ptr < EngineWindow > getFocusedWindow () const

Returns the current window viewport which is currently in focus.
### Return value

Current window viewport which is currently in focus.
## Ptr < EngineWindow > getUnderCursorWindow () const

Returns the current window viewport which is currently under cursor.
### Return value

Current window viewport which is currently under cursor.
## Ptr < EngineWindowViewport > getSystemFocusedWindow () const

Returns the current engine window viewport that has the [isSystemFocused()](../../../api/library/gui/class.enginewindow_cpp.md#isSystemFocused_int) flag enabled, either a window itself or its parent group with the system focus is enabled. If there is no window with such a flag, nullptr is returned.
### Return value

Current engine window viewport that has the [isSystemFocused()](../../../api/library/gui/class.enginewindow_cpp.md#isSystemFocused_int) flag enabled, or nullptr if there is no such window.
## bool isAutoDpiScaling () const

Returns the current value specifying if automatic DPI scaling is applied to the window. If automatic DPI scaling is disabled, all GUI elements have the 100% size, only the system window size is scaled.
> **Notice:** This value is stored in the boot config file and can be changed only at the application startup. It cannot be changed at runtime, thus at an attempt to change the value the console will show the corresponding warning.


### Return value

**true** if all GUI elements of the window are scaled is enabled ; otherwise **false**.
## WindowManager::DPI_AWARENESS getDpiAwareness () const

Returns the current DPI awareness mode, the value indicating how the application processes the DPI scaling. The value is set to [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) by default. On Windows, if a specified mode cannot be set, it will switch to a possible lower value with a corresponding warning. On Linux, [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) is currently not supported, setting this value will switch the mode to the [SYSTEM_AWARE](#DPI_AWARENESS_SYSTEM_AWARE) mode with the corresponding warning in the console.
> **Notice:** This value is stored in the boot config file and can be changed only at the application startup. It cannot be changed at runtime, thus at an attempt to change the value the console will show the corresponding warning.


### Return value

Current DPI awareness mode, the value indicating how the application processes the DPI scaling.
## WindowManager::DPI_AWARENESS getCurrentDpiAwareness () const

Returns the current actual DPI awareness mode, the value indicating how the application processes the DPI scaling. The value is set to [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) by default. On Windows, if a specified mode cannot be set, it will switch to a possible lower value with a corresponding warning. On Linux, [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) is currently not supported, setting this value will switch the mode to the [SYSTEM_AWARE](#DPI_AWARENESS_SYSTEM_AWARE) mode with the corresponding warning in the console.
> **Notice:** This is an actual value, it may differ from the mode stored in the boot config file (in case the system cannot set the specified mode it will try to use the one that is suitable instead).


### Return value

Current actual DPI awareness mode
## static Event<const Ptr < WindowEvent > &> getEventImmediateWindowEvent () const

event triggered immediately as event from the window is received from proxy before being processed by the engine. This event can be triggered in different threads depending on the proxy implementation. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<WindowEvent> & **event**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ImmediateWindowEvent event handler
void immediatewindowevent_event_handler(const Ptr<WindowEvent> & event)
{
	Log::message("\Handling ImmediateWindowEvent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections immediatewindowevent_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager::getEventImmediateWindowEvent().connect(immediatewindowevent_event_connections, immediatewindowevent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager::getEventImmediateWindowEvent().connect(immediatewindowevent_event_connections, [](const Ptr<WindowEvent> & event) {
		Log::message("\Handling ImmediateWindowEvent event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
immediatewindowevent_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection immediatewindowevent_event_connection;

// subscribe to the ImmediateWindowEvent event with a handler function keeping the connection
WindowManager::getEventImmediateWindowEvent().connect(immediatewindowevent_event_connection, immediatewindowevent_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
immediatewindowevent_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
immediatewindowevent_event_connection.setEnabled(true);

// ...

// remove subscription to the ImmediateWindowEvent event via the connection
immediatewindowevent_event_connection.disconnect();

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

	// A ImmediateWindowEvent event handler implemented as a class member
	void event_handler(const Ptr<WindowEvent> & event)
	{
		Log::message("\Handling ImmediateWindowEvent event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
WindowManager::getEventImmediateWindowEvent().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId immediatewindowevent_handler_id;

// subscribe to the ImmediateWindowEvent event with a lambda handler function and keeping connection ID
immediatewindowevent_handler_id = WindowManager::getEventImmediateWindowEvent().connect(e_connections, [](const Ptr<WindowEvent> & event) {
		Log::message("\Handling ImmediateWindowEvent event (lambda).\n");
	}
);

// remove the subscription later using the ID
WindowManager::getEventImmediateWindowEvent().disconnect(immediatewindowevent_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ImmediateWindowEvent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager::getEventImmediateWindowEvent().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
WindowManager::getEventImmediateWindowEvent().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < EngineWindow > &> getEventWindowUnstacked () const

event triggered after the window has been unstacked. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<EngineWindow> & **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the WindowUnstacked event handler
void windowunstacked_event_handler(const Ptr<EngineWindow> & window)
{
	Log::message("\Handling WindowUnstacked event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowunstacked_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager::getEventWindowUnstacked().connect(windowunstacked_event_connections, windowunstacked_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager::getEventWindowUnstacked().connect(windowunstacked_event_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling WindowUnstacked event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
windowunstacked_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection windowunstacked_event_connection;

// subscribe to the WindowUnstacked event with a handler function keeping the connection
WindowManager::getEventWindowUnstacked().connect(windowunstacked_event_connection, windowunstacked_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
windowunstacked_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
windowunstacked_event_connection.setEnabled(true);

// ...

// remove subscription to the WindowUnstacked event via the connection
windowunstacked_event_connection.disconnect();

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

	// A WindowUnstacked event handler implemented as a class member
	void event_handler(const Ptr<EngineWindow> & window)
	{
		Log::message("\Handling WindowUnstacked event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
WindowManager::getEventWindowUnstacked().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId windowunstacked_handler_id;

// subscribe to the WindowUnstacked event with a lambda handler function and keeping connection ID
windowunstacked_handler_id = WindowManager::getEventWindowUnstacked().connect(e_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling WindowUnstacked event (lambda).\n");
	}
);

// remove the subscription later using the ID
WindowManager::getEventWindowUnstacked().disconnect(windowunstacked_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all WindowUnstacked events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager::getEventWindowUnstacked().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
WindowManager::getEventWindowUnstacked().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < EngineWindow > &> getEventWindowStacked () const

event triggered after the window has been stacked. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<EngineWindow> & **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the WindowStacked event handler
void windowstacked_event_handler(const Ptr<EngineWindow> & window)
{
	Log::message("\Handling WindowStacked event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowstacked_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager::getEventWindowStacked().connect(windowstacked_event_connections, windowstacked_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager::getEventWindowStacked().connect(windowstacked_event_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling WindowStacked event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
windowstacked_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection windowstacked_event_connection;

// subscribe to the WindowStacked event with a handler function keeping the connection
WindowManager::getEventWindowStacked().connect(windowstacked_event_connection, windowstacked_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
windowstacked_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
windowstacked_event_connection.setEnabled(true);

// ...

// remove subscription to the WindowStacked event via the connection
windowstacked_event_connection.disconnect();

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

	// A WindowStacked event handler implemented as a class member
	void event_handler(const Ptr<EngineWindow> & window)
	{
		Log::message("\Handling WindowStacked event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
WindowManager::getEventWindowStacked().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId windowstacked_handler_id;

// subscribe to the WindowStacked event with a lambda handler function and keeping connection ID
windowstacked_handler_id = WindowManager::getEventWindowStacked().connect(e_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling WindowStacked event (lambda).\n");
	}
);

// remove the subscription later using the ID
WindowManager::getEventWindowStacked().disconnect(windowstacked_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all WindowStacked events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager::getEventWindowStacked().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
WindowManager::getEventWindowStacked().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < EngineWindow > &> getEventWindowRemoved () const

event triggered after the window has been removed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<EngineWindow> & **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the WindowRemoved event handler
void windowremoved_event_handler(const Ptr<EngineWindow> & window)
{
	Log::message("\Handling WindowRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowremoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager::getEventWindowRemoved().connect(windowremoved_event_connections, windowremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager::getEventWindowRemoved().connect(windowremoved_event_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling WindowRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
windowremoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection windowremoved_event_connection;

// subscribe to the WindowRemoved event with a handler function keeping the connection
WindowManager::getEventWindowRemoved().connect(windowremoved_event_connection, windowremoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
windowremoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
windowremoved_event_connection.setEnabled(true);

// ...

// remove subscription to the WindowRemoved event via the connection
windowremoved_event_connection.disconnect();

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

	// A WindowRemoved event handler implemented as a class member
	void event_handler(const Ptr<EngineWindow> & window)
	{
		Log::message("\Handling WindowRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
WindowManager::getEventWindowRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId windowremoved_handler_id;

// subscribe to the WindowRemoved event with a lambda handler function and keeping connection ID
windowremoved_handler_id = WindowManager::getEventWindowRemoved().connect(e_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling WindowRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
WindowManager::getEventWindowRemoved().disconnect(windowremoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all WindowRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager::getEventWindowRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
WindowManager::getEventWindowRemoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < EngineWindow > &> getEventWindowCreated () const

event triggered after the window has been created. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<EngineWindow> & **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the WindowCreated event handler
void windowcreated_event_handler(const Ptr<EngineWindow> & window)
{
	Log::message("\Handling WindowCreated event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowcreated_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager::getEventWindowCreated().connect(windowcreated_event_connections, windowcreated_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager::getEventWindowCreated().connect(windowcreated_event_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling WindowCreated event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
windowcreated_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection windowcreated_event_connection;

// subscribe to the WindowCreated event with a handler function keeping the connection
WindowManager::getEventWindowCreated().connect(windowcreated_event_connection, windowcreated_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
windowcreated_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
windowcreated_event_connection.setEnabled(true);

// ...

// remove subscription to the WindowCreated event via the connection
windowcreated_event_connection.disconnect();

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

	// A WindowCreated event handler implemented as a class member
	void event_handler(const Ptr<EngineWindow> & window)
	{
		Log::message("\Handling WindowCreated event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
WindowManager::getEventWindowCreated().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId windowcreated_handler_id;

// subscribe to the WindowCreated event with a lambda handler function and keeping connection ID
windowcreated_handler_id = WindowManager::getEventWindowCreated().connect(e_connections, [](const Ptr<EngineWindow> & window) {
		Log::message("\Handling WindowCreated event (lambda).\n");
	}
);

// remove the subscription later using the ID
WindowManager::getEventWindowCreated().disconnect(windowcreated_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all WindowCreated events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager::getEventWindowCreated().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
WindowManager::getEventWindowCreated().setEnabled(true);

```

</details>

### Return value

Event instance.
## Ptr < EngineWindowViewport > getFullscreenWindow () const

Returns the current first engine window viewport that is in the fullscreen state.
### Return value

Current first engine window viewport that is in the fullscreen state, or NULL if noneThe viewport in the fullscreen state, or nullptr if no window is found.
---

## Ptr < EngineWindow > getWindow ( int index )

Returns the window by its index.
### Arguments

- *int* **index** - Index of the window.

### Return value

Engine window.
## int getWindowIndex ( const Ptr < EngineWindow > & window ) const

Returns the index of the specified window.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - Engine window.

### Return value

Index of the window.
## Ptr < EngineWindowGroup > stack ( const Ptr < EngineWindow > & first_window , const Ptr < EngineWindow > & second_window , EngineWindowGroup::GROUP_TYPE group_type , int index = -1 , bool decompose_second = false )

Stacks the window to the other window. If the first argument is the separate window, a new window group is returned. If the first argument is the nested window, the window is added to its group.
```cpp
EngineWindowPtr window_1 = EngineWindowViewport::create("Window 1", 512, 256);
EngineWindowPtr window_2 = EngineWindowViewport::create("Window 2", 512, 256);
EngineWindowPtr window_3 = EngineWindowViewport::create("Window 3", 512, 256);

// create a group of 2 windows
EngineWindowGroupPtr group_1 = WindowManager::stack(window_1, window_2, EngineWindowGroup::GROUP_TYPE_HORIZONTAL);
// stack a separate window to the window from the window group
WindowManager::stack(window_1, window_3, EngineWindowGroup::GROUP_TYPE_VERTICAL);


```

 In the result, *group_1* will consist of 3 windows: *window_1* and *window_3* stacked vertically and *window_2* stacked horizontally.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **first_window** - The parent window to which another window is stacked.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **second_window** - The window to be stacked.
- *[EngineWindowGroup::GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cpp.md#GROUP_TYPE)* **group_type** - Type of a group to be created.
- *int* **index**
- *bool* **decompose_second** - Flag to decompose the second argument of the merge, if it is a group, and combine with the first group.

### Return value

Group of stacked windows.
## Ptr < EngineWindowGroup > stackToParentGroup ( const Ptr < EngineWindow > & window_in_group , const Ptr < EngineWindow > & window , int index = -1 , bool decompose_second = false )

Stacks the second window to the parent window group of the first window. In the result, both windows passed as arguments will be on the same level in the group hierarchy. If the first window has no parent group, the function will return it as is.
```cpp
EngineWindowPtr window_1 = EngineWindowViewport::create("Window 1", 512, 256);
EngineWindowPtr window_2 = EngineWindowViewport::create("Window 2", 512, 256);
EngineWindowPtr window_3 = EngineWindowViewport::create("Window 3", 512, 256);

// stack 2 separate windows
EngineWindowGroupPtr group_0 = WindowManager::stack(window_1, window_2, EngineWindowGroup::GROUP_TYPE_HORIZONTAL);
// stack a separate window to the parent group of "window_1"
WindowManager::stackToParentGroup(window_1, window_3);


```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window_in_group** - The window into the parent group of which the other window is stacked.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - The window to be stacked.
- *int* **index** - A place where a window or a group should be placed in a group.
- *bool* **decompose_second** - Flag to decompose the second argument of the merge, if it is a group, and combine with the first window or a group.

### Return value

Group of windows.
## Ptr < EngineWindowGroup > stackWindows ( const Ptr < EngineWindowViewport > & first_viewport , const Ptr < EngineWindowViewport > & second_viewport , EngineWindowGroup::GROUP_TYPE group_type = Enum.EngineWindowGroup.GROUP_TYPE.TAB )

Returns a newly created group of the separate and/or nested windows. You cannot stack the window group to the separate window, however, you can stack a window nested in the window group: in this case, the window will be unstacked from its parent group and added to the new one. The windows are stacked in the default order. For example:
```cpp
EngineWindowViewportPtr window_1 = EngineWindowViewport::create("Window 1", 512, 256);
EngineWindowViewportPtr window_2 = EngineWindowViewport::create("Window 2", 512, 256);
EngineWindowViewportPtr window_3 = EngineWindowViewport::create("Window 3", 512, 256);

// stack 2 separate windows
EngineWindowGroupPtr group_0 = WindowManager::stack(window_1, window_2, EngineWindowGroup::GROUP_TYPE_HORIZONTAL);

// stack a window from the window group to a separate window
EngineWindowGroupPtr group_1 = WindowManager::stackWindows(window_3, window_1, EngineWindowGroup::GROUP_TYPE_VERTICAL);


```

 In the result, *group_1* will be a vertical group of *window_3* and *window_1*.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cpp.md)> &* **first_viewport** - The window to be stacked.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cpp.md)> &* **second_viewport** - The window to be stacked.
- *[EngineWindowGroup::GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cpp.md#GROUP_TYPE)* **group_type** - Type of a group to be created.

### Return value

Group of windows.
## Ptr < EngineWindowGroup > stackWithWindow ( const Ptr < EngineWindowViewport > & window_viewport , const Ptr < EngineWindow > & window , EngineWindowGroup::GROUP_TYPE group_type , bool decompose_second = false )

Returns a newly created group of the engine window viewport and any other engine window � another viewport or a window group.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cpp.md)> &* **window_viewport** - The window viewport to be stacked.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - The window to be stacked.
- *[EngineWindowGroup::GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cpp.md#GROUP_TYPE)* **group_type** - Type of a window group to be created.
- *bool* **decompose_second** - Flag to decompose the second argument of the merge, if it is a group, and combine with the first group.

### Return value

Group of windows.
## Ptr < EngineWindowGroup > stackGroups ( const Ptr < EngineWindowGroup > & first_group , const Ptr < EngineWindowGroup > & second_group , EngineWindowGroup::GROUP_TYPE group_type )

Returns the group of window groups. The second group is added to the first group. To combine two windows or a group and a window, use the *[stack()](#stack_EngineWindow_EngineWindow_int_int_int_EngineWindowGroup)* method.
```cpp
EngineWindowPtr window_1 = EngineWindowViewport::create("Window 1", 512, 256);
EngineWindowPtr window_2 = EngineWindowViewport::create("Window 2", 512, 256);
EngineWindowPtr window_3 = EngineWindowViewport::create("Window 3", 512, 256);
EngineWindowPtr window_4 = EngineWindowViewport::create("Window 4", 512, 256);

// create 2 horizontal groups of windows
EngineWindowGroupPtr group_1 = WindowManager::stack(window_1, window_2, EngineWindowGroup::GROUP_TYPE_HORIZONTAL);
EngineWindowGroupPtr group_2 = WindowManager::stack(window_3, window_4, EngineWindowGroup::GROUP_TYPE_HORIZONTAL);
// stack one group to another to create a new vertical group
EngineWindowGroupPtr group_3 = WindowManager::stackGroups(group_1, group_2, EngineWindowGroup::GROUP_TYPE_VERTICAL);


```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cpp.md)> &* **first_group** - The first window group for merging.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cpp.md)> &* **second_group** - The second window group for merging.
- *[EngineWindowGroup::GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cpp.md#GROUP_TYPE)* **group_type** - Type of a group to be created.

### Return value

Group of windows.
## Ptr < EngineWindowGroup > stackToGroup ( const Ptr < EngineWindowGroup > & destination_group , const Ptr < EngineWindow > & group , int index = -1 , bool decompose_second = false )

Stacks the window or window group to another window group. The updated group of windows is returned.
```cpp
EngineWindowPtr window_1 = EngineWindowViewport::create("Window 1", 512, 256);
EngineWindowPtr window_2 = EngineWindowViewport::create("Window 2", 512, 256);
EngineWindowPtr window_3 = EngineWindowViewport::create("Window 3", 512, 256);
EngineWindowPtr window_4 = EngineWindowViewport::create("Window 4", 512, 256);

// create 2 horizontal groups of windows
EngineWindowGroupPtr group_1 = WindowManager::stack(window_1, window_2, EngineWindowGroup::GROUP_TYPE_HORIZONTAL);
EngineWindowGroupPtr group_2 = WindowManager::stack(window_3, window_4, EngineWindowGroup::GROUP_TYPE_HORIZONTAL);

// stack one group to another
WindowManager::stackToGroup(group_1, group_2);


```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cpp.md)> &* **destination_group** - The parent group to which another group is stacked.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **group** - The window or window group to be stacked.
- *int* **index** - A place where a window or a group should be placed in a group.
- *bool* **decompose_second** - Flag to decompose the second argument of the merge and combine with the first group.

### Return value

Group of stacked windows.
## void unstack ( const Ptr < EngineWindow > & unstacked )

Removes a window or a group from a parent group. If there is only one window left, the group is automatically deleted after removing the window from it.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **unstacked** - A window or a group to be removed from a parent group.

## bool isFullscreenWindow ( const Ptr < EngineWindow > & window )

Returns the value indicating if the specified window is in a fullscreen state.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)> &* **window** - The window to be checked.

### Return value

true if the engine window is the fullscreen state, false if it is in the window mode.
## Ptr < EngineWindow > getWindowByID ( unsigned long long win_id ) const

Returns the window by its ID.
### Arguments

- *unsigned long long* **win_id** - Window ID.

### Return value

Window with the specified ID, or nullptr if the window is not found.
## bool dialogMessage ( const char * title , const char * message )

Displays a message dialog with the specified title and text.
### Arguments

- *const char ** **title** - Title of the message dialog to be displayed.
- *const char ** **message** - Message text to be displayed.

### Return value

true if the message is displayed successfully; otherwise, false.
## bool dialogWarning ( const char * title , const char * warning )

Displays a warning dialog with the specified title and text.
### Arguments

- *const char ** **title** - Title of the warning dialog to be displayed.
- *const char ** **warning** - Warning message text to be displayed.

### Return value

true if the message is displayed successfully; otherwise, false.
## bool dialogError ( const char * title , const char * error )

Displays an error dialog with the specified title and text.
### Arguments

- *const char ** **title** - Title of the error dialog to be displayed.
- *const char ** **error** - Error message text to be displayed.

### Return value

**true** if the message is displayed successfully; otherwise, **false**.
## int showSystemDialog ( const Ptr < SystemDialog > & dialog )

Displays a custom [system dialog](../../../api/library/engine/class.systemdialog_cpp.md) with an arbitrary set of buttons.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SystemDialog](../../../api/library/engine/class.systemdialog_cpp.md)> &* **dialog** - [*SystemDialog*](../../../api/library/engine/class.systemdialog_cpp.md) class instance representing the custom system dialog to be shown.

### Return value

Number of the dialog button clicked by the user; or **-1** if an error has occurred.
## const char * dialogOpenFolder ( const char * path )

Opens a common dialog enabling the user to specify a folder to open. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *const char ** **path** - Path to be set by default when the dialog opens.

### Return value

Resulting folder name specified by the user.
## const char * dialogOpenFolder ( )

Opens a common dialog enabling the user to specify a folder to open.
### Return value

Resulting folder name specified by the user.
## Vector < String > dialogOpenFiles ( const char * path , const char * filter )

Opens a common dialog enabling the user to specify a list of filenames to open multiple files. When the dialog opens the specified default path and file filter shall be set displaying the corresponding elements.
### Arguments

- *const char ** **path** - Path to be set by default when the dialog opens.
- *const char ** **filter** - File name filter string to be set by default when the dialog opens. This filter string determines file type choices to be displayed in the *Files of type* box.

### Return value

Resulting list of filenames specified by the user.
## Vector < String > dialogOpenFiles ( const char * path )

Opens a common dialog enabling the user to specify a list of filenames to open multiple files. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *const char ** **path** - Path to be set by default when the dialog opens.

### Return value

Resulting list of filenames specified by the user.
## Vector < String > dialogOpenFiles ( )

Opens a common dialog enabling the user to specify a list of filenames to open multiple files.
### Return value

Resulting list of filenames specified by the user.
## const char * dialogOpenFile ( const char * path , const char * filter )

Opens a common dialog enabling the user to specify a filename to open a file. When the dialog opens the specified default path and file filter shall be set displaying the corresponding elements.
### Arguments

- *const char ** **path** - Path to be set by default when the dialog opens.
- *const char ** **filter** - File name filter string to be set by default when the dialog opens. This filter string determines file type choices to be displayed in the *Files of type* box.

### Return value

Resulting filename specified by the user.
## const char * dialogOpenFile ( const char * path )

Opens a common dialog enabling the user to specify a filename to open a file. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *const char ** **path** - Path to be set by default when the dialog opens.

### Return value

Resulting filename specified by the user.
## const char * dialogOpenFile ( )

Opens a common dialog enabling the user to specify a filename to open a file.
### Return value

Resulting filename specified by the user.
## const char * dialogSaveFile ( const char * path , const char * filter )

Opens a common dialog enabling the user to specify a filename to save a file as. When the dialog opens the specified default path and file filter shall be set displaying the corresponding elements.
### Arguments

- *const char ** **path** - Path to be set by default when the dialog opens.
- *const char ** **filter** - File name filter string to be set by default when the dialog opens. This filter string determines file type choices to be displayed in the *Save as file type* or *Files of type* box.

### Return value

Resulting filename specified by the user.
## const char * dialogSaveFile ( const char * path )

Opens a common dialog enabling the user to specify a filename to save a file as. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *const char ** **path** - Path to be set by default when the dialog opens.

### Return value

Resulting filename specified by the user.
## const char * dialogSaveFile ( )

Opens a common dialog enabling the user to specify a filename to save a file as.
### Return value

Resulting filename specified by the user.
## Ptr < EngineWindow > getIntersection ( const Math:: ivec2 & global_pos , const Vector < Ptr < EngineWindow >> & excludes ) const

Returns the window the intersection with which is detected.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **global_pos** - The position of the intersection point in global coordinates.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)>> &* **excludes** - The windows to be excluded from the intersection detection.

### Return value

The window the intersection with which is detected.
## Ptr < EngineWindow > getIntersection ( const Math:: ivec2 & global_pos ) const

Returns the window the intersection with which is detected.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **global_pos** - The position of the intersection point in global coordinates.

### Return value

The window the intersection with which is detected.
## void forceUpdateWindowOrders ( )

Updates the Z order of all windows.
> **Notice:** It is recommended to use this method only when required, because it is very slow.


## void setEventsFilter ( int (*)(const Ptr < InputEvent > &) func )

Sets a callback function to be executed on receiving input events. This input event filter enables you to reject certain input events for the Engine and get necessary information on all input events.
### Arguments

- *int (*)(const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[InputEvent](../../../api/library/controls/class.inputevent_cpp.md)> &)* **func** - Input event callback.
