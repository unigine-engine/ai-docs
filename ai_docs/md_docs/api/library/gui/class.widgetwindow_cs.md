# Unigine::WidgetWindow Class (CS)

**Inherits from:** Widget


This class creates a [titled window](../../../code/gui/ui/ui_containers.md#window).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/window.png)


By default, the window created by means of this class consists of a [single vertical column container](../../../api/library/gui/class.widgetvbox_cs.md) and a drag area at the top.


The WidgetWindow class provides methods that allow [editing the drag area](#setDragAreaEnabled_int_void). For example:


<details>
<summary>DragArea.cs | Close</summary>

`DragArea.cs`


```csharp
EngineWindowViewport window;

void on_close()
{
	window.DeleteLater();
}

private void Init()
{

		// borderless additional window
		window = new EngineWindowViewport(new ivec2(512, 256));
		window.BordersEnabled = false;

		Gui gui = window.SelfGui;

		// create window widget
		WidgetWindow widget_window = new WidgetWindow(gui, "Borderless Window");
		widget_window.Sizeable = false;
		widget_window.Moveable = false;
		window.AddChild(widget_window, Gui.ALIGN_EXPAND);

		// add a close icon to the window
		WidgetIcon close_icon = new WidgetIcon(gui, "window_close.png");
		close_icon.SetPosition(10, -24);
		close_icon.EventClicked.Connect(on_close);
		widget_window.AddChild(close_icon, Gui.ALIGN_OVERLAP | Gui.ALIGN_RIGHT | Gui.ALIGN_TOP);

		// adjust the window's drag area so that it doesn't cross the close icon
		widget_window.SetDragAreaPadding(3, 30, 3, 0);
		widget_window.DragAreaBackground = 1;
		widget_window.DragAreaBackgroundColor = new vec4(1.0f, 0.0f, 0.0f, 0.3f);

		window.Position = new ivec2(100, 100);
		window.Show();

}


```

</details>


The window will be rendered as follows:


![](drag_area.png)


### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


## WidgetWindow Class

### Properties

## string Text

The window title.
## int TextAlign

The alignment of the window title. One of the **[ALIGN_*](../../../api/library/gui/class.gui_cs.md#ALIGN_BACKGROUND)** pre-defined variables.
## 🔒︎ int PaddingBottom

The bottom padding for the widget content.
## 🔒︎ int PaddingTop

The top padding for the widget content.
## 🔒︎ int PaddingRight

The right-side padding for the widget content.
## 🔒︎ int PaddingLeft

The left-side padding for the widget content.
## 🔒︎ int SpaceY

The vertical space between the widgets in the window and between them and the window border.
## 🔒︎ int SpaceX

The horizontal space between the widgets in the window and between them and the window border.
## int MaxHeight

The maximum height value of the window.
## int MaxWidth

The maximum width value of the window.
## mat4 Transform

The global widget transformation matrix.
## vec4 Color

The color for the global color multiplier. The default is equivalent to vec4(1,1,1,1) (white).
## int SnapDistance

The distance, at which the window snaps to another window or screen edge. The default is 0 (do not snap).
## bool Floatable

The value indicating if the window is animated when changing to the minimized state and back. By default this option is disabled.
## bool Blendable

The value indicating if the window can fade in and out when changing to the minimized state and back. By default this option is disabled.
## bool Titleable

The value indicating if the window is minimized when double-clicking on it. By default this option is disabled.
## bool Sizeable

The value indicating if the window is resizeable. By default this option is disabled.
## bool Moveable

The value indicating if the window is movable. By default this option is disabled.
## vec4 BorderColor

The border color for the widget.
## vec4 BackgroundColor

The background color used for the widget.
## bool DragAreaEnabled

The value indicating if the drag area of the window is enabled.
## 🔒︎ int DragAreaPaddingTop

The top padding for the drag area.
## 🔒︎ int DragAreaPaddingRight

The right-side padding for the drag area.
## vec4 DragAreaBackgroundColor

The color for the background of the drag area.
## int DragAreaBackground

The value indicating if background rendering is enabled or disabled for the drag area.
## 🔒︎ int DragAreaPaddingLeft

The left-side padding for the drag area.
## 🔒︎ int DragAreaPaddingBottom

The bottom padding for the drag area.
## bool GlobalMovement

The value specifying if the window can be moved across the whole GUI or only within the parent widget. By default, this option is set to false, and the window can be moved only relevant to its parent.
## 🔒︎ int MinTextureWidth

The minimum width of the window render � the width of the window texture from the GUI skin.
## 🔒︎ int TextWidth

The window header width.
## 🔒︎ int TextHeight

The window header height.
## bool OutBoundsCallbacksEnabled

The value specifying if the callback processing for the window child widgets is enabled when the cursor is outside the window.
## 🔒︎ int MinTextureHeight

The minimum height of the window render � the height of the window texture from the GUI skin.
## int Stencil

The value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_cs.md#setWidth_int_void). Everything that lies outside of them, is not rendered. This option works only if children have [ALIGN_OVERLAP](../../../api/library/gui/class.gui_cs.md#ALIGN_OVERLAP) flag set (otherwise, they will expand the box widget bounds and no cutting will be done).
### Members

---

## WidgetWindow ( Gui gui , string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a window with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new window will belong.
- *string* **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the window and between them and the window border. This is an optional parameter.

## WidgetWindow ( string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a window with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Window title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the window and between them and the window border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the window and between them and the window border. This is an optional parameter.

## void SetPadding ( int l , int r , int t , int b )

Sets widget paddings for all sides. Padding clears an area around the content of a widget (inside of it).
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.

## void SetSpace ( int x , int y )

Sets a space between the widgets in the window and between them and the window border.
### Arguments

- *int* **x** - Horizontal space. If a negative value is provided, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is provided, 0 will be used instead.

## void SetDragAreaPadding ( int l , int r , int t , int b )

Sets paddings for all sides of the drag area.
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.
