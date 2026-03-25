# Unigine::WidgetSpinBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates a [spin box](../../../code/gui/ui/ui_widgets.md#spinbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/spinbox.png)


#### See Also


- C++ sample
- C# Component sample


### Usage Example


This example illustrates creation of a spinbox via code.


```cpp
#include "AppWorldLogic.h"
#include <UnigineWidgets.h>
#include <UnigineGui.h>

using namespace Unigine;

WidgetSpinBoxPtr spinbox;

// create an instance of the EventConnection class
EventConnection connection;

// event handler function to handle the changing spinbox value event
void onSpinboxChanged(const Ptr<Widget> & widget) {
	WidgetSpinBoxPtr sb = checked_ptr_cast<WidgetSpinBox>(widget);

	// printing the current spinbox value to the console
	Log::message("Spinbox value changed: %d \n", sb->getValue());
}

// Method creating a spinbox with specified parameters at the specified position
WidgetSpinBoxPtr createSB(int x, int y, int min, int max, int value, int step)
{

	// get a pointer to the system GUI
	GuiPtr gui = Gui::getCurrent();

	// creating a new edit line and adding it to the GUI
	WidgetEditLinePtr new_el = WidgetEditLine::create(gui);
	gui->addChild(new_el, Gui::ALIGN_OVERLAP);

	// setting widget's position
	new_el->setPosition(x, y);

	// creating a spinbox with the specified parameters and adding it to the GUI
	WidgetSpinBoxPtr new_sb = WidgetSpinBox::create(gui, min, max, value, step);
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
	spinbox = createSB(100, 100, 0, 10, 5, 1);

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


## WidgetSpinBox Class

### Members

---

## static WidgetSpinBoxPtr create ( const Ptr < Gui > & gui , int min = 0 , int max = 100 , int value = 0 , int step = 1 )

Constructor. Creates a spinbox with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the spinbox will belong.
- *int* **min** - Minimum value.
- *int* **max** - Maximum value.
- *int* **value** - Initial value.
- *int* **step** - Initial step.

## static WidgetSpinBoxPtr create ( int min = 0 , int max = 100 , int value = 0 , int step = 1 )

Constructor. Creates a spinbox with given parameters and adds it to the Engine GUI.
### Arguments

- *int* **min** - Minimum value.
- *int* **max** - Maximum value.
- *int* **value** - Initial value.
- *int* **step** - Initial step.

## void setMaxExpand ( int expand )

Sets the maximum value, up to which the upper limit of the range of the spinbox values can be expanded.
### Arguments

- *int* **expand** - Maximum value, up to which the spinbox upper limit can be raised.

## int getMaxExpand ( ) const

Returns the current maximum value, up to which the upper limit of the range of the spinbox values can be expanded. The upper limit of the spinbox can be expanded only if the spinbox is attached to an editline with the Gui::ATTACH_MAX_EXPAND flag.
### Return value

Maximum value, up to which the spinbox upper limit can be raised.
## void setMaxValue ( int value )

Sets a maximum value of the spinbox.
### Arguments

- *int* **value** - Maximum spinbox value.

## int getMaxValue ( ) const

Returns a maximum value of the spinbox.
### Return value

Maximum spinbox value.
## void setMinExpand ( int expand )

Sets the minimum value, up to which the lower limit of the range of the spinbox values can be expanded.
### Arguments

- *int* **expand** - Minimum value, up to which the spinbox lower limit can be dropped.

## int getMinExpand ( ) const

Returns the current minimum value, up to which the lower limit of the range of the spinbox values can be expanded. The lower limit of the spinbox can be expanded only if the spinbox is attached to an editline with the Gui::ATTACH_MIN_EXPAND flag.
### Return value

Minimum value, up to which the spinbox lower limit can be dropped.
## void setMinValue ( int value )

Sets a minimum value of the spinbox.
### Arguments

- *int* **value** - Minimum spinbox value.

## int getMinValue ( ) const

Returns a minimum value of the spinbox.
### Return value

Minimum spinbox value.
## void setValue ( int value )

Updates the current value of the spinbox.
### Arguments

- *int* **value** - New spinbox value.

## int getValue ( ) const

Returns the current value of the spinbox.
### Return value

Current spinbox value.
## void setStep ( int step )

Updates the current step of the spinbox.
### Arguments

- *int* **step** - New spinbox step.

## int getStep ( ) const

Returns the current step of the spinbox.
### Return value

Current spinbox step.
## void setButtonColor ( const Math:: vec4 & color )

Sets the color for the widget's button.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Four-component vector specifying the color in the RGBA format.

## Math:: vec4 getButtonColor ( ) const

Returns the current color for the widget's button.
### Return value

Four-component vector specifying the color in the RGBA format.
