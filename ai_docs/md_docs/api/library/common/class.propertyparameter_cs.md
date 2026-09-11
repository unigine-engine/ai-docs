# Unigine::PropertyParameter Class (CS)


This class is used to represent a [property parameter](../../../code/formats/property_format.md#element_parameter).


## PropertyParameter Class

### Properties

## 🔒︎ string StructName

The name of the structure that defines the type of the struct parameter.
## 🔒︎ int ArrayDim

The dimension of the array parameter.
> **Notice:** Multi-dimensional arrays are represented as arrays of arrays, thus, the return value of this method will decrease with each level down the hierarchy.


## 🔒︎ string ArrayTypeName

The type name of elements of the array parameter.
## 🔒︎ int ArrayType

The type of elements of the array parameter.
## int ArraySize

The size of the array parameter.
## string ValueFile

The
value of the [file parameter](../../../code/formats/property_format.md#parameter_type). If the property is not [editable](../../../api/library/common/class.property_cs.md#isEditable_int), the value won't be updated.


The value stored in the file parameter depends on the [flags](../../../code/formats/property_format.md#parameter_flags) set for the parameter.


## 🔒︎ int MaskType

The type of elements of the mask parameter.
## 🔒︎ int SwitchNumItems

The
## 🔒︎ int SliderMaxExpand

The value indicating if the maximum value of the slider parameter can be [decreased](../../../code/formats/property_format.md#parameter_flags). Slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cs.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cs.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cs.md#PARAMETER_INT).
## 🔒︎ int SliderMinExpand

The value indicating if the minimum value of the slider parameter can be [decreased](../../../code/formats/property_format.md#parameter_flags). Slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cs.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cs.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cs.md#PARAMETER_INT).
## 🔒︎ int SliderLog10

The value indicating if the slider parameter uses a [logarithmic scale](../../../code/formats/property_format.md#parameter_flags) (with the base ten). The slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cs.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cs.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cs.md#PARAMETER_DOUBLE).
## 🔒︎ double DoubleMaxValue

The maximum double value of the property parameter.
## 🔒︎ double DoubleMinValue

The minimum double value of the property parameter.
## 🔒︎ float FloatMaxValue

The maximum float value of the property parameter.
## 🔒︎ float FloatMinValue

The minimum float value of the property parameter.
## 🔒︎ int IntMaxValue

The maximum integer value of the property parameter.
## 🔒︎ int IntMinValue

The minimum integer value of the property parameter.
## UGUID ValueGUID

The value of the [UGUID](../../../api/library/filesystem/class.uguid_cs.md) property parameter.
## int ValueMask

The value of the [mask parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_MASK*](../../../api/library/common/class.property_cs.md#PARAMETER_MASK) variable isn't set for the parameter, or the property is not [editable](../../../api/library/common/class.property_cs.md#isEditable_int), the value won't be updated.
## int ValueSwitch

The value of the [switch parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_SWITCH*](../../../api/library/common/class.property_cs.md#PARAMETER_SWITCH) variable isn't set for the parameter, the function will return 0.
## bool ValueToggle

The value of the [toggle parameter](../../../code/formats/property_format.md#parameter_type). If the [*PARAMETER_TOGGLE*](../../../api/library/common/class.property_cs.md#PARAMETER_TOGGLE) variable isn't set for the parameter, the function will return 0.
## int ValueNodeID

The value of the node ID property parameter.
## Node ValueNode

The value of the *[Node](../../../api/library/nodes/class.node_cs.md)* property parameter.
## Material ValueMaterial

The value of the *[Material](../../../api/library/rendering/class.material_cs.md)* property parameter.
## Property ValueProperty

The value of the *[Property](../../../api/library/common/class.property_cs.md)*-type property parameter.
## vec4 ValueVec4

The value of the four-component [vec4](../../../api/library/math/class.vec4_cs.md) vector property parameter
## vec3 ValueVec3

The value of the three-component [vec3](../../../api/library/math/class.vec3_cs.md) vector property parameter
## string ValueString

The value of the string property parameter.
## vec4 ValueColor

The value of the four-component [vec4](../../../api/library/math/class.vec4_cs.md) color vector (R, G, B, A) property parameter.
## double ValueDouble

The value of the double property parameter.
## float ValueFloat

The value of the float property parameter.
## int ValueInt

The value of the integer property parameter.
## 🔒︎ Curve2d ValueCurve2dOverride

The [Curve2d](../../../api/library/common/class.curve2d_cs.md) instance for the data stored in the specified property parameter overriding the default one.
This method enables you to set individual curves, adjusting the value of the resulting property.


> **Notice:** Modifications made to the curve shall not propagate to the parent and sibling properties.


## Curve2d ValueCurve2d

The [Curve2d](../../../api/library/common/class.curve2d_cs.md) value of the property parameter.
## 🔒︎ bool IsCurve2d

The value indicating if the property parameter is a 2d curve.
## 🔒︎ bool IsStruct

The value indicating if the property parameter is a structure.
## 🔒︎ bool IsArray

The value indicating if the property parameter is an array.
## 🔒︎ bool IsNode

The value indicating if the property parameter is a node.
## 🔒︎ bool IsMaterial

The value indicating if the property parameter is a material.
## 🔒︎ bool IsProperty

The value indicating if the property parameter is a property.
## 🔒︎ bool IsFile

The value indicating if the property parameter is a file.
## 🔒︎ bool IsMask

The value indicating if the property parameter is a mask.
## 🔒︎ bool IsIVec4

The value indicating if the property parameter is a vector of 4 integer components.
## 🔒︎ bool IsIVec3

The value indicating if the property parameter is a vector of 3 integer components.
## 🔒︎ bool IsIVec2

The value indicating if the property parameter is a vector of 2 integer components.
## 🔒︎ bool IsDVec4

The value indicating if the property parameter is a vector of 4 double components.
## 🔒︎ bool IsDVec3

The value indicating if the property parameter is a vector of 3 double components.
## 🔒︎ bool IsDVec2

The value indicating if the property parameter is a vector of 2 double components.
## 🔒︎ bool IsVec4

The value indicating if the property parameter is a vector of 4 float components.
## 🔒︎ bool IsVec3

The value indicating if the property parameter is a vector of 3 float components.
## 🔒︎ bool IsVec2

The value indicating if the property parameter is a vector of 2 float components.
## 🔒︎ bool IsColor

The value indicating if the property parameter is a color.
## 🔒︎ bool IsString

The value indicating if the property parameter is a string.
## 🔒︎ bool IsSwitch

The value indicating if the property parameter is a switch.
## 🔒︎ bool IsToggle

The value indicating if the property parameter is a toggle.
## 🔒︎ bool IsDouble

The value indicating if the property parameter is a *double*.
## 🔒︎ bool IsFloat

The value indicating if the property parameter is a *float*.
## 🔒︎ bool IsInt

The value indicating if the property parameter is an integer.
## 🔒︎ string Filter

The filter string associated with the property parameter.
This string specifies a filter for *File, Material* or *Property* parameter values thet will be used in the UnigineEditor. for example, you can specify *".xml|.node|.txt"* to filter certain types of assets, or specify a base material to filter out materials, that cannot be used in a particular case (e.g. to avoid an attempt of assigning a post material to a mesh).


> **Notice:** This attribute is available only for [file](../../../api/library/common/class.property_cs.md#PARAMETER_FILE), [material](../../../api/library/common/class.property_cs.md#PARAMETER_MATERIAL) and [property](../../../api/library/common/class.property_cs.md#PARAMETER_PROPERTY) parameter types.


## 🔒︎ string Group

The name of the group to which the property parameter belongs.
## 🔒︎ string Tooltip

The tooltip for the property parameter. This title is displayed in the UnigineEditor UI.
## 🔒︎ string Title

The title of the property parameter. This title is displayed in the UnigineEditor UI.
## 🔒︎ string Name

The name of the property parameter.
## 🔒︎ int Type

The [type](../../../code/formats/property_format.md#parameter_type) identifier of the property parameter.
You can get the name of the parameter type using the *[Property.ParameterNameByType()](../../../api/library/common/class.property_cs.md#parameterNameByType_int_cstr)* method:


```csharp
Log.Message("Parameter type: {0}\n", my_property.ParameterNameByType(my_prop_param.Type));
```


## 🔒︎ string TypeName

The name of the property parameter type.
## 🔒︎ bool IsOverridden

The value indicating if the property parameter is overridden. For all parameter types except for *int* and *string* **the value will be considered overridden even in case of assigning the initial (default) value to it**. To check whether the default value for the parameter has actually changed, we recommend using comparison operators and methods, as in this respect *IsOverridden* will only help you with *int* and *string*.
## 🔒︎ bool IsInherited

The value indicating if the property parameter is inherited from a parent.
## 🔒︎ bool IsHidden

The value indicating if the property parameter is [hidden](../../../code/formats/property_format.md#parameter_hidden).
## 🔒︎ bool IsExist

The value indicating if the property parameter is an existing one.
## 🔒︎ int NumChildren

The total number of children of the property parameter.
## 🔒︎ PropertyParameter Parent

The parent property parameter, if it exists.
## 🔒︎ UGUID PropertyGUID

The [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property that owns the parameter.
## 🔒︎ Property Property

The property that owns the parameter.
## 🔒︎ int ID

The ID of the property parameter.
## int SwitchItem

The number of the [item](../../../code/formats/property_format.md#parameter_items) of the [switch parameter](../../../code/formats/property_format.md#parameter_type).
Suppose we have a property switch parameter declared as follows:


```xml
<parameter items="red=-1,green,blue=5,yellow"/>
```


> **Notice:** Spaces in the *items* attribute declaration are taken into account. Thus, **items="red=-1, green"** shall produce 2 items: **"red"** and **" green"**


After loading we'll have switch items with the following values: *red = -1, green = 0, blue = 5, yellow = 6*.


```csharp
PropertyParameter.SetValue(5); // "blue" shall be selected in the corresponding combobox in the UnigineEditor
PropertyParameter.SetSwitchItem(3); // "yellow" shall be selected in the corresponding combobox in the UnigineEditor (as it is the 3-rd item, starting from 0).

// If "green" item is selected in the UnigineEditor:
PropertyParameter.GetValueInt(); // returns 0, as "green" corresponds to the value of 0.
PropertyParameter.GetSwitchItem() // returns 1, as "green" is the 1-st element in the combobox (starting from 0).

```


## ivec4 ValueIVec4

The value of the four-component [ivec4](../../../api/library/math/class.ivec4_cs.md) vector property parameter.
## ivec3 ValueIVec3

The value of the three-component [ivec3](../../../api/library/math/class.ivec3_cs.md) vector property parameter.
## ivec2 ValueIVec2

The value of the two-component [ivec2](../../../api/library/math/class.ivec2_cs.md) vector property parameter.
## dvec4 ValueDVec4

The value of the four-component [dvec4](../../../api/library/math/class.dvec4_cs.md) vector property parameter.
## dvec3 ValueDVec3

The value of the three-component [dvec3](../../../api/library/math/class.dvec3_cs.md) vector property parameter.
## dvec2 ValueDVec2

The value of the two-component [dvec2](../../../api/library/math/class.dvec2_cs.md) vector property parameter.
## vec2 ValueVec2

The value of the two-component [vec2](../../../api/library/math/class.vec2_cs.md) vector property parameter.
### Members

---

## bool IsChild ( PropertyParameter parameter )

Returns a value indicating if the specified property parameter is a child of this property parameter.
### Arguments

- *[PropertyParameter](../../../api/library/common/class.propertyparameter_cs.md)* **parameter** - Property parameter to be checked.

### Return value

true if the specified property parameter is a child of this property parameter; otherwise, false.
## int FindChild ( string name )

Returns the number of the child property parameter with the specified name.
### Arguments

- *string* **name** - Name of the child property parameter to be found.

### Return value

Number of the child property parameter with the specified name, if it exists; otherwise, -1.
## PropertyParameter GetChild ( int num )

Returns a child property parameter by its number.
### Arguments

- *int* **num** - Number of the child property parameter in the range from 0 to the [total number of children](#getNumChildren_int) of this property parameter.

### Return value

Child property parameter instance, if it exists; otherwise, nullptr.
## PropertyParameter GetChild ( string name )

Returns a child property parameter by its name.
### Arguments

- *string* **name** - Child property parameter name.

### Return value

Child property parameter instance, if it exists; otherwise, nullptr.
## int GetChildIndex ( PropertyParameter parameter )

Returns the index of the specified child property parameter.
### Arguments

- *[PropertyParameter](../../../api/library/common/class.propertyparameter_cs.md)* **parameter** - Child property parameter for which an index is to be found.

### Return value

Index of the child property parameter in the range from 0 to the [total number of children](#getNumChildren_int) of this property parameter, if such a child exists; otherwise, -1.
## void SetValue ( int value )

Sets the value of the property parameter using the integer value specified.
### Arguments

- *int* **value** - Integer value to be set as the value of the property parameter.

## void SetValue ( float value )

Sets the value of the property parameter using the float value specified.
### Arguments

- *float* **value** - Float value to be set as the value of the property parameter.

## void SetValue ( double value )

Sets the value of the property parameter using the double value specified.
### Arguments

- *double* **value** - Double value to be set as the value of the property parameter.

## void SetValue ( string value )

Sets the value of the property parameter using the string specified.
### Arguments

- *string* **value** - String to be set as the value of the property parameter.

## void SetValue ( vec2 value )

Sets the value of the property parameter using the two-component [vec2](../../../api/library/math/class.vec2_cs.md) vector specified.
### Arguments

- *vec2* **value** - Two-component float vector to be set as the value of the property parameter.

## void SetValue ( vec3 value )

Sets the value of the property parameter using the three-component [vec3](../../../api/library/math/class.vec3_cs.md) vector specified.
### Arguments

- *vec3* **value** - Three-component float vector to be set as the value of the property parameter.

## void SetValue ( vec4 value )

Sets the value of the property parameter using the four-component [vec4](../../../api/library/math/class.vec4_cs.md) vector specified.
### Arguments

- *vec4* **value** - Four-component float vector to be set as the value of the property parameter.

## void SetValue ( dvec2 value )

Sets the value of the property parameter using the two-component [dvec2](../../../api/library/math/class.dvec2_cs.md) vector specified.
### Arguments

- *dvec2* **value** - Two-component double vector to be set as the value of the property parameter.

## void SetValue ( dvec3 value )

Sets the value of the property parameter using the three-component [dvec3](../../../api/library/math/class.dvec3_cs.md) vector specified.
### Arguments

- *dvec3* **value** - Three-component double vector to be set as the value of the property parameter.

## void SetValue ( dvec4 value )

Sets the value of the property parameter using the four-component [dvec4](../../../api/library/math/class.dvec4_cs.md) vector specified.
### Arguments

- *dvec4* **value** - Four-component double vector to be set as the value of the property parameter.

## void SetValue ( ivec2 value )

Sets the value of the property parameter using the two-component [ivec2](../../../api/library/math/class.ivec2_cs.md) vector specified.
### Arguments

- *ivec2* **value** - Two-component integer vector to be set as the value of the property parameter.

## void SetValue ( ivec3 value )

Sets the value of the property parameter using the three-component [ivec3](../../../api/library/math/class.ivec3_cs.md) vector specified.
### Arguments

- *ivec3* **value** - Three-component integer vector to be set as the value of the property parameter.

## void SetValue ( ivec4 value )

Sets the value of the property parameter using the four-component [ivec4](../../../api/library/math/class.ivec4_cs.md) vector specified.
### Arguments

- *ivec4* **value** - Four-component integer vector to be set as the value of the property parameter.

## void SetValue ( UGUID value )

Sets the value of the property parameter using the [UGUID](../../../api/library/filesystem/class.uguid_cs.md) value specified.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **value** - [UGUID](../../../api/library/filesystem/class.uguid_cs.md) value to be set as the value of the property parameter.

## void SetValue ( Node value )

Sets the value of the property parameter using the [Node](../../../api/library/nodes/class.node_cs.md) specified.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **value** - [Node](../../../api/library/nodes/class.node_cs.md) to be set as the value of the property parameter.

## void SetValue ( Material value )

Sets the value of the property parameter using the [Material](../../../api/library/rendering/class.material_cs.md) specified.
### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **value** - [Material](../../../api/library/rendering/class.material_cs.md) to be set as the value of the property parameter.

## void SetValue ( Property value )

Sets the value of the property parameter using the [Property](../../../api/library/common/class.property_cs.md) specified.
### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **value** - [Property](../../../api/library/common/class.property_cs.md) to be set as the value of the property parameter.

## bool SetValue ( Variable value )

Sets the value of the property parameter using the [Variable](../../../api/library/common/class.variable_cs.md) specified.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **value** - [Variable](../../../api/library/common/class.variable_cs.md) to be set as the value of the property parameter.

### Return value

true if the property value is set successfully; otherwise, false.
## void SetValue ( Curve2d value )

Sets the value of the property parameter using the [Curve2d](../../../api/library/common/class.curve2d_cs.md) value specified.
### Arguments

- *[Curve2d](../../../api/library/common/class.curve2d_cs.md)* **value** - [Curve2d](../../../api/library/common/class.curve2d_cs.md) value to be set as the value of the property parameter.

## void ResetValue ( )


Resets an overridden value of the property parameter.


> **Notice:** Resetting a value of the property parameter affects all its children.


## Variable GetValue ( )

Returns the current value of the property parameter as a *[Variable](../../../api/library/common/class.variable_cs.md)*.
### Return value

Value of the property parameter.
## bool HasSliderMinValue ( )

Returns a value indicating if the slider parameter has the minimum value specified. The slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cs.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cs.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cs.md#PARAMETER_DOUBLE).
### Return value

true if the slider parameter has the minimum value specified; otherwise, false.
## bool HasSliderMaxValue ( )

Returns a value indicating if the slider parameter has the maximum value specified. The slider parameter is a parameter of one of the following types: [PARAMETER_INT](../../../api/library/common/class.property_cs.md#PARAMETER_INT), [PARAMETER_FLOAT](../../../api/library/common/class.property_cs.md#PARAMETER_FLOAT), [PARAMETER_DOUBLE](../../../api/library/common/class.property_cs.md#PARAMETER_DOUBLE).
### Return value

true if the slider parameter has the maximum value specified; otherwise, false.
## string GetSwitchItemName ( int item )

Returns the name of the [item](../../../code/formats/property_format.md#parameter_items) of the [switch parameter](../../../code/formats/property_format.md#parameter_type).
### Arguments

- *int* **item** - Number of the item of the switch parameter.

### Return value

Name of the item of the switch parameter with the specified number.
## int GetSwitchItemValue ( int item )

Returns the value of the [item](../../../code/formats/property_format.md#parameter_items) of the [switch parameter](../../../code/formats/property_format.md#parameter_type) with the specified number.
### Arguments

- *int* **item** - Number of the item of the switch parameter.

### Return value

Value of the item of the switch parameter with the specified number.
## string GetValueFile ( bool fast = 0 )

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


## bool GetFileIsAsset ( )

Returns a value indicating if the file parameter stores a reference to an asset file.
### Return value

true if the file parameter stores a reference to an asset file; otherwise, false.
## bool GetFileIsRuntime ( )

Returns a value indicating if the file parameter stores a reference to a runtime file.
### Return value

true if the file parameter stores a reference to a runtime file; otherwise, false.
## bool GetFileIsAbsPath ( )

Returns a value indicating if the file parameter stores an absolute file path.
### Return value

true if the file parameter stores an absolute file path; otherwise, false.
## bool IsFileExist ( )

Returns a value indicating if a file corresponding to the property parameter exists.
### Return value

true if a file corresponding to the property parameter exists; otherwise, false.
## bool SaveState ( Stream stream )

Saves data of the property parameter into a binary stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int_int)* methods:


```csharp
// create a property parameter and set its state
propertyparam1.ValueInt = 7;

// save state
Blob blob_state = new Blob();
propertyparam1.SaveState(blob_state);

// change state
propertyparam1.ValueInt = 4;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
propertyparam1.RestoreState(blob_state, 0);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream into which the property parameter data will be saved.

### Return value

true if the property parameter data is saved successfully; otherwise, false.
## bool RestoreState ( Stream stream , int restore_mode = 0 )


Restores the data of the property parameter from a binary stream in the specified mode.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```csharp
// create a property parameter and set its state
propertyparam1.ValueInt = 7;

// save state
Blob blob_state = new Blob();
propertyparam1.SaveState(blob_state);

// change state
propertyparam1.ValueInt = 4;

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
propertyparam1.RestoreState(blob_state, 0);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream in which the saved property parameter data is stored.
- *int* **restore_mode** - Restore mode. One of the [Property.RESTORE_MODE_*](../../../api/library/common/class.property_cs.md#RESTORE_MODE_MERGE) values. The default value is [Property.RESTORE_MODE_REPLACE](../../../api/library/common/class.property_cs.md#RESTORE_MODE_REPLACE).

### Return value

true if the property parameter data is restored successfully; otherwise, false.
## bool IsValuePropertyInternal ( )

Checks if the property parameter [flag](../../../code/formats/property_format.md#parameter_flags) is set to internal (*flags="internal"*). If it is internal, only a property assigned to some node can be assigned to it. If the property parameter is not internal, a property from the Asset Browser can be assigned to it.
### Return value

true if a property parameter's flag is set to *"Internal"*; otherwise, false.
## bool IsValueFitFilter ( Node value )

Checks if the type of the indicated node fits the current property parameter [filter](../../../code/formats/property_format.md#parameter_filter).
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **value** - Value to be checked.

### Return value

true, if the node fits the filter; otherwise, false.
## bool IsValueFitFilter ( Property value )

Checks if the indicated property fits the current property parameter [filter](../../../code/formats/property_format.md#parameter_filter).
### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **value** - Value to be checked.

### Return value

true, if the property fits the filter; otherwise, false.
## bool IsValueFitFilter ( Material value )

Checks if the indicated material fits the current property parameter [filter](../../../code/formats/property_format.md#parameter_filter).
### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **value** - Value to be checked.

### Return value

true, if the material fits the filter; otherwise, false.
## bool IsValueFitFilter ( UGUID value )

Checks if the indicated GUID fits the current property parameter [filter](../../../code/formats/property_format.md#parameter_filter).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **value** - Value to be checked.

### Return value

true, if the GUID fits the filter; otherwise, false.
## bool IsValuePropertyInterface ( )


Checks if the property parameter [flag](../../../code/formats/property_format.md#parameter_flags) is defined as an interface type (*flags="interface"*), allowing any component that implements the required interface to be assigned to it.


> **Notice:** You can use interfaces only within the C# Component System. For more information, see the article [C# Interfaces and Abstract Classes.](../../../code/csharp/interfaces_and_abstract_classes.md).

### Return value

true if a property parameter's flag is set to *"interface"*; otherwise, false.
