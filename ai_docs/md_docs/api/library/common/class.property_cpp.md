# Unigine::Property Class (CPP)

**Header:** #include <UnigineProperties.h>


This class provides an interface for property manipulation: it is used to modify [properties](../../../principles/world_structure/index.md#properties) that allow you to control values of the logic-related parameters. When a property is assigned to a node, an instanced [internal property](../../../principles/properties/index.md#internal) is created and saved into a `.world` or `.node` file. However, rather than the whole list of parameters it contains only the modified ones.


The concepts of a [path](#setFilePath_cstr_int) and a [name](#setName_cstr_void) of the property should be distinguished:


- The **path** specifies where the property is stored on the disk. The path includes a property file name.
- The **name** specifies how the property will be displayed in the UnigineEditor (the Property Hierarchy window, the nodes surface section of the Parameters window). The name can also be used to refer to a property from the [code](../../../api/library/engine/class.properties_cpp.md#findProperty_cstr_Property).


By default, the property name and the `*.prop` file name coincide.


By using functions of this class, you can, for example, implement a *properties editor*.


**Properties** specify the way the object will behave and interact with other objects and the scene environment.


A property is a "material" for application logic represented by a set of logic-related **[parameters](../../../code/formats/property_format.md#element_parameter)**. Properties can be used to build [**components**](../../../principles/component_system/index.md) to extend the functionality of nodes.


All properties in the project are organized into a [hierarchy](../../../principles/properties/inheritance.md). To be modified, properties should be obtained from the hierarchy via [*API*](../../../api/library/engine/class.properties_cpp.md) functions.


Property parameters are managed individually via the *[PropertyParameter](../../../api/library/common/class.propertyparameter_cpp.md)* class, to get any parameter by its name or ID you should use the **[getParameterPtr()](../../...md#getParameterPtr_cstr_PropertyParameter)** method.


```cpp
PropertyParameterPtr pPropertyParameter = pProperty->getParameterPtr(); // get "root" parameter
NodePtr pTargetNode = pPropertyParameter->getChild(k)->getValueNode(); // get child with index "k", then its value

// ...

float positionFactor = pPropertyParameter->getChild(k)->getValueFloat();
// etc.

// If you know names, you can use:
pTargetNode = pProperty->getParameterPtr("target")->getValueNode();
positionFactor = pProperty->getParameterPtr("position_factor")->getValueFloat();


```


Automatic type conversion of property parameters make them act like some universal variables i.e. you can set a new value for an integer parameter int_param and type it like this:


```cpp
PropertyParameterPtr int_param;

/* ... */

// setting a new value of integer parameter using a string
int_param->setValue("15");

// setting a new value of integer parameter using a float
int_param->setValue(5.0f);

// getting integer parameter's value as a string
Log::message("Integer parameter value : %s", int_param->getValueString());


```


> **Notice:** You can modify only existing parameters of the property. To add or remove new parameters, you should manually edit the `.prop` file or use API to edit the XML file via the code.


### Adding and Removing Properties


> **Notice:** The *Property* class doesn't allow adding a new property to the property hierarchy.


A new property can be added to the hierarchy in one of the following ways:


- By creating and editing the corresponding `.prop` file manually. For example, in the `data` folder let us create the following file describing a property for a GameObjectUnit: ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.16.0.2" manual="1" editable="0" name="GameObjectsUnit"> <parameter name="weapon_type" type="switch" items="air,land,all_types">0</parameter> <parameter name="attack" type="toggle">1</parameter> <parameter name="damage" type="int" max="1000">1</parameter> <parameter name="velocity" type="float" max="100">30</parameter> <parameter name="material" type="string"/> </property> ```
- By inheriting from the existing property via [*Properties::inheritProperty()*](../../../api/library/engine/class.properties_cpp.md#inheritProperty_UGUID_cstr_cstr_Property) function or [*inherit()*](#inherit_cstr_Property) function of the Property class. For example: ```cpp // inherit a GameObjectsUnit_0 property from the GameObjectsUnit property PropertyPtr inherited_prop = Properties::findManualProperty("GameObjectsUnit")->inherit("GameObjectsUnit_0", "game_object_unit_0.prop"); // inherit a GameObjectsUnit_1 property from the GameObjectsUnit_0 property via the Manager Properties::inheritProperty(inherited_prop->getGUID(), "GameObjectsUnit_1", "game_object_unit_1.prop"); ``` To save all properties in the hierarchy that can be saved (i.e., editable, having a path specified, and not internal or manual ones) via the [*Properties::saveProperties()*](../../../api/library/engine/class.properties_cpp.md#saveProperties_int) function. > **Notice:** By default, all parameters and states of the inherited property are the same as specified in the parent property. A child property can [override some parameters of its parent or add new ones](../../../principles/world_structure/index.md#properties_hierarchy).
- By editing the corresponding `.prop` file [via API](../../../api/library/common/class.xml_cpp.md): you can open an XML file, write data into it and save it.


To delete a property, you can simply call the *[removeProperty()](../../../api/library/engine/class.properties_cpp.md#removeProperty_UGUID_int_int_int)* function:


```cpp
// remove the property with the given name with all its children and delete the *.prop file
Properties::removeProperty(Properties::findProperty("GameObjectsUnit_0")->getGUID(), 1, 1);


```


### Handling Events


You can subscribe for events to track any changes made to the property and its parameters and perform certain actions. The signature of the handler function can be one of the following:


```cpp
// for the ParameterChanged type
void handler_function_name(const PropertyPtr &property, int parameter_num);

// for all other types
void handler_function_name(const PropertyPtr &property);


```


The example below shows how to subscribe for events to track changes of property parameters and report the name of the property and the changed parameter (suppose we have a manual property named *my_prop* with an integer parameter named *my_int_param*).


```cpp
// EventConnections class instance to manage event subscriptions
EventConnections econn;

void parameter_changed(const PropertyPtr &property, int num)
{
	Log::message("Parameter \"%s\" of the property \"%s\" has changed its value.\n", property->getParameterPtr(num)->getName(), property->getName());
	// ...
}

	// somewhere in the code

	// getting a manual property named "my_prop" via the Property Manager
	PropertyPtr property = Properties::findManualProperty("my_prop.prop");

	// subscribing to the parameter change event
	property->getEventParameterChanged().connect(econn, parameter_changed);

	// changing the value of the "my_int_param" parameter
	property->getParameterPtr("my_int_param")->setValueInt(3);

	// ...

	// removing all event subscriptions somewhere on shutdown
	econn.disconnectAll();


```


### Usage Example


To illustrate how properties and their parameters are managed let's make a simple viewer for all properties in the project as well as for their parameters. Our viewer will have the following features:


- View the list of all properties used in the project.
- View the list of parameters of the currently selected property. Inherited, overridden and unique parameters are displayed in different colors.
- Change the value of the selected property parameter.
- Reset the value of the selected property parameter.
- Inherit a new property from the selected one.
- Clone the selected property.
- Save the currently selected property to a file.
- Reload all properties.


![](property_viewer.png)


We can add the the following `*.prop` files to the `data` folder of our project to check our viewer:


- `my_property.prop` <details> <summary>my_property.prop | Close</summary> **my_property.prop** ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.16.0.2" name="my_property" parent="node_base" manual="1"> <parameter name="damage" type="int" max="1000">1</parameter> <parameter name="mass" type="float" tooltip="Aircraft mass">1345</parameter> <parameter name="attack" type="toggle">1</parameter> <parameter name="weapon_type" type="switch" items="air,land,all_types">0</parameter> <parameter name="Mask" type="mask"/> <parameter name="Base Material" type="material"/> <parameter name="Model Node" type="node"/> <struct name="member"> <parameter name="name" type="string"></parameter> <parameter name="rank" type="switch" items="2LT,1LT,CPT,MAJ,LTC,COL,BG,MG">0</parameter> <parameter name="year" type="int"></parameter> <parameter name="status" type="toggle">1</parameter> </struct> <parameter name="Members" type="array" array_type="member" group="Crew Information"> <value> <parameter name="name">Mike Watts</parameter> <parameter name="rank" type="switch" items="2LT,1LT,CPT,MAJ,LTC,COL,BG,MG">3</parameter> <parameter name="year">1990</parameter> </value> <value> <parameter name="name">John Doe</parameter> <parameter name="rank" type="switch" items="2LT,1LT,CPT,MAJ,LTC,COL,BG,MG">2</parameter> <parameter name="year">1995</parameter> </value> <value> <parameter name="name">Vincent Preston</parameter> <parameter name="rank" type="switch" items="2LT,1LT,CPT,MAJ,LTC,COL,BG,MG">1</parameter> <parameter name="year">1997</parameter> </value> </parameter> <parameter name="Service Flags" type="array" array_type="toggle" group="Auxiliary"> <value>1</value> <value>0</value> <value>1</value> <value>0</value> </parameter> </property> ``` </details>
- `custom_prop.prop` <details> <summary>custom_prop.prop | Close</summary> **custom_prop.prop** ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.16.0.2" name="custom_prop" manual="1"> <!-- First structure declaration --> <struct name="struct1"> <parameter name="param_a" type="int">1</parameter> <parameter name="param_b" type="toggle">0</parameter> <parameter name="param_c" type="int">1</parameter> </struct> <!-- Inherited structure declaration--> <struct name="struct2" parent_name="struct1"> <parameter name="param2_a" type="toggle">0</parameter> <parameter name="param2_b" type="float">1.0</parameter> </struct> <!-- Struct parameter of struct2 type --> <parameter name="my_struct_param" type="struct2"></parameter> <!-- Nested structure declaration --> <struct name="struct3"> <parameter name="param3_a" type="struct2">0</parameter> <parameter name="param3_b" type="int">15</parameter> </struct> <!-- Declaration of a one-dimensional array of struct3 elements--> <parameter name="my_struct_array" array_type="struct3"></parameter> </property> ``` </details>
- `custom_prop_0.prop` inherited from the **custom_prop** property. <details> <summary>custom_prop_0.prop | Close</summary> **custom_prop_0.prop** ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.16.0.2" name="custom_prop_0" manual="1" parent_name="custom_prop"> <!-- Declaration of a 2-dimensional array (matrix) of integer elements--> <parameter name="my_int_array" array_type="int" array_dim="2"></parameter> </property> ``` </details>


Below is the source code in C++ implementing our Property Viewer. You can copy and paste it to the corresponding files of your project.


<details>
<summary>AppSystemLogic.h | Close</summary>

**AppSystemLogic.h**


```cpp
#ifndef __APP_SYSTEM_LOGIC_H__
#define __APP_SYSTEM_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineWidgets.h>
#include <UnigineGui.h>
#include <UnigineMap.h>

using namespace Unigine;
using namespace Math;

class AppSystemLogic : public Unigine::SystemLogic
{

private:
	// declaring UI widgets to be used
	WidgetWindowPtr window;
	WidgetHBoxPtr hbox;

	WidgetGroupBoxPtr properties_gb;
	WidgetTreeBoxPtr properties;
	WidgetGroupBoxPtr parameters_gb;
	WidgetTreeBoxPtr parameters;
	WidgetGroupBoxPtr value_gb;
	WidgetGroupBoxPtr menu_gb;

	WidgetVBoxPtr vbox2, vbox3;
	WidgetHBoxPtr hbox2;
	WidgetButtonPtr reload;
	WidgetButtonPtr clone;
	WidgetButtonPtr inherit;
	WidgetButtonPtr save_prop;

	// values
	Vector<WidgetLabelPtr> label;
	WidgetEditLinePtr value;
	WidgetButtonPtr change;
	WidgetButtonPtr reset;

	WidgetLabelPtr info;
	WidgetLabelPtr prop_info;
	// lists of properties and parameters
	Map<int, PropertyPtr> item_prop;
	Map<int, PropertyParameterPtr> item_param;

	void refresh_properties();
	void properties_changed();
	void parameters_changed();

	void change_clicked(const Unigine::WidgetPtr &button, int mbuttons);
	void reset_clicked(const Unigine::WidgetPtr &button, int mbuttons);
	void reload_clicked(const Unigine::WidgetPtr &button, int mbuttons);
	void refresh_info();
	void clone_clicked(const Unigine::WidgetPtr &button, int mbuttons);
	void inherit_clicked(const Unigine::WidgetPtr &button, int mbuttons);
	void save_prop_clicked(const Unigine::WidgetPtr &button, int mbuttons);
public:
	AppSystemLogic();
	~AppSystemLogic() override;

	int init() override;

	int update() override;
	int postUpdate() override;

	int shutdown() override;
};

#endif // __APP_SYSTEM_LOGIC_H__

```

</details>


<details>
<summary>AppSystemLogic.cpp | Close</summary>

**AppSystemLogic.cpp**


```cpp
#include "AppSystemLogic.h"
#include <UnigineProperties.h>
#include <UnigineFileSystem.h>
#include <functional>

using namespace Unigine;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

// System logic, it exists during the application life cycle.
// These methods are called right after corresponding system script's (UnigineScript) methods.

AppSystemLogic::AppSystemLogic()
{
}

AppSystemLogic::~AppSystemLogic()
{
}

int AppSystemLogic::init()
{
	Engine::get()->setBackgroundUpdate(Engine::BACKGROUND_UPDATE_RENDER_NON_MINIMIZED);

	// creating user interface
	GuiPtr gui = Gui::getCurrent();
	window = WidgetWindow::create(gui, "Properties Viewer");
	window->setSizeable(1);
	window->setWidth(WindowManager::getMainWindow()->getSize().x);
	window->setHeight(WindowManager::getMainWindow()->getSize().y);
	gui->addChild(window, Gui::ALIGN_OVERLAP);

	vbox2 = WidgetVBox::create(gui);
	window->addChild(vbox2, Gui::ALIGN_EXPAND);

	hbox = WidgetHBox::create(gui);
	vbox2->addChild(hbox, Gui::ALIGN_EXPAND);

	properties_gb = WidgetGroupBox::create(gui, "Properties");
	parameters_gb = WidgetGroupBox::create(gui, "Parameters");
	hbox->addChild(properties_gb, Gui::ALIGN_EXPAND);
	hbox->addChild(parameters_gb, Gui::ALIGN_EXPAND);

	properties = WidgetTreeBox::create(gui);
	parameters = WidgetTreeBox::create(gui);
	properties_gb->addChild(properties, Gui::ALIGN_EXPAND);
	parameters_gb->addChild(parameters, Gui::ALIGN_EXPAND);

	vbox3 = WidgetVBox::create(gui);
	hbox->addChild(vbox3, Gui::ALIGN_EXPAND);
	value_gb = WidgetGroupBox::create(gui, "Value");
	value_gb->setWidth(300);
	value_gb->setHeight(300);
	value_gb->arrange();
	menu_gb = WidgetGroupBox::create(gui, "Menu");
	vbox3->addChild(value_gb, Gui::ALIGN_LEFT);
	vbox3->addChild(menu_gb, Gui::ALIGN_EXPAND);

	label.append() = WidgetLabel::create(gui, "");
	label.last()->setFontRich(1);
	value_gb->addChild(label.last(), Gui::ALIGN_LEFT);
	value = WidgetEditLine::create(gui);
	value_gb->addChild(value, Gui::ALIGN_EXPAND);
	for (int i = 0; i < 12; i++)
	{
		label.append() = WidgetLabel::create(gui, "");
		label.last()->setFontRich(1);
		value_gb->addChild(label.last(), Gui::ALIGN_LEFT);
	}
	change = WidgetButton::create(gui, "Change Value");
	value_gb->addChild(change, Gui::ALIGN_LEFT);
	reset = WidgetButton::create(gui, "Reset Value");
	value_gb->addChild(reset, Gui::ALIGN_LEFT);

	reload = WidgetButton::create(gui, "Reload Property Files");
	clone = WidgetButton::create(gui, "Clone Property");
	inherit = WidgetButton::create(gui, "Inherit Property");
	save_prop = WidgetButton::create(gui, "Save Property");

	menu_gb->addChild(reload, Gui::ALIGN_EXPAND);
	menu_gb->addChild(clone, Gui::ALIGN_EXPAND);
	menu_gb->addChild(inherit, Gui::ALIGN_EXPAND);
	menu_gb->addChild(save_prop, Gui::ALIGN_EXPAND);

	info = WidgetLabel::create(gui);
	info->setFontRich(1);
	info->setText(
		"<font color=00ffff>Unique value</font><br>"
		"<font color=ffffff>Inherited value</font><br>"
		"<font color=ffff00>Overridden value</font><br>");
	menu_gb->addChild(info, Gui::ALIGN_LEFT);
	prop_info = WidgetLabel::create(gui);
	menu_gb->addChild(prop_info, Gui::ALIGN_LEFT);

	// subscribing to UI element events
	properties->getEventChanged().connect(econnections, this, &AppSystemLogic::properties_changed);
	parameters->getEventChanged().connect(econnections, this, &AppSystemLogic::parameters_changed);

	change->getEventClicked().connect(econnections, this, &AppSystemLogic::change_clicked);
	reset->getEventClicked().connect(econnections, this, &AppSystemLogic::reset_clicked);
	reload->getEventClicked().connect(econnections, this, &AppSystemLogic::reload_clicked);
	clone->getEventClicked().connect(econnections, this, &AppSystemLogic::clone_clicked);
	inherit->getEventClicked().connect(econnections, this, &AppSystemLogic::inherit_clicked);
	save_prop->getEventClicked().connect(econnections, this, &AppSystemLogic::save_prop_clicked);

	refresh_properties();
	return 1;
}

/// method refreshing properties
void AppSystemLogic::refresh_properties()
{
	properties->getEventChanged().setEnabled(false);
	properties->clear();
	item_prop.clear();

	// recursive function iterating through all children properties and building property hierarchy
	std::function<void(int, const PropertyPtr &)> attach_children = [&, this](int parent, const PropertyPtr &prop_parent)
	{
		for (int k = 0; k < prop_parent->getNumChildren(); k++)
		{
			PropertyPtr prop = prop_parent->getChild(k);
			if (prop != prop_parent && prop->getParent() && prop->getParent() == prop_parent)
			{
				int child = properties->addItem(prop->getName());
				properties->addItemChild(parent, child);
				item_prop.append(child, prop);
				attach_children(child, prop);
			}
		}
	};
	// building property hierarchy
	for (int i = 0; i < Properties::getNumProperties(); i++)
	{
		PropertyPtr prop_base = Properties::getProperty(i);
		if (prop_base->isBase())
		{
			int parent = properties->addItem(prop_base->getName());
			item_prop.append(parent, prop_base);
			attach_children(parent, prop_base);
		}
	}
	properties->getEventChanged().setEnabled(true);
}

/// method refreshing property parameters
void AppSystemLogic::properties_changed()
{
	parameters->getEventChanged().setEnabled(false);
	// clearing the list of property parameters and updating values displayed
	parameters->clear();
	value_gb->setEnabled(0);
	for (int i = 0; i <= 12; i++)
		label[i]->setText("");

	item_param.clear();

	int item = properties->getCurrentItem();
	if (item == -1)
	{
		parameters->getEventChanged().setEnabled(true);
		return;
	}
	// getting a property from the list in accordance with current selection
	PropertyPtr prop = item_prop[item];

	// getting a root parameter of the selected property
	PropertyParameterPtr pp = prop->getParameterPtr();

	// recursive function iterating through all parameters of a property
	std::function<void(int, const PropertyParameterPtr &)> add_parameters = [&, this](int parent, const PropertyParameterPtr &p)
	{
		for (int i = 0; i < p->getNumChildren(); i++)
		{
			PropertyParameterPtr child = p->getChild(i);
			int child_index = parameters->addItem(child->getName());
			parameters->setItemColor(child_index,
				vec4(
					itof(child->isInherited()),
					1,
					itof(!child->isOverridden()),
					child->isHidden() ? 0.5f : 1.0f));
			item_param.append(child_index, child);

			if (parent != -1)
				parameters->addItemChild(parent, child_index);

			add_parameters(child_index, child);
		}
	};

	// building the hierarchy of parameters for the selected property
	add_parameters(-1, pp);

	// preparing property information
	String pi = String::format("\nName: %s\nPath: %s\nInternal: %d\nStructs: %d\n", prop->getName(), prop->getFilePath(), prop->isInternal(), prop->getNumStructs());
	// adding all structures defined in the property (if any)
	for (int i = 0; i < prop->getNumStructs(); i++)
		pi += String::format("%d) %s\n", i, prop->getStructName(i));
	// displaying property information
	prop_info->setText(pi.get());

	parameters->getEventChanged().setEnabled(true);
	parameters->setCurrentItem(-1);
}
/// method refreshing information about the currently selected property parameter
void AppSystemLogic::parameters_changed()
{
	// checking if any property parameter is selected
	int item = parameters->getCurrentItem();
	if (item == -1)
		return;

	value_gb->setEnabled(1);
	// getting the parameter from the list in accordance with current selection
	PropertyParameterPtr p = item_param[item];
	int i = 0;
	label[i++]->setText(String::format("<font color=ffff00>ID:</font> %d", p->getID()));
	label[i++]->setText(String::format("<font color=ffff00>Name:</font> %s", p->getName()));
	label[i++]->setText(String::format("<font color=ffff00>Title:</font> %s", p->getTitle()));
	label[i++]->setText(String::format("<font color=ffff00>Tooltip:</font> %s", p->getTooltip()));
	label[i++]->setText(String::format("<font color=ffff00>Group:</font> %s", p->getGroup()));
	label[i++]->setText(String::format("<font color=ffff00>Filter:</font> %s", p->getFilter()));

	String s;
	// displaying parameter's type
	if (p->getType() == Property::PARAMETER_ARRAY)
		s = String::format("<font color=ffff00>Type:</font> array "
			"[<font color=ffff00>Size:</font> %d, <font color=ffff00>Type:</font> %s]", p->getArraySize(), p->getArrayTypeName());
	else if (p->getType() == Property::PARAMETER_STRUCT)
		s = String::format("<font color=ffff00>Type:</font> struct [<font color=ffff00>Struct Name:</font> %s]", p->getStructName());
	else
		s = String::format("<font color=ffff00>Type:</font> %s", p->getProperty()->parameterNameByType(p->getType()));
	label[i++]->setText(s.get());
	label[i++]->setText(String::format("<font color=ffff00>Hidden:</font> %d", p->isHidden()));
	label[i++]->setText(String::format("<font color=ffff00>Inherited:</font> %d", p->isInherited()));
	label[i++]->setText(String::format("<font color=ffff00>Overridden:</font> %d", p->isOverridden()));
	label[i++]->setText(String::format("<font color=ffff00>Has Min:</font> %d", p->hasSliderMinValue()));
	label[i++]->setText(String::format("<font color=ffff00>Has Max:</font> %d", p->hasSliderMaxValue()));
	s = "";
	if (p->getType() == Property::PARAMETER_INT)
		s = String::format("<font color=ffff00>Min:</font> %d <font color=ffff00>Max:</font> %d", p->getIntMinValue(), p->getIntMaxValue());
	else if (p->getType() == Property::PARAMETER_FLOAT)
		s = String::format("<font color=ffff00>Min:</font> %f <font color=ffff00>Max:</font> %f", p->getFloatMinValue(), p->getFloatMaxValue());
	else if (p->getType() == Property::PARAMETER_DOUBLE)
		s = String::format("<font color=ffff00>Min:</font> %f <font color=ffff00>Max:</font> %f", p->getDoubleMinValue(), p->getDoubleMaxValue());
	else if (p->getType() == Property::PARAMETER_SWITCH)
		s = String::format("<font color=ffff00>Switch Num Items:</font> %d", p->getSwitchNumItems());
	label[i++]->setText(s.get());
	value->setText(p->getValueString());
	reset->setEnabled(p->isOverridden());
}

/// change button on_click event handler
void AppSystemLogic::change_clicked(const WidgetPtr &button, int mbuttons)
{
	// checking if any property parameter is currently selected
	int item = parameters->getCurrentItem();
	if (item == -1)
		return;
	// setting the value of the currently selected property parameter and refreshing information
	PropertyParameterPtr pp = item_param[item];
	pp->setValue(value->getText());

	refresh_info();
}

/// reset button on_click event handler
void AppSystemLogic::reset_clicked(const WidgetPtr &button, int mbuttons)
{
	// checking if any property parameter is currently selected
	int item = parameters->getCurrentItem();
	if (item == -1)
		return;

	// resetting the value of the currently selected property parameter and refreshing information
	PropertyParameterPtr pp = item_param[item];
	pp->resetValue();

	refresh_info();
}

/// reload button on_click event handler
void AppSystemLogic::reload_clicked(const WidgetPtr &button, int mbuttons)
{
	// reload all properties and refreshing information
	Properties::reloadProperties();
	refresh_info();
}

/// method refreshing property and parameter information
void AppSystemLogic::refresh_info()
{
	// getting current indices of property and parameter selection
	int item_pr = properties->getCurrentItem();
	int item_pa = parameters->getCurrentItem();
	refresh_properties();

	// setting current items and updating information displayed
	properties->setCurrentItem(clamp(item_pr, -1, properties->getNumItems() - 1));
	properties_changed();
	parameters->setCurrentItem(clamp(item_pa, -1, parameters->getNumItems() - 1));
	parameters_changed();
}

void AppSystemLogic::clone_clicked(const WidgetPtr &button, int mbuttons)
{
	// checking if any property is selected in the hierarchy
	int item = properties->getCurrentItem();
	if (item == -1)
		return;
	// cloning the selected property
	PropertyPtr p = item_prop[item];
	PropertyPtr p_clone = p->clone();
	p_clone->setName(String::format("%s_cloned", p->getName()));

	// refreshing information displayed
	refresh_info();
}

/// inherit button on_click event handler
void AppSystemLogic::inherit_clicked(const WidgetPtr &button, int mbuttons)
{
	// checking if any property is selected in the hierarchy
	int item = properties->getCurrentItem();
	if (item == -1)
		return;
	// inheriting a new property from the selected one
	PropertyPtr p = item_prop[item];
	p->inherit()->setName(String::format("%s_inherited", p->getName()));

	// refreshing information displayed
	refresh_info();
}

/// method saving the currently selected property to the "my_test_prop.prop" file
void AppSystemLogic::save_prop_clicked(const WidgetPtr &button, int mbuttons)
{
	// checking if any property is selected in the hierarchy
	int item = properties->getCurrentItem();
	if (item == -1)
		return;
	// saving a property to the specified file
	PropertyPtr p = item_prop[item];
	p->save("my_test_prop.prop");
}
////////////////////////////////////////////////////////////////////////////////
// start of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppSystemLogic::update()
{
	// Write here code to be called before updating each render frame.
	return 1;
}

int AppSystemLogic::postUpdate()
{
	// Write here code to be called after updating each render frame.
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// end of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppSystemLogic::shutdown()
{
	// removing all event subscriptions somewhere on shutdown
	econnections.disconnectAll();
	return 1;
}

```

</details>


## Property Class

### Members

## Ptr < Node > getNode () const

Returns the current node to which the property is assigned.
### Return value

Current node to which the property is assigned.
## int getNumStructs () const

Returns the current number of structures of the property.
### Return value

Current number of structures of the property.
## Ptr < PropertyParameter > getParameterPtr () const

Returns the current root [property parameter](../../../api/library/common/class.propertyparameter_cpp.md).
You can't iterate through all parameters of the property in a single loop, a recursive function should be used instead:


```cpp
#include <functional>
std::function<void(const PropertyParameterPtr &)> recursive_func = [&, this](const PropertyParameterPtr &p)
{
	for (int i = 0; i < p->getNumChildren(); i++)
	{
		PropertyParameterPtr child = p->getChild(i);

		// do something... e.g. print parameter names and values
		Log::message("- %s: %s \n", child->getName(), child->getValueString().get());

		recursive_func(child);
	}
};

/* ... */
int AppWorldLogic::init() {
	/* ... */

	// getting the root parameter of the property
	PropertyParameterPtr root_parameter = property->getParameterPtr();

	// iterating through all parameters of the property
	recursive_func(root_parameter);

	return 1;
}

```


### Return value

Current root property parameter smart pointer.
## int getNumChildren () const

Returns the current number of children of the current property.
### Return value

Current number of child properties.
## bool isHierarchyValid () const

Returns the current value indicating if there are no missing parents in the hierarchy of the property.
### Return value

**true** if there are no missing parents in the hierarchy of the property; otherwise **false**.
## const UGUID & getFileGUID () const

Returns the current GUID of the property file.
### Return value

Current new [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the property file.
## const char * getFilePath () const

Returns the current [path](#name_path) to the property file.
### Return value

Current [path](#name_path) to the property file.
## UGUID getGUID () const

Returns the current GUID of the property.
### Return value

Current GUID of the property.
## void setName ( const char * name )

Sets a new new [name](../../../code/formats/property_format.md#property_name) for the property.
> **Notice:** This method is not available for [manual](#isManual_int) and [non-editable](#isEditable_int) properties.


### Arguments

- *const char ** **name** - The property [name](../../../code/formats/property_format.md#property_name). > **Notice:** If the property is [internal](#isInternal_int) and has a parent, the parent's name will be returned.

## const char * getName () const

Returns the current new [name](../../../code/formats/property_format.md#property_name) for the property.
> **Notice:** This method is not available for [manual](#isManual_int) and [non-editable](#isEditable_int) properties.


### Return value

Current property [name](../../../code/formats/property_format.md#property_name).
> **Notice:** If the property is [internal](#isInternal_int) and has a parent, the parent's name will be returned.

## bool isEngine () const

Returns the current value indicating if the property is engine-related (i.e. required for engine operation).
Such properties are stored in the `core`, `editor` and `editor2` folders.

### Return value

**true** if the property is engine-related; otherwise **false**.
## bool isManual () const

Returns the current value indicating if the property is a [manual](../../../principles/properties/index.md#manual) one.
### Return value

**true** if the property is manual; otherwise **false**.
## bool isInternal () const

Returns the current value indicating if the property is an [internal](../../../principles/properties/index.md#internal) one.
### Return value

**true** if the property is internal; otherwise **false**.
## bool isEditable () const

Returns the current value indicating if the property can be [edited](../../../code/formats/property_format.md#property_editable).
### Return value

**true** if the property is editable; otherwise **false**.
## bool isHidden () const

Returns the current value indicating if the property is [hidden](../../../code/formats/property_format.md#property_hidden).
### Return value

**true** if the property is hidden; otherwise **false**.
## bool isBase () const

Returns the current value indicating if the property is a base property.
### Return value

**true** if the property is a base property; otherwise **false**.
## int getID () const

Returns the current identifier of the property.
### Return value

Current property ID.
## Ptr < Property > getParent () const

Returns the current [parent](../../../code/formats/property_format.md#property_parent) property.
### Return value

Current parent property if it exists; if the current property has no parent, nullptr will be returned.
## const char * getTooltip () const

Returns the current tooltip for the property.
### Return value

Current tooltip for the property.
## int getNumInterfaces () const

Returns the current total number of interfaces.
> **Notice:** You can use interfaces only within the C# Component System. For more information, see the article [C# Interfaces and Abstract Classes.](../../../code/csharp/interfaces_and_abstract_classes.md).

### Return value

Current total number of interfaces.
## Event<const Ptr < Property > &> getEventDestroy () const

event triggered when the property is destroyed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Destroy event handler
void destroy_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Destroy event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections destroy_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventDestroy().connect(destroy_event_connections, destroy_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventDestroy().connect(destroy_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Destroy event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
destroy_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection destroy_event_connection;

// subscribe to the Destroy event with a handler function keeping the connection
publisher->getEventDestroy().connect(destroy_event_connection, destroy_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
destroy_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
destroy_event_connection.setEnabled(true);

// ...

// remove subscription to the Destroy event via the connection
destroy_event_connection.disconnect();

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

	// A Destroy event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Destroy event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventDestroy().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId destroy_handler_id;

// subscribe to the Destroy event with a lambda handler function and keeping connection ID
destroy_handler_id = publisher->getEventDestroy().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Destroy event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventDestroy().disconnect(destroy_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Destroy events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventDestroy().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventDestroy().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Property > &, int> getEventParameterChanged () const

event triggered when the value of any parameter of the property is changed or reset to default. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**, int **param_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ParameterChanged event handler
void parameterchanged_event_handler(const Ptr<Property> & property,  int param_index)
{
	Log::message("\Handling ParameterChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections parameterchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventParameterChanged().connect(parameterchanged_event_connections, parameterchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventParameterChanged().connect(parameterchanged_event_connections, [](const Ptr<Property> & property,  int param_index) {
		Log::message("\Handling ParameterChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
parameterchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection parameterchanged_event_connection;

// subscribe to the ParameterChanged event with a handler function keeping the connection
publisher->getEventParameterChanged().connect(parameterchanged_event_connection, parameterchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
parameterchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
parameterchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the ParameterChanged event via the connection
parameterchanged_event_connection.disconnect();

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

	// A ParameterChanged event handler implemented as a class member
	void event_handler(const Ptr<Property> & property,  int param_index)
	{
		Log::message("\Handling ParameterChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventParameterChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId parameterchanged_handler_id;

// subscribe to the ParameterChanged event with a lambda handler function and keeping connection ID
parameterchanged_handler_id = publisher->getEventParameterChanged().connect(e_connections, [](const Ptr<Property> & property,  int param_index) {
		Log::message("\Handling ParameterChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventParameterChanged().disconnect(parameterchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ParameterChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventParameterChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventParameterChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Property > &> getEventReparented () const

event triggered when the parent of the property is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Reparented event handler
void reparented_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Reparented event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections reparented_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventReparented().connect(reparented_event_connections, reparented_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventReparented().connect(reparented_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Reparented event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
reparented_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection reparented_event_connection;

// subscribe to the Reparented event with a handler function keeping the connection
publisher->getEventReparented().connect(reparented_event_connection, reparented_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
reparented_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
reparented_event_connection.setEnabled(true);

// ...

// remove subscription to the Reparented event via the connection
reparented_event_connection.disconnect();

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

	// A Reparented event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Reparented event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventReparented().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId reparented_handler_id;

// subscribe to the Reparented event with a lambda handler function and keeping connection ID
reparented_handler_id = publisher->getEventReparented().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Reparented event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventReparented().disconnect(reparented_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Reparented events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventReparented().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventReparented().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Property > &> getEventRenamed () const

event triggered when the [name](#name_path) of the property is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Renamed event handler
void renamed_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Renamed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections renamed_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventRenamed().connect(renamed_event_connections, renamed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventRenamed().connect(renamed_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Renamed event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
renamed_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection renamed_event_connection;

// subscribe to the Renamed event with a handler function keeping the connection
publisher->getEventRenamed().connect(renamed_event_connection, renamed_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
renamed_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
renamed_event_connection.setEnabled(true);

// ...

// remove subscription to the Renamed event via the connection
renamed_event_connection.disconnect();

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

	// A Renamed event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Renamed event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventRenamed().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId renamed_handler_id;

// subscribe to the Renamed event with a lambda handler function and keeping connection ID
renamed_handler_id = publisher->getEventRenamed().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Renamed event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventRenamed().disconnect(renamed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Renamed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventRenamed().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventRenamed().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Property > &> getEventMoved () const

event triggered when the [path](#name_path) of the property is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Moved event handler
void moved_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Moved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections moved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventMoved().connect(moved_event_connections, moved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventMoved().connect(moved_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Moved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
moved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection moved_event_connection;

// subscribe to the Moved event with a handler function keeping the connection
publisher->getEventMoved().connect(moved_event_connection, moved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
moved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
moved_event_connection.setEnabled(true);

// ...

// remove subscription to the Moved event via the connection
moved_event_connection.disconnect();

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

	// A Moved event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Moved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventMoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId moved_handler_id;

// subscribe to the Moved event with a lambda handler function and keeping connection ID
moved_handler_id = publisher->getEventMoved().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Moved event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventMoved().disconnect(moved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Moved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventMoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventMoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Property > &> getEventReloaded () const

event triggered when the property is reloaded. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Reloaded event handler
void reloaded_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Reloaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections reloaded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventReloaded().connect(reloaded_event_connections, reloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventReloaded().connect(reloaded_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Reloaded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
reloaded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection reloaded_event_connection;

// subscribe to the Reloaded event with a handler function keeping the connection
publisher->getEventReloaded().connect(reloaded_event_connection, reloaded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
reloaded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
reloaded_event_connection.setEnabled(true);

// ...

// remove subscription to the Reloaded event via the connection
reloaded_event_connection.disconnect();

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

	// A Reloaded event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Reloaded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventReloaded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId reloaded_handler_id;

// subscribe to the Reloaded event with a lambda handler function and keeping connection ID
reloaded_handler_id = publisher->getEventReloaded().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Reloaded event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventReloaded().disconnect(reloaded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Reloaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventReloaded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventReloaded().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static PropertyPtr create ( )

Constructor. Creates a new property instance.
## Ptr < Property > getChild ( int num ) const

Returns the child property of the current property.
### Arguments

- *int* **num** - The number of the target child property.

### Return value

Child property.
## void setEditable ( int editable )

Sets a value indicating if the property can be [edited](../../../code/formats/property_format.md#property_editable).
### Arguments

- *int* **editable** - 1 to make the property editable; 0 to make it read-only.

## bool hasOverrides ( ) const

Returns a value indicating if the property has at least one overridden parameter.
### Return value

true if the property has at least one overridden parameter; otherwise, false.
## bool isParent ( const char * name ) const


Returns a value indicating if the property with the given name is a [parent](../../../code/formats/property_format.md#property_parent) of this property.


Suppose we have the following two manual properties in our project:


- ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.7.3" name="my_prop" parent_name="surface_base" manual="1"> <parameter name="my_parameter">100</parameter> </property> ```
- ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.7.3" name="my_prop_0" parent_name="my_prop" manual="1"> <parameter name="my_parameter1">101</parameter> <parameter name="my_parameter2">101</parameter> </property> ```


The following code will return 1 as the *my_prop* property is the parent of the *my_prop_0* property:


```cpp
// get a property named my_prop_0
PropertyPtr property = Properties::findManualProperty("my_prop_0");
// perform parent check
Log::message("%d\n",property->isParent("my_prop"));

```


### Arguments

- *const char ** **name** - Parent property name.

### Return value

true if the property with the given name is a parent of this property; otherwise, false.
## bool isParent ( const UGUID & guid ) const

Returns a value indicating if the property with the given GUID is a [parent](../../../code/formats/property_format.md#property_parent) of this property.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Parent property GUID.

### Return value

true if the property with the given GUID is a parent of this property; otherwise, false.
## int setParent ( const Ptr < Property > & property , bool save_all_values = 0 )


Sets the given property as the parent for this property and saves the parameter values of the property (if the corresponding flag is set).


> **Notice:** The method is not available for [manual](#isManual_int) and [non-editable](#isEditable_int) properties.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Property to be set as the parent for this property.
- *bool* **save_all_values** - Flag indicating if parameter values of the property will be saved after reparenting.

### Return value

1 if the given property was successfully set as the parent for this property; otherwise, 0.
## Ptr < Property > clone ( )

Clones the property. The cloned property won't have a name, a path and won't be displayed in the properties hierarchy.
### Return value

Cloned property smart pointer.
## Ptr < Property > clone ( const char * name , const char * path )

Clones the property and assigns the specified name and path to the clone. The cloned property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_cpp.md#saveProperties_int)* call. This method may be used, for example, to create a property missed during project's migration.
### Arguments

- *const char ** **name** - Cloned property name.
- *const char ** **path** - Path to save the cloned property.

### Return value

Cloned property smart pointer.
## Ptr < Property > clone ( const char * name , const char * path , const UGUID & guid )

Clones the property and assigns the specified name, GUID and path to the clone. The cloned property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_cpp.md#saveProperties_int)* call. This method may be used, for example, to create a property missed during project's migration.
### Arguments

- *const char ** **name** - Cloned property name.
- *const char ** **path** - Path to save the cloned property.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Cloned property [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Cloned property smart pointer.
## Ptr < Property > clone ( const char * name )

Clones the property.
```cpp
// get a property to be cloned
PropertyPtr property = Properties::findProperty("surface_base_0");
// clone the property
PropertyPtr cloned = property->clone("cloned_surface_base_0");
// perform something on the cloned pointer
// ...
// delete the pointer
cloned.grab();
cloned.destroy();

```


### Arguments

- *const char ** **name** - Cloned property name.

### Return value

Cloned property smart pointer.
## Ptr < Property > inherit ( )

Inherits a new property from this one. The inherited property will be empty: it won't have a name, a path and won't be displayed in the properties hierarchy.
### Return value

Inherited property smart pointer.
## Ptr < Property > inherit ( const char * name )

Inherits a new property from this one and assigns the specified name to it.
### Arguments

- *const char ** **name** - Inherited property name.

### Return value

Inherited property smart pointer.
## Ptr < Property > inherit ( const char * name , const char * path )

Inherits a new property from this one and assigns the specified name and path to it. The inherited property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_cpp.md#saveProperties_int)* call.
### Arguments

- *const char ** **name** - Inherited property name.
- *const char ** **path** - Path to save the inherited property.

### Return value

Inherited property smart pointer.
## Ptr < Property > inherit ( const char * name , const char * path , const UGUID & guid )

Inherits a new property from this one and assigns the specified name, GUID and path to it. The inherited property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_cpp.md#saveProperties_int)* call.
### Arguments

- *const char ** **name** - Inherited property name.
- *const char ** **path** - Path to save the inherited property.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Inherited property [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Inherited property smart pointer.
## bool load ( )


Loads the property from the file specified by the *[setFilePath()](#setFilePath_cstr_int)* function.


> **Notice:** This function can be used to load properties created during application execution or stored outside the `data` directory.


### Return value

true if the property data is loaded successfully; otherwise, false.
## bool load ( const char * path )

Loads the property from the specified [`*.prop` file](../../../code/formats/property_format.md).
### Arguments

- *const char ** **path** - Path to the `*.prop` file to load the property data from.

### Return value

true if the property data is loaded successfully; otherwise, false.
## bool loadXml ( const Ptr < Xml > & xml )

Loads data of the property (all its parameters) from the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../api/library/common/class.xml_cpp.md) instance in which the property data is stored.

### Return value

true if the property data is loaded successfully; otherwise, false.
## bool loadWorld ( const Ptr < Xml > & xml )

Loads data of the current property (all its options, states and parameters) from the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../api/library/common/class.xml_cpp.md) instance in which the property data is stored.

### Return value

true if the property data is loaded successfully; otherwise, false.
## bool reload ( )

Reloads the property and all its children.
### Return value

true if the property is reloaded successfully; otherwise, false.
## bool canSaveInFile ( ) const

Returns a value indicating if the property can be saved to a file. For example, this function will return 0 for an [internal](#isInternal_int) or [manual](#isManual_int) property.
### Return value

true if the property can be saved to a file; otherwise, false.
## bool saveState ( const Ptr < Stream > & stream ) const


Saves data of the current property (all its parameters) into a binary stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int_int)* methods:


```cpp
// somewhere in code

// getting a manual property named "my_prop" via the Property Manager
PropertyPtr property = Properties::findManualProperty("my_prop");
property->setParameterInt(property->findParameter("my_int_param"), 3);

// save state
Blob blob_state = new Blob();
property.SaveState(blob_state);

// change state
property->setParameterInt(property->findParameter("my_int_param"), 4);

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
propertyparam1.RestoreState(blob_state, 0);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream into which the property data will be saved.

### Return value

true if the property data is saved successfully; otherwise, false.
## bool restoreState ( const Ptr < Stream > & stream , int restore_mode = 0 )


Restores the data of the property (all its parameters) from a binary stream in the specified mode.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```cpp
// somewhere in code

// getting a manual property named "my_prop" via the Property Manager
PropertyPtr property = Properties::findManualProperty("my_prop");
property->setParameterInt(property->findParameter("my_int_param"), 3);

// save state
Blob blob_state = new Blob();
property.SaveState(blob_state);

// change state
property->setParameterInt(property->findParameter("my_int_param"), 4);

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
propertyparam1.RestoreState(blob_state, 0);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream in which the saved property parameter data is stored.
- *int* **restore_mode** - Restore mode. One of the [Property::RESTORE_MODE_*](#RESTORE_MODE_MERGE) values. The default value is [Property::RESTORE_MODE_REPLACE](#RESTORE_MODE_REPLACE).

### Return value

true on success; otherwise, false.
## bool save ( )


Saves the property data to the file specified by the *[setFilePath()](#setFilePath_cstr_int)* function.


> **Notice:** This method is not available for [manual](#isManual_int) and [internal](#isInternal_int) properties.


### Return value

true if the property data is saved successfully; otherwise, false.
## bool save ( const char * path )


Saves the property data to the specified [`*.prop` file](../../../code/formats/property_format.md).


> **Notice:** This method is not available for [manual](#isManual_int) properties.


### Arguments

- *const char ** **path** - Path to the `*.prop` file to save the property data to.

### Return value

true if the property data is saved successfully; otherwise, false.
## bool saveXml ( const Ptr < Xml > & xml ) const


Saves data of the property (all its parameters) to the given instance of the Xml class.


> **Notice:** This method is not available for [manual](#isManual_int) properties.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../api/library/common/class.xml_cpp.md) instance into which the property data will be saved.

### Return value

true if the property data is saved successfully; otherwise, false.
## bool saveWorld ( const Ptr < Xml > & xml , int force = 0 ) const

Saves data of the current property (all its parameters) into the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../api/library/common/class.xml_cpp.md) instance into which the property data will be saved.
- *int* **force** - A value indicating if forced saving of property data is used: 1 to enable forced saving, 0 to disable it.

### Return value

true if the property data is saved successfully; otherwise, false.
## int parameterTypeByName ( const char * param_type ) const

Returns parameter type identifier by the type name specified.
### Arguments

- *const char ** **param_type** - Parameter type name.

### Return value

Parameter type identifier, one of the [PARAMETER_*](#PARAMETER_COLOR) variables.
## const char * parameterNameByType ( int param_type ) const

Returns parameter type name by the type identifier specified.
### Arguments

- *int* **param_type** - Parameter type identifier, one of the [PARAMETER_*](#PARAMETER_COLOR) variables.

### Return value

Parameter type name.
## Ptr < PropertyParameter > getParameterPtr ( const char * name )

Returns a [property parameter](../../../api/library/common/class.propertyparameter_cpp.md) by its name.
### Arguments

- *const char ** **name** - Property parameter name.

### Return value

Property parameter smart pointer.


> **Notice:** This method never returns nullptr, regardless of whether a parameter with the specified name exists or not. It only displays an error message in the console in case of a non-existing parameter. To check if such parameter really exists, use the [*PropertyParameter.isExist()*](../../../api/library/common/class.propertyparameter_cpp.md#isExist_int) method. For example:
>
>
> ```cpp
> // getting some property named "my_property"
> PropertyPtr pProperty = Properties::findManualProperty("my_property");
>
> // trying to get a property parameter named "some_parameter"
> PropertyParameterPtr param = pProperty->getParameterPtr("some_parameter");
>
> // checking if such parameter exists and displaying a message
> if (param->isExist())
> 	Log::message("Specified property parameter exists!\n");
> else
> 	Log::message("No such parameter!\n");
>
> ```


## Ptr < PropertyParameter > getParameterPtr ( int id )

Returns a [property parameter](../../../api/library/common/class.propertyparameter_cpp.md) by its ID.
### Arguments

- *int* **id** - Property parameter ID.

### Return value

Property parameter smart pointer.


> **Notice:** This method never returns nullptr, regardless of whether a parameter with the specified ID exists or not. It only displays an error message in the console in case of a non-existing parameter. To check if such parameter really exists, use the [*PropertyParameter.isExist()*](../../../api/library/common/class.propertyparameter_cpp.md#isExist_int) method. For example:
>
>
> ```cpp
> // getting some property named "my_property"
> PropertyPtr pProperty = Properties::findManualProperty("my_property");
>
> // trying to get a property parameter having the ID=30
> PropertyParameterPtr param = pProperty->getParameterPtr(30);
>
> // checking if such parameter exists and displaying a message
> if (param->isExist())
> 	Log::message("Property parameter with the specified ID exists!\n");
> else
> 	Log::message("No such parameter!\n");
>
> ```


## int findStruct ( const char * name ) const

Returns the number of the structure with the specified name.
### Arguments

- *const char ** **name** - Name of the structure to be found.

### Return value

Number of the structure with the specified name, if it exists; otherwise, -1.
## const char * getStructName ( int num ) const

Returns the name of the structure with the specified number.
### Arguments

- *int* **num** - Structure number.

### Return value

Structure name, if such structure exists, otherwise nullptr.
## const char * getInterfaceName ( int num ) const


Returns the name of the interface with the specified number.


> **Notice:** You can use interfaces only within the C# Component System. For more information, see the article [C# Interfaces and Abstract Classes.](../../../code/csharp/interfaces_and_abstract_classes.md).

### Arguments

- *int* **num** - Interface number.

### Return value

Interface name, if such interface exists, otherwise nullptr.
## bool setFileGUID ( const UGUID & fileguid )

Changes the GUID of the file this property is stored in, re-binding the property to another property file.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **fileguid** - New file GUID.

### Return value

true if the file GUID is changed successfully or already matches the current one; otherwise, false (another property is already registered with that file GUID).
## bool setFilePath ( const char * path )

Sets the path of the file the property is stored in: the path is registered as a virtual file in the engine file system and the resulting GUID is assigned to the property.
### Arguments

- *const char ** **path** - Target file path.

### Return value

true on success; otherwise, false (a different property already occupies the resulting file GUID).
