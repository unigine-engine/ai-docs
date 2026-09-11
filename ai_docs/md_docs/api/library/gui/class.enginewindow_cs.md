# Unigine::EngineWindow Class (CS)


This base class operates with engine windows: their components, relations with other windows, size, position, visual representation and other features.


When you create [a window viewport](../../../api/library/gui/class.enginewindowviewport_cs.md) or [a window group](../../../api/library/gui/class.enginewindowgroup_cs.md), the engine window is created.


The image below demonstrates the window components that can be controlled by the EngineWindow class methods.


![Window components](window_structure.png)


To create the engine window, use one of the *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* or *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cs.md)* class constructors. For example:


```csharp
// create an engine window of the specified size with the specified name
EngineWindowViewport window = new EngineWindowViewport("New window", 580, 300);

```


Then, by using methods of the *EngineWindow* class, you can specify the window appearance (for example, set a title, an icon, change opacity, add borders, and so on), and properties (whether the window can be nested, or whether it can become a group), define its style (system or engine), change the window state (whether it is shown/hidden, minimized/maximized, focused, etc.), manage window intersections and events.


### Setting Up Position and Size


In UNIGINE, the window size and position coordinates are measured in both [logical units](../../../principles/dpi/index.md) and pixels:


- The size and position in *units* don't depend on the [DPI scale](#getDpiScale_float) and always remain the same. You can change the window and client area size via **[Size](../../...md#setSize_ivec2_void)**and **[ClientSize](../../...md#setClientSize_ivec2_void)**, adjust the [minimum](#setMinSize_ivec2_void) and [maximum size](#setMaxSize_ivec2_void) and set the window and client position via the corresponding methods. All of them work with units.
- The size and position in *pixels* are calculated by multiplying the size in units by the current [DPI scale](#getDpiScale_float). You can get it using one of the *RenderSize*-related methods/properties (e.g., **[RenderSize](../../...md#getRenderSize_ivec2)**, and so on). When the DPI scale is 100%, *1 unit corresponds to 1 pixel*. > **Notice:** DPI scaling is applied only when the `auto_dpi` flag is enabled. You can check the current flag value via the console or by using **[WindowManager.IsAutoDpiScaling](../../../api/library/gui/class.windowmanager_cs.md#isAutoDpiScaling_int)**. >  To determine how the OS handles the DPI scale, specify the *[DPI awareness mode](../../../api/library/gui/class.windowmanager_cs.md#DPI_AWARENESS)*.


You should consider this information when resizing textures, calculating mouse intersections, etc. The window size and position should be set individually, depending on the situation.


> **Notice:** If necessary, you can convert the size and position coordinates *from units to pixels* and visa versa:
> - Use one of the **[ToRenderSize()](../../...md#toRenderSize_int_int)**or **[ToUnitSize()](../../...md#toUnitSize_int_int)**to convert the size.
> - Use **[GlobalToLocalUnitPosition()](../../...md#globalToLocalUnitPosition_ivec2_ivec2)**to transform the coordinates in pixels into units or **[LocalUnitToGlobalPosition()](../../...md#localUnitToGlobalPosition_ivec2_ivec2)**to do the opposite.


In the following example, the positions of the window and client area (in units) change to the mouse cursor when you press the **P** or **C** respectively:


<details>
<summary>EngineWindowClass.cs</summary>

```csharp
EngineWindowViewport system_viewport;

private void Init()
{

	// create a separate window viewport
	system_viewport = new EngineWindowViewport("Separate System Viewport", 400, 350);
	// specify an intial position
	system_viewport.Position = new ivec2(30, 30);

	// render the window viewport
	system_viewport.Show();

}

private void Update()
{

	// get the current mouse position
	ivec2 mouse_pos = Input.MousePosition;

	// change the window position to the mouse cursor when pressing 'P'
	if (Input.IsKeyDown(Input.KEY.P))
	{

		if (system_viewport.IsDeleted == false)
			system_viewport.Position = mouse_pos;
	}

	// change the client area position to the mouse cursor when pressing 'C'
	if (Input.IsKeyDown(Input.KEY.C))
	{
		if (system_viewport.IsDeleted == false)
			system_viewport.ClientPosition = mouse_pos;
	}

}


```

</details>


### Adjusting Visual Representation


The window visual representation includes all available window parameters such as title and title bar, icon, borders, opacity, and window style (the engine or system one).


Here are some window examples:


<details>
<summary>EngineWindowClass.cs</summary>

```csharp
EngineWindowViewport system_viewport;

EngineWindowViewport system_viewport_borderless;
EngineWindowViewport engine_viewport_borderless;
EngineWindowViewport engine_viewport;

private void Init()
{
	// create a separate system viewport
	system_viewport = new EngineWindowViewport("Window", 200, 200);
	// specify an intial position
	system_viewport.Position = new ivec2(30, 30);

	// specify an intial size
	system_viewport.Size = new ivec2(400, 350);

	// render the window viewport
	system_viewport.Show();

	// create a separate system viewport with borders and title bar disabled
	system_viewport_borderless = new EngineWindowViewport(400, 350);
	system_viewport_borderless.Position = new ivec2(460, 30);
	system_viewport_borderless.Size = new ivec2(400, 350);
	// disable borders
	system_viewport_borderless.BordersEnabled = false;
	// disable a title bar
	system_viewport_borderless.TitleBarEnabled = false;
	system_viewport_borderless.Show();

	// create a separate engine viewport with no borders
	engine_viewport_borderless = new EngineWindowViewport("Window", 400, 350);
	engine_viewport_borderless.Position = new ivec2(460, 30);
	engine_viewport_borderless.EngineStyle = true;
	engine_viewport_borderless.Size = new ivec2(400, 350);
	// disable borders
	engine_viewport_borderless.BordersEnabled = false;
	engine_viewport_borderless.Show();

	// create a separate engine viewport with borders
	engine_viewport = new EngineWindowViewport("Window", 400, 350);
	engine_viewport.Position = new ivec2(460, 30);
	engine_viewport.EngineStyle = true;
	engine_viewport.Size = new ivec2(400, 350);
	engine_viewport.Show();

}


```

</details>


| ![](system_style.jpg) *A system-style window* | ![](borders_bar_disabled.jpg) *A window (either system or engine style),borders and title bar disabled* |
|---|---|
| ![](engine_style_borders_disabled.jpg) *An engine-style window, borders disabled* | ![](engine_style_borders_enabled.jpg) *An engine-style window, borders enabled* |


The *system* and *engine* style windows have the same component layout except the sizing border: in the engine style, it is in the visual part of the window.


The ability to customize the window style makes it possible to create a standard set of window settings for different systems and frameworks.


### Setting Up Order


In the following example, the order of the window under the cursor changes when you press the specific button: **T** to make the window appear on top of all other windows, **A** to always render the window above the other windows.


<details>
<summary>EngineWindowClass.cs</summary>

```csharp
EngineWindow current_window;

EngineWindowViewport system_viewport;

EngineWindowViewport system_viewport_borderless;
EngineWindowViewport engine_viewport_borderless;
EngineWindowViewport engine_viewport;

private void Init()
{
	// create a separate system viewport
	system_viewport = new EngineWindowViewport("Window", 200, 200);
	// specify an intial position
	system_viewport.Position = new ivec2(30, 30);

	// specify an intial size
	system_viewport.Size = new ivec2(400, 350);

	// render the window viewport
	system_viewport.Show();

	// create a separate system viewport with borders and title bar disabled
	system_viewport_borderless = new EngineWindowViewport(400, 350);
	system_viewport_borderless.Position = new ivec2(460, 30);
	system_viewport_borderless.Size = new ivec2(400, 350);
	// disable borders
	system_viewport_borderless.BordersEnabled = false;
	// disable a title bar
	system_viewport_borderless.TitleBarEnabled = false;
	system_viewport_borderless.Show();

	// create a separate engine viewport with no borders
	engine_viewport_borderless = new EngineWindowViewport("Window", 400, 350);
	engine_viewport_borderless.Position = new ivec2(460, 30);
	engine_viewport_borderless.EngineStyle = true;
	engine_viewport_borderless.Size = new ivec2(400, 350);
	// disable borders
	engine_viewport_borderless.BordersEnabled = false;
	engine_viewport_borderless.Show();

	// create a separate engine viewport with borders
	engine_viewport = new EngineWindowViewport("Window", 400, 350);
	engine_viewport.Position = new ivec2(460, 30);
	engine_viewport.EngineStyle = true;
	engine_viewport.Size = new ivec2(400, 350);
	engine_viewport.Show();

}

private void Update()
{

	// get the current mouse position
	ivec2 mouse_pos = Input.MousePosition;

	// make the window under the cursor appear on top when pressing 'T'
	if (Input.IsKeyDown(Input.KEY.T))
	{
		current_window = WindowManager.UnderCursorWindow;
		if (current_window.IsDeleted == false)
			current_window.ToTop();
	}

	// set the window under the cursor to be always on top when pressing 'A'
	if (Input.IsKeyDown(Input.KEY.A))
	{
		current_window = WindowManager.UnderCursorWindow;
		if (current_window.IsDeleted == false)
			current_window.AlwaysOnTop = true;
	}

}


```

</details>


### Changing Behavior


With the set of behavior-related functions, you can do the following:


- Force the engine to [stop operating](#setHoldEngine_int_void) while the engine window is opened.
- Ignore or allow [using the OS methods for windows closing](#setIgnoreSystemClose_int_void).
- Specify whether the window is [resizable](#setResizable_int_void).
- Specify the sizing border size.
- Control rendering of the engine window - [show, hide, focus, minimize, maximize, restore, or close](#show_void).


### Working with Modal Windows


The following example demonstrates how to create modal windows and add modal children to the main window. Additionally, the main window includes a message that informs the user whether they can close the window or not.


<details>
<summary>WindowModal.cs</summary>

```csharp
WidgetLabel label;
EngineWindowViewport main_window;

private void Init()
{
	// main window
	main_window = WindowManager.MainWindow;
	main_window.Size = new ivec2(1600, 900);
	main_window.Position = new ivec2(30, 30);
	main_window.CanBeNested = false;
	main_window.CanCreateGroup = false;

	// add an info label to the main window
	label = new WidgetLabel("");
	label.FontOutline = 1;
	label.Lifetime = Widget.LIFETIME.WINDOW;
	label.FontColor = vec4.RED;
	main_window.AddChild(label, Gui.ALIGN_LEFT);

	// first modal window of the main window
	EngineWindowViewport main_modal_0 = new EngineWindowViewport("Modal for Main 0", 600, 650);
	main_modal_0.Position = new ivec2(50, 250);
	main_modal_0.CanBeNested = false;
	main_modal_0.CanCreateGroup = false;
	main_modal_0.Show();
	main_modal_0.SetModal(main_window);

	// second modal window of the main window
	EngineWindowViewport main_modal_1 = new EngineWindowViewport("Modal for Main 1", 900, 650);
	main_modal_1.Position = new ivec2(700, 250);
	main_modal_1.CanBeNested = false;
	main_modal_1.CanCreateGroup = false;
	main_modal_1.Show();
	main_modal_1.SetModal(main_window);

}

private void Update()
{
	String text = "";

	// check if the modal children of the main window are still opened
	if (main_window.ModalParent == true)
		text += "You CANNOT close this window. Please close modal children first.\n";
	else
		text += "You CAN close this window.\n";

	// render the info label
	label.Text = text;

}


```

</details>


## EngineWindow Class

### Enums

## HITTEST

| Name | Description |
|---|---|
| **INVALID** = -1 | The hittest result is invalid. |
| **NORMAL** = 0 | Client area of the window. |
| **DRAGGABLE** = 1 | Area of the window, by clicking onto which the window can be moved. |
| **RESIZE_TOPLEFT** = 2 | Area of the window that can be dragged to resize the window to the top and/or left direction. |
| **RESIZE_TOP** = 3 | Area of the window that can be dragged to resize the window to the top direction. |
| **RESIZE_TOPRIGHT** = 4 | Area of the window that can be dragged to resize the window to the top and/or right direction. |
| **RESIZE_RIGHT** = 5 | Area of the window that can be dragged to resize the window to the right direction. |
| **RESIZE_BOTTOMRIGHT** = 6 | Area of the window that can be dragged to resize the window to the bottom and/or right direction. |
| **RESIZE_BOTTOM** = 7 | Area of the window that can be dragged to resize the window to the bottom direction. |
| **RESIZE_BOTTOMLEFT** = 8 | Area of the window that can be dragged to resize the window to the bottom and/or left direction. |
| **RESIZE_LEFT** = 9 | Area of the window that can be dragged to resize the window to the left direction. |

## FLAGS

| Name | Description |
|---|---|
| **SHOWN** = 1 << 0 | Window is rendered. |
| **FIXED_SIZE** = 1 << 1 | Window size is fixed. |
| **HOLD_ENGINE** = 1 << 2 | Engine can't stop operating while this window is open. |
| **MAIN** = 1 << 3 | Main window. |
| **CONSOLE_USAGE** = 1 << 4 | Usage of the console for the window is enabled. |
| **PROFILER_USAGE** = 1 << 5 | Usage of the profiler for the window is enabled. |
| **VISUALIZER_USAGE** = 1 << 6 | Usage of the visualizer for the window is enabled. |

## AREA

| Name | Description |
|---|---|
| **NONE** = 0 | None of the areas of the window split into 9 parts is selected. |
| **TOP_LEFT** = 1 | Top left area of the window split into 9 parts. |
| **TOP_CENTER** = 2 | Top center area of the window split into 9 parts. |
| **TOP_RIGHT** = 3 | Top right area of the window split into 9 parts. |
| **CENTER_LEFT** = 4 | Center left area of the window split into 9 parts. |
| **CENTER_CENTER** = 5 | Center area of the window split into 9 parts. |
| **CENTER_RIGHT** = 6 | Center right area of the window split into 9 parts. |
| **BOTTOM_LEFT** = 7 | Bottom left area of the window split into 9 parts. |
| **BOTTOM_CENTER** = 8 | Bottom center area of the window split into 9 parts. |
| **BOTTOM_RIGHT** = 9 | Bottom right area of the window split into 9 parts. |

## TYPE

| Name | Description |
|---|---|
| **ENGINE_WINDOW** = 0 | Engine window. |
| **ENGINE_WINDOW_VIEWPORT** = 1 | Engine viewport window. |
| **ENGINE_WINDOW_GROUP** = 2 | Engine window group. |
| **NUM_ENGINE_WINDOWS** = 3 | Total number of engine windows. |

### Properties

## 🔒︎ Gui Gui

The parent Gui for a window. If the window is nested, this Gui differs from [SelfGui](#getSelfGui_Gui).
## 🔒︎ int DisplayIndex

The number of the display, on which the window is currently displayed. For separate windows, this index is requested from the system proxy; for nested windows, the index is provided based on the location of the client center point.
## 🔒︎ bool IsNested

The value indicating if this is a nested window or group of windows.
## 🔒︎ bool IsSeparate

The value indicating if this is a separate window or group of windows.
## 🔒︎ Gui SelfGui

The Gui instance for a window. This Gui remains unchanged during the whole lifecycle of the window.
## ivec2 Position

The position of the [top left corner](#window_structure) of the window in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## ivec2 ClientPosition

The position of the [top left corner](#window_structure) of the client (the window content area without the top bar and borders) in the screen coordinates (pixels). In case of several displays, the position is relative to the main display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## 🔒︎ ivec2 ClientLocalPosition

The position of the [top left corner](#window_structure) of the client (the window content area without the top bar and borders) relative to the window position in the screen coordinates (pixels).
## ivec2 Size

The engine [window size](#window_structure) in [logical units](../../../principles/dpi/index.md) (including the sizing border).
> **Notice:** This method is for a separate or parent window, using this method for a nested window is not allowed (when requesting the current value, it will return the value of the global parent group).


## ivec2 ClientSize

The size of the window [client (content) area](#window_structure) in [logical units](../../../principles/dpi/index.md).
## ivec2 MinSize

The minimum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is more than the current maximum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current maximum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return zero values).


## ivec2 MaxSize

The maximum possible window size in [logical units](../../../principles/dpi/index.md) when resizing the window. If the value is less than the current minimum size, use the [setMinAndMaxSize()](#setMinAndMaxSize_ivec2_ivec2_void) method, to change both values at once. Otherwise the value will be clamped to the current minimum size.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## string Title

The text of the title for the window. For a separate window, the title is set via system proxy in the title bar only; for a nested window, it is also set in the tab of the parent group.
## float Opacity

The opacity for the window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will always return 1.0f).


## bool BordersEnabled

The value indicating if the borders are enabled for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


## int BorderSize

The engine window border size.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


## bool Resizable

The value indicating if the engine window is resizable by the mouse.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return false).


## 🔒︎ bool IsShown

The value indicating if the engine window is rendered.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


## 🔒︎ bool IsHidden

The value indicating if the engine window isn't rendered.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


## 🔒︎ bool IsFocused

The value indicating if the engine window is in focus.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


## 🔒︎ bool IsMinimized

The value indicating if the engine window is minimized.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


## 🔒︎ bool IsMaximized

The value indicating if the engine window is maximized.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


## 🔒︎ int Order

The order of the window. This value allows comparing which window is closer to the viewer (a relatively smaller value).
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


## 🔒︎ EngineWindowGroup ParentGroup

The group into which the current window is nested, or NULL if it is a separate window.
## 🔒︎ EngineWindowGroup GlobalParentGroup

The top group of the hierarchy into which the current window is nested, or NULL if it is a separate window.
## 🔒︎ int NumDroppedItems

The total number of files and/or folders dropped to the window.
## 🔒︎ int NumModalWindows

The total number of modal windows for this window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return 0.


## 🔒︎ EngineWindow ModalParent

The modal parent of the window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return nullptr.


## 🔒︎ bool IsModalParent

The value indicating if the window is parent for any modal window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return false.


## 🔒︎ bool IsModal

The value indicating if the window is modal. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return false.


## bool IgnoreSystemClose

The value indicating if closing the window using the OS methods is ignored (*ALT+F4* or cross in the top-right corner of the window).
## bool HoldEngine

The value indicating if the engine operation can't be stopped while this window is open.
## 🔒︎ ulong ID

The ID of the engine window, which is unchanged during the whole lifecycle of the window.
## bool AlwaysOnTop

The value indicating if the window is always rendered above the other windows.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return the value of the global parent group).


## 🔒︎ bool IsHiddenByTab

The value indicating if the window is overlapped by any other tab (either by switching to another tab or resizing this window to have zero client area).
## bool CanCreateGroup

The value indicating if the engine window can become a group.
## bool CanBeNested

The value indicating if the engine window can be used as a nested window.
## 🔒︎ bool IsSystemFocused

The value indicating if the engine window is currently in focus.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return the value of the global parent group.


## int SizingBorderSize

The [size of the border](#window_examples) in the widget that is manipulated to resize the window.
> **Notice:** - This method should not be applied to a system-style window with enabled borders, as the system settings cannot be changed (for an unmodified system-style window (i.e. with the enabled border size), the system value is applied).
> - This method should not be applied to nested windows (it will return 0).


## bool EngineStyle

The value indicating if the [engine style](#window_examples) or the default system style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


## bool SystemStyle

The value indicating if the default [system style](#window_examples) or the engine style is set for the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return true).


## int TitleBarHeight

The height of the window title bar.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method can be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


## bool TitleBarEnabled

The value indicating if the title bar is enabled for the engine window.
> **Notice:** - This value is applied to the windows in the [engine style](#isEngineStyle_int) only. For system-style windows system settings are applied.
> - This method should be applied to a separate or parent window, using this method for a nested window is not allowed (it will return 0).


## 🔒︎ string TypeName

The name of the engine window type as a string.
## 🔒︎ EngineWindow.TYPE Type

The type of the engine window.
## 🔒︎ float DpiScale

The DPI scale applied to the elements inside the window.
## 🔒︎ int Dpi

The DPI level for the window.
## 🔒︎ ivec2 MaxRenderSize

The maximum window size in pixels.
## 🔒︎ ivec2 MinRenderSize

The minimum window size in pixels.
## 🔒︎ ivec2 ClientRenderSize

The client area size in pixels.
## 🔒︎ ivec2 RenderSize

The engine window frame size in pixels.
## 🔒︎ Event EventUnstack

The event triggered when when the window is unstacked. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Unstack event handler
void unstack_event_handler()
{
	Log.Message("\Handling Unstack event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections unstack_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventUnstack.Connect(unstack_event_connections, unstack_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventUnstack.Connect(unstack_event_connections, () => {
		Log.Message("Handling Unstack event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
unstack_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Unstack event with a handler function
publisher.EventUnstack.Connect(unstack_event_handler);

// remove subscription to the Unstack event later by the handler function
publisher.EventUnstack.Disconnect(unstack_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection unstack_event_connection;

// subscribe to the Unstack event with a lambda handler function and keeping the connection
unstack_event_connection = publisher.EventUnstack.Connect(() => {
		Log.Message("Handling Unstack event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
unstack_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
unstack_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
unstack_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Unstack events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventUnstack.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventUnstack.Enabled = true;

```

</details>

## 🔒︎ Event EventStack

The event triggered when the window is stacked. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Stack event handler
void stack_event_handler()
{
	Log.Message("\Handling Stack event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections stack_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventStack.Connect(stack_event_connections, stack_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventStack.Connect(stack_event_connections, () => {
		Log.Message("Handling Stack event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
stack_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Stack event with a handler function
publisher.EventStack.Connect(stack_event_handler);

// remove subscription to the Stack event later by the handler function
publisher.EventStack.Disconnect(stack_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection stack_event_connection;

// subscribe to the Stack event with a lambda handler function and keeping the connection
stack_event_connection = publisher.EventStack.Connect(() => {
		Log.Message("Handling Stack event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
stack_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
stack_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
stack_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Stack events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventStack.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventStack.Enabled = true;

```

</details>

## 🔒︎ Event< EngineWindow > EventUnstackMove

The event triggered when the window is unstacked and moved. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(EngineWindow **window**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the UnstackMove event handler
void unstackmove_event_handler(EngineWindow window)
{
	Log.Message("\Handling UnstackMove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections unstackmove_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventUnstackMove.Connect(unstackmove_event_connections, unstackmove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventUnstackMove.Connect(unstackmove_event_connections, (EngineWindow window) => {
		Log.Message("Handling UnstackMove event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
unstackmove_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the UnstackMove event with a handler function
publisher.EventUnstackMove.Connect(unstackmove_event_handler);

// remove subscription to the UnstackMove event later by the handler function
publisher.EventUnstackMove.Disconnect(unstackmove_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection unstackmove_event_connection;

// subscribe to the UnstackMove event with a lambda handler function and keeping the connection
unstackmove_event_connection = publisher.EventUnstackMove.Connect((EngineWindow window) => {
		Log.Message("Handling UnstackMove event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
unstackmove_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
unstackmove_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
unstackmove_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring UnstackMove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventUnstackMove.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventUnstackMove.Enabled = true;

```

</details>

## 🔒︎ Event<string> EventItemDrop

The event triggered when an item is dropped to the window. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **item**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ItemDrop event handler
void itemdrop_event_handler(string item)
{
	Log.Message("\Handling ItemDrop event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections itemdrop_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventItemDrop.Connect(itemdrop_event_connections, itemdrop_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventItemDrop.Connect(itemdrop_event_connections, (string item) => {
		Log.Message("Handling ItemDrop event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
itemdrop_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ItemDrop event with a handler function
publisher.EventItemDrop.Connect(itemdrop_event_handler);

// remove subscription to the ItemDrop event later by the handler function
publisher.EventItemDrop.Disconnect(itemdrop_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection itemdrop_event_connection;

// subscribe to the ItemDrop event with a lambda handler function and keeping the connection
itemdrop_event_connection = publisher.EventItemDrop.Connect((string item) => {
		Log.Message("Handling ItemDrop event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
itemdrop_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
itemdrop_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
itemdrop_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ItemDrop events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventItemDrop.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventItemDrop.Enabled = true;

```

</details>

## 🔒︎ Event EventClose

The event triggered when the window is closed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Close event handler
void close_event_handler()
{
	Log.Message("\Handling Close event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections close_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventClose.Connect(close_event_connections, close_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventClose.Connect(close_event_connections, () => {
		Log.Message("Handling Close event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
close_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Close event with a handler function
publisher.EventClose.Connect(close_event_handler);

// remove subscription to the Close event later by the handler function
publisher.EventClose.Disconnect(close_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection close_event_connection;

// subscribe to the Close event with a lambda handler function and keeping the connection
close_event_connection = publisher.EventClose.Connect(() => {
		Log.Message("Handling Close event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
close_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
close_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
close_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Close events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventClose.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventClose.Enabled = true;

```

</details>

## 🔒︎ Event EventRestored

The event triggered when the window is restored. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Restored event handler
void restored_event_handler()
{
	Log.Message("\Handling Restored event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections restored_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventRestored.Connect(restored_event_connections, restored_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventRestored.Connect(restored_event_connections, () => {
		Log.Message("Handling Restored event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
restored_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Restored event with a handler function
publisher.EventRestored.Connect(restored_event_handler);

// remove subscription to the Restored event later by the handler function
publisher.EventRestored.Disconnect(restored_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection restored_event_connection;

// subscribe to the Restored event with a lambda handler function and keeping the connection
restored_event_connection = publisher.EventRestored.Connect(() => {
		Log.Message("Handling Restored event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
restored_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
restored_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
restored_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Restored events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventRestored.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventRestored.Enabled = true;

```

</details>

## 🔒︎ Event EventMaximized

The event triggered when the window is maximized. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Maximized event handler
void maximized_event_handler()
{
	Log.Message("\Handling Maximized event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections maximized_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventMaximized.Connect(maximized_event_connections, maximized_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventMaximized.Connect(maximized_event_connections, () => {
		Log.Message("Handling Maximized event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
maximized_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Maximized event with a handler function
publisher.EventMaximized.Connect(maximized_event_handler);

// remove subscription to the Maximized event later by the handler function
publisher.EventMaximized.Disconnect(maximized_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection maximized_event_connection;

// subscribe to the Maximized event with a lambda handler function and keeping the connection
maximized_event_connection = publisher.EventMaximized.Connect(() => {
		Log.Message("Handling Maximized event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
maximized_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
maximized_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
maximized_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Maximized events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventMaximized.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventMaximized.Enabled = true;

```

</details>

## 🔒︎ Event EventMinimized

The event triggered when the window is minimized. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Minimized event handler
void minimized_event_handler()
{
	Log.Message("\Handling Minimized event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections minimized_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventMinimized.Connect(minimized_event_connections, minimized_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventMinimized.Connect(minimized_event_connections, () => {
		Log.Message("Handling Minimized event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
minimized_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Minimized event with a handler function
publisher.EventMinimized.Connect(minimized_event_handler);

// remove subscription to the Minimized event later by the handler function
publisher.EventMinimized.Disconnect(minimized_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection minimized_event_connection;

// subscribe to the Minimized event with a lambda handler function and keeping the connection
minimized_event_connection = publisher.EventMinimized.Connect(() => {
		Log.Message("Handling Minimized event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
minimized_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
minimized_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
minimized_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Minimized events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventMinimized.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventMinimized.Enabled = true;

```

</details>

## 🔒︎ Event EventHidden

The event triggered when the window is hidden. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Hidden event handler
void hidden_event_handler()
{
	Log.Message("\Handling Hidden event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections hidden_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventHidden.Connect(hidden_event_connections, hidden_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventHidden.Connect(hidden_event_connections, () => {
		Log.Message("Handling Hidden event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
hidden_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Hidden event with a handler function
publisher.EventHidden.Connect(hidden_event_handler);

// remove subscription to the Hidden event later by the handler function
publisher.EventHidden.Disconnect(hidden_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection hidden_event_connection;

// subscribe to the Hidden event with a lambda handler function and keeping the connection
hidden_event_connection = publisher.EventHidden.Connect(() => {
		Log.Message("Handling Hidden event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
hidden_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
hidden_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
hidden_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Hidden events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventHidden.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventHidden.Enabled = true;

```

</details>

## 🔒︎ Event EventShown

The event triggered when the window is shown. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Shown event handler
void shown_event_handler()
{
	Log.Message("\Handling Shown event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections shown_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventShown.Connect(shown_event_connections, shown_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventShown.Connect(shown_event_connections, () => {
		Log.Message("Handling Shown event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
shown_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Shown event with a handler function
publisher.EventShown.Connect(shown_event_handler);

// remove subscription to the Shown event later by the handler function
publisher.EventShown.Disconnect(shown_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection shown_event_connection;

// subscribe to the Shown event with a lambda handler function and keeping the connection
shown_event_connection = publisher.EventShown.Connect(() => {
		Log.Message("Handling Shown event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
shown_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
shown_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
shown_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Shown events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventShown.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventShown.Enabled = true;

```

</details>

## 🔒︎ Event EventMouseLeave

The event triggered when the mouse leaves the window area. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the MouseLeave event handler
void mouseleave_event_handler()
{
	Log.Message("\Handling MouseLeave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mouseleave_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventMouseLeave.Connect(mouseleave_event_connections, mouseleave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventMouseLeave.Connect(mouseleave_event_connections, () => {
		Log.Message("Handling MouseLeave event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
mouseleave_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the MouseLeave event with a handler function
publisher.EventMouseLeave.Connect(mouseleave_event_handler);

// remove subscription to the MouseLeave event later by the handler function
publisher.EventMouseLeave.Disconnect(mouseleave_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection mouseleave_event_connection;

// subscribe to the MouseLeave event with a lambda handler function and keeping the connection
mouseleave_event_connection = publisher.EventMouseLeave.Connect(() => {
		Log.Message("Handling MouseLeave event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
mouseleave_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
mouseleave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
mouseleave_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring MouseLeave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventMouseLeave.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventMouseLeave.Enabled = true;

```

</details>

## 🔒︎ Event EventMouseEnter

The event triggered when the mouse enters the window area. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the MouseEnter event handler
void mouseenter_event_handler()
{
	Log.Message("\Handling MouseEnter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections mouseenter_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventMouseEnter.Connect(mouseenter_event_connections, mouseenter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventMouseEnter.Connect(mouseenter_event_connections, () => {
		Log.Message("Handling MouseEnter event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
mouseenter_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the MouseEnter event with a handler function
publisher.EventMouseEnter.Connect(mouseenter_event_handler);

// remove subscription to the MouseEnter event later by the handler function
publisher.EventMouseEnter.Disconnect(mouseenter_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection mouseenter_event_connection;

// subscribe to the MouseEnter event with a lambda handler function and keeping the connection
mouseenter_event_connection = publisher.EventMouseEnter.Connect(() => {
		Log.Message("Handling MouseEnter event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
mouseenter_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
mouseenter_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
mouseenter_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring MouseEnter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventMouseEnter.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventMouseEnter.Enabled = true;

```

</details>

## 🔒︎ Event EventUnfocused

The event triggered when the window loses the focus. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Unfocused event handler
void unfocused_event_handler()
{
	Log.Message("\Handling Unfocused event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections unfocused_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventUnfocused.Connect(unfocused_event_connections, unfocused_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventUnfocused.Connect(unfocused_event_connections, () => {
		Log.Message("Handling Unfocused event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
unfocused_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Unfocused event with a handler function
publisher.EventUnfocused.Connect(unfocused_event_handler);

// remove subscription to the Unfocused event later by the handler function
publisher.EventUnfocused.Disconnect(unfocused_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection unfocused_event_connection;

// subscribe to the Unfocused event with a lambda handler function and keeping the connection
unfocused_event_connection = publisher.EventUnfocused.Connect(() => {
		Log.Message("Handling Unfocused event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
unfocused_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
unfocused_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
unfocused_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Unfocused events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventUnfocused.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventUnfocused.Enabled = true;

```

</details>

## 🔒︎ Event EventFocused

The event triggered when the window gains the focus. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Focused event handler
void focused_event_handler()
{
	Log.Message("\Handling Focused event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focused_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFocused.Connect(focused_event_connections, focused_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFocused.Connect(focused_event_connections, () => {
		Log.Message("Handling Focused event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
focused_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Focused event with a handler function
publisher.EventFocused.Connect(focused_event_handler);

// remove subscription to the Focused event later by the handler function
publisher.EventFocused.Disconnect(focused_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection focused_event_connection;

// subscribe to the Focused event with a lambda handler function and keeping the connection
focused_event_connection = publisher.EventFocused.Connect(() => {
		Log.Message("Handling Focused event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
focused_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
focused_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
focused_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Focused events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFocused.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFocused.Enabled = true;

```

</details>

## 🔒︎ Event<ivec2> EventResized

The event triggered when the window is resized. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ivec2 **new_size**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Resized event handler
void resized_event_handler(ivec2 new_size)
{
	Log.Message("\Handling Resized event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections resized_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventResized.Connect(resized_event_connections, resized_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventResized.Connect(resized_event_connections, (ivec2 new_size) => {
		Log.Message("Handling Resized event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
resized_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Resized event with a handler function
publisher.EventResized.Connect(resized_event_handler);

// remove subscription to the Resized event later by the handler function
publisher.EventResized.Disconnect(resized_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection resized_event_connection;

// subscribe to the Resized event with a lambda handler function and keeping the connection
resized_event_connection = publisher.EventResized.Connect((ivec2 new_size) => {
		Log.Message("Handling Resized event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
resized_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
resized_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
resized_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Resized events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventResized.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventResized.Enabled = true;

```

</details>

## 🔒︎ Event<ivec2> EventMoved

The event triggered when the window is moved. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ivec2 **new_coords**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Moved event handler
void moved_event_handler(ivec2 new_coords)
{
	Log.Message("\Handling Moved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections moved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventMoved.Connect(moved_event_connections, moved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventMoved.Connect(moved_event_connections, (ivec2 new_coords) => {
		Log.Message("Handling Moved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
moved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Moved event with a handler function
publisher.EventMoved.Connect(moved_event_handler);

// remove subscription to the Moved event later by the handler function
publisher.EventMoved.Disconnect(moved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection moved_event_connection;

// subscribe to the Moved event with a lambda handler function and keeping the connection
moved_event_connection = publisher.EventMoved.Connect((ivec2 new_coords) => {
		Log.Message("Handling Moved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
moved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
moved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
moved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Moved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventMoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventMoved.Enabled = true;

```

</details>

## 🔒︎ Event EventFuncSwap

The event triggered before calling the window swap. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FuncSwap event handler
void funcswap_event_handler()
{
	Log.Message("\Handling FuncSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcswap_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFuncSwap.Connect(funcswap_event_connections, funcswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFuncSwap.Connect(funcswap_event_connections, () => {
		Log.Message("Handling FuncSwap event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
funcswap_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FuncSwap event with a handler function
publisher.EventFuncSwap.Connect(funcswap_event_handler);

// remove subscription to the FuncSwap event later by the handler function
publisher.EventFuncSwap.Disconnect(funcswap_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection funcswap_event_connection;

// subscribe to the FuncSwap event with a lambda handler function and keeping the connection
funcswap_event_connection = publisher.EventFuncSwap.Connect(() => {
		Log.Message("Handling FuncSwap event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
funcswap_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
funcswap_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
funcswap_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FuncSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFuncSwap.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFuncSwap.Enabled = true;

```

</details>

## 🔒︎ Event EventFuncEndRender

The event triggered after the window rendering has ended. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FuncEndRender event handler
void funcendrender_event_handler()
{
	Log.Message("\Handling FuncEndRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcendrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFuncEndRender.Connect(funcendrender_event_connections, funcendrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFuncEndRender.Connect(funcendrender_event_connections, () => {
		Log.Message("Handling FuncEndRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
funcendrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FuncEndRender event with a handler function
publisher.EventFuncEndRender.Connect(funcendrender_event_handler);

// remove subscription to the FuncEndRender event later by the handler function
publisher.EventFuncEndRender.Disconnect(funcendrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection funcendrender_event_connection;

// subscribe to the FuncEndRender event with a lambda handler function and keeping the connection
funcendrender_event_connection = publisher.EventFuncEndRender.Connect(() => {
		Log.Message("Handling FuncEndRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
funcendrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
funcendrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
funcendrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FuncEndRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFuncEndRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFuncEndRender.Enabled = true;

```

</details>

## 🔒︎ Event< Gui > EventFuncEndRenderGui

The event triggered after the GUI rendering has ended. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Gui **gui**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FuncEndRenderGui event handler
void funcendrendergui_event_handler(Gui gui)
{
	Log.Message("\Handling FuncEndRenderGui event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcendrendergui_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFuncEndRenderGui.Connect(funcendrendergui_event_connections, funcendrendergui_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFuncEndRenderGui.Connect(funcendrendergui_event_connections, (Gui gui) => {
		Log.Message("Handling FuncEndRenderGui event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
funcendrendergui_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FuncEndRenderGui event with a handler function
publisher.EventFuncEndRenderGui.Connect(funcendrendergui_event_handler);

// remove subscription to the FuncEndRenderGui event later by the handler function
publisher.EventFuncEndRenderGui.Disconnect(funcendrendergui_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection funcendrendergui_event_connection;

// subscribe to the FuncEndRenderGui event with a lambda handler function and keeping the connection
funcendrendergui_event_connection = publisher.EventFuncEndRenderGui.Connect((Gui gui) => {
		Log.Message("Handling FuncEndRenderGui event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
funcendrendergui_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
funcendrendergui_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
funcendrendergui_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FuncEndRenderGui events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFuncEndRenderGui.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFuncEndRenderGui.Enabled = true;

```

</details>

## 🔒︎ Event< Gui > EventFuncBeginRenderGui

The event triggered when the GUI rendering has begun. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Gui **gui**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FuncBeginRenderGui event handler
void funcbeginrendergui_event_handler(Gui gui)
{
	Log.Message("\Handling FuncBeginRenderGui event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcbeginrendergui_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFuncBeginRenderGui.Connect(funcbeginrendergui_event_connections, funcbeginrendergui_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFuncBeginRenderGui.Connect(funcbeginrendergui_event_connections, (Gui gui) => {
		Log.Message("Handling FuncBeginRenderGui event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
funcbeginrendergui_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FuncBeginRenderGui event with a handler function
publisher.EventFuncBeginRenderGui.Connect(funcbeginrendergui_event_handler);

// remove subscription to the FuncBeginRenderGui event later by the handler function
publisher.EventFuncBeginRenderGui.Disconnect(funcbeginrendergui_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection funcbeginrendergui_event_connection;

// subscribe to the FuncBeginRenderGui event with a lambda handler function and keeping the connection
funcbeginrendergui_event_connection = publisher.EventFuncBeginRenderGui.Connect((Gui gui) => {
		Log.Message("Handling FuncBeginRenderGui event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
funcbeginrendergui_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
funcbeginrendergui_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
funcbeginrendergui_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FuncBeginRenderGui events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFuncBeginRenderGui.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFuncBeginRenderGui.Enabled = true;

```

</details>

## 🔒︎ Event EventFuncRender

The event triggered after the window rendering function. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FuncRender event handler
void funcrender_event_handler()
{
	Log.Message("\Handling FuncRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFuncRender.Connect(funcrender_event_connections, funcrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFuncRender.Connect(funcrender_event_connections, () => {
		Log.Message("Handling FuncRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
funcrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FuncRender event with a handler function
publisher.EventFuncRender.Connect(funcrender_event_handler);

// remove subscription to the FuncRender event later by the handler function
publisher.EventFuncRender.Disconnect(funcrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection funcrender_event_connection;

// subscribe to the FuncRender event with a lambda handler function and keeping the connection
funcrender_event_connection = publisher.EventFuncRender.Connect(() => {
		Log.Message("Handling FuncRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
funcrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
funcrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
funcrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FuncRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFuncRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFuncRender.Enabled = true;

```

</details>

## 🔒︎ Event EventFuncBeginRender

The event triggered when the window rendering has begun. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FuncBeginRender event handler
void funcbeginrender_event_handler()
{
	Log.Message("\Handling FuncBeginRender event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcbeginrender_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFuncBeginRender.Connect(funcbeginrender_event_connections, funcbeginrender_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFuncBeginRender.Connect(funcbeginrender_event_connections, () => {
		Log.Message("Handling FuncBeginRender event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
funcbeginrender_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FuncBeginRender event with a handler function
publisher.EventFuncBeginRender.Connect(funcbeginrender_event_handler);

// remove subscription to the FuncBeginRender event later by the handler function
publisher.EventFuncBeginRender.Disconnect(funcbeginrender_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection funcbeginrender_event_connection;

// subscribe to the FuncBeginRender event with a lambda handler function and keeping the connection
funcbeginrender_event_connection = publisher.EventFuncBeginRender.Connect(() => {
		Log.Message("Handling FuncBeginRender event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
funcbeginrender_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
funcbeginrender_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
funcbeginrender_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FuncBeginRender events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFuncBeginRender.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFuncBeginRender.Enabled = true;

```

</details>

## 🔒︎ Event EventFuncUpdate

The event triggered after the window update. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FuncUpdate event handler
void funcupdate_event_handler()
{
	Log.Message("\Handling FuncUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections funcupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFuncUpdate.Connect(funcupdate_event_connections, funcupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFuncUpdate.Connect(funcupdate_event_connections, () => {
		Log.Message("Handling FuncUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
funcupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FuncUpdate event with a handler function
publisher.EventFuncUpdate.Connect(funcupdate_event_handler);

// remove subscription to the FuncUpdate event later by the handler function
publisher.EventFuncUpdate.Disconnect(funcupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection funcupdate_event_connection;

// subscribe to the FuncUpdate event with a lambda handler function and keeping the connection
funcupdate_event_connection = publisher.EventFuncUpdate.Connect(() => {
		Log.Message("Handling FuncUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
funcupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
funcupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
funcupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FuncUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFuncUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFuncUpdate.Enabled = true;

```

</details>

## 🔒︎ Event< WindowEvent > EventWindowEvent

The event triggered on the window event. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WindowEvent **event**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the WindowEvent event handler
void windowevent_event_handler(WindowEvent event)
{
	Log.Message("\Handling WindowEvent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections windowevent_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventWindowEvent.Connect(windowevent_event_connections, windowevent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventWindowEvent.Connect(windowevent_event_connections, (WindowEvent event) => {
		Log.Message("Handling WindowEvent event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
windowevent_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the WindowEvent event with a handler function
publisher.EventWindowEvent.Connect(windowevent_event_handler);

// remove subscription to the WindowEvent event later by the handler function
publisher.EventWindowEvent.Disconnect(windowevent_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection windowevent_event_connection;

// subscribe to the WindowEvent event with a lambda handler function and keeping the connection
windowevent_event_connection = publisher.EventWindowEvent.Connect((WindowEvent event) => {
		Log.Message("Handling WindowEvent event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
windowevent_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
windowevent_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
windowevent_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring WindowEvent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventWindowEvent.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventWindowEvent.Enabled = true;

```

</details>

### Members

---

## void MoveToCenter ( )

Positions the window so that the client center coincides with the center of the current display.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void SetMinAndMaxSize ( ivec2 min_size , ivec2 max_size )

Sets the minimum and maximum possible window size when resizing the window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *ivec2* **min_size** - The minimum possible size of the window.
- *ivec2* **max_size** - The maximum possible size of the window.

## int SetIcon ( Image image )

Sets the icon for the window.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - The icon for the window.

### Return value

1 if the specified icon is successfully set for the window, otherwise 0.
## int GetIcon ( Image image )

Gets the icon for the engine window and puts it to the specified target Image.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Target image for the window icon.

### Return value

1 if the icon for the window is returned successfully, otherwise 0.
## void Show ( )

Enables rendering of the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void Hide ( )

Disables rendering of the engine window.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void SetFocus ( )

Sets the focus to the window.
## void SetSystemFocus ( )

Sets the focus to the engine window.
> **Notice:** This method is applied to a separate or parent window, for nested windows use [setFocus()](#setFocus_void).


## void Minimize ( )

Minimizes the engine window to an iconic representation.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void Maximize ( )

Makes the engine window as large as possible.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## void Restore ( )

Restores the size and position of the minimized or maximized engine window via the system proxy.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## EngineWindow.HITTEST GetHitTestResult ( ivec2 global_pos )

Returns a value indicating in which area of the engine window the mouse is located.
> **Notice:** This method is used for interaction with system windows only, i.e. it cannot be used for nested windows.


### Arguments

- *ivec2* **global_pos** - Global coordinates of the hit-test point.

### Return value

Value indicating the window area, one of the [HITTEST.*](#HITTEST) values.
## string GetHitTestResultName ( EngineWindow.HITTEST hit_test )

Returns the string representation of the hit test result value.
### Arguments

- *[EngineWindow.HITTEST](../../../api/library/gui/class.enginewindow_cs.md#HITTEST)* **hit_test** - Value indicating the window area, one of the [HITTEST.*](#HITTEST) values.

### Return value

The string representation of the hit test result value (e.g., HITTEST_RESIZE_RIGHT is RESIZE RIGHT).
## void ToTop ( )

Makes the window appear on top of all other windows.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


## bool IsGlobalChildOf ( EngineWindowGroup group )

Returns the value specifying if the current window is a part of a hierarchy of the specified window.
### Arguments

- *[EngineWindowGroup](../../../api/library/gui/class.enginewindowgroup_cs.md)* **group** - Window to be checked.

### Return value

true if the current window is globally a child of the specified one, otherwise false.
## void UpdateGuiHierarchy ( )

Updates the hierarchy for all widgets � the widgets are arranged, expanded to the required sizes and then their positions are updated. Updating the hierarchy may be required, for example, for getting the screen position immediately after the widget has been added to the hierarchy. For a separate window, the hierarchy in [self gui](#getSelfGui_Gui) is updated; for a nested window, the hierarchy in [self gui](#getSelfGui_Gui) of the global parent group is updated.
## string GetDroppedItem ( int index )

Returns the absolute path to the file or folder dropped to the window.
### Arguments

- *int* **index** - Index of the dropped file or folder.

### Return value

Absolute path to the dropped file or folder.
## void Screenshot ( string path )

Creates a screenshot after the rendering stage is completed.
> **Notice:** This method should be applied to a separate or parent window, using this method for a nested window is not allowed.


### Arguments

- *string* **path** - Path to save the screenshot.

## void SetModal ( EngineWindow parent_window )

Sets the current window modal to the specified parent window. Both the parent and the child windows must be separate. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, a nested window can't be a parent for a modal window.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **parent_window** - Parent window.

## void AddModalWindow ( EngineWindow window )

Adds the argument window as modal to the current window. Both the parent and the child windows must be separate. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, a nested window can't be a parent for a modal window.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - Window to be added as modal.

## void RemoveModalWindow ( EngineWindow window )

Removes the argument modal window from this window. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, a nested window can't be a parent for a modal window.


### Arguments

- *[EngineWindow](../../../api/library/gui/class.enginewindow_cs.md)* **window** - Engine window.

## EngineWindow GetModalWindow ( int index )

Returns the modal window for this window by its index. The concept of **modal** assumes that if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.
> **Notice:** This method should be applied to a separate or parent window, for a nested window it will return nullptr.


### Arguments

- *int* **index** - Index of the modal window.

### Return value

Modal window.
## void Unstack ( )

Removes the current window from a parent group.
## void Close ( )

Deletes the window if this window is not a [modal parent](#getModalParent_EngineWindow) or a member of a [fixed group](../../../api/library/gui/class.enginewindowgroup_cs.md#isFixed_int). If a window is a member of a fixed group, it cannot be closed (i.e. deleted).
## bool GetIntersection ( ivec2 global_mouse_pos )

Returns the value indicating if the mouse is hovering over the window.
### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

true if the mouse hovers over the current window, otherwise false.
## bool GetClientIntersection ( ivec2 global_mouse_pos )

Returns the value indicating if the mouse is hovering over the client area of the window.
```csharp
//checks if the mouse is hovering over the main window
EngineWindow main_window = WindowManager.MainWindow;
main_window.GetClientIntersection(Input.MousePosition);


```


### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

true if the mouse hovers over the client area of the window, otherwise false.
## EngineWindow.AREA GetClient9Area ( ivec2 global_mouse_pos )

Returns the area over which the mouse hovers, one of the nine areas into which the window is segmented.
### Arguments

- *ivec2* **global_mouse_pos** - Global screen coordinates of the mouse relative to the main display.

### Return value

One of the nine segments the screen area is split into.
## string Get9AreaName ( EngineWindow.AREA area )

Returns the name of the screen segment as a string.
### Arguments

- *[EngineWindow.AREA](../../../api/library/gui/class.enginewindow_cs.md#AREA)* **area** - One of the nine segments the screen area is split into.

### Return value

The string representation of the segment value (e.g., AREA_TOP_LEFT is TOP LEFT).
## ivec2 GlobalToLocalUnitPosition ( ivec2 global_pos )

Transforms the global screen coordinates in pixels into [logical units](../../../principles/dpi/index.md) relative to the window client area.
### Arguments

- *ivec2* **global_pos** - The position in global coordinates.

### Return value

The coordinates in [logical units](../../../principles/dpi/index.md) relative to the window client area.
## ivec2 LocalUnitToGlobalPosition ( ivec2 unit_pos )

Transforms the position in [logical units](../../../principles/dpi/index.md) relative to the window client area into the global screen coordinates in pixels.
### Arguments

- *ivec2* **unit_pos** - The coordinates in [logical units](../../../principles/dpi/index.md) relative to the window client area.

### Return value

The position in global coordinates.
## int ToRenderSize ( int unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *int* **unit_size** - Size in [logical units](../../../principles/dpi/index.md).

### Return value

Size in pixels.
## int ToUnitSize ( int render_size )

Transforms the pixel value to the unit value.
### Arguments

- *int* **render_size** - Size in pixels.

### Return value

Size in [logical units](../../../principles/dpi/index.md).
## ivec2 ToRenderSize ( ivec2 unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *ivec2* **unit_size** - Size in [logical units](../../../principles/dpi/index.md).

### Return value

Size in pixels.
## ivec2 ToUnitSize ( ivec2 render_size )

Transforms the pixel value to the unit value.
### Arguments

- *ivec2* **render_size** - Size in pixels.

### Return value

Size in [logical units](../../../principles/dpi/index.md).
