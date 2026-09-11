# Window Management (CS)


UNIGINE provides an advanced toolkit simplifying development of various visual tools, with a large number of widgets and capabilities.


You can easily create and adjust window viewports and window groups, control their behavior and rendering order, stack them, handle events, check window intersections, and so on via API:


- All window management operations are performed via the *[WindowManager](../../api/library/gui/class.windowmanager_cs.md)* class, enabling you to access any application window, group or stack windows, create various dialogs, and so on.
- Window components, relations with other windows, size, position, order, window events and intersections are managed by the base *[EngineWindow](../../api/library/gui/class.enginewindow_cs.md)* class.
- For window viewport creation, the *[EngineWindowViewport](../../api/library/gui/class.enginewindowviewport_cs.md)* class is used. It inherits from *[EngineWindow](../../api/library/gui/class.enginewindow_cs.md)* class and allows managing window viewports: setting cameras, specifying engine tools available (console, profiler, visualizer, etc.), adding widgets to the client area.
- For window groups, there is the *[EngineWindowGroup](../../api/library/gui/class.enginewindowgroup_cs.md)* class. It also inherits from *[EngineWindow](../../api/library/gui/class.enginewindow_cs.md)* class and allows implementing custom grouping logic.


> **Notice:** - Both a window viewport and a window group are **engine windows**.
> - Usually the engine windows stay available during the whole UNIGINE Engine runtime, so their creation and management should be implemented as a part of the [System Logic](../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic).


## Creating a Window Viewport


To create the engine window viewport, one of the *EngineWindowViewport* class constructors is used.


```csharp
// create an engine window of the specified size with the specified name
EngineWindowViewport window = new EngineWindowViewport("Window", 580, 300);


```


When the window viewport is created, you can change its settings: specify the engine tools available, set the viewport as the main one, specify the camera the image from which is rendered into the viewport, and so on. All these operations are provided by the *EngineWindowViewport* class. For example:


```csharp
// set the window viewport as the main one
window.Main = true;

// enable the console, profiler and visualizer for the window viewport
window.ConsoleUsage = true;
window.ProfilerUsage = true;
window.VisualizerUsage = true;


```


You can also add widgets to the client area of the window:


```csharp
// add widgets to the client area
window.AddChild(new WidgetLabel(window.SelfGui,  String.Format("This is {0} window.", window.Title)));
window.AddChild(new WidgetButton(window.SelfGui, window.Title), Gui.ALIGN_CENTER);


```


> **Notice:** The window viewport is considered a **separate engine window** until it is added to a group.


To control window components, its behaviour, visual representaion, and style, use the *[EngineWindow](../../api/library/gui/class.enginewindow_cs.md)* class functionality. The corresponding article contains short samples that cover most of the available functions.


## Creating a Window Group


When the engine windows are grouped, a new window containing these windows is created. This new window is called a **group**, and the windows in the group - **nested**. The number of windows in the group is unlimited. Moreover, you can group both the separate engine windows and the existing window groups.


There are three types of the **window groups**:


- Vertical
- Horizontal
- Group of tabs


Within the group, all windows are stacked according to one of these types.


![](group_types.png)


> **Notice:** Grouping of the created windows can be done via the code or [by using the mouse](#mouse_grouping) while the application is running.


### Grouping via Code


A window group is an instance of the *[EngineWindowGroup](../../api/library/gui/class.enginewindowgroup_cs.md)* class that can be created in one of the following ways:


- You can create an empty group using one of the *EngineWindowGroup* class constructors and then add windows or other groups to it. ```csharp // create separate windows that will be grouped EngineWindowViewport horizontal_1 = new EngineWindowViewport("Horizontal 1", 512, 256); EngineWindowViewport horizontal_2 = new EngineWindowViewport("Horizontal 2", 512, 256); EngineWindowViewport horizontal_3 = new EngineWindowViewport("Horizontal 3", 512, 256); // create a horizontal group EngineWindowGroup horizontal_group = new EngineWindowGroup(EngineWindowGroup.GROUP_TYPE.HORIZONTAL, "Horizontal Group", 565, 310); // add windows to the group horizontal_group.Add(horizontal_1); horizontal_group.Add(horizontal_2); horizontal_group.Add(horizontal_3); // set a position of the group horizontal_group.Position = new ivec2(50, 60); ``` > **Notice:** This approach implies that you implement custom grouping and ungrouping logic: check if the windows can be nested or produce a group, set the automatic deletion mode, and so on. The *[EngineWindow](../../api/library/gui/class.enginewindow_cs.md)* and *[EngineWindowGroup](../../api/library/gui/class.enginewindowgroup_cs.md)* classes provide the required funtionality for controlling the engine windows stacking.
- You can [stack windows](#manage_window_groups) using *[WindowManager](../../api/library/gui/class.windowmanager_cs.md)* class functionality. In this case, the manager will automatically validate windows before adding them to the group and manage the group after removing a window from it.


When the window group is created, you can adjust its elements: set titles and icons for tabs, change its width or height, adjust separators. All these operations are provided by the *EngineWindowGroup* class.


> **Notice:** You may need to call [*UpdateGuiHierarchy()*](../../api/library/gui/class.enginewindow_cs.md#updateGuiHierarchy_void) first, if you have added a new window to the group and want to access its settings immediately. Otherwise, you may get incorrect results.


For example, to change the first tab in the group, you can do the following:


```csharp
// update a hierarchy in self gui of the group
horizontal_group.UpdateGuiHierarchy();

int position_offset = 100;
float value_offset = 0.2f;

for (int i = 0; i < horizontal_group.NumNestedWindows; i++)
{
	// change a tab
	horizontal_group.SetTabTitle(i, "New name " + i.ToString());
	if (i == 0) horizontal_group.SetHorizontalTabWidth(i, position_offset);

	// change a separator
	horizontal_group.SetSeparatorValue(i, horizontal_group.GetSeparatorValue(i) + value_offset);
}


```


UNIGINE SDK provides several samples (`source/samples/Api/WindowManager`) on the window groups: you can check different group types in the `GroupTypes` sample or create a new window group and try to adjust it in the `WindowSandbox` sample. Also the article on the *[EngineWindowGroup](../../api/library/gui/class.enginewindowgroup_cs.md)* class contains short samples demonstrating the available functions.


### Grouping Using the Mouse


While the application is running, you can group and ungroup the existing windows by using the mouse.


To group two separate windows, do the following:


1. Hold the mouse button while moving the window to the destination one. The destination window will be divided into 9 sectors.
2. Choose the required sector and release the mouse button � the windows will be grouped.


![](mouse_grouping.png)


To add the window to the existing group, you should hold the mouse button while moving the window and release it in one of the following areas:


- For the horizontal group: ![](mouse_horizontal.png)
- For the vertical group: ![](mouse_vertical.png)
- For the group of tabs: ![](mouse_tabs.png)


To ungroup the window, move it outside the group by dragging the title bar.


## Accessing Windows


The engine window can be accessed via the *[WindowManager.GetWindow()](../../api/library/gui/class.windowmanager_cs.md#getWindow_int_EngineWindow)* function.


```csharp
// get the number of windows
int num = WindowManager.NumWindows;
// check each window
for (int i = 0; i < num; i++)
{
	// get the window with the current index
	EngineWindow window = WindowManager.GetWindow(i);
	// change its position and size if it is main
	if (window == WindowManager.MainWindow)
	{
		window.Position = new ivec2(1020, 60);
		window.Size = new ivec2(305, 670);
	}
}


```


There are also some functions (like *[WindowManager.MainWindow](../../api/library/gui/class.windowmanager_cs.md#getMainWindow_EngineWindowViewport)*) that allow accessing the specific windows (the [main](../../api/library/gui/class.windowmanager_cs.md#getMainWindow_EngineWindowViewport), [focused](../../api/library/gui/class.windowmanager_cs.md#getFocusedWindow_EngineWindowViewport), [fullscreen](../../api/library/gui/class.windowmanager_cs.md#getFullscreenWindow_EngineWindowViewport) window and so on). For example:


```csharp
// get the main window
EngineWindow main_window = WindowManager.MainWindow;
// change its position and size
if (main_window)
{
	main_window.Position = new ivec2(1020, 60);
	main_window.Size = new ivec2(305, 670);
}


```


## Managing Window Groups


As it was mentioned above, you can implement custom logic for grouping and ungrouping windows or use functionality provided by the *[WindowManager](../../api/library/gui/class.windowmanager_cs.md)* class. Here we will consider the latter.


In the *WindowManager* class, there are two main functions for grouping windows:


- *[WindowManager.Stack()](../../api/library/gui/class.windowmanager_cs.md#stack_EngineWindow_EngineWindow_int_int_int_EngineWindowGroup)* creates a group of two windows.
- *[WindowManager.StackGroups()](../../api/library/gui/class.windowmanager_cs.md#stackGroups_EngineWindowGroup_EngineWindowGroup_int_EngineWindowGroup)* creates a group of two window groups.


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


Each window or window group has a [state](../../api/library/gui/class.enginewindow_cs.md#TYPE), so it changes after stacking.


![](window_manager_stacking.png)


There are also functions based on the *WindowManager.Stack()* function that should be used in specific cases to avoid additional checking of arguments:


- *[WindowManager.StackToParentGroup()](../../api/library/gui/class.windowmanager_cs.md#stackToParentGroup_EngineWindow_EngineWindow_int_int_EngineWindowGroup)* stacks the second window to the parent group of the first window. In the result, both windows passed as arguments will be on the same level in the group hierarchy. ```csharp // create separate windows EngineWindowViewport window_1 = new EngineWindowViewport("Window 1", 512, 256); EngineWindowViewport window_2 = new EngineWindowViewport("Window 2", 512, 256); EngineWindowViewport window_3 = new EngineWindowViewport("Window 3", 512, 256); // stack 2 separate windows EngineWindowGroup group_0 = WindowManager.StackWindows(window_1, window_2, EngineWindowGroup.GROUP_TYPE.HORIZONTAL); // stack a separate window to the parent group of "window_1" WindowManager.StackToParentGroup(window_1, window_3); ``` ![](stackto_parent_group.png)
- *[WindowManager.StackWithWindow()](../../api/library/gui/class.windowmanager_cs.md#stackWithWindow_EngineWindowViewport_EngineWindow_int_int_EngineWindowGroup)* stacks the window to the other window. If the first argument is the separate window, a new window group is returned. If the first argument is the nested window, the window is added to its group. ```csharp // create a group of 2 windows EngineWindowGroup group_1 = WindowManager.Stack(window_1, window_2, EngineWindowGroup.GROUP_TYPE.HORIZONTAL); // stack a separate window to the window from the window group WindowManager.StackWithWindow(window_1, window_3, EngineWindowGroup.GROUP_TYPE.VERTICAL); ``` ![](stackto_window.png)
- *[WindowManager.StackWindows()](../../api/library/gui/class.windowmanager_cs.md#stackWindows_EngineWindowViewport_EngineWindowViewport_int_EngineWindowGroup)* creates a group of the separate/nested windows. The windows are stacked in the default order.
- *[WindowManager.StackToGroup()](../../api/library/gui/class.windowmanager_cs.md#stackToGroup_EngineWindowGroup_EngineWindow_int_int_EngineWindowGroup)* stacks the window or window group to another window group.


For ungrouping, the *[WindowManager.Unstack()](../../api/library/gui/class.windowmanager_cs.md#unstack_EngineWindow_void)* function is used: it removes the window or the window group from the parent group. If only one window remains in the group, it is automatically removed from the group and the group is deleted.


## Working with Dialogs


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


If you press the button in the client area of the created window, the following dialog will be shown:


![](dialog_message.png)
