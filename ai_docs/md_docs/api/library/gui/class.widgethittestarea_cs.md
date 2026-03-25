# Unigine::WidgetHitTestArea Class (CS)

**Inherits from:** Widget


This class is used to define the widget area in engine-style windows and borderless system windows intersected by a user-controlled cursor. If the hit test area type is "resize", the system automatically changes the cursor shape, if the hit test area is draggable, the window can be dragged by clicking and dragging this area.


In the following example, the system borders of the main window are disabled and 2 custom drag areas are added. The first area is located at the top of the window and the second area is in its center. For demonstration purposes, the background is enabled for both areas.


<details>
<summary>WidgetHitTestAreaClass.cs | Close</summary>

`WidgetDragAreaClass.cs`


```csharp
private void Init()
{

	EngineWindowViewport main_window = WindowManager.MainWindow;
	if (main_window)
	{
		// disable system borders
		main_window.BordersEnabled = false;

		Gui gui = main_window.SelfGui;

		// add a drag area similar to title bar
		WidgetVBox top_drag_container = new WidgetVBox(gui);
		main_window.AddChild(top_drag_container);

		WidgetHitTestArea top_drag_area = new WidgetHitTestArea(gui, (int)EngineWindow.HITTEST.DRAGGABLE);
		top_drag_area.Height = 25;
		top_drag_container.AddChild(top_drag_area, Gui.ALIGN_EXPAND);

		top_drag_area.Background = 1;
		top_drag_area.BackgroundColor = vec4.RED;

		// add an extra drag area
		WidgetHitTestArea drag_area = new WidgetHitTestArea(gui, (int)EngineWindow.HITTEST.DRAGGABLE);
		drag_area.Width = 512;
		drag_area.Height = 256;
		main_window.AddChild(drag_area, Gui.ALIGN_CENTER);

		drag_area.Background = 1;
		drag_area.BackgroundColor = vec4.BLUE;
	}

}


```

</details>


## WidgetHitTestArea Class

### Properties

## 🔒︎ int HitTestResult

The hit test area type, one of the **[EngineWindow.HITTEST](../../../api/library/gui/class.enginewindow_cs.md#HITTEST_INVALID)** values.
## vec4 BackgroundColor

The color for the background of the drag area to be used for debug purposes.
## int Background

The flag indicating if background rendering is enabled for the drag area for debug purposes.
### Members

---

## WidgetHitTestArea ( Gui gui , int hit_test )

Constructor. Creates a hit test area widget and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the hit test area widget belongs.
- *int* **hit_test** - Hit test area type, one of the **[EngineWindow.HITTEST](../../../api/library/gui/class.enginewindow_cs.md#HITTEST_INVALID)** values.

## WidgetHitTestArea ( int hit_test )

Constructor. Creates a hit test area widget of the specified type.
### Arguments

- *int* **hit_test** - Hit test area type, one of the **[EngineWindow.HITTEST](../../../api/library/gui/class.enginewindow_cs.md#HITTEST_INVALID)** values.
