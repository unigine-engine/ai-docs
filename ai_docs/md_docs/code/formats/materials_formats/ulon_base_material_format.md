# ULON Base Material File Format


Material specifies which shaders the specific [rendering pass](../../../principles/render/sequence/index.md) will use to render. When you assign the material, the engine starts using its shaders to render the image.


A base material is a `*.basemat` text file that contains all the information to provide the final appearance for an object. The base material is created by programmers and cannot be edited via the *Parameters* window.


It is based on *[ULON](../../../code/formats/ulon_format.md)* file format declarations that define a base material with the given properties (options, states, textures, parameters, shaders and so on).


Besides the *ULON* nodes, a base material file can also contain an inline *[UUSL](../../../code/uusl/index.md)* code or *[UnigineScript](../../../code/uniginescript/index.md)* expressions.


The syntax is the following:


```xml
BaseMaterial <node=ObjectMeshStatic options_hidden=0 preview_hidden=0 var_prefix=var texture_prefix=tex>
{
	/* Other ULON nodes here*/
}

```


There are two types of base material supported:


- **BaseMaterial** � base material for objects
- **BaseBrushMaterial** � base material for terrain brushes


> **Notice:** All node names in *ULON* are case-sensitive.


## Arguments


> **Notice:** Argument names and values are case-sensitive.


### editable


***Boolean***


A flag indicating if all of the base material settings can be changed in the *[Parameters](../../../editor2/materials_settings/index.md)* window or via [API](../../../api/library/rendering/class.material_cpp.md).


Available values:


- false � unchangeable
- true � changeable (by default)


### hidden


***Boolean***


A flag indicating if the material is displayed in the *[Materials](../../../editor2/materials_settings/organizing_materials/index.md)* Hierarchy.


Available values:


- false � displayed (by default)
- true � hidden


### manual


A flag, indicating if a material is [manual](../../../content/materials/index.md#manual_internal_materials): created or edited manually, not via UnigineEditor.


Available values:


- false � not manual
- true � manual (by default)


### guid


A GUID for the base material.


The guid argument is optional. The GUID for the base material will be generated from its manual name in runtime, if the *guid* argument isn't specified.


### options_hidden


***Boolean***


A flag indicating if the *[Options](../../../code/formats/materials_formats/ulon_base_material_format.md)* section is displayed for the material in the *Common* tab.


Available values:


- false � displayed (by default)
- true � hidden


### preview_hidden


***Boolean***


A flag indicating if the material preview is displayed.


Available values:


- false � displayed (by default)
- true � hidden


### legacy


***Boolean***


A flag indicating if the legacy mode is enabled.


Available values:


- false � displayed (by default)
- true � hidden


### var_prefix


***String***


The prefix added to the parameters when they are passed to the shader as a variable.


### texture_prefix


***String***


The prefixes that are added to the textures when they are passed to the shader.


### defines


***String***


The argument that specifies names of definitions that will be passed to all shaders.


### node


***String***


The type of node to which this material can be applied.


Available values:


- **[DecalProj](../../../api/library/decals/class.decalproj_cpp.md)** � projected decal
- **[DecalOrtho](../../../api/library/decals/class.decalortho_cpp.md)** � orthographic decal
- **[DecalMesh](../../../api/library/decals/class.decalmesh_cpp.md)** � mesh decal
- **[LandscapeLayerMap](../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md)** � landscape layer map
- **[ObjectDummy](../../../api/library/objects/class.objectdummy_cpp.md)** � *Dummy* object
- **[ObjectDynamic](../../../api/library/objects/class.objectdynamic_cpp.md)** � dynamic object
- **[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)** � static mesh
- **[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)** � *Mesh Cluster*
- **[ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md)** � *Mesh Clutter*
- **[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)** � *Skinned Mesh*
- **[ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)** � *Dynamic Mesh*
- **[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)** � mesh spline cluster
- **[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/index.md)** � *Landscape Terrain* object
- **[ObjectTerrainGlobal](../../../api/library/objects/class.objectterrainglobal_cpp.md)** � *Global Terrain* object
- **[ObjectGrass](../../../api/library/objects/class.objectgrass_cpp.md)** � *Grass* object
- **[ObjectParticles](../../../api/library/objects/class.objectparticles_cpp.md)** � particles
- **[ObjectBillboards](../../../api/library/objects/class.objectbillboards_cpp.md)** � *Billboards*
- **[ObjectVolumeBox](../../../api/library/objects/class.objectvolumebox_cpp.md)** � *Volume Box*
- **[ObjectVolumeSphere](../../../api/library/objects/class.objectvolumesphere_cpp.md)** � *Volume Sphere*
- **[ObjectVolumeOmni](../../../api/library/objects/class.objectvolumeomni_cpp.md)** � *Volume Omni* object
- **[ObjectVolumeProj](../../../api/library/objects/class.objectvolumeproj_cpp.md)** � *Volume Projected* object
- **[ObjectGui](../../../api/library/objects/class.objectgui_cpp.md)** � *GUI* object
- **[ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cpp.md)** � *GUI* mesh
- **[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md)** � *Global Water* object


### default


***Boolean***


Indicates that this material is used by default for the specified type of nodes.


Available values:


- false � not used as the default material (by default)
- true � sets as the default material


### namespace


***String***


The material namespace. Every manual material's name will contain this namespace: `namespace::filename`.

> **Notice:** The Engine has its own reserved namespaces: *Unigine* and *Editor*.


### shader_warning_mode


***String***


The shader warning mode that defines the way warnings are treated.


Available values:


- disable � disables shader warnings output
- soft � only errors result in shader compilation failure
- hard � warnings treated as errors and shader compilation fails (default)


### shader_optimization_level


> **Notice:** Available only for DirectX API.


Available values:


- 0 � skip optimization steps during code generation
- 1 � the compiler produces the slower code compared to other levels but does it quicker > **Notice:** Use this level for the shader debugging.
- 2 � the second lowest optimization
- 3 � the second highest optimization
- 4 � the compiler produces the best possible code but might take significantly longer to do so (default) > **Notice:** Use this level for the final builds when application performance matters.


### shader_disable_error


***Boolean***


A flag indicating if the shader compilation error output is disabled.


Available values:


- false � enables the shader compilation error output (by default)
- true � disables the shader compilation error output


### shader_disable_export


***Boolean***


A flag indicating if the preprocessored shader exporting is disabled.


Available values:


- false � enables the preprocessored shader exporting (by default)
- true � disables the preprocessored shader exporting


### shader_ieee_strictness


***Boolean***


A flag indicating if the floating math follows *IEEE-754* specification for generated shaders.


Available values:


- false � disables the floating math strictness (by default)
- true � enables the floating math strictness


### use_ui


***Boolean***


A flag indicating if the ui [groups](../../../code/formats/materials_formats/ulon_materials/groups.md) parsing is not skipped for this and inherited materials.


Available values:


- false � skip the ui elements parsing (by default)
- true � enable the ui elements parsing
