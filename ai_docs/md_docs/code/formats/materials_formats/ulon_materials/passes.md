# Passes


Specifies shaders and their defines to be used during the specific pass. The shaders are compiled for the specified render pass using the defines specified in attributes.


The syntax is the following:


```cpp
Pass render_pass_name
{
	Vertex = deferred_shader
	Fragment = deferred_shader
}

```


> **Notice:** You can specify various types of shaders in the pass ([see the list](../../../../code/formats/materials_formats/ulon_materials/shaders.md#types) of available shaders in UNIGINE).


You can check the current pass in the shader using the following **defines**:


```glsl
PASS_<pass name>

```


## Types of Passes


- custom_pass_name (*string*) � name of a custom rendering pass (up to 32 custom passes are supported)
- wireframe � *wireframe* pass
- visualizer_solid � *visualizer* solid pass
- lightmap_data � *lightmap baking* pass
- deferred � *deferred* pass
- auxiliary � *auxiliary* pass
- emission � *emission* pass
- refraction � *refraction* pass
- reflection � *reflection* pass
- transparent_blur � *transparent blur* pass
- ambient � *ambient* pass
- light_environment_probe � *Environment Probe* light pass
- light_voxel_probe � *Voxel Probe* light pass
- light_omni � *omni-directional* light pass
- light_proj � *projected light* pass
- light_world � *world light* pass (called only when there are more than one *[WorldLight](../../../../objects/lights/world/index.md)* present in the world)
- light_all � *environment probe, omni-directional light, projected light, world light* passes
- depth_pre_pass � *native depth* pre-pass
- ms_depth � *SRAA* pass
- shadow � *shadows* pass
- post � *post-process* pass
- object_post � *object post-process* pass
- procedural_decals � *procedural decals* pass
- procedural_fields � *procedural fields* pass


## Usage Examples


```cpp
Pass deferred
{
	Vertex = deferred_shader
	Fragment = deferred_shader
}

Pass shadow
{
	Vertex = deferred_shader
	Fragment = deferred_shader
}

Pass depth_pre_pass
{
	Vertex = depth_pre_pass_shader
	Fragment = depth_pre_pass_shader
}

Pass ms_depth
{
	Vertex = depth_pre_pass_shader
	Fragment = depth_pre_pass_shader
}

```


> **Notice:** If the vertex shader isn't specified, the default `core/shaders/common/empty.vert` shader will be used.


Besides the shader node you can specify the relative path (as a string) to the file containing shader code in *UUSL*:


```cpp
Pass lightmap_data
{
	Vertex = "core/shaders/mesh/lightmap_data.shader"
	Fragment = "core/shaders/mesh/lightmap_data.shader"
}

```


It is also possible to write inline shaders inside the *Pass* node (put them inside the **#{ � #}** construct):


```cpp
Pass name
{
	Geometry =
	#{
		// UUSL code
	#}
}

```


## Arguments


### defines


***String***


Definitions that will be passed to the shader.


Usage Example:


```cpp
defines="MY_DEFINE=32,MY_DEFINE_2"

```


> **Notice:** You can list multiple defines separated by a comma without any space. To specify a value for a define, write the value after the equals sign symbol.


### node


***String***


Specifies the type of a node for which this pass will be used (by default - all node types).


Available values:


- [DecalProj](../../../../api/library/decals/class.decalproj_cpp.md) � projected decal
- [DecalOrtho](../../../../api/library/decals/class.decalortho_cpp.md) � orthographic decal
- [DecalMesh](../../../../api/library/decals/class.decalmesh_cpp.md) � mesh decal
- [LandscapeLayerMap](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) � landscape layer map
- [ObjectDummy](../../../../api/library/objects/class.objectdummy_cpp.md) � *Dummy* object
- [ObjectDynamic](../../../../api/library/objects/class.objectdynamic_cpp.md) � dynamic object
- [ObjectMeshStatic](../../../../api/library/objects/class.objectmeshstatic_cpp.md) � static mesh
- [ObjectMeshCluster](../../../../api/library/objects/class.objectmeshcluster_cpp.md) � mesh cluster
- [ObjectMeshClutter](../../../../api/library/objects/class.objectmeshclutter_cpp.md) � mesh clutter
- [ObjectMeshSkinned](../../../../api/library/objects/class.objectmeshskinned_cpp.md) � *Skinned Mesh*
- [ObjectMeshDynamic](../../../../api/library/objects/class.objectmeshdynamic_cpp.md) � *Dynamic Mesh*
- [ObjectMeshSplineCluster](../../../../api/library/objects/class.objectmeshsplinecluster_cpp.md) � mesh spline cluster
- [ObjectLandscapeTerrain](../../../../api/library/objects/landscape_terrain/index.md) � *Landscape Terrain*
- [ObjectTerrainGlobal](../../../../api/library/objects/class.objectterrainglobal_cpp.md) � *Global Terrain*
- [ObjectGrass](../../../../api/library/objects/class.objectgrass_cpp.md) � *Grass*
- [ObjectParticles](../../../../api/library/objects/class.objectparticles_cpp.md) � particles
- [ObjectBillboards](../../../../api/library/objects/class.objectbillboards_cpp.md) � billboards
- [ObjectVolumeBox](../../../../api/library/objects/class.objectvolumebox_cpp.md) � *Volume Box*
- [ObjectVolumeSphere](../../../../api/library/objects/class.objectvolumesphere_cpp.md) � *Volume Sphere*
- [ObjectVolumeOmni](../../../../api/library/objects/class.objectvolumeomni_cpp.md) � *Volume Omni*
- [ObjectVolumeProj](../../../../api/library/objects/class.objectvolumeproj_cpp.md) � *Volume Projected*
- [ObjectGui](../../../../api/library/objects/class.objectgui_cpp.md) � *GUI* object
- [ObjectGuiMesh](../../../../api/library/objects/class.objectguimesh_cpp.md) � *GUI* mesh
- [ObjectWaterGlobal](../../../../api/library/objects/class.objectwaterglobal_cpp.md) � *Global Water*


#### Usage Example


```cpp
Pass ambient <defines="BOX,HEIGHT" node=ObjectVolumeBox>
{
	Vertex = volume_shader
	Fragment = volume_shader
}

Pass ambient <defines="SPHERE,HEIGHT" node=ObjectVolumeSphere>
{
	Vertex = volume_shader
	Fragment = volume_shader
}

```
