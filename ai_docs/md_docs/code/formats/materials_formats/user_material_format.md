# User Material File Format


## Material File Structure


A user material is a `*.mat` ("User Material") text file that overrides properties of the [base material](../../../code/formats/materials_formats/ulon_base_material_format.md).


> **Notice:** Options, states, textures and parameters are presented in the `*.mat` file only if they are overridden.


The user material is adjusted in the [Parameters](../../../editor2/materials_settings/index.md) window. If required, the `*.mat` text file can be [edited manually](../../../content/materials/custom.md#custom_user_material).


The `*.mat` file is created, when the user material is inherited from the base or another user material. The new material is created in the same directory as the parent one.


> **Notice:** When inheriting from the base material, by default, the user material is created in the `data` folder of the project.


The `*.mat` file is based on the `*.xml` file type and shares all its methods.


As well as for the base material, the `*.mat` file is based on 3 entities:


- **Element.** A component that may contain attributes, other elements, some content etc.
- **Attribute.** A component placed inside the element tag containing the specified value.
- **Value.** A component specifying the value of the attribute.


The syntax is the following:


```xml
<parent_element attribute="value">
 <child_element_1/>
 <child_element_2>content</child_element_2>
</parent_element>

```


All of the `*.mat` file elements, attributes and values are listed below.


## Material Element


A <material/> element defines a user material with the given properties.


It can have the attributes listed below.


### version


A version of the `*.mat` file.


### name


The unique name of the material. For [manual](../../../content/materials/index.md#manual_internal_materials) materials, the name is used as identifier for the material: by using it, the material's [GUID](../../../content/materials/inheritance.md#material_guid) is generated in run-time.


### guid


The [GUID](../../../content/materials/inheritance.md#material_guid) of the user material. For [manual](../../../content/materials/index.md#manual_internal_materials) materials, the name is used instead of the GUID.


### parent


a [GUID](../../../content/materials/inheritance.md#material_guid) of a parent material.


### parent_name


A name of a parent material. The attribute is used when the parent material is the manual user material.


### base_material


The name of a base material. The base material will be used as the parent one if the parent material isn't loaded.


If the parent has another base material, it will be changed to the specified one.


### editable


A flag, indicating if settings of the material can be changed in the [Parameters](../../../editor2/materials_settings/index.md) window or via [API](../../../api/library/rendering/class.material_cpp.md).


> **Notice:** If you set the flag for a [manual material](#material_manual), you still won't be able to save changes made to the material via UnigineEditor.


Available values:


- 0 - unchangeable
- 1 - changeable (by default)


### hidden


A flag, indicating if a material is displayed in the [Materials Hierarchy](../../../editor2/materials_settings/organizing_materials/index.md).


Available values:


- 0 - displayed (by default)
- 1  �- �hidden


### manual


A flag, indicating if a material is [manual](../../../content/materials/index.md#manual_internal_materials): created or edited manually, not via UnigineEditor.


> **Notice:** If the attribute isn't specified, the [custom user material](../../../content/materials/custom.md#custom_user_material) won't be loaded as it will be treated as the user material without a [GUID](../../../content/materials/inheritance.md#material_guid).


Available values:


- 0 - manual (by default)
- 1  �- �not manual


### Usage Example


For example, the displayed unchangeable material named user_material_0 and inherited from the *mesh_base_0* user material will be as follows:


```xml
<material version="2.7.3.0" name="user_material_0" parent="3e7f5c9535777e15966cb5f915d25b62620b2bef" base_material="mesh_base" editable="0">
...
</material>

```


## Blend Element


A <blend/> element allows you to override a value of a parent material's [blending](../../../principles/render/blending/index.md) option.


It can have the attributes listed below.


### src and dest


A polygon color (source image) and a screen buffer color (destination image) multipliers.


Available values for both attributes:


- none - blending is not used.
- zero - RGBA components of the source/destination image color are multiplied by zero.
- one - RGBA components of the source/destination image color are multiplied by one.
- src_color - RGBA components of the source/destination image color are multiplied by the mR, mG, mB, mA components (per component).
- one_minus_src_color - RGBA components of the source/destination image color are multiplied by the 1�- �mR , 1�- �mG , 1�- �mB , 1�- �mA  components (per component).
- src_alpha - RGBA components of the source/destination image color are multiplied by the mA component.
- one_minus_src_alpha - RGBA components of the source/destination image color are multiplied by the 1�- �mA  component.
- dest_color - RGBA components of the source/destination image color are multiplied by the bR, bG, bB, bA components (per component).
- one_minus_dest_color - RGBA components of the source/destination image color are multiplied by the 1�- �bR , 1�- �bG , 1�- �bB , 1�- �bA  components (per component).
- dest_alpha - RGBA components of the source/destination image color are multiplied by the bA component.
- one_minus_dest_alpha - RGBA components of the source/destination image color are multiplied by the 1�- �bA  component. Where mR, mG, mB, mA are normalized Red, Blue, Green and Alpha material image channels; bR, bG, bB, bA are normalized Red, Blue, Green and Alpha background image channels.


### Usage Example


For example, the user material that has the opaque areas receiving a material color and transparent areas receiving a screen buffer color will have the following element:


```xml
<blend src="one" dest="one_minus_src_alpha"/>
```


### Material Settings


In the *Parameters* window, the blending option value can be set in the **Transparency** group of the  [Common](../../../editor2/materials_settings/index.md#common_tab)  tab.


## Options Element


An <options/> element stores the overridden value of the parent material's option.


### order


[Rendering order](../../../editor2/materials_settings/index.md#order) of the material. Specifies the priority of the material rendering inside the group.


Available values:


- -128 - 127. The default value is 0. The higher the rendering order, the lower the rendering priority (the material with the -128 order will be rendered first).


### shadow_mask


A [shadow mask](../../../editor2/materials_settings/index.md#shadow_mask) used to control shadows cast by an object lit by light sources.


Available values:


- Integer, representing a mask. The default value is ~0.


### viewport_mask


A [viewport mask](../../../editor2/materials_settings/index.md#viewport_mask).


Available values:


- Integer, representing a mask. The default value is ~0.


### transparent


A flag indicating whether the material is [transparent](../../../editor2/materials_settings/index.md#blending).


Available values:


- 0 - the material is opaque
- 1 - the *Alpha test* blending preset.
- 2 - the *Alpha blend*, *Additive*, *Multiplicative* or *Custom* blending preset.


### depth_mask


A flag indicating if writing in the [depth buffer](../../../editor2/materials_settings/index.md#depth_write) is enabled for a material.


Available values:


- 0 - not used
- 1 - used (by default)


### depth_pre_pass


A flag indicating if the [native depth pre-pass](../../../principles/render/sequence/index.md#depth_pre_pass) is performed for a material.


Available values:


- 0 - is performed
- 1 - not performed


### transparent_order


The [Transparent Order](../../../editor2/materials_settings/index.md#transparent_order) option of a material.


Available values:


- 0 - Before SSR (by default)
- 1 - Before Post
- 2 - After Post


### two_sided


A flag indicating if a [Two Sided](../../../editor2/materials_settings/index.md#two_sided) option is enabled for a material.


Available values:


- 0 - disabled (by default)
- 1 - enabled


### depth_test


A flag indicating if a [Depth Test](../../../editor2/materials_settings/index.md#depth_test) option is enabled for a material.


Available values:


- 0 - disabled
- 1 - enabled (by default)


### cast_shadow


A flag indicating if a *[Cast Proj and Omni Shadow](../../../editor2/materials_settings/index.md#cast_shadow)* option is enabled for a material.


Available values:


- 0 - disabled
- 1 - enabled (by default)


### cast_world_shadow


A flag indicating if a *[Cast World Shadow](../../../editor2/materials_settings/index.md#cast_world_shadow)* option is enabled for a material.


Available values:


- 0 - disabled
- 1 - enabled (by default)


### Usage Example


For example, if you enable the Alpha test and Two sided options, the following is written into the `*.mat` file:


```xml
<options alpha_test="1" two_sided="1"/>
```


### Material Settings


In the *Parameters* window, a common option value can be set on the [Common](../../../editor2/materials_settings/index.md#common_tab) tab.


## State Element


A <state/> element stores the overridden value of the parent material's state (a mode of a rendering pass or a value of a rendering option).


### name


Name of the state.


### Usage Example


For example, if you set the *Ambient occlusion* state, the following string will be written into the `*.mat` file:


```xml
<state name="ao_map">1</state>
```


## Texture Element


A <texture/> element stores the overridden path to the texture of the parent material.


### name


Texture name.


### wrap


A texture wrapping methods.


Available values:


- clamp - a texture is clamped along all axes
- clamp_x - a texture is clamped along X-axis
- clamp_y - a texture is clamped along Y-axis
- clamp_z - a texture is clamped along Z-axis
- border - a texture is bordered along all axes
- border_x - a texture is bordered along X-axis
- border_y - a texture is bordered along Y-axis
- border_z - a texture is bordered along Z-axis
- repeat - no wrap, a texture is tiled along all axes. This value can be used, for example, when a base material's texture is bordered, and the child material's texture shouldn't.


### anisotropy


A flag, indicating if the anisotropy for the texture is enabled.


Available values:


- 0  �- �enabled (by default)
- 1  �- �disabled


### filter


A type of the texture filtering.


Available values:


- point  � - point �
- linear  � - linear �
- bilinear  � - bilinear �


### Usage Example


For example, if you change the path to the *Albedo* texture, the following will be written into the `*.mat` file:


```xml
<texture name="albedo" anisotropy="0">unigine_project/textures/ground_dirt_alb.texture</texture>

```


## Parameter Element


A <parameter/> element stores the overridden value of the parent material's parameter.


### name


Name of the parameter.


### Usage Example


If you override the *Albedo color* and *Metalness* parameters of the material, inherited from the *mesh_base*, the following will be written into the `*.mat` file:


```xml
<parameter name="albedo_color">0.501960814 0 0 1</parameter>
<parameter name="metalness">0.76700002</parameter>

```
