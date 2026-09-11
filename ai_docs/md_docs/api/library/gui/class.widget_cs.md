# Unigine::Widget Class (CS)


This base class is used to create [graphical user interface](../../../objects/objects/gui/index.md) widgets of different types. The Widget class doesn't provide creating of a widget: you can create the required widget by using a constructor of the corresponding class inherited from the Widget class.


Widgets can be used separately or form a hierarchy.


### Working with Widgets


The example below demonstrates how to create a single widget, a hierarchy of widgets, and subscribe for a widget's event.


<details>
<summary>WidgetClass.cs | Close</summary>

`WidgetClass.cs`


```csharp
public void on_button_click()
{
	Log.Message("world button click\n");
}

private void Init()
{
	// create a single widget
	WidgetButton button = new WidgetButton("WORLD_BUTTON");
	// subscribing for the button Click event
	button.EventClicked.Connect(on_button_click);
	// add the button to WindowManager
	WindowManager.MainWindow.AddChild(button);

	// create a hierarchy of widgets
	WidgetHBox hbox = new WidgetHBox();
	hbox.Background = 1;
	hbox.BackgroundColor = vec4.WHITE;
	WindowManager.MainWindow.AddChild(hbox, Gui.ALIGN_EXPAND);

	WidgetGroupBox group = new WidgetGroupBox();
	group.Background = 1;
	group.Text = "Widgets Hierarchy";
	hbox.AddChild(group);

	group.AddChild(new WidgetLabel("hierarchy_label_0"));
	group.AddChild(new WidgetLabel("hierarchy_label_1"));

}


```

</details>


#### Lifetime of Widgets


By default each new widget's lifetime matches the lifetime of the **[Engine](#LIFETIME_ENGINE)** (i.e. the widget shall be deleted on Engine shutdown). But you can choose widget's lifetime to be managed:

- By a separate **[window](#LIFETIME_WINDOW)** � in this case the widget is deleted automatically on deleting the window.
- By the **[world](#LIFETIME_WORLD)** � in this case the widget is deleted when the world is closed.
- **[Manually](#LIFETIME_MANUAL)** � in this case the widget should be deleted manually.


The examples below show how the different lifetime management types work.


##### Managing Lifetime by the World


In this example, the widgets appear on loading the world. When you reload or exit the world, or close the Engine window, the widgets are deleted as their lifetime is managed by the *world*. The corresponding messages will be shown in the console.


<details>
<summary>WidgetLifetimeWorld.cs | Close</summary>

`WidgetLifetimeWorld.cs`


```csharp
public void on_button_click()
{
	Log.Message("world button click\n");
}

public void on_button_remove()
{
	Log.Message("world button removed\n");
}

public void on_hbox_remove()
{
	Log.Message("world hbox hierarchy removed\n");
}

private void Init()
{

	// create a single widget
	WidgetButton button = new WidgetButton("WORLD_BUTTON");
	// set the world lifetime
	button.Lifetime = Widget.LIFETIME.WORLD;
	// subscribing for the button Click event
	button.EventClicked.Connect(on_button_click);
	// the "on_button_remove" handler will be executed on reloading or closing the world, or on Engine shutdown
	button.EventRemove.Connect(on_button_remove);
	// add the button to WindowManager
	WindowManager.MainWindow.AddChild(button);

	// create a hierarchy of widgets
	WidgetHBox hbox = new WidgetHBox();
	// set the world lifetime
	hbox.Lifetime = Widget.LIFETIME.WORLD;
	// the "on_hbox_remove" handler will be executed on reloading or closing the world, or on Engine shutdown
	hbox.EventRemove.Connect(on_hbox_remove);
	hbox.Background = 1;
	hbox.BackgroundColor = vec4.WHITE;
	WindowManager.MainWindow.AddChild(hbox, Gui.ALIGN_EXPAND);

	WidgetGroupBox group = new WidgetGroupBox();
	group.Background = 1;
	group.Text = "Widgets Hierarchy";
	hbox.AddChild(group);

	group.AddChild(new WidgetLabel("hierarchy_label_0"));
	group.AddChild(new WidgetLabel("hierarchy_label_1"));

}


```

</details>


##### Managing Lifetime by the Window


In this example, widgets appear in a separate window. When you close the window, the widgets are deleted as their lifetime is managed by this *window*. The console shows the following information:

- Whether the window, button and hbox hierarchy are deleted or not.
- Whether the remove callbacks are fired or not.
- Messages from the remove callbacks.


After closing, the window can be re-created by pressing **T**.


<details>
<summary>WidgetLifetimeWindow.cs | Close</summary>

`WidgetLifetimeWindow.cs`


```csharp
public EngineWindowViewport window;

public WidgetButton button;
public WidgetHBox hbox;

bool button_remove_handler = false;
bool hbox_remove_handler = false;

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

}


```

</details>


##### Managing Lifetime by the Engine


Widgets are created on Engine initialization, and then added to a separate window. The console shows the following information:


- Whether the window, button and hbox hierarchy are deleted or not.
- Whether the remove callbacks are fired or not.
- Messages from the remove callbacks.


If you close the window, it will be deleted and the information in the console will change. All the other widgets are deleted only on Engine shutdown, as their lifetime is managed by the Engine.


If the separate window is closed, press **T** to re-create it.


<details>
<summary>WidgetLifetimeEngine.cs | Close</summary>

`WidgetLifetimeEngine.cs`


```csharp
EngineWindowViewport engine_window;

WidgetButton engine_button;
WidgetHBox engine_hbox;

bool engine_button_remove_handler = false;
bool engine_hbox_remove_handler = false;

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

	create_engine_window();
}

private void Update()
{
	if (Input.IsKeyDown(Input.KEY.T) && engine_window.IsDeleted)
		create_engine_window();

	Log.Message("engine window deleted: {0}, engine button deleted: {1}, engine hbox deleted: {2}, engine button remove handler: {3}, engine hbox remove handler: {4}\n",
		engine_window.IsDeleted, engine_button.IsDeleted, engine_hbox.IsDeleted, engine_button_remove_handler, engine_hbox_remove_handler);

}


```

</details>


### See Also


- C++ sample
- C# Component sample
- A set of [UnigineScript samples](../../../code/uniginescript/samples/widgets.md) located in the `<UnigineSDK>/data/samples/widgets/` folder


## Widget Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **WIDGET_VBOX** = 0 | [Vertical box](../../../code/gui/ui/ui_containers.md#vbox). See also: [WidgetVBox](../../../api/library/gui/class.widgetvbox_cs.md). |
| **WIDGET_HBOX** = 1 | [Horizontal box](../../../code/gui/ui/ui_containers.md#hbox). See also: [WidgetHBox](../../../api/library/gui/class.widgethbox_cs.md). |
| **WIDGET_GRID_BOX** = 2 | [Grid box](../../../code/gui/ui/ui_containers.md#gridbox). See also: [WidgetGridBox](../../../api/library/gui/class.widgetgridbox_cs.md). |
| **WIDGET_VPANED** = 3 | [Vertical box that allows resizing of its children](../../../code/gui/ui/ui_containers.md#vpaned). See also: [WidgetVPaned](../../../api/library/gui/class.widgetvpaned_cs.md). |
| **WIDGET_HPANED** = 4 | [Horizontal box that allows resizing of its children](../../../code/gui/ui/ui_containers.md#hpaned). See also: [WidgetHPaned](../../../api/library/gui/class.widgethpaned_cs.md). |
| **WIDGET_LABEL** = 5 | [Text label](../../../code/gui/ui/ui_widgets.md#label). See also: [WidgetLabel](../../../api/library/gui/class.widgetlabel_cs.md). |
| **WIDGET_BUTTON** = 6 | [Simple button](../../../code/gui/ui/ui_widgets.md#button). See also: [WidgetButton](../../../api/library/gui/class.widgetbutton_cs.md). |
| **WIDGET_EDIT_LINE** = 7 | [Text field](../../../code/gui/ui/ui_widgets.md#editline). See also: [WidgetEditline](../../../api/library/gui/class.widgeteditline_cs.md). |
| **WIDGET_EDIT_TEXT** = 8 | [Multiline text field](../../../code/gui/ui/ui_widgets.md#edittext). See also: [WidgetEdittext](../../../api/library/gui/class.widgetedittext_cs.md). |
| **WIDGET_CHECK_BOX** = 9 | [Checkbox](../../../code/gui/ui/ui_widgets.md#checkbox). See also: [WidgetCheckbox](../../../api/library/gui/class.widgetcheckbox_cs.md). |
| **WIDGET_COMBO_BOX** = 10 | [Combobox](../../../code/gui/ui/ui_widgets.md#combobox). See also: [WidgetCombobox](../../../api/library/gui/class.widgetcombobox_cs.md). |
| **WIDGET_CANVAS** = 11 | Canvas widget for drawing text, lines and polygons. See also: [WidgetCanvas](../../../api/library/gui/class.widgetcanvas_cs.md). |
| **WIDGET_GROUP_BOX** = 12 | [Group box](../../../code/gui/ui/ui_containers.md#groupbox). See also: [WidgetGroupBox](../../../api/library/gui/class.widgetgroupbox_cs.md). |
| **WIDGET_LIST_BOX** = 13 | [List box](../../../code/gui/ui/ui_widgets.md#listbox). See also: [WidgetListBox](../../../api/library/gui/class.widgetlistbox_cs.md). |
| **WIDGET_TREE_BOX** = 14 | [Tree box](../../../code/gui/ui/ui_widgets.md#treebox). See also: [WidgetTreeBox](../../../api/library/gui/class.widgettreebox_cs.md). |
| **WIDGET_TAB_BOX** = 15 | [Tabbed box](../../../code/gui/ui/ui_containers.md#tabbox). See also: [WidgetTabBox](../../../api/library/gui/class.widgettabbox_cs.md). |
| **WIDGET_SCROLL** = 16 | A scrollbar: [horizontal](../../../code/gui/ui/ui_widgets.md#hscroll) or [vertical](../../../code/gui/ui/ui_widgets.md#vscroll) one. See also: [WidgetScroll](../../../api/library/gui/class.widgetscroll_cs.md). |
| **WIDGET_SCROLL_BOX** = 17 | [Box with scrolling](../../../code/gui/ui/ui_containers.md#scrollbox). See also: [WidgetScrollBox](../../../api/library/gui/class.widgetscrollbox_cs.md). |
| **WIDGET_SPACER** = 18 | Spacer: [horizontal](../../../code/gui/ui/ui_widgets.md#hspacer) or [vertical](../../../code/gui/ui/ui_widgets.md#vspacer) one. See also: [WidgetSpacer](../../../api/library/gui/class.widgetspacer_cs.md). |
| **WIDGET_SLIDER** = 19 | A slider: [horizontal](../../../code/gui/ui/ui_widgets.md#hslider) or [vertical](../../../code/gui/ui/ui_widgets.md#vslider) one. See also: [WidgetSlider](../../../api/library/gui/class.widgetslider_cs.md). |
| **WIDGET_SPIN_BOX** = 20 | [Spinbox](../../../code/gui/ui/ui_widgets.md#spinbox). See also: [WidgetSpinBox](../../../api/library/gui/class.widgetspinbox_cs.md). |
| **WIDGET_SPIN_BOX_DOUBLE** = 21 | [Spinbox](../../../code/gui/ui/ui_widgets.md#spinbox) with double values. See also: [WidgetSpinBoxDouble](../../../api/library/gui/class.widgetspinboxdouble_cs.md). |
| **WIDGET_ICON** = 22 | [Icon](../../../code/gui/ui/ui_widgets.md#icon). See also: [WidgetIcon](../../../api/library/gui/class.widgeticon_cs.md). |
| **WIDGET_SPRITE** = 23 | [Sprite](../../../code/gui/ui/ui_widgets.md#sprite). See also: [WidgetSprite](../../../api/library/gui/class.widgetsprite_cs.md). |
| **WIDGET_SPRITE_VIDEO** = 24 | Video Sprite. See also: [WidgetSpriteVideo](../../../api/library/gui/class.widgetspritevideo_cs.md). |
| **WIDGET_SPRITE_SHADER** = 25 | Shader Sprite. See also: [WidgetSpriteShader](../../../api/library/gui/class.widgetspriteshader_cs.md). |
| **WIDGET_SPRITE_VIEWPORT** = 26 | Viewport Sprite. See also: [WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cs.md). |
| **WIDGET_SPRITE_NODE** = 27 | Node Sprite. See also: [WidgetSpriteNode](../../../api/library/gui/class.widgetspritenode_cs.md). |
| **WIDGET_MENU_BAR** = 28 | [Menu bar](../../../code/gui/ui/ui_widgets.md#menubar). See also: [WidgetMenuBar](../../../api/library/gui/class.widgetmenubar_cs.md). |
| **WIDGET_MENU_BOX** = 29 | [Menu](../../../code/gui/ui/ui_widgets.md#menubox). See also: [WidgetMenuBox](../../../api/library/gui/class.widgetmenubox_cs.md). |
| **WIDGET_WINDOW** = 30 | [Window](../../../code/gui/ui/ui_containers.md#window). See also: [WidgetWindow](../../../api/library/gui/class.widgetwindow_cs.md). |
| **WIDGET_DIALOG** = 31 | [Dialog window](../../../code/gui/ui/ui_containers.md#dialog). See also: [WidgetDialog](../../../api/library/gui/class.widgetdialog_cs.md). |
| **WIDGET_DIALOG_MESSAGE** = 32 | Message Dialog. See also: [WidgetDialogMessage](../../../api/library/gui/class.widgetdialogmessage_cs.md). |
| **WIDGET_DIALOG_FILE** = 33 | File Dialog. See also: [WidgetDialogFile](../../../api/library/gui/class.widgetdialogfile_cs.md). |
| **WIDGET_DIALOG_COLOR** = 34 | Color Dialog. See also: [WidgetDialogColor](../../../api/library/gui/class.widgetdialogcolor_cs.md). |
| **WIDGET_DIALOG_IMAGE** = 35 | Image Dialog. See also: [WidgetDialogImage](../../../api/library/gui/class.widgetdialogimage_cs.md). |
| **WIDGET_MANIPULATOR** = 36 | Manipulator widget. See also: [WidgetManipulator](../../../api/library/gui/class.widgetmanipulator_cs.md). |
| **WIDGET_MANIPULATOR_TRANSLATOR** = 37 | Translator Manipulator. See also: [WidgetManipulatorTranslator](../../../api/library/gui/class.widgetmanipulatortranslator_cs.md). |
| **WIDGET_MANIPULATOR_ROTATOR** = 38 | Rotator Manipulator. See also: [WidgetManipulatorRotator](../../../api/library/gui/class.widgetmanipulatorrotator_cs.md). |
| **WIDGET_MANIPULATOR_SCALER** = 39 | Scaler Manipulator. See also: [WidgetManipulatorScaler](../../../api/library/gui/class.widgetmanipulatorscaler_cs.md). |
| **WIDGET_EXTERN** = 40 | External widget. |
| **WIDGET_ENGINE** = 41 | Engine-specific widget (manipulator). See also: [WidgetManipulator](../../../api/library/gui/class.widgetmanipulator_cs.md). |
| **WIDGET_HIT_TEST_AREA** = 42 | Hit-Test Area. See also: [WidgetHitTestArea](../../../api/library/gui/class.widgethittestarea_cs.md). |
| **NUM_WIDGETS** = 43 | Total number of widget types. |

## LIFETIME

| Name | Description |
|---|---|
| **WORLD** = 0 | Lifetime of the widget or user interface is managed by the world. The widget/user interface will be deleted automatically on closing the world. |
| **WINDOW** = 1 | Lifetime of the widget or user interface is managed by the window. The widget/user interface will be deleted automatically on deleting the window. |
| **ENGINE** = 2 | Lifetime of the widget or user interface is managed by the Engine. The widget/user interface will be deleted automatically on Engine shutdown. > **Notice:** When using this lifetime management type, the GUI instance can be empty for the widget: it will be assigned automatically when adding the widget to a window. For a user interface, the Gui instance must be set via the *[setGui()](../../../api/library/gui/class.userinterface_cs.md#setGui_Gui_void)* method. |
| **MANUAL** = 3 | Lifetime of the widget or user interface is managed by the user. The widget/user interface should be deleted manually. > **Notice:** When using this lifetime management type, the GUI instance can be empty for the widget: it will be assigned automatically when adding the widget to a window. For a user interface, the Gui instance must be set via the *[setGui()](../../../api/library/gui/class.userinterface_cs.md#setGui_Gui_void)* method. |

### Properties

## 🔒︎ int NumChildren

The number of child widgets.
## int FontWrap

The value indicating if text wrapping to widget width is enabled.
## int FontRich

The value indicating if rich text formatting is used.
## int FontOutline

The value indicating if widget text is rendered casting a shadow. Positive or negative values determine the distance in pixels used to offset the font outline.
## int FontVOffset

The vertical offset of the font used by the widget.
## int FontHOffset

The horizontal offset of the font used by the widget.
## int FontVSpacing

The spacing (in pixels) between widget text lines.
## int FontHSpacing

The spacing (in pixels) between widget text characters.
## int FontPermanent

The flag indicating if color of the widget text is not changed (for example, when the widget becomes inactive or loses focus).
## vec4 FontColor

The color of the font used by the widget.
## int FontSize

The size of the font used by the widget.
## int MouseCursor

The mouse pointer set for the widget.
## 🔒︎ int MouseY

The Y coordinate of the mouse pointer position in the widget's local space.
## 🔒︎ int MouseX

The X coordinate of the mouse pointer position in the widget's local space.
## int Height

The widget minimal height.
> **Notice:** The widget cannot be smaller than its content (the texture, video, etc.). It is only possible to make the widget bigger then the size of its content. For example, [WidgetButton](../../../api/library/gui/class.widgetbutton_cs.md) can be made bigger than its texture, but it cannot be made any smaller than the texture dimensions.


## int Width

The widget minimal width.
> **Notice:** The widget cannot be smaller than its content (the texture, video, etc.). It is only possible to make the widget bigger then the size of its content. For example, [WidgetButton](../../../api/library/gui/class.widgetbutton_cs.md) can be made bigger than its texture, but it cannot be made any smaller than the texture dimensions.


## 🔒︎ int ScreenPositionY

The screen position of the widget (its top left corner) on the screen along the y axis.
## 🔒︎ int ScreenPositionX

The screen position of the widget (its top left corner) on the screen along the x axis.
## int PositionY

The Y coordinate of the widget position relative to its parent.
## int PositionX

The X coordinate of the widget position relative to its parent.
## Widget NextFocus

The widget which will be focused next if the user presses **TAB**.
## string Data

The user data associated with the widget.
## int Order

The rendering order (Z-order) for the widget. The higher the value, the higher the order of the widget is.
> **Notice:** Works only for widgets added to GUI via the [*Gui.AddChild()*](../../../api/library/gui/class.gui_cs.md#addChild_Widget_int_void) function with the [Gui.ALIGN_OVERLAP](../../../api/library/gui/class.gui_cs.md#ALIGN_OVERLAP) flag specified (should not be [Gui.ALIGN_FIXED](../../../api/library/gui/class.gui_cs.md#ALIGN_FIXED)).


## bool Hidden

The value indicating if the widget is hidden.
## bool Enabled

The value indicating if the widget is enabled (the user can interact with the widget).
## bool IntersectionEnabled

The value indicating if intersection detection is enabled for the widget.
## int Flags

The widget flags.
## Widget Parent

The pointer to the parent widget.
## 🔒︎ Gui ParentGui

The [Gui](../../../api/library/gui/class.gui_cs.md) instance that currently renders the widget's parent, if the widget has a parent. (This function can be used if the widget is created and used in two different GUIs, for example, in case of the Interface plugin.)
## 🔒︎ Gui Gui

The [Gui](../../../api/library/gui/class.gui_cs.md) instance that renders the widget. (This function can be used if the widget is created and used in two different GUIs, for example, in case of the Interface plugin.) It can be called only by root widgets. For child widgets, see *[ParentGui](#getParentGui_Gui)*.
## 🔒︎ string TypeName

The name of the widget type.
## 🔒︎ Widget.TYPE Type

The type of the widget.
## 🔒︎ bool IsLayout

The value indicating if the widget is a layout.
## 🔒︎ bool IsFixed

The value indicating if the widget is fixed.
## 🔒︎ bool IsBackground

The value indicating if the widget is a background one.
## 🔒︎ bool IsOverlapped

The value indicating if the widget is overlapped.
## 🔒︎ bool IsExpanded

The value indicating if the widget is expanded.
## Widget.LIFETIME Lifetime

The lifetime management type for the root of the widget, or for the widget itself (if it is not a child for another widget).
> **Notice:** Lifetime of each widget in the hierarchy is defined by its root. Thus, lifetime management type set for a child widget that differs from the one set for the root is ignored.

. One of the [LIFETIME_*](#LIFETIME) variables.
## 🔒︎ float DpiScale

The DPI scale applied to the widget.
## 🔒︎ int RenderHeight

The widget frame height in pixels.
## 🔒︎ int RenderWidth

The widget frame width in pixels.
## 🔒︎ Event< Widget > EventRemove

The event triggered when a widget is removed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Remove event handler
void remove_event_handler(Widget widget)
{
	Log.Message("\Handling Remove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections remove_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventRemove.Connect(remove_event_connections, remove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventRemove.Connect(remove_event_connections, (Widget widget) => {
		Log.Message("Handling Remove event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
remove_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Remove event with a handler function
publisher.EventRemove.Connect(remove_event_handler);

// remove subscription to the Remove event later by the handler function
publisher.EventRemove.Disconnect(remove_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection remove_event_connection;

// subscribe to the Remove event with a lambda handler function and keeping the connection
remove_event_connection = publisher.EventRemove.Connect((Widget widget) => {
		Log.Message("Handling Remove event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
remove_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
remove_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
remove_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Remove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventRemove.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventRemove.Enabled = true;

```

</details>

## 🔒︎ Event< Widget , Widget > EventDragDrop

The event triggered when a drag-and-drop operation is performed with a widget. Supported by all widgets. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**, Widget **target_widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the DragDrop event handler
void dragdrop_event_handler(Widget widget,  Widget target_widget)
{
	Log.Message("\Handling DragDrop event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections dragdrop_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventDragDrop.Connect(dragdrop_event_connections, dragdrop_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventDragDrop.Connect(dragdrop_event_connections, (Widget widget,  Widget target_widget) => {
		Log.Message("Handling DragDrop event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
dragdrop_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the DragDrop event with a handler function
publisher.EventDragDrop.Connect(dragdrop_event_handler);

// remove subscription to the DragDrop event later by the handler function
publisher.EventDragDrop.Disconnect(dragdrop_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection dragdrop_event_connection;

// subscribe to the DragDrop event with a lambda handler function and keeping the connection
dragdrop_event_connection = publisher.EventDragDrop.Connect((Widget widget,  Widget target_widget) => {
		Log.Message("Handling DragDrop event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
dragdrop_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
dragdrop_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
dragdrop_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring DragDrop events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventDragDrop.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventDragDrop.Enabled = true;

```

</details>

## 🔒︎ Event< Widget , Widget > EventDragMove

The event triggered when a focused widget is moved. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**, Widget **underlying_widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the DragMove event handler
void dragmove_event_handler(Widget widget,  Widget underlying_widget)
{
	Log.Message("\Handling DragMove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections dragmove_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventDragMove.Connect(dragmove_event_connections, dragmove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventDragMove.Connect(dragmove_event_connections, (Widget widget,  Widget underlying_widget) => {
		Log.Message("Handling DragMove event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
dragmove_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the DragMove event with a handler function
publisher.EventDragMove.Connect(dragmove_event_handler);

// remove subscription to the DragMove event later by the handler function
publisher.EventDragMove.Disconnect(dragmove_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection dragmove_event_connection;

// subscribe to the DragMove event with a lambda handler function and keeping the connection
dragmove_event_connection = publisher.EventDragMove.Connect((Widget widget,  Widget underlying_widget) => {
		Log.Message("Handling DragMove event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
dragmove_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
dragmove_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
dragmove_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring DragMove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventDragMove.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventDragMove.Enabled = true;

```

</details>

## 🔒︎ Event< Widget > EventLeave

The event triggered when the mouse pointer leaves a widget. Supported by all widgets. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Leave event handler
void leave_event_handler(Widget widget)
{
	Log.Message("\Handling Leave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections leave_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventLeave.Connect(leave_event_connections, leave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventLeave.Connect(leave_event_connections, (Widget widget) => {
		Log.Message("Handling Leave event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
leave_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Leave event with a handler function
publisher.EventLeave.Connect(leave_event_handler);

// remove subscription to the Leave event later by the handler function
publisher.EventLeave.Disconnect(leave_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection leave_event_connection;

// subscribe to the Leave event with a lambda handler function and keeping the connection
leave_event_connection = publisher.EventLeave.Connect((Widget widget) => {
		Log.Message("Handling Leave event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
leave_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
leave_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
leave_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Leave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventLeave.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventLeave.Enabled = true;

```

</details>

## 🔒︎ Event< Widget > EventEnter

The event triggered when the mouse pointer enters a widget. Supported by all widgets. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Enter event handler
void enter_event_handler(Widget widget)
{
	Log.Message("\Handling Enter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enter_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEnter.Connect(enter_event_connections, enter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEnter.Connect(enter_event_connections, (Widget widget) => {
		Log.Message("Handling Enter event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
enter_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Enter event with a handler function
publisher.EventEnter.Connect(enter_event_handler);

// remove subscription to the Enter event later by the handler function
publisher.EventEnter.Disconnect(enter_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection enter_event_connection;

// subscribe to the Enter event with a lambda handler function and keeping the connection
enter_event_connection = publisher.EventEnter.Connect((Widget widget) => {
		Log.Message("Handling Enter event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
enter_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
enter_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
enter_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Enter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEnter.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEnter.Enabled = true;

```

</details>

## 🔒︎ Event< Widget , uint> EventTextPressed

The event triggered when a virtual key is pressed while a widget is in focus. Supported by the following widgets:
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cs.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cs.md)

 **Virtual key** - is a value to which a scan code was converted by an Operating System (e.g., the **Q** scan code will have the **Q** virtual key on a *QWERTY*-keyboard, while on an *AZERTY*-keyboard it will have the **A** virtual key; or **NUMPAD_DIGIT_7** scan code can be translated into virtual **NUMPAD_HOME** or **NUMPAD_DIGIT_7** depending on the current *Num Lock* state. Virtual keys are used, when it is important to know what exactly did user type (not just the physical button, but rather a letter).
 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**, uint **unicode**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TextPressed event handler
void textpressed_event_handler(Widget widget,  uint unicode)
{
	Log.Message("\Handling TextPressed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections textpressed_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventTextPressed.Connect(textpressed_event_connections, textpressed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventTextPressed.Connect(textpressed_event_connections, (Widget widget,  uint unicode) => {
		Log.Message("Handling TextPressed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
textpressed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TextPressed event with a handler function
publisher.EventTextPressed.Connect(textpressed_event_handler);

// remove subscription to the TextPressed event later by the handler function
publisher.EventTextPressed.Disconnect(textpressed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection textpressed_event_connection;

// subscribe to the TextPressed event with a lambda handler function and keeping the connection
textpressed_event_connection = publisher.EventTextPressed.Connect((Widget widget,  uint unicode) => {
		Log.Message("Handling TextPressed event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
textpressed_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
textpressed_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
textpressed_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TextPressed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventTextPressed.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventTextPressed.Enabled = true;

```

</details>

## 🔒︎ Event< Widget , int> EventKeyPressed

The event triggered when a key (by a scan code) is pressed while a widget is in focus. Supported by the following widgets:
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cs.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cs.md)

 **Scan code** - is a code assigned to avery key on the keyboard. Keyboard drivers use scan codes to detect which key is pressed. Scan codes are assigned to keys on the hardware level and are not affected by the states of modifiers like *Caps Lock*, *Num Lock*, *Scroll Lock*, *Shift*, *Alt*, and *Ctrl* making it possible to implement identical control on different types of keyboards (*uiQWERTY*, *AZERTY*, *QWERTC*, etc.). Scan codes are used when only a physical position of a key (a button) is important (e.g. in the *ControlsApp* class or Console key).
 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**, int **key**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the KeyPressed event handler
void keypressed_event_handler(Widget widget,  int key)
{
	Log.Message("\Handling KeyPressed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections keypressed_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventKeyPressed.Connect(keypressed_event_connections, keypressed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventKeyPressed.Connect(keypressed_event_connections, (Widget widget,  int key) => {
		Log.Message("Handling KeyPressed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
keypressed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the KeyPressed event with a handler function
publisher.EventKeyPressed.Connect(keypressed_event_handler);

// remove subscription to the KeyPressed event later by the handler function
publisher.EventKeyPressed.Disconnect(keypressed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection keypressed_event_connection;

// subscribe to the KeyPressed event with a lambda handler function and keeping the connection
keypressed_event_connection = publisher.EventKeyPressed.Connect((Widget widget,  int key) => {
		Log.Message("Handling KeyPressed event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
keypressed_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
keypressed_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
keypressed_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring KeyPressed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventKeyPressed.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventKeyPressed.Enabled = true;

```

</details>

## 🔒︎ Event< Widget , int> EventReleased

The event triggered when the mouse is released after clicking somewhere on a widget. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cs.md)
- [*WidgetGroupBox*](../../../api/library/gui/class.widgetgroupbox_cs.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cs.md)
- [*WidgetManipulatorRotator*](../../../api/library/gui/class.widgetmanipulatorrotator_cs.md) (**mouse_buttons** is always 0)
- [*WidgetManipulatorScaler*](../../../api/library/gui/class.widgetmanipulatorscaler_cs.md) (**mouse_buttons** is always 0)
- [*WidgetManipulatorTranslator*](../../../api/library/gui/class.widgetmanipulatortranslator_cs.md) (**mouse_buttons** is always 0)
- [*WidgetSlider*](../../../api/library/gui/class.widgetslider_cs.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cs.md)
- [*WidgetSpinBoxDouble*](../../../api/library/gui/class.widgetspinboxdouble_cs.md)
- [*WidgetWindow*](../../../api/library/gui/class.widgetwindow_cs.md)
- [*EngineWindow*](../../../api/library/gui/class.enginewindow_cs.md) (**mouse_buttons** is always 0)

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**, int **mouse_buttons**)*
- The `mouse_buttons` argument is a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_RIGHT)*.


**Usage Example:**


```csharp
// auxiliary variable simplifying subscriptions management
EventConnections econn = new EventConnections();

// ...

// creating a button widget and adding it to GUI
WidgetButton widget_button = new WidgetButton(WindowManager.MainWindow.Gui, "button");
WindowManager.MainWindow.Gui.AddChild(widget_button, Gui.ALIGN_OVERLAP | Gui.ALIGN_FIXED);

// enabling Console onscreen overlay
Console.Onscreen = true;

// subscribing to the Released event with a lambda-handler displaying the list of released mouse buttons
widget_button.EventReleased.Connect(econn, (Widget widget, int mouse_buttons) => {
	bool left = (mouse_buttons & Gui.MOUSE_MASK_LEFT) == Gui.MOUSE_MASK_LEFT;
	bool right = (mouse_buttons & Gui.MOUSE_MASK_RIGHT) == Gui.MOUSE_MASK_RIGHT;
	bool middle = (mouse_buttons & Gui.MOUSE_MASK_MIDDLE) == Gui.MOUSE_MASK_MIDDLE;

	// displaying information on the currently released mouse buttons
	Console.OnscreenMessageLine(
		"EventReleased(mouse_buttons: {0} {1} {2})",
		left ? "left" : "",
		right ? "right" : "",
		middle ? "middle" : ""
	);
});

```


<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Released event handler
void released_event_handler(Widget widget,  int mouse_buttons)
{
	Log.Message("\Handling Released event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections released_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventReleased.Connect(released_event_connections, released_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventReleased.Connect(released_event_connections, (Widget widget,  int mouse_buttons) => {
		Log.Message("Handling Released event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
released_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Released event with a handler function
publisher.EventReleased.Connect(released_event_handler);

// remove subscription to the Released event later by the handler function
publisher.EventReleased.Disconnect(released_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection released_event_connection;

// subscribe to the Released event with a lambda handler function and keeping the connection
released_event_connection = publisher.EventReleased.Connect((Widget widget,  int mouse_buttons) => {
		Log.Message("Handling Released event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
released_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
released_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
released_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Released events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventReleased.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventReleased.Enabled = true;

```

</details>

## 🔒︎ Event< Widget , int> EventPressed

The event triggered when a mouse button or **ENTER** (**RETURN**) is pressed, while the mouse pointer is somewhere on a widget. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cs.md)
- [*WidgetCanvas*](../../../api/library/gui/class.widgetcanvas_cs.md)
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cs.md)
- [*WidgetSlider*](../../../api/library/gui/class.widgetslider_cs.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cs.md)
- [*WidgetLabel*](../../../api/library/gui/class.widgetlabel_cs.md)
- [*WidgetListBox*](../../../api/library/gui/class.widgetlistbox_cs.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cs.md)
- [*WidgetSprite*](../../../api/library/gui/class.widgetsprite_cs.md)
- [*WidgetWindow*](../../../api/library/gui/class.widgetwindow_cs.md)

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**, int **mouse_buttons**)*
- The `mouse_buttons` argument is a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_RIGHT)*.


**Usage Example:**


```csharp
// auxiliary variable simplifying subscriptions management
EventConnections econn = new EventConnections();

// ...

// creating a button widget and adding it to GUI
WidgetButton widget_button = new WidgetButton(WindowManager.MainWindow.Gui, "button");
WindowManager.MainWindow.Gui.AddChild(widget_button, Gui.ALIGN_OVERLAP | Gui.ALIGN_FIXED);

// enabling Console onscreen overlay
Console.Onscreen = true;

// subscribing to the Pressed event with a lambda-handler displaying the list of pressed mouse buttons
widget_button.EventPressed.Connect(econn, (Widget widget, int mouse_buttons) => {
	bool left = (mouse_buttons & Gui.MOUSE_MASK_LEFT) == Gui.MOUSE_MASK_LEFT;
	bool right = (mouse_buttons & Gui.MOUSE_MASK_RIGHT) == Gui.MOUSE_MASK_RIGHT;
	bool middle = (mouse_buttons & Gui.MOUSE_MASK_MIDDLE) == Gui.MOUSE_MASK_MIDDLE;

	// displaying information on the currently pressed mouse buttons
	Console.OnscreenMessageLine(
		"EventPressed(mouse_buttons: {0} {1} {2})",
		left ? "left" : "",
		right ? "right" : "",
		middle ? "middle" : ""
	);
});

```


<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Pressed event handler
void pressed_event_handler(Widget widget,  int mouse_buttons)
{
	Log.Message("\Handling Pressed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pressed_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventPressed.Connect(pressed_event_connections, pressed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventPressed.Connect(pressed_event_connections, (Widget widget,  int mouse_buttons) => {
		Log.Message("Handling Pressed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
pressed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Pressed event with a handler function
publisher.EventPressed.Connect(pressed_event_handler);

// remove subscription to the Pressed event later by the handler function
publisher.EventPressed.Disconnect(pressed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection pressed_event_connection;

// subscribe to the Pressed event with a lambda handler function and keeping the connection
pressed_event_connection = publisher.EventPressed.Connect((Widget widget,  int mouse_buttons) => {
		Log.Message("Handling Pressed event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
pressed_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
pressed_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
pressed_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Pressed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventPressed.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventPressed.Enabled = true;

```

</details>

## 🔒︎ Event< Widget > EventDoubleClicked

The event triggered when the mouse is double-clicked somewhere on a widget. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cs.md)
- [*WidgetCheckBox*](../../../api/library/gui/class.widgetcheckbox_cs.md)
- [*WidgetComboBox*](../../../api/library/gui/class.widgetcombobox_cs.md)
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cs.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cs.md)
- [*WidgetHPaned*](../../../api/library/gui/class.widgethpaned_cs.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cs.md)
- [*WidgetLabel*](../../../api/library/gui/class.widgetlabel_cs.md)
- [*WidgetListBox*](../../../api/library/gui/class.widgetlistbox_cs.md)
- [*WidgetManipulatorRotator*](../../../api/library/gui/class.widgetmanipulatorrotator_cs.md)
- [*WidgetManipulatorScaler*](../../../api/library/gui/class.widgetmanipulatorscaler_cs.md)
- [*WidgetManipulatorTranslator*](../../../api/library/gui/class.widgetmanipulatortranslator_cs.md)
- [*WidgetScroll*](../../../api/library/gui/class.widgetscroll_cs.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cs.md)
- [*WidgetTreeBox*](../../../api/library/gui/class.widgettreebox_cs.md)
- [*WidgetVPaned*](../../../api/library/gui/class.widgetvpaned_cs.md)
- [*WidgetWindow*](../../../api/library/gui/class.widgetwindow_cs.md)

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the DoubleClicked event handler
void doubleclicked_event_handler(Widget widget)
{
	Log.Message("\Handling DoubleClicked event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections doubleclicked_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventDoubleClicked.Connect(doubleclicked_event_connections, doubleclicked_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventDoubleClicked.Connect(doubleclicked_event_connections, (Widget widget) => {
		Log.Message("Handling DoubleClicked event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
doubleclicked_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the DoubleClicked event with a handler function
publisher.EventDoubleClicked.Connect(doubleclicked_event_handler);

// remove subscription to the DoubleClicked event later by the handler function
publisher.EventDoubleClicked.Disconnect(doubleclicked_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection doubleclicked_event_connection;

// subscribe to the DoubleClicked event with a lambda handler function and keeping the connection
doubleclicked_event_connection = publisher.EventDoubleClicked.Connect((Widget widget) => {
		Log.Message("Handling DoubleClicked event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
doubleclicked_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
doubleclicked_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
doubleclicked_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring DoubleClicked events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventDoubleClicked.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventDoubleClicked.Enabled = true;

```

</details>

## 🔒︎ Event< Widget , int> EventClicked

The event triggered when the mouse is clicked somewhere on a widget. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cs.md)
- [*WidgetCheckBox*](../../../api/library/gui/class.widgetcheckbox_cs.md)
- [*WidgetComboBox*](../../../api/library/gui/class.widgetcombobox_cs.md)
- [*WidgetDialog*](../../../api/library/gui/class.widgetdialog_cs.md)
- [*WidgetDialogFile*](../../../api/library/gui/class.widgetdialogfile_cs.md)
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cs.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cs.md)
- [*WidgetHPaned*](../../../api/library/gui/class.widgethpaned_cs.md)
- [*WidgetScroll*](../../../api/library/gui/class.widgetscroll_cs.md)
- [*WidgetSlider*](../../../api/library/gui/class.widgetslider_cs.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cs.md)
- [*WidgetLabel*](../../../api/library/gui/class.widgetlabel_cs.md)
- [*WidgetListBox*](../../../api/library/gui/class.widgetlistbox_cs.md)
- [*WidgetManipulatorRotator*](../../../api/library/gui/class.widgetmanipulatorrotator_cs.md)
- [*WidgetManipulatorScaler*](../../../api/library/gui/class.widgetmanipulatorscaler_cs.md)
- [*WidgetManipulatorTranslator*](../../../api/library/gui/class.widgetmanipulatortranslator_cs.md)
- [*WidgetMenuBox*](../../../api/library/gui/class.widgetmenubox_cs.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cs.md)
- [*WidgetSprite*](../../../api/library/gui/class.widgetsprite_cs.md)
- [*WidgetTreeBox*](../../../api/library/gui/class.widgettreebox_cs.md)
- [*WidgetVPaned*](../../../api/library/gui/class.widgetvpaned_cs.md)

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**, int **mouse_buttons**)*
- The `mouse_buttons` argument is a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_RIGHT)*.


**Usage Example:**


```csharp
// auxiliary variable simplifying subscriptions management
EventConnections econn = new EventConnections();

// ...

// creating a button widget and adding it to GUI
WidgetButton widget_button = new WidgetButton(WindowManager.MainWindow.Gui, "button");
WindowManager.MainWindow.Gui.AddChild(widget_button, Gui.ALIGN_OVERLAP | Gui.ALIGN_FIXED);

// enabling Console onscreen overlay
Console.Onscreen = true;

// subscribing to the Clicked event with a lambda-handler displaying the list of clicked mouse buttons
widget_button.EventClicked.Connect(econn, (Widget widget, int mouse_buttons) => {
	bool left = (mouse_buttons & Gui.MOUSE_MASK_LEFT) == Gui.MOUSE_MASK_LEFT;
	bool right = (mouse_buttons & Gui.MOUSE_MASK_RIGHT) == Gui.MOUSE_MASK_RIGHT;
	bool middle = (mouse_buttons & Gui.MOUSE_MASK_MIDDLE) == Gui.MOUSE_MASK_MIDDLE;

	// displaying information on the currently clicked mouse buttons
	Console.OnscreenMessageLine(
		"EventClicked(mouse_buttons: {0} {1} {2})",
		left ? "left" : "",
		right ? "right" : "",
		middle ? "middle" : ""
	);
});

```


<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Clicked event handler
void clicked_event_handler(Widget widget,  int mouse_buttons)
{
	Log.Message("\Handling Clicked event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections clicked_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventClicked.Connect(clicked_event_connections, clicked_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventClicked.Connect(clicked_event_connections, (Widget widget,  int mouse_buttons) => {
		Log.Message("Handling Clicked event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
clicked_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Clicked event with a handler function
publisher.EventClicked.Connect(clicked_event_handler);

// remove subscription to the Clicked event later by the handler function
publisher.EventClicked.Disconnect(clicked_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection clicked_event_connection;

// subscribe to the Clicked event with a lambda handler function and keeping the connection
clicked_event_connection = publisher.EventClicked.Connect((Widget widget,  int mouse_buttons) => {
		Log.Message("Handling Clicked event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
clicked_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
clicked_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
clicked_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Clicked events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventClicked.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventClicked.Enabled = true;

```

</details>

## 🔒︎ Event< Widget > EventChanged

The event triggered when a widget has changed its state. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cs.md)
- [*WidgetCheckBox*](../../../api/library/gui/class.widgetcheckbox_cs.md)
- [*WidgetComboBox*](../../../api/library/gui/class.widgetcombobox_cs.md)
- [*WidgetDialogColor*](../../../api/library/gui/class.widgetdialogcolor_cs.md)
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cs.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cs.md)
- [*WidgetHPaned*](../../../api/library/gui/class.widgethpaned_cs.md)
- [*WidgetScroll*](../../../api/library/gui/class.widgetscroll_cs.md)
- [*WidgetScrollBox*](../../../api/library/gui/class.widgetscrollbox_cs.md)
- [*WidgetSlider*](../../../api/library/gui/class.widgetslider_cs.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cs.md)
- [*WidgetLabel*](../../../api/library/gui/class.widgetlabel_cs.md)
- [*WidgetListBox*](../../../api/library/gui/class.widgetlistbox_cs.md)
- [*WidgetManipulator*](../../../api/library/gui/class.widgetmanipulator_cs.md)
- [*WidgetManipulatorRotator*](../../../api/library/gui/class.widgetmanipulatorrotator_cs.md)
- [*WidgetManipulatorScaler*](../../../api/library/gui/class.widgetmanipulatorscaler_cs.md)
- [*WidgetManipulatorTranslator*](../../../api/library/gui/class.widgetmanipulatortranslator_cs.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cs.md)
- [*WidgetSpinBoxDouble*](../../../api/library/gui/class.widgetspinboxdouble_cs.md)
- [*WidgetTabBox*](../../../api/library/gui/class.widgettabbox_cs.md)
- [*WidgetTreeBox*](../../../api/library/gui/class.widgettreebox_cs.md)
- [*WidgetVPaned*](../../../api/library/gui/class.widgetvpaned_cs.md)

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Changed event handler
void changed_event_handler(Widget widget)
{
	Log.Message("\Handling Changed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections changed_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventChanged.Connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventChanged.Connect(changed_event_connections, (Widget widget) => {
		Log.Message("Handling Changed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Changed event with a handler function
publisher.EventChanged.Connect(changed_event_handler);

// remove subscription to the Changed event later by the handler function
publisher.EventChanged.Disconnect(changed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection changed_event_connection;

// subscribe to the Changed event with a lambda handler function and keeping the connection
changed_event_connection = publisher.EventChanged.Connect((Widget widget) => {
		Log.Message("Handling Changed event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
changed_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
changed_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
changed_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventChanged.Enabled = true;

```

</details>

## 🔒︎ Event< Widget > EventFocusOut

The event triggered when a widget loses focus. Supported by all widgets. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FocusOut event handler
void focusout_event_handler(Widget widget)
{
	Log.Message("\Handling FocusOut event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focusout_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFocusOut.Connect(focusout_event_connections, focusout_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFocusOut.Connect(focusout_event_connections, (Widget widget) => {
		Log.Message("Handling FocusOut event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
focusout_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FocusOut event with a handler function
publisher.EventFocusOut.Connect(focusout_event_handler);

// remove subscription to the FocusOut event later by the handler function
publisher.EventFocusOut.Disconnect(focusout_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection focusout_event_connection;

// subscribe to the FocusOut event with a lambda handler function and keeping the connection
focusout_event_connection = publisher.EventFocusOut.Connect((Widget widget) => {
		Log.Message("Handling FocusOut event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
focusout_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
focusout_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
focusout_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FocusOut events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFocusOut.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFocusOut.Enabled = true;

```

</details>

## 🔒︎ Event< Widget > EventFocusIn

The event triggered when a widget is focused. Supported by all widgets. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FocusIn event handler
void focusin_event_handler(Widget widget)
{
	Log.Message("\Handling FocusIn event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focusin_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFocusIn.Connect(focusin_event_connections, focusin_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFocusIn.Connect(focusin_event_connections, (Widget widget) => {
		Log.Message("Handling FocusIn event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
focusin_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FocusIn event with a handler function
publisher.EventFocusIn.Connect(focusin_event_handler);

// remove subscription to the FocusIn event later by the handler function
publisher.EventFocusIn.Disconnect(focusin_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection focusin_event_connection;

// subscribe to the FocusIn event with a lambda handler function and keeping the connection
focusin_event_connection = publisher.EventFocusIn.Connect((Widget widget) => {
		Log.Message("Handling FocusIn event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
focusin_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
focusin_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
focusin_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FocusIn events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFocusIn.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFocusIn.Enabled = true;

```

</details>

## 🔒︎ Event< Widget > EventHide

The event triggered when a widget is removed using [*Gui::removeChild()*](../../../api/library/gui/class.gui_cs.md#removeChild_Widget_void). Supported by all widgets. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Hide event handler
void hide_event_handler(Widget widget)
{
	Log.Message("\Handling Hide event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections hide_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventHide.Connect(hide_event_connections, hide_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventHide.Connect(hide_event_connections, (Widget widget) => {
		Log.Message("Handling Hide event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
hide_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Hide event with a handler function
publisher.EventHide.Connect(hide_event_handler);

// remove subscription to the Hide event later by the handler function
publisher.EventHide.Disconnect(hide_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection hide_event_connection;

// subscribe to the Hide event with a lambda handler function and keeping the connection
hide_event_connection = publisher.EventHide.Connect((Widget widget) => {
		Log.Message("Handling Hide event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
hide_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
hide_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
hide_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Hide events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventHide.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventHide.Enabled = true;

```

</details>

## 🔒︎ Event< Widget > EventShow

The event triggered when a widget is shown. Supported by all widgets. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Widget **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Show event handler
void show_event_handler(Widget widget)
{
	Log.Message("\Handling Show event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections show_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventShow.Connect(show_event_connections, show_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventShow.Connect(show_event_connections, (Widget widget) => {
		Log.Message("Handling Show event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
show_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Show event with a handler function
publisher.EventShow.Connect(show_event_handler);

// remove subscription to the Show event later by the handler function
publisher.EventShow.Disconnect(show_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection show_event_connection;

// subscribe to the Show event with a lambda handler function and keeping the connection
show_event_connection = publisher.EventShow.Connect((Widget widget) => {
		Log.Message("Handling Show event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
show_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
show_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
show_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Show events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventShow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventShow.Enabled = true;

```

</details>

## Gui.TextDirection TextDirection

The base paragraph direction for this widget's text, one of the *Gui::TEXT_DIRECTION_** values. With *TEXT_DIRECTION_AUTO* (default) the direction is inherited from the **[GlobalTextDirection](../../../api/library/gui/class.gui_cs.md#getGlobalTextDirection_int)** property of the GUI, and if that is also set to auto, it is detected from the text content.
### Members

---

## Widget GetChild ( int num )

Returns a child widget with a given number.
### Arguments

- *int* **num** - Widget number.

### Return value

Required widget.
## int IsChild ( Widget w )

Checks if a given widget is a child of the current one.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **w** - Widget to check.

### Return value

**1** if the widget in question is a child; otherwise, **0**.
## void SetFocus ( )

Sets focus on the widget.
## int IsFocused ( )

Returns a value indicating if the widget is currently in focus.
### Return value

1 if the widget is in focus; otherwise, 0.
## void SetFont ( string name )

Sets a true-type font (*.ttf) that will be used to render text on the widget by file path.
### Arguments

- *string* **name** - Path to the font file (`*.ttf`) stored in your project's `data` folder.

## bool GetIntersection ( int local_pos_x , int local_pos_y )

Checks for an intersection with the widget's bounds for the given point.
### Arguments

- *int* **local_pos_x** - Local X coordinate.
- *int* **local_pos_y** - Local Y coordinate.

### Return value

true if the input coordinate is inside the widget; otherwise, false.
## Widget GetHierarchyIntersection ( int screen_pos_x , int screen_pos_y )

Checks for an intersection with a widget that belongs to the hierarchy of the current widget.
### Arguments

- *int* **screen_pos_x** - The X coordinate of the screen position.
- *int* **screen_pos_y** - The Y coordinate of the screen position.

### Return value

Widget the intersection with which is found.
## int GetKeyActivity ( uint key )

Checks if a given key already has a special purpose for the widget.
### Arguments

- *uint* **key** - ASCII key code: one of the *[Input.KEY.*](../../../api/library/controls/class.input_cs.md#KEY_UNKNOWN)*values.

### Return value

1 if the key cannot be used; otherwise, 0.
## void SetPermanentFocus ( )

Sets permanent focus on the widget (it means that the widget is always in focus).
## void SetPosition ( int x , int y )

Sets a position of the widget relative to its parent in [logical units](../../../principles/dpi/index.md).
### Arguments

- *int* **x** - X coordinate of the upper left corner of the widget in [logical units](../../../principles/dpi/index.md).
- *int* **y** - Y coordinate of the upper left corner of the widget in [logical units](../../../principles/dpi/index.md).

## void SetToolTip ( string str , int reset = 0 )

Sets a tooltip for the widget.
### Arguments

- *string* **str** - Tooltip text.
- *int* **reset** - **1** to recalculate a tooltip location if the mouse cursor was relocated; otherwise � **0**(by default).

## string GetToolTip ( )

Returns the widget's tooltip text.
### Return value

Tooltip text.
## void AddAttach ( Widget w , string format = 0 , int multiplier = 1 , int flags = 0 )

Attaches a given widget to the current one. When applied to checkboxes, converts them into a group of radio buttons. A horizontal/vertical slider can be attached to a label or a text field. The text field can be attached to any of the sliders.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **w** - Widget to attach.
- *string* **format** - Format string for values entered into the attached widget. If none specified, **"%d"** is implied. This is an optional parameter.
- *int* **multiplier** - Multiplier value, which is used to scale values provided by the attached widget. This is an optional parameter.
- *int* **flags** - One of the [*ATTACH_**](../../../api/library/gui/class.gui_cs.md) pre-defined variables. This is an optional parameter.

## void AddChild ( Widget w , int flags = 0 )

Adds a child to the widget.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **w** - Child widget.
- *int* **flags** - One of the [*ALIGN_**](../../../api/library/gui/class.gui_cs.md) pre-defined variables. This is an optional parameter.

## void Arrange ( )

Rearranges the widget and its children to lay them out neatly. This function forces to recalculate widget size and allows to get updated GUI layout data in the current frame. If this function is not called, widget modifications made in the current *update()* will be available only in the next frame (i.e. with one-frame lag), as GUI is calculated and rendered after the script *update()* function has been executed.
## void Raise ( Widget w )

Brings a given widget to the top.
> **Notice:** Works only for widgets added to GUI via the [*Gui.addChild()*](../../../api/library/gui/class.gui_cs.md#addChild_Widget_int_void) function with the [Gui.ALIGN_OVERLAP](../../../api/library/gui/class.gui_cs.md#ALIGN_OVERLAP) flag specified (should not be [Gui.ALIGN_FIXED](../../../api/library/gui/class.gui_cs.md#ALIGN_FIXED)).


### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **w** - Widget to be brought up.

## void RemoveAttach ( Widget w )

Detaches a given widget from the current one.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **w** - Widget to detach.

## void RemoveChild ( Widget w )

Removes a child widget from the list of the widget's children.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **w** - Child widget.

## void RemoveFocus ( )

Removes focus from the widget.
## void ReplaceChild ( Widget w , Widget old_w , int flags = 0 )

Replaces one child widget with another.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **w** - Replacement widget.
- *[Widget](../../../api/library/gui/class.widget_cs.md)* **old_w** - Widget to be replaced.
- *int* **flags** - One of the [*ALIGN_**](../../../api/library/gui/class.gui_cs.md) pre-defined variables. This is an optional parameter.

## Widget.LIFETIME GetLifetimeSelf ( )

Returns the lifetime management type set for the widget.
> **Notice:** Lifetime of each widget in the hierarchy is defined by it's root. Setting lifetime management type for a child widget different from the one set for the root has no effect.


## int ToRenderSize ( int unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *int* **unit_size** - Size in units.

### Return value

Size in pixels.
## int ToUnitSize ( int render_size )

Transforms the pixel value to the unit value.
### Arguments

- *int* **render_size** - Size in pixels.

### Return value

Size in units.
## ivec2 ToRenderSize ( ivec2 unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *ivec2* **unit_size** - Size in units.

### Return value

Size in pixels.
## ivec2 ToUnitSize ( ivec2 render_size )

Transforms the pixel value to the unit value.
### Arguments

- *ivec2* **render_size** - Size in pixels.

### Return value

Size in units.
## ivec2 GetTextRenderSize ( char[] OUT_text )

Returns the size (in pixels) of the specified text string rendered on the screen with taking into account all text output settings such as dpi, font size and style.
### Arguments

- *char[]* **OUT_text** - Text string. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Text size in pixels.
## void RunEventShow ( )

Emulates the *[Show](#getEventShow_Event)* event.
## void RunEventHide ( )

Emulates the *[Hide](#getEventHide_Event)* event.
## void RunEventFocusIn ( )

Emulates the *[FocusIn](#getEventFocusIn_Event)* event.
## void RunEventFocusOut ( )

Emulates the *[FocusOut](#getEventFocusOut_Event)* event.
## void RunEventChanged ( )

Emulates the *[Changed](#getEventChanged_Event)* event.
## void RunEventClicked ( int mouse_buttons )

Emulates the *[Clicked](#getEventClicked_Event)* event.
### Arguments

- *int* **mouse_buttons** - Mouse button - a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_RIGHT)*.

## void RunEventDoubleClicked ( )

Emulates the *[DoubleClicked](#getEventDoubleClicked_Event)* event.
## void RunEventPressed ( int mouse_buttons )

Emulates the *[Pressed](#getEventPressed_Event)* event.
### Arguments

- *int* **mouse_buttons** - Mouse button - a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_RIGHT)*.

## void RunEventReleased ( int mouse_buttons )

Emulates the *[Released](#getEventReleased_Event)* event.
### Arguments

- *int* **mouse_buttons** - Mouse button - a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cs.md#MOUSE_MASK_RIGHT)*.

## void RunEventKeyPressed ( int key )

Emulates the *[KeyPressed](#getEventKeyPressed_Event)* event.
### Arguments

- *int* **key** - Key scan code.

## void RunEventTextPressed ( uint code )

Emulates the *[TextPressed](#getEventTextPressed_Event)* event.
### Arguments

- *uint* **code** - Vistual key.

## void RunEventEnter ( )

Emulates the *[Enter](#getEventEnter_Event)* event.
## void RunEventLeave ( )

Emulates the *[Leave](#getEventLeave_Event)* event.
## void RunEventDragMove ( Widget pointer )

Emulates the *[DragMove](#getEventDragMove_Event)* event.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **pointer** - Underlying widget.

## void RunEventDragDrop ( Widget pointer )

Emulates the *[DragDrop](#getEventDragDrop_Event)* event.
### Arguments

- *[Widget](../../../api/library/gui/class.widget_cs.md)* **pointer** - Target widget.

## ivec2 GetTextUnitSize ( string text )

Returns the text dimensions (width and height in logical unit). This function helps you estimate how well the text will fit in the widget before rendering.
### Arguments

- *string* **text** - Text string.

### Return value

Text size in logical unit (width, height).
