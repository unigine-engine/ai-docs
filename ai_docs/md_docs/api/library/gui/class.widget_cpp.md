# Unigine::Widget Class (CPP)

**Header:** #include <UnigineWidgets.h>


This base class is used to create [graphical user interface](../../../objects/objects/gui/index.md) widgets of different types. The Widget class doesn't provide creating of a widget: you can create the required widget by using a constructor of the corresponding class inherited from the Widget class.


Widgets can be used separately or form a hierarchy.


### Working with Widgets


The example below demonstrates how to create a single widget, a hierarchy of widgets, and subscribe for a widget's event.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
#include "AppWorldLogic.h"
#include <UnigineWidgets.h>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

void on_button_click(const WidgetPtr& button, int mbuttons)
{
	Log::message("world button click\n");
}

int AppWorldLogic::init()
{
	// create a single widget
	WidgetButtonPtr button = WidgetButton::create("WORLD_BUTTON");
	// subscribe for the Clicked event
	button->getEventClicked().connect(econnections, on_button_click);
	// add the button to WindowManager
	WindowManager::getMainWindow()->addChild(button);

	// create a hierarchy of widgets
	WidgetHBoxPtr hbox = WidgetHBox::create();
	hbox->setBackground(1);
	hbox->setBackgroundColor(Math::vec4_white);
	WindowManager::getMainWindow()->addChild(hbox, Gui::ALIGN_EXPAND);

	WidgetGroupBoxPtr group = WidgetGroupBox::create();
	group->setBackground(1);
	group->setText("Widgets Hierarchy");
	hbox->addChild(group);

	group->addChild(WidgetLabel::create("hierarchy_label_0"));
	group->addChild(WidgetLabel::create("hierarchy_label_1"));

	return 1;
}

int AppWorldLogic::shutdown()
{
	// removing all event subscriptions somewhere on shutdown
	econnections.disconnectAll();

	return 1;
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
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
#include "AppWorldLogic.h"
#include <UnigineWidgets.h>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econn;

void on_button_click(const WidgetPtr &button, int mbuttons)
{
	Log::message("world button click\n");
}

void on_button_remove(const WidgetPtr &button)
{
	Log::message("world button removed\n");
}

void on_hbox_remove(const WidgetPtr &hbox)
{
	Log::message("world hbox hierarchy removed\n");
}

int AppWorldLogic::init()
{

	// single world widget
	WidgetButtonPtr button = WidgetButton::create("WORLD_BUTTON");
	button->setLifetime(Widget::LIFETIME_WORLD);
	button->getEventClicked().connect(econn, on_button_click);
	button->getEventRemove().connect(econn, on_button_remove);
	WindowManager::getMainWindow()->addChild(button);

	// world hierarchy
	WidgetHBoxPtr hbox = WidgetHBox::create();
	hbox->setLifetime(Widget::LIFETIME_WORLD);
	hbox->getEventRemove().connect(econn, on_hbox_remove);
	hbox->setBackground(1);
	hbox->setBackgroundColor(Math::vec4_red);
	WindowManager::getMainWindow()->addChild(hbox, Gui::ALIGN_EXPAND);

	WidgetGroupBoxPtr group = WidgetGroupBox::create();
	group->setBackground(1);
	group->setText("World Hierarchy");
	hbox->addChild(group);

	group->addChild(WidgetLabel::create("hierarchy_world_label_0"));
	group->addChild(WidgetLabel::create("hierarchy_world_label_1"));

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


##### Managing Lifetime by the Window


In this example, widgets appear in a separate window. When you close the window, the widgets are deleted as their lifetime is managed by this *window*. The console shows the following information:

- Whether the window, button and hbox hierarchy are deleted or not.
- Whether the remove callbacks are fired or not.
- Messages from the remove callbacks.


After closing, the window can be re-created by pressing **T**.


<details>
<summary>AppSystemLogic.cpp | Close</summary>

`AppSystemLogic.cpp`


```cpp
#include "AppSystemLogic.h"
#include <UnigineWidgets.h>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

EngineWindowViewportPtr window;

WidgetButtonPtr button;
WidgetHBoxPtr hbox;

bool button_remove_handler = false;
bool hbox_remove_handler = false;

void on_window_button_click()
{
	Log::message("window button click\n");
}

void on_window_button_remove()
{
	Log::message("window button removed\n");
	button_remove_handler = true;
}

void on_window_hbox_remove()
{
	Log::message("window hbox hierarchy removed\n");
	hbox_remove_handler = true;
}

void create_window()
{

	button_remove_handler = false;
	hbox_remove_handler = false;

	window = EngineWindowViewport::create("Test", 512, 256, EngineWindow::FLAGS_SHOWN);

	// single window widget
	button = WidgetButton::create("WINDOW_BUTTON");
	button->setLifetime(Widget::LIFETIME_WINDOW);
	button->getEventClicked().connect(econnections, on_window_button_click);
	button->getEventRemove().connect(econnections, on_window_button_remove);
	window->addChild(button);

	// window hierarchy
	hbox = WidgetHBox::create();
	hbox->setLifetime(Widget::LIFETIME_WINDOW);
	hbox->getEventRemove().connect(econnections, on_window_hbox_remove);
	hbox->setBackground(1);
	hbox->setBackgroundColor(Math::vec4_red);
	window->addChild(hbox, Gui::ALIGN_EXPAND);

	WidgetGroupBoxPtr group = WidgetGroupBox::create();
	group->setBackground(1);
	group->setText("Window Hierarchy");
	hbox->addChild(group);

	group->addChild(WidgetLabel::create("hierarchy_window_label_0"));
	group->addChild(WidgetLabel::create("hierarchy_window_label_1"));

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

	Log::message("window deleted: %d, button deleted: %d, hbox deleted: %d, button remove handler: %d, hbox remove handler: %d\n",
		window.isDeleted(), button.isDeleted(), hbox.isDeleted(), button_remove_handler, hbox_remove_handler);

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


##### Managing Lifetime by the Engine


Widgets are created on Engine initialization, and then added to a separate window. The console shows the following information:


- Whether the window, button and hbox hierarchy are deleted or not.
- Whether the remove callbacks are fired or not.
- Messages from the remove callbacks.


If you close the window, it will be deleted and the information in the console will change. All the other widgets are deleted only on Engine shutdown, as their lifetime is managed by the Engine.


If the separate window is closed, press **T** to re-create it.


<details>
<summary>AppSystemLogic.cpp | Close</summary>

`AppSystemLogic.cpp`


```cpp
#include "AppSystemLogic.h"
#include <UnigineWidgets.h>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

EngineWindowViewportPtr engine_window;

WidgetButtonPtr engine_button;
WidgetHBoxPtr engine_hbox;

bool engine_button_remove_handler = false;
bool engine_hbox_remove_handler = false;

void on_engine_button_click(const WidgetPtr &button, int mbuttons)
{
	Log::message("engine button click\n");
}

void on_engine_button_remove(const WidgetPtr &button)
{
	Log::message("engine button removed\n");
	engine_button_remove_handler = true;
}

void on_engine_hbox_remove(const WidgetPtr &hbox)
{
	Log::message("engine hbox hierarchy removed\n");
	engine_hbox_remove_handler = true;
}

void create_engine_window()
{

	engine_window = EngineWindowViewport::create("Test", 512, 256, EngineWindow::FLAGS_SHOWN);

	engine_window->addChild(engine_button);
	engine_window->addChild(engine_hbox, Gui::ALIGN_EXPAND);

}

int AppSystemLogic::init()
{

	engine_button_remove_handler = false;
	engine_hbox_remove_handler = false;

	// single engine widget
	engine_button = WidgetButton::create("ENGINE_BUTTON");
	engine_button->setLifetime(Widget::LIFETIME_ENGINE);
	engine_button->getEventClicked().connect(econnections, on_engine_button_click);
	engine_button->getEventRemove().connect(econnections, on_engine_button_remove);

	// engine hierarchy
	engine_hbox = WidgetHBox::create();
	engine_hbox->setLifetime(Widget::LIFETIME_ENGINE);
	engine_hbox->getEventRemove().connect(econnections, on_engine_hbox_remove);
	engine_hbox->setBackground(1);
	engine_hbox->setBackgroundColor(Math::vec4_red);

	WidgetGroupBoxPtr engine_group = WidgetGroupBox::create();
	engine_group->setBackground(1);
	engine_group->setText("Engine Hierarchy");
	engine_hbox->addChild(engine_group);

	engine_group->addChild(WidgetLabel::create("hierarchy_engine_label_0"));
	engine_group->addChild(WidgetLabel::create("hierarchy_engine_label_1"));

	create_engine_window();

	return 1;
}

int AppSystemLogic::update()
{

	if (Input::isKeyDown(Input::KEY_T) && engine_window.isDeleted())
		create_engine_window();

	Log::message("engine window deleted: %d, engine button deleted: %d, engine hbox deleted: %d, engine button remove handler: %d, engine hbox remove handler: %d\n",
		engine_window.isDeleted(), engine_button.isDeleted(), engine_hbox.isDeleted(), engine_button_remove_handler, engine_hbox_remove_handler);

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
- A set of [UnigineScript samples](../../../code/uniginescript/samples/widgets.md) located in the `<UnigineSDK>/data/samples/widgets/` folder


## Widget Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **WIDGET_VBOX** = 0 | [Vertical box](../../../code/gui/ui/ui_containers.md#vbox). See also: [WidgetVBox](../../../api/library/gui/class.widgetvbox_cpp.md). |
| **WIDGET_HBOX** = 1 | [Horizontal box](../../../code/gui/ui/ui_containers.md#hbox). See also: [WidgetHBox](../../../api/library/gui/class.widgethbox_cpp.md). |
| **WIDGET_GRID_BOX** = 2 | [Grid box](../../../code/gui/ui/ui_containers.md#gridbox). See also: [WidgetGridBox](../../../api/library/gui/class.widgetgridbox_cpp.md). |
| **WIDGET_VPANED** = 3 | [Vertical box that allows resizing of its children](../../../code/gui/ui/ui_containers.md#vpaned). See also: [WidgetVPaned](../../../api/library/gui/class.widgetvpaned_cpp.md). |
| **WIDGET_HPANED** = 4 | [Horizontal box that allows resizing of its children](../../../code/gui/ui/ui_containers.md#hpaned). See also: [WidgetHPaned](../../../api/library/gui/class.widgethpaned_cpp.md). |
| **WIDGET_LABEL** = 5 | [Text label](../../../code/gui/ui/ui_widgets.md#label). See also: [WidgetLabel](../../../api/library/gui/class.widgetlabel_cpp.md). |
| **WIDGET_BUTTON** = 6 | [Simple button](../../../code/gui/ui/ui_widgets.md#button). See also: [WidgetButton](../../../api/library/gui/class.widgetbutton_cpp.md). |
| **WIDGET_EDIT_LINE** = 7 | [Text field](../../../code/gui/ui/ui_widgets.md#editline). See also: [WidgetEditline](../../../api/library/gui/class.widgeteditline_cpp.md). |
| **WIDGET_EDIT_TEXT** = 8 | [Multiline text field](../../../code/gui/ui/ui_widgets.md#edittext). See also: [WidgetEdittext](../../../api/library/gui/class.widgetedittext_cpp.md). |
| **WIDGET_CHECK_BOX** = 9 | [Checkbox](../../../code/gui/ui/ui_widgets.md#checkbox). See also: [WidgetCheckbox](../../../api/library/gui/class.widgetcheckbox_cpp.md). |
| **WIDGET_COMBO_BOX** = 10 | [Combobox](../../../code/gui/ui/ui_widgets.md#combobox). See also: [WidgetCombobox](../../../api/library/gui/class.widgetcombobox_cpp.md). |
| **WIDGET_CANVAS** = 11 | Canvas widget for drawing text, lines and polygons. See also: [WidgetCanvas](../../../api/library/gui/class.widgetcanvas_cpp.md). |
| **WIDGET_GROUP_BOX** = 12 | [Group box](../../../code/gui/ui/ui_containers.md#groupbox). See also: [WidgetGroupBox](../../../api/library/gui/class.widgetgroupbox_cpp.md). |
| **WIDGET_LIST_BOX** = 13 | [List box](../../../code/gui/ui/ui_widgets.md#listbox). See also: [WidgetListBox](../../../api/library/gui/class.widgetlistbox_cpp.md). |
| **WIDGET_TREE_BOX** = 14 | [Tree box](../../../code/gui/ui/ui_widgets.md#treebox). See also: [WidgetTreeBox](../../../api/library/gui/class.widgettreebox_cpp.md). |
| **WIDGET_TAB_BOX** = 15 | [Tabbed box](../../../code/gui/ui/ui_containers.md#tabbox). See also: [WidgetTabBox](../../../api/library/gui/class.widgettabbox_cpp.md). |
| **WIDGET_SCROLL** = 16 | A scrollbar: [horizontal](../../../code/gui/ui/ui_widgets.md#hscroll) or [vertical](../../../code/gui/ui/ui_widgets.md#vscroll) one. See also: [WidgetScroll](../../../api/library/gui/class.widgetscroll_cpp.md). |
| **WIDGET_SCROLL_BOX** = 17 | [Box with scrolling](../../../code/gui/ui/ui_containers.md#scrollbox). See also: [WidgetScrollBox](../../../api/library/gui/class.widgetscrollbox_cpp.md). |
| **WIDGET_SPACER** = 18 | Spacer: [horizontal](../../../code/gui/ui/ui_widgets.md#hspacer) or [vertical](../../../code/gui/ui/ui_widgets.md#vspacer) one. See also: [WidgetSpacer](../../../api/library/gui/class.widgetspacer_cpp.md). |
| **WIDGET_SLIDER** = 19 | A slider: [horizontal](../../../code/gui/ui/ui_widgets.md#hslider) or [vertical](../../../code/gui/ui/ui_widgets.md#vslider) one. See also: [WidgetSlider](../../../api/library/gui/class.widgetslider_cpp.md). |
| **WIDGET_SPIN_BOX** = 20 | [Spinbox](../../../code/gui/ui/ui_widgets.md#spinbox). See also: [WidgetSpinBox](../../../api/library/gui/class.widgetspinbox_cpp.md). |
| **WIDGET_SPIN_BOX_DOUBLE** = 21 | [Spinbox](../../../code/gui/ui/ui_widgets.md#spinbox) with double values. See also: [WidgetSpinBoxDouble](../../../api/library/gui/class.widgetspinboxdouble_cpp.md). |
| **WIDGET_ICON** = 22 | [Icon](../../../code/gui/ui/ui_widgets.md#icon). See also: [WidgetIcon](../../../api/library/gui/class.widgeticon_cpp.md). |
| **WIDGET_SPRITE** = 23 | [Sprite](../../../code/gui/ui/ui_widgets.md#sprite). See also: [WidgetSprite](../../../api/library/gui/class.widgetsprite_cpp.md). |
| **WIDGET_SPRITE_VIDEO** = 24 | Video Sprite. See also: [WidgetSpriteVideo](../../../api/library/gui/class.widgetspritevideo_cpp.md). |
| **WIDGET_SPRITE_SHADER** = 25 | Shader Sprite. See also: [WidgetSpriteShader](../../../api/library/gui/class.widgetspriteshader_cpp.md). |
| **WIDGET_SPRITE_VIEWPORT** = 26 | Viewport Sprite. See also: [WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md). |
| **WIDGET_SPRITE_NODE** = 27 | Node Sprite. See also: [WidgetSpriteNode](../../../api/library/gui/class.widgetspritenode_cpp.md). |
| **WIDGET_MENU_BAR** = 28 | [Menu bar](../../../code/gui/ui/ui_widgets.md#menubar). See also: [WidgetMenuBar](../../../api/library/gui/class.widgetmenubar_cpp.md). |
| **WIDGET_MENU_BOX** = 29 | [Menu](../../../code/gui/ui/ui_widgets.md#menubox). See also: [WidgetMenuBox](../../../api/library/gui/class.widgetmenubox_cpp.md). |
| **WIDGET_WINDOW** = 30 | [Window](../../../code/gui/ui/ui_containers.md#window). See also: [WidgetWindow](../../../api/library/gui/class.widgetwindow_cpp.md). |
| **WIDGET_DIALOG** = 31 | [Dialog window](../../../code/gui/ui/ui_containers.md#dialog). See also: [WidgetDialog](../../../api/library/gui/class.widgetdialog_cpp.md). |
| **WIDGET_DIALOG_MESSAGE** = 32 | Message Dialog. See also: [WidgetDialogMessage](../../../api/library/gui/class.widgetdialogmessage_cpp.md). |
| **WIDGET_DIALOG_FILE** = 33 | File Dialog. See also: [WidgetDialogFile](../../../api/library/gui/class.widgetdialogfile_cpp.md). |
| **WIDGET_DIALOG_COLOR** = 34 | Color Dialog. See also: [WidgetDialogColor](../../../api/library/gui/class.widgetdialogcolor_cpp.md). |
| **WIDGET_DIALOG_IMAGE** = 35 | Image Dialog. See also: [WidgetDialogImage](../../../api/library/gui/class.widgetdialogimage_cpp.md). |
| **WIDGET_MANIPULATOR** = 36 | Manipulator widget. See also: [WidgetManipulator](../../../api/library/gui/class.widgetmanipulator_cpp.md). |
| **WIDGET_MANIPULATOR_TRANSLATOR** = 37 | Translator Manipulator. See also: [WidgetManipulatorTranslator](../../../api/library/gui/class.widgetmanipulatortranslator_cpp.md). |
| **WIDGET_MANIPULATOR_ROTATOR** = 38 | Rotator Manipulator. See also: [WidgetManipulatorRotator](../../../api/library/gui/class.widgetmanipulatorrotator_cpp.md). |
| **WIDGET_MANIPULATOR_SCALER** = 39 | Scaler Manipulator. See also: [WidgetManipulatorScaler](../../../api/library/gui/class.widgetmanipulatorscaler_cpp.md). |
| **WIDGET_EXTERN** = 40 | External widget. |
| **WIDGET_ENGINE** = 41 | Engine-specific widget (manipulator). See also: [WidgetManipulator](../../../api/library/gui/class.widgetmanipulator_cpp.md). |
| **WIDGET_HIT_TEST_AREA** = 42 | Hit-Test Area. See also: [WidgetHitTestArea](../../../api/library/gui/class.widgethittestarea_cpp.md). |
| **NUM_WIDGETS** = 43 | Total number of widget types. |

## LIFETIME

| Name | Description |
|---|---|
| **LIFETIME_WORLD** = 0 | Lifetime of the widget or user interface is managed by the world. The widget/user interface will be deleted automatically on closing the world. |
| **LIFETIME_WINDOW** = 1 | Lifetime of the widget or user interface is managed by the window. The widget/user interface will be deleted automatically on deleting the window. |
| **LIFETIME_ENGINE** = 2 | Lifetime of the widget or user interface is managed by the Engine. The widget/user interface will be deleted automatically on Engine shutdown. > **Notice:** When using this lifetime management type, the GUI instance can be empty for the widget: it will be assigned automatically when adding the widget to a window. For a user interface, the Gui instance must be set via the *[setGui()](../../../api/library/gui/class.userinterface_cpp.md#setGui_Gui_void)* method. |
| **LIFETIME_MANUAL** = 3 | Lifetime of the widget or user interface is managed by the user. The widget/user interface should be deleted manually. > **Notice:** When using this lifetime management type, the GUI instance can be empty for the widget: it will be assigned automatically when adding the widget to a window. For a user interface, the Gui instance must be set via the *[setGui()](../../../api/library/gui/class.userinterface_cpp.md#setGui_Gui_void)* method. |

### Members

## int getNumChildren () const

Returns the current number of child widgets.
### Return value

Current number of child widgets.
## void setFontWrap ( int wrap )

Sets a new value indicating if text wrapping to widget width is enabled.
### Arguments

- *int* **wrap** - The value of 1 for text wrapping; otherwise, 0.

## int getFontWrap () const

Returns the current value indicating if text wrapping to widget width is enabled.
### Return value

Current value of 1 for text wrapping; otherwise, 0.
## void setFontRich ( int rich )

Sets a new value indicating if rich text formatting is used.
### Arguments

- *int* **rich** - The value of 1 for rich text formatting; otherwise, 0.

## int getFontRich () const

Returns the current value indicating if rich text formatting is used.
### Return value

Current value of 1 for rich text formatting; otherwise, 0.
## void setFontOutline ( int outline )

Sets a new value indicating if widget text is rendered casting a shadow. Positive or negative values determine the distance in pixels used to offset the font outline.
### Arguments

- *int* **outline** - The positive value if outline is offset in the bottom-right corner direction, negative value if outline is offset in the top-left corner direction. 0 if font is not outlined.

## int getFontOutline () const

Returns the current value indicating if widget text is rendered casting a shadow. Positive or negative values determine the distance in pixels used to offset the font outline.
### Return value

Current positive value if outline is offset in the bottom-right corner direction, negative value if outline is offset in the top-left corner direction. 0 if font is not outlined.
## void setFontVOffset ( int voffset )

Sets a new vertical offset of the font used by the widget.
### Arguments

- *int* **voffset** - The vertical offset value, in pixels.

## int getFontVOffset () const

Returns the current vertical offset of the font used by the widget.
### Return value

Current vertical offset value, in pixels.
## void setFontHOffset ( int hoffset )

Sets a new horizontal offset of the font used by the widget.
### Arguments

- *int* **hoffset** - The horizontal offset value, in pixels.

## int getFontHOffset () const

Returns the current horizontal offset of the font used by the widget.
### Return value

Current horizontal offset value, in pixels.
## void setFontVSpacing ( int vspacing )

Sets a new spacing (in pixels) between widget text lines.
### Arguments

- *int* **vspacing** - The vertical spacing value, in pixels.

## int getFontVSpacing () const

Returns the current spacing (in pixels) between widget text lines.
### Return value

Current vertical spacing value, in pixels.
## void setFontHSpacing ( int hspacing )

Sets a new spacing (in pixels) between widget text characters.
### Arguments

- *int* **hspacing** - The horizontal spacing value, in pixels.

## int getFontHSpacing () const

Returns the current spacing (in pixels) between widget text characters.
### Return value

Current horizontal spacing value, in pixels.
## void setFontPermanent ( int permanent )

Sets a new flag indicating if color of the widget text is not changed (for example, when the widget becomes inactive or loses focus).
### Arguments

- *int* **permanent** - The value of 1 to keep the text color unchanged; 0 to change it.

## int getFontPermanent () const

Returns the current flag indicating if color of the widget text is not changed (for example, when the widget becomes inactive or loses focus).
### Return value

Current value of 1 to keep the text color unchanged; 0 to change it.
## void setFontColor ( const Math:: vec4 & color )

Sets a new color of the font used by the widget.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The font color.

## Math:: vec4 getFontColor () const

Returns the current color of the font used by the widget.
### Return value

Current font color.
## void setFontSize ( int size )

Sets a new size of the font used by the widget.
### Arguments

- *int* **size** - The Font size in pixels.

## int getFontSize () const

Returns the current size of the font used by the widget.
### Return value

Current Font size in pixels.
## void setMouseCursor ( int cursor )

Sets a new mouse pointer set for the widget.
### Arguments

- *int* **cursor** - The mouse pointer. See the list of available pointers with CURSOR_* prefixes in the article on Gui class functions.

## int getMouseCursor () const

Returns the current mouse pointer set for the widget.
### Return value

Current mouse pointer. See the list of available pointers with CURSOR_* prefixes in the article on Gui class functions.
## int getMouseY () const

Returns the current Y coordinate of the mouse pointer position in the widget's local space.
### Return value

Current Y coordinate of the mouse pointer position in the widget's local space.
## int getMouseX () const

Returns the current X coordinate of the mouse pointer position in the widget's local space.
### Return value

Current X coordinate of the mouse pointer position in the widget's local space.
## void setHeight ( int height )

Sets a new widget minimal height.
> **Notice:** The widget cannot be smaller than its content (the texture, video, etc.). It is only possible to make the widget bigger then the size of its content. For example, [WidgetButton](../../../api/library/gui/class.widgetbutton_cpp.md) can be made bigger than its texture, but it cannot be made any smaller than the texture dimensions.


### Arguments

- *int* **height** - The widget minimal height, in [logical units](../../../principles/dpi/index.md). If a negative value is provided, the value of 0 will be used instead.

## int getHeight () const

Returns the current widget minimal height.
> **Notice:** The widget cannot be smaller than its content (the texture, video, etc.). It is only possible to make the widget bigger then the size of its content. For example, [WidgetButton](../../../api/library/gui/class.widgetbutton_cpp.md) can be made bigger than its texture, but it cannot be made any smaller than the texture dimensions.


### Return value

Current widget minimal height, in [logical units](../../../principles/dpi/index.md). If a negative value is provided, the value of 0 will be used instead.
## void setWidth ( int width )

Sets a new widget minimal width.
> **Notice:** The widget cannot be smaller than its content (the texture, video, etc.). It is only possible to make the widget bigger then the size of its content. For example, [WidgetButton](../../../api/library/gui/class.widgetbutton_cpp.md) can be made bigger than its texture, but it cannot be made any smaller than the texture dimensions.


### Arguments

- *int* **width** - The widget minimal width, in [logical units](../../../principles/dpi/index.md). If a negative value is provided, the value of 0 will be used instead.

## int getWidth () const

Returns the current widget minimal width.
> **Notice:** The widget cannot be smaller than its content (the texture, video, etc.). It is only possible to make the widget bigger then the size of its content. For example, [WidgetButton](../../../api/library/gui/class.widgetbutton_cpp.md) can be made bigger than its texture, but it cannot be made any smaller than the texture dimensions.


### Return value

Current widget minimal width, in [logical units](../../../principles/dpi/index.md). If a negative value is provided, the value of 0 will be used instead.
## int getScreenPositionY () const

Returns the current screen position of the widget (its top left corner) on the screen along the y axis.
### Return value

Current screen position along the Y axis in [logical units](../../../principles/dpi/index.md).
## int getScreenPositionX () const

Returns the current screen position of the widget (its top left corner) on the screen along the x axis.
### Return value

Current screen position along the X axis in [logical units](../../../principles/dpi/index.md).
## void setPositionY ( int y )

Sets a new Y coordinate of the widget position relative to its parent.
### Arguments

- *int* **y** - The Y coordinate of the widget position relative to its parent.

## int getPositionY () const

Returns the current Y coordinate of the widget position relative to its parent.
### Return value

Current Y coordinate of the widget position relative to its parent.
## void setPositionX ( int x )

Sets a new X coordinate of the widget position relative to its parent.
### Arguments

- *int* **x** - The X coordinate of the widget position relative to its parent.

## int getPositionX () const

Returns the current X coordinate of the widget position relative to its parent.
### Return value

Current X coordinate of the widget position relative to its parent.
## void setNextFocus ( const Ptr < Widget >& focus )

Sets a new widget which will be focused next if the user presses **TAB**.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)>&* **focus** - The widget which will be focused next if the user presses **TAB**.

## Ptr < Widget > getNextFocus () const

Returns the current widget which will be focused next if the user presses **TAB**.
### Return value

Current widget which will be focused next if the user presses **TAB**.
## void setData ( const char * data )

Sets a new user data associated with the widget.
### Arguments

- *const char ** **data** - The user data associated with the widget. Data can be an xml formatted string.

## const char * getData () const

Returns the current user data associated with the widget.
### Return value

Current user data associated with the widget. Data can be an xml formatted string.
## void setOrder ( int order )

Sets a new rendering order (Z-order) for the widget. The higher the value, the higher the order of the widget is.
> **Notice:** Works only for widgets added to GUI via the [*Gui::addChild()*](../../../api/library/gui/class.gui_cpp.md#addChild_Widget_int_void) function with the [Gui::ALIGN_OVERLAP](../../../api/library/gui/class.gui_cpp.md#ALIGN_OVERLAP) flag specified (should not be [Gui::ALIGN_FIXED](../../../api/library/gui/class.gui_cpp.md#ALIGN_FIXED)).


```cpp
Unigine::Vector<Unigine::WidgetSpritePtr> sprites;

int AppWorldLogic::init()
{
	// create 3 squares with different colors
	for (int i = 0; i < 3; i++)
	{
		WidgetSpritePtr &sprite = sprites.append();
		sprite = WidgetSprite::create(Gui::get(), "white.texture");
		sprite->setPosition(i * 40 + 50, i * 40 + 50);
		sprite->setWidth(100);
		sprite->setHeight(100);
		Gui::get()->addChild(sprite, Gui::ALIGN_OVERLAP);
	}

	sprites[0]->setColor(vec4(1, 0.3f, 0.3f, 1));
	sprites[1]->setColor(vec4(0.3f, 1, 0.3f, 1));
	sprites[2]->setColor(vec4(0.3f, 0.3f, 1, 1));

	return 1;
}

int AppWorldLogic::update()
{
	// press space key to random reorder squares
	if (App::clearKeyState(' '))
	{
		for (int i = 0; i < 3; i++)
		{
			sprites[i]->setOrder(Game::getRandomInt(0, 10));

			Gui::get()->removeChild(sprites[i]);
			Gui::get()->addChild(sprites[i]);

			Log::message("%d ", sprites[i]->getOrder());
		}
		Log::message("\n");
	}
	return 1;
}

```


### Arguments

- *int* **order** - The rendering order (z-order) for the widget, in the range **[-128;127]**. (126 for the Profiler, 127 for the Console).

## int getOrder () const

Returns the current rendering order (Z-order) for the widget. The higher the value, the higher the order of the widget is.
> **Notice:** Works only for widgets added to GUI via the [*Gui::addChild()*](../../../api/library/gui/class.gui_cpp.md#addChild_Widget_int_void) function with the [Gui::ALIGN_OVERLAP](../../../api/library/gui/class.gui_cpp.md#ALIGN_OVERLAP) flag specified (should not be [Gui::ALIGN_FIXED](../../../api/library/gui/class.gui_cpp.md#ALIGN_FIXED)).


```cpp
Unigine::Vector<Unigine::WidgetSpritePtr> sprites;

int AppWorldLogic::init()
{
	// create 3 squares with different colors
	for (int i = 0; i < 3; i++)
	{
		WidgetSpritePtr &sprite = sprites.append();
		sprite = WidgetSprite::create(Gui::get(), "white.texture");
		sprite->setPosition(i * 40 + 50, i * 40 + 50);
		sprite->setWidth(100);
		sprite->setHeight(100);
		Gui::get()->addChild(sprite, Gui::ALIGN_OVERLAP);
	}

	sprites[0]->setColor(vec4(1, 0.3f, 0.3f, 1));
	sprites[1]->setColor(vec4(0.3f, 1, 0.3f, 1));
	sprites[2]->setColor(vec4(0.3f, 0.3f, 1, 1));

	return 1;
}

int AppWorldLogic::update()
{
	// press space key to random reorder squares
	if (App::clearKeyState(' '))
	{
		for (int i = 0; i < 3; i++)
		{
			sprites[i]->setOrder(Game::getRandomInt(0, 10));

			Gui::get()->removeChild(sprites[i]);
			Gui::get()->addChild(sprites[i]);

			Log::message("%d ", sprites[i]->getOrder());
		}
		Log::message("\n");
	}
	return 1;
}

```


### Return value

Current rendering order (z-order) for the widget, in the range **[-128;127]**. (126 for the Profiler, 127 for the Console).
## void setHidden ( bool hidden )

Sets a new value indicating if the widget is hidden.
### Arguments

- *bool* **hidden** - true if the widget is hidden, false if it is shown

## bool isHidden () const

Returns the current value indicating if the widget is hidden.
### Return value

true if the widget is hidden, false if it is shown
## void setEnabled ( bool enabled )

Sets a new value indicating if the widget is enabled (the user can interact with the widget).
### Arguments

- *bool* **enabled** - Set **true** to enable interaction with the widget; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the widget is enabled (the user can interact with the widget).
### Return value

**true** if interaction with the widget is enabled ; otherwise **false**.
## void setIntersectionEnabled ( bool enabled )

Sets a new value indicating if intersection detection is enabled for the widget.
### Arguments

- *bool* **enabled** - Set **true** to enable intersection detection for the widget; **false** - to disable it.

## bool isIntersectionEnabled () const

Returns the current value indicating if intersection detection is enabled for the widget.
### Return value

**true** if intersection detection for the widget is enabled ; otherwise **false**.
## void setFlags ( int flags )

Sets a new widget flags.
### Arguments

- *int* **flags** - The widget flags, [*ALIGN_**](../../../api/library/gui/class.gui_cpp.md#ALIGN_BACKGROUND) pre-defined variables.

## int getFlags () const

Returns the current widget flags.
### Return value

Current widget flags, [*ALIGN_**](../../../api/library/gui/class.gui_cpp.md#ALIGN_BACKGROUND) pre-defined variables.
## void setParent ( const Ptr < Widget >& parent )

Sets a new pointer to the parent widget.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)>&* **parent** - The parent widget.

## Ptr < Widget > getParent () const

Returns the current pointer to the parent widget.
### Return value

Current parent widget.
## Ptr < Gui > getParentGui () const

Returns the current [Gui](../../../api/library/gui/class.gui_cpp.md) instance that currently renders the widget's parent, if the widget has a parent. (This function can be used if the widget is created and used in two different GUIs, for example, in case of the Interface plugin.)
### Return value

Current GUI instance used for the widget's parent.
## Ptr < Gui > getGui () const

Returns the current [Gui](../../../api/library/gui/class.gui_cpp.md) instance that renders the widget. (This function can be used if the widget is created and used in two different GUIs, for example, in case of the Interface plugin.) It can be called only by root widgets. For child widgets, see *[getParentGui()](#getParentGui_Gui)*.
### Return value

Current GUI instance used for the widget.
## const char * getTypeName () const

Returns the current name of the widget type.
### Return value

Current name of the widget type.
## Widget::TYPE getType () const

Returns the current type of the widget.
### Return value

Current type of the widget.
## bool isLayout () const

Returns the current value indicating if the widget is a layout.
### Return value

**true** if the widget is a layout; otherwise **false**.
## bool isFixed () const

Returns the current value indicating if the widget is fixed.
### Return value

**true** if the widget is fixed; otherwise **false**.
## bool isBackground () const

Returns the current value indicating if the widget is a background one.
### Return value

**true** if the widget is a background one; otherwise **false**.
## bool isOverlapped () const

Returns the current value indicating if the widget is overlapped.
### Return value

**true** if the widget is overlapped; otherwise **false**.
## bool isExpanded () const

Returns the current value indicating if the widget is expanded.
### Return value

**true** if the widget is expanded; otherwise **false**.
## void setLifetime ( Widget::LIFETIME lifetime )

Sets a new lifetime management type for the root of the widget, or for the widget itself (if it is not a child for another widget).
> **Notice:** Lifetime of each widget in the hierarchy is defined by its root. Thus, lifetime management type set for a child widget that differs from the one set for the root is ignored.

. One of the [LIFETIME_*](#LIFETIME) variables.
### Arguments

- *[Widget::LIFETIME](../../../api/library/gui/class.widget_cpp.md#LIFETIME)* **lifetime** - The lifetime management type.

## Widget::LIFETIME getLifetime () const

Returns the current lifetime management type for the root of the widget, or for the widget itself (if it is not a child for another widget).
> **Notice:** Lifetime of each widget in the hierarchy is defined by its root. Thus, lifetime management type set for a child widget that differs from the one set for the root is ignored.

. One of the [LIFETIME_*](#LIFETIME) variables.
### Return value

Current lifetime management type.
## float getDpiScale () const

Returns the current DPI scale applied to the widget.
### Return value

Current DPI scale applied to the widget.
## int getRenderHeight () const

Returns the current widget frame height in pixels.
### Return value

Current widget frame height in pixels.
## int getRenderWidth () const

Returns the current widget frame width in pixels.
### Return value

Current widget frame width in pixels.
## Event<const Ptr < Widget > &> getEventRemove () const

event triggered when a widget is removed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Remove event handler
void remove_event_handler(const Ptr<Widget> & widget)
{
	Log::message("\Handling Remove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections remove_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventRemove().connect(remove_event_connections, remove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventRemove().connect(remove_event_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Remove event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
remove_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection remove_event_connection;

// subscribe to the Remove event with a handler function keeping the connection
publisher->getEventRemove().connect(remove_event_connection, remove_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
remove_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
remove_event_connection.setEnabled(true);

// ...

// remove subscription to the Remove event via the connection
remove_event_connection.disconnect();

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

	// A Remove event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget)
	{
		Log::message("\Handling Remove event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventRemove().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId remove_handler_id;

// subscribe to the Remove event with a lambda handler function and keeping connection ID
remove_handler_id = publisher->getEventRemove().connect(e_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Remove event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventRemove().disconnect(remove_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Remove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventRemove().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventRemove().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &, const Ptr < Widget > &> getEventDragDrop () const

event triggered when a drag-and-drop operation is performed with a widget. Supported by all widgets.. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**, const Ptr<Widget> & **target_widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the DragDrop event handler
void dragdrop_event_handler(const Ptr<Widget> & widget,  const Ptr<Widget> & target_widget)
{
	Log::message("\Handling DragDrop event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections dragdrop_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventDragDrop().connect(dragdrop_event_connections, dragdrop_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventDragDrop().connect(dragdrop_event_connections, [](const Ptr<Widget> & widget,  const Ptr<Widget> & target_widget) {
		Log::message("\Handling DragDrop event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
dragdrop_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection dragdrop_event_connection;

// subscribe to the DragDrop event with a handler function keeping the connection
publisher->getEventDragDrop().connect(dragdrop_event_connection, dragdrop_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
dragdrop_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
dragdrop_event_connection.setEnabled(true);

// ...

// remove subscription to the DragDrop event via the connection
dragdrop_event_connection.disconnect();

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

	// A DragDrop event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget,  const Ptr<Widget> & target_widget)
	{
		Log::message("\Handling DragDrop event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventDragDrop().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId dragdrop_handler_id;

// subscribe to the DragDrop event with a lambda handler function and keeping connection ID
dragdrop_handler_id = publisher->getEventDragDrop().connect(e_connections, [](const Ptr<Widget> & widget,  const Ptr<Widget> & target_widget) {
		Log::message("\Handling DragDrop event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventDragDrop().disconnect(dragdrop_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all DragDrop events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventDragDrop().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventDragDrop().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &, const Ptr < Widget > &> getEventDragMove () const

event triggered when a focused widget is moved. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**, const Ptr<Widget> & **underlying_widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the DragMove event handler
void dragmove_event_handler(const Ptr<Widget> & widget,  const Ptr<Widget> & underlying_widget)
{
	Log::message("\Handling DragMove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections dragmove_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventDragMove().connect(dragmove_event_connections, dragmove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventDragMove().connect(dragmove_event_connections, [](const Ptr<Widget> & widget,  const Ptr<Widget> & underlying_widget) {
		Log::message("\Handling DragMove event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
dragmove_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection dragmove_event_connection;

// subscribe to the DragMove event with a handler function keeping the connection
publisher->getEventDragMove().connect(dragmove_event_connection, dragmove_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
dragmove_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
dragmove_event_connection.setEnabled(true);

// ...

// remove subscription to the DragMove event via the connection
dragmove_event_connection.disconnect();

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

	// A DragMove event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget,  const Ptr<Widget> & underlying_widget)
	{
		Log::message("\Handling DragMove event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventDragMove().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId dragmove_handler_id;

// subscribe to the DragMove event with a lambda handler function and keeping connection ID
dragmove_handler_id = publisher->getEventDragMove().connect(e_connections, [](const Ptr<Widget> & widget,  const Ptr<Widget> & underlying_widget) {
		Log::message("\Handling DragMove event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventDragMove().disconnect(dragmove_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all DragMove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventDragMove().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventDragMove().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &> getEventLeave () const

event triggered when the mouse pointer leaves a widget. Supported by all widgets. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Leave event handler
void leave_event_handler(const Ptr<Widget> & widget)
{
	Log::message("\Handling Leave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections leave_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventLeave().connect(leave_event_connections, leave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventLeave().connect(leave_event_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Leave event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
leave_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection leave_event_connection;

// subscribe to the Leave event with a handler function keeping the connection
publisher->getEventLeave().connect(leave_event_connection, leave_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
leave_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
leave_event_connection.setEnabled(true);

// ...

// remove subscription to the Leave event via the connection
leave_event_connection.disconnect();

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

	// A Leave event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget)
	{
		Log::message("\Handling Leave event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventLeave().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId leave_handler_id;

// subscribe to the Leave event with a lambda handler function and keeping connection ID
leave_handler_id = publisher->getEventLeave().connect(e_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Leave event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventLeave().disconnect(leave_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Leave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventLeave().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventLeave().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &> getEventEnter () const

event triggered when the mouse pointer enters a widget. Supported by all widgets. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Enter event handler
void enter_event_handler(const Ptr<Widget> & widget)
{
	Log::message("\Handling Enter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enter_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEnter().connect(enter_event_connections, enter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEnter().connect(enter_event_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Enter event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
enter_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection enter_event_connection;

// subscribe to the Enter event with a handler function keeping the connection
publisher->getEventEnter().connect(enter_event_connection, enter_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
enter_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
enter_event_connection.setEnabled(true);

// ...

// remove subscription to the Enter event via the connection
enter_event_connection.disconnect();

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

	// A Enter event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget)
	{
		Log::message("\Handling Enter event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEnter().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId enter_handler_id;

// subscribe to the Enter event with a lambda handler function and keeping connection ID
enter_handler_id = publisher->getEventEnter().connect(e_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Enter event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEnter().disconnect(enter_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Enter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEnter().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEnter().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &, unsigned int> getEventTextPressed () const

event triggered when a virtual key is pressed while a widget is in focus. Supported by the following widgets:
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cpp.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cpp.md)

 **Virtual key** - is a value to which a scan code was converted by an Operating System (e.g., the **Q** scan code will have the **Q** virtual key on a *QWERTY*-keyboard, while on an *AZERTY*-keyboard it will have the **A** virtual key; or **NUMPAD_DIGIT_7** scan code can be translated into virtual **NUMPAD_HOME** or **NUMPAD_DIGIT_7** depending on the current *Num Lock* state. Virtual keys are used, when it is important to know what exactly did user type (not just the physical button, but rather a letter).
 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**, unsigned int **unicode**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TextPressed event handler
void textpressed_event_handler(const Ptr<Widget> & widget,  unsigned int unicode)
{
	Log::message("\Handling TextPressed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections textpressed_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventTextPressed().connect(textpressed_event_connections, textpressed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventTextPressed().connect(textpressed_event_connections, [](const Ptr<Widget> & widget,  unsigned int unicode) {
		Log::message("\Handling TextPressed event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
textpressed_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection textpressed_event_connection;

// subscribe to the TextPressed event with a handler function keeping the connection
publisher->getEventTextPressed().connect(textpressed_event_connection, textpressed_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
textpressed_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
textpressed_event_connection.setEnabled(true);

// ...

// remove subscription to the TextPressed event via the connection
textpressed_event_connection.disconnect();

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

	// A TextPressed event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget,  unsigned int unicode)
	{
		Log::message("\Handling TextPressed event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventTextPressed().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId textpressed_handler_id;

// subscribe to the TextPressed event with a lambda handler function and keeping connection ID
textpressed_handler_id = publisher->getEventTextPressed().connect(e_connections, [](const Ptr<Widget> & widget,  unsigned int unicode) {
		Log::message("\Handling TextPressed event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventTextPressed().disconnect(textpressed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TextPressed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventTextPressed().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventTextPressed().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &, int> getEventKeyPressed () const

event triggered when when a key (by a scan code) is pressed while a widget is in focus. Supported by the following widgets:
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cpp.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cpp.md)

 **Scan code** - is a code assigned to avery key on the keyboard. Keyboard drivers use scan codes to detect which key is pressed. Scan codes are assigned to keys on the hardware level and are not affected by the states of modifiers like *Caps Lock*, *Num Lock*, *Scroll Lock*, *Shift*, *Alt*, and *Ctrl* making it possible to implement identical control on different types of keyboards (*uiQWERTY*, *AZERTY*, *QWERTC*, etc.). Scan codes are used when only a physical position of a key (a button) is important (e.g. in the *ControlsApp* class or Console key).
 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**, int **key**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the KeyPressed event handler
void keypressed_event_handler(const Ptr<Widget> & widget,  int key)
{
	Log::message("\Handling KeyPressed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections keypressed_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventKeyPressed().connect(keypressed_event_connections, keypressed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventKeyPressed().connect(keypressed_event_connections, [](const Ptr<Widget> & widget,  int key) {
		Log::message("\Handling KeyPressed event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
keypressed_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection keypressed_event_connection;

// subscribe to the KeyPressed event with a handler function keeping the connection
publisher->getEventKeyPressed().connect(keypressed_event_connection, keypressed_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
keypressed_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
keypressed_event_connection.setEnabled(true);

// ...

// remove subscription to the KeyPressed event via the connection
keypressed_event_connection.disconnect();

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

	// A KeyPressed event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget,  int key)
	{
		Log::message("\Handling KeyPressed event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventKeyPressed().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId keypressed_handler_id;

// subscribe to the KeyPressed event with a lambda handler function and keeping connection ID
keypressed_handler_id = publisher->getEventKeyPressed().connect(e_connections, [](const Ptr<Widget> & widget,  int key) {
		Log::message("\Handling KeyPressed event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventKeyPressed().disconnect(keypressed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all KeyPressed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventKeyPressed().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventKeyPressed().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &, int> getEventReleased () const

event triggered when the mouse is released after clicking somewhere on a widget. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cpp.md)
- [*WidgetGroupBox*](../../../api/library/gui/class.widgetgroupbox_cpp.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cpp.md)
- [*WidgetManipulatorRotator*](../../../api/library/gui/class.widgetmanipulatorrotator_cpp.md) (**mouse_buttons** is always 0)
- [*WidgetManipulatorScaler*](../../../api/library/gui/class.widgetmanipulatorscaler_cpp.md) (**mouse_buttons** is always 0)
- [*WidgetManipulatorTranslator*](../../../api/library/gui/class.widgetmanipulatortranslator_cpp.md) (**mouse_buttons** is always 0)
- [*WidgetSlider*](../../../api/library/gui/class.widgetslider_cpp.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cpp.md)
- [*WidgetSpinBoxDouble*](../../../api/library/gui/class.widgetspinboxdouble_cpp.md)
- [*WidgetWindow*](../../../api/library/gui/class.widgetwindow_cpp.md)
- [*EngineWindow*](../../../api/library/gui/class.enginewindow_cpp.md) (**mouse_buttons** is always 0)

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**, int **mouse_buttons**)*
- The `mouse_buttons` argument is a mask representing a combination of the following flags: *[Gui::MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_LEFT) | [Gui::MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_MIDDLE) | [Gui::MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_RIGHT)*.


**Usage Example:**


```cpp
// auxiliary variable simplifying subscriptions management
EventConnections econn;

// ...

// creating a button widget
auto widget_button = WidgetButton::create(WindowManager::getMainWindow()->getGui(), "button");
WindowManager::getMainWindow()->getGui()->addChild(widget_button, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

// enabling Console onscreen overlay
Console::setOnscreen(true);

// subscribing to the Released event with a lambda-handler
widget_button->getEventReleased().connect(econn, [](WidgetPtr const& widget, int mouse_buttons) {
	int left = mouse_buttons & Gui::MOUSE_MASK_LEFT;
	int right = mouse_buttons & Gui::MOUSE_MASK_RIGHT;
	int middle = mouse_buttons & Gui::MOUSE_MASK_MIDDLE;

	// displaying information on the currently released mouse buttons
	Console::onscreenMessageLine(
		"getEventReleased(mouse_buttons: %s %s %s)",
		left ? "left" : "",
		right ? "right" : "",
		middle ? "middle" : ""
	);
});

```


<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Released event handler
void released_event_handler(const Ptr<Widget> & widget,  int mouse_buttons)
{
	Log::message("\Handling Released event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections released_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventReleased().connect(released_event_connections, released_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventReleased().connect(released_event_connections, [](const Ptr<Widget> & widget,  int mouse_buttons) {
		Log::message("\Handling Released event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
released_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection released_event_connection;

// subscribe to the Released event with a handler function keeping the connection
publisher->getEventReleased().connect(released_event_connection, released_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
released_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
released_event_connection.setEnabled(true);

// ...

// remove subscription to the Released event via the connection
released_event_connection.disconnect();

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

	// A Released event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget,  int mouse_buttons)
	{
		Log::message("\Handling Released event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventReleased().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId released_handler_id;

// subscribe to the Released event with a lambda handler function and keeping connection ID
released_handler_id = publisher->getEventReleased().connect(e_connections, [](const Ptr<Widget> & widget,  int mouse_buttons) {
		Log::message("\Handling Released event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventReleased().disconnect(released_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Released events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventReleased().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventReleased().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &, int> getEventPressed () const

event triggered when a mouse button or **ENTER** (**RETURN**) is pressed, while the mouse pointer is somewhere on a widget. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cpp.md)
- [*WidgetCanvas*](../../../api/library/gui/class.widgetcanvas_cpp.md)
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cpp.md)
- [*WidgetSlider*](../../../api/library/gui/class.widgetslider_cpp.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cpp.md)
- [*WidgetLabel*](../../../api/library/gui/class.widgetlabel_cpp.md)
- [*WidgetListBox*](../../../api/library/gui/class.widgetlistbox_cpp.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cpp.md)
- [*WidgetSprite*](../../../api/library/gui/class.widgetsprite_cpp.md)
- [*WidgetWindow*](../../../api/library/gui/class.widgetwindow_cpp.md)

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**, int **mouse_buttons**)*
- The `mouse_buttons` argument is a mask representing a combination of the following flags: *[Gui::MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_LEFT) | [Gui::MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_MIDDLE) | [Gui::MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_RIGHT)*.


**Usage Example:**


```cpp
// auxiliary variable simplifying subscriptions management
EventConnections econn;

// ...

// creating a button widget
auto widget_button = WidgetButton::create(WindowManager::getMainWindow()->getGui(), "button");
WindowManager::getMainWindow()->getGui()->addChild(widget_button, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

// enabling Console onscreen overlay
Console::setOnscreen(true);

// subscribing to the Pressed event with a lambda-handler
widget_button->getEventPressed().connect(econn, [](WidgetPtr const& widget, int mouse_buttons) {
	int left = mouse_buttons & Gui::MOUSE_MASK_LEFT;
	int right = mouse_buttons & Gui::MOUSE_MASK_RIGHT;
	int middle = mouse_buttons & Gui::MOUSE_MASK_MIDDLE;

	// displaying information on the currently pressed mouse buttons
	Console::onscreenMessageLine(
		"getEventPressed(mouse_buttons: %s %s %s)",
		left ? "left" : "",
		right ? "right" : "",
		middle ? "middle" : ""
	);
});

```


<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Pressed event handler
void pressed_event_handler(const Ptr<Widget> & widget,  int mouse_buttons)
{
	Log::message("\Handling Pressed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pressed_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventPressed().connect(pressed_event_connections, pressed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventPressed().connect(pressed_event_connections, [](const Ptr<Widget> & widget,  int mouse_buttons) {
		Log::message("\Handling Pressed event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
pressed_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection pressed_event_connection;

// subscribe to the Pressed event with a handler function keeping the connection
publisher->getEventPressed().connect(pressed_event_connection, pressed_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
pressed_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
pressed_event_connection.setEnabled(true);

// ...

// remove subscription to the Pressed event via the connection
pressed_event_connection.disconnect();

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

	// A Pressed event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget,  int mouse_buttons)
	{
		Log::message("\Handling Pressed event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventPressed().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId pressed_handler_id;

// subscribe to the Pressed event with a lambda handler function and keeping connection ID
pressed_handler_id = publisher->getEventPressed().connect(e_connections, [](const Ptr<Widget> & widget,  int mouse_buttons) {
		Log::message("\Handling Pressed event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventPressed().disconnect(pressed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Pressed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventPressed().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventPressed().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &> getEventDoubleClicked () const

event triggered when the mouse is double-clicked somewhere on a widget. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cpp.md)
- [*WidgetCheckBox*](../../../api/library/gui/class.widgetcheckbox_cpp.md)
- [*WidgetComboBox*](../../../api/library/gui/class.widgetcombobox_cpp.md)
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cpp.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cpp.md)
- [*WidgetHPaned*](../../../api/library/gui/class.widgethpaned_cpp.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cpp.md)
- [*WidgetLabel*](../../../api/library/gui/class.widgetlabel_cpp.md)
- [*WidgetListBox*](../../../api/library/gui/class.widgetlistbox_cpp.md)
- [*WidgetManipulatorRotator*](../../../api/library/gui/class.widgetmanipulatorrotator_cpp.md)
- [*WidgetManipulatorScaler*](../../../api/library/gui/class.widgetmanipulatorscaler_cpp.md)
- [*WidgetManipulatorTranslator*](../../../api/library/gui/class.widgetmanipulatortranslator_cpp.md)
- [*WidgetScroll*](../../../api/library/gui/class.widgetscroll_cpp.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cpp.md)
- [*WidgetTreeBox*](../../../api/library/gui/class.widgettreebox_cpp.md)
- [*WidgetVPaned*](../../../api/library/gui/class.widgetvpaned_cpp.md)
- [*WidgetWindow*](../../../api/library/gui/class.widgetwindow_cpp.md)

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the DoubleClicked event handler
void doubleclicked_event_handler(const Ptr<Widget> & widget)
{
	Log::message("\Handling DoubleClicked event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections doubleclicked_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventDoubleClicked().connect(doubleclicked_event_connections, doubleclicked_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventDoubleClicked().connect(doubleclicked_event_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling DoubleClicked event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
doubleclicked_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection doubleclicked_event_connection;

// subscribe to the DoubleClicked event with a handler function keeping the connection
publisher->getEventDoubleClicked().connect(doubleclicked_event_connection, doubleclicked_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
doubleclicked_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
doubleclicked_event_connection.setEnabled(true);

// ...

// remove subscription to the DoubleClicked event via the connection
doubleclicked_event_connection.disconnect();

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

	// A DoubleClicked event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget)
	{
		Log::message("\Handling DoubleClicked event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventDoubleClicked().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId doubleclicked_handler_id;

// subscribe to the DoubleClicked event with a lambda handler function and keeping connection ID
doubleclicked_handler_id = publisher->getEventDoubleClicked().connect(e_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling DoubleClicked event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventDoubleClicked().disconnect(doubleclicked_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all DoubleClicked events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventDoubleClicked().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventDoubleClicked().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &, int> getEventClicked () const

event triggered when the mouse is clicked somewhere on a widget. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cpp.md)
- [*WidgetCheckBox*](../../../api/library/gui/class.widgetcheckbox_cpp.md)
- [*WidgetComboBox*](../../../api/library/gui/class.widgetcombobox_cpp.md)
- [*WidgetDialog*](../../../api/library/gui/class.widgetdialog_cpp.md)
- [*WidgetDialogFile*](../../../api/library/gui/class.widgetdialogfile_cpp.md)
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cpp.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cpp.md)
- [*WidgetHPaned*](../../../api/library/gui/class.widgethpaned_cpp.md)
- [*WidgetScroll*](../../../api/library/gui/class.widgetscroll_cpp.md)
- [*WidgetSlider*](../../../api/library/gui/class.widgetslider_cpp.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cpp.md)
- [*WidgetLabel*](../../../api/library/gui/class.widgetlabel_cpp.md)
- [*WidgetListBox*](../../../api/library/gui/class.widgetlistbox_cpp.md)
- [*WidgetManipulatorRotator*](../../../api/library/gui/class.widgetmanipulatorrotator_cpp.md)
- [*WidgetManipulatorScaler*](../../../api/library/gui/class.widgetmanipulatorscaler_cpp.md)
- [*WidgetManipulatorTranslator*](../../../api/library/gui/class.widgetmanipulatortranslator_cpp.md)
- [*WidgetMenuBox*](../../../api/library/gui/class.widgetmenubox_cpp.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cpp.md)
- [*WidgetSprite*](../../../api/library/gui/class.widgetsprite_cpp.md)
- [*WidgetTreeBox*](../../../api/library/gui/class.widgettreebox_cpp.md)
- [*WidgetVPaned*](../../../api/library/gui/class.widgetvpaned_cpp.md)

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**, int **mouse_buttons**)*
- The `mouse_buttons` argument is a mask representing a combination of the following flags: *[Gui::MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_LEFT) | [Gui::MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_MIDDLE) | [Gui::MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_RIGHT)*.


**Usage Example:**


```cpp
// auxiliary variable simplifying subscriptions management
EventConnections econn;

// ...

// creating a button widget
auto widget_button = WidgetButton::create(WindowManager::getMainWindow()->getGui(), "button");
WindowManager::getMainWindow()->getGui()->addChild(widget_button, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

// enabling Console onscreen overlay
Console::setOnscreen(true);

// subscribing to the Clicked event with a lambda-handler
widget_button->getEventClicked().connect(econn, [](WidgetPtr const& widget, int mouse_buttons) {
	int left = mouse_buttons & Gui::MOUSE_MASK_LEFT;
	int right = mouse_buttons & Gui::MOUSE_MASK_RIGHT;
	int middle = mouse_buttons & Gui::MOUSE_MASK_MIDDLE;

	// displaying information on the currently clicked mouse buttons
	Console::onscreenMessageLine(
		"getEventClicked(mouse_buttons: %s %s %s)",
		left ? "left" : "",
		right ? "right" : "",
		middle ? "middle" : ""
	);
});

```


<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Clicked event handler
void clicked_event_handler(const Ptr<Widget> & widget,  int mouse_buttons)
{
	Log::message("\Handling Clicked event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections clicked_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventClicked().connect(clicked_event_connections, clicked_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventClicked().connect(clicked_event_connections, [](const Ptr<Widget> & widget,  int mouse_buttons) {
		Log::message("\Handling Clicked event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
clicked_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection clicked_event_connection;

// subscribe to the Clicked event with a handler function keeping the connection
publisher->getEventClicked().connect(clicked_event_connection, clicked_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
clicked_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
clicked_event_connection.setEnabled(true);

// ...

// remove subscription to the Clicked event via the connection
clicked_event_connection.disconnect();

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

	// A Clicked event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget,  int mouse_buttons)
	{
		Log::message("\Handling Clicked event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventClicked().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId clicked_handler_id;

// subscribe to the Clicked event with a lambda handler function and keeping connection ID
clicked_handler_id = publisher->getEventClicked().connect(e_connections, [](const Ptr<Widget> & widget,  int mouse_buttons) {
		Log::message("\Handling Clicked event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventClicked().disconnect(clicked_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Clicked events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventClicked().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventClicked().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &> getEventChanged () const

event triggered when a widget has changed its state. Supported by the following widgets:
- [*WidgetButton*](../../../api/library/gui/class.widgetbutton_cpp.md)
- [*WidgetCheckBox*](../../../api/library/gui/class.widgetcheckbox_cpp.md)
- [*WidgetComboBox*](../../../api/library/gui/class.widgetcombobox_cpp.md)
- [*WidgetDialogColor*](../../../api/library/gui/class.widgetdialogcolor_cpp.md)
- [*WidgetEditLine*](../../../api/library/gui/class.widgeteditline_cpp.md)
- [*WidgetEditText*](../../../api/library/gui/class.widgetedittext_cpp.md)
- [*WidgetHPaned*](../../../api/library/gui/class.widgethpaned_cpp.md)
- [*WidgetScroll*](../../../api/library/gui/class.widgetscroll_cpp.md)
- [*WidgetScrollBox*](../../../api/library/gui/class.widgetscrollbox_cpp.md)
- [*WidgetSlider*](../../../api/library/gui/class.widgetslider_cpp.md)
- [*WidgetIcon*](../../../api/library/gui/class.widgeticon_cpp.md)
- [*WidgetLabel*](../../../api/library/gui/class.widgetlabel_cpp.md)
- [*WidgetListBox*](../../../api/library/gui/class.widgetlistbox_cpp.md)
- [*WidgetManipulator*](../../../api/library/gui/class.widgetmanipulator_cpp.md)
- [*WidgetManipulatorRotator*](../../../api/library/gui/class.widgetmanipulatorrotator_cpp.md)
- [*WidgetManipulatorScaler*](../../../api/library/gui/class.widgetmanipulatorscaler_cpp.md)
- [*WidgetManipulatorTranslator*](../../../api/library/gui/class.widgetmanipulatortranslator_cpp.md)
- [*WidgetSpinBox*](../../../api/library/gui/class.widgetspinbox_cpp.md)
- [*WidgetSpinBoxDouble*](../../../api/library/gui/class.widgetspinboxdouble_cpp.md)
- [*WidgetTabBox*](../../../api/library/gui/class.widgettabbox_cpp.md)
- [*WidgetTreeBox*](../../../api/library/gui/class.widgettreebox_cpp.md)
- [*WidgetVPaned*](../../../api/library/gui/class.widgetvpaned_cpp.md)

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Changed event handler
void changed_event_handler(const Ptr<Widget> & widget)
{
	Log::message("\Handling Changed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections changed_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventChanged().connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventChanged().connect(changed_event_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection changed_event_connection;

// subscribe to the Changed event with a handler function keeping the connection
publisher->getEventChanged().connect(changed_event_connection, changed_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
changed_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
changed_event_connection.setEnabled(true);

// ...

// remove subscription to the Changed event via the connection
changed_event_connection.disconnect();

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

	// A Changed event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget)
	{
		Log::message("\Handling Changed event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId changed_handler_id;

// subscribe to the Changed event with a lambda handler function and keeping connection ID
changed_handler_id = publisher->getEventChanged().connect(e_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventChanged().disconnect(changed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &> getEventFocusOut () const

event triggered when a widget loses focus. Supported by all widgets. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FocusOut event handler
void focusout_event_handler(const Ptr<Widget> & widget)
{
	Log::message("\Handling FocusOut event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focusout_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFocusOut().connect(focusout_event_connections, focusout_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFocusOut().connect(focusout_event_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling FocusOut event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
focusout_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection focusout_event_connection;

// subscribe to the FocusOut event with a handler function keeping the connection
publisher->getEventFocusOut().connect(focusout_event_connection, focusout_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
focusout_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
focusout_event_connection.setEnabled(true);

// ...

// remove subscription to the FocusOut event via the connection
focusout_event_connection.disconnect();

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

	// A FocusOut event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget)
	{
		Log::message("\Handling FocusOut event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFocusOut().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId focusout_handler_id;

// subscribe to the FocusOut event with a lambda handler function and keeping connection ID
focusout_handler_id = publisher->getEventFocusOut().connect(e_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling FocusOut event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFocusOut().disconnect(focusout_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FocusOut events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFocusOut().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFocusOut().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &> getEventFocusIn () const

event triggered when a widget is focused. Supported by all widgets. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FocusIn event handler
void focusin_event_handler(const Ptr<Widget> & widget)
{
	Log::message("\Handling FocusIn event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections focusin_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFocusIn().connect(focusin_event_connections, focusin_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFocusIn().connect(focusin_event_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling FocusIn event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
focusin_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection focusin_event_connection;

// subscribe to the FocusIn event with a handler function keeping the connection
publisher->getEventFocusIn().connect(focusin_event_connection, focusin_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
focusin_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
focusin_event_connection.setEnabled(true);

// ...

// remove subscription to the FocusIn event via the connection
focusin_event_connection.disconnect();

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

	// A FocusIn event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget)
	{
		Log::message("\Handling FocusIn event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFocusIn().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId focusin_handler_id;

// subscribe to the FocusIn event with a lambda handler function and keeping connection ID
focusin_handler_id = publisher->getEventFocusIn().connect(e_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling FocusIn event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFocusIn().disconnect(focusin_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FocusIn events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFocusIn().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFocusIn().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &> getEventHide () const

event triggered when a widget is removed using [*Gui::removeChild()*](../../../api/library/gui/class.gui_cpp.md#removeChild_Widget_void). Supported by all widgets. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Hide event handler
void hide_event_handler(const Ptr<Widget> & widget)
{
	Log::message("\Handling Hide event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections hide_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventHide().connect(hide_event_connections, hide_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventHide().connect(hide_event_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Hide event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
hide_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection hide_event_connection;

// subscribe to the Hide event with a handler function keeping the connection
publisher->getEventHide().connect(hide_event_connection, hide_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
hide_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
hide_event_connection.setEnabled(true);

// ...

// remove subscription to the Hide event via the connection
hide_event_connection.disconnect();

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

	// A Hide event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget)
	{
		Log::message("\Handling Hide event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventHide().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId hide_handler_id;

// subscribe to the Hide event with a lambda handler function and keeping connection ID
hide_handler_id = publisher->getEventHide().connect(e_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Hide event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventHide().disconnect(hide_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Hide events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventHide().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventHide().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Widget > &> getEventShow () const

event triggered when a widget is shown. Supported by all widgets. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Widget> & **widget**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Show event handler
void show_event_handler(const Ptr<Widget> & widget)
{
	Log::message("\Handling Show event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections show_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventShow().connect(show_event_connections, show_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventShow().connect(show_event_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Show event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
show_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection show_event_connection;

// subscribe to the Show event with a handler function keeping the connection
publisher->getEventShow().connect(show_event_connection, show_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
show_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
show_event_connection.setEnabled(true);

// ...

// remove subscription to the Show event via the connection
show_event_connection.disconnect();

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

	// A Show event handler implemented as a class member
	void event_handler(const Ptr<Widget> & widget)
	{
		Log::message("\Handling Show event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventShow().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId show_handler_id;

// subscribe to the Show event with a lambda handler function and keeping connection ID
show_handler_id = publisher->getEventShow().connect(e_connections, [](const Ptr<Widget> & widget) {
		Log::message("\Handling Show event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventShow().disconnect(show_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Show events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventShow().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventShow().setEnabled(true);

```

</details>

### Return value

Event instance.
## void setTextDirection ( Gui::TextDirection direction )

Sets a new base paragraph direction for this widget's text, one of the *Gui::TEXT_DIRECTION_** values. With *TEXT_DIRECTION_AUTO* (default) the direction is inherited from the **[getGlobalTextDirection()](../../../api/library/gui/class.gui_cpp.md#getGlobalTextDirection_int)** property of the GUI, and if that is also set to auto, it is detected from the text content.
### Arguments

- *[Gui::TextDirection](../../../api/library/gui/class.gui_cpp.md#TextDirection)* **direction** - The base direction of the widget text

## Gui::TextDirection getTextDirection () const

Returns the current base paragraph direction for this widget's text, one of the *Gui::TEXT_DIRECTION_** values. With *TEXT_DIRECTION_AUTO* (default) the direction is inherited from the **[getGlobalTextDirection()](../../../api/library/gui/class.gui_cpp.md#getGlobalTextDirection_int)** property of the GUI, and if that is also set to auto, it is detected from the text content.
### Return value

Current base direction of the widget text
---

## Ptr < Widget > getChild ( int num ) const

Returns a child widget with a given number.
### Arguments

- *int* **num** - Number of the child widget.

### Return value

Pointer to the child widget.
## int isChild ( const Ptr < Widget > & w ) const

Checks if a given widget is a child of the current one.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **w** - Widget to check.

### Return value

**1** if the widget in question is a child; otherwise, **0**.
## void setFocus ( )

Sets focus on the widget.
## int isFocused ( ) const

Returns a value indicating if the widget is currently in focus.
### Return value

1 if the widget is in focus; otherwise, 0.
## void setFont ( const char * name )

Sets a true-type font (*.ttf) that will be used to render text on the widget by file path.
### Arguments

- *const char ** **name** - Path to the font file (`*.ttf`) stored in your project's `data` folder.

## bool getIntersection ( int local_pos_x , int local_pos_y ) const

Checks for an intersection with the widget's bounds for the given point.
### Arguments

- *int* **local_pos_x** - Local X coordinate.
- *int* **local_pos_y** - Local Y coordinate.

### Return value

true if the input coordinate is inside the widget; otherwise, false.
## Ptr < Widget > getHierarchyIntersection ( int screen_pos_x , int screen_pos_y )

Checks for an intersection with a widget that belongs to the hierarchy of the current widget.
### Arguments

- *int* **screen_pos_x** - The X coordinate of the screen position.
- *int* **screen_pos_y** - The Y coordinate of the screen position.

### Return value

Widget the intersection with which is found.
## int getKeyActivity ( unsigned int key ) const

Checks if a given key already has a special purpose for the widget.
### Arguments

- *unsigned int* **key** - ASCII key code: one of the *[Input::KEY_*](../../../api/library/controls/class.input_cpp.md#KEY_UNKNOWN)*values.

### Return value

1 if the key cannot be used; otherwise, 0.
## void setPermanentFocus ( )

Sets permanent focus on the widget (it means that the widget is always in focus).
## void setPosition ( int x , int y )

Sets a position of the widget relative to its parent in [logical units](../../../principles/dpi/index.md).
### Arguments

- *int* **x** - X coordinate of the upper left corner of the widget in [logical units](../../../principles/dpi/index.md).
- *int* **y** - Y coordinate of the upper left corner of the widget in [logical units](../../../principles/dpi/index.md).

## void setToolTip ( const char * str , int reset = 0 )

Sets a tooltip for the widget.
### Arguments

- *const char ** **str** - Tooltip text.
- *int* **reset** - **1** to recalculate a tooltip location if the mouse cursor was relocated; otherwise � **0**(by default).

## const char * getToolTip ( ) const

Returns the widget's tooltip text.
### Return value

Tooltip text.
## void addAttach ( const Ptr < Widget > & w , const char * format = 0 , int multiplier = 1 , int flags = 0 )

Attaches a given widget to the current one. When applied to checkboxes, converts them into a group of radio buttons. A horizontal/vertical slider can be attached to a label or a text field. The text field can be attached to any of the sliders.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **w** - Widget to attach.
- *const char ** **format** - Format string or values entered into the attached widget. If none specified, "%d" is implied. This is an optional parameter.
- *int* **multiplier** - Multiplier value, which is used to scale values provided by the attached widget. This is an optional parameter.
- *int* **flags** - Attachment flags: one of the [Gui::](../../../api/library/gui/class.gui_cpp.md) Enumeration with ATTACH_* prefixes. This is an optional parameter.

## void addChild ( const Ptr < Widget > & w , int flags = 0 )

Adds a child to the widget.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **w** - Child widget.
- *int* **flags** - Widget flags: one of the [Gui::](../../../api/library/gui/class.gui_cpp.md) Enumeration with ALIGN_* prefixes. This is an optional parameter.

## void arrange ( )

Rearranges the widget and its children to lay them out neatly. This function forces to recalculate widget size and allows to get updated GUI layout data in the current frame. If this function is not called, widget modifications made in the current *update()* will be available only in the next frame (i.e. with one-frame lag), as GUI is calculated and rendered after the script *update()* function has been executed.
## void raise ( const Ptr < Widget > & w )

Brings a given widget to the top.
> **Notice:** Works only for widgets added to GUI via the [*Gui::addChild()*](../../../api/library/gui/class.gui_cpp.md#addChild_Widget_int_void) function with the [Gui::ALIGN_OVERLAP](../../../api/library/gui/class.gui_cpp.md#ALIGN_OVERLAP) flag specified (should not be [Gui::ALIGN_FIXED](../../../api/library/gui/class.gui_cpp.md#ALIGN_FIXED)).


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **w** - Widget to be brought up.

## void removeAttach ( const Ptr < Widget > & w )

Detaches a given widget from the current one.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **w** - Widget to detach.

## void removeChild ( const Ptr < Widget > & w )

Removes a child widget from the list of the widget's children.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **w** - Child widget smart pointer.

## void removeFocus ( )

Removes focus from the widget.
## void replaceChild ( const Ptr < Widget > & w , const Ptr < Widget > & old_w , int flags = 0 )

Replaces one child widget with another.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **w** - New child widget smart pointer.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **old_w** - Widget to be replaced.
- *int* **flags** - Widget flags: one of the [Gui::](../../../api/library/gui/class.gui_cpp.md) Enumeration with ALIGN_* prefixes. This is an optional parameter.

## Widget::LIFETIME getLifetimeSelf ( ) const

Returns the lifetime management type set for the widget.
> **Notice:** Lifetime of each widget in the hierarchy is defined by it's root. Setting lifetime management type for a child widget different from the one set for the root has no effect.


## int toRenderSize ( int unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *int* **unit_size** - Size in units.

### Return value

Size in pixels.
## int toUnitSize ( int render_size )

Transforms the pixel value to the unit value.
### Arguments

- *int* **render_size** - Size in pixels.

### Return value

Size in units.
## Math:: ivec2 toRenderSize ( const Math:: ivec2 & unit_size )

Transforms the unit value to the pixel value.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **unit_size** - Size in units.

### Return value

Size in pixels.
## Math:: ivec2 toUnitSize ( const Math:: ivec2 & render_size )

Transforms the pixel value to the unit value.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **render_size** - Size in pixels.

### Return value

Size in units.
## Math:: ivec2 getTextRenderSize ( const char * OUT_text ) const

Returns the size (in pixels) of the specified text string rendered on the screen with taking into account all text output settings such as dpi, font size and style.
### Arguments

- *const char ** **OUT_text** - Text string. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Text size in pixels.
## void runEventShow ( )

Emulates the *[Show](#getEventShow_Event)* event.
## void runEventHide ( )

Emulates the *[Hide](#getEventHide_Event)* event.
## void runEventFocusIn ( )

Emulates the *[FocusIn](#getEventFocusIn_Event)* event.
## void runEventFocusOut ( )

Emulates the *[FocusOut](#getEventFocusOut_Event)* event.
## void runEventChanged ( )

Emulates the *[Changed](#getEventChanged_Event)* event.
## void runEventClicked ( int mouse_buttons )

Emulates the *[Clicked](#getEventClicked_Event)* event.
### Arguments

- *int* **mouse_buttons** - Mouse button - a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_RIGHT)*.

## void runEventDoubleClicked ( )

Emulates the *[DoubleClicked](#getEventDoubleClicked_Event)* event.
## void runEventPressed ( int mouse_buttons )

Emulates the *[Pressed](#getEventPressed_Event)* event.
### Arguments

- *int* **mouse_buttons** - Mouse button - a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_RIGHT)*.

## void runEventReleased ( int mouse_buttons )

Emulates the *[Released](#getEventReleased_Event)* event.
### Arguments

- *int* **mouse_buttons** - Mouse button - a mask representing a combination of the following flags: *[Gui.MOUSE_MASK_LEFT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_LEFT) | [Gui.MOUSE_MASK_MIDDLE](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_MIDDLE) | [Gui.MOUSE_MASK_RIGHT](../../../api/library/gui/class.gui_cpp.md#MOUSE_MASK_RIGHT)*.

## void runEventKeyPressed ( int key )

Emulates the *[KeyPressed](#getEventKeyPressed_Event)* event.
### Arguments

- *int* **key** - Key scan code.

## void runEventTextPressed ( unsigned int code )

Emulates the *[TextPressed](#getEventTextPressed_Event)* event.
### Arguments

- *unsigned int* **code** - Vistual key.

## void runEventEnter ( )

Emulates the *[Enter](#getEventEnter_Event)* event.
## void runEventLeave ( )

Emulates the *[Leave](#getEventLeave_Event)* event.
## void runEventDragMove ( const Ptr < Widget > & pointer )

Emulates the *[DragMove](#getEventDragMove_Event)* event.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **pointer** - Underlying widget.

## void runEventDragDrop ( const Ptr < Widget > & pointer )

Emulates the *[DragDrop](#getEventDragDrop_Event)* event.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Widget](../../../api/library/gui/class.widget_cpp.md)> &* **pointer** - Target widget.

## Math:: ivec2 getTextUnitSize ( const char * text ) const

Returns the text dimensions (width and height in logical unit). This function helps you estimate how well the text will fit in the widget before rendering.
### Arguments

- *const char ** **text** - Text string.

### Return value

Text size in logical unit (width, height).
