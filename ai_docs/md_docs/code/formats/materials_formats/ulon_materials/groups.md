# Groups


This node combines a set of [parameters](../../../../code/formats/materials_formats/ulon_materials/parameters.md), [textures](../../../../code/formats/materials_formats/ulon_materials/textures.md), [states](../../../../code/formats/materials_formats/ulon_materials/states.md), and [options](../../../../code/formats/materials_formats/ulon_materials/options.md) into a single group in UnigineEditor.


The syntax is the following:


```cpp
Group name
{
	// some parameters
}

```


## Usage Example


Put the parameters inside the *Group* node to combine them. It is also possible to create nested groups (nesting depth is unlimited).


```cpp
Group group_example
{
	Float width = 1.0f <min=0 max=2>
	Float height = 1.0f <min=0 max=2>

	Group nested_group_1
	{
		Float3 light_pos = [-6 -6 0]
		Int two_sided = false <min=0 max=2>
	}

	Group nested_group_2
	{
		ArrayFloat array_example = [1 2 3 4 5] <size=5>
		Mask24 mask24_example = 4096
	}
}

```


## Arguments


### merge_group


***Boolean***


Enables the identical named groups merging for inheritance. The group in the child material will be merged with parent group that have the same name.


Available values:


- **false** � disable (*by default*)
- **true** � enable


### toggle_state


***String***


Name of the state that is used to toggle the group.


Usage Example:


```cpp
State my_group_toggle = false

Group "My Group" if [my_group_toggle] <toggle_state = my_group_toggle>
{
	Slider my_group_slider = 0
	State my_group_state = true
}

```
