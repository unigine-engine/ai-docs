# Unigine::Property Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class provides an interface for property manipulation: it is used to modify [properties](../../../principles/world_structure/index.md#properties) that allow you to control values of the logic-related parameters. When a property is assigned to a node, an instanced [internal property](../../../principles/properties/index.md#internal) is created and saved into a `.world` or `.node` file. However, rather than the whole list of parameters it contains only the modified ones.


The concepts of a [path](#setFilePath_cstr_int) and a [name](#setName_cstr_void) of the property should be distinguished:


- The **path** specifies where the property is stored on the disk. The path includes a property file name.
- The **name** specifies how the property will be displayed in the UnigineEditor (the Property Hierarchy window, the nodes surface section of the Parameters window). The name can also be used to refer to a property from the [code](../../../api/library/engine/class.properties_usc.md#findProperty_cstr_Property).


By default, the property name and the `*.prop` file name coincide.


By using functions of this class, you can, for example, implement a *properties editor*.


**Properties** specify the way the object will behave and interact with other objects and the scene environment.


A property is a "material" for application logic represented by a set of logic-related **[parameters](../../../code/formats/property_format.md#element_parameter)**. Properties can be used to build [**components**](../../../principles/component_system/index.md) to extend the functionality of nodes.


All properties in the project are organized into a [hierarchy](../../../principles/properties/inheritance.md). To be modified, properties should be obtained from the hierarchy via [*API*](../../../api/library/engine/class.properties_usc.md) functions.


Property parameters are managed individually via the *[PropertyParameter](../../../api/library/common/class.propertyparameter_usc.md)* class, to get any parameter by its name or ID you should use the **[getParameterPtr()()](../../...md#getParameterPtr_cstr_PropertyParameter)** method.


Automatic type conversion of property parameters make them act like some universal variables i.e. you can set a new value for an integer parameter int_param and type it like this:


> **Notice:** You can modify only existing parameters of the property. To add or remove new parameters, you should manually edit the `.prop` file or use API to edit the XML file via the code.


### Adding and Removing Properties


> **Notice:** The *Property* class doesn't allow adding a new property to the property hierarchy.


A new property can be added to the hierarchy in one of the following ways:


- By creating and editing the corresponding `.prop` file manually. For example, in the `data` folder let us create the following file describing a property for a GameObjectUnit: ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.7.3" manual="1" editable="0" name="GameObjectsUnit"> <parameter name="weapon_type" type="switch" items="air,land,all_types">0</parameter> <parameter name="attack" type="toggle">1</parameter> <parameter name="damage" type="int" max="1000">1</parameter> <parameter name="velocity" type="float" max="100">30</parameter> <parameter name="material" type="string"/> </property> ``` > **Notice:** If the new property is assigned to a surface, it is recommended to inherit it from the *surface_base* property or one of its children.
- By inheriting from the existing property via the [*engine.properties.inheritProperty()*](../../../api/library/engine/class.properties_usc.md#inheritProperty_UGUID_cstr_cstr_Property) function or [*inherit()*](#inherit_cstr_Property) function of the Property class. For example: ```cpp // inherit a GameObjectsUnit_0 property from the GameObjectsUnit property Property inherited_prop = engine.properties.findManualProperty("GameObjectsUnit").inherit("GameObjectsUnit_0", "game_object_unit_0.prop"); // inherit a GameObjectsUnit_1 property from the GameObjectsUnit_0 property via the Manager engine.properties.inheritProperty(inherited_prop.getGUID(), "GameObjectsUnit_1", "game_object_unit_1.prop"); ``` To save all properties in the hierarchy that can be saved (i.e., editable, having a path specified, and not internal or manual ones) via the [*engine.properties.saveProperties()*](../../../api/library/engine/class.properties_usc.md#saveProperties_int) function. > **Notice:** By default, all parameters and states of the inherited property are the same as specified in the parent property. A child property can [override some parameters of its parent or add new ones](../../../principles/world_structure/index.md#properties_hierarchy).
- By editing the corresponding `.prop` file [via API](../../../api/library/common/class.xml_usc.md): you can open an XML file, write data into it and save it.


To delete a property, you can simply call the *[engine.properties.removeProperty()](../../../api/library/engine/class.properties_usc.md#removeProperty_UGUID_int_int_int)* function:


```cpp
// remove the property with the given name with all its children and delete the *.prop file
engine.properties.removeProperty(engine.properties.findProperty("GameObjectsUnit_0").getGUID(), 1, 1);

```


### Handling Events


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


Below is the source code in UnigineScript implementing our Property Viewer. You can copy and paste it to the corresponding files of your project.


<details>
<summary>my_world.usc | Close</summary>

**my_world.usc**


```cpp
#include <core/unigine.h>
// This file is in UnigineScript language.
// World script, it takes effect only when the world is loaded.

	// declaring UI widgets to be used
    WidgetWindow window;
    WidgetHBox hbox;

    WidgetGroupBox properties_gb;
    WidgetTreeBox properties;
    WidgetGroupBox parameters_gb;
    WidgetTreeBox parameters;
    WidgetGroupBox value_gb;
    WidgetGroupBox menu_gb;

    WidgetVBox vbox2, vbox3;
    WidgetHBox hbox2;
    WidgetButton reload;
    WidgetButton clone;
    WidgetButton inherit;
    WidgetButton save_prop;

    // UI widgets for values
    WidgetLabel label[0];
    WidgetEditLine value;
    WidgetButton change;
    WidgetButton reset;

    WidgetLabel info;
    WidgetLabel prop_info;
	// lists of properties and parameters
    int item_prop[];
    int item_param[];

/// method refreshing properties
void refresh_properties()
{
	properties.setCallbackEnabled(GUI_CHANGED, 0);
	properties.clear();
	item_prop.clear();

	// recursive function iterating through all children properties and building property hierarchy
	void attach_children(int parent, Property prop_parent)
	{
		for (int k = 0; k < prop_parent.getNumChildren(); k++)
		{
			Property prop = prop_parent.getChild(k);

			if ((prop.getParent() != NULL) && (prop != prop_parent) && (prop.getParent() == prop_parent))
			{
				int child = properties.addItem(prop.getName());
				properties.addItemChild(parent, child);
				item_prop.append(child, prop);
				attach_children(child, prop);
			}
		}
	}
	// building property hierarchy
	for (int i = 0; i < engine.properties.getNumProperties(); i++)
	{
		Property prop_base = engine.properties.getProperty(i);
		if (prop_base.isBase() == 1)
		{
			int parent = properties.addItem(prop_base.getName());
			item_prop.append(parent, prop_base);
			attach_children(parent, prop_base);
		}
	}
	properties.setCallbackEnabled(GUI_CHANGED, 1);
}

/// method refreshing property parameters
void properties_changed()
{
	parameters.setCallbackEnabled(GUI_CHANGED, 0);
	// clearing the list of property parameters and updating values displayed
	parameters.clear();
	value_gb.setEnabled(0);
	for (int i = 0; i <= 12; i++)
		label[i].setText("");

	item_param.clear();

	int item = properties.getCurrentItem();
	if (item == -1)
	{
		parameters.setCallbackEnabled(GUI_CHANGED, 1);
		return;
	}
	// getting a property from the list in accordance with current selection
	Property prop = item_prop[item];

	// getting a root parameter of the selected property
	PropertyParameter pp = prop.getParameterPtr();

	// recursive function iterating through all parameters of a property
	void add_parameters(int parent, PropertyParameter p)
	{
		for (int i = 0; i < p.getNumChildren(); i++)
		{
			PropertyParameter child = p.getChild(i);
			int child_index = parameters.addItem(child.getName());
			parameters.setItemColor(child_index,
				Vec4(
				(child.isInherited()),
				1,
				(1 - child.isOverridden()),
				(child.isHidden() == 1) ? 0.5f : 1.0f));
		item_param.append(child_index, child);

			if (parent != -1)
				parameters.addItemChild(parent, child_index);

			add_parameters(child_index, child);
		}
	}

	// building the hierarchy of parameters for the selected property
	add_parameters(-1, pp);

	// preparing property information
	string pi = format("\nName: %s\nPath: %s\nInternal: %d\nStructs: %d\n", prop.getName(), prop.getFilePath(), prop.isInternal(), prop.getNumStructs());
	// adding all structures defined in the property (if any)
	for (int i = 0; i < prop.getNumStructs(); i++)
		pi += format("%d) %s\n", i, prop.getStructName(i));
	// displaying property information
	prop_info.setText(pi);

	parameters.setCallbackEnabled(GUI_CHANGED, 1);
	parameters.setCurrentItem(-1);
}

/// method refreshing information about the currently selected property parameter
void parameters_changed()
{
    // checking if any property parameter is selected
	int item = parameters.getCurrentItem();
	if (item == -1)
		return;

	value_gb.setEnabled(1);
	// getting the parameter from the list in accordance with current selection
	PropertyParameter p = item_param[item];
	int i = 0;
	label[i++].setText(format("<font color=ffff00>ID:</font> %d", p.getID()));
	label[i++].setText(format("<font color=ffff00>Name:</font> %s", p.getName()));
	label[i++].setText(format("<font color=ffff00>Title:</font> %s", p.getTitle()));
	label[i++].setText(format("<font color=ffff00>Tooltip:</font> %s", p.getTooltip()));
	label[i++].setText(format("<font color=ffff00>Group:</font> %s", p.getGroup()));
	label[i++].setText(format("<font color=ffff00>Filter:</font> %s", p.getFilter()));

	string s;
	// displaying parameter's type
	if (p.getType() == PROPERTY_PARAMETER_ARRAY)
		s = format("<font color=ffff00>Type:</font> array [<font color=ffff00>Size:</font> %d, <font color=ffff00>Type:</font> %s]", p.getArraySize(), p.getArrayTypeName());
	else if (p.getType() == PROPERTY_PARAMETER_STRUCT)
		s = format("<font color=ffff00>Type:</font> struct [<font color=ffff00>Struct Name:</font> %s]", p.getStructName());
	else
		s = format("<font color=ffff00>Type:</font> %s", p.getProperty().parameterNameByType(p.getType()));
	label[i++].setText(s);
	label[i++].setText(format("<font color=ffff00>Hidden:</font> %d", p.isHidden()));
	label[i++].setText(format("<font color=ffff00>Inherited:</font> %d", p.isInherited()));
	label[i++].setText(format("<font color=ffff00>Overridden:</font> %d", p.isOverridden()));
	label[i++].setText(format("<font color=ffff00>Has Min:</font> %d", p.hasSliderMinValue()));
	label[i++].setText(format("<font color=ffff00>Has Max:</font> %d", p.hasSliderMaxValue()));
	s = "";
	if (p.getType() == PROPERTY_PARAMETER_INT)
		s = format("<font color=ffff00>Min:</font> %d <font color=ffff00>Max:</font> %d", p.getIntMinValue(), p.getIntMaxValue());
	else if (p.getType() == PROPERTY_PARAMETER_FLOAT)
		s = format("<font color=ffff00>Min:</font> %d <font color=ffff00>Max:</font> %d", p.getFloatMinValue(), p.getFloatMaxValue());
	else if (p.getType() == PROPERTY_PARAMETER_DOUBLE)
		s = format("<font color=ffff00>Min:</font> %d <font color=ffff00>Max:</font> %d", p.getDoubleMinValue(), p.getDoubleMaxValue());
	else if (p.getType() == PROPERTY_PARAMETER_SWITCH)
		s = format("<font color=ffff00>Switch Num Items:</font> %d", p.getSwitchNumItems());
	label[i++].setText(s);
	value.setText(p.getValueString());
	reset.setEnabled(p.isOverridden());
}

/// change button on_click event handler
void change_clicked()
{
    // checking if any property parameter is currently selected
    int item = parameters.getCurrentItem();
    if (item == -1)
        return;
    // setting the value of the currently selected property parameter and refreshing information
    PropertyParameter pp = item_param[item];
    pp.setValue(value.getText());

    refresh_info();
}

/// reset button on_click event handler
void reset_clicked()
{
    // checking if any property parameter is currently selected
    int item = parameters.getCurrentItem();
    if (item == -1)
        return;

    // resetting the value of the currently selected property parameter and refreshing information
    PropertyParameter pp = item_param[item];
    pp.resetValue();

    refresh_info();
}

/// reload button on_click event handler
void reload_clicked()
{
    // reload all properties and refreshing information
    engine.properties.reloadProperties();
    refresh_info();
}

/// method refreshing property and parameter information
void refresh_info()
{
	// getting current indices of property and parameter selection
	int item_pr = properties.getCurrentItem();
	int item_pa = parameters.getCurrentItem();
	refresh_properties();

	// setting current items and updating information displayed
	properties.setCurrentItem(clamp(item_pr, -1, properties.getNumItems() - 1));
	properties_changed();
	parameters.setCurrentItem(clamp(item_pa, -1, parameters.getNumItems() - 1));
	parameters_changed();
}

/// clone button on_click event handler
void clone_clicked()
{
    // checking if any property is selected in the hierarchy
    int item = properties.getCurrentItem();
    if (item == -1)
        return;
    // cloning the selected property
    Property p = item_prop[item];
    Property p_clone = p.clone();
    p_clone.setName(format("%s_cloned", p.getName()));

    // refreshing information displayed
    refresh_info();
}

/// inherit button on_click event handler
void inherit_clicked()
{
    // checking if any property is selected in the hierarchy
    int item = properties.getCurrentItem();
    if (item == -1)
        return;
    // inheriting a new property from the selected one
    Property p = item_prop[item];
    p.inherit().setName(format("%s_inherited", p.getName()));

	// refreshing information displayed
    refresh_info();
}

/// method saving the currently selected property to the "my_test_prop.prop" file
void save_prop_clicked()
{
    // checking if any property is selected in the hierarchy
    int item = properties.getCurrentItem();
    if (item == -1)
        return;
    // saving a property to the specified file
    Property p = item_prop[item];
    p.save("my_test_prop.prop");
}

int init() {
	// Write here code to be called on world initialization: initialize resources for your world scene during the world start.

	Player player = new PlayerSpectator();
	player.setPosition(Vec3(0.0f,3.401f,1.5f));
	player.setDirection(Vec3(0.0f,-1.0f,-0.4f));
	engine.game.setPlayer(player);
	Property property = engine.properties.findManualProperty("my_property");

	engine.app.setUpdate(1);

	// creating user interface
	Gui gui = engine.getGui();

	window = new WidgetWindow(gui, "Properties Viewer");
	window.setSizeable(1);
	window.setWidth(engine.app.getWidth());
	window.setHeight(engine.app.getHeight());
	gui.addChild(window, GUI_ALIGN_OVERLAP);

	vbox2 = new WidgetVBox(gui);
	window.addChild(vbox2, GUI_ALIGN_EXPAND);

	hbox = new WidgetHBox(gui);
	vbox2.addChild(hbox, GUI_ALIGN_EXPAND);

	properties_gb = new WidgetGroupBox(gui, "Properties");
	parameters_gb = new WidgetGroupBox(gui, "Parameters");
	hbox.addChild(properties_gb, GUI_ALIGN_EXPAND);
	hbox.addChild(parameters_gb, GUI_ALIGN_EXPAND);

	properties = new WidgetTreeBox(gui);
	parameters = new WidgetTreeBox(gui);
	properties_gb.addChild(properties, GUI_ALIGN_EXPAND);
	parameters_gb.addChild(parameters, GUI_ALIGN_EXPAND);

	vbox3 = new WidgetVBox(gui);
	hbox.addChild(vbox3, GUI_ALIGN_EXPAND);
	value_gb = new WidgetGroupBox(gui, "Value");
	value_gb.setWidth(300);
	value_gb.setHeight(300);
	value_gb.arrange();
	menu_gb = new WidgetGroupBox(gui, "Menu");
	vbox3.addChild(value_gb, GUI_ALIGN_LEFT);
	vbox3.addChild(menu_gb, GUI_ALIGN_EXPAND);

	label.append(new WidgetLabel(gui, ""));
	label[label.size()-1].setFontRich(1);
	value_gb.addChild(label[label.size()-1], GUI_ALIGN_LEFT);
	value = new WidgetEditLine(gui);
	value_gb.addChild(value, GUI_ALIGN_EXPAND);
	for (int i = 0; i <= 12; i++)
	{
		label.append(new WidgetLabel(gui, ""));
		label[label.size()-1].setFontRich(1);
		value_gb.addChild(label[label.size()-1], GUI_ALIGN_LEFT);
	}
	change = new WidgetButton(gui, "Change Value");
	value_gb.addChild(change, GUI_ALIGN_LEFT);
	reset = new WidgetButton(gui, "Reset Value");
	value_gb.addChild(reset, GUI_ALIGN_LEFT);

	reload = new WidgetButton(gui, "Reload Property Files");
	clone = new WidgetButton(gui, "Clone Property");
	inherit = new WidgetButton(gui, "Inherit Property");
	save_prop = new WidgetButton(gui, "Save Property");

	menu_gb.addChild(reload, GUI_ALIGN_EXPAND);
	menu_gb.addChild(clone, GUI_ALIGN_EXPAND);
	menu_gb.addChild(inherit, GUI_ALIGN_EXPAND);
	menu_gb.addChild(save_prop, GUI_ALIGN_EXPAND);

	info = new WidgetLabel(gui);
	info.setFontRich(1);
	info.setText("<font color=00ffff>Unique value</font><br><font color=ffffff>Inherited value</font><br><font color=ffff00>Overridden value</font><br>");
	menu_gb.addChild(info, GUI_ALIGN_LEFT);
	prop_info = new WidgetLabel(gui);
	menu_gb.addChild(prop_info, GUI_ALIGN_LEFT);

	// setting callbacks for UI elements
	properties.setCallback(GUI_CHANGED, "properties_changed");
	parameters.setCallback(GUI_CHANGED, "parameters_changed");

	change.setCallback(GUI_CLICKED, "change_clicked");
	reset.setCallback(GUI_CLICKED, "reset_clicked");
	reload.setCallback(GUI_CLICKED, "reload_clicked");

	clone.setCallback(GUI_CLICKED, "clone_clicked");
	inherit.setCallback(GUI_CLICKED, "inherit_clicked");
	save_prop.setCallback(GUI_CLICKED, "save_prop_clicked");

	refresh_properties();

	return 1;
}

// start of the main loop
int update() {
	// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.

	return 1;
}

int postUpdate() {
	// The engine calls this function before rendering each render frame: correct behavior after the state of the node has been updated.

	return 1;
}

int updatePhysics() {
	// Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations.
	// The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value.
	// WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress.

	return 1;
}
// end of the main loop

```

</details>


## Property Class

### Members

## Node getNode () const

Returns the current node to which the property is assigned.
### Return value

Current node to which the property is assigned.
## int getNumStructs () const

Returns the current number of structures of the property.
### Return value

Current number of structures of the property.
## getParameterPtr () const

Returns the current root [property parameter](../../../api/library/common/class.propertyparameter_usc.md).
You can't iterate through all parameters of the property in a single loop, a recursive function should be used instead:


```cpp
void recursive_func (PropertyParameter p)
{

	for (int i = 0; i < p.getNumChildren(); i++)
	{
		PropertyParameter child = p.getChild(i);

		// do something... e.g. print parameter names and values
		log.message("- %s: %s \n", child.getName(), child.getValueString());

		recursive_func(child);
	}
}

/* ... */

int init() {
	/* ... */

	// getting the root parameter of the property
	PropertyParameter root_parameter = property.getParameterPtr();

	// iterating through all parameters of the property
	recursive_func(root_parameter);

	return 1;
}

```


### Return value

Current root property parameter instance
## int getNumChildren () const

Returns the current number of children of the current property.
### Return value

Current number of child properties.
## int isHierarchyValid () const

Returns the current value indicating if there are no missing parents in the hierarchy of the property.
### Return value

Current there are no missing parents in the hierarchy of the property
## UGUID getFileGUID () const

Returns the current GUID of the property file.
### Return value

Current new [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the property file.
## const char * getFilePath () const

Returns the current [path](#name_path) to the property file.
### Return value

Current [path](#name_path) to the property file.
## UGUID getGUID () const

Returns the current GUID of the property.
### Return value

Current GUID of the property.
## void setName ( string name )

Sets a new new [name](../../../code/formats/property_format.md#property_name) for the property.
> **Notice:** This method is not available for [manual](#isManual_int) and [non-editable](#isEditable_int) properties.


### Arguments

- *string* **name** - The property [name](../../../code/formats/property_format.md#property_name). > **Notice:** If the property is [internal](#isInternal_int) and has a parent, the parent's name will be returned.

## const char * getName () const

Returns the current new [name](../../../code/formats/property_format.md#property_name) for the property.
> **Notice:** This method is not available for [manual](#isManual_int) and [non-editable](#isEditable_int) properties.


### Return value

Current property [name](../../../code/formats/property_format.md#property_name).
> **Notice:** If the property is [internal](#isInternal_int) and has a parent, the parent's name will be returned.

## int isEngine () const

Returns the current value indicating if the property is engine-related (i.e. required for engine operation).
Such properties are stored in the `core`, `editor` and `editor2` folders.

### Return value

Current the property is engine-related
## int isManual () const

Returns the current value indicating if the property is a [manual](../../../principles/properties/index.md#manual) one.
### Return value

Current the property is manual
## int isInternal () const

Returns the current value indicating if the property is an [internal](../../../principles/properties/index.md#internal) one.
### Return value

Current the property is internal
## int isEditable () const

Returns the current value indicating if the property can be [edited](../../../code/formats/property_format.md#property_editable).
### Return value

Current the property is editable
## int isHidden () const

Returns the current value indicating if the property is [hidden](../../../code/formats/property_format.md#property_hidden).
### Return value

Current the property is hidden
## int isBase () const

Returns the current value indicating if the property is a base property.
### Return value

Current the property is a base property
## int getID () const

Returns the current identifier of the property.
### Return value

Current property ID.
## Property getParent () const

Returns the current [parent](../../../code/formats/property_format.md#property_parent) property.
### Return value

Current parent property if it exists; if the property has no parent, NULL will be returned.
## const char * getTooltip () const

Returns the current tooltip for the property.
### Return value

Current tooltip for the property.
## int getNumInterfaces () const

Returns the current total number of interfaces.
> **Notice:** You can use interfaces only within the C# Component System. For more information, see the article [C# Interfaces and Abstract Classes.](../../../code/csharp/interfaces_and_abstract_classes.md).

### Return value

Current total number of interfaces.
## getEventDestroy () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventParameterChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventReparented () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventRenamed () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventMoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventReloaded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## static Property ( )

Constructor. Creates a new property instance.
## Property getChild ( int num )

Returns the child property of the current property.
### Arguments

- *int* **num** - The number of the target child property.

### Return value

Child property.
## void setEditable ( int editable )

Sets a value indicating if the property can be [edited](../../../code/formats/property_format.md#property_editable).
### Arguments

- *int* **editable** - 1 to make the property editable; 0 to make it read-only.

## int hasOverrides ( )

Returns a value indicating if the property has at least one overridden parameter.
### Return value

**1** if the property has at least one overridden parameter; otherwise, **0**.
## int isParent ( string name )


Returns a value indicating if the property with the given name is a [parent](../../../code/formats/property_format.md#property_parent) of this property.


Suppose we have the following two manual properties in our project:


- ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.7.3" name="my_prop" parent_name="surface_base" manual="1"> <parameter name="my_parameter">100</parameter> </property> ```
- ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.7.3" name="my_prop_0" parent_name="my_prop" manual="1"> <parameter name="my_parameter1">101</parameter> <parameter name="my_parameter2">101</parameter> </property> ```


The following code will return 1 as the *my_prop* property is the parent of the *my_prop_0* property:


```cpp
// get a property named my_prop_0
Property property = engine.properties.findManualProperty("my_prop_0");
// perform parent check
log.message("%d\n",property.isParent("my_prop"));

```


### Arguments

- *string* **name** - Parent property name.

### Return value

**1** if the property with the given name is a parent of this property; otherwise, **0**.
## int setParent ( Property property , int save_all_values = 0 )


Sets the given property as the parent for this property and saves the parameter values of the property (if the corresponding flag is set).


> **Notice:** The method is not available for [manual](#isManual_int) and [non-editable](#isEditable_int) properties.


### Arguments

- *[Property](../../../api/library/common/class.property_usc.md)* **property** - Property to be set as the parent for this property.
- *int* **save_all_values** - Flag indicating if parameter values of the property will be saved after reparenting.

### Return value

1 if the given property was successfully set as the parent for this property; otherwise, 0.
## Property clone ( )

Clones the property. The cloned property won't have a name, a path and won't be displayed in the properties hierarchy.
### Return value

Cloned property.
## Property clone ( string name , string path )

Clones the property and assigns the specified name and path to the clone. The cloned property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_usc.md#saveProperties_int)* call. This method may be used, for example, to create a property missed during project's migration.
### Arguments

- *string* **name** - Cloned property name.
- *string* **path** - Path to save the cloned property.

### Return value

Cloned property.
## Property clone ( string name , string path , UGUID guid )

Clones the property and assigns the specified name, GUID and path to the clone. The cloned property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_usc.md#saveProperties_int)* call. This method may be used, for example, to create a property missed during project's migration.
### Arguments

- *string* **name** - Cloned property name.
- *string* **path** - Path to save the cloned property.
- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Cloned property [GUID](../../../api/library/filesystem/class.uguid_usc.md).

### Return value

Cloned property.
## Property clone ( string name )

Clones the property.
```cpp
// get a property to be cloned
Property property = engine.properties.findProperty("surface_base_0");
// clone the property
property.clone("cloned_surface_base_0");

```


### Arguments

- *string* **name** - Cloned property name.

### Return value

Cloned property.
## Property inherit ( )

Inherits a new property from this one. The inherited property will be empty: it won't have a name, a path and won't be displayed in the properties hierarchy.
### Return value

Inherited property.
## Property inherit ( string name )

Inherits a new property from this one and assigns the specified name to it.
### Arguments

- *string* **name** - Inherited property name.

### Return value

Inherited property.
## Property inherit ( string name , string path )

Inherits a new property from this one and assigns the specified name and path to it. The inherited property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_usc.md#saveProperties_int)* call.
### Arguments

- *string* **name** - Inherited property name.
- *string* **path** - Path to save the inherited property.

### Return value

Inherited property.
## Property inherit ( string name , string path , UGUID guid )

Inherits a new property from this one and assigns the specified name, GUID and path to it. The inherited property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_usc.md#saveProperties_int)* call.
### Arguments

- *string* **name** - Inherited property name.
- *string* **path** - Path to save the inherited property.
- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Inherited property [GUID](../../../api/library/filesystem/class.uguid_usc.md).

### Return value

Inherited property.
## int load ( )


Loads the property from the file specified by the *[setFilePath()](#setFilePath_cstr_int)* function.


> **Notice:** This function can be used to load properties created during application execution or stored outside the `data` directory.


### Return value

**1** if the property data is loaded successfully; otherwise, **0**.
## int load ( string path )

Loads the property from the specified [`*.prop` file](../../../code/formats/property_format.md).
### Arguments

- *string* **path** - Path to the `*.prop` file to load the property data from.

### Return value

**1** if the property data is loaded successfully; otherwise, **0**.
## int loadXml ( Xml xml )

Loads data of the property (all its parameters) from the given instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../api/library/common/class.xml_usc.md) instance in which the property data is stored.

### Return value

**1** if the property data is loaded successfully; otherwise, **0**.
## int loadWorld ( Xml xml )

Loads data of the current property (all its options, states and parameters) from the given instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../api/library/common/class.xml_usc.md) instance in which the property data is stored.

### Return value

**1** if the property data is loaded successfully; otherwise, **0**.
## int reload ( )

Reloads the property and all its children.
### Return value

**1** if the property is reloaded successfully; otherwise, **0**.
## int canSaveInFile ( )

Returns a value indicating if the property can be saved to a file. For example, this function will return 0 for an [internal](#isInternal_int) or [manual](#isManual_int) property.
### Return value

**1** if the property can be saved to a file; otherwise, **0**.
## int saveState ( Stream stream )


Saves data of the current property (all its parameters) into a binary stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int_int)* methods:


```cpp
// somewhere in code

// getting a manual property named "my_prop" via the Property Manager
Property property = engine.properties.findManualProperty("my_prop");
property.setParameterInt(property.findParameter("my_int_param"), 3);

// save state
Blob blob_state = new Blob();
property.saveState(blob_state);

// change state
property.setParameterInt(property.findParameter("my_int_param"), 4);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
property.restoreState(blob_state, 0);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream into which the property data will be saved.

### Return value

**1** if the property data is saved successfully; otherwise, **0**.
## int restoreState ( Stream stream , int restore_mode = 0 )


Restores the data of the property (all its parameters) from a binary stream in the specified mode.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```cpp
// somewhere in code

// getting a manual property named "my_prop" via the Property Manager
Property property = engine.properties.findManualProperty("my_prop");
property.setParameterInt(property.findParameter("my_int_param"), 3);

// save state
Blob blob_state = new Blob();
property.saveState(blob_state);

// change state
property.setParameterInt(property.findParameter("my_int_param"), 4);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
property.restoreState(blob_state, 0);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream in which the saved property parameter data is stored.
- *int* **restore_mode** - Restore mode. One of the [PROPERTY_RESTORE_MODE_*](#RESTORE_MODE_MERGE) values. The default value is [PROPERTY_RESTORE_MODE_REPLACE](#RESTORE_MODE_REPLACE).

### Return value

**1** on success; otherwise, **0**.
## int save ( )


Saves the property data to the file specified by the *[setFilePath()](#setFilePath_cstr_int)* function.


> **Notice:** This method is not available for [manual](#isManual_int) and [internal](#isInternal_int) properties.


### Return value

**1** if the property data is saved successfully; otherwise, **0**.
## int save ( string path )


Saves the property data to the specified [`*.prop` file](../../../code/formats/property_format.md).


> **Notice:** This method is not available for [manual](#isManual_int) properties.


### Arguments

- *string* **path** - Path to the `*.prop` file to save the property data to.

### Return value

**1** if the property data is saved successfully; otherwise, **0**.
## int saveXml ( Xml xml )


Saves data of the property (all its parameters) to the given instance of the Xml class.


> **Notice:** This method is not available for [manual](#isManual_int) properties.


### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../api/library/common/class.xml_usc.md) instance into which the property data will be saved.

### Return value

**1** if the property data is saved successfully; otherwise, **0**.
## int saveWorld ( Xml xml , int force = 0 )

Saves data of the current property (all its parameters) into the given instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../api/library/common/class.xml_usc.md) instance into which the property data will be saved.
- *int* **force** - A value indicating if forced saving of property data is used: 1 to enable forced saving, 0 to disable it.

### Return value

**1** if the property data is saved successfully; otherwise, **0**.
## int parameterTypeByName ( string param_type )

Returns parameter type identifier by the type name specified.
### Arguments

- *string* **param_type** - Parameter type name.

### Return value

Parameter type identifier, one of the [PROPERTY_PARAMETER_*](#PARAMETER_COLOR) variables.
## string parameterNameByType ( int param_type )

Returns parameter type name by the type identifier specified.
### Arguments

- *int* **param_type** - Parameter type identifier, one of the [PROPERTY_PARAMETER_*](#PARAMETER_COLOR) variables.

### Return value

Parameter type name.
## getParameterPtr ( int id )

Returns a [property parameter](../../../api/library/common/class.propertyparameter_usc.md) by its ID.
### Arguments

- *int* **id** - Property parameter ID.

### Return value

Property parameter instance.


> **Notice:** This method never returns NULL, regardless of whether a parameter with the specified ID exists or not. It only displays an error message in the console in case of a non-existing parameter. To check if such parameter really exists, use the [*PropertyParameter.isExist()*](../../../api/library/common/class.propertyparameter_usc.md#isExist_int) method. For example:
>
>
> ```cpp
> // getting some property named "my_property"
> Property pProperty = engine.properties.findManualProperty("my_property");
>
> // trying to get a property parameter having the ID=30
> PropertyParameter param = pProperty.getParameterPtr(30);
>
> // checking if such parameter exists and displaying a message
> if (param.isExist() == 1)
> 	log.message("Property parameter with the specified ID exists!\n");
> else
> 	log.message("No such parameter!\n");
> 	return 1;
>
> ```


## int findStruct ( string name )

Returns the number of the structure with the specified name.
### Arguments

- *string* **name** - Name of the structure to be found.

### Return value

Number of the structure with the specified name, if it exists; otherwise, -1.
## string getStructName ( int num )

Returns the name of the structure with the specified number.
### Arguments

- *int* **num** - Structure number.

### Return value

## string getInterfaceName ( int num )


Returns the name of the interface with the specified number.


> **Notice:** You can use interfaces only within the C# Component System. For more information, see the article [C# Interfaces and Abstract Classes.](../../../code/csharp/interfaces_and_abstract_classes.md).

### Arguments

- *int* **num** - Interface number.

### Return value

## int setFileGUID ( UGUID fileguid )

Changes the GUID of the file this property is stored in, re-binding the property to another property file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **fileguid** - New file GUID.

### Return value

true if the file GUID is changed successfully or already matches the current one; otherwise, false (another property is already registered with that file GUID).
## int setFilePath ( string path )

Sets the path of the file the property is stored in: the path is registered as a virtual file in the engine file system and the resulting GUID is assigned to the property.
### Arguments

- *string* **path** - Target file path.

### Return value

true on success; otherwise, false (a different property already occupies the resulting file GUID).
