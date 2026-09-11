# Unigine::PropertyParameter Class (CPP)

**Header:** #include <UnigineProperties.h>


This class is used to represent a [property parameter](../../../code/formats/property_format.md#element_parameter).


## PropertyParameter Class

### Members

## const char * getStructName () const

Returns the current name of the structure that defines the type of the struct parameter.
### Return value

Current name of the structure that defines the type of the struct parameter.
## int getArrayDim () const

Returns the current dimension of the array parameter.
> **Notice:** Multi-dimensional arrays are represented as arrays of arrays, thus, the return value of this method will decrease with each level down the hierarchy.


### Return value

Current dimension of the array parameter.
## const char * getArrayTypeName () const

Returns the current type name of elements of the array parameter.
### Return value

Current type name of elements of the array parameter (Float, Node, Material, etc.).
## int getArrayType () const

Returns the current type of elements of the array parameter.
### Return value

Current type of array elements, one of the [*PARAMETER_**](../../../api/library/common/class.property_cpp.md#PARAMETER_COLOR) variables.
> **Notice:** This method does not return [*PARAMETER_ARRAY*](../../../api/library/common/class.property_cpp.md#PARAMETER_ARRAY) for an array parameter, it returns the type of array elements instead (e.g. [*PARAMETER_FLOAT*](../../../api/library/common/class.property_cpp.md#PARAMETER_FLOAT), [*PARAMETER_STRUCT*](../../../api/library/common/class.property_cpp.md#PARAMETER_STRUCT), etc.)

## void setArraySize ( int size )

Sets a new size of the array parameter.
### Arguments

- *int* **size** - The array size (number of elements).

## int getArraySize () const

Returns the current size of the array parameter.
### Return value

Current array size (number of elements).
## void setValueFile ( const char * file )

Sets a new
value of the [file parameter](../../../code/formats/property_format.md#parameter_type). If the property is not [editable](../../../api/library/common/class.property_cpp.md#isEditable_int), the value won't be updated.


The value stored in the file parameter depends on the [flags](../../../code/formats/property_format.md#parameter_flags) set for the parameter.


```cpp
// flags = "asset"
setValueFile("guid://asset_guid"); 		// getValueFile() -> asset_path
setValueFile("guid://runtime_guid");	// getValueFile() -> asset_path
setValueFile("asset_path");				// getValueFile() -> asset_path
setValueFile("runtime_path");			// getValueFile() -> asset_path

// flags = "runtime" - default
setValueFile("guid://asset_guid"); 		// getValueFile() -> runtime_path
setValueFile("guid://runtime_guid");	// getValueFile() -> runtime_path
setValueFile("asset_path");				// getValueFile() -> runtime_path
setValueFile("runtime_path");			// getValueFile() -> runtime_path

// flags = "abspath"
setValueFile(file_path);				// getValueFile() -> file_path

```


### Arguments

- *const char ** **file** - The value for the file parameter.

## const char * getValueFile () const

Returns the current
value of the [file parameter](../../../code/formats/property_format.md#parameter_type). If the property is not [editable](../../../api/library/common/class.property_cpp.md#isEditable_int), the value won't be updated.


The value stored in the file parameter depends on the [flags](../../../code/formats/property_format.md#parameter_flags) set for the parameter.


```cpp
// flags = "asset"
setValueFile("guid://asset_guid"); 		// getValueFile() -> asset_path
setValueFile("guid://runtime_guid");	// getValueFile() -> asset_path
setValueFile("asset_path");				// getValueFile() -> asset_path
setValueFile("runtime_path");			// getValueFile() -> asset_path

// flags = "runtime" - default
setValueFile("guid://asset_guid"); 		// getValueFile() -> runtime_path
setValueFile("guid://runtime_guid");	// getValueFile() -> runtime_path
setValueFile("asset_path");				// getValueFile() -> runtime_path
setValueFile("runtime_path");			// getValueFile() -> runtime_path

// flags = "abspath"
setValueFile(file_path);				// getValueFile() -> file_path

```


### Return value

Current value for the file parameter.
## int getMaskType () const

Returns the current type of elements of the mask parameter.
### Return value

Current Type of the mask parameter, one of the [*PARAMETER_MASK_**](../../../api/library/common/class.property_cpp.md#PARAMETER_MASK_FIELD) variables.
## int getSwitchNumItems () const

Returns the current number of [items](../../../code/formats/property_format.md#parameter_items) of the [switch parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_SWITCH*](../../../api/library/common/class.property_cpp.md#PARAMETER_SWITCH) variable isn't set for the parameter, the function will return 0.
### Return value

Current number of items of the switch parameter.
## int getSliderMaxExpand () const

Returns the current value indicating if the maximum value of the slider parameter can be [decreased](../../../code/formats/property_format.md#parameter_flags). Slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cpp.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cpp.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cpp.md#PARAMETER_INT).
### Return value

Current 1 if the maximum value can be changed; otherwise, 0.
## int getSliderMinExpand () const

Returns the current value indicating if the minimum value of the slider parameter can be [decreased](../../../code/formats/property_format.md#parameter_flags). Slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cpp.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cpp.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cpp.md#PARAMETER_INT).
### Return value

Current 1 if the minimum value can be changed; otherwise, 0.
## int getSliderLog10 () const

Returns the current value indicating if the slider parameter uses a [logarithmic scale](../../../code/formats/property_format.md#parameter_flags) (with the base ten). The slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cpp.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cpp.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cpp.md#PARAMETER_DOUBLE).
### Return value

Current 1 if the property parameter uses a logarithmic scale; otherwise, 0.
## double getDoubleMaxValue () const

Returns the current maximum double value of the property parameter.
### Return value

Current maximum double value of the property parameter.
## double getDoubleMinValue () const

Returns the current minimum double value of the property parameter.
### Return value

Current minimum double value of the property parameter.
## float getFloatMaxValue () const

Returns the current maximum float value of the property parameter.
### Return value

Current maximum float value of the property parameter.
## float getFloatMinValue () const

Returns the current minimum float value of the property parameter.
### Return value

Current minimum float value of the property parameter.
## int getIntMaxValue () const

Returns the current maximum integer value of the property parameter.
### Return value

Current maximum integer value of the property parameter.
## int getIntMinValue () const

Returns the current minimum integer value of the property parameter.
### Return value

Current minimum integer value of the property parameter.
## void setValueGUID ( const UGUID & guid )

Sets a new value of the [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) property parameter.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - The value of the [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) property parameter.

## const UGUID & getValueGUID () const

Returns the current value of the [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) property parameter.
### Return value

Current value of the [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) property parameter.
## void setValueMask ( int mask )

Sets a new value of the [mask parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_MASK*](../../../api/library/common/class.property_cpp.md#PARAMETER_MASK) variable isn't set for the parameter, or the property is not [editable](../../../api/library/common/class.property_cpp.md#isEditable_int), the value won't be updated.
### Arguments

- *int* **mask** - The value of the integer mask property parameter.

## int getValueMask () const

Returns the current value of the [mask parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_MASK*](../../../api/library/common/class.property_cpp.md#PARAMETER_MASK) variable isn't set for the parameter, or the property is not [editable](../../../api/library/common/class.property_cpp.md#isEditable_int), the value won't be updated.
### Return value

Current value of the integer mask property parameter.
## void setValueSwitch ( int switch )

Sets a new value of the [switch parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_SWITCH*](../../../api/library/common/class.property_cpp.md#PARAMETER_SWITCH) variable isn't set for the parameter, the function will return 0.
### Arguments

- *int* **switch** - The value of the switch parameter.

## int getValueSwitch () const

Returns the current value of the [switch parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_SWITCH*](../../../api/library/common/class.property_cpp.md#PARAMETER_SWITCH) variable isn't set for the parameter, the function will return 0.
### Return value

Current value of the switch parameter.
## void setValueToggle ( bool toggle )

Sets a new value of the [toggle parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_TOGGLE*](../../../api/library/common/class.property_cpp.md#PARAMETER_TOGGLE) variable isn't set for the parameter, the function will return 0.
### Arguments

- *bool* **toggle** - true for the toggle parameter value set as enabled, and false for the disabled value.

## bool getValueToggle () const

Returns the current value of the [toggle parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_TOGGLE*](../../../api/library/common/class.property_cpp.md#PARAMETER_TOGGLE) variable isn't set for the parameter, the function will return 0.
### Return value

true for the toggle parameter value set as enabled, and false for the disabled value.
## void setValueNodeID ( int id )

Sets a new value of the node ID property parameter.
### Arguments

- *int* **id** - The value of the node ID property parameter.

## int getValueNodeID () const

Returns the current value of the node ID property parameter.
### Return value

Current value of the node ID property parameter.
## void setValueNode ( const Ptr < Node >& node )

Sets a new value of the *[Node](../../../api/library/nodes/class.node_cpp.md)* property parameter.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>&* **node** - The value of the *[Node](../../../api/library/nodes/class.node_cpp.md)* property parameter.

## Ptr < Node > getValueNode () const

Returns the current value of the *[Node](../../../api/library/nodes/class.node_cpp.md)* property parameter.
### Return value

Current value of the *[Node](../../../api/library/nodes/class.node_cpp.md)* property parameter.
## void setValueMaterial ( const Ptr < Material >& material )

Sets a new value of the *[Material](../../../api/library/rendering/class.material_cpp.md)* property parameter.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)>&* **material** - The value of the *[Material](../../../api/library/rendering/class.material_cpp.md)* property parameter.

## Ptr < Material > getValueMaterial () const

Returns the current value of the *[Material](../../../api/library/rendering/class.material_cpp.md)* property parameter.
### Return value

Current value of the *[Material](../../../api/library/rendering/class.material_cpp.md)* property parameter.
## void setValueProperty ( const Ptr < Property >& property )

Sets a new value of the *[Property](../../../api/library/common/class.property_cpp.md)*-type property parameter.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)>&* **property** - The value of the *[Property](../../../api/library/common/class.property_cpp.md)*-type property parameter.

## Ptr < Property > getValueProperty () const

Returns the current value of the *[Property](../../../api/library/common/class.property_cpp.md)*-type property parameter.
### Return value

Current value of the *[Property](../../../api/library/common/class.property_cpp.md)*-type property parameter.
## void setValueVec4 ( const Math:: vec4 & vec4 )

Sets a new value of the four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector property parameter
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **vec4** - The value of the four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector property parameter

## Math:: vec4 getValueVec4 () const

Returns the current value of the four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector property parameter
### Return value

Current value of the four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector property parameter
## void setValueVec3 ( const Math:: vec3 & vec3 )

Sets a new value of the three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector property parameter
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **vec3** - The value of the three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector property parameter

## Math:: vec3 getValueVec3 () const

Returns the current value of the three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector property parameter
### Return value

Current value of the three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector property parameter
## void setValueString ( const char * string )

Sets a new value of the string property parameter.
### Arguments

- *const char ** **string** - The value of the string property parameter.

## const char * getValueString () const

Returns the current value of the string property parameter.
### Return value

Current value of the string property parameter.
## void setValueColor ( const Math:: vec4 & color )

Sets a new value of the four-component [vec4](../../../api/library/math/class.vec4_cpp.md) color vector (R, G, B, A) property parameter.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The value of the four-component [vec4](../../../api/library/math/class.vec4_cpp.md) color vector (R, G, B, A) property parameter.

## Math:: vec4 getValueColor () const

Returns the current value of the four-component [vec4](../../../api/library/math/class.vec4_cpp.md) color vector (R, G, B, A) property parameter.
### Return value

Current value of the four-component [vec4](../../../api/library/math/class.vec4_cpp.md) color vector (R, G, B, A) property parameter.
## void setValueDouble ( double double )

Sets a new value of the double property parameter.
### Arguments

- *double* **double** - The value of the double property parameter.

## double getValueDouble () const

Returns the current value of the double property parameter.
### Return value

Current value of the double property parameter.
## void setValueFloat ( float float )

Sets a new value of the float property parameter.
### Arguments

- *float* **float** - The value of the float property parameter.

## float getValueFloat () const

Returns the current value of the float property parameter.
### Return value

Current value of the float property parameter.
## void setValueInt ( int int )

Sets a new value of the integer property parameter.
### Arguments

- *int* **int** - The value of the integer property parameter.

## int getValueInt () const

Returns the current value of the integer property parameter.
### Return value

Current value of the integer property parameter.
## Ptr < Curve2d > getValueCurve2dOverride () const

Returns the current [Curve2d](../../../api/library/common/class.curve2d_cpp.md) instance for the data stored in the specified property parameter overriding the default one.
This method enables you to set individual curves, adjusting the value of the resulting property.


> **Notice:** Modifications made to the curve shall not propagate to the parent and sibling properties.


### Return value

Current
## void setValueCurve2d ( const Ptr < Curve2d >& curve2d )

Sets a new [Curve2d](../../../api/library/common/class.curve2d_cpp.md) value of the property parameter.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Curve2d](../../../api/library/common/class.curve2d_cpp.md)>&* **curve2d** - The [Curve2d](../../../api/library/common/class.curve2d_cpp.md) value of the property parameter.

## Ptr < Curve2d > getValueCurve2d () const

Returns the current [Curve2d](../../../api/library/common/class.curve2d_cpp.md) value of the property parameter.
### Return value

Current [Curve2d](../../../api/library/common/class.curve2d_cpp.md) value of the property parameter.
## bool isCurve2d () const

Returns the current value indicating if the property parameter is a 2d curve.
### Return value

**true** if the property parameter is a 2d curve; otherwise **false**.
## bool isStruct () const

Returns the current value indicating if the property parameter is a structure.
### Return value

**true** if the property parameter is a structure; otherwise **false**.
## bool isArray () const

Returns the current value indicating if the property parameter is an array.
### Return value

**true** if the property parameter is an array; otherwise **false**.
## bool isNode () const

Returns the current value indicating if the property parameter is a node.
### Return value

**true** if the property parameter is a node; otherwise **false**.
## bool isMaterial () const

Returns the current value indicating if the property parameter is a material.
### Return value

**true** if the property parameter is a material; otherwise **false**.
## bool isProperty () const

Returns the current value indicating if the property parameter is a property.
### Return value

**true** if the property parameter is a property; otherwise **false**.
## bool isFile () const

Returns the current value indicating if the property parameter is a file.
### Return value

**true** if the property parameter is a file; otherwise **false**.
## bool isMask () const

Returns the current value indicating if the property parameter is a mask.
### Return value

**true** if the property parameter is a mask; otherwise **false**.
## bool isIVec4 () const

Returns the current value indicating if the property parameter is a vector of 4 integer components.
### Return value

**true** if the property parameter is a vector of 4 integer components; otherwise **false**.
## bool isIVec3 () const

Returns the current value indicating if the property parameter is a vector of 3 integer components.
### Return value

**true** if the property parameter is a vector of 3 integer components; otherwise **false**.
## bool isIVec2 () const

Returns the current value indicating if the property parameter is a vector of 2 integer components.
### Return value

**true** if the property parameter is a vector of 2 integer components; otherwise **false**.
## bool isDVec4 () const

Returns the current value indicating if the property parameter is a vector of 4 double components.
### Return value

**true** if the property parameter is a vector of 4 double components; otherwise **false**.
## bool isDVec3 () const

Returns the current value indicating if the property parameter is a vector of 3 double components.
### Return value

**true** if the property parameter is a vector of 3 double components; otherwise **false**.
## bool isDVec2 () const

Returns the current value indicating if the property parameter is a vector of 2 double components.
### Return value

**true** if the property parameter is a vector of 2 double components; otherwise **false**.
## bool isVec4 () const

Returns the current value indicating if the property parameter is a vector of 4 float components.
### Return value

**true** if the property parameter is a vector of 4 float components; otherwise **false**.
## bool isVec3 () const

Returns the current value indicating if the property parameter is a vector of 3 float components.
### Return value

**true** if the property parameter is a vector of 3 float components; otherwise **false**.
## bool isVec2 () const

Returns the current value indicating if the property parameter is a vector of 2 float components.
### Return value

**true** if the property parameter is a vector of 2 float components; otherwise **false**.
## bool isColor () const

Returns the current value indicating if the property parameter is a color.
### Return value

**true** if the property parameter is a color; otherwise **false**.
## bool isString () const

Returns the current value indicating if the property parameter is a string.
### Return value

**true** if the property parameter is a string; otherwise **false**.
## bool isSwitch () const

Returns the current value indicating if the property parameter is a switch.
### Return value

**true** if the property parameter is a switch; otherwise **false**.
## bool isToggle () const

Returns the current value indicating if the property parameter is a toggle.
### Return value

**true** if the property parameter is a toggle; otherwise **false**.
## bool isDouble () const

Returns the current value indicating if the property parameter is a *double*.
### Return value

**true** if the property parameter is a *double*; otherwise **false**.
## bool isFloat () const

Returns the current value indicating if the property parameter is a *float*.
### Return value

**true** if the property parameter is a *float*; otherwise **false**.
## bool isInt () const

Returns the current value indicating if the property parameter is an integer.
### Return value

**true** if the property parameter is an integer; otherwise **false**.
## const char * getFilter () const

Returns the current filter string associated with the property parameter.
This string specifies a filter for *File, Material* or *Property* parameter values thet will be used in the UnigineEditor. for example, you can specify *".xml|.node|.txt"* to filter certain types of assets, or specify a base material to filter out materials, that cannot be used in a particular case (e.g. to avoid an attempt of assigning a post material to a mesh).


> **Notice:** This attribute is available only for [file](../../../api/library/common/class.property_cpp.md#PARAMETER_FILE), [material](../../../api/library/common/class.property_cpp.md#PARAMETER_MATERIAL) and [property](../../../api/library/common/class.property_cpp.md#PARAMETER_PROPERTY) parameter types.


### Return value

Current string specifying a filter for *File, Material* or *Property* parameter values.
## const char * getGroup () const

Returns the current name of the group to which the property parameter belongs.
### Return value

Current name of the group to which the property parameter belongs.
## const char * getTooltip () const

Returns the current tooltip for the property parameter. This title is displayed in the UnigineEditor UI.
### Return value

Current tooltip for the property parameter.
## const char * getTitle () const

Returns the current title of the property parameter. This title is displayed in the UnigineEditor UI.
### Return value

Current title of the property parameter.
## const char * getName () const

Returns the current name of the property parameter.
### Return value

Current name of the property parameter.
## int getType () const

Returns the current [type](../../../code/formats/property_format.md#parameter_type) identifier of the property parameter.
You can get the name of the parameter type using the *[Property::parameterNameByType()](../../../api/library/common/class.property_cpp.md#parameterNameByType_int_cstr)* method:


```cpp
Log::message("Parameter type: %s\n", prop_param->parameterNameByType(prop_param->getType()));
```


### Return value

Current One of the **[PARAMETER_*](../../../api/library/common/class.property_cpp.md#PARAMETER_COLOR)** pre-defined variables; if an error occurs, -1 will be returned.
## const char * getTypeName () const

Returns the current name of the property parameter type.
### Return value

Current name of the property parameter type.
## bool isOverridden () const

Returns the current value indicating if the property parameter is overridden. For all parameter types except for *int* and *string* **the value will be considered overridden even in case of assigning the initial (default) value to it**. To check whether the default value for the parameter has actually changed, we recommend using comparison operators and methods, as in this respect *isOverridden()* will only help you with *int* and *string*.
### Return value

**true** if the property parameter is overridden; otherwise **false**.
## bool isInherited () const

Returns the current value indicating if the property parameter is inherited from a parent.
### Return value

**true** if the property parameter is inherited from a parent; otherwise **false**.
## bool isHidden () const

Returns the current value indicating if the property parameter is [hidden](../../../code/formats/property_format.md#parameter_hidden).
### Return value

**true** if the property parameter is hidden; otherwise **false**.
## bool isExist () const

Returns the current value indicating if the property parameter is an existing one.
### Return value

**true** if the property parameter is an existing one; otherwise **false**.
## int getNumChildren () const

Returns the current total number of children of the property parameter.
### Return value

Current total number of children of the property parameter.
## Ptr < PropertyParameter > getParent () const

Returns the current parent property parameter, if it exists.
### Return value

Current Parent property parameter, if it exists; otherwise, nullptr.
## UGUID getPropertyGUID () const

Returns the current [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property that owns the parameter.
### Return value

Current [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property that owns the parameter.
## Ptr < Property > getProperty () const

Returns the current property that owns the parameter.
### Return value

Current property that owns the parameter.
## int getID () const

Returns the current ID of the property parameter.
### Return value

Current ID of the property parameter.
## void setSwitchItem ( int item )

Sets a new number of the [item](../../../code/formats/property_format.md#parameter_items) of the [switch parameter](../../../code/formats/property_format.md#parameter_type).
Suppose we have a property switch parameter declared as follows:


```xml
<parameter items="red=-1,green,blue=5,yellow"/>
```


> **Notice:** Spaces in the *items* attribute declaration are taken into account. Thus, **items="red=-1, green"** shall produce 2 items: **"red"** and **" green"**


After loading we'll have switch items with the following values: *red = -1, green = 0, blue = 5, yellow = 6*.


```cpp
PropertyParameter::setValue(5); // "blue" shall be selected in the corresponding combobox in the UnigineEditor
PropertyParameter::setSwitchItem(3); // "yellow" shall be selected in the corresponding combobox in the UnigineEditor (as it is the 3-rd item, starting from 0).

// If "green" item is selected in the UnigineEditor:
PropertyParameter::getValueInt(); // returns 0, as "green" corresponds to the value of 0.
PropertyParameter::getSwitchItem() // returns 1, as "green" is the 1-st element in the combobox (starting from 0).

```


### Arguments

- *int* **item** - The number of the item of the switch parameter.

## int getSwitchItem () const

Returns the current number of the [item](../../../code/formats/property_format.md#parameter_items) of the [switch parameter](../../../code/formats/property_format.md#parameter_type).
Suppose we have a property switch parameter declared as follows:


```xml
<parameter items="red=-1,green,blue=5,yellow"/>
```


> **Notice:** Spaces in the *items* attribute declaration are taken into account. Thus, **items="red=-1, green"** shall produce 2 items: **"red"** and **" green"**


After loading we'll have switch items with the following values: *red = -1, green = 0, blue = 5, yellow = 6*.


```cpp
PropertyParameter::setValue(5); // "blue" shall be selected in the corresponding combobox in the UnigineEditor
PropertyParameter::setSwitchItem(3); // "yellow" shall be selected in the corresponding combobox in the UnigineEditor (as it is the 3-rd item, starting from 0).

// If "green" item is selected in the UnigineEditor:
PropertyParameter::getValueInt(); // returns 0, as "green" corresponds to the value of 0.
PropertyParameter::getSwitchItem() // returns 1, as "green" is the 1-st element in the combobox (starting from 0).

```


### Return value

Current number of the item of the switch parameter.
## void setValueIVec4 ( const Math:: ivec4 & ivec4 )

Sets a new value of the four-component [ivec4](../../../api/library/math/class.ivec4_cpp.md) vector property parameter.
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md)&* **ivec4** - The value of the property parameter.

## Math:: ivec4 getValueIVec4 () const

Returns the current value of the four-component [ivec4](../../../api/library/math/class.ivec4_cpp.md) vector property parameter.
### Return value

Current value of the property parameter.
## void setValueIVec3 ( const Math:: ivec3 & ivec3 )

Sets a new value of the three-component [ivec3](../../../api/library/math/class.ivec3_cpp.md) vector property parameter.
### Arguments

- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md)&* **ivec3** - The value of the property parameter.

## Math:: ivec3 getValueIVec3 () const

Returns the current value of the three-component [ivec3](../../../api/library/math/class.ivec3_cpp.md) vector property parameter.
### Return value

Current value of the property parameter.
## void setValueIVec2 ( const Math:: ivec2 & ivec2 )

Sets a new value of the two-component [ivec2](../../../api/library/math/class.ivec2_cpp.md) vector property parameter.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **ivec2** - The value of the property parameter.

## Math:: ivec2 getValueIVec2 () const

Returns the current value of the two-component [ivec2](../../../api/library/math/class.ivec2_cpp.md) vector property parameter.
### Return value

Current value of the property parameter.
## void setValueDVec4 ( const Math:: dvec4 & dvec4 )

Sets a new value of the four-component [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector property parameter.
### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md)&* **dvec4** - The value of the property parameter.

## Math:: dvec4 getValueDVec4 () const

Returns the current value of the four-component [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector property parameter.
### Return value

Current value of the property parameter.
## void setValueDVec3 ( const Math:: dvec3 & dvec3 )

Sets a new value of the three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector property parameter.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md)&* **dvec3** - The value of the property parameter.

## Math:: dvec3 getValueDVec3 () const

Returns the current value of the three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector property parameter.
### Return value

Current value of the property parameter.
## void setValueDVec2 ( const Math:: dvec2 & dvec2 )

Sets a new value of the two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) vector property parameter.
### Arguments

- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md)&* **dvec2** - The value of the property parameter.

## Math:: dvec2 getValueDVec2 () const

Returns the current value of the two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) vector property parameter.
### Return value

Current value of the property parameter.
## void setValueVec2 ( const Math:: vec2 & vec2 )

Sets a new value of the two-component [vec2](../../../api/library/math/class.vec2_cpp.md) vector property parameter.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **vec2** - The value of the property parameter.

## Math:: vec2 getValueVec2 () const

Returns the current value of the two-component [vec2](../../../api/library/math/class.vec2_cpp.md) vector property parameter.
### Return value

Current value of the property parameter.
---

## bool isChild ( const Ptr < PropertyParameter > & parameter ) const

Returns a value indicating if the specified property parameter is a child of this property parameter.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PropertyParameter](../../../api/library/common/class.propertyparameter_cpp.md)> &* **parameter** - Property parameter to be checked.

### Return value

true if the specified property parameter is a child of this property parameter; otherwise, false.
## int findChild ( const char * name ) const

Returns the number of the child property parameter with the specified name.
### Arguments

- *const char ** **name** - Name of the child property parameter to be found.

### Return value

Number of the child property parameter with the specified name, if it exists; otherwise, -1.
## Ptr < PropertyParameter > getChild ( int num ) const

Returns a child property parameter by its number.
### Arguments

- *int* **num** - Number of the child property parameter in the range from 0 to the [total number of children](#getNumChildren_int) of this property parameter.

### Return value

Child property parameter smart pointer, if it exists; otherwise, nullptr.
## Ptr < PropertyParameter > getChild ( const char * name ) const

Returns a child property parameter by its name.
### Arguments

- *const char ** **name** - Child property parameter name.

### Return value

Child property parameter smart pointer, if it exists; otherwise, nullptr.
## int getChildIndex ( const Ptr < PropertyParameter > & parameter ) const

Returns the index of the specified child property parameter.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PropertyParameter](../../../api/library/common/class.propertyparameter_cpp.md)> &* **parameter** - Child property parameter for which an index is to be found.

### Return value

Index of the child property parameter in the range from 0 to the [total number of children](#getNumChildren_int) of this property parameter, if such a child exists; otherwise, -1.
## void setValue ( int value )

Sets the value of the property parameter using the integer value specified.
### Arguments

- *int* **value** - Integer value to be set as the value of the property parameter.

## void setValue ( float value )

Sets the value of the property parameter using the float value specified.
### Arguments

- *float* **value** - Float value to be set as the value of the property parameter.

## void setValue ( double value )

Sets the value of the property parameter using the double value specified.
### Arguments

- *double* **value** - Double value to be set as the value of the property parameter.

## void setValue ( const char * value )

Sets the value of the property parameter using the string specified.
### Arguments

- *const char ** **value** - String to be set as the value of the property parameter.

## void setValue ( const Math:: vec2 & value )

Sets the value of the property parameter using the two-component [vec2](../../../api/library/math/class.vec2_cpp.md) vector specified.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Two-component float vector to be set as the value of the property parameter.

## void setValue ( const Math:: vec3 & value )

Sets the value of the property parameter using the three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector specified.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Three-component float vector to be set as the value of the property parameter.

## void setValue ( const Math:: vec4 & value )

Sets the value of the property parameter using the four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector specified.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Four-component float vector to be set as the value of the property parameter.

## void setValue ( const Math:: dvec2 & value )

Sets the value of the property parameter using the two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) vector specified.
### Arguments

- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Two-component double vector to be set as the value of the property parameter.

## void setValue ( const Math:: dvec3 & value )

Sets the value of the property parameter using the three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector specified.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Three-component double vector to be set as the value of the property parameter.

## void setValue ( const Math:: dvec4 & value )

Sets the value of the property parameter using the four-component [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector specified.
### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Four-component double vector to be set as the value of the property parameter.

## void setValue ( const Math:: ivec2 & value )

Sets the value of the property parameter using the two-component [ivec2](../../../api/library/math/class.ivec2_cpp.md) vector specified.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Two-component integer vector to be set as the value of the property parameter.

## void setValue ( const Math:: ivec3 & value )

Sets the value of the property parameter using the three-component [ivec3](../../../api/library/math/class.ivec3_cpp.md) vector specified.
### Arguments

- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Three-component integer vector to be set as the value of the property parameter.

## void setValue ( const Math:: ivec4 & value )

Sets the value of the property parameter using the four-component [ivec4](../../../api/library/math/class.ivec4_cpp.md) vector specified.
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Four-component integer vector to be set as the value of the property parameter.

## void setValue ( const UGUID & value )

Sets the value of the property parameter using the [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) value specified.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **value** - [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) value to be set as the value of the property parameter.

## void setValue ( const Ptr < Node > & value )

Sets the value of the property parameter using the [Node](../../../api/library/nodes/class.node_cpp.md) specified.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **value** - [Node](../../../api/library/nodes/class.node_cpp.md) to be set as the value of the property parameter.

## void setValue ( const Ptr < Material > & value )

Sets the value of the property parameter using the [Material](../../../api/library/rendering/class.material_cpp.md) specified.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **value** - [Material](../../../api/library/rendering/class.material_cpp.md) to be set as the value of the property parameter.

## void setValue ( const Ptr < Property > & value )

Sets the value of the property parameter using the [Property](../../../api/library/common/class.property_cpp.md) specified.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **value** - [Property](../../../api/library/common/class.property_cpp.md) to be set as the value of the property parameter.

## bool setValue ( const Variable & value )

Sets the value of the property parameter using the [Variable](../../../api/library/common/class.variable_cpp.md) specified.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **value** - [Variable](../../../api/library/common/class.variable_cpp.md) to be set as the value of the property parameter.

### Return value

true if the property value is set successfully; otherwise, false.
## void setValue ( const Ptr < Curve2d > & value )

Sets the value of the property parameter using the [Curve2d](../../../api/library/common/class.curve2d_cpp.md) value specified.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Curve2d](../../../api/library/common/class.curve2d_cpp.md)> &* **value** - [Curve2d](../../../api/library/common/class.curve2d_cpp.md) value to be set as the value of the property parameter.

## void resetValue ( )


Resets an overridden value of the property parameter.


> **Notice:** Resetting a value of the property parameter affects all its children.


## Variable getValue ( ) const

Returns the current value of the property parameter as a *[Variable](../../../api/library/common/class.variable_cpp.md)*.
### Return value

Value of the property parameter.
## bool hasSliderMinValue ( ) const

Returns a value indicating if the slider parameter has the minimum value specified. The slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cpp.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cpp.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cpp.md#PARAMETER_DOUBLE).
### Return value

true if the slider parameter has the minimum value specified; otherwise, false.
## bool hasSliderMaxValue ( ) const

Returns a value indicating if the slider parameter has the maximum value specified. The slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cpp.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cpp.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cpp.md#PARAMETER_DOUBLE).
### Return value

true if the slider parameter has the maximum value specified; otherwise, false.
## const char * getSwitchItemName ( int item ) const

Returns the name of the [item](../../../code/formats/property_format.md#parameter_items) of the [switch parameter](../../../code/formats/property_format.md#parameter_type).
### Arguments

- *int* **item** - Number of the item of the switch parameter.

### Return value

Name of the item of the switch parameter with the specified number.
## int getSwitchItemValue ( int item ) const

Returns the value of the [item](../../../code/formats/property_format.md#parameter_items) of the [switch parameter](../../../code/formats/property_format.md#parameter_type) with the specified number.
### Arguments

- *int* **item** - Number of the item of the switch parameter.

### Return value

Value of the item of the switch parameter with the specified number.
## const char * getValueFile ( bool fast = 0 ) const

Returns the current value of the [file parameter](../../../code/formats/property_format.md#parameter_type).
### Arguments

- *bool* **fast** - true to use the specified number as an index in users auxiliary parameters cache; otherwise, false.

### Return value


Current file parameter value depending on the [flags](../../../code/formats/property_format.md#parameter_flags) set for the parameter:


```cpp
// flags = "asset"
setValueFile("guid://asset_guid"); 		// getValueFile() -> asset_path
setValueFile("guid://runtime_guid");	// getValueFile() -> asset_path
setValueFile("asset_path");				// getValueFile() -> asset_path
setValueFile("runtime_path");			// getValueFile() -> asset_path

// flags = "runtime" - default
setValueFile("guid://asset_guid"); 		// getValueFile() -> runtime_path
setValueFile("guid://runtime_guid");	// getValueFile() -> runtime_path
setValueFile("asset_path");				// getValueFile() -> runtime_path
setValueFile("runtime_path");			// getValueFile() -> runtime_path

// flags = "abspath"
setValueFile(file_path);				// getValueFile() -> file_path

```


> **Notice:** To get a GUID of the file, use the *[getValueGUID()](#getValueGUID_UGUID)* method.


## const char * getValueFile ( ) const

Returns the current value of the [file parameter](../../../code/formats/property_format.md#parameter_type).
### Return value

Current file parameter value
## bool getFileIsAsset ( ) const

Returns a value indicating if the file parameter stores a reference to an asset file.
### Return value

true if the file parameter stores a reference to an asset file; otherwise, false.
## bool getFileIsRuntime ( ) const

Returns a value indicating if the file parameter stores a reference to a runtime file.
### Return value

true if the file parameter stores a reference to a runtime file; otherwise, false.
## bool getFileIsAbsPath ( ) const

Returns a value indicating if the file parameter stores an absolute file path.
### Return value

true if the file parameter stores an absolute file path; otherwise, false.
## bool isFileExist ( ) const

Returns a value indicating if a file corresponding to the property parameter exists.
### Return value

true if a file corresponding to the property parameter exists; otherwise, false.
## bool saveState ( const Ptr < Stream > & stream ) const

Saves data of the property parameter into a binary stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int_int)* methods:


```cpp
// create a property parameter and set its state
propertyparam1->setValueInt(7);

// save state
BlobPtr blob_state = Blob::create();
propertyparam1->saveState(blob_state);

// change state
propertyparam1->setValueInt(4);

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
propertyparam1->restoreState(blob_state, 0);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream into which the property parameter data will be saved.

### Return value

true if the property parameter data is saved successfully; otherwise, false.
## bool restoreState ( const Ptr < Stream > & stream , int restore_mode = 0 )


Restores the data of the property parameter from a binary stream in the specified mode.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```cpp
// create a property parameter and set its state
propertyparam1->setValueInt(7);

// save state
BlobPtr blob_state = Blob::create();
propertyparam1->saveState(blob_state);

// change state
propertyparam1->setValueInt(4);

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
propertyparam1->restoreState(blob_state, 0);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream in which the saved property parameter data is stored.
- *int* **restore_mode** - Restore mode. One of the [Property::RESTORE_MODE_*](../../../api/library/common/class.property_cpp.md#RESTORE_MODE_MERGE) values. The default value is [Property::RESTORE_MODE_REPLACE](../../../api/library/common/class.property_cpp.md#RESTORE_MODE_REPLACE).

### Return value

true if the property parameter data is restored successfully; otherwise, false.
## bool isValuePropertyInternal ( ) const

Checks if the property parameter [flag](../../../code/formats/property_format.md#parameter_flags) is set to internal (*flags="internal"*). If it is internal, only a property assigned to some node can be assigned to it. If the property parameter is not internal, a property from the Asset Browser can be assigned to it.
### Return value

true if a property parameter's flag is set to *"Internal"*; otherwise, false.
## bool isValueFitFilter ( const Ptr < Node > & value ) const

Checks if the type of the indicated node fits the current property parameter [filter](../../../code/formats/property_format.md#parameter_filter).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **value** - Value to be checked.

### Return value

true, if the node fits the filter; otherwise, false.
## bool isValueFitFilter ( const Ptr < Property > & value ) const

Checks if the indicated property fits the current property parameter [filter](../../../code/formats/property_format.md#parameter_filter).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **value** - Value to be checked.

### Return value

true, if the property fits the filter; otherwise, false.
## bool isValueFitFilter ( const Ptr < Material > & value ) const

Checks if the indicated material fits the current property parameter [filter](../../../code/formats/property_format.md#parameter_filter).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **value** - Value to be checked.

### Return value

true, if the material fits the filter; otherwise, false.
## bool isValueFitFilter ( const UGUID & value ) const

Checks if the indicated GUID fits the current property parameter [filter](../../../code/formats/property_format.md#parameter_filter).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **value** - Value to be checked.

### Return value

true, if the GUID fits the filter; otherwise, false.
## bool isValuePropertyInterface ( ) const


Checks if the property parameter [flag](../../../code/formats/property_format.md#parameter_flags) is defined as an interface type (*flags="interface"*), allowing any component that implements the required interface to be assigned to it.


> **Notice:** You can use interfaces only within the C# Component System. For more information, see the article [C# Interfaces and Abstract Classes.](../../../code/csharp/interfaces_and_abstract_classes.md).

### Return value

true if a property parameter's flag is set to *"interface"*; otherwise, false.
