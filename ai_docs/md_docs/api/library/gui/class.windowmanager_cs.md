# Unigine::WindowManager Class (CS)

> **Notice:** This class is a singleton.


The class to manage windows enabling you to access any window of the appllication, group or stack windows, create various dialogs and so on.


### Accessing Windows


An application window can be accessed via the *[WindowManager.GetWindow()](#getWindow_int_EngineWindow)* function. There are also some properties (like *[WindowManager.MainWindow](#getMainWindow_EngineWindowViewport)*) that allow accessing the specific windows (a focused window, a fullscreen window, the main application window, and so on). That's how you get an *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* class instance (or its child) that you can use to set screen size/resolution, position on the screen, decoration etc.


```csharp
// get the main window
EngineWindow main_window = WindowManager.MainWindow;
// change position and size(resolution) of the main window
if (main_window)
{
	main_window.Position = new ivec2(1020, 60);
	main_window.Size = new ivec2(305, 670);
}


```


### Grouping Windows


The engine windows created via the *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* class can be grouped. There are three types of the **window groups**:


- Vertical
- Horizontal
- Group of tabs


The number of windows in the group is unlimited.


The WindowManager class provides two main functions for grouping windows:


- *[WindowManager.Stack()](#stack_EngineWindow_EngineWindow_int_int_int_EngineWindowGroup)* creates a group of two windows.
- *[WindowManager.StackGroups()](#stackGroups_EngineWindowGroup_EngineWindowGroup_int_EngineWindowGroup)* creates a group of two window groups.


```csharp
// create separate windows
EngineWindowViewport horizontal_1 = new EngineWindowViewport("Horizontal 1", 512, 256);
EngineWindowViewport horizontal_2 = new EngineWindowViewport("Horizontal 2", 512, 256);
EngineWindowViewport horizontal_3 = new EngineWindowViewport("Horizontal 3", 512, 256);
EngineWindowViewport horizontal_4 = new EngineWindowViewport("Horizontal 4", 512, 256);

// create 2 horizontal window groups
EngineWindowGroup horizontal_group_1 = WindowManager.Stack(horizontal_1, horizontal_2, EngineWindowGroup.GROUP_TYPE.HORIZONTAL);
EngineWindowGroup horizontal_group_2 = WindowManager.Stack(horizontal_3, horizontal_4, EngineWindowGroup.GROUP_TYPE.HORIZONTAL);
// create a vertical group of 2 horizontal groups
EngineWindowGroup vertical_group = WindowManager.StackGroups(horizontal_group_1, horizontal_group_2, EngineWindowGroup.GROUP_TYPE.VERTICAL);
// specify position, size, title of the verical window group
vertical_group.Position = new ivec2(50, 60);
vertical_group.Size = new ivec2(565, 310);
vertical_group.Title = "Vertical Group";
// render the window group
vertical_group.Show();


```


Each window or window group has a [state](../../../api/library/gui/class.enginewindow_cs.md#TYPE), so it changes after stacking.


![](window_manager_stacking.png)


There are also functions based on the *WindowManager.Stack()* function that should be used in specific cases to avoid additional checking of arguments:


- *[WindowManager.StackToParentGroup()](#stackToParentGroup_EngineWindow_EngineWindow_int_int_EngineWindowGroup)* stacks the second window to the parent group of the first window. In the result, both windows passed as arguments will be on the same level in the group hierarchy.
- *[WindowManager.StackWindows()](#stackWindows_EngineWindowViewport_EngineWindowViewport_int_EngineWindowGroup)* creates a group of the separate/nested windows. The windows are stacked in the default order.
- *[WindowManager.Stack()](#stack_EngineWindow_EngineWindow_int_int_int_EngineWindowGroup)* stacks the window to the other window. If the first argument is the separate window, a new window group is returned. If the first argument is the nested window, the window is added to its group.
- *[WindowManager.StackToGroup()](#stackToGroup_EngineWindowGroup_EngineWindow_int_int_EngineWindowGroup)* stacks the window or window group to another window group.


Follow the links to see the code examples.


For ungrouping, the *[WindowManager.Unstack()](#unstack_EngineWindow_void)* function is used: it removes the window or the window group from the parent group.


### Creating Dialog Windows


To create a dialog window, use the corresponding functions of the class. For example:


```csharp
// create a window with widgets in the client area
private EngineWindowViewport create_window (string name)
{
	EngineWindowViewport window = new EngineWindowViewport(name, 512, 256);

	window.AddChild(new WidgetLabel(window.SelfGui, String.Format("This is a {0}.", name)), Gui.ALIGN_TOP);
	window.AddChild(new WidgetButton(window.SelfGui, name), Gui.ALIGN_CENTER);

	return window;
}

private void Init()
{

	// create a window
	EngineWindowViewport window = create_window("Window");
	// get the child widget of the window
	Widget button = window.GetChild(1);
	// subscribe for the Click event for this widget
	button.EventClicked.Connect(() => WindowManager.DialogMessage("Message", "The button has been pressed."));
	// show the window
	window.Position = new ivec2(50, 60);
	window.Show();

}


```


## WindowManager Class

### Enums

## DPI_AWARENESS

| Name | Description |
|---|---|
| **CUSTOM** = -1 | The DPI awareness is set not on the engine side. For example, when the application is integrated via CustomSystemProxy, the user sets the required mode. |
| **UNAWARE** = CUSTOM + 1 | Scaling is not taken into account. Windows are displayed with the default DPI level of 96 (100%). The operating system will stretch the raster part of the window and it will look blurry. |
| **SYSTEM_AWARE** = UNAWARE + 1 | The DPI level of the main system display is obtained. Only with this DPI level the image is displayed clearly. Displays with another DPI level of changing of the DPI value on the main system display while running the application will cause the image blurring. |
| **PER_MONITOR_AWARE** = SYSTEM_AWARE + 1 | Windows get the DPI level from each display individually. > **Notice:** Not available on Linux. |

### Properties

## 🔒︎ EngineWindowViewport MainWindow

The window viewport that is set as the main window by default.
> **Notice:** There may be several windows that are set as main, or no main windows at all.


## 🔒︎ int NumWindows

The number of windows.
## 🔒︎ bool IsFullscreenMode

The value indicating if the window is the fullscreen state, or in the window mode.
## 🔒︎ bool IsMultipleWindowsSupported

The value indicating if the engine can create more than one window.
## 🔒︎ EngineWindowViewport FocusedWindow

The window viewport which is currently in focus.
## 🔒︎ EngineWindow UnderCursorWindow

The window viewport which is currently under cursor.
## 🔒︎ EngineWindowViewport SystemFocusedWindow

The engine window viewport that has the [IsSystemFocused](../../../api/library/gui/class.enginewindow_cs.md#isSystemFocused_int) flag enabled, either a window itself or its parent group with the system focus is enabled. If there is no window with such a flag, null is returned.
## 🔒︎ bool IsAutoDpiScaling

The value specifying if automatic DPI scaling is applied to the window. If automatic DPI scaling is disabled, all GUI elements have the 100% size, only the system window size is scaled.
> **Notice:** This value is stored in the boot config file and can be changed only at the application startup. It cannot be changed at runtime, thus at an attempt to change the value the console will show the corresponding warning.


## 🔒︎ WindowManager.DPI_AWARENESS DpiAwareness

The DPI awareness mode, the value indicating how the application processes the DPI scaling. The value is set to [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) by default. On Windows, if a specified mode cannot be set, it will switch to a possible lower value with a corresponding warning. On Linux, [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) is currently not supported, setting this value will switch the mode to the [SYSTEM_AWARE](#DPI_AWARENESS_SYSTEM_AWARE) mode with the corresponding warning in the console.
> **Notice:** This value is stored in the boot config file and can be changed only at the application startup. It cannot be changed at runtime, thus at an attempt to change the value the console will show the corresponding warning.


## 🔒︎ WindowManager.DPI_AWARENESS CurrentDpiAwareness

The actual DPI awareness mode, the value indicating how the application processes the DPI scaling. The value is set to [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) by default. On Windows, if a specified mode cannot be set, it will switch to a possible lower value with a corresponding warning. On Linux, [PER_MONITOR_AWARE](#DPI_AWARENESS_PER_MONITOR_AWARE) is currently not supported, setting this value will switch the mode to the [SYSTEM_AWARE](#DPI_AWARENESS_SYSTEM_AWARE) mode with the corresponding warning in the console.
> **Notice:** This is an actual value, it may differ from the mode stored in the boot config file (in case the system cannot set the specified mode it will try to use the one that is suitable instead).


## 🔒︎ Event< WindowEvent > EventImmediateWindowEvent

The event triggered immediately as event from the window is received from proxy before being processed by the engine. This event can be triggered in different threads depending on the proxy implementation. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WindowEvent **event**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ImmediateWindowEvent event handler
void immediatewindowevent_event_handler(WindowEvent event)
{
	Log.Message("\Handling ImmediateWindowEvent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections immediatewindowevent_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager.EventImmediateWindowEvent.Connect(immediatewindowevent_event_connections, immediatewindowevent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager.EventImmediateWindowEvent.Connect(immediatewindowevent_event_connections, (WindowEvent event) => {
		Log.Message("Handling ImmediateWindowEvent event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
immediatewindowevent_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ImmediateWindowEvent event with a handler function
WindowManager.EventImmediateWindowEvent.Connect(immediatewindowevent_event_handler);

// remove subscription to the ImmediateWindowEvent event later by the handler function
WindowManager.EventImmediateWindowEvent.Disconnect(immediatewindowevent_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection immediatewindowevent_event_connection;

// subscribe to the ImmediateWindowEvent event with a lambda handler function and keeping the connection
immediatewindowevent_event_connection = WindowManager.EventImmediateWindowEvent.Connect((WindowEvent event) => {
		Log.Message("Handling ImmediateWindowEvent event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
immediatewindowevent_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
immediatewindowevent_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
immediatewindowevent_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ImmediateWindowEvent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager.EventImmediateWindowEvent.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
WindowManager.EventImmediateWindowEvent.Enabled = true;

```

</details>

## 🔒︎ Event< EngineWindow > EventWindowUnstacked

The event triggered after the window has been unstacked. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(EngineWindow **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the WindowUnstacked event handler
void windowunstacked_event_handler(EngineWindow window)
{
	Log.Message("\Handling WindowUnstacked event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowunstacked_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager.EventWindowUnstacked.Connect(windowunstacked_event_connections, windowunstacked_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager.EventWindowUnstacked.Connect(windowunstacked_event_connections, (EngineWindow window) => {
		Log.Message("Handling WindowUnstacked event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
windowunstacked_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the WindowUnstacked event with a handler function
WindowManager.EventWindowUnstacked.Connect(windowunstacked_event_handler);

// remove subscription to the WindowUnstacked event later by the handler function
WindowManager.EventWindowUnstacked.Disconnect(windowunstacked_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection windowunstacked_event_connection;

// subscribe to the WindowUnstacked event with a lambda handler function and keeping the connection
windowunstacked_event_connection = WindowManager.EventWindowUnstacked.Connect((EngineWindow window) => {
		Log.Message("Handling WindowUnstacked event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
windowunstacked_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
windowunstacked_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
windowunstacked_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring WindowUnstacked events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager.EventWindowUnstacked.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
WindowManager.EventWindowUnstacked.Enabled = true;

```

</details>

## 🔒︎ Event< EngineWindow > EventWindowStacked

The event triggered after the window has been stacked. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(EngineWindow **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the WindowStacked event handler
void windowstacked_event_handler(EngineWindow window)
{
	Log.Message("\Handling WindowStacked event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowstacked_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager.EventWindowStacked.Connect(windowstacked_event_connections, windowstacked_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager.EventWindowStacked.Connect(windowstacked_event_connections, (EngineWindow window) => {
		Log.Message("Handling WindowStacked event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
windowstacked_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the WindowStacked event with a handler function
WindowManager.EventWindowStacked.Connect(windowstacked_event_handler);

// remove subscription to the WindowStacked event later by the handler function
WindowManager.EventWindowStacked.Disconnect(windowstacked_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection windowstacked_event_connection;

// subscribe to the WindowStacked event with a lambda handler function and keeping the connection
windowstacked_event_connection = WindowManager.EventWindowStacked.Connect((EngineWindow window) => {
		Log.Message("Handling WindowStacked event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
windowstacked_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
windowstacked_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
windowstacked_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring WindowStacked events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager.EventWindowStacked.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
WindowManager.EventWindowStacked.Enabled = true;

```

</details>

## 🔒︎ Event< EngineWindow > EventWindowRemoved

The event triggered after the window has been removed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(EngineWindow **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the WindowRemoved event handler
void windowremoved_event_handler(EngineWindow window)
{
	Log.Message("\Handling WindowRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowremoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager.EventWindowRemoved.Connect(windowremoved_event_connections, windowremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager.EventWindowRemoved.Connect(windowremoved_event_connections, (EngineWindow window) => {
		Log.Message("Handling WindowRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
windowremoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the WindowRemoved event with a handler function
WindowManager.EventWindowRemoved.Connect(windowremoved_event_handler);

// remove subscription to the WindowRemoved event later by the handler function
WindowManager.EventWindowRemoved.Disconnect(windowremoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection windowremoved_event_connection;

// subscribe to the WindowRemoved event with a lambda handler function and keeping the connection
windowremoved_event_connection = WindowManager.EventWindowRemoved.Connect((EngineWindow window) => {
		Log.Message("Handling WindowRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
windowremoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
windowremoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
windowremoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring WindowRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager.EventWindowRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
WindowManager.EventWindowRemoved.Enabled = true;

```

</details>

## 🔒︎ Event< EngineWindow > EventWindowCreated

The event triggered after the window has been created. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(EngineWindow **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the WindowCreated event handler
void windowcreated_event_handler(EngineWindow window)
{
	Log.Message("\Handling WindowCreated event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowcreated_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
WindowManager.EventWindowCreated.Connect(windowcreated_event_connections, windowcreated_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
WindowManager.EventWindowCreated.Connect(windowcreated_event_connections, (EngineWindow window) => {
		Log.Message("Handling WindowCreated event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
windowcreated_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the WindowCreated event with a handler function
WindowManager.EventWindowCreated.Connect(windowcreated_event_handler);

// remove subscription to the WindowCreated event later by the handler function
WindowManager.EventWindowCreated.Disconnect(windowcreated_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection windowcreated_event_connection;

// subscribe to the WindowCreated event with a lambda handler function and keeping the connection
windowcreated_event_connection = WindowManager.EventWindowCreated.Connect((EngineWindow window) => {
		Log.Message("Handling WindowCreated event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
windowcreated_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
windowcreated_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
windowcreated_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring WindowCreated events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
WindowManager.EventWindowCreated.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
WindowManager.EventWindowCreated.Enabled = true;

```

</details>

## 🔒︎ EngineWindowViewport FullscreenWindow

The first engine window viewport that is in the fullscreen state.
### Members

---

## EngineWindow GetWindow ( int index )

Returns the window by its index.
### Arguments

- *int* **index** - Index of the window.

### Return value

Engine window.
## int GetWindowIndex ( EngineWindow window )

Returns the index of the specified window.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - Engine window.

### Return value

Index of the window.
## EngineWindowGroup Stack ( EngineWindow first_window , EngineWindow second_window , EngineWindowGroup.GROUP_TYPE group_type , int index = -1 , bool decompose_second = false )

Stacks the window to the other window. If the first argument is the separate window, a new window group is returned. If the first argument is the nested window, the window is added to its group.
```csharp
EngineWindow window_1 = new EngineWindowViewport("Window 1", 512, 256);
EngineWindow window_2 = new EngineWindowViewport("Window 2", 512, 256);
EngineWindow window_3 = new EngineWindowViewport("Window 3", 512, 256);

// create a group of 2 windows
EngineWindowGroup group_1 = WindowManager.Stack(window_1, window_2, EngineWindowGroup.GROUP_TYPE.HORIZONTAL);
// stack a separate window to the window from the window group
WindowManager.Stack(window_1, window_3, EngineWindowGroup.GROUP_TYPE.VERTICAL);


```

 In the result, *group_1* will consist of 3 windows: *window_1* and *window_3* stacked vertically and *window_2* stacked horizontally.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **first_window** - The parent window to which another window is stacked.
- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **second_window** - The window to be stacked.
- *[EngineWindowGroup.GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cs.md#GROUP_TYPE)* **group_type** - Type of a group to be created.
- *int* **index**
- *bool* **decompose_second** - Flag to decompose the second argument of the merge, if it is a group, and combine with the first group.

### Return value

Group of stacked windows.
## EngineWindowGroup StackToParentGroup ( EngineWindow window_in_group , EngineWindow window , int index = -1 , bool decompose_second = false )

Stacks the second window to the parent window group of the first window. In the result, both windows passed as arguments will be on the same level in the group hierarchy. If the first window has no parent group, the function will return it as is.
```csharp
EngineWindowViewport window_1 = new EngineWindowViewport("Window 1", 512, 256);
EngineWindowViewport window_2 = new EngineWindowViewport("Window 2", 512, 256);
EngineWindow window_3 = new EngineWindowViewport("Window 3", 512, 256);

// stack 2 separate windows
EngineWindowGroup group_0 = WindowManager.StackWindows(window_1, window_2, EngineWindowGroup.GROUP_TYPE.HORIZONTAL);
// stack a separate window to the parent group of "window_1"
WindowManager.StackToParentGroup(window_1,window_3);


```


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window_in_group** - The window into the parent group of which the other window is stacked.
- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - The window to be stacked.
- *int* **index** - A place where a window or a group should be placed in a group.
- *bool* **decompose_second** - Flag to decompose the second argument of the merge, if it is a group, and combine with the first window or a group.

### Return value

Group of windows.
## EngineWindowGroup StackWindows ( EngineWindowViewport first_viewport , EngineWindowViewport second_viewport , EngineWindowGroup.GROUP_TYPE group_type = Enum.EngineWindowGroup.GROUP_TYPE.TAB )

Returns a newly created group of the separate and/or nested windows. You cannot stack the window group to the separate window, however, you can stack a window nested in the window group: in this case, the window will be unstacked from its parent group and added to the new one. The windows are stacked in the default order. For example:
```csharp
EngineWindowViewport window_1 = new EngineWindowViewport("Window 1", 512, 256);
EngineWindowViewport window_2 = new EngineWindowViewport("Window 2", 512, 256);
EngineWindowViewport window_3 = new EngineWindowViewport("Window 3", 512, 256);

// stack 2 separate windows
EngineWindow group_0 = WindowManager.StackWindows(window_1, window_2, EngineWindowGroup.GROUP_TYPE.HORIZONTAL);

// stack a window from the window group to a separate window
EngineWindow group_1 = WindowManager.StackWindows(window_3, window_1, EngineWindowGroup.GROUP_TYPE.VERTICAL);


```

 In the result, *group_1* will be a vertical group of *window_3* and *window_1*.
### Arguments

- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* **first_viewport** - The window to be stacked.
- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* **second_viewport** - The window to be stacked.
- *[EngineWindowGroup.GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cs.md#GROUP_TYPE)* **group_type** - Type of a group to be created.

### Return value

Group of windows.
## EngineWindowGroup StackWithWindow ( EngineWindowViewport window_viewport , EngineWindow window , EngineWindowGroup.GROUP_TYPE group_type , bool decompose_second = false )

Returns a newly created group of the engine window viewport and any other engine window � another viewport or a window group.
### Arguments

- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* **window_viewport** - The window viewport to be stacked.
- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - The window to be stacked.
- *[EngineWindowGroup.GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cs.md#GROUP_TYPE)* **group_type** - Type of a window group to be created.
- *bool* **decompose_second** - Flag to decompose the second argument of the merge, if it is a group, and combine with the first group.

### Return value

Group of windows.
## EngineWindowGroup StackGroups ( EngineWindowGroup first_group , EngineWindowGroup second_group , EngineWindowGroup.GROUP_TYPE group_type )

Returns the group of window groups. The second group is added to the first group. To combine two windows or a group and a window, use the *[Stack()](#stack_EngineWindow_EngineWindow_int_int_int_EngineWindowGroup)* method.
```csharp
EngineWindow window_1 = new EngineWindowViewport("Window 1", 512, 256);
EngineWindow window_2 = new EngineWindowViewport("Window 2", 512, 256);
EngineWindow window_3 = new EngineWindowViewport("Window 3", 512, 256);
EngineWindow window_4 = new EngineWindowViewport("Window 4", 512, 256);

// create 2 horizontal groups of windows
EngineWindowGroup group_1 = WindowManager.Stack(window_1, window_2, EngineWindowGroup.GROUP_TYPE.HORIZONTAL);
EngineWindowGroup group_2 = WindowManager.Stack(window_3, window_4, EngineWindowGroup.GROUP_TYPE.HORIZONTAL);
// stack one group to another to create a new vertical group
EngineWindow group_3 = WindowManager.StackGroups(group_1, group_2, EngineWindowGroup.GROUP_TYPE.VERTICAL);


```


### Arguments

- *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cs.md)* **first_group** - The first window group for merging.
- *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cs.md)* **second_group** - The second window group for merging.
- *[EngineWindowGroup.GROUP_TYPE](../../../api/library/gui/class.enginewindowgroup_cs.md#GROUP_TYPE)* **group_type** - Type of a group to be created.

### Return value

Group of windows.
## EngineWindowGroup StackToGroup ( EngineWindowGroup destination_group , EngineWindow group , int index = -1 , bool decompose_second = false )

Stacks the window or window group to another window group. The updated group of windows is returned.
```csharp
EngineWindow window_1 = new EngineWindowViewport("Window 1", 512, 256);
EngineWindow window_2 = new EngineWindowViewport("Window 2", 512, 256);
EngineWindow window_3 = new EngineWindowViewport("Window 3", 512, 256);
EngineWindow window_4 = new EngineWindowViewport("Window 4", 512, 256);

// create 2 horizontal groups of windows
EngineWindowGroup group_1 = WindowManager.Stack(window_1, window_2, EngineWindowGroup.GROUP_TYPE.HORIZONTAL);
EngineWindow group_2 = WindowManager.Stack(window_3, window_4, EngineWindowGroup.GROUP_TYPE.HORIZONTAL);

// stack one group to another
WindowManager.StackToGroup(group_1, group_2);


```


### Arguments

- *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cs.md)* **destination_group** - The parent group to which another group is stacked.
- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **group** - The window or window group to be stacked.
- *int* **index** - A place where a window or a group should be placed in a group.
- *bool* **decompose_second** - Flag to decompose the second argument of the merge and combine with the first group.

### Return value

Group of stacked windows.
## void Unstack ( EngineWindow unstacked )

Removes a window or a group from a parent group. If there is only one window left, the group is automatically deleted after removing the window from it.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **unstacked** - A window or a group to be removed from a parent group.

## bool IsFullscreenWindow ( EngineWindow window )

Returns the value indicating if the specified window is in a fullscreen state.
### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - The window to be checked.

### Return value

true if the engine window is the fullscreen state, false if it is in the window mode.
## EngineWindow GetWindowByID ( ulong win_id )

Returns the window by its ID.
### Arguments

- *ulong* **win_id** - Window ID.

### Return value

Window with the specified ID, or null if the window is not found.
## bool DialogMessage ( string title , string message )

Displays a message dialog with the specified title and text.
### Arguments

- *string* **title** - Title of the message dialog to be displayed.
- *string* **message** - Message text to be displayed.

### Return value

true if the message is displayed successfully; otherwise, false.
## bool DialogWarning ( string title , string warning )

Displays a warning dialog with the specified title and text.
### Arguments

- *string* **title** - Title of the warning dialog to be displayed.
- *string* **warning** - Warning message text to be displayed.

### Return value

true if the message is displayed successfully; otherwise, false.
## bool DialogError ( string title , string error )

Displays an error dialog with the specified title and text.
### Arguments

- *string* **title** - Title of the error dialog to be displayed.
- *string* **error** - Error message text to be displayed.

### Return value

**true** if the message is displayed successfully; otherwise, **false**.
## int ShowSystemDialog ( SystemDialog dialog )

Displays a custom [system dialog](../../../api/library/engine/class.systemdialog_cs.md) with an arbitrary set of buttons.
### Arguments

- *[SystemDialog](../../../api/library/engine/class.systemdialog_cs.md)* **dialog** - [*SystemDialog*](../../../api/library/engine/class.systemdialog_cs.md) class instance representing the custom system dialog to be shown.

### Return value

Number of the dialog button clicked by the user; or **-1** if an error has occurred.
## string DialogOpenFolder ( string path )

Opens a common dialog enabling the user to specify a folder to open. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.

### Return value

Resulting folder name specified by the user.
## string DialogOpenFolder ( )

Opens a common dialog enabling the user to specify a folder to open.
### Return value

Resulting folder name specified by the user.
## string[] DialogOpenFiles ( string path , string filter )

Opens a common dialog enabling the user to specify a list of filenames to open multiple files. When the dialog opens the specified default path and file filter shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.
- *string* **filter** - File name filter string to be set by default when the dialog opens. This filter string determines file type choices to be displayed in the *Files of type* box.

### Return value

Resulting list of filenames specified by the user.
## string[] DialogOpenFiles ( string path )

Opens a common dialog enabling the user to specify a list of filenames to open multiple files. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.

### Return value

Resulting list of filenames specified by the user.
## string[] DialogOpenFiles ( )

Opens a common dialog enabling the user to specify a list of filenames to open multiple files.
### Return value

Resulting list of filenames specified by the user.
## string DialogOpenFile ( string path , string filter )

Opens a common dialog enabling the user to specify a filename to open a file. When the dialog opens the specified default path and file filter shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.
- *string* **filter** - File name filter string to be set by default when the dialog opens. This filter string determines file type choices to be displayed in the *Files of type* box.

### Return value

Resulting filename specified by the user.
## string DialogOpenFile ( string path )

Opens a common dialog enabling the user to specify a filename to open a file. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.

### Return value

Resulting filename specified by the user.
## string DialogOpenFile ( )

Opens a common dialog enabling the user to specify a filename to open a file.
### Return value

Resulting filename specified by the user.
## string DialogSaveFile ( string path , string filter )

Opens a common dialog enabling the user to specify a filename to save a file as. When the dialog opens the specified default path and file filter shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.
- *string* **filter** - File name filter string to be set by default when the dialog opens. This filter string determines file type choices to be displayed in the *Save as file type* or *Files of type* box.

### Return value

Resulting filename specified by the user.
## string DialogSaveFile ( string path )

Opens a common dialog enabling the user to specify a filename to save a file as. When the dialog opens the specified default path shall be set displaying the corresponding elements.
### Arguments

- *string* **path** - Path to be set by default when the dialog opens.

### Return value

Resulting filename specified by the user.
## string DialogSaveFile ( )

Opens a common dialog enabling the user to specify a filename to save a file as.
### Return value

Resulting filename specified by the user.
## EngineWindow GetIntersection ( ivec2 global_pos , EngineWindow [] excludes )

Returns the window the intersection with which is detected.
### Arguments

- *ivec2* **global_pos** - The position of the intersection point in global coordinates.
- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)[]* **excludes** - The windows to be excluded from the intersection detection.

### Return value

The window the intersection with which is detected.
## EngineWindow GetIntersection ( ivec2 global_pos )

Returns the window the intersection with which is detected.
### Arguments

- *ivec2* **global_pos** - The position of the intersection point in global coordinates.

### Return value

The window the intersection with which is detected.
## void ForceUpdateWindowOrders ( )

Updates the Z order of all windows.
> **Notice:** It is recommended to use this method only when required, because it is very slow.


## void SetEventsFilter ( IntPtr func )

Sets a callback function to be executed on receiving input events. This input event filter enables you to reject certain input events for the Engine and get necessary information on all input events.
### Arguments

- *IntPtr* **func** - Input event callback.
