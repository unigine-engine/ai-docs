# States


State allows you to set a mode for rendering passes and a value for rendering options. States change a set of generated definitions passed to shaders, so any changes made to a state cause shaders recompilation. A material state generates *defines* for shaders only if the state meets the conditions. You can specify your own states or use and specify values for UNIGINE's internal states.


The syntax is the following:


```cpp
StateType state_name = value(s)

```


You can acces states in the shader using the following **defines**:


```glsl
GET_STATE_<state name in uppercase> = value // for all states

STATE_<state name> // if the state value is bigger than 0 (for example, StateToogle)

STATE_<state name>_<name of an element from the items array> // for State and StateSwitch

```


To change the state's values use the corresponding [API methods](../../../../api/library/rendering/class.material_cpp.md#setState_cstr_int_void).


## Types of States


- **StateToggle** (*bool*) � a switch that enables/disables the state
- **StateSwitch** (*integer*) � a multiple-value switch based on array of items (mandatory argument)
- **StateInt** (*integer*) � a state with an integer number (used to pass the state value via the API to the shader)
- **State** � auto detection of the state type (if the *items* argument is present, then *[StateSwitch](#state_switch)*; otherwise *[StateToggle](#state_toggle)*)


## Usage Examples


Suppose we got the base material with these *states* defined:


```cpp
BaseMaterial
{
	State my_state_switch = 4 <items = [a b c d e]> // or StateSwitch my_state_switch = 4 <items = [a b c d e]>
	State my_state_toggle = 1
	StateInt my_state_int = 256 <internal = true>
}

```


Then the following *defines* are available in the shaders:


```glsl
#define GET_STATE_MY_STATE_SWITCH 4
#define GET_STATE_MY_STATE_TOGGLE 1
#define GET_STATE_MY_STATE_INT 256

#ifdef STATE_MY_STATE_SWITCH_A
    /* some UUSL code */
#elif  STATE_MY_STATE_SWITCH_B
    /* some UUSL code */
#elif  STATE_MY_STATE_SWITCH_E
    /* some UUSL code */
#endif

#ifdef STATE_MY_STATE_TOGGLE
    /*some UUSL code*/
#endif

int my_state_int = GET_STATE_MY_STATE_INT;

```


## Arguments


### editable


***Boolean***


A flag indicating if state can be changed in the *[Parameters](../../../../editor2/materials_settings/index.md)* window or via [API](../../../../api/library/rendering/class.material_cpp.md).


Available values:


- false � unchangeable
- true � changeable (by default)


### title


***String***


Title for the Editor.


### tooltip


***String***


Tooltip for the Editor.


### switch_group


***String***


Sets this state to be responsible for the toggle of the specified group.


### hidden


***Boolean***


A flag indicating if the state is hidden in the Editor.


Available values:


- false � shows the state in the Editor
- true � hides the state in the Editor


### internal


***Boolean***


A flag indicating if the state is hidden in the Editor and the state values are not saved for the inherited materials.


Available values:


- false � shows the state in the Editor and saves the state values for the inherited materials
- true � hides the state in the Editor and does not save the state values for the inherited materials


### items


***Array of Strings***


Items used for the [StateSwitch](#state_switch) type.


### pass


***Array of Strings***


Specifies what passes use this state.


Available values:


- wireframe � the wireframe pass
- visualizer_solid � the visualizer solid pass
- deferred � the deferred pass
- auxiliary � the auxiliary pass
- emission � the emission pass
- refraction � the refraction pass
- reflection � the reflection pass
- transparent_blur � the transparent blur pass
- ambient � the ambient pass
- light_voxel_probe � the voxel probe light pass
- light_environment_probe � the environment probe pass
- light_omni � the omni-directional light pass
- light_proj � the projected light pass
- light_world � the world light pass
- depth_pre_pass � the native depth pre-pass
- shadow � the shadows pass
- post � the post-process pass
- light_all � the [environment probe](#texture_pass_light_environment_probe), [omni-directional light](#texture_pass_light_omni), [projected light](#texture_pass_light_proj), [world light](#texture_pass_light_world) passes
- forward � the [environment probe](#texture_pass_light_environment_probe), [omni-directional light](#texture_pass_light_omni), [projected light](#texture_pass_light_proj), [world light](#texture_pass_light_world) and [ambient](#texture_pass_ambient) passes
- transparent � the *[forward](#texture_pass_forward), [refraction](#texture_pass_refraction), [transparent blur](#texture_pass_transparent_blur)* passes
- custom_pass_name � name of a custom rendering pass (up to 32 custom passes are supported)
- object � [deferred](#texture_pass_deferred), [auxiliary](#texture_pass_auxiliary), [emission](#texture_pass_emission), [refraction](#texture_pass_refraction), [reflection](#texture_pass_reflection), [transparent blur](#texture_pass_transparent_blur), [ambient](#texture_pass_ambient), [voxel probe light](#texture_pass_light_voxel_probe), [environment probe](#texture_pass_light_environment_probe), [omni-directional light](#texture_pass_light_omni), [projected light](#texture_pass_light_proj), [world light](#texture_pass_light_world), [shadow](#texture_pass_shadow) and [native depth passes](#texture_pass_depth_pre_pass)


> **Notice:** To make one or more passes use this state, write passes in square brackets and separate them with spaces. For example:
>
>
> ```cpp
> State wireframe_antialiasing <pass=[wireframe post custom_pass_name]>
>
> ```
