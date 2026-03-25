# AnimScript Class (CS)


This class provides the code-level interface for interacting with animation graphs at runtime. Animation graphs are visual, node-based assets (`*.agraph` files) created in the editor that define complex animation logic - state machines, blend trees, and transitions.


The AnimScript class serves as the runtime controller for a graph instance: it allows reading and writing graph parameters to drive animation from gameplay logic (e.g., setting a speed parameter to control walk/run blending, or a boolean flag to trigger a jump state). It also provides access to root motion data for physics-driven character movement.


An AnimScript instance is obtained from a [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cs.md) node via [getAnimScript()](../../../../api/library/nodes/class.nodeskeletonpose_cs.md#getAnimScript_AnimScript).


## AnimScript Class

### Enums

## PARAM_TYPE

Parameter type identifier used to distinguish different value types of animation graph parameters.
| Name | Description |
|---|---|
| **UNKNOWN** = 0 | Unknown or uninitialized parameter type. |
| **INT** = 1 | Integer parameter. |
| **FLOAT** = 2 | Floating-point parameter. |
| **BOOL** = 3 | Boolean parameter. |
| **QUAT** = 4 | Quaternion rotation parameter. |
| **VEC2** = 5 | 2-component float vector parameter. |
| **VEC3** = 6 | 3-component float vector parameter. |
| **VEC4** = 7 | 4-component float vector parameter. |
| **IVEC2** = 8 | 2-component integer vector parameter. |
| **IVEC3** = 9 | 3-component integer vector parameter. |
| **IVEC4** = 10 | 4-component integer vector parameter. |
| **MAT3** = 11 | 3x3 matrix parameter. |
| **MAT4** = 12 | 4x4 matrix parameter. |
| **ANIM_ASSET** = 13 | Animation asset reference parameter (GUID). |
| **TRIGGER** = 14 | Trigger parameter. A trigger is a boolean-like parameter that automatically resets to false after being consumed by the animation graph. |
| **NUM_PARAM_TYPES** = 15 | Total number of parameter types. |

### Properties

## 🔒︎ bool IsInit

The value indicating whether the animation graph has been initialized and is ready for use.
## 🔒︎ UGUID FileGUID

The GUID of the source animation graph asset file.
## 🔒︎ string FilePath

The file path of the source animation graph asset.
## 🔒︎ int NumParams

The total number of parameters defined in the animation graph.
## 🔒︎ bool IsActiveRootMotion

The value indicating whether root motion extraction is currently active in the animation graph.
## 🔒︎ FloatTransform RootMotionDelta

The root motion delta transform accumulated during the last graph update, representing the character's movement and rotation extracted from animation.
### Members

---

## AnimScript.PARAM_TYPE GetParamType ( int index )

Returns the type of the parameter at the specified index.
### Arguments

- *int* **index** - Index of the parameter.

### Return value

Type of the parameter.
## string GetParamName ( int index )

Returns the name of the parameter at the specified index.
### Arguments

- *int* **index** - Index of the parameter.

### Return value

Name of the parameter.
## void ResetParam ( string name )

Resets the specified parameter to its default value defined in the animation graph.
### Arguments

- *string* **name** - Name of the parameter to reset.

## void SetParamInt ( string name , int value )

Sets the value of the specified integer parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *int* **value** - Value to set.

## int GetParamInt ( string name )

Returns the value of the specified integer parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamFloat ( string name , float value )

Sets the value of the specified floating-point parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *float* **value** - Value to set.

## float GetParamFloat ( string name )

Returns the value of the specified floating-point parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamBool ( string name , bool value )

Sets the value of the specified boolean parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *bool* **value** - Value to set.

## bool GetParamBool ( string name )

Returns the value of the specified boolean parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamQuat ( string name , quat value )

Sets the value of the specified quaternion parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *quat* **value** - Value to set.

## quat GetParamQuat ( string name )

Returns the value of the specified quaternion parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamVec2 ( string name , vec2 value )

Sets the value of the specified vec2 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *vec2* **value** - Value to set.

## vec2 GetParamVec2 ( string name )

Returns the value of the specified vec2 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamVec3 ( string name , vec3 value )

Sets the value of the specified vec3 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *vec3* **value** - Value to set.

## vec3 GetParamVec3 ( string name )

Returns the value of the specified vec3 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamVec4 ( string name , vec4 value )

Sets the value of the specified vec4 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *vec4* **value** - Value to set.

## vec4 GetParamVec4 ( string name )

Returns the value of the specified vec4 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamIVec2 ( string name , ivec2 value )

Sets the value of the specified ivec2 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *ivec2* **value** - Value to set.

## ivec2 GetParamIVec2 ( string name )

Returns the value of the specified ivec2 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamIVec3 ( string name , ivec3 value )

Sets the value of the specified ivec3 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *ivec3* **value** - Value to set.

## ivec3 GetParamIVec3 ( string name )

Returns the value of the specified ivec3 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamIVec4 ( string name , ivec4 value )

Sets the value of the specified ivec4 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *ivec4* **value** - Value to set.

## ivec4 GetParamIVec4 ( string name )

Returns the value of the specified ivec4 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamMat3 ( string name , mat3 value )

Sets the value of the specified mat3 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *mat3* **value** - Value to set.

## mat3 GetParamMat3 ( string name )

Returns the value of the specified mat3 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamMat4 ( string name , mat4 value )

Sets the value of the specified mat4 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *mat4* **value** - Value to set.

## mat4 GetParamMat4 ( string name )

Returns the value of the specified mat4 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void SetParamAnimAsset ( string name , UGUID guid )

Sets the animation asset GUID for the specified parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the animation asset to set.

## UGUID GetParamAnimAsset ( string name )

Returns the animation asset GUID of the specified parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

GUID of the animation asset.
## void SetParamTrigger ( string name , bool value )

Sets the value of the specified trigger parameter. A trigger automatically resets to false after being consumed by the animation graph.
### Arguments

- *string* **name** - Name of the parameter.
- *bool* **value** - Value to set.

## bool GetParamTrigger ( string name )

Returns the current value of the specified trigger parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the trigger parameter.
## bool IsStateMachineActive ( string sm_name )

Returns a value indicating whether the specified state machine is currently active.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

true if the state machine is currently active; otherwise, false.
## string GetStateMachineCurrentStateName ( string sm_name )

Returns the name of the current state in the specified state machine.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

Name of the current state.
## string GetStateMachinePreviousStateName ( string sm_name )

Returns the name of the previous state in the specified state machine.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

Name of the previous state.
## bool IsStateMachineInTransition ( string sm_name )

Returns a value indicating whether the specified state machine is currently transitioning between states.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

true if the state machine is currently transitioning between states; otherwise, false.
## float GetStateMachineTransitionProgress ( string sm_name )

Returns the current transition progress of the specified state machine.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

Transition progress in the [0.0, 1.0] range, where 0.0 is the start and 1.0 is complete.
