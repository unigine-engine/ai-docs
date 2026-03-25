# Custom Materials


If for some reason you cannot find the appropriate base material or you need a special post-process, there is a way of creating a brand new material. This way is not recommended, as even slight changes in the engine source code can influence your material and it would not work correctly.


A **custom material** is a [manual material](../../content/materials/index.md#manual_internal_materials) implemented using XML according to the base or user material file [format](../../code/formats/materials_formats/index.md). Both the base and the user material can be the custom one.


## Custom Base Material


The custom base material is the same as the default one: it is read-only, non-hierarchical, referred by the name and [so on](../../content/materials/index.md#base_materials).


So, the algorithm of custom base material creation is the following:


1. Create a `*.basemat` material file in the target directory (all of the Unigine base materials are located in the `data/core/materials/default` directory). Check the **[ULON Base Material File Format](../../code/formats/materials_formats/ulon_base_material_format.md)** article for the details.
2. Implement the base material according to the [base material file format](../../code/formats/materials_formats/ulon_base_material_format.md) in the created `*.basemat` file. ```cpp BaseMaterial mesh_base <node=ObjectMeshStatic editable=true var_prefix=var texture_prefix=tex> { /* ... */ } ``` > **Notice:** As any manual material, the base material doesn't need the [GUID](../../content/materials/inheritance.md#material_guid). It will be generated in run-time by its name. When implementing the custom base material, you can set the *[editable](../../code/formats/materials_formats/ulon_base_material_format.md#editable)* flag to true: it will allow you to adjust the material via the [Materials Editor](../../editor2/materials_settings/index.md) to get the desired visual effect. > **Notice:** Despite the fact that the base material can become editable, you cannot save changes made to it via the Materials Editor, so you should manually transfer the obtained values to the `*.basemat` file.
3. Specify a set of shaders for passes - either combine existing shaders or write your own ones. ```text Pass deferred <defines="BASE_DEFERRED,TWO_SIDED,ALPHA_TEST,TRANSPARENT_BLEND" node=ObjectMeshStatic> { Vertex = "core/shaders/mesh/opacity/deferred.shader" Fragment = "core/shaders/mesh/opacity/deferred.shader" } Pass depth_pre_pass <defines="BASE_ALPHA_TEST,TWO_SIDED,ALPHA_TEST,TRANSPARENT_BLEND" node=ObjectMeshStatic> { Vertex = "core/shaders/mesh/depth_pre_pass.shader" Fragment = "core/shaders/mesh/depth_pre_pass.shader" } ``` Check the **[pass](../../code/formats/materials_formats/ulon_materials/passes.md)** ULON node for the details.
4. Depending on the set of shaders, add required textures, parameters, and states to the base material:

  - Specify material states. ```text State ambient_light = 1 <hidden = true> State alpha_fade <hidden = true> State skinned <hidden = true> State spline <hidden = true> Group Default { State workflow <items = ["metalness","specular"]> State deferred = 1 <title = "Deferred Buffers" tooltip = "Deferred buffers rendering"> State multiple_environment_probes = 0 if [transparent == 2] } ``` Check the **[state](../../code/formats/materials_formats/base_material_format.md#element_state)** element for the details.
  - Set parameters. ```text Group Default { Mask24 material_mask = 0xffffffff <pass = "deferred" shared = false expression = true> } Group Base { Color albedo_color = [1.0 1.0 1.0 1.0] <shared = false title = "Albedo"> Slider metalness = 0.0 <shared = false tooltip = "Metalness multiplier"> Slider roughness = 1.0 <shared = false tooltip = "Roughness multiplier"> Slider specular = 0.5 <shared = false title="Specular" tooltip = "Specular multiplier"> Slider triplanar_blendr = 0.5 <shared = false  title = "Triplanar blend" tooltip = "Triplanar"> } ``` Check the **[parameter](../../code/formats/materials_formats/base_material_format.md#element_parameter)** element for the details.
  - Add textures. ```text Group Base { Texture diffuse = "core/textures/common/white.texture" <unit = 0 anisotropy = true tooltip = "Diffuse texture, alpha channel is detail texturing modulation"> Texture albedo = "core/textures/common/white.texture" <unit = 0 anisotropy = true tooltip = "Albedo texture"> } ``` Check the **[texture](../../code/formats/materials_formats/base_material_format.md#element_texture)** element for the details.
  - Set bindings. ```text Bind ObjectMeshStatic = ObjectMeshCluster <defines = "USE_CLUTTER_CLUSTER_PARAMETERS"> Bind ObjectMeshStatic = ObjectMeshClutter <defines = "USE_CLUTTER_CLUSTER_PARAMETERS"> Bind ObjectMeshStatic = ObjectMeshDynamic Bind ObjectMeshStatic = ObjectMeshSkinned ``` Check the **[bind](../../code/formats/materials_formats/base_material_format.md#element_bind)** element for the details.
5. Check, if the new material is loaded and rendered correctly.


As an example, check the base *[mesh_base](../../content/materials/library/mesh_base/index.md)* material (`data/core/materials/default/mesh/mesh_base.basemat`). It has two workflows: specular and metalness, contains a huge set of features.


When the base material is ready, you can use it as any default base material.


## Custom User Material


A custom user material is similar to the [custom base material](#custom_base_material) except that such material is hierarchical: it has a parent material and refers to the base material. As any manual material, the custom user material cannot be renamed and its parent cannot be changed. Also changes made to parameters of such material via Materials Editor won't be saved (even if the `editable` flag is set).


The custom user material is implemented by programmers when it is necessary to create a material without using Materials Editor.


In `*.mat` file, a name of the custom user material is stored. However, its child materials can store [name-based or GUID-based](../../content/materials/inheritance.md#parent_manual) reference to it. A [GUID](../../content/materials/inheritance.md#material_guid) for such material will be generated in run time by using its name.


The algorithm of custom user material creation is the following:


1. Create a `*.mat` material file in the target directory.
2. Implement the user material according to the [material file format](../../code/formats/materials_formats/user_material_format.md) in the created `*.mat` file. As any manual material, the custom material doesn't need a [GUID](../../content/materials/inheritance.md#material_guid). > **Notice:** Specify the *manual* attribute for the custom material. Otherwise, the material won't be loaded as it will be treated as the run-time user material without the GUID.


In the example below, the user material is inherited from the *mesh_base* material and overrides its parameters:


```xml
<?xml version="1.0" encoding="utf-8"?>
<material version="2.5.0.2" name="mesh_base_1" base_material="mesh_base" manual="1">
	<parameter name="albedo_color">0 0 0 0</parameter>
	<parameter name="metalness">1</parameter>
	<parameter name="roughness">0</parameter>
</material>

```
