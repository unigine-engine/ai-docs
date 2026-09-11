# AnimScript Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class provides the code-level interface for interacting with animation graphs at runtime. Animation graphs are visual, node-based assets (`*.agraph` files) created in the editor that define complex animation logic - state machines, blend trees, and transitions.


The AnimScript class serves as the runtime controller for a graph instance: it allows reading and writing graph parameters to drive animation from gameplay logic (e.g., setting a speed parameter to control walk/run blending, or a boolean flag to trigger a jump state). It also provides access to root motion data for physics-driven character movement.


An AnimScript instance is obtained from a [NodeSkeletonPose](../../../../api/library/nodes/class.nodeskeletonpose_usc.md) node via [getAnimScript()](../../../../api/library/nodes/class.nodeskeletonpose_usc.md#getAnimScript_AnimScript).


The class also reports the state of every [state machine](../../../../content/animations/state_machines/index.md) in the graph. Machines are addressed by index: resolve it once with [findStateMachine()](#findStateMachine_cstr_int) or [findStateMachineByName()](#findStateMachineByName_cstr_int), keep the value, and pass it to the **getStateMachine*** methods. The index stays valid as long as the same animation graph is loaded.


## AnimScript Class

### Members

## int isInit () const

Returns the current value indicating whether the animation graph has been initialized and is ready for use.
### Return value

Current the animation graph is initialized
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
## int isActiveRootMotion () const

Returns the current value indicating whether root motion extraction is currently active in the animation graph.
### Return value

Current root motion is active
## FloatTransform FloatTransform getRootMotionDelta () const

Returns the current root motion delta transform accumulated during the last graph update, representing the character's movement and rotation extracted from animation.
### Return value

Current root motion delta transform.
## vec3 getRootMotionDeltaPosition () const

Returns the current translation part of the root motion delta accumulated during the last graph update, that is, how far the character moved. It is the same value the [RootMotionDelta](#RootMotionDelta) transform carries, offered on its own for code that moves the character and leaves its heading alone.
### Return value

Current translation part of the root motion delta
## quat getRootMotionDeltaRotation () const

Returns the current rotation part of the root motion delta accumulated during the last graph update, that is, how far the character turned. It is the same value the [RootMotionDelta](#RootMotionDelta) transform carries, offered on its own for code that turns the character and leaves its position alone.
### Return value

Current rotation part of the root motion delta
## int getNumStateMachines () const

Returns the current total number of state machines in the animation graph, including the ones nested inside states.
### Return value

Current number of state machines
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
## int findStateMachine ( string path )

Returns the index of the state machine with the specified path. The index is stable for the lifetime of the loaded animation graph, so it is worth caching it instead of resolving the path each frame.
### Arguments

- *string* **path** - Path of the state machine, with the names of the enclosing machines separated by a slash (for example, Locomotion/Upper Body). For a top-level machine the path is simply its name.

### Return value

Index of the state machine, or -1 if there is no machine with such a path.
## int findStateMachineByName ( string name )

Returns the index of the state machine with the specified name. If several machines in the graph share a name, the first one found is returned - use [findStateMachine()](#findStateMachine_cstr_int) with a full path to address a particular one.
### Arguments

- *string* **name** - Name of the state machine, without the path of the enclosing machines.

### Return value

Index of the first state machine with such a name, or -1 if there is none.
## string getStateMachinePath ( int sm )

Returns the full path of the state machine with the specified index.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Path of the state machine.
## string getStateMachineName ( int sm )

Returns the name of the state machine with the specified index, without the path of the enclosing machines.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Name of the state machine.
## int getStateMachineParent ( int sm )

Returns the index of the state machine that encloses the specified one.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Index of the enclosing state machine, or -1 for a top-level machine.
## string getStateMachineOwnerStateName ( int sm )

Returns the name of the state, in the enclosing machine, whose subgraph contains the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Name of the state that contains this machine, or an empty string for a top-level machine.
## int isStateMachineRelevant ( int sm )

Returns a value indicating whether the state machine took part in the last graph update and therefore contributes to the current pose. A machine nested in a state that is not active is not updated, so the values it reports are those of the frame it was last updated on.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

true if the state machine took part in the last graph update; otherwise, false.
## int getStateMachineNumStates ( int sm )

Returns the number of states in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Number of states.
## string getStateMachineStateName ( int sm , int state )

Returns the name of the state with the specified index in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.
- *int* **state** - Index of the state.

### Return value

Name of the state.
## int findStateMachineState ( int sm , string state_name )

Returns the index of the state with the specified name in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.
- *string* **state_name** - Name of the state.

### Return value

Index of the state, or -1 if the machine has no state with such a name.
## int getStateMachineCurrentState ( int sm )

Returns the index of the state that is currently active in the specified state machine. During a transition this is the state being transitioned to.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Index of the current state, or -1 if the machine has no active state.
## string getStateMachineCurrentStateName ( int sm )

Returns the name of the state that is currently active in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Name of the current state.
## int getStateMachinePreviousState ( int sm )

Returns the index of the state that was active before the current one in the specified state machine. During a transition this is the state being transitioned from.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Index of the previous state, or -1 if the machine has not changed state yet.
## string getStateMachinePreviousStateName ( int sm )

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

## int isStateMachineInTransition ( int sm )

Returns a value indicating whether the specified state machine is currently blending from one state to another.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

true if the state machine is currently transitioning between states; otherwise, false.
## float getStateMachineTransitionProgress ( int sm )

Returns the progress of the transition that is currently running in the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Transition progress in the [0, 1] range, where 0 is the start of the blend and 1 is its end.
## float getStateMachineTransitionTime ( int sm )

Returns the time that has passed since the current transition of the specified state machine started.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Time elapsed since the transition started, in seconds.
## float getStateMachineTransitionDuration ( int sm )

Returns the total duration of the transition that is currently running in the specified state machine, as set by the **Duration** property of the corresponding Condition node.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Total duration of the current transition, in seconds.
## float getStateMachineStateTime ( int sm )

Returns the time that has passed since the current state of the specified state machine was entered. This is the same value that the [State Time](../../../../content/animations/graph/node_library/time/state_time.md) node reports inside a condition graph.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Time elapsed since the current state was entered, in seconds.
## float getStateMachineAnimTime ( int sm )

Returns the current playback position of the animation that drives the current state of the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Current playback position of the animation, in seconds.
## float getStateMachineAnimTimeFraction ( int sm )

Returns the current playback position of the animation that drives the current state of the specified state machine, normalized by the clip length.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Current playback position of the animation in the [0, 1] range.
## float getStateMachineAnimLength ( int sm )

Returns the length of the animation that drives the current state of the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Length of the animation, in seconds.
## float getStateMachineAnimTimeRemaining ( int sm )

Returns the time left until the end of the animation that drives the current state of the specified state machine.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Time left until the end of the animation, in seconds.
## float getStateMachineAnimTimeRemainingFraction ( int sm )

Returns the time left until the end of the animation that drives the current state of the specified state machine, normalized by the clip length.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Time left until the end of the animation in the [0, 1] range.
## int isStateMachineAnimEnded ( int sm )

Returns a value indicating whether the animation that drives the current state of the specified state machine has reached its end. A looping animation never reports the end.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

true if the animation has reached its end; otherwise, false.
## int getStateMachineNumTransitionConditions ( int sm )

Returns the number of Condition nodes the transition that is currently running in the specified state machine has passed through. Conditions can be chained into a routing tree, so a single transition may pass several of them.
### Arguments

- *int* **sm** - Index of the state machine.

### Return value

Number of conditions passed by the current transition.
## string getStateMachineTransitionConditionName ( int sm , int index )

Returns the name of the Condition node the transition that is currently running in the specified state machine has passed through.
### Arguments

- *int* **sm** - Index of the state machine.
- *int* **index** - Index of the condition in the range from 0 to the total number of conditions passed by the current transition.

### Return value

Name of the Condition node.
