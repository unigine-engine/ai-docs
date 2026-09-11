# Declaring Parameters and Setting Values (CPP)


## Declaring Parameters


A parameter has to be declared before it can hold a value. There are two independent sets, one for surfaces and one for materials. They are reached through *[*Render::getSurfaceParameters()*](../../../api/library/rendering/class.render_cpp.md#SurfaceParameters)* and *[*Materials::getMaterialParameters()*](../../../api/library/rendering/class.materials_cpp.md#MaterialParameters)*, and both return a **CustomParameterLayout**.


There are two ways to declare parameters, and both fill the same layout: by hand in *UnigineEditor*, which is how a project is usually set up, or from code, which is what an application needs when the set of parameters is decided at run time.


> **Notice:** Both layouts are global. Adding, removing or reordering a parameter changes the block for every surface, or every material, in the project - and every shader compiled against that block. Declaring parameters is project setup, not per-level logic.


### In UnigineEditor


Open *Settings -> Runtime -> World -> Render -> [Custom Parameters](../../../editor2/settings/render_settings/custom_parameters/index.md)*. The page holds a *Save* button, the *Multilayered* checkbox described in [Surface ID Buffers and the Multilayered Mode](../../../content/materials/custom_parameters/ids_and_buffers.md#modes), and three tabs, each a table of its own with the number of declared parameters in the caption: *Surface* and *Material* for the two layouts this article is about, and *Render* for the global [custom render parameters](../../../content/materials/render_parameters.md), which are a separate feature sharing the page. Add an entry on the tab you need, give the parameter a name, a type (float, int or uint), a default value and a range for the slider, and press *Save* - one button commits all three tabs.


![A float parameter being added on the Surface tab of the Custom Parameters settings page](custom_surface_parameter_create.png)


> **Warning:** Until *Save* is pressed the parameter exists only in the table: nothing in the scene knows about it yet, and the *Custom Parameters* section of a node stays hidden.
>
>
> Pressing it reloads the materials and recompiles their shaders, which may take a while on a large project.
>
>
> Saving the project is a different thing and does not apply the declaration.


### From Code


The same layout is reachable as an object:


```cpp
using namespace Unigine;

// the surface layout: what one surface is, and what it is doing right now
CustomParameterLayoutPtr surface_layout = Render::getSurfaceParameters();

// each addParameter* returns the index of the new parameter
int offset = surface_layout->addParameterFloat("gamma_offset", 0.0f);
surface_layout->setParameterMinFloat(offset, -20.0f);
surface_layout->setParameterMaxFloat(offset, 20.0f);

int team = surface_layout->addParameterInt("team", 0);

// the material layout: what a substance is like, for every surface made of it
CustomParameterLayoutPtr material_layout = Materials::getMaterialParameters();

int gamma = material_layout->addParameterFloat("radar_gamma_db", -20.0f);
material_layout->setParameterMinFloat(gamma, -40.0f);
material_layout->setParameterMaxFloat(gamma, 30.0f);

// either layout can be read back and rearranged
int num = surface_layout->findParameter("team");
surface_layout->moveParameter(num, 0);

```


The two layouts are reached differently but behave identically, and a parameter of the same name can exist in both without the one having anything to do with the other. Which of them a value belongs in is decided by how many surfaces one change to it should reach - see [Choosing Where a Value Belongs](../../../content/materials/custom_parameters/index.md#choosing).


Every parameter is added, read and changed through methods of **CustomParameterLayout**:


| Method | What it does |
|---|---|
| [*addParameterFloat()*](../../../api/library/common/class.customparameterlayout_cpp.md#addParameterFloat_cstr_float_UGUID_int), [*addParameterInt()*](../../../api/library/common/class.customparameterlayout_cpp.md#addParameterInt_cstr_int_UGUID_int), [*addParameterUInt()*](../../../api/library/common/class.customparameterlayout_cpp.md#addParameterUInt_cstr_uint_UGUID_uint) | Declare a parameter of that type, taking a name and a default value, and return its index in the layout |
| [*getNumParameters()*](../../../api/library/common/class.customparameterlayout_cpp.md#NumParameters), [*getParameterName()*](../../../api/library/common/class.customparameterlayout_cpp.md#getParameterName_int_cstr), [*getParameterType()*](../../../api/library/common/class.customparameterlayout_cpp.md#getParameterType_int_int), [*findParameter()*](../../../api/library/common/class.customparameterlayout_cpp.md#findParameter_cstr_int) | Read the layout back: how many parameters it holds, the name and the type of one of them, and the index of the parameter with a given name or -1 if there is none |
| [*setParameterName()*](../../../api/library/common/class.customparameterlayout_cpp.md#setParameterName_int_cstr_void), [*setParameterType()*](../../../api/library/common/class.customparameterlayout_cpp.md#setParameterType_int_int_void) | Rename a declared parameter or change its type |
| [*setParameterDefault*()*](../../../api/library/common/class.customparameterlayout_cpp.md#setParameterDefaultFloat_int_float_void), [*setParameterMin*()*](../../../api/library/common/class.customparameterlayout_cpp.md#setParameterMinFloat_int_float_void), [*setParameterMax*()*](../../../api/library/common/class.customparameterlayout_cpp.md#setParameterMaxFloat_int_float_void) | Change the default value and the range the slider in the editor offers |
| [*swapParameters()*](../../../api/library/common/class.customparameterlayout_cpp.md#swapParameters_int_int_void), [*moveParameter()*](../../../api/library/common/class.customparameterlayout_cpp.md#moveParameter_int_int_void) | Reorder the layout |
| [*removeParameter()*](../../../api/library/common/class.customparameterlayout_cpp.md#removeParameter_int_void) | Drop a parameter |
| [*getStructureSize()*](../../../api/library/common/class.customparameterlayout_cpp.md#StructureSize) | Report how large the resulting block is, in bytes: the built-in fields plus four bytes per declared parameter, rounded up to a multiple of 16 and never below 16, the minimum stride of a float4 |
| [*getParameterGUID()*](../../../api/library/common/class.customparameterlayout_cpp.md#getParameterGUID_int_UGUID), [*findParameterByGUID()*](../../../api/library/common/class.customparameterlayout_cpp.md#findParameterByGUID_UGUID_int), [*makeParameterURI()*](../../../api/library/common/class.customparameterlayout_cpp.md#makeParameterURI_UGUID_String), [*parseParameterURI()*](../../../api/library/common/class.customparameterlayout_cpp.md#parseParameterURI_cstr_UGUID) | Address a parameter by the GUID it carries besides its name, which every *[*addParameter*()*](../../../api/library/common/class.customparameterlayout_cpp.md#addParameterFloat_cstr_float_UGUID_int)* accepts as an optional last argument |


A value written on a surface or a material is stored under the parameter's GUID, not under its name or its position in the layout. That is what lets a parameter be renamed, or moved up and down the list, without losing the values already written into it.


> **Warning:** A declaration from code takes effect immediately, but it does not do two things the editor's *Save* does:
>
>
> - **It does not rebuild the shaders** - the ones already compiled carry the old **SurfaceParameters** / **MaterialParameters** structure and cannot read the new parameter until *[*Materials::reloadMaterials()*](../../../api/library/rendering/class.materials_cpp.md#reloadMaterials_void)* is called. Declare the layout before the materials are loaded, or call that afterwards. The [graph nodes](../../../content/materials/custom_parameters/reading_parameters.md#shader_graph) are the exception - *UnigineEditor* rebuilds them, and the materials generated from the graphs, by itself.
> - **It does not save the declaration** - the layout is written into the [global configuration](#declare_storage) by *[*GlobalConfig::save()*](../../../api/library/engine/class.globalconfig_cpp.md#save_int)* or by the **global_config_save** console command; **global_config_autosave** does it on shutdown and is disabled by default. Until the configuration is saved the parameter exists for one session only, and *UnigineEditor* does not show it anywhere: no row on the *Custom Parameters* settings page, no entry in the *Custom Parameters* section of a surface, no output port on the *Surface Parameters* node. So you can neither set its value by hand nor connect it in a [material graph](../../../content/materials/graph/index.md).


### Parameter Names


A parameter name becomes a field of a shader structure, so it has to follow these rules:


- latin letters, digits and underscores only;
- a letter first - a leading underscore is reserved for the engine�s padding fields;
- no unigine_ prefix - it is reserved for the engine�s built-ins;
- no shader keyword and no type name - float, float4, min16int2x3 and the like;
- no name that another parameter of the same layout already has.


In the editor *Save* stays disabled until every name in the table passes these rules; from code such a call returns -1 and writes the reason to the log. The same check is available on its own as *[*Render::isValidSurfaceMaterialParameterName()*](../../../api/library/rendering/class.render_cpp.md#isValidSurfaceMaterialParameterName_cstr_int)*, for code that builds names of its own.


### Where Declarations and Settings Are Saved


The declarations, the switch that decides the buffer layout, and the values themselves are stored apart from each other:


| What | Where it is saved |
|---|---|
| Both declared layouts - the name, type, default, range and GUID of every parameter | The [global configuration](../../../code/configuration_file_cpp.md#global) of the project, in its **render** section, next to the global [render parameters](../../../content/materials/render_parameters.md). That file is `configs/default.global`, unless the `global_config` console variable points elsewhere. *Save* writes it by running the `global_config_save` command. |
| The *[Multilayered](../../../content/materials/custom_parameters/ids_and_buffers.md#modes)* checkbox | The boot configuration of the project, `configs/default.boot`, in its **console** section, as **render_surface_id_multilayered**. It goes there because it is a console variable, and the engine reads those when it starts. |
| Values set on a surface or on a decal | The world |
| Values set on a material | The `*.mat` file of that material |


> **Notice:** Neither configuration file is meant to be edited by hand.


The layouts and the values live in different files, so they can drift apart: an asset can be copied from another project, taken from a library, or opened after someone has edited the declarations.


Values are saved together with a record of the parameters they were written for. When the asset is loaded, the engine compares that record with the layout the project declares now and writes a warning to the log if they differ: values of a parameter the project no longer declares are dropped, and values of a parameter whose type has changed (for example, a float became int) are converted to the new type.


## Setting Values


Values can be filled in by hand or written from code. In *UnigineEditor* every place that owns a parameter block has *Custom Parameters* of its own:


- for an object surface or a decal, a section in the *Parameters* window;
- for a material, a tab in the *Materials* window.


All of them behave alike:


- they are shown only while their layout declares at least one parameter, and hold one entry per parameter it declares. A surface and a decal read the surface layout, a material reads the material one;
- a value is changed for the current selection only, not for everything the object owns;
- ![Go to declarations button](search_glass.png) jumps straight to the declarations, on the tab of *Settings -> Runtime -> World -> Render -> [Custom Parameters](../../../editor2/settings/render_settings/custom_parameters/index.md)* that the selection reads;
- ![Copy and paste parameters button](copy_paste_parameters.png) offers *Copy Parameters* / *Paste Parameters* for a surface and for a decal, to carry a whole set over to another selection.


### Object Surfaces


By hand, values are set on the surface selected in the *Surfaces* section of the object ([Quick Start](../../../content/materials/custom_parameters/quick_start.md) goes through that step). A *[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)* is the exception: it has no such section, so its values are written from code, both per surface and per instance (see [Mesh Cluster Instances](#values_instance)).


From code values are set per surface, by parameter index or by name:


```cpp
mesh->setSurfaceRenderCustomParameterFloat(0, "gamma_offset", -6.0f);
mesh->setSurfaceRenderCustomParameterInt(0, "team", 2);

float g = mesh->getSurfaceRenderCustomParameterFloat(0, "gamma_offset");

```


A surface that has not been given a value uses the declared default. *[*isSurfaceRenderCustomParameterOverridden()*](../../../api/library/objects/class.object_cpp.md#isSurfaceRenderCustomParameterOverridden_int_int_bool)* tells the two apart, *[*resetSurfaceRenderCustomParameter()*](../../../api/library/objects/class.object_cpp.md#resetSurfaceRenderCustomParameter_int_int_void)* drops a single override and *[*resetSurfaceRenderCustomParameters()*](../../../api/library/objects/class.object_cpp.md#resetSurfaceRenderCustomParameters_int_void)* all of them.


Values are often edited by pointing at geometry - in an editor tool, or in a debug mode of the application. A ray cast returns the node, the surface number and the instance number, so the setters are called on the node itself and no Surface ID is involved:


```cpp
WorldIntersectionPtr wip = WorldIntersection::create();

Math::Vec3 p0 = Game::getPlayer()->getWorldPosition();
Math::Vec3 p1 = p0 + Math::Vec3(Game::getPlayer()->getViewDirection()) * RAY_DISTANCE;

// 1 is the intersection mask: only objects with a matching mask are hit
ObjectPtr hit = World::getIntersection(p0, p1, 1, wip);
if (!hit)
	return;

const float DELTA = 10.0f; // how much one click heats the surface up

int surface = wip->getSurface();
int instance = wip->getInstance();

// an instance of a Mesh Cluster carries values of its own, everything else goes through the surface
if (hit->getType() == Node::OBJECT_MESH_CLUSTER)
{
	ObjectMeshClusterPtr cluster = static_ptr_cast<ObjectMeshCluster>(hit);
	float t = cluster->getInstanceCustomParameterFloat(instance, surface, "temperature");
	cluster->setInstanceCustomParameterFloat(instance, surface, "temperature", t + DELTA);
}
else
{
	float t = hit->getSurfaceRenderCustomParameterFloat(surface, "temperature");
	hit->setSurfaceRenderCustomParameterFloat(surface, "temperature", t + DELTA);
}

```


### Mesh Cluster Instances


Instances of a *[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)* share the surfaces of the source mesh, and their values come in two layers. What is set on a surface of the cluster is the base every instance starts from; *[*setInstanceCustomParameterFloat/Int/UInt(instance, surface, param, value)*](../../../api/library/objects/class.objectmeshcluster_cpp.md#setInstanceCustomParameterFloat_int_int_cstr_float_void)* overrides it for one instance and one surface. An instance is addressed by the index of its mesh transform, a parameter by index or by name:


```cpp
ObjectMeshClusterPtr cluster = static_ptr_cast<ObjectMeshCluster>(node);

int body = cluster->findSurface("body");
int glass = cluster->findSurface("glass");

// the base for every instance: the values of the cluster surfaces
cluster->setSurfaceRenderCustomParameterFloat(body, "gamma_offset", 0.0f);
cluster->setSurfaceRenderCustomParameterFloat(glass, "gamma_offset", -3.0f);

// an override per instance and surface on top of that base
for (int i = 0; i < cluster->getNumMeshes(); i++)
{
	cluster->setInstanceCustomParameterInt(i, body, "instance_id", i);
	cluster->setInstanceCustomParameterInt(i, glass, "instance_id", i);
}

// reading gives the value of the instance, or the surface value while it has no override
float g = cluster->getInstanceCustomParameterFloat(0, glass, "gamma_offset");

// an override is dropped by parameter index
int param = Render::getSurfaceParameters()->findParameter("gamma_offset");
cluster->resetInstanceCustomParameter(0, glass, param);

```


*[*isInstanceCustomParameterOverridden()*](../../../api/library/objects/class.objectmeshcluster_cpp.md#isInstanceCustomParameterOverridden_int_int_int_bool)* tells an override from an inherited value, *[*hasInstanceCustomParameters()*](../../../api/library/objects/class.objectmeshcluster_cpp.md#hasInstanceCustomParameters_int_int_int)* answers the same for the whole instance surface, and *[*resetInstanceCustomParameters()*](../../../api/library/objects/class.objectmeshcluster_cpp.md#resetInstanceCustomParameters_int_int_void)* drops every override of one.


> **Notice:** - A cluster has no *Custom Parameters* section in *UnigineEditor*, neither for its surfaces nor for its instances, so both layers are written from code. The values are saved with the world, and the editor carries the instance overrides over when a cluster is extended with new instances or split back into objects.
> - None of this applies to a *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md)*, which has no per-instance parameters.


### Materials


By hand, values are edited on the *Custom Parameters* tab of the *Materials* window, which appears once the material layout declares at least one parameter. From code they are set on the material itself. Either way the values are shared by every surface the material is assigned to:


```cpp
// every surface made of this material answers with these, without being touched itself
material->setCustomParameterFloat("radar_gamma_db", 15.0f);
material->setCustomParameterFloat("emission_boost", 2.0f);

```


Not every material can carry custom parameters. [Scriptable materials](../../../content/materials/scriptable.md) cannot, and neither can materials that draw no geometry, a post-effect one for instance. *[*Material::isCustomParametersSupported()*](../../../api/library/rendering/class.material_cpp.md#isCustomParametersSupported_int)* answers for a given material, so ask it before writing.


The same helpers exist as for surfaces: *[*isCustomParameterOverridden()*](../../../api/library/rendering/class.material_cpp.md#isCustomParameterOverridden_int_int)* shows whether a value was written or the declared default is in use, *[*resetCustomParameter()*](../../../api/library/rendering/class.material_cpp.md#resetCustomParameter_int_void)* drops one override, and *[*resetCustomParameters()*](../../../api/library/rendering/class.material_cpp.md#resetCustomParameters_void)* drops all of them.


### Decals


A decal has its own Surface ID and its own set of the same methods, without the surface index: *[*Decal::setSurfaceRenderCustomParameterFloat(name, value)*](../../../api/library/decals/class.decal_cpp.md#setSurfaceRenderCustomParameterFloat_cstr_float_void)* and so on, alongside *[*isSurfaceRenderCustomParameterOverridden()*](../../../api/library/decals/class.decal_cpp.md#isSurfaceRenderCustomParameterOverridden_int_bool)*, *[*resetSurfaceRenderCustomParameter()*](../../../api/library/decals/class.decal_cpp.md#resetSurfaceRenderCustomParameter_int_void)* and *[*resetSurfaceRenderCustomParameters()*](../../../api/library/decals/class.decal_cpp.md#resetSurfaceRenderCustomParameters_void)*.


By hand, values are set the same way as for an object surface: select the decal, and its own *Custom Parameters* section appears in the *Parameters* window. A decal reads the surface layout, not one of its own.


> **Notice:** A decal writes its ID only while *Write Surface ID* (**surface_id_write**) is enabled on its material - off by default. The Decal Buffer itself does not depend on [multilayered Surface ID](../../../content/materials/custom_parameters/ids_and_buffers.md#modes): decals read and write the Surface ID while they are being rendered, so they always get a target of their own.
