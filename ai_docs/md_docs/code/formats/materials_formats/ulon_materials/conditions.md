# Conditions


For each ULON node a logical condition can be specified using a [state](../../../../code/formats/materials_formats/ulon_materials/states.md) value. If the condition fails the node with all its children is ignored. Thus you can dynamically build the flexible hierarchy of ULON nodes. This can be useful when the contents of the node depends on certain parameters, e.g. a shader to be used is defined by the rendering pass.


Conditions are specified after the node's name, starting with the **if** keyword, the condition itself is enclosed in brackets **[ ... ]**.


The syntax is the following:


```cpp
Node name if [condition]

```


The [Group](../../../../code/formats/materials_formats/ulon_materials/groups.md) nodes support the nested conditions:


```cpp
Group parent if [condition]
{
	Group child if [condition]
}

```


Condition of the parent node is added to the condition of the child like so: **(parent_conditon) && (child_conditon)**.


You can write complex conditions using logical operations:


```cpp
Node name if [(state1 == 1 || state2 == 1) && !state3]

```


## Preprocessor Auto Generation for Shaders


In the *UUSL* code all conditions are enclosed in **#if** and **#endif** preprocessor on shader compilation, for instance:


```cpp
StateInt do_a_thing = 1

Slider do_a_thing = 0.5 if [do_a_thing == 2]
Texture do_a_thing = black if [do_a_thing == 3]

Shader example =
#{
   // the following UUSL preprocessors are inlined on shader compilations
   #if GET_STATE_DO_A_THING == 2
          UNIFORM float var_do_a_thing;
   #endif

   #if GET_STATE_DO_A_THING == 3
          INIT_TEXTURE(0, tex_do_a_thing);
   #endif

   // the variable or the texture is available only when the corresponding condition is met
   color.r = var_do_a_thing; // valid only when do_a_thing = 2
   color.gb = TEXTURE(tex_do_a_thing, IN_UV); // valid only when do_a_thing = 3
#}

```


## Usage Examples


```cpp
Int some_var = 1 <min=0 max=1>

Pass deferred if [some_var == 0]
{
	Vertex = "shaders/a.vert"
	Fragment = "shaders/a.frag"
}

Pass deferred if [some_var == 1]
{
	Vertex = "shaders/b.vert"
	Fragment = "shaders/b.frag"
}

```


Based on the value of some variable you can specify different shaders for the same render pass (deferred in our example).
