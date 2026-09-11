# Parameters


The material parameter that is available in the shader as a variable. Use the type of the *ULON* node for the parameter type.


The syntax is the following:


```cpp
ParameterType name = value <attributes>

```


The parameters are passed to shaders with the specified variable [prefix](../../../../code/formats/materials_formats/ulon_base_material_format.md#var_prefix).


## Types of Parameters


- float / float2 / float3 / float4 � a float vector of N components in *[UUSL](../../../../code/uusl/types.md#wrapper_types)*
- Int / Int2 / Int3 / Int4 � an integer (int) vector of N components in *[UUSL](../../../../code/uusl/types.md#wrapper_types)*
- ArrayFloat / ArrayFloat2 / ArrayFloat4 � an array of float vectors with N components in *[UUSL](../../../../code/uusl/types.md#wrapper_types)*
- ArrayInt / ArrayInt2 / ArrayInt4 � an array of integer (int) vectors with N components in *[UUSL](../../../../code/uusl/types.md#wrapper_types)*
- Color � a float vector with 4 components representing a color in *[UUSL](../../../../code/uusl/types.md#wrapper_types)*
- Mask24 / Mask32 � an integer representing the mask in *[UUSL](../../../../code/uusl/types.md#wrapper_types)*
- UV � a float vector of 4 components representing a UV transformation
- Slider � a float variable with the default range of [0, 1]


| [ULON](../../../../code/formats/materials_formats/ulon_base_material_format.md) | What to use for initialization in ULON? | [UUSL](../../../../code/uusl/types.md#wrapper_types) |
|---|---|---|
| Float | float value | float |
| Float2 | array of **2** float values | float2 |
| Float3 | array of **3** float values | float3 |
| Float4 | array of **4** float values | float4 |
| ArrayFloat | float value | float[N] |
| ArrayFloat2 | array of arrays of **2** float values | float2[N] |
| ArrayFloat4 | array of arrays of **4** float values | float4[N] |
| Color | array of **4** float values | float4 |
| UV | array of **4** float values | float4 |


## Usage Examples


For instance, the following *example* parameters are defined using the expression:


```cpp
Float float_example = 1
Int int_example = 1
ArrayFloat array_example = [1 2 3 4 5] <size=5>
ArrayFloat2 array_float2_example = [1 2 3 4 5 6] <size=3>
Float4 float4_example = [1 2 3 4]
Color color_example = [1 1 1 1]
UV uv_example = [1 1 0 0]
Mask24 mask24_example = 1

```


They are accessible in the shaders with the specified prefix:


```cpp
float a = var_float_example;
int b = var_int_example;
float c = var_array_example[0];
float d = array_float2_example [0][1];
float4 e = var_float4_example;
float4 f = var_color_example;
float4 g = var_uv_example;
int h = var_mask24_example;

```


## Arguments


### name


***String***


The name of the parameter.


### shader_name


***String***


Uniform name in the shader. If specified the provided uniform name is used, otherwise default [naming logic](#usage) is used.


### min


***Float***


The minimum limit for a parameter range (not applicable for *[Color](#color)* and *Array* types).


*Default values:*


- 0.0 � for the *[Slider](#slider)* parameter
- -inf � for all the others parameters


### max


***Float***


The maximum limit for a parameter range (not applicable for *[Color](#color)* and *Array* types).


*Default values:*


- 1.0 � for the *[Slider](#slider)* parameter
- +inf � for all the others parameters


### title


***String***


The parameter group title that will be displayed in the Editor.


### tooltip


***String***


The tooltip text displayed in the Editor on cursor hover over the parameter field.


### widget


***String***


The type of widget used for the parameter in the Editor.


If the type of widget is not specified, the most appropriate will be used (box fields for vector components or a slider). For the following types of parameters these widgets are set as defaults:


| Parameter type | Widget |
|---|---|
| Mask24 | mask24 |
| UV | uv |
| Color | сolor |
| Slider | slider |


### min_expand


***Boolean***


A flag that enables the ability to specify values outside the minimum range limit.


Available values:


- false � fix the minimum range limit
- true � expand the minimum range limit


*Default values:*


- false � for the *[Slider](#slider)* parameter
- true � for all the others parameters


### max_expand


***Boolean***


A flag that enables the ability to specify values outside the maximum range limit.


Available values:


- false � fix the maximum range limit
- true � expand the maximum range limit


*Default values:*


- false � for the *[Slider](#slider)* parameter
- true � for all the others parameters


### expand


***Boolean***


A flag that enables the ability to specify values outside the minimum and maximum range limit.


Available values:


- false � fix the range limit
- true � expand the range limit


*Default values:*


- false � for the *[Slider](#slider)* parameter
- true � for all the others parameters


### shared


***Boolean***


A flag that disables the passing of the parameter to shaders.


Available values:


- false � do not pass the parameter to the shader as a variable
- true � pass the parameter to the shader as a variable (*by default*)


### internal


***Boolean***


A flag that hides the parameter in the Editor and its values are not saved for the inherited materials.


- false � do not hide the parameter and save its values for the inherited materials (*by default*)
- true � hide the parameter and do not save its values for the inherited materials


### hidden


***Boolean***


A flag that hides the parameter in the Editor. The default value depends on the state of the *internal* argument. Enabled by default, except for *[Slider](#slider)*.


- false � do not hide the parameter
- true � hide the parameter


### auto_init


***Boolean***


A flag that determines whether the parameter should be automatically declared in the shader.


- false � auto initialized
- true � not auto initialized (*by default*)


### size


***Integer***


The size of an array (applicable only to array types), the default value is 0.


### pass


***String***


The set of passes during which the parameter will be used. If not specified the parameter is passed to all passes by default.


Available values:


- custom_pass_name � name of a custom rendering pass (up to 32 custom passes are supported)
- wireframe � the wireframe pass
- visualizer_solid � the visualizer solid pass
- lightmap_data - the lightmap baking pass
- deferred � the deferred pass
- auxiliary � the auxiliary pass
- emission � the emission pass
- refraction � the refraction pass
- transparent_blur � the transparent blur pass
- ambient � the ambient pass
- light_voxel_probe � the *Voxel Probe* light pass
- light_environment_probe � the *Environment Probe* pass
- light_planar_probe � the *Planar Probe* pass
- light_omni � the *Omni Light* pass
- light_proj � the *Proj Light* pass
- light_world � the *World Light* pass
- depth_pre_pass � the native depth pre-pass
- ms_depth - the *SRAA* pass
- shadow � the shadows pass
- post � the post-process pass
- procedural_decals - the procedural decal pass
- procedural_fields - the procedural field pass
- light_all � the *[Voxel Probe](#texture_pass_light_voxel_probe), [Environment Probe](#texture_pass_light_environment_probe), [Planar Probe](#texture_pass_light_planar_probe), [Omni Light](#texture_pass_light_omni), [Projected Light](#texture_pass_light_proj), [World Light](#texture_pass_light_world)* passes
- forward � the *[Voxel Probe](#texture_pass_light_voxel_probe), [Environment Probe](#texture_pass_light_environment_probe), [Planar Probe](#texture_pass_light_planar_probe), [Omni Light](#texture_pass_light_omni), [Projected Light](#texture_pass_light_proj), [World Light](#texture_pass_light_world)* and [ambient](#texture_pass_ambient) passes
- transparent � the [forward](#texture_pass_forward), [refraction](#texture_pass_refraction), [transparent blur](#texture_pass_transparent_blur) passes
- object � [deferred](#texture_pass_deferred), [auxiliary](#texture_pass_auxiliary), [emission](#texture_pass_emission), [refraction](#texture_pass_refraction), [transparent blur](#texture_pass_transparent_blur), [ambient](#texture_pass_ambient), *[Voxel Probe](#texture_pass_light_voxel_probe), [Environment Probe](#texture_pass_light_environment_probe), [Planar Probe](#texture_pass_light_planar_probe), [Omni Light](#texture_pass_light_omni), [Projected Light](#texture_pass_light_proj), [World Light](#texture_pass_light_world)*, [shadow](#texture_pass_shadow) and [native depth passes](#texture_pass_depth_pre_pass)


### expression


***Boolean***


A flag indicating if the parameter is controlled via an [expression](../../../../code/formats/materials_formats/ulon_materials/expressions.md) (UnigineScript). It also enables the ability to specify an expression in the Editor.


Available values:


- false � requires the user to assign specific values to the parameter (*by default*)
- true � use expression to calculate the parameter's values
