# Unigine::Property Class (CS)


This class provides an interface for property manipulation: it is used to modify [properties](../../../principles/world_structure/index.md#properties) that allow you to control values of the logic-related parameters. When a property is assigned to a node, an instanced [internal property](../../../principles/properties/index.md#internal) is created and saved into a `.world` or `.node` file. However, rather than the whole list of parameters it contains only the modified ones.


The concepts of a [path](#setFilePath_cstr_int) and a [name](#setName_cstr_void) of the property should be distinguished:


- The **path** specifies where the property is stored on the disk. The path includes a property file name.
- The **name** specifies how the property will be displayed in the UnigineEditor (the Property Hierarchy window, the nodes surface section of the Parameters window). The name can also be used to refer to a property from the [code](../../../api/library/engine/class.properties_cs.md#findProperty_cstr_Property).


By default, the property name and the `*.prop` file name coincide.


By using functions of this class, you can, for example, implement a *properties editor*.


**Properties** specify the way the object will behave and interact with other objects and the scene environment.


A property is a "material" for application logic represented by a set of logic-related **[parameters](../../../code/formats/property_format.md#element_parameter)**. Properties can be used to build [**components**](../../../principles/component_system/index.md) to extend the functionality of nodes.


All properties in the project are organized into a [hierarchy](../../../principles/properties/inheritance.md). To be modified, properties should be obtained from the hierarchy via [*API*](../../../api/library/engine/class.properties_cs.md) functions.


Property parameters are managed individually via the *[PropertyParameter](../../../api/library/common/class.propertyparameter_cs.md)* class, to get any parameter by its name or ID you should use the **[GetParameterPtr()](../../...md#getParameterPtr_cstr_PropertyParameter)** method.


```csharp
PropertyParameter pPropertyParameter = pProperty.ParameterPtr; // get "root" parameter
Node pTargetNode = pPropertyParameter.GetChild(k).ValueNode; // get child with index "k", then its value

// ...

float positionFactor = pPropertyParameter.GetChild(k).ValueFloat;
// etc.

// If you know names, you can use:
pTargetNode = pProperty.GetParameterPtr("target").ValueNode;
positionFactor = pProperty.GetParameterPtr("position_factor").ValueFloat;


```


Automatic type conversion of property parameters make them act like some universal variables i.e. you can set a new value for an integer parameter int_param and type it like this:


```csharp
PropertyParameter int_param = pProperty.GetParameterPtr("my_int_param");

/* ... */

// setting a new value of integer parameter using a string
int_param.SetValue("15");

// setting a new value of integer parameter using a float
int_param.SetValue(5.0f);

// getting integer parameter's value as a string
Log.Message("Integer parameter value : %s", int_param.GetValue().String);


```


> **Notice:** You can modify only existing parameters of the property. To add or remove new parameters, you should manually edit the `.prop` file or use API to edit the XML file via the code.


### Adding and Removing Properties


> **Notice:** The *Property* class doesn't allow adding a new property to the property hierarchy.


A new property can be added to the hierarchy in one of the following ways:


- By creating and editing the corresponding `.prop` file manually. For example, in the `data` folder let us create the following file describing a property for a GameObjectsUnit: ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.16.0.2" manual="1" editable="0" name="GameObjectsUnit"> <parameter name="weapon_type" type="switch" items="air,land,all_types">0</parameter> <parameter name="attack" type="toggle">1</parameter> <parameter name="damage" type="int" max="1000">1</parameter> <parameter name="velocity" type="float" max="100">30</parameter> <parameter name="material" type="string"/> </property> ```
- By inheriting from the existing property via [*Properties.inheritProperty()*](../../../api/library/engine/class.properties_cs.md#inheritProperty_UGUID_cstr_cstr_Property) function or [*inherit()*](#inherit_cstr_Property) function of the Property class. For example: ```csharp // inherit a GameObjectsUnit_0 property from the GameObjectsUnit property Property inherited_prop = Properties.FindManualProperty("GameObjectsUnit").Inherit("GameObjectsUnit_0", "game_object_unit_0.prop"); // inherit a GameObjectsUnit_1 property from the GameObjectsUnit_0 property via the Manager Properties.InheritProperty(inherited_prop.GUID, "GameObjectsUnit_1", "game_object_unit_1.prop"); ``` To save all properties in the hierarchy that can be saved (i.e., editable, having a path specified, and not internal or manual ones) via the [*Properties.saveProperties()*](../../../api/library/engine/class.properties_cs.md#saveProperties_int) function. > **Notice:** By default, all parameters and states of the inherited property are the same as specified in the parent property. A child property can [override some parameters of its parent or add new ones](../../../principles/world_structure/index.md#properties_hierarchy).
- By editing the corresponding `.prop` file [via API](../../../api/library/common/class.xml_cs.md): you can open an XML file, write data into it and save it.


To delete a property, you can simply call the *[removeProperty()](../../../api/library/engine/class.properties_cs.md#removeProperty_UGUID_int_int_int)* function:


```csharp
// remove the property with the given name with all its children and delete the *.prop file
Properties.RemoveProperty(Properties.FindProperty("GameObjectsUnit_0").GUID, true, true);


```


### Handling Events


You can subscribe for events to track any changes made to the property and its parameters and perform certain actions. The signature of the handler function can be one of the following:


```csharp
// for the ParameterChanged event
void handler_function_name(Property property, int parameter_num){}

// for all other types
void handler_function_name(Property property){}


```


The example below shows how to subscribe for events to track changes of property parameters and report the name of the property and the changed parameter (suppose we have a manual property named *my_prop* with an integer parameter named *my_int_param*).


```csharp
void parameter_changed(Property property, int num)
{
	Log.Message("Parameter \"%s\" of the property \"%s\" has changed its value.\n", property.GetParameterPtr(num).Name, property.Name);
	// ...
}

	// somewhere in the code

	// getting a manual property named "my_prop" via the Property Manager
	Property property = Properties.FindManualProperty("my_prop.prop");

	// subscribing to the ParameterChange event and setting our handler
	property.EventParameterChanged.Connect(parameter_changed);

	// changing the value of the "my_int_param" parameter
	property.GetParameterPtr("my_int_param").ValueInt = 3;


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


Below is the source code in C# implementing our Property Viewer as a *PropertyViewer* component. You can copy and paste it to the corresponding file of your project.


<details>
<summary>PropertyViewer.cs | Close</summary>

**AppSystemLogic.cs**


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class PropertyViewer : Component
{
 	WidgetWindow window;
    WidgetHBox hbox;

    WidgetGroupBox properties_gb;
    WidgetTreeBox properties;
    WidgetGroupBox parameters_gb;
    WidgetTreeBox parameters;
    WidgetGroupBox value_gb;
    WidgetGroupBox menu_gb;

    WidgetVBox vbox2, vbox3;
    WidgetButton reload;
    WidgetButton clone;
    WidgetButton inherit;
    WidgetButton save_prop;

    // values
    List <WidgetLabel> label;
    WidgetEditLine value;
    WidgetButton change;
    WidgetButton reset;

    WidgetLabel info;
    WidgetLabel prop_info;

    Dictionary<int, Property> item_prop;
    Dictionary<int, PropertyParameter> item_param;

	/// method refreshing properties
	void refresh_properties()
	{
		properties.EventChanged.Enabled = false;
		properties.Clear();
		item_prop.Clear();

		// recursive function iterating through all children properties and building property hierarchy
		Action<int, Property> attach_children = null;
		attach_children = new Action<int, Property>((int parent, Property prop_parent) =>
		{
			for (int k = 0; k < prop_parent.NumChildren; k++)
			{
				Property prop = prop_parent.GetChild(k);

				if ((prop.Parent != null) && (prop != prop_parent) && (prop.Parent.GUID.ToString() == prop_parent.GUID.ToString()))
				{
					int child = properties.AddItem(prop.Name);
					properties.AddItemChild(parent, child);
					item_prop.Add(child, prop);
					attach_children(child, prop);
				}
			}
		});
		// building property hierarchy
		for (int i = 0; i < Properties.NumProperties; i++)
		{
			Property prop_base = Properties.GetProperty(i);
			if (prop_base.IsBase)
			{
				int parent = properties.AddItem(prop_base.Name);
				item_prop.Add(parent, prop_base);
				attach_children(parent, prop_base);
			}
		}
		properties.EventChanged.Enabled = true;
	}

	/// method refreshing property parameters
	void properties_changed()
	{
		parameters.EventChanged.Enabled = false;
		// clearing the list of property parameters and updating values displayed
		parameters.Clear();
		value_gb.Enabled = false;
		for (int i = 0; i <= 12; i++)
			label[i].Text = "";
			item_param.Clear();

		int item = properties.CurrentItem;
		if (item == -1)
		{
			parameters.EventChanged.Enabled = true;
			return;
		}
		// getting a property from the list in accordance with current selection
		Property prop = item_prop[item];

		// getting a root parameter of the selected property
		PropertyParameter pp = prop.ParameterPtr;

		// recursive function iterating through all parameters of a property
		Action<int, PropertyParameter> add_parameters = null;
		add_parameters = new Action<int, PropertyParameter>((parent, p) =>
		{
			for (int i = 0; i < p.NumChildren; i++)
			{
				PropertyParameter child = p.GetChild(i);
				int child_index = parameters.AddItem(child.Name);
				parameters.SetItemColor(child_index,
					new vec4(
					MathLib.ToFloat(child.IsInherited),
					1,
					MathLib.ToFloat(!child.IsOverridden),
					(child.IsHidden) ? 0.5f : 1.0f));
				item_param.Add(child_index, child);

				if (parent != -1)
					parameters.AddItemChild(parent, child_index);

				add_parameters(child_index, child);
			}
		});

		// building the hierarchy of parameters for the selected property
		add_parameters(-1, pp);

		// preparing property information
		String pi = String.Format("\nName: {0}\nPath: {1}\nInternal: {2}\nStructs: {3}\n", prop.Name, prop.FilePath, prop.IsInternal, prop.NumStructs);
		// adding all structures defined in the property (if any)
		for (int i = 0; i < prop.NumStructs; i++)
			pi += String.Format("{0}) {1}\n", i, prop.GetStructName(i));
		// displaying property information
		prop_info.Text = pi;

		parameters.EventChanged.Enabled = true;
		parameters.CurrentItem =-1;
	}

	/// method refreshing information about the currently selected property parameter
	void parameters_changed()
	{
		// checking if any property parameter is selected
		int item = parameters.CurrentItem;
		if (item == -1)
			return;

		value_gb.Enabled = true;
		// getting the parameter from the list in accordance with current selection
		PropertyParameter p = item_param[item];
		int i = 0;
		label[i++].Text = String.Format("<font color=ffff00>ID:</font> {0}", p.ID);
		label[i++].Text = String.Format("<font color=ffff00>Name:</font> {0}", p.Name);
		label[i++].Text = String.Format("<font color=ffff00>Title:</font> {0}", p.Title);
		label[i++].Text = String.Format("<font color=ffff00>Tooltip:</font> {0}", p.Tooltip);
		label[i++].Text = String.Format("<font color=ffff00>Group:</font> {0}", p.Group);
		label[i++].Text = String.Format("<font color=ffff00>Filter:</font> {0}", p.Filter);

		String s;
		// displaying parameter's type
		if (p.Type == Property.PARAMETER_ARRAY)
			s = String.Format("<font color=ffff00>Type:</font> array [<font color=ffff00>Size:</font> {0}, <font color=ffff00>Type:</font> {1}]", p.ArraySize, p.ArrayTypeName);
		else if (p.Type == Property.PARAMETER_STRUCT)
			s = String.Format("<font color=ffff00>Type:</font> struct [<font color=ffff00>Struct Name:</font> {0}]", p.StructName);
		else
			s = String.Format("<font color=ffff00>Type:</font> {0}", p.Property.ParameterNameByType(p.Type));
		label[i++].Text = s;
		label[i++].Text = String.Format("<font color=ffff00>Hidden:</font> {0}", p.IsHidden);
		label[i++].Text = String.Format("<font color=ffff00>Inherited:</font> {0}", p.IsInherited);
		label[i++].Text = String.Format("<font color=ffff00>Overridden:</font> {0}", p.IsOverridden);
		label[i++].Text = String.Format("<font color=ffff00>Has Min:</font> {0}", p.HasSliderMinValue());
		label[i++].Text = String.Format("<font color=ffff00>Has Max:</font> {0}", p.HasSliderMaxValue());
		s = "";
		if (p.Type == Property.PARAMETER_INT)
			s = String.Format("<font color=ffff00>Min:</font> {0} <font color=ffff00>Max:</font> {1}", p.IntMinValue, p.IntMaxValue);
		else if (p.Type == Property.PARAMETER_FLOAT)
			s = String.Format("<font color=ffff00>Min:</font> {0} <font color=ffff00>Max:</font> {1}", p.FloatMinValue, p.FloatMaxValue);
		else if (p.Type == Property.PARAMETER_DOUBLE)
			s = String.Format("<font color=ffff00>Min:</font> {0} <font color=ffff00>Max:</font> {1}", p.DoubleMinValue, p.DoubleMaxValue);
		else if (p.Type == Property.PARAMETER_SWITCH)
			s = String.Format("<font color=ffff00>Switch Num Items:</font> {0}", p.SwitchNumItems);
		label[i++].Text = s;
		value.Text = p.ValueString;
		reset.Enabled = p.IsOverridden;
	}

	/// change button on_click event handler
	void change_clicked()
	{
		// checking if any property parameter is currently selected
		int item = parameters.CurrentItem;
		if (item == -1)
			return;
		// setting the value of the currently selected property parameter and refreshing information
		PropertyParameter pp = item_param[item];
		pp.SetValue(value.Text);

		refresh_info();
	}

	/// reset button on_click event handler
	void reset_clicked()
	{
		// checking if any property parameter is currently selected
		int item = parameters.CurrentItem;
		if (item == -1)
			return;

		// resetting the value of the currently selected property parameter and refreshing information
		PropertyParameter pp = item_param[item];
		pp.ResetValue();

		refresh_info();
	}

	/// reload button on_click event handler
	void reload_clicked()
	{
		// reload all properties and refreshing information
		Properties.ReloadProperties();
		refresh_info();
	}

	/// method refreshing property and parameter information
	void refresh_info()
	{
		// getting current indices of property and parameter selection
		int item_pr = properties.CurrentItem;
		int item_pa = parameters.CurrentItem;
		refresh_properties();

		// setting current items and updating information displayed
		properties.CurrentItem = MathLib.Clamp(item_pr, -1, properties.NumItems - 1);
		properties_changed();
		parameters.CurrentItem =MathLib.Clamp(item_pa, -1, parameters.NumItems - 1);
		parameters_changed();
	}

	/// clone button on_click event handler
	void clone_clicked()
	{
		// checking if any property is selected in the hierarchy
		int item = properties.CurrentItem;
		if (item == -1)
			return;
		// cloning the selected property
		Property p = item_prop[item];
		Property p_clone = p.Clone();
		p_clone.Name =String.Format("{0}_cloned", p.Name);

		// refreshing information displayed
		refresh_info();
	}

	/// inherit button on_click event handler
	void inherit_clicked()
	{
		// checking if any property is selected in the hierarchy
		int item = properties.CurrentItem;
		if (item == -1)
			return;
		// inheriting a new property from the selected one
		Property p = item_prop[item];
		p.Inherit().Name = String.Format("{0}_inherited", p.Name);

		// refreshing information displayed
		refresh_info();
	}

	/// method saving the currently selected property to the "my_test_prop.prop" file
	void save_prop_clicked()
	{
		// checking if any property is selected in the hierarchy
		int item = properties.CurrentItem;
		if (item == -1)
			return;
		// saving a property to the specified file
		Property p = item_prop[item];
		p.Save("my_test_prop.prop");
	}

	private void Init()
	{
		// write here code to be called on component initialization
		Engine.BackgroundUpdate = Engine.BACKGROUND_UPDATE.BACKGROUND_UPDATE_RENDER_NON_MINIMIZED;

            label = new List<WidgetLabel>();
            item_prop = new Dictionary<int, Property>();
            item_param = new Dictionary<int, PropertyParameter>();
	        // creating user interface
	        Gui gui = Gui.GetCurrent();
	        window = new WidgetWindow(gui, "Properties Viewer");
	        window.Sizeable = true;
	        window.Width = WindowManager.MainWindow.Size.x;
	        window.Height = WindowManager.MainWindow.Size.y;
	        gui.AddChild(window, Gui.ALIGN_OVERLAP);

	        vbox2 = new WidgetVBox(gui);
	        window.AddChild(vbox2, Gui.ALIGN_EXPAND);

	        hbox = new WidgetHBox(gui);
	        vbox2.AddChild(hbox, Gui.ALIGN_EXPAND);

	        properties_gb = new WidgetGroupBox(gui, "Properties");
	        parameters_gb = new WidgetGroupBox(gui, "Parameters");
	        hbox.AddChild(properties_gb, Gui.ALIGN_EXPAND);
	        hbox.AddChild(parameters_gb, Gui.ALIGN_EXPAND);

	        properties = new WidgetTreeBox(gui);
	        parameters = new WidgetTreeBox(gui);
	        properties_gb.AddChild(properties, Gui.ALIGN_EXPAND);
	        parameters_gb.AddChild(parameters, Gui.ALIGN_EXPAND);

	        vbox3 = new WidgetVBox(gui);
	        hbox.AddChild(vbox3, Gui.ALIGN_EXPAND);
	        value_gb = new WidgetGroupBox(gui, "Value");
	        value_gb.Width = 300;
	        value_gb.Height = 300;
	        value_gb.Arrange();
	        menu_gb = new WidgetGroupBox(gui, "Menu");
	        vbox3.AddChild(value_gb, Gui.ALIGN_LEFT);
	        vbox3.AddChild(menu_gb, Gui.ALIGN_EXPAND);

	        label.Add(new WidgetLabel(gui, ""));
	        label[label.Count-1].FontRich = 1;
	        value_gb.AddChild(label[label.Count-1], Gui.ALIGN_LEFT);
	        value = new WidgetEditLine(gui);
	        value_gb.AddChild(value, Gui.ALIGN_EXPAND);
	        for (int i = 0; i < 12; i++)
	        {
		        label.Add(new WidgetLabel(gui, ""));
		        label[label.Count-1].FontRich = 1;
		        value_gb.AddChild(label[label.Count-1], Gui.ALIGN_LEFT);
	        }
	        change = new WidgetButton(gui, "Change Value");
	        value_gb.AddChild(change, Gui.ALIGN_LEFT);
	        reset = new WidgetButton(gui, "Reset Value");
	        value_gb.AddChild(reset, Gui.ALIGN_LEFT);

	        reload = new WidgetButton(gui, "Reload Property Files");
	        clone = new WidgetButton(gui, "Clone Property");
	        inherit = new WidgetButton(gui, "Inherit Property");
	        save_prop = new WidgetButton(gui, "Save Property");

	        menu_gb.AddChild(reload, Gui.ALIGN_EXPAND);
	        menu_gb.AddChild(clone, Gui.ALIGN_EXPAND);
	        menu_gb.AddChild(inherit, Gui.ALIGN_EXPAND);
	        menu_gb.AddChild(save_prop, Gui.ALIGN_EXPAND);

	        info = new WidgetLabel(gui);
	        info.FontRich = 1;
	        info.Text = "<font color=00ffff>Unique value</font><br><font color=ffffff>Inherited value</font><br><font color=ffff00>Overridden value</font><br>";
	        menu_gb.AddChild(info, Gui.ALIGN_LEFT);
	        prop_info = new WidgetLabel(gui);
	        menu_gb.AddChild(prop_info, Gui.ALIGN_LEFT);

	        // subscriptions to events for UI elements
	        properties.EventChanged.Connect(properties_changed);
	        parameters.EventChanged.Connect(parameters_changed);

	        change.EventClicked.Connect(change_clicked);
	        reset.EventClicked.Connect(reset_clicked);
	        reload.EventClicked.Connect(reload_clicked);
	        clone.EventClicked.Connect(clone_clicked);
	        inherit.EventClicked.Connect(inherit_clicked);
	        save_prop.EventClicked.Connect(save_prop_clicked);

	        refresh_properties();
	}

	private void Update()
	{
		// write here code to be called before updating each render frame

	}
}

```

</details>


## Property Class

### Properties

## 🔒︎ Node Node

The node to which the property is assigned.
## 🔒︎ int NumStructs

The number of structures of the property.
## 🔒︎ PropertyParameter ParameterPtr

The root [property parameter](../../../api/library/common/class.propertyparameter_cs.md).
You can't iterate through all parameters of the property in a single loop, a recursive function should be used instead:


```csharp
public void recursive_func (PropertyParameter p)
{

	for (int i = 0; i < p.getNumChildren(); i++)
	{
		PropertyParameter child = p.getChild(i);

		// do something... e.g. print parameter names and values
		Log.Message("- {0}: {1} \n", child.getName(), child.getValueString());

		recursive_func(child);
	}
}
/* ... */

public override bool Init()
{
	/* ... */

	// getting the root parameter of the property
	PropertyParameter root_parameter = property.getParameterPtr();

	// iterating through all parameters of the property
	recursive_func(root_parameter);

	return 1;
}

```


## 🔒︎ int NumChildren

The number of children of the current property.
## 🔒︎ bool IsHierarchyValid

The value indicating if there are no missing parents in the hierarchy of the property.
## 🔒︎ UGUID FileGUID

The GUID of the property file.
## 🔒︎ string FilePath

The [path](#name_path) to the property file.
## 🔒︎ UGUID GUID

The GUID of the property.
## string Name

The new [name](../../../code/formats/property_format.md#property_name) for the property.
> **Notice:** This method is not available for [manual](#isManual_int) and [non-editable](#isEditable_int) properties.


## 🔒︎ bool IsEngine

The value indicating if the property is engine-related (i.e. required for engine operation).
Such properties are stored in the `core`, `editor` and `editor2` folders.

## 🔒︎ bool IsManual

The value indicating if the property is a [manual](../../../principles/properties/index.md#manual) one.
## 🔒︎ bool IsInternal

The value indicating if the property is an [internal](../../../principles/properties/index.md#internal) one.
## 🔒︎ bool IsEditable

The value indicating if the property can be [edited](../../../code/formats/property_format.md#property_editable).
## 🔒︎ bool IsHidden

The value indicating if the property is [hidden](../../../code/formats/property_format.md#property_hidden).
## 🔒︎ bool IsBase

The value indicating if the property is a base property.
## 🔒︎ int ID

The identifier of the property.
## 🔒︎ Property Parent

The [parent](../../../code/formats/property_format.md#property_parent) property.
## 🔒︎ string Tooltip

The tooltip for the property.
## 🔒︎ int NumInterfaces

The total number of interfaces.
> **Notice:** You can use interfaces only within the C# Component System. For more information, see the article [C# Interfaces and Abstract Classes.](../../../code/csharp/interfaces_and_abstract_classes.md).

## 🔒︎ Event< Property > EventDestroy

The event triggered when the property is destroyed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Destroy event handler
void destroy_event_handler(Property property)
{
	Log.Message("\Handling Destroy event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections destroy_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventDestroy.Connect(destroy_event_connections, destroy_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventDestroy.Connect(destroy_event_connections, (Property property) => {
		Log.Message("Handling Destroy event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
destroy_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Destroy event with a handler function
publisher.EventDestroy.Connect(destroy_event_handler);

// remove subscription to the Destroy event later by the handler function
publisher.EventDestroy.Disconnect(destroy_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection destroy_event_connection;

// subscribe to the Destroy event with a lambda handler function and keeping the connection
destroy_event_connection = publisher.EventDestroy.Connect((Property property) => {
		Log.Message("Handling Destroy event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
destroy_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
destroy_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
destroy_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Destroy events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventDestroy.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventDestroy.Enabled = true;

```

</details>

## 🔒︎ Event< Property , int> EventParameterChanged

The event triggered when the value of any parameter of the property is changed or reset to default. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**, int **param_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ParameterChanged event handler
void parameterchanged_event_handler(Property property,  int param_index)
{
	Log.Message("\Handling ParameterChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections parameterchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventParameterChanged.Connect(parameterchanged_event_connections, parameterchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventParameterChanged.Connect(parameterchanged_event_connections, (Property property,  int param_index) => {
		Log.Message("Handling ParameterChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
parameterchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ParameterChanged event with a handler function
publisher.EventParameterChanged.Connect(parameterchanged_event_handler);

// remove subscription to the ParameterChanged event later by the handler function
publisher.EventParameterChanged.Disconnect(parameterchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection parameterchanged_event_connection;

// subscribe to the ParameterChanged event with a lambda handler function and keeping the connection
parameterchanged_event_connection = publisher.EventParameterChanged.Connect((Property property,  int param_index) => {
		Log.Message("Handling ParameterChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
parameterchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
parameterchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
parameterchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ParameterChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventParameterChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventParameterChanged.Enabled = true;

```

</details>

## 🔒︎ Event< Property > EventReparented

The event triggered when the parent of the property is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Reparented event handler
void reparented_event_handler(Property property)
{
	Log.Message("\Handling Reparented event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections reparented_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventReparented.Connect(reparented_event_connections, reparented_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventReparented.Connect(reparented_event_connections, (Property property) => {
		Log.Message("Handling Reparented event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
reparented_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Reparented event with a handler function
publisher.EventReparented.Connect(reparented_event_handler);

// remove subscription to the Reparented event later by the handler function
publisher.EventReparented.Disconnect(reparented_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection reparented_event_connection;

// subscribe to the Reparented event with a lambda handler function and keeping the connection
reparented_event_connection = publisher.EventReparented.Connect((Property property) => {
		Log.Message("Handling Reparented event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
reparented_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
reparented_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
reparented_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Reparented events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventReparented.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventReparented.Enabled = true;

```

</details>

## 🔒︎ Event< Property > EventRenamed

The event triggered when the [name](#name_path) of the property is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Renamed event handler
void renamed_event_handler(Property property)
{
	Log.Message("\Handling Renamed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections renamed_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventRenamed.Connect(renamed_event_connections, renamed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventRenamed.Connect(renamed_event_connections, (Property property) => {
		Log.Message("Handling Renamed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
renamed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Renamed event with a handler function
publisher.EventRenamed.Connect(renamed_event_handler);

// remove subscription to the Renamed event later by the handler function
publisher.EventRenamed.Disconnect(renamed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection renamed_event_connection;

// subscribe to the Renamed event with a lambda handler function and keeping the connection
renamed_event_connection = publisher.EventRenamed.Connect((Property property) => {
		Log.Message("Handling Renamed event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
renamed_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
renamed_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
renamed_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Renamed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventRenamed.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventRenamed.Enabled = true;

```

</details>

## 🔒︎ Event< Property > EventMoved

The event triggered when the [path](#name_path) of the property is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Moved event handler
void moved_event_handler(Property property)
{
	Log.Message("\Handling Moved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections moved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventMoved.Connect(moved_event_connections, moved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventMoved.Connect(moved_event_connections, (Property property) => {
		Log.Message("Handling Moved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
moved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Moved event with a handler function
publisher.EventMoved.Connect(moved_event_handler);

// remove subscription to the Moved event later by the handler function
publisher.EventMoved.Disconnect(moved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection moved_event_connection;

// subscribe to the Moved event with a lambda handler function and keeping the connection
moved_event_connection = publisher.EventMoved.Connect((Property property) => {
		Log.Message("Handling Moved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
moved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
moved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
moved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Moved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventMoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventMoved.Enabled = true;

```

</details>

## 🔒︎ Event< Property > EventReloaded

The event triggered when the property is reloaded. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Reloaded event handler
void reloaded_event_handler(Property property)
{
	Log.Message("\Handling Reloaded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections reloaded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventReloaded.Connect(reloaded_event_connections, reloaded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventReloaded.Connect(reloaded_event_connections, (Property property) => {
		Log.Message("Handling Reloaded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
reloaded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Reloaded event with a handler function
publisher.EventReloaded.Connect(reloaded_event_handler);

// remove subscription to the Reloaded event later by the handler function
publisher.EventReloaded.Disconnect(reloaded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection reloaded_event_connection;

// subscribe to the Reloaded event with a lambda handler function and keeping the connection
reloaded_event_connection = publisher.EventReloaded.Connect((Property property) => {
		Log.Message("Handling Reloaded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
reloaded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
reloaded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
reloaded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Reloaded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventReloaded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventReloaded.Enabled = true;

```

</details>

### Members

---

## Property ( )

Constructor. Creates a new property instance.
## Property GetChild ( int num )

Returns the child property of the current property.
### Arguments

- *int* **num** - The number of the target child property.

### Return value

Child property.
## void SetEditable ( int editable )

Sets a value indicating if the property can be [edited](../../../code/formats/property_format.md#property_editable).
### Arguments

- *int* **editable** - 1 to make the property editable; 0 to make it read-only.

## bool HasOverrides ( )

Returns a value indicating if the property has at least one overridden parameter.
### Return value

true if the property has at least one overridden parameter; otherwise, false.
## bool IsParent ( string name )


Returns a value indicating if the property with the given name is a [parent](../../../code/formats/property_format.md#property_parent) of this property.


Suppose we have the following two manual properties in our project:


- ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.7.3" name="my_prop" parent_name="surface_base" manual="1"> <parameter name="my_parameter">100</parameter> </property> ```
- ```xml <?xml version="1.0" encoding="utf-8"?> <property version="2.7.3" name="my_prop_0" parent_name="my_prop" manual="1"> <parameter name="my_parameter1">101</parameter> <parameter name="my_parameter2">101</parameter> </property> ```


The following code will return 1 as the *my_prop* property is the parent of the *my_prop_0* property:


```csharp
// get a property named my_prop_0
Property property = Properties.findManualProperty("my_prop_0");
// perform parent check
Log.Message("{0}\n",property.isParent("my_prop"));

```


### Arguments

- *string* **name** - Parent property name.

### Return value

true if the property with the given name is a parent of this property; otherwise, false.
## bool IsParent ( UGUID guid )

Returns a value indicating if the property with the given GUID is a [parent](../../../code/formats/property_format.md#property_parent) of this property.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Parent property GUID.

### Return value

true if the property with the given GUID is a parent of this property; otherwise, false.
## int SetParent ( Property property , bool save_all_values = 0 )


Sets the given property as the parent for this property and saves the parameter values of the property (if the corresponding flag is set).


> **Notice:** The method is not available for [manual](#isManual_int) and [non-editable](#isEditable_int) properties.


### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property to be set as the parent for this property.
- *bool* **save_all_values** - Flag indicating if parameter values of the property will be saved after reparenting.

### Return value

1 if the given property was successfully set as the parent for this property; otherwise, 0.
## Property Clone ( )

Clones the property. The cloned property won't have a name, a path and won't be displayed in the properties hierarchy.
### Return value

Cloned property.
## Property Clone ( string name , string path )

Clones the property and assigns the specified name and path to the clone. The cloned property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_cs.md#saveProperties_int)* call. This method may be used, for example, to create a property missed during project's migration.
### Arguments

- *string* **name** - Cloned property name.
- *string* **path** - Path to save the cloned property.

### Return value

Cloned property.
## Property Clone ( string name , string path , UGUID guid )

Clones the property and assigns the specified name, GUID and path to the clone. The cloned property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_cs.md#saveProperties_int)* call. This method may be used, for example, to create a property missed during project's migration.
### Arguments

- *string* **name** - Cloned property name.
- *string* **path** - Path to save the cloned property.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Cloned property [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Cloned property.
## Property Clone ( string name )

Clones the property.
```cpp
Property property = Properties.findProperty("surface_base_0");
// clone the property
Property cloned = property.clone("cloned_surface_base_0");
// perform something on the cloned pointer
// ...
// delete the pointer
cloned.grab();
cloned.destroyPtr();

```


### Arguments

- *string* **name** - Cloned property name.

### Return value

Cloned property.
## Property Inherit ( )

Inherits a new property from this one. The inherited property will be empty: it won't have a name, a path and won't be displayed in the properties hierarchy.
### Return value

Inherited property.
## Property Inherit ( string name )

Inherits a new property from this one and assigns the specified name to it.
### Arguments

- *string* **name** - Inherited property name.

### Return value

Inherited property smart pointer.
## Property Inherit ( string name , string path )

Inherits a new property from this one and assigns the specified name and path to it. The inherited property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_cs.md#saveProperties_int)* call.
### Arguments

- *string* **name** - Inherited property name.
- *string* **path** - Path to save the inherited property.

### Return value

Inherited property.
## Property Inherit ( string name , string path , UGUID guid )

Inherits a new property from this one and assigns the specified name, GUID and path to it. The inherited property will be saved to the specified path on *[saveProperties()](../../../api/library/engine/class.properties_cs.md#saveProperties_int)* call.
### Arguments

- *string* **name** - Inherited property name.
- *string* **path** - Path to save the inherited property.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Inherited property [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Inherited property.
## bool Load ( )


Loads the property from the file specified by the *[setFilePath()](#setFilePath_cstr_int)* function.


> **Notice:** This function can be used to load properties created during application execution or stored outside the `data` directory.


### Return value

true if the property data is loaded successfully; otherwise, false.
## bool Load ( string path )

Loads the property from the specified [`*.prop` file](../../../code/formats/property_format.md).
### Arguments

- *string* **path** - Path to the `*.prop` file to load the property data from.

### Return value

true if the property data is loaded successfully; otherwise, false.
## bool LoadXml ( Xml xml )

Loads data of the property (all its parameters) from the given instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../api/library/common/class.xml_cs.md) instance in which the property data is stored.

### Return value

true if the property data is loaded successfully; otherwise, false.
## bool LoadWorld ( Xml xml )

Loads data of the current property (all its options, states and parameters) from the given instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../api/library/common/class.xml_cs.md) instance in which the property data is stored.

### Return value

true if the property data is loaded successfully; otherwise, false.
## bool Reload ( )

Reloads the property and all its children.
### Return value

true if the property is reloaded successfully; otherwise, false.
## bool CanSaveInFile ( )

Returns a value indicating if the property can be saved to a file. For example, this function will return 0 for an [internal](#isInternal_int) or [manual](#isManual_int) property.
### Return value

true if the property can be saved to a file; otherwise, false.
## bool SaveState ( Stream stream )


Saves data of the current property (all its parameters) into a binary stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int_int)* methods:


```csharp
// somewhere in code

// getting a manual property named "my_prop" via the Property Manager
Property property = Properties.findManualProperty("my_prop");
property.setParameterInt(property.findParameter("my_int_param"), 3);

// save state
Blob blob_state = new Blob();
property.SaveState(blob_state);

// change the state
property.setParameterInt(property.findParameter("my_int_param"), 4);

// restore state
blob_state.SeekSet(0);        // returning the carriage to the start of the blob
property.RestoreState(blob_state, 0);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream into which the property data will be saved.

### Return value

true if the property data is saved successfully; otherwise, false.
## bool RestoreState ( Stream stream , int restore_mode = 0 )


Restores the data of the property (all its parameters) from a binary stream in the specified mode.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```csharp
// somewhere in code

// getting a manual property named "my_prop" via the Property Manager
Property property = Properties.findManualProperty("my_prop");
property.setParameterInt(property.findParameter("my_int_param"), 3);

// save state
Blob blob_state = new Blob();
property.SaveState(blob_state);

// change the state
property.setParameterInt(property.findParameter("my_int_param"), 4);

// restore state
blob_state.SeekSet(0);        // returning the carriage to the start of the blob
property.RestoreState(blob_state, 0);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream in which the saved property parameter data is stored.
- *int* **restore_mode** - Restore mode. One of the [Property.RESTORE_MODE_*](#RESTORE_MODE_MERGE) values. The default value is [Property.RESTORE_MODE_REPLACE](#RESTORE_MODE_REPLACE).

### Return value

true on success; otherwise, false.
## bool Save ( )


Saves the property data to the file specified by the *[setFilePath()](#setFilePath_cstr_int)* function.


> **Notice:** This method is not available for [manual](#isManual_int) and [internal](#isInternal_int) properties.


### Return value

true if the property data is saved successfully; otherwise, false.
## bool Save ( string path )


Saves the property data to the specified [`*.prop` file](../../../code/formats/property_format.md).


> **Notice:** This method is not available for [manual](#isManual_int) properties.


### Arguments

- *string* **path** - Path to the `*.prop` file to save the property data to.

### Return value

true if the property data is saved successfully; otherwise, false.
## bool SaveXml ( Xml xml )


Saves data of the property (all its parameters) to the given instance of the Xml class.


> **Notice:** This method is not available for [manual](#isManual_int) properties.


### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../api/library/common/class.xml_cs.md) instance into which the property data will be saved.

### Return value

true if the property data is saved successfully; otherwise, false.
## bool SaveWorld ( Xml xml , int force = 0 )

Saves data of the current property (all its parameters) into the given instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../api/library/common/class.xml_cs.md) instance into which the property data will be saved.
- *int* **force** - A value indicating if forced saving of property data is used: 1 to enable forced saving, 0 to disable it.

### Return value

true if the property data is saved successfully; otherwise, false.
## int ParameterTypeByName ( string param_type )

Returns parameter type identifier by the type name specified.
### Arguments

- *string* **param_type** - Parameter type name.

### Return value

Parameter type identifier, one of the [PARAMETER_*](#PARAMETER_COLOR) variables.
## string ParameterNameByType ( int param_type )

Returns parameter type name by the type identifier specified.
### Arguments

- *int* **param_type** - Parameter type identifier, one of the [PARAMETER_*](#PARAMETER_COLOR) variables.

### Return value

Parameter type name.
## PropertyParameter GetParameterPtr ( string name )

Returns a [property parameter](../../../api/library/common/class.propertyparameter_cs.md) by its name.
### Arguments

- *string* **name** - Property parameter name.

### Return value

Property parameter instance.


> **Notice:** This method never returns nullptr, regardless of whether a parameter with the specified name exists or not. It only displays an error message in the console in case of a non-existing parameter. To check if such parameter really exists, use the [*PropertyParameter.isExist()*](../../../api/library/common/class.propertyparameter_cs.md#isExist_int) method. For example:
>
>
> ```csharp
> // getting some property named "my_property"
> Property pProperty = Properties.findManualProperty("my_property");
>
> // trying to get a property parameter named "some_parameter"
> PropertyParameter param = pProperty.getParameterPtr("some_parameter");
>
> // checking if such parameter exists and displaying a message
> if (param.isExist() == 1)
>     Log.Message("Specified property parameter exists!\n");
> else
>    Log.Message("No such parameter!\n");
>
> ```


## PropertyParameter GetParameterPtr ( int id )

Returns a [property parameter](../../../api/library/common/class.propertyparameter_cs.md) by its ID.
### Arguments

- *int* **id** - Property parameter ID.

### Return value

Property parameter instance.


> **Notice:** This method never returns nullptr, regardless of whether a parameter with the specified ID exists or not. It only displays an error message in the console in case of a non-existing parameter. To check if such parameter really exists, use the [*PropertyParameter.isExist()*](../../../api/library/common/class.propertyparameter_cs.md#isExist_int) method. For example:
>
>
> ```csharp
> // getting some property named "my_property"
> Property pProperty = Properties.findManualProperty("my_property");
>
> // trying to get a property parameter having the ID=30
> PropertyParameter param = pProperty.getParameterPtr(30);
>
> // checking if such parameter exists and displaying a message
> if (param.isExist() == 1)
>     Log.Message("Property parameter with the specified ID exists!\n");
> else
>    Log.Message("No such parameter!\n");
>
> ```


## int FindStruct ( string name )

Returns the number of the structure with the specified name.
### Arguments

- *string* **name** - Name of the structure to be found.

### Return value

Number of the structure with the specified name, if it exists; otherwise, -1.
## string GetStructName ( int num )

Returns the name of the structure with the specified number.
### Arguments

- *int* **num** - Structure number.

### Return value

Structure name, if such structure exists, otherwise NULL.
## string GetInterfaceName ( int num )


Returns the name of the interface with the specified number.


> **Notice:** You can use interfaces only within the C# Component System. For more information, see the article [C# Interfaces and Abstract Classes.](../../../code/csharp/interfaces_and_abstract_classes.md).

### Arguments

- *int* **num** - Interface number.

### Return value

Interface name, if such interface exists, otherwise NULL.
## bool SetFileGUID ( UGUID fileguid )

Changes the GUID of the file this property is stored in, re-binding the property to another property file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **fileguid** - New file GUID.

### Return value

true if the file GUID is changed successfully or already matches the current one; otherwise, false (another property is already registered with that file GUID).
## bool SetFilePath ( string path )

Sets the path of the file the property is stored in: the path is registered as a virtual file in the engine file system and the resulting GUID is assigned to the property.
### Arguments

- *string* **path** - Target file path.

### Return value

true on success; otherwise, false (a different property already occupies the resulting file GUID).
