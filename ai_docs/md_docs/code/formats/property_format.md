# Property File Format


## Property File Structure


A property is a `.prop` text file that contains the information to specify the way the object will behave and interact with other objects and the scene environment. Properties can be adjusted via the [UnigineEditor](../../editor2/node_parameters/properties/index.md) ([user](../../principles/properties/index.md#user) properties), via [API](../../api/library/common/class.property_cpp.md) or by manually editing the corresponding `.prop` file.


It is based on the `.xml` file type and shares all its methods.


A document (a `.prop` file) should have the `.xml` file declaration, containing its version and the type of encoding you are using. For example, to specify the 1.0 version and UTF-8 encoding, type:


```xml
<?xml version="1.0" encoding="utf-8"?>
```


There are 3 basic entities of the `.prop` file:


- **Element.** A component that may contain attributes, other elements, some content etc.
- **Attribute.** A component placed inside the element tag containing the specified value.
- **Value.** A component specifying the value of the attribute.


The syntax is the following:


```xml
<parent_element attribute="value">
	<child_element_1/>
	<child_element_2>content</child_element_2>
</parent_element>

```


## Property Element


The <property/> element defines a property.


It can have the attributes listed below.


### version


Version of the `.prop` file.


### name


Name of the property. Manual properties inherited from a manual property refer to it by name. This name is also used to generate GUID for the manual property at run time. This GUID is used by child user properties to refer to their manual parent.


> **Notice:** You cannot use two manual properties with the same name.


### guid


GUID for the property.


The guid attribute is optional. The GUID for the property will be generated from its name at runtime, if this attribute is not specified. GUID of a manual property is uniquely defined by its name.


### parent


[GUID](../../principles/properties/inheritance.md#property_guid) of a parent property. This attribute is used by a user property to refer to its parent.


### parent_name


Name of a parent property. The attribute is used in a manual property to refer to a manual parent property.


### manual


Flag, indicating if the property is [manual](../../principles/properties/index.md#manual): created or edited manually (not via the UnigineEditor).


Available values:


- 0 - not manual (by default)
- 1 - manual


### editable


Flag indicating if settings of the property can be modified in the [UnigineEditor](../../editor2/properties_settings/index.md) or via [code](../../api/library/common/class.property_cpp.md).


> **Notice:** [Manual](../../principles/properties/index.md#manual) properties are displayed as read-only in the Editor regardless of the value of this flag.


Available values:


- 0 - cannot be edited
- 1 - editable (by default)


### hidden


Flag indicating if the property is displayed in the [Properties Hierarchy](../../editor2/interface/index.md#properties_hierarchy) window. Sometimes it may be necessary to hide properties from artists in the UnigineEditor (e.g. to store certain information used for debugging purposes), this flag allows you to do so.


Available values:


- 0 - displayed (by default)
- 1 - hidden


### editor_only


Flag indicating if the property is assigned to a node only when the application is opened in UnigineEditor. When enabled, the property isn't added to the node in the play mode, reducing RAM consumption.


Available values:


- 0 - always assigned to the node (by default)
- 1 - assigned to the node only when the application is opened in UnigineEditor.


### interfaces


Flag that specifies the list of **[interfaces](../../code/csharp/interfaces_and_abstract_classes.md)** implemented by a C# Component. Applicable in the context of the property-based C# Component System.


### Usage Example


For example, to create a manual property named custom_property and make it unchangeable, use the following:


```xml
<property version="2.20" name="custom_property" manual="1" editable="0">
...
</property>

```


## Parameter Struct


A <struct/> element defines a structured type to be used for a property [parameter](#element_parameter)(s). The property can have an as many structures as necessary. You can think of structure as "a definition of a property inside a property", so it can have the same child elements as the *<property/>* element (i.e. *<parameter/> and <struct/>*)


> **Notice:** A [structure](../../principles/properties/index.md#structures) can be inherited from another structure, in this case the parent must be defined inside the `*.prop` file before its child.


The element can have the attributes listed below.


### name


Unique name of the structure.


> **Notice:** Reserved attribute names ("name", "type", etc.) cannot be used.


### parent_name


Unique name of the base structure from which this structure inherits.


> **Notice:** Reserved attribute names ("name", "type", etc.) cannot be used.


### Usage Example


For example, to create a base structure named "struct1", inherit another structure named "struct2" with an extended set of parameters, and create a parameter named "my_struct_param" of the *struct2* type, use the following:


```xml
<?xml version="1.0" encoding="utf-8"?>
<property version="2.20" name="custom_prop" manual="1">
	<struct name="struct1">
		<parameter name="param_a" type="int" a="0">1</parameter>
		<parameter name="param_b" type="toggle">0</parameter>
		<parameter name="param_c" type="int" sa="100">1</parameter>
	</struct>
	<struct name="struct2" parent_name="struct1">
		<parameter name="param2_a" type="toggle">0</parameter>
		<parameter name="param2_b" type="toggle">1</parameter>
	</struct>
	<parameter name="my_struct_param" type="struct2"></parameter>
</property>

```


## Value Element


A <value/> element defines an element of an [array parameter](#array_type).


> **Notice:** This element can be used only inside a [<parameter>](#element_parameter) element having the *array* [type](#parameter_type)


```xml
<?xml version="1.0" encoding="utf-8"?>
<property version="2.20" name="custom_prop" manual="1">
	<parameter name="my_array" type="array" array_type="int">
		<value>1</value>
		<value>2</value>
		<value>3</value>
	</parameter>
</property>

```


The element has the following attribute:


### index


Index of an array element for which a value is declared. For example, to specify a value of the 10th element of the array of *integer* elements, you can use:


```xml
<?xml version="1.0" encoding="utf-8"?>
<property version="2.20" name="custom_prop" manual="1">
	<parameter name="my_array" type="array" array_type="int">
		<value index="10">133</value>
	</parameter>
</property>

```


## Parameter Element


A <parameter/> element defines a single parameter of the property. The property can have several parameters.


The element can have the attributes listed below.


### flags


Attribute that allows specifying some additional conditions for the parameters of the different types.


Available values for *file* type:


- asset - indicates that the [*file*](#parameter_type) parameter refers to an [asset](../../editor2/assets_workflow/assets_runtimes.md)
- runtime - indicates that the [*file*](#parameter_type) parameter refers to a [runtime file](../../editor2/assets_workflow/assets_runtimes.md) (this flag is set by default)
- abspath - indicates that the [*file*](#parameter_type) parameter stores an absolute file path


Available values for *int*, *float* and *double* types:


- log10 - a logarithmic slider (with the base ten)
- expand - a value indicating if the [minimum and maximum](#parameter_min_max) values of the slider parameter can be exceeded
- min_expand - a value indicating if the [minimum](#parameter_min_max) value of the slider parameter can be decreased
- max_expand - a value indicating if the [maximum](#parameter_min_max) value of the slider parameter can be increased


The *flags* parameter of the *mask* type can have one of the following values defining the type of the [bit mask](../../principles/bit_masking/index.md): intersection, physics_intersection, collision, exclusion, viewport, shadows, material, sound_source, sound_reverb, sound_occlusion, navigation, obstacle, physical, field.


The *property* type parameter can have the following flags:


- [internal](../../principles/properties/index.md#internal) - indicates that the property parameter accepts only properties that are already attached to a node in the world. When this flag is set, properties from the Asset Browser cannot be assigned to the parameter.
- interface - indicates that the property parameter is of interface type, allowing it to reference any component that implements the specified interface, regardless of its concrete type.


```xml
<parameter name="My_bit_mask" type="mask" flags="collision">1</parameter>

```


### hidden


Flag indicating if the parameter is displayed in the [Parameters](../../editor2/interface/index.md#parameters) window.


Available values:


- 0 - displayed (by default)
- 1 - hidden


### items


Attribute that contains a set of values of the [switch](#parameter_type) parameter. Each of these values may have an optional arbitrary name associated with it. Items can have positive or negative values, several items can have the same value.


```xml
<parameter name="material_color" type="switch" items="red,green,blue,orange,yellow">0</parameter>

```


> **Notice:** The space in the *items* attribute declaration is also a symbol included in the item name. Thus, **items="red,�green"** shall produce the items with the following names: **"red"** and **" green"** (with the space before the word).


For example, if a property switch parameter is declared as follows:


```xml
<parameter items="red=-1,green,blue=5,yellow"/>
```


After loading we'll have switch items with the following values: *red* = **-1**, *green* = **0**, *blue* = **5**, *yellow* = **6**. When addressing these switch items via code, we can use either their ordinal numbers starting from 0, or the values assigned to them.


```cpp
PropertyParameter::setValue(5); // "blue" is selected in the corresponding combobox in UnigineEditor
PropertyParameter::setSwitchItem(3); // "yellow" is selected (3rd item, starting from 0)

// If "green" item is selected in UnigineEditor:
PropertyParameter::getValueInt(); // returns 0, as "green" corresponds to the value of 0.
PropertyParameter::getSwitchItem() // returns 1, as "green" is the 1st element in the combobox (starting from 0).

```


### min and max


Minimum and maximum available values of the *[integer](../../api/library/common/class.propertyparameter_cpp.md#getIntMaxValue_int)*, *[float](../../api/library/common/class.propertyparameter_cpp.md#getFloatMaxValue_float)* and *[double](../../api/library/common/class.propertyparameter_cpp.md#getDoubleMaxValue_double)* parameters.


### name


Unique name of the parameter.


> **Notice:** Reserved attribute names ("name", "type", etc.) cannot be used.


### title


Parameter title that will be displayed in the UnigineEditor.


### tooltip


Tooltip for the parameter. The tooltip will be displayed in the UnigineEditor when the parameter field is pointed with the mouse.


### group


Group to which the parameter belongs. The parameter will be displayed in the specified group in the UnigineEditor. This attribute is optional: you can use the *[group](#element_group)* element instead.


### type


Type of the parameter.


Available values:


- int - type of the property parameter that allows accepting an *integer* value in a given range
- mask - type of the property parameter that allows specifying a mask (an *integer* value)
- float - type of the property parameter that allows accepting a *float* value in a given range
- double - type of the property parameter that allows accepting a *double* value in a given range
- string - type of the property parameter that allows accepting a *string* value
- switch - a set of several possible values (more than 2) for the parameter is available
- toggle - only 2 possible values for the parameter are available (default)
- vec2 - type of the property parameter that allows accepting a *vec2* value
- vec3 - type of the property parameter that allows accepting a *vec3* value
- vec4 - type of the property parameter that allows accepting a *vec4* value
- dvec2 - type of the property parameter that allows accepting a *dvec2* value
- dvec3 - type of the property parameter that allows accepting a *dvec3* value
- dvec4 - type of the property parameter that allows accepting a *dvec4* value
- ivec2 - type of the property parameter that allows accepting a *ivec2* value
- ivec3 - type of the property parameter that allows accepting a *ivec3* value
- ivec4 - type of the property parameter that allows accepting a *ivec4* value
- color - type of the property parameter that allows specifying a color (a *vec4* value)
- curve2d - type of the property parameter that allows specifying a 2D curve (a *[Curve2d](../../api/library/common/class.curve2d_cpp.md)* instance)
- file - type of the property parameter that allows accepting any file *GUID* or path (e.g. to [a runtime file or an asset](../../editor2/assets_workflow/assets_runtimes.md))
- property - type of the property parameter that allows accepting a *GUID* value of a property
- material - type of the property parameter that allows accepting a *GUID* value of a material
- node - type of the property parameter that allows specifying a *node* or a node ID (an *integer* value)
- <struct_name> - type of the property parameter that allows specifying a structure. > **Notice:** <struct_name>here can be any name of a [<struct/>](#element_struct) element previously defined in the `*.prop` file.
- array - type of the property parameter that allows specifying an array of parameters, all having the same type (any of the above, including *struct* types previously defined), and accessed using a common name followed by an index: array[0].


### array_type


String specifying the type of elements for an *array* parameter (see above).


> **Notice:** This attribute is available only for *array* [parameter types](#parameter_type).


Here you can specify any of the types listed above, plus any name of a [<struct/>](#element_struct) element previously defined in the `*.prop` file.


### array_dim


Dimension of the *array* parameter (see above). This attribute is used to declare multi-dimensional arrays.


> **Notice:** This attribute is available only for *array* [parameter types](#parameter_type).


By default it is assumed that **array_dim = 1**, So, this attribute is optional for one-dimensional arrays.


### filter


String specifying a filter for *file*, *material* or *property* parameter values. For example, you can specify ".xml|.node|.txt" to filter certain types of files.


> **Notice:** This attribute is available only for *file*, *material* and *property* [parameter types](#parameter_type).


The attribute is optional.


### Parameter Conditions


You can use conditions to display or hide the parameter in the UnigineEditor depending on the values of some other parameters. The condition should be declared as follows:


**PARAMETER_NAME = "VALUE_1 [, VALUE_2, ..., VALUE_8]".**


> **Notice:** - Conditions can be evaluated for *int*, *toggle* and *switch* [parameter types](#parameter_type)
> - Maximum number of values is 8.
> - Conditions for standard attributes ("name", "type", etc.) cannot be used.


You can use multiple conditions (see the example below), the parameter will be displayed only when all specified conditions are true.


### Usage Example


For example, to add a *string* parameter named "my_str" that will be displayed only when *my_toggle* parameter is enabled, *my_switch* parameter is set to **type2** or **type3**, and *my_int* parameter is equal to 15 use the following:


```xml
<?xml version="1.0" encoding="utf-8"?>
<property version="2.20" name="custom_prop" manual="1">
	<parameter name="my_type" type="switch" items="type1,type2,type3">1</parameter>
	<parameter name="my_toggle" type="toggle">1</parameter>
	<parameter name="my_int">15</parameter>
	<parameter name="my_str" my_type="1,2" my_toggle="1" my_int="15" type="string">All conditions are true!</parameter>
</property>

```


## Group Element


A <group/> element specifies the group to which the parameters of the property belong to. The element is optional: parameters can be defined out of it. You can also specify the *group* attribute for the *<parameter/>* element instead of using the *<group/>* element.


### name


Name of the group.


### Usage Example


For example, some parameters of a property named "my_property" can be grouped as follows:


```xml
<?xml version="1.0" encoding="utf-8"?>
<property version="2.20" name="my_property" parent_name="node_base" manual="1">
	<group name="Default">
		<parameter name="Param1">15</parameter>
		<parameter name="Param2">25</parameter>
		<parameter name="my_file" type="file" flags="asset">1.png</parameter>
		<parameter name="Param3" title="test_title">150</parameter>
	</group>
</property>

```


Or the *group* attribute can be used instead of the corresponding element:


```xml
<?xml version="1.0" encoding="utf-8"?>
<property version="2.20" name="custom_prop" manual="1">
	<parameter name="Param1" group="Group1">15</parameter>
	<parameter name="Param2" group="Group1">25</parameter>
	<parameter name="Param3" title="test_title" type="string">Hello, World!!!</parameter>
</property>

```


## Declaring Arrays


[*Array*](#array_type) parameter type enables you to declare a collection of parameters, all having the same type (specified via the [*array_type*](#parameter_array_type) attribute), and accessed using a common name followed by an index: **array[0]**.


You can declare multi-dimensional (specifying dimension via the [*array_type*](#parameter_array_type) attribute), but be careful: the amount of memory needed for an array increases exponentially with each dimension.  Arrays of [structures](#element_struct) are also supported.


To specify values of array elements when declaring an array, use the [<value/>](#element_value) element.


> **Notice:** It is not necessary to declare all array elements. You can specify values only for some of them via the [*index*](#value_index) attribute of the [<value/>](#element_value) element (can be useful for declaring overrides).


Below is an example of declaring a property with a 2-dimensional array of *float* elements, named **my_array2D**, and specifying values for some of the elements.


So, the array parameter of the property has **4** elements:


1. array containing three float values: **0.0, 0.5, 1.0**
2. array containing two float values: **0.0** (*default*), **0.25**
3. array containing a single float value: **3.25**
4. empty array (no elements)


```xml
<?xml version="1.0" encoding="utf-8"?>
<property version="2.20" name="my_property" parent_name="node_base" manual="1">
<parameter name="my_array2D" type="array" array_type="float" array_dim="2">
  <value>
	<value>0.0</value>
	<value>0.5</value>
	<value>1.0</value>
  </value>
  <value>
   <value index="1">0.25</value>
  </value>
  <value>
   <value>3.25</value>
  </value>
  <value/>
 </parameter>
</property>

```
