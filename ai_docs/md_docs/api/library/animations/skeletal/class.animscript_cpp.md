# AnimScript Class (CPP)

**Header:** #include <UnigineAnimation.h>


This class provides the code-level interface for interacting with animation graphs at runtime. Animation graphs are visual, node-based assets (`*.agraph` files) created in the editor that define complex animation logic - state machines, blend trees, and transitions.


The AnimScript class serves as the runtime controller for a graph instance: it allows reading and writing graph parameters to drive animation from gameplay logic (e.g., setting a speed parameter to control walk/run blending, or a boolean flag to trigger a jump state). It also provides access to root motion data for physics-driven character movement.


An AnimScript instance is obtained from a [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md) node via [getAnimScript()](../../../../api/library/nodes/class.nodeskeletonpose_cpp.md#getAnimScript_AnimScript).


The class also reports the state of every [state machine](../../../../content/animations/state_machines/index.md) in the graph. Machines are addressed by index: resolve it once with [findStateMachine()](#findStateMachine_cstr_int) or [findStateMachineByName()](#findStateMachineByName_cstr_int), keep the value, and pass it to the **getStateMachine*** methods. The index stays valid as long as the same animation graph is loaded.


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

## bool isInit () const

Returns the current value indicating whether the animation graph has been initialized and is ready for use.
### Return value

**true** if the animation graph is initialized; otherwise **false**.
## UGUID getFileGUID () const

Returns the current GUID of the source animation graph asset file.
### Return value

Current animation graph file GUID.
## const char * getFilePath () const

Returns the current file path of the source animation graph asset.
### Return value

Current animation graph file path.
## int getNumParams () const

Returns the current total number of parameters defined in the animation graph.
### Return value

Current number of parameters.
## bool isActiveRootMotion () const

Returns the current value indicating whether root motion extraction is currently active in the animation graph.
### Return value

**true** if root motion is active; otherwise **false**.
## Math::Transform Math::Transform getRootMotionDelta () const

Returns the current root motion delta transform accumulated during the last graph update, representing the character's movement and rotation extracted from animation.
### Return value

Current root motion delta transform.
## Math:: vec3 getRootMotionDeltaPosition () const

Returns the current translation part of the root motion delta accumulated during the last graph update, that is, how far the character moved. It is the same value the [RootMotionDelta](#RootMotionDelta) transform carries, offered on its own for code that moves the character and leaves its heading alone.
### Return value

Current translation part of the root motion delta
## Math:: quat getRootMotionDeltaRotation () const

Returns the current rotation part of the root motion delta accumulated during the last graph update, that is, how far the character turned. It is the same value the [RootMotionDelta](#RootMotionDelta) transform carries, offered on its own for code that turns the character and leaves its position alone.
### Return value

Current rotation part of the root motion delta
## int getNumStateMachines () const

Returns the current total number of state machines in the animation graph, including the ones nested inside states.
### Return value

Current number of state machines
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
## int findStateMachine ( const char * path ) const

Returns the index of the state machine with the specified path. The index is stable for the lifetime of the loaded animation graph, so it is worth caching it instead of resolving the path each frame.
### Arguments

- *const char ** **path** - Path of the state machine, with the names of the enclosing machines separated by a slash (for example, Locomotion/Upper Body). For a top-level machine the path is simply its name.

### Return value

Index of the state machine, or -1 if there is no machine with such a path.
## int findStateMachineByName ( const char * name ) const

Returns the index of the state machine with the specified name. If several machines in the graph share a name, the first one found is returned - use [findStateMachine()](#findStateMachine_cstr_int) with a full path to address a particular one.
### Arguments

- *const char ** **name** - Name of the state machine, without the path of the enclosing machines.

### Return value

Index of the first state machine with such a name, or -1 if there is none.
## const char * getStateMachinePath ( int sm ) const

Returns the full path of the state machine with the specified index.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Path of the state machine.
## const char * getStateMachineName ( int sm ) const

Returns the name of the state machine with the specified index, without the path of the enclosing machines.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Name of the state machine.
## int getStateMachineParent ( int sm ) const

Returns the index of the state machine that encloses the specified one.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Index of the enclosing state machine, or -1 for a top-level machine.
## const char * getStateMachineOwnerStateName ( int sm ) const

Returns the name of the state, in the enclosing machine, whose subgraph contains the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Name of the state that contains this machine, or an empty string for a top-level machine.
## bool isStateMachineRelevant ( int sm ) const

Returns a value indicating whether the state machine took part in the last graph update and therefore contributes to the current pose. A machine nested in a state that is not active is not updated, so the values it reports are those of the frame it was last updated on.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

true if the state machine took part in the last graph update; otherwise, false.
## int getStateMachineNumStates ( int sm ) const

Returns the number of states in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Number of states.
## const char * getStateMachineStateName ( int sm , int state ) const

Returns the name of the state with the specified index in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.
- *int* **state** - Index of the state.

### Return value

Name of the state.
## int findStateMachineState ( int sm , const char * state_name ) const

Returns the index of the state with the specified name in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.
- *const char ** **state_name** - Name of the state.

### Return value

Index of the state, or -1 if the machine has no state with such a name.
## int getStateMachineCurrentState ( int sm ) const

Returns the index of the state that is currently active in the specified state machine. During a transition this is the state being transitioned to.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Index of the current state, or -1 if the machine has no active state.
## const char * getStateMachineCurrentStateName ( int sm ) const

Returns the name of the state that is currently active in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Name of the current state.
## int getStateMachinePreviousState ( int sm ) const

Returns the index of the state that was active before the current one in the specified state machine. During a transition this is the state being transitioned from.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Index of the previous state, or -1 if the machine has not changed state yet.
## const char * getStateMachinePreviousStateName ( int sm ) const

Returns the name of the state that was active before the current one in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Name of the previous state.
## void setStateMachineState ( int sm , int state , float duration )

Forces the specified state machine to switch to the given state, bypassing the transition conditions authored in the graph. The target animation starts from the beginning.
### Arguments

- *int* **sm** - Index of the state machine.
- *int* **state** - Index of the state to switch to.
- *float* **duration** - Duration of the blend into the target state, in seconds. 0 switches immediately.

## void setStateMachineStateAtTime ( int sm , int state , float duration , float normalized_time )

Forces the specified state machine to switch to the given state and start its animation at the given normalized time, bypassing the transition conditions authored in the graph. If the target node belongs to an active [sync group](../../../../content/animations/synchronization/index.md), the group time takes priority over the requested one.
### Arguments

- *int* **sm** - Index of the state machine.
- *int* **state** - Index of the state to switch to.
- *float* **duration** - Duration of the blend into the target state, in seconds. 0 switches immediately.
- *float* **normalized_time** - Position to start the target animation at, in the [0, 1] range, where 0 is the beginning of the clip and 1 is its end.

## bool isStateMachineInTransition ( int sm ) const

Returns a value indicating whether the specified state machine is currently blending from one state to another.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

true if the state machine is currently transitioning between states; otherwise, false.
## float getStateMachineTransitionProgress ( int sm ) const

Returns the progress of the transition that is currently running in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Transition progress in the [0, 1] range, where 0 is the start of the blend and 1 is its end.
## float getStateMachineTransitionTime ( int sm ) const

Returns the time that has passed since the current transition of the specified state machine started.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Time elapsed since the transition started, in seconds.
## float getStateMachineTransitionDuration ( int sm ) const

Returns the total duration of the transition that is currently running in the specified state machine, as set by the **Duration** property of the corresponding Condition node.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Total duration of the current transition, in seconds.
## float getStateMachineStateTime ( int sm ) const

Returns the time that has passed since the current state of the specified state machine was entered. This is the same value that the [State Time](../../../../content/animations/graph/node_library/time/state_time.md) node reports inside a condition graph.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Time elapsed since the current state was entered, in seconds.
## float getStateMachineAnimTime ( int sm ) const

Returns the current playback position of the animation that drives the current state of the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Current playback position of the animation, in seconds.
## float getStateMachineAnimTimeFraction ( int sm ) const

Returns the current playback position of the animation that drives the current state of the specified state machine, normalized by the clip length.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Current playback position of the animation in the [0, 1] range.
## float getStateMachineAnimLength ( int sm ) const

Returns the length of the animation that drives the current state of the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Length of the animation, in seconds.
## float getStateMachineAnimTimeRemaining ( int sm ) const

Returns the time left until the end of the animation that drives the current state of the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Time left until the end of the animation, in seconds.
## float getStateMachineAnimTimeRemainingFraction ( int sm ) const

Returns the time left until the end of the animation that drives the current state of the specified state machine, normalized by the clip length.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Time left until the end of the animation in the [0, 1] range.
## bool isStateMachineAnimEnded ( int sm ) const

Returns a value indicating whether the animation that drives the current state of the specified state machine has reached its end. A looping animation never reports the end.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

true if the animation has reached its end; otherwise, false.
## int getStateMachineNumTransitionConditions ( int sm ) const

Returns the number of Condition nodes the transition that is currently running in the specified state machine has passed through. Conditions can be chained into a routing tree, so a single transition may pass several of them.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Number of conditions passed by the current transition.
## const char * getStateMachineTransitionConditionName ( int sm , int index ) const

Returns the name of the Condition node the transition that is currently running in the specified state machine has passed through.
### Arguments

- *int* **sm** - Index of the state machine.
- *int* **index** - Index of the condition in the range from 0 to the total number of conditions passed by the current transition.

### Return value

Name of the Condition node.
