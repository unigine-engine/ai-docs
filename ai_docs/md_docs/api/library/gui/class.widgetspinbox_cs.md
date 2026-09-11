# Unigine::WidgetSpinBox Class (CS)

**Inherits from:** Widget


This class creates a [spin box](../../../code/gui/ui/ui_widgets.md#spinbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/spinbox.png)


#### See Also


- C++ sample
- C# Component sample


### Usage Example


This example illustrates creation of a spinbox via code.


```csharp
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class ComponentName : Component
{
	 // declaring a spinbox
		WidgetSpinBox spinbox;

		// implement the Changed event handler to be fired on changing spinbox value
		void onSpinboxChanged(Widget widget)
		{
			// printing the current spinbox value to the console and
			Log.Message("Spinbox value changed: {0} \n", (widget as WidgetSpinBox).Value);
			(widget as WidgetSpinBox).SetFocus();
		}

	// Method creating a spinbox with specified parameters at the specified position
	WidgetSpinBox CreateSB(int x, int y, int min, int max, int value, int step)
	{
		// get a pointer to the system GUI
		Gui gui = Gui.GetCurrent();
		// creating a new edit line and adding it to the GUI
		WidgetEditLine new_el = new WidgetEditLine(gui);
		gui.AddChild(new_el, Gui.ALIGN_OVERLAP);
		// setting widget's position
		new_el.SetPosition(x, y);

		// creating a spinbox with the specified parameters and adding it to the GUI
		WidgetSpinBox new_sb = new WidgetSpinBox(gui, min, max, value, step);
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
			spinbox = CreateSB(100, 100, 0, 10, 5, 1);

	}
}

```


## WidgetSpinBox Class

### Properties

## int Value

The value of the spinbox.
## int MaxExpand

The maximum value, up to which the upper limit of the range of the spinbox values can be expanded. The upper limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_cs.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MAX_EXPAND flag.
## int MinExpand

The minimum value, up to which the lower limit of the range of the spinbox values can be expanded. The lower limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_cs.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MIN_EXPAND flag.
## int MaxValue

The maximum value of the spinbox.
## int MinValue

The minimum value of the spinbox.
## vec4 ButtonColor

The color for the widget's button.
## int Step

The step of the spinbox.
### Members

---

## WidgetSpinBox ( Gui gui , int min = 0 , int max = 100 , int value = 0 , int step = 1 )

Constructor. Creates a spinbox with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the spinbox will belong.
- *int* **min** - Minimum value.
- *int* **max** - Maximum value.
- *int* **value** - Initial value.
- *int* **step** - Initial step.

## WidgetSpinBox ( int min = 0 , int max = 100 , int value = 0 , int step = 1 )

Constructor. Creates a spinbox with given parameters and adds it to the Engine GUI.
### Arguments

- *int* **min** - Minimum value.
- *int* **max** - Maximum value.
- *int* **value** - Initial value.
- *int* **step** - Initial step.
