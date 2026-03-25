# Unigine::WidgetCheckBox Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** Widget


This class creates [checkboxes](../../../code/gui/ui/ui_widgets.md#checkbox). A set of checkboxes can be converted into a radio buttons group (that act as a single mutually exclusive control), if all the checkboxes are [attached](../../../api/library/gui/class.widget_cpp.md#addAttach_Widget_cstr_int_int_void) to a certain one among them (for example, the first).


The object of this class may look as follows:


![Checkbox widget](../../../code/gui/ui/widgets/checkbox.png)


![Radio button widget](../../../code/gui/ui/widgets/radiobutton.png)


### See Also


- C++ sample
- C# Component sample


## Example


The following code illustrates how to create a checkbox widget and set its parameters.


```cpp
#include "AppWorldLogic.h"
#include <UnigineWidgets.h>

using namespace Unigine;

/* .. */

// event handler function
int onCheckBoxEventChanged()
{
	/* .. */

	return 1;
}
// create an instance of the EventConnection class
EventConnection connection;

/* .. */

int AppWorldLogic::init()
{
	GuiPtr gui = Gui::getCurrent();

	// creating a checkbox widget and setting its caption
	WidgetCheckBoxPtr widget_checkbox = WidgetCheckBox::create(gui, "Automatic mode");

	// setting a tooltip
	widget_checkbox->setToolTip("Toggle automatic mode");

	// rearranging checkbox size
	widget_checkbox->arrange();

	// setting checkbox position
	widget_checkbox->setPosition(10, 10);

	// setting checkbox state to checked
	widget_checkbox->setChecked(1);

	// setting onCheckBoxChanged function to handle CHANGED event
	widget_checkbox->getEventChanged().connect(connection, onCheckBoxEventChanged);

	// adding created checkbox widget to the system GUI
	gui->addChild(widget_checkbox, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

	return 1;
}

// ...

int AppWorldLogic::shutdown()
{
	// removing an event subscriptions
	connection.disconnect();
	return 1;
}


```


## WidgetCheckBox Class

### Members

---

## static WidgetCheckBoxPtr create ( const Ptr < Gui > & gui , const char * str = 0 )

Constructor. Creates a checkbox with a given text label and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the new checkbox will belong.
- *const char ** **str** - Checkbox label. This is an optional parameter.

## static WidgetCheckBoxPtr create ( const char * str = 0 )

Constructor. Creates a checkbox with a given text label and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Checkbox label. This is an optional parameter.

## void setChecked ( bool checked )

Sets a value indicating if the checkbox is selected.
### Arguments

- *bool* **checked** - 1 to check (select) the checkbox, 0 to uncheck it.

## bool isChecked ( ) const

Returns a value indicating if the checkbox is selected.
### Return value

1 if the checkbox is checked (selected); otherwise, 0.
## void setText ( const char * text )

Sets a checkbox text label.
### Arguments

- *const char ** **text** - Checkbox label.

## const char * getText ( ) const

Returns the checkbox text label.
### Return value

Checkbox label.
## void setCheckedColor ( const Math:: vec4 & color )

Sets the color to be used for the checked widget's state.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getCheckedColor ( ) const

Returns the current color used for the checked widget's state.
### Return value

The four-component vector specifying the color in the RGBA format.
## void setUncheckedColor ( const Math:: vec4 & color )

Sets the color to be used for the unchecked widget's state.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - The four-component vector specifying the color in the RGBA format.

## Math:: vec4 getUncheckedColor ( ) const

Returns the current color used for the unchecked widget's state.
### Return value

The four-component vector specifying the color in the RGBA format.
