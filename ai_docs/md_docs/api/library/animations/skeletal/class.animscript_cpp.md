# AnimScript Class (CPP)

**Header:** #include <UnigineAnimation.h>


This class provides the code-level interface for interacting with animation graphs at runtime. Animation graphs are visual, node-based assets (`*.agraph` files) created in the editor that define complex animation logic - state machines, blend trees, and transitions.


The AnimScript class serves as the runtime controller for a graph instance: it allows reading and writing graph parameters to drive animation from gameplay logic (e.g., setting a speed parameter to control walk/run blending, or a boolean flag to trigger a jump state). It also provides access to root motion data for physics-driven character movement.


An AnimScript instance is obtained from a [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) node via [getAnimScript()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#getAnimScript_AnimScript).


## AnimScript Class

### Enums

## PARAM_TYPE

Parameter type identifier used to distinguish different value types of animation graph parameters.
| Name | Description |
|---|---|
| **PARAM_TYPE_UNKNOWN** = 0 | Unknown or uninitialized parameter type. |
| **PARAM_TYPE_INT** = 1 | Integer parameter. |
| **PARAM_TYPE_FLOAT** = 2 | Floating-point parameter. |
| **PARAM_TYPE_BOOL** = 3 | Boolean parameter. |
| **PARAM_TYPE_QUAT** = 4 | Quaternion rotation parameter. |
| **PARAM_TYPE_VEC2** = 5 | 2-component float vector parameter. |
| **PARAM_TYPE_VEC3** = 6 | 3-component float vector parameter. |
| **PARAM_TYPE_VEC4** = 7 | 4-component float vector parameter. |
| **PARAM_TYPE_IVEC2** = 8 | 2-component integer vector parameter. |
| **PARAM_TYPE_IVEC3** = 9 | 3-component integer vector parameter. |
| **PARAM_TYPE_IVEC4** = 10 | 4-component integer vector parameter. |
| **PARAM_TYPE_MAT3** = 11 | 3x3 matrix parameter. |
| **PARAM_TYPE_MAT4** = 12 | 4x4 matrix parameter. |
| **PARAM_TYPE_ANIM_ASSET** = 13 | Animation asset reference parameter (GUID). |
| **PARAM_TYPE_TRIGGER** = 14 | Trigger parameter. A trigger is a boolean-like parameter that automatically resets to false after being consumed by the animation graph. |
| **NUM_PARAM_TYPES** = 15 | Total number of parameter types. |

### Members

## isInit () const

Returns the current value indicating whether the animation graph has been initialized and is ready for use.
### Return value

Current the animation graph is initialized.
## getFileGUID () const

Returns the current GUID of the source animation graph asset file.
### Return value

Current animation graph file GUID.
## const char * getFilePath () const

Returns the current file path of the source animation graph asset.
### Return value

Current animation graph file path.
## getNumParams () const

Returns the current total number of parameters defined in the animation graph.
### Return value

Current number of parameters.
## isActiveRootMotion () const

Returns the current value indicating whether root motion extraction is currently active in the animation graph.
### Return value

Current root motion is active.
## Math::Transform Math::Transform getRootMotionDelta () const

Returns the current root motion delta transform accumulated during the last graph update, representing the character's movement and rotation extracted from animation.
### Return value

Current root motion delta transform.
---

## AnimScript::PARAM_TYPE getParamType ( int index ) const

Returns the type of the parameter at the specified index.
### Arguments

- *int* **index** - Index of the parameter.

### Return value

Type of the parameter.
## const char * getParamName ( int index ) const

Returns the name of the parameter at the specified index.
### Arguments

- *int* **index** - Index of the parameter.

### Return value

Name of the parameter.
## void resetParam ( const char * name )

Resets the specified parameter to its default value defined in the animation graph.
### Arguments

- *const char ** **name** - Name of the parameter to reset.

## void setParamInt ( const char * name , int value )

Sets the value of the specified integer parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *int* **value** - Value to set.

## int getParamInt ( const char * name ) const

Returns the value of the specified integer parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamFloat ( const char * name , float value )

Sets the value of the specified floating-point parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *float* **value** - Value to set.

## float getParamFloat ( const char * name ) const

Returns the value of the specified floating-point parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamBool ( const char * name , bool value )

Sets the value of the specified boolean parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *bool* **value** - Value to set.

## bool getParamBool ( const char * name ) const

Returns the value of the specified boolean parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamQuat ( const char * name , const Math:: quat & value )

Sets the value of the specified quaternion parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const  Math::[quat](../../../../api/library/math/class.quat_cpp.md) &* **value** - Value to set.

## Math:: quat getParamQuat ( const char * name ) const

Returns the value of the specified quaternion parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamVec2 ( const char * name , const Math:: vec2 & value )

Sets the value of the specified vec2 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **value** - Value to set.

## Math:: vec2 getParamVec2 ( const char * name ) const

Returns the value of the specified vec2 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamVec3 ( const char * name , const Math:: vec3 & value )

Sets the value of the specified vec3 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **value** - Value to set.

## Math:: vec3 getParamVec3 ( const char * name ) const

Returns the value of the specified vec3 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamVec4 ( const char * name , const Math:: vec4 & value )

Sets the value of the specified vec4 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md) &* **value** - Value to set.

## Math:: vec4 getParamVec4 ( const char * name ) const

Returns the value of the specified vec4 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamIVec2 ( const char * name , const Math:: ivec2 & value )

Sets the value of the specified ivec2 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **value** - Value to set.

## Math:: ivec2 getParamIVec2 ( const char * name ) const

Returns the value of the specified ivec2 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamIVec3 ( const char * name , const Math:: ivec3 & value )

Sets the value of the specified ivec3 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const  Math::[ivec3](../../../../api/library/math/class.ivec3_cpp.md) &* **value** - Value to set.

## Math:: ivec3 getParamIVec3 ( const char * name ) const

Returns the value of the specified ivec3 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamIVec4 ( const char * name , const Math:: ivec4 & value )

Sets the value of the specified ivec4 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const  Math::[ivec4](../../../../api/library/math/class.ivec4_cpp.md) &* **value** - Value to set.

## Math:: ivec4 getParamIVec4 ( const char * name ) const

Returns the value of the specified ivec4 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamMat3 ( const char * name , const Math:: mat3 & value )

Sets the value of the specified mat3 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const  Math::[mat3](../../../../api/library/math/class.mat3_cpp.md) &* **value** - Value to set.

## Math:: mat3 getParamMat3 ( const char * name ) const

Returns the value of the specified mat3 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamMat4 ( const char * name , const Math:: mat4 & value )

Sets the value of the specified mat4 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **value** - Value to set.

## Math:: mat4 getParamMat4 ( const char * name ) const

Returns the value of the specified mat4 parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamAnimAsset ( const char * name , const UGUID & guid )

Sets the animation asset GUID for the specified parameter.
### Arguments

- *const char ** **name** - Name of the parameter.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the animation asset to set.

## UGUID getParamAnimAsset ( const char * name ) const

Returns the animation asset GUID of the specified parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

GUID of the animation asset.
## void setParamTrigger ( const char * name , bool value )

Sets the value of the specified trigger parameter. A trigger automatically resets to false after being consumed by the animation graph.
### Arguments

- *const char ** **name** - Name of the parameter.
- *bool* **value** - Value to set.

## bool getParamTrigger ( const char * name ) const

Returns the current value of the specified trigger parameter.
### Arguments

- *const char ** **name** - Name of the parameter.

### Return value

Current value of the trigger parameter.
## bool isStateMachineActive ( const char * sm_name ) const

Returns a value indicating whether the specified state machine is currently active.
### Arguments

- *const char ** **sm_name** - Name of the state machine.

### Return value

true if the state machine is currently active; otherwise, false.
## const char * getStateMachineCurrentStateName ( const char * sm_name ) const

Returns the name of the current state in the specified state machine.
### Arguments

- *const char ** **sm_name** - Name of the state machine.

### Return value

Name of the current state.
## const char * getStateMachinePreviousStateName ( const char * sm_name ) const

Returns the name of the previous state in the specified state machine.
### Arguments

- *const char ** **sm_name** - Name of the state machine.

### Return value

Name of the previous state.
## bool isStateMachineInTransition ( const char * sm_name ) const

Returns a value indicating whether the specified state machine is currently transitioning between states.
### Arguments

- *const char ** **sm_name** - Name of the state machine.

### Return value

true if the state machine is currently transitioning between states; otherwise, false.
## float getStateMachineTransitionProgress ( const char * sm_name ) const

Returns the current transition progress of the specified state machine.
### Arguments

- *const char ** **sm_name** - Name of the state machine.

### Return value

Transition progress in the [0.0, 1.0] range, where 0.0 is the start and 1.0 is complete.
