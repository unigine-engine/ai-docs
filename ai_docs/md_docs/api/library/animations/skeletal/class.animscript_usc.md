# AnimScript Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class provides the code-level interface for interacting with animation graphs at runtime. Animation graphs are visual, node-based assets (`*.agraph` files) created in the editor that define complex animation logic - state machines, blend trees, and transitions.


The AnimScript class serves as the runtime controller for a graph instance: it allows reading and writing graph parameters to drive animation from gameplay logic (e.g., setting a speed parameter to control walk/run blending, or a boolean flag to trigger a jump state). It also provides access to root motion data for physics-driven character movement.


An AnimScript instance is obtained from a [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_usc.md) node via [getAnimScript()](../../../../api/library/nodes/class.nodeskeletonpose_usc.md#getAnimScript_AnimScript).


## AnimScript Class

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
## getRootMotionDelta () const

Returns the current root motion delta transform accumulated during the last graph update, representing the character's movement and rotation extracted from animation.
### Return value

Current root motion delta transform.
---

## int getParamType ( int index )

Returns the type of the parameter at the specified index.
### Arguments

- *int* **index** - Index of the parameter.

### Return value

Type of the parameter.
## string getParamName ( int index )

Returns the name of the parameter at the specified index.
### Arguments

- *int* **index** - Index of the parameter.

### Return value

Name of the parameter.
## void resetParam ( string name )

Resets the specified parameter to its default value defined in the animation graph.
### Arguments

- *string* **name** - Name of the parameter to reset.

## void setParamInt ( string name , int value )

Sets the value of the specified integer parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *int* **value** - Value to set.

## int getParamInt ( string name )

Returns the value of the specified integer parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamFloat ( string name , float value )

Sets the value of the specified floating-point parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *float* **value** - Value to set.

## float getParamFloat ( string name )

Returns the value of the specified floating-point parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamBool ( string name , int value )

Sets the value of the specified boolean parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *int* **value** - Value to set.

## int getParamBool ( string name )

Returns the value of the specified boolean parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamQuat ( string name , quat value )

Sets the value of the specified quaternion parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *quat* **value** - Value to set.

## quat getParamQuat ( string name )

Returns the value of the specified quaternion parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamVec2 ( string name , vec2 value )

Sets the value of the specified vec2 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *vec2* **value** - Value to set.

## vec2 getParamVec2 ( string name )

Returns the value of the specified vec2 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamVec3 ( string name , vec3 value )

Sets the value of the specified vec3 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *vec3* **value** - Value to set.

## vec3 getParamVec3 ( string name )

Returns the value of the specified vec3 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamVec4 ( string name , vec4 value )

Sets the value of the specified vec4 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *vec4* **value** - Value to set.

## vec4 getParamVec4 ( string name )

Returns the value of the specified vec4 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamIVec2 ( string name , ivec2 value )

Sets the value of the specified ivec2 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *ivec2* **value** - Value to set.

## ivec2 getParamIVec2 ( string name )

Returns the value of the specified ivec2 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamIVec3 ( string name , ivec3 value )

Sets the value of the specified ivec3 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *ivec3* **value** - Value to set.

## ivec3 getParamIVec3 ( string name )

Returns the value of the specified ivec3 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamIVec4 ( string name , ivec4 value )

Sets the value of the specified ivec4 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *ivec4* **value** - Value to set.

## ivec4 getParamIVec4 ( string name )

Returns the value of the specified ivec4 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamMat3 ( string name , mat3 value )

Sets the value of the specified mat3 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *mat3* **value** - Value to set.

## mat3 getParamMat3 ( string name )

Returns the value of the specified mat3 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamMat4 ( string name , mat4 value )

Sets the value of the specified mat4 parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *mat4* **value** - Value to set.

## mat4 getParamMat4 ( string name )

Returns the value of the specified mat4 parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the parameter.
## void setParamAnimAsset ( string name , UGUID guid )

Sets the animation asset GUID for the specified parameter.
### Arguments

- *string* **name** - Name of the parameter.
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the animation asset to set.

## UGUID getParamAnimAsset ( string name )

Returns the animation asset GUID of the specified parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

GUID of the animation asset.
## void setParamTrigger ( string name , int value )

Sets the value of the specified trigger parameter. A trigger automatically resets to false after being consumed by the animation graph.
### Arguments

- *string* **name** - Name of the parameter.
- *int* **value** - Value to set.

## int getParamTrigger ( string name )

Returns the current value of the specified trigger parameter.
### Arguments

- *string* **name** - Name of the parameter.

### Return value

Current value of the trigger parameter.
## int isStateMachineActive ( string sm_name )

Returns a value indicating whether the specified state machine is currently active.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

true if the state machine is currently active; otherwise, false.
## string getStateMachineCurrentStateName ( string sm_name )

Returns the name of the current state in the specified state machine.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

Name of the current state.
## string getStateMachinePreviousStateName ( string sm_name )

Returns the name of the previous state in the specified state machine.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

Name of the previous state.
## int isStateMachineInTransition ( string sm_name )

Returns a value indicating whether the specified state machine is currently transitioning between states.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

true if the state machine is currently transitioning between states; otherwise, false.
## float getStateMachineTransitionProgress ( string sm_name )

Returns the current transition progress of the specified state machine.
### Arguments

- *string* **sm_name** - Name of the state machine.

### Return value

Transition progress in the [0.0, 1.0] range, where 0.0 is the start and 1.0 is complete.
