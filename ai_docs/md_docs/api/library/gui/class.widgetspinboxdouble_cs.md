# Unigine::WidgetSpinBoxDouble Class (CS)

**Inherits from:** Widget


This class creates a [spin box](../../../code/gui/ui/ui_widgets.md#spinbox) with double values.


### Usage Example


This example illustrates creation of a spinbox via code.


```csharp
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class ComponentName : Component
{
	 // declaring a spinbox
		WidgetSpinBoxDouble spinbox;

		// implement the Changed event handler to be fired on changing spinbox value
		void onSpinboxChanged(Widget widget)
		{
			// printing the current spinbox value to the console and
			Log.Message("Spinbox value changed: {0} \n", (widget as WidgetSpinBoxDouble).Value);
			(widget as WidgetSpinBoxDouble).SetFocus();
		}

	// Method creating a spinbox with specified parameters at the specified position
	WidgetSpinBoxDouble CreateSB(double x, double y, double min, double max, double value, double step)
	{
		// get a pointer to the system GUI
		Gui gui = Gui.GetCurrent();
		// creating a new edit line and adding it to the GUI
		WidgetEditLine new_el = new WidgetEditLine(gui);
		gui.AddChild(new_el, Gui.ALIGN_OVERLAP);
		// setting widget's position
		new_el.SetPosition(x, y);

		// creating a spinbox with the specified parameters and adding it to the GUI
		WidgetSpinBoxDouble new_sb = new WidgetSpinBoxDouble(gui, min, max, value, step);
		gui.AddChild(new_sb, Gui.ALIGN_OVERLAP);

		// adding a callback to be fired on changing spinbox value
		new_sb.EventChanged.Connect(onSpinboxChanged);
		new_sb.Order = 1;

		// attaching the spinbox to the edit line
		new_el.AddAttach(new_sb);

		// setting initial spinbox value
		new_sb.Value = value;

		return new_sb;
	}

	void Init()
	{
		  // creating a spinbox with values in [0, 10] range (current - 5) at position (100, 100)
			spinbox = CreateSB(100, 100, 0.0, 10.0, 5.0, 1.0);

	}
}

```


## WidgetSpinBoxDouble Class

### Properties

## double Value

The value of the spinbox.
## double MaxExpand

The maximum value, up to which the upper limit of the range of the spinbox values can be expanded. The upper limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_cs.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MAX_EXPAND flag.
## double MinExpand

The minimum value, up to which the lower limit of the range of the spinbox values can be expanded. The lower limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_cs.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MIN_EXPAND flag.
## double MaxValue

The maximum value of the spinbox.
## double MinValue

The minimum value of the spinbox.
## vec4 ButtonColor

The color for the widget's button.
## double Step

The step of the spinbox.
### Members

---

## WidgetSpinBoxDouble ( Gui gui , double min = 0.0 , double max = 100.0 , double value = 0.0 , double step = 1.0 )

Constructor. Creates a spinbox with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the spinbox will belong.
- *double* **min** - Minimum value.
- *double* **max** - Maximum value.
- *double* **value** - Initial value.
- *double* **step** - Initial step.

## WidgetSpinBoxDouble ( double min = 0.0 , double max = 100.0 , double value = 0.0 , double step = 1.0 )

Constructor. Creates a spinbox with given parameters and adds it to the Engine GUI.
### Arguments

- *double* **min** - Minimum value.
- *double* **max** - Maximum value.
- *double* **value** - Initial value.
- *double* **step** - Initial step.
