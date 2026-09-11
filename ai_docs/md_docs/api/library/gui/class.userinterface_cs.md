# Unigine::UserInterface Class (CS)


The class is used to work with widgets that are created by loading a UI file.


### Usage Examples


The examples below show:

- Loading a UserInterface from the `*.ui` file and accessing the widgets it stores.
- Adding callbacks to these widgets.
- Managing the UserInterface lifetime.


#### Managing Lifetime by the World


The UserInterface is created on loading the world. When you reload or exit the world, or close the Engine window, the UserInterface is deleted.


<details>
<summary>WidgetLifetimeWorld.cs | Close</summary>

`WidgetLifetimeWorld.cs`


```csharp
void on_group_remove()
{
	Log.Message("world group removed\n");
}

private void Init()
{

	// world user interface
	UserInterface ui = new UserInterface(Gui.GetCurrent(), "user_interface.ui");
	ui.Lifetime = Widget.LIFETIME.WORLD;

	WidgetGroupBox main_group = (WidgetGroupBox)ui.GetWidget(ui.FindWidget("main_group"));
	main_group.Text = "World User Interface";
	main_group.EventRemove.Connect(on_group_remove);
	WindowManager.MainWindow.AddChild(main_group, Gui.ALIGN_EXPAND);

}


```

</details>


#### Managing Lifetime by the Window


The UserInterface is created in a separate window. When you close the window, the UserInterface is deleted as its lifetime is managed by this window. The console shows whether the window and UserInterface are deleted or not, whether the remove event is fired, and the message from the remove event handler (if it is).


After closing, the window can be re-created by pressing **T**.


<details>
<summary>WidgetLifetimeWindow.cs | Close</summary>

`WidgetLifetimeWorld.cs`


```csharp
public EngineWindowViewport window;

public UserInterface ui;
public WidgetGroupBox main_group;

bool group_remove_handler = false;

void on_window_group_remove()
{
	Log.Message("window group removed\n");
	group_remove_handler = true;
}

public void on_window_button_click()
{
	Log.Message("window button click\n");
}

public void on_window_button_remove()
{
	Log.Message("window button removed\n");
	button_remove_handler = true;
}

public void on_window_hbox_remove()
{
	Log.Message("window hbox hierarchy removed\n");
	hbox_remove_handler = true;
}
public void create_window()
{
	button_remove_handler = false;
	hbox_remove_handler = false;
	window = new EngineWindowViewport("Test", 512, 256, (int)EngineWindow.FLAGS.SHOWN);
	// single window widget
	button = new WidgetButton("WINDOW_BUTTON");
	button.Lifetime = Widget.LIFETIME.WINDOW;
	button.EventClicked.Connect(on_window_button_click);
	button.EventRemove.Connect(on_window_button_remove);
	window.AddChild(button);

	// window hierarchy
	hbox = new WidgetHBox();
	hbox.Lifetime = Widget.LIFETIME.WINDOW;
	hbox.EventRemove.Connect(on_window_hbox_remove);
	hbox.Background = 1;
	hbox.BackgroundColor = vec4.WHITE;
	window.AddChild(hbox, Gui.ALIGN_EXPAND);

	WidgetGroupBox group = new WidgetGroupBox();
	group.Background = 1;
	group.Text = "Window Hierarchy";
	hbox.AddChild(group);

	group.AddChild(new WidgetLabel("hierarchy_window_label_0"));
	group.AddChild(new WidgetLabel("hierarchy_window_label_1"));
	// window user interface
	ui = new UserInterface(window.Gui, "user_interface.ui");
	ui.Lifetime = Widget.LIFETIME.WINDOW;

	main_group = (WidgetGroupBox)ui.GetWidget(ui.FindWidget("main_group"));
	main_group.Text = "Window User Interface";
	main_group.EventRemove.Connect(on_window_group_remove);
	window.AddChild(main_group, Gui.ALIGN_EXPAND);
}

private void Init()
{
	create_window();
}
private void Update()
{
	if (Input.IsKeyDown(Input.KEY.T) && window.IsDeleted)
		create_window();
	Log.Message("window deleted: {0}, button deleted: {1}, hbox deleted: {2}, button remove handler: {3}, hbox remove handler: {4}\n",
				window.IsDeleted, button.IsDeleted, hbox.IsDeleted, button_remove_handler, hbox_remove_handler);
	Log.Message("window deleted: {0}, group deleted: {1}, ui deleted: {2}, group remove handler {3}\n",
	window.IsDeleted, main_group.IsDeleted, ui.IsDeleted, group_remove_handler);
}
}
void on_window_group_remove()
{
	Log.Message("window group removed\n");
	group_remove_handler = true;
}

public void create_window()
{

	window = new EngineWindowViewport("Test", 512, 256, (int)EngineWindow.FLAGS.SHOWN);

	// window user interface
	ui = new UserInterface(window.Gui, "user_interface.ui");
	ui.Lifetime = Widget.LIFETIME.WINDOW;

	main_group = (WidgetGroupBox)ui.GetWidget(ui.FindWidget("main_group"));
	main_group.Text = "Window User Interface";
	main_group.EventRemove.Connect(on_window_group_remove);
	window.AddChild(main_group, Gui.ALIGN_EXPAND);

}

private void Init()
{
	create_window();
}

private void Update()
{
	if (Input.IsKeyDown(Input.KEY.T) && window.IsDeleted)
		create_window();

	Log.Message("window deleted: {0}, group deleted: {1}, ui deleted: {2}, group remove handler {3}\n",
	window.IsDeleted, main_group.IsDeleted, ui.IsDeleted, group_remove_handler);

}


```

</details>


#### Managing Lifetime by the Engine


The lifetime of the UserInterface is managed by the Engine, so it is deleted on Engine shutdown. A [Gui](../../../api/library/gui/class.gui_cs.md) instance is set manually via the *[setGui()](#setGui_Gui_void)* method.


The console shows whether the window and UserInterface are deleted or not, whether the remove event is fired, and the message from the remove event handler (if it is). After closing, the window can be re-created by pressing **T**.


<details>
<summary>WidgetLifetimeEngine.cs | Close</summary>

`WidgetLifetimeEngine.cs`


```csharp
EngineWindowViewport engine_window;

UserInterface engine_ui;
WidgetGroupBox engine_main_group;

bool engine_group_remove_handler = false;

void on_engine_group_remove()
{
	Log.Message("engine group removed\n");
	engine_group_remove_handler = true;
}
void on_engine_button_click()
{
	Log.Message("engine button click\n");
}

void on_engine_button_remove()
{
	Log.Message("engine button removed\n");
	engine_button_remove_handler = true;
}

void on_engine_hbox_remove()
{
	Log.Message("engine hbox hierarchy removed\n");
	engine_hbox_remove_handler = true;
}
void create_engine_window()
{
	engine_window = new EngineWindowViewport("Test", 512, 256, (int)EngineWindow.FLAGS.SHOWN);
	engine_window.AddChild(engine_button);
	engine_window.AddChild(engine_hbox, Gui.ALIGN_EXPAND);
	engine_ui.Gui = engine_window.Gui;
	engine_window.AddChild(engine_main_group, Gui.ALIGN_EXPAND);
}

private void Init()
{
	engine_button_remove_handler = false;
	engine_hbox_remove_handler = false;

	// single engine widget
	engine_button = new WidgetButton("ENGINE_BUTTON");
	engine_button.Lifetime = Widget.LIFETIME.ENGINE;
	engine_button.EventClicked.Connect(on_engine_button_click);
	engine_button.EventRemove.Connect(on_engine_button_remove);

	// engine hierarchy
	engine_hbox = new WidgetHBox();
	engine_hbox.Lifetime = Widget.LIFETIME.ENGINE;
	engine_hbox.EventRemove.Connect(on_engine_hbox_remove);
	engine_hbox.Background = 1;
	engine_hbox.BackgroundColor = vec4.WHITE;

	WidgetGroupBox engine_group = new WidgetGroupBox();
	engine_group.Background = 1;
	engine_group.Text = "Engine Hierarchy";
	engine_hbox.AddChild(engine_group);

	engine_group.AddChild(new WidgetLabel("hierarchy_engine_label_0"));
	engine_group.AddChild(new WidgetLabel("hierarchy_engine_label_1"));
	// engine user interface
	engine_ui = new UserInterface(Gui.GetCurrent(), "user_interface.ui");
	engine_ui.Lifetime = Widget.LIFETIME.ENGINE;

	engine_main_group = (WidgetGroupBox)engine_ui.GetWidget(engine_ui.FindWidget("main_group"));
	engine_main_group.Text = "Engine User Interface";
	engine_main_group.EventRemove.Connect(on_engine_group_remove);
	create_engine_window();
}
private void Update()
{
	if (Input.IsKeyDown(Input.KEY.T) && engine_window.IsDeleted)
		create_engine_window();
	Log.Message("engine window deleted: {0}, engine button deleted: {1}, engine hbox deleted: {2}, engine button remove handler: {3}, engine hbox remove handler: {4}\n",
		engine_window.IsDeleted, engine_button.IsDeleted, engine_hbox.IsDeleted, engine_button_remove_handler, engine_hbox_remove_handler);
	Log.Message("engine window deleted: {0},engine group deleted: {1}, engine ui deleted: {2}, engine group remove handler {3}\n",
	engine_window.IsDeleted, engine_main_group.IsDeleted, engine_ui.IsDeleted, engine_group_remove_handler);
}
}
void on_engine_group_remove()
{
	Log.Message("engine group removed\n");
	engine_group_remove_handler = true;
}

void create_engine_window()
{
	engine_window = new EngineWindowViewport("Test", 512, 256, (int)EngineWindow.FLAGS.SHOWN);

	engine_ui.Gui = engine_window.Gui;
	engine_window.AddChild(engine_main_group, Gui.ALIGN_EXPAND);

}

private void Init()
{

	// engine user interface
	engine_ui = new UserInterface(Gui.GetCurrent(), "user_interface.ui");
	engine_ui.Lifetime = Widget.LIFETIME.ENGINE;

	engine_main_group = (WidgetGroupBox)engine_ui.GetWidget(engine_ui.FindWidget("main_group"));
	engine_main_group.Text = "Engine User Interface";
	engine_main_group.EventRemove.Connect(on_engine_group_remove);

	create_engine_window();
}

private void Update()
{
	if (Input.IsKeyDown(Input.KEY.T) && engine_window.IsDeleted)
		create_engine_window();

	Log.Message("engine window deleted: {0},engine group deleted: {1}, engine ui deleted: {2}, engine group remove handler {3}\n",
	engine_window.IsDeleted, engine_main_group.IsDeleted, engine_ui.IsDeleted, engine_group_remove_handler);

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

### Properties

## 🔒︎ int NumWidgets

The number of associated widgets.
## Gui Gui

The *[Gui](../../../api/library/gui/class.gui_cs.md)* instance used for the UserInterface.
## Widget.LIFETIME Lifetime

The lifetime management type for the UserInterface. By default, the [LIFETIME_ENGINE](../../../api/library/gui/class.widget_cs.md#LIFETIME) type is used.
> **Notice:** Lifetime of each UserInterface in the hierarchy is defined by its root. Thus, a lifetime management type set for a child UserInterface that differs from the one set for the root is ignored.

### Members

---

## UserInterface ( Gui gui , string name , string prefix = 0 )

UserInterface constructor.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - GUI smart pointer.
- *string* **name** - User interface name.
- *string* **prefix** - Names prefix.

## int GetCallback ( int num , int callback )

Returns the number of a given callback function.
### Arguments

- *int* **num** - Widget number.
- *int* **callback**

### Return value

Callback number.
## string GetCallbackInstanceData ( int num , Gui.CALLBACK_INDEX callback )

Returns the callback instance data.
### Arguments

- *int* **num** - Widget number.
- *[Gui.CALLBACK_INDEX](../../../api/library/gui/class.gui_cs.md#CALLBACK_INDEX)* **callback**

### Return value

Callback instance data.
## string GetCallbackName ( int num , Gui.CALLBACK_INDEX callback )

Returns the name of a given callback function.
### Arguments

- *int* **num** - Widget number.
- *[Gui.CALLBACK_INDEX](../../../api/library/gui/class.gui_cs.md#CALLBACK_INDEX)* **callback**

### Return value

Callback function name.
## string GetCallbackStringData ( int num , Gui.CALLBACK_INDEX callback )

Returns the callback string data.
### Arguments

- *int* **num** - Widget number.
- *[Gui.CALLBACK_INDEX](../../../api/library/gui/class.gui_cs.md#CALLBACK_INDEX)* **callback**

### Return value

Callback string data.
## string GetCallbackVariableData ( int num , Gui.CALLBACK_INDEX callback )

Returns the callback variable data.
### Arguments

- *int* **num** - Widget number.
- *[Gui.CALLBACK_INDEX](../../../api/library/gui/class.gui_cs.md#CALLBACK_INDEX)* **callback**

### Return value

Callback variable data.
## Widget GetCallbackWidgetData ( int num , Gui.CALLBACK_INDEX callback )

Returns the callback widget data.
### Arguments

- *int* **num** - Widget number.
- *[Gui.CALLBACK_INDEX](../../../api/library/gui/class.gui_cs.md#CALLBACK_INDEX)* **callback**

### Return value

Widget data.
## int GetNumCallbacks ( int num )

Returns the total number of callbacks for a given widget.
### Arguments

- *int* **num** - Widget number.

### Return value

Number of callbacks.
## Widget GetWidget ( int num )

Returns a widget with the given ID.
### Arguments

- *int* **num** - Widget ID.

### Return value

Pointer to the widget with the given number.
## Widget GetWidgetByName ( string name )

Returns a widget with the given name.
### Arguments

- *string* **name** - Widget name.

### Return value

Widget with the given ID.
## int GetWidgetExport ( int num )

Returns a value indicating if a given widget is exported into a script.
### Arguments

- *int* **num** - Widget ID.

### Return value

Returns 1 if the widget is exported; otherwise, 0.
## string GetWidgetName ( int num )

Returns widget name by its number.
### Arguments

- *int* **num** - Widget ID.

### Return value

Widget name.
## string GetWidgetNext ( int num )

Returns the name of the widget, which will be focused next.
### Arguments

- *int* **num** - Widget number.

### Return value

Next Widget name.
## int FindWidget ( string name )

Searches a widget by its name.
### Arguments

- *string* **name** - Widget name.

### Return value

Returns the number of the widget if exists; otherwise, -1.
## void UpdateWidgets ( )

Updates all widgets belonging to the user interface. This function should be called, for example, after change of the interface language.
