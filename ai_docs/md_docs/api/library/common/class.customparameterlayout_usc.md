# Unigine::CustomParameterLayout Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *CustomParameterLayout* class represents a global layout (schema) of custom parameters: an ordered list of typed parameters, each having a name, a GUID, a default value, and an editor slider range. Two layouts exist in the engine: the *[surface parameters layout](../../../api/library/rendering/class.render_usc.md#getSurfaceParameters_CustomParameterLayout)*, each parameter of which exists on every surface of every object and on every decal, and the *[material parameters layout](../../../api/library/rendering/class.materials_usc.md#getMaterialParameters_CustomParameterLayout)*, each parameter of which exists on every material. Instances of this class are never created manually: the two layouts are obtained from the corresponding singletons.


Each layout compiles into a GPU-side structure available to shaders and the material graph, with one 4-byte slot per parameter. Owners of parameter values (surfaces, decals, cluster instances, materials) either override a parameter or use the inherited value: material values are inherited down the material hierarchy, surface values fall back to the layout default, and cluster instances add one more override layer on top of their surface. In files, parameters are referred to by GUID (the *puid://<guid>* URI form), so renaming or reordering parameters keeps the stored values attached.


Both layouts can be defined in UnigineEditor (the *Custom Parameters* section of the render settings) or via this API; the schemas are stored in the engine global config. Changing the schema at runtime triggers the *[EventChangedParameters](../../../api/library/rendering/class.render_usc.md#getEventChangedParameters_Event)* event.


## CustomParameterLayout Class

### Members

## int getNumParameters () const

Returns the current number of custom parameters in the layout.
### Return value

Current number of custom parameters in the layout
## int getStructureSize () const

Returns the current size of the GPU-side structure storing the parameter values of a single owner, in bytes. The size includes the engine builtin fields and 4 bytes per custom parameter, rounded up to a multiple of 16 bytes (the minimum size is 16 bytes).
### Return value

Current size of the GPU-side parameters structure, in bytes
---

## int findParameter ( string name )

Searches for a custom parameter by its name.
### Arguments

- *string* **name** - Parameter name.

### Return value

Parameter number, or -1 if a parameter with the given name does not exist.
## int findParameterByGUID ( UGUID guid )

Searches for a custom parameter by its GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Parameter GUID.

### Return value

Parameter number, or -1 if a parameter with the given GUID does not exist.
## UGUID getParameterGUID ( int num )

Returns the GUID of the custom parameter with the given number. Files refer to parameters by GUID rather than by name, so renaming or reordering parameters keeps the stored values attached.
### Arguments

- *int* **num** - Parameter number.

### Return value

Parameter GUID.
## String makeParameterURI ( UGUID guid )

Returns the URI reference for the given parameter GUID, in the *puid://<guid>* format. This URI form is used to refer to the parameter in files (materials, nodes, worlds).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Parameter GUID.

### Return value

Parameter URI string.
## UGUID parseParameterURI ( string uri )

Extracts the parameter GUID from the given URI reference (*puid://<guid>*).
### Arguments

- *string* **uri** - Parameter URI string.

### Return value

Parameter GUID, or an empty GUID if the string is not a valid parameter URI.
## string getParameterName ( int num )

Returns the name of the custom parameter with the given number.
### Arguments

- *int* **num** - Parameter number.

### Return value

Parameter name, or an empty string if the number is out of range.
## int getParameterType ( int num )

Returns the type of the custom parameter with the given number.
### Arguments

- *int* **num** - Parameter number.

### Return value

Parameter type, one of the *TYPE_** values.
## void setParameterName ( int num , string name )

Sets a new name for the custom parameter with the given number. The name must be a valid parameter name (see *[isValidSurfaceMaterialParameterName()](../../../api/library/rendering/class.render_usc.md#isValidSurfaceMaterialParameterName_cstr_int)*); if a parameter with the same name already exists, a numeric suffix is added to the new name automatically. Stored parameter values are bound to the parameter GUID and survive renaming.
### Arguments

- *int* **num** - Parameter number.
- *string* **name** - New parameter name.

## void setParameterType ( int num , int type )

Sets a new type for the custom parameter with the given number. The default, minimum, and maximum values of the parameter are converted to the new type.
### Arguments

- *int* **num** - Parameter number.
- *int* **type** - New parameter type, one of the *TYPE_** values.

## void removeParameter ( int num )

Removes the custom parameter with the given number from the layout. Values stored for this parameter in files can no longer be resolved and are ignored.
### Arguments

- *int* **num** - Parameter number.

## void swapParameters ( int num0 , int num1 )

Swaps two custom parameters in the layout. Parameter values are bound to GUIDs, so reordering does not affect the stored values.
### Arguments

- *int* **num0** - Number of the first parameter.
- *int* **num1** - Number of the second parameter.

## void moveParameter ( int from , int to )

Moves the custom parameter to the given position in the layout. Parameter values are bound to GUIDs, so reordering does not affect the stored values.
### Arguments

- *int* **from** - Number of the parameter to be moved.
- *int* **to** - Target position in the layout.

## int addParameterFloat ( string name , float default_value , UGUID guid = UGUID() )

Adds a new custom parameter of the floating-point type to the layout. The name must be a valid parameter name (see *[isValidSurfaceMaterialParameterName()](../../../api/library/rendering/class.render_usc.md#isValidSurfaceMaterialParameterName_cstr_int)*).
### Arguments

- *string* **name** - Parameter name.
- *float* **default_value** - Default parameter value.
- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Parameter GUID. If an empty GUID is passed, a new one is generated automatically.

### Return value

Number of the added parameter, or -1 if the parameter cannot be added (the name is invalid, or a parameter with the same name or GUID already exists).
## void setParameterDefaultFloat ( int num , float value )

Sets a new default value for the custom parameter with the given number. The default value applies wherever the parameter is not overridden explicitly.
### Arguments

- *int* **num** - Parameter number.
- *float* **value** - New default parameter value.

## float getParameterDefaultFloat ( int num )

Returns the default value of the custom parameter with the given number.
### Arguments

- *int* **num** - Parameter number.

### Return value

Default parameter value, or 0 if the number is out of range.
## void setParameterMinFloat ( int num , float value )

Sets a new minimum value for the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine (values outside the range are not clamped).
### Arguments

- *int* **num** - Parameter number.
- *float* **value** - New minimum parameter value.

## float getParameterMinFloat ( int num )

Returns the minimum value of the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine.
### Arguments

- *int* **num** - Parameter number.

### Return value

Minimum parameter value, or 0 if the number is out of range.
## void setParameterMaxFloat ( int num , float value )

Sets a new maximum value for the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine (values outside the range are not clamped).
### Arguments

- *int* **num** - Parameter number.
- *float* **value** - New maximum parameter value.

## float getParameterMaxFloat ( int num )

Returns the maximum value of the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine.
### Arguments

- *int* **num** - Parameter number.

### Return value

Maximum parameter value, or 0 if the number is out of range.
## int addParameterInt ( string name , int default_value , UGUID guid = UGUID() )

Adds a new custom parameter of the signed integer type to the layout. The name must be a valid parameter name (see *[isValidSurfaceMaterialParameterName()](../../../api/library/rendering/class.render_usc.md#isValidSurfaceMaterialParameterName_cstr_int)*).
### Arguments

- *string* **name** - Parameter name.
- *int* **default_value** - Default parameter value.
- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Parameter GUID. If an empty GUID is passed, a new one is generated automatically.

### Return value

Number of the added parameter, or -1 if the parameter cannot be added (the name is invalid, or a parameter with the same name or GUID already exists).
## void setParameterDefaultInt ( int num , int value )

Sets a new default value for the custom parameter with the given number. The default value applies wherever the parameter is not overridden explicitly.
### Arguments

- *int* **num** - Parameter number.
- *int* **value** - New default parameter value.

## int getParameterDefaultInt ( int num )

Returns the default value of the custom parameter with the given number.
### Arguments

- *int* **num** - Parameter number.

### Return value

Default parameter value, or 0 if the number is out of range.
## void setParameterMinInt ( int num , int value )

Sets a new minimum value for the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine (values outside the range are not clamped).
### Arguments

- *int* **num** - Parameter number.
- *int* **value** - New minimum parameter value.

## int getParameterMinInt ( int num )

Returns the minimum value of the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine.
### Arguments

- *int* **num** - Parameter number.

### Return value

Minimum parameter value, or 0 if the number is out of range.
## void setParameterMaxInt ( int num , int value )

Sets a new maximum value for the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine (values outside the range are not clamped).
### Arguments

- *int* **num** - Parameter number.
- *int* **value** - New maximum parameter value.

## int getParameterMaxInt ( int num )

Returns the maximum value of the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine.
### Arguments

- *int* **num** - Parameter number.

### Return value

Maximum parameter value, or 0 if the number is out of range.
## unsigned int addParameterUInt ( string name , unsigned int default_value , UGUID guid = UGUID() )

Adds a new custom parameter of the unsigned integer type to the layout. The name must be a valid parameter name (see *[isValidSurfaceMaterialParameterName()](../../../api/library/rendering/class.render_usc.md#isValidSurfaceMaterialParameterName_cstr_int)*).
### Arguments

- *string* **name** - Parameter name.
- *unsigned int* **default_value** - Default parameter value.
- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - Parameter GUID. If an empty GUID is passed, a new one is generated automatically.

### Return value

Number of the added parameter, or -1 if the parameter cannot be added (the name is invalid, or a parameter with the same name or GUID already exists).
## void setParameterDefaultUInt ( int num , unsigned int value )

Sets a new default value for the custom parameter with the given number. The default value applies wherever the parameter is not overridden explicitly.
### Arguments

- *int* **num** - Parameter number.
- *unsigned int* **value** - New default parameter value.

## unsigned int getParameterDefaultUInt ( int num )

Returns the default value of the custom parameter with the given number.
### Arguments

- *int* **num** - Parameter number.

### Return value

Default parameter value, or 0 if the number is out of range.
## void setParameterMinUInt ( int num , unsigned int value )

Sets a new minimum value for the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine (values outside the range are not clamped).
### Arguments

- *int* **num** - Parameter number.
- *unsigned int* **value** - New minimum parameter value.

## unsigned int getParameterMinUInt ( int num )

Returns the minimum value of the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine.
### Arguments

- *int* **num** - Parameter number.

### Return value

Minimum parameter value, or 0 if the number is out of range.
## void setParameterMaxUInt ( int num , unsigned int value )

Sets a new maximum value for the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine (values outside the range are not clamped).
### Arguments

- *int* **num** - Parameter number.
- *unsigned int* **value** - New maximum parameter value.

## unsigned int getParameterMaxUInt ( int num )

Returns the maximum value of the custom parameter with the given number. The minimum and maximum define the slider range for the parameter in UnigineEditor and are not enforced by the engine.
### Arguments

- *int* **num** - Parameter number.

### Return value

Maximum parameter value, or 0 if the number is out of range.
