# Unigine::WidgetSpinBoxDouble Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [spin box](../../../code/gui/ui/ui_widgets.md#spinbox) with double values.


### Usage Example


This example illustrates creation of a spinbox via code.


```cpp
#include "AppWorldLogic.h"
#include <UnigineWidgets.h>
#include <UnigineGui.h>

using namespace Unigine;

WidgetSpinBoxDoublePtr spinbox;

// create an instance of the EventConnection class
EventConnection connection;

// event handler function to handle the changing spinbox value event
void onSpinboxChanged(const Ptr<Widget> & widget) {
	WidgetSpinBoxDoublePtr sb = checked_ptr_cast<WidgetSpinBoxDouble>(widget);

	// printing the current spinbox value to the console
	Log::message("Spinbox value changed: %d \n", sb->getValue());
}

// Method creating a spinbox with specified parameters at the specified position
WidgetSpinBoxDoublePtr createSB(double x, double y, double min, double max, double value, double step)
{

	// get a pointer to the system GUI
	GuiPtr gui = Gui::getCurrent();

	// creating a new edit line and adding it to the GUI
	WidgetEditLinePtr new_el = WidgetEditLine::create(gui);
	gui->addChild(new_el, Gui::ALIGN_OVERLAP);

	// setting widget's position
	new_el->setPosition(x, y);

	// creating a spinbox with the specified parameters and adding it to the GUI
	WidgetSpinBoxDoublePtr new_sb = WidgetSpinBoxDouble::create(gui, min, max, value, step);
	gui->addChild(new_sb, Gui::ALIGN_OVERLAP);

	// adding a callback to be fired on changing spinbox value
	new_sb->getEventChanged().connect(connection, onSpinboxChanged);
	new_sb->setOrder(1);

	// attaching the spinbox to the edit line
	new_el->addAttach(new_sb);

	// setting initial spinbox value
	new_sb->setValue(value);

	return new_sb;
}
// ...

int AppWorldLogic::init()
{
	// creating a spinbox with values in [0, 10] range (current - 5) at position (100, 100)
	spinbox = createSB(100, 100, 0.0, 10.0, 5.0, 1.0);

	return 1;
}

// ...

int AppWorldLogic::shutdown()
{
	// cleanup
	spinbox.deleteLater();

	return 1;
}


```


## WidgetSpinBoxDouble Class

### Members

## void setValue ( double value )

Sets a new value of the spinbox.
### Arguments

- *double* **value** - The value of the spinbox

## double getValue () const

Returns the current value of the spinbox.
### Return value

Current value of the spinbox
## void setMaxExpand ( double expand )

Sets a new maximum value, up to which the upper limit of the range of the spinbox values can be expanded. The upper limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_cpp.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MAX_EXPAND flag.
### Arguments

- *double* **expand** - The maximum value, up to which the upper limit of the spinbox value range can be expanded

## double getMaxExpand () const

Returns the current maximum value, up to which the upper limit of the range of the spinbox values can be expanded. The upper limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_cpp.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MAX_EXPAND flag.
### Return value

Current maximum value, up to which the upper limit of the spinbox value range can be expanded
## void setMinExpand ( double expand )

Sets a new minimum value, up to which the lower limit of the range of the spinbox values can be expanded. The lower limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_cpp.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MIN_EXPAND flag.
### Arguments

- *double* **expand** - The minimum value, up to which the lower limit of the spinbox value range can be expanded

## double getMinExpand () const

Returns the current minimum value, up to which the lower limit of the range of the spinbox values can be expanded. The lower limit of the spinbox can be expanded only if the spinbox is [attached](../../../api/library/gui/class.widget_cpp.md#addAttach_Widget_cstr_int_int_void) to an editline with the Gui::ATTACH_MIN_EXPAND flag.
### Return value

Current minimum value, up to which the lower limit of the spinbox value range can be expanded
## void setMaxValue ( double value )

Sets a new maximum value of the spinbox.
### Arguments

- *double* **value** - The maximum value of the spinbox

## double getMaxValue () const

Returns the current maximum value of the spinbox.
### Return value

Current maximum value of the spinbox
## void setMinValue ( double value )

Sets a new minimum value of the spinbox.
### Arguments

- *double* **value** - The minimum value of the spinbox

## double getMinValue () const

Returns the current minimum value of the spinbox.
### Return value

Current minimum value of the spinbox
## void setButtonColor ( const Math:: vec4 & color )

Sets a new color for the widget's button.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The color for the widget's button

## Math:: vec4 getButtonColor () const

Returns the current color for the widget's button.
### Return value

Current color for the widget's button
## void setStep ( double step )

Sets a new step of the spinbox.
### Arguments

- *double* **step** - The step of the spinbox

## double getStep () const

Returns the current step of the spinbox.
### Return value

Current step of the spinbox
---

## static WidgetSpinBoxDoublePtr create ( const Ptr < Gui > & gui , double min = 0.0 , double max = 100.0 , double value = 0.0 , double step = 1.0 )

Constructor. Creates a spinbox with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the spinbox will belong.
- *double* **min** - Minimum value.
- *double* **max** - Maximum value.
- *double* **value** - Initial value.
- *double* **step** - Initial step.

## static WidgetSpinBoxDoublePtr create ( double min = 0.0 , double max = 100.0 , double value = 0.0 , double step = 1.0 )

Constructor. Creates a spinbox with given parameters and adds it to the Engine GUI.
### Arguments

- *double* **min** - Minimum value.
- *double* **max** - Maximum value.
- *double* **value** - Initial value.
- *double* **step** - Initial step.
