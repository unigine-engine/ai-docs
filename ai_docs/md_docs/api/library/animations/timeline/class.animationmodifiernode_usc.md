# Unigine::AnimationModifierNode Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationModifier


## AnimationModifierNode Class

### Members

## Node getDefaultValue () const

Returns the current default value of all modifier elements.
### Return value

Current default value of all modifier elements.
## void setCurveID ( AnimationCurveInt id )

Sets a new identifier of the animation curve.
### Arguments

- *[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_usc.md)* **id** - The identifier of the animation curve.

## AnimationCurveInt getCurveID () const

Returns the current identifier of the animation curve.
### Return value

Current identifier of the animation curve.
---

## AnimationModifierNode ( int param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.

## AnimationModifierNode ( int param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierNode ( int param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *int* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## AnimationModifierNode ( string param )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.

## AnimationModifierNode ( string param , int param_index )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *int* **param_index** - Index of the parameter.

## AnimationModifierNode ( string param , string param_name )

Creates the animation modifier to animate the specified parameter.
### Arguments

- *string* **param** - Parameter to be animated by the modifier.
- *string* **param_name** - Name of the parameter.

## void copy ( AnimationModifierNode modifier )

Copies all data from the specified source animation modifier.
### Arguments

- *[AnimationModifierNode](../../../../api/library/animations/timeline/class.animationmodifiernode_usc.md)* **modifier** - Source animation modifier.

## Node getValueByTime ( float time )

Returns the value of the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The modifier value at the specified time.
## Node getValueByNormalizedTime ( float normalized_time )

Returns the normalized value of the modifier at the specified time.
### Arguments

- *float* **normalized_time** - The normalized time value.

### Return value

The modifier value at the specified time.
## void addValue ( float time , int node_id )

Adds the node to the modifier at the specified time.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *int* **node_id** - Identifier of the node.
