# Unigine.Node Class (CPP)

**Header:** #include <UnigineNode.h>


In terms of Unigine, all of the objects added into the scene are called [nodes](../../../objects/nodes/index.md). Nodes can be of different types, determining their visual representation and behavior.


The node is created and stored in the world. All changes are saved into the `.world` file.


The node can be also [saved](../../../api/library/engine/class.world_cpp.md#saveNode_cstr_Node_int_int) into an external `.node` file and then [imported](../../../api/library/engine/class.world_cpp.md#loadNode_cstr_int_Node) into the world when necessary. Also it is possible to create a [reference](../../../api/library/nodes/class.nodereference_cpp.md) to the exported node.


You can associate any [string data](#setData_cstr_cstr_void) (written directly into a *.node or a *.world file) or an arbitrary [user variable](#setVariable_Variable_void) with a node.


### See Also


- How to handle [ownership](../../../code/uniginescript/memory_management.md)
- How to work with the node's [matrix transformations](../../../code/fundamentals/matrix_transformations/index_cpp.md)


### Creating a Node


The Node class doesn't provide creating of a node. You can create an instance of any class inherited from the Node class and then obtain the node via automatic upcasting.


For example:

1. Create a box mesh by using the [Mesh](../../../api/library/rendering/class.mesh_cpp.md) class.
2. Use the box mesh to create an instance of the [ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md) class. This class is inherited from the Node class.
3. Get the node via upcasting.


```cpp
// AppWorldLogic.cpp

#include "AppWorldLogic.h"

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init() {


	// declare a smart pointer for any type of the node inherited from the Node class (e.g. ObjectMeshDynamic)
	// and call a constructor of the corresponding class
	ObjectMeshDynamicPtr object_mesh = ObjectMeshDynamic::create("core/meshes/box.mesh");

	// declare a smart pointer for the node
	// and obtain the node pointer from the created ObjectMeshDynamic
	NodePtr node = object_mesh;

	return 1;
}

```


Now you can operate the ObjectMeshDynamic instance as a node.


### Editing a Node and Saving Changes


The Node class contains common settings of the node. Also each node has special settings, which vary depending on the type of the node.

> **Notice:** The special settings of a node can be found in the article on the corresponding class.


Editing the node also includes editing materials and properties assigned to the node.


For the edited node to be saved in the `.world` file, you should enable the corresponding option via the *[setSaveToWorldEnabled()](#setSaveToWorldEnabled_int_void)* method.

> **Notice:** The node shall be saved to a `*.world` file only if this option is enabled for all of its ancestors as well.


For example:

1. Create a box mesh by using the [Mesh](../../../api/library/rendering/class.mesh_cpp.md) class.
2. Save the mesh on the disk. It is required as the node we are going to save to the `.world` file need to reference to a mesh stored on the disk.
3. Use the saved `.mesh` file to create an instance of the [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md) class. This class is inherited from the Node class.
4. Get the node from the ObjectMeshStatic instance via upcasting.
5. Enable saving to `.world` file for the node (and all its children).
6. Edit the node and save the world by calling the `world_save`console command.


```cpp
#include "AppWorldLogic.h"

#include <UnigineConsole.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init() {

	// create a mesh
	MeshPtr mesh = Mesh::create();
	mesh->addBoxSurface("box_0",vec3(1.0f));
	// save a mesh into a file on the disk
	mesh->save("unigine_project/meshes/my_mesh.mesh");
	// declare a smart pointer for any type of the node inherited from the Node class (e.g. ObjectMeshStatic)
	// and call a constructor of the corresponding class create an instance of any class inherited from the Node class (e.g. ObjectMeshStatic)
	ObjectMeshStaticPtr object_mesh = ObjectMeshStatic::create("unigine_project/meshes/my_mesh.mesh");

	// declare a smart pointer for the node,
	// obtain the node pointer from the created ObjectMeshStatic,
	NodePtr node = object_mesh;

	// enable saving the node(and all its children) to a .world file
	node->setSaveToWorldEnabledRecursive(true);

	// change the node name
	node->setName("my_node");
	// change node transformation
	node->setWorldTransform(translate(Vec3(0.0f, 0.0f, 2.0f)));

	// save node changes in the .world file
	Console::run("world_save");

	return 1;
}

```


### Exporting and Importing a Node


To export a node stored in the world into the external `.node` file, you should pass it to the *[saveNode()](../../../api/library/engine/class.world_cpp.md#saveNode_cstr_Node_int_int)* method of the World class.


To import the existing node stored in the `.node` file to the world, you should call the *[loadNode()](../../../api/library/engine/class.world_cpp.md#loadNode_cstr_int_Node)* method of the World class.


For example:


1. Create a box mesh by using the [Mesh](../../../api/library/rendering/class.mesh_cpp.md) class.
2. Save the mesh on the disk. It is required as the node we are going to export need to reference to a mesh stored on the disk.
3. Use the saved `.mesh` file to create an instance of the [ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md) class. This class is inherited from the Node class.
4. Get the node from the ObjectMeshStatic instance via upcasting.
5. Export the node to an external `.node` file.
6. Import the prevoiusly exported node to check the result.


```cpp
#include "AppWorldLogic.h"

#include <UnigineNode.h>
#include <UnigineObjects.h>
#include <UnigineWorld.h>
#include <UnigineEditor.h>
#include <UnigineConsole.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init() {

	// create a mesh
	MeshPtr mesh = Mesh::create();
	mesh->addBoxSurface("box_0", vec3(1.0f));
	// save a mesh into a file on the disk
	mesh->save("unigine_project/meshes/my_mesh.mesh");
	// create an instance of any class inherited from the Node class (e.g. ObjectMeshStatic)
	ObjectMeshStaticPtr object_mesh = ObjectMeshStatic::create("unigine_project/meshes/my_mesh.mesh");
	// declare a smart pointer for the node
	// and obtain the node pointer from the created NodeDummy
	NodePtr node = object_mesh;
	// export the node into a .node file
	World::saveNode("unigine_project/nodes/my_node.node", node);
	// import the exported node to check the result
	NodePtr imported_node = World::loadNode("unigine_project/nodes/my_node.node");
	// set position of the node
	imported_node->setPosition(Vec3(4.0f, 0.0f, 1.0f));

	return 1;
}

```


### Deleting a Node


By default each new node's lifetime matches the lifetime of the **World** (i.e. such node shall be deleted when the world is closed). But you can also choose node's lifetime to be managed:


- **by the Engine** - is this case the node shall be deleted automatically on Engine shutdown.
- **manually** - is this case the node should be deleted manually by the user.


To delete a node you can use the following two methods:


- [*deleteLater()*](../../../api/library/common/class.ptr_cpp.md#deleteLater_void) - performs delayed deletion, in this case the object will be deleted during the next swap stage of the main loop (rendering of the object ceases immediately, but it still exists in memory for a while, so you can get it from its parent, for example). This method simplifies object deletion from a secondary thread, so you can call it and forget about the details, letting the Engine take control over the process of deletion, which can be used for future optimizations.
- [*deleteForce()*](../../../api/library/common/class.ptr_cpp.md#deleteForce_void) - performs immediate deletion, which might be necessary in some cases. Calling this method for main-loop-dependent objects (e.g., nodes) is safe only when performed from the Main thread.


```cpp
// AppWorldLogic.cpp

#include <UnigineNode.h>
#include <UnigineObjects.h>
#include <UnigineWorld.h>
#include <UnigineEditor.h>
#include <UnigineConsole.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init() {

	// create a mesh
	MeshPtr mesh = Mesh::create();
	mesh->addBoxSurface("box_0", vec3(1.0f));
	// save a mesh into a file on the disk
	mesh->save("unigine_project/meshes/my_mesh.mesh");
	// create an instance of any class inherited from the Node class (e.g. ObjectMeshStatic)
	ObjectMeshStaticPtr object_mesh = ObjectMeshStatic::create("unigine_project/meshes/my_mesh.mesh");
	// declare a smart pointer for the node
	// and obtain the node pointer from the created NodeDummy
	NodePtr node = object_mesh;

	// do something with the node
	// ...

	// delete the node
	node.deleteLater();

	return 1;
}

```


## Node Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **ANY_TYPE** = -1 | Any node type. |
| **NODE_BEGIN** = 0 | Begin of the nodes range. |
| **NODE_DUMMY** = 0 | Dummy node. See the [NodeDummy](../../../api/library/nodes/class.nodedummy_cpp.md) class. |
| **NODE_LAYER** = 1 | Layer node. See the [NodeLayer](../../../api/library/nodes/class.nodelayer_cpp.md) class. |
| **NODE_TRIGGER** = 2 | Dummy node that can fire callbacks on its enabling/disabling or repositioning. See the [NodeTrigger](../../../api/library/nodes/class.nodetrigger_cpp.md) class. |
| **NODE_REFERENCE** = 3 | Node reference that refers to an external NODE file. See the [NodeReference](../../../api/library/nodes/class.nodereference_cpp.md) class. |
| **NODE_EXTERN** = 4 | Extern node. See the [NodeExtern](../../../api/library/nodes/class.nodeextern_cpp.md) class. |
| **NODE_SEQUENCE_PLAYER** = 5 | Sequence player node. See the [NodeSequencePlayer](../../../api/library/nodes/class.nodesequenceplayer_cpp.md) class. |
| **NODE_SKELETON_POSE** = 6 | Skeleton pose node. See the [NodeSkeletonPose](../../../api/library/nodes/class.nodeskeletonpose_cpp.md) class. |
| **NODE_END** = 6 | End of the nodes range. |
| **WORLD_BEGIN** = 7 | Begin of the world nodes range. |
| **WORLD_SPLINE_GRAPH** = 7 | World spline graph. See the [WorldSplineGraph](../../../api/library/worlds/class.worldsplinegraph_cpp.md) class. |
| **WORLD_TRIGGER** = 8 | World trigger. See the [WorldTrigger](../../../api/library/worlds/class.worldtrigger_cpp.md) class. |
| **WORLD_CLUTTER** = 9 | World clutter. See the [WorldClutter](../../../api/library/worlds/class.worldclutter_cpp.md) class. |
| **WORLD_SWITCHER** = 10 | Node switcher (to switch off parts of the world). See the [WorldSwitcher](../../../api/library/worlds/class.worldswitcher_cpp.md) class. |
| **WORLD_OCCLUDER** = 11 | World occluder. See the [WorldOccluder](../../../api/library/worlds/class.worldoccluder_cpp.md) class. |
| **WORLD_OCCLUDER_MESH** = 12 | World mesh occluder. See the [WorldOccluderMesh](../../../api/library/worlds/class.worldoccludermesh_cpp.md) class. |
| **WORLD_TRANSFORM_PATH** = 13 | Path defined transformer. See the [WorldTransformPath](../../../api/library/worlds/class.worldtransformpath_cpp.md) |
| **WORLD_TRANSFORM_JOINT** = 14 | Joint defined transformer. See the [WorldTransformJoint](../../../api/library/worlds/class.worldtransformjoint_cpp.md) class. |
| **WORLD_EXPRESSION** = 15 | Node which allows to execute arbitrary expression. See the [WorldExpression](../../../api/library/worlds/class.worldexpression_cpp.md) class. |
| **WORLD_EXTERN** = 16 | External world. See the [WorldExtern](../../../api/library/worlds/class.worldextern_cpp.md) class. |
| **WORLD_END** = 16 | End of the world nodes range. |
| **GEODETIC_BEGIN** = 17 | Begin of the geodetic nodes range. |
| **GEODETIC_PIVOT** = 17 | Geodetic Pivot node. See the [GeodeticPivot](../../../api/library/geodetics/class.geodeticpivot_cpp.md) class. |
| **GEODETIC_END** = 17 | End of the geodetic nodes range. |
| **FIELD_BEGIN** = 18 | Begin of the field nodes range. |
| **FIELD_SPACER** = 18 | Field Spacer node. See the [FieldSpacer](../../../api/library/fields/class.fieldspacer_cpp.md) class. |
| **FIELD_ANIMATION** = 19 | Field Animation node. See the [FieldAnimation](../../../api/library/fields/class.fieldanimation_cpp.md) class. |
| **FIELD_HEIGHT** = 20 | Field Height node. See the [FieldHeight](../../../api/library/fields/class.fieldheight_cpp.md) class. |
| **FIELD_SHORELINE** = 21 | Field Shoreline node. See the [FieldShoreline](../../../api/library/fields/class.fieldshoreline_cpp.md) class. |
| **FIELD_WEATHER** = 22 | Field Weather node. See the [FieldWeather](../../../api/library/fields/class.fieldweather_cpp.md) class. |
| **FIELD_END** = 22 | End of the field nodes range. |
| **PARTICLES_FIELD_BEGIN** = 23 | Beginning of the particles field range. |
| **PARTICLES_FIELD_SPACER** = 23 | Particles Field Spacer node. See the [ParticlesFieldSpacer](../../../api/library/objects/class.particlesfieldspacer_cpp.md) class. |
| **PARTICLES_FIELD_DEFLECTOR** = 24 | Particles Field Deflector node. See the [ParticlesFieldDeflector](../../../api/library/objects/class.particlesfielddeflector_cpp.md) class. |
| **PARTICLES_FIELD_END** = 24 | End of the particles field nodes range. |
| **LIGHT_BEGIN** = 25 | Begin of the light nodes range. |
| **LIGHT_VOXEL_PROBE** = 25 | Voxel probe. See the [LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_cpp.md) class. |
| **LIGHT_ENVIRONMENT_PROBE** = 26 | Environment probe. See the [LightEnvironmentProbe](../../../api/library/lights/class.lightenvironmentprobe_cpp.md) class. |
| **LIGHT_PLANAR_PROBE** = 27 | Planar probe. See the [LightPlanarProbe](../../../api/library/lights/class.lightplanarprobe_cpp.md) class. |
| **LIGHT_OMNI** = 28 | Omni-directional light source. See the [LightOmni](../../../api/library/lights/class.lightomni_cpp.md) class. |
| **LIGHT_PROJ** = 29 | Projected light source. See the [LightProj](../../../api/library/lights/class.lightproj_cpp.md) class. |
| **LIGHT_WORLD** = 30 | World light source. See the [LightWorld](../../../api/library/lights/class.lightworld_cpp.md) class. |
| **LIGHT_END** = 30 | End of the light nodes range. |
| **DECAL_BEGIN** = 31 | Begin of the decal nodes range. |
| **DECAL_PROJ** = 31 | Projected decal node. See the [DecalProj](../../../api/library/decals/class.decalproj_cpp.md) class. |
| **DECAL_ORTHO** = 32 | Orthographic decal node. See the [DecalOrtho](../../../api/library/decals/class.decalortho_cpp.md) class. |
| **DECAL_MESH** = 33 | Mesh decal node. See the [DecalMesh](../../../api/library/decals/class.decalmesh_cpp.md) class. |
| **DECAL_END** = 33 | End of the decal nodes range. |
| **LANDSCAPE_LAYER_BEGIN** = 34 | Beginning of the landscape layers range. |
| **LANDSCAPE_LAYER_MAP** = 34 | Landscape Layer Map. See the [LandscapeLayerMap](../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) class. |
| **LANDSCAPE_LAYER_END** = 34 | End of the landscape layers range. |
| **OBJECT_BEGIN** = 35 | Begin of the object nodes range. |
| **OBJECT_DUMMY** = 35 | Dummy object. See the [ObjectDummy](../../../api/library/objects/class.objectdummy_cpp.md) class. |
| **OBJECT_DYNAMIC** = 36 | Dynamic object. See the [ObjectDynamic](../../../api/library/objects/class.objectdynamic_cpp.md) class. |
| **OBJECT_MESH_STATIC** = 37 | Static mesh object. See the [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md) class. |
| **OBJECT_MESH_CLUSTER** = 38 | [Mesh Cluster](../../../objects/objects/mesh_cluster/index.md) object. See the [ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md) class. |
| **OBJECT_MESH_CLUTTER** = 39 | [Mesh Clutter](../../../objects/objects/mesh_clutter/index.md) object. See the [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cpp.md) class. |
| **OBJECT_MESH_SKINNED_LEGACY** = 40 | Legacy skinned mesh object. See the [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md) class. |
| **OBJECT_MESH_SKINNED** = 41 | Skinned mesh object. See the [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md) class. |
| **OBJECT_MESH_DYNAMIC** = 42 | Dynamic mesh object. See the [ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md) class. |
| **OBJECT_MESH_SPLINE_CLUSTER** = 43 | Mesh Spline Cluster object. See the [ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md) class. |
| **OBJECT_LANDSCAPE_TERRAIN** = 44 | LandscapeTerrain object. See the [ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md) class. |
| **OBJECT_TERRAIN_GLOBAL** = 45 | Terrain global object. See the [ObjectTerrainGlobal](../../../api/library/objects/class.objectterrainglobal_cpp.md) class. |
| **OBJECT_GRASS** = 46 | Grass. See the [ObjectGrass](../../../api/library/objects/class.objectgrass_cpp.md) class. |
| **OBJECT_PARTICLES** = 47 | Particles object. See the [ObjectParticles](../../../api/library/objects/class.objectparticles_cpp.md) class. |
| **OBJECT_BILLBOARDS** = 48 | [Billboards](../../../objects/objects/billboards/index.md) object for rendering a high number of billboards. See the [ObjectBillboard](../../../api/library/objects/class.objectbillboards_cpp.md) class. |
| **OBJECT_VOLUME_BOX** = 49 | Volume box object. See the [ObjectVolumeBox](../../../api/library/objects/class.objectvolumebox_cpp.md) class. |
| **OBJECT_VOLUME_SPHERE** = 50 | Volume sphere object. See the [ObjectVolumeSphere](../../../api/library/objects/class.objectvolumesphere_cpp.md) class. |
| **OBJECT_VOLUME_OMNI** = 51 | Volume omni light object. See the [ObjectVolumeOmni](../../../api/library/objects/class.objectvolumeomni_cpp.md) class. |
| **OBJECT_VOLUME_PROJ** = 52 | Volume projected light object. See the [ObjectVolumeProj](../../../api/library/objects/class.objectvolumeproj_cpp.md) class. |
| **OBJECT_GUI** = 53 | GUI object. See the [ObjectGui](../../../api/library/objects/class.objectgui_cpp.md) class. |
| **OBJECT_GUI_MESH** = 54 | GUI mesh object. See the [ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cpp.md) class. |
| **OBJECT_WATER_GLOBAL** = 55 | Water global object. See the [ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md) class. |
| **OBJECT_WATER_MESH** = 56 | Water mesh object. See the [ObjectWaterMesh](../../../api/library/objects/class.objectwatermesh_cpp.md) class. |
| **OBJECT_SKY** = 57 | Sky object. See the [ObjectSky](../../../api/library/objects/class.objectsky_cpp.md) class. |
| **OBJECT_CLOUD_LAYER** = 58 | Cloud layer object. See the [ObjectCloudLayer](../../../api/library/objects/class.objectcloudlayer_cpp.md) class. |
| **OBJECT_EXTERN** = 59 | Extern object. See the [ObjectExtern](../../../api/library/objects/class.objectextern_cpp.md) class. |
| **OBJECT_TEXT** = 60 | Text object. See the [ObjectText](../../../api/library/objects/class.objecttext_cpp.md) class. |
| **OBJECT_END** = 60 | End of the object nodes range. |
| **PLAYER_BEGIN** = 61 | Begin of the player nodes range. |
| **PLAYER_DUMMY** = 61 | Dummy player. See the [PlayerDummy](../../../api/library/players/class.playerdummy_cpp.md) class. |
| **PLAYER_SPECTATOR** = 62 | Observing player. See the [PlayerSpectator](../../../api/library/players/class.playerspectator_cpp.md) class. |
| **PLAYER_PERSECUTOR** = 63 | Persecuting player. See the [PlayerPersecutor](../../../api/library/players/class.playerpersecutor_cpp.md) class. |
| **PLAYER_ACTOR** = 64 | Acting player. See the [PlayerActor](../../../api/library/players/class.playeractor_cpp.md) class. |
| **PLAYER_END** = 64 | End of the player nodes range. |
| **PHYSICAL_BEGIN** = 65 | Begin of the physical nodes range. |
| **PHYSICAL_WIND** = 65 | Physical wind object. See the [PhysicalWind](../../../api/library/physics/class.physicalwind_cpp.md) class. |
| **PHYSICAL_FORCE** = 66 | Physical force node that allows to simulate point forces applied to dynamic objects. See the [PhysicalForce](../../../api/library/physics/class.physicalforce_cpp.md) class. |
| **PHYSICAL_NOISE** = 67 | Physical noise node that allows to simulate force field. See the [PhysicalNoise](../../../api/library/physics/class.physicalnoise_cpp.md) class. |
| **PHYSICAL_WATER** = 68 | Physical water object that has no visual representation. See the [PhysicalWater](../../../api/library/physics/class.physicalwater_cpp.md) class. |
| **PHYSICAL_TRIGGER** = 69 | Physical trigger. See the [PhysicalTrigger](../../../api/library/physics/class.physicaltrigger_cpp.md) class. |
| **PHYSICAL_END** = 69 | End of the physical nodes range. |
| **NAVIGATION_BEGIN** = 70 | Begin of the navigation nodes range. |
| **NAVIGATION_SECTOR** = 70 | Sector within which pathfinding is performed. See the [NavigationSector](../../../api/library/pathfinding/class.navigationsector_cpp.md) class. |
| **NAVIGATION_MESH** = 71 | Mesh-based navigation area across which pathfinding is performed. See the [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md) class. |
| **NAVIGATION_END** = 71 | End of the navigation nodes range. |
| **EXPERIMENTAL_NAVIGATION_BEGIN** = 72 | Begin of the experimental navigation nodes range. |
| **EXPERIMENTAL_NAVIGATION_MESH** = 72 | Navigation mesh baked from the scene geometry, across which pathfinding is performed. See the [ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md) class. |
| **EXPERIMENTAL_NAVIGATION_MESH_INVOKER** = 73 | Node that keeps the tiles of a baked navigation mesh resident around itself. See the [ExperimentalNavigationMeshInvoker](../../../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cpp.md) class. |
| **EXPERIMENTAL_NAVIGATION_MESH_AREA_VOLUME** = 74 | Volume that stamps an area onto the polygons of a baked navigation mesh. See the [ExperimentalNavigationMeshAreaVolume](../../../api/library/pathfinding/class.experimentalnavigationmeshareavolume_cpp.md) class. |
| **EXPERIMENTAL_NAVIGATION_END** = 74 | End of the experimental navigation nodes range. |
| **OBSTACLE_BEGIN** = 75 | Begin of the obstacle nodes range. |
| **OBSTACLE_BOX** = 75 | Obstacle in the shape of a box avoided by pathfinding. See the [ObstacleBox](../../../api/library/pathfinding/class.obstaclebox_cpp.md) class. |
| **OBSTACLE_SPHERE** = 76 | Obstacle in the shape of a sphere avoided by pathfinding. See the [ObstacleSphere](../../../api/library/pathfinding/class.obstaclesphere_cpp.md) class. |
| **OBSTACLE_CAPSULE** = 77 | Obstacle in the shape of a capsule avoided by pathfinding. See the [ObstacleCapsule](../../../api/library/pathfinding/class.obstaclecapsule_cpp.md) class. |
| **OBSTACLE_END** = 77 | End of the obstacle nodes range. |
| **SOUND_BEGIN** = 78 | Begin of the sound nodes range. |
| **SOUND_SOURCE** = 78 | Sound source. See the [SoundSource](../../../api/library/sounds/class.soundsource_cpp.md) class. |
| **SOUND_REVERB** = 79 | Sound reverberation zone. See the [SoundReverb](../../../api/library/sounds/class.soundreverb_cpp.md) class. |
| **SOUND_END** = 79 | End of the sound nodes range. |
| **NUM_NODES** = 80 | Counter of node types. |
| **NUM_WORLDS** = WORLD_END - WORLD_BEGIN + 1 | Counter of world node types. |
| **NUM_GEODETICS** = GEODETIC_END - GEODETIC_BEGIN + 1 | Counter of geodetic node types. |
| **NUM_FIELDS** = FIELD_END - FIELD_BEGIN + 1 | Counter of field node types. |
| **NUM_PARTICLES_FIELDS** = PARTICLES_FIELD_END - PARTICLES_FIELD_BEGIN + 1 | Counter of particles field node types. |
| **NUM_LIGHTS** = LIGHT_END - LIGHT_BEGIN + 1 | Counter of light node types. |
| **NUM_DECALS** = DECAL_END - DECAL_BEGIN + 1 | Counter of decal node types. |
| **NUM_OBJECTS** = OBJECT_END - OBJECT_BEGIN + 1 | Counter of object node types. |
| **NUM_PLAYERS** = PLAYER_END - PLAYER_BEGIN + 1 | Counter of player node types. |
| **NUM_PHYSICALS** = PHYSICAL_END - PHYSICAL_BEGIN + 1 | Counter of physical node types. |
| **NUM_NAVIGATIONS** = NAVIGATION_END - NAVIGATION_BEGIN + 1 | Counter of navigation node types. |
| **NUM_OBSTACLES** = OBSTACLE_BEGIN - OBSTACLE_END + 1 | Counter of obstacle node types. |
| **NUM_SOUNDS** = SOUND_END - SOUND_BEGIN + 1 | Counter of sound node types. |
| **DUMMY** = 0 | Dummy node. See the [NodeDummy](../../../api/library/nodes/class.nodedummy_cpp.md) class. |
| **LAYER** = 1 | Layer node. See the [NodeLayer](../../../api/library/nodes/class.nodelayer_cpp.md) class. |
| **TRIGGER** = 2 | Dummy node that can fire callbacks on its enabling/disabling or repositioning. See the [NodeTrigger](../../../api/library/nodes/class.nodetrigger_cpp.md) class. |
| **REFERENCE** = 3 | Node reference that refers to an external NODE file. See the [NodeReference](../../../api/library/nodes/class.nodereference_cpp.md) class. |
| **EXTERN** = 4 | Extern node. See the [NodeExtern](../../../api/library/nodes/class.nodeextern_cpp.md) class. |

## LIFETIME

| Name | Description |
|---|---|
| **LIFETIME_WORLD** = 0 | Node's lifetime is managed by the world. The node shall be deleted automatically on closing the world. |
| **LIFETIME_ENGINE** = 1 | Node's lifetime is managed by the Engine. The node shall be deleted automatically on Engine shutdown. |
| **LIFETIME_MANUAL** = 2 | Node's lifetime is managed by the user. The node should be deleted manually by the user. |

### Members

## Ptr < GeodeticPivot > getGeodeticPivot () const

Returns the current pointer to geodetic pivot of the node.
### Return value

Current geodetic pivot, or NULL if the node is not a child of a geodetic pivot node.
## void setVariable ( const Variable & variable )

Sets a new value of the single unnamed variable parameter of the node. If this variable does not exist it will be created with a specified value (on requesting the non-existent value 0 will be returned).
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **variable** - The variable value.

## const Variable & getVariable () const

Returns the current value of the single unnamed variable parameter of the node. If this variable does not exist it will be created with a specified value (on requesting the non-existent value 0 will be returned).
### Return value

Current variable value.
## void setWorldScale ( const Math:: vec3 & scale )

Sets a new node scale in the world space.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **scale** - The node scale in the world space.

## Math:: vec3 getWorldScale () const

Returns the current node scale in the world space.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


### Return value

Current node scale in the world space.
## void setWorldPosition ( const Math:: Vec3 & position )

Sets a new node position in the world coordinates.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **position** - The node position in the world coordinates.

## Math:: Vec3 getWorldPosition () const

Returns the current node position in the world coordinates.
### Return value

Current node position in the world coordinates.
## void setScale ( const Math:: vec3 & scale )

Sets a new scale of the node.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **scale** - The node scale in the local space.

## Math:: vec3 getScale () const

Returns the current scale of the node.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


### Return value

Current node scale in the local space.
## void setPosition ( const Math:: Vec3 & position )

Sets a new node position.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **position** - The node position in the local space.

## Math:: Vec3 getPosition () const

Returns the current node position.
### Return value

Current node position in the local space.
## Math:: vec3 getBodyAngularVelocity () const

Returns the current angular velocity of the node's physical body in the world space.
### Return value

Current angular velocity of the node's physical body in the world space.
## Math:: vec3 getBodyLinearVelocity () const

Returns the current linear velocity of the node's physical body in the local space.
### Return value

Current linear velocity of the node's physical body in the local space.
## Ptr < BodyRigid > getObjectBodyRigid () const

Returns the current [rigid body](../../../principles/physics/bodies/rigid/index.md) assigned to the node if it is an object node.
### Return value

Current [rigid body](../../../principles/physics/bodies/rigid/index.md) assigned to the node if it is an object node; otherwise, NULL (0).
## Ptr < Body > getObjectBody () const

Returns the current physical body assigned to the node if it is an object node.
### Return value

Current physical body assigned to the node if it is an object node; otherwise, NULL (0).
## Math:: WorldBoundSphere getWorldBoundSphere () const

Returns the current bounding sphere of the node in world's coordinate system.
### Return value

Current bounding sphere of the node in world's coordinate system.
## Math:: WorldBoundBox getWorldBoundBox () const

Returns the current bounding box of the node in world's coordinate system.
### Return value

Current [world bounding box](../../../api/library/math/bounds/class.worldboundbox_cpp.md).
## Math:: BoundSphere getBoundSphere () const

Returns the current bounding sphere of the node.
> **Notice:** The coordinates of the bounding sphere are in the node's local coordinate system. To get the bounding sphere in world coordinates, use the [*getWorldBoundSphere()*](#getWorldBoundSphere_WorldBoundSphere) method.


### Return value

Current [bounding sphere](../../../api/library/math/bounds/class.boundsphere_cpp.md) of the node.
## Math:: BoundBox getBoundBox () const

Returns the current bounding box of the node.
> **Notice:** The coordinates of the bounding box are in the node's local coordinate system. To get the bounding box in world coordinates, use the [*getWorldBoundBox()*](#getWorldBoundBox_WorldBoundBox) method.


### Return value

Current [bounding box](../../../api/library/math/bounds/class.boundbox_cpp.md) of the node.
## void setOldWorldTransform ( const Math:: Mat4 & transform )

Sets a new old (previous frame) transformation matrix for the node in the world coordinates.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The old (previous frame) transformation matrix for the node in the world coordinates.

## Math:: Mat4 getOldWorldTransform () const

Returns the current old (previous frame) transformation matrix for the node in the world coordinates.
### Return value

Current old (previous frame) transformation matrix for the node in the world coordinates.
## void setWorldTransform ( const Math:: Mat4 & transform )

Sets a new transformation matrix of the node in the world coordinates.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation matrix of the node in the world coordinates.

## Math:: Mat4 getWorldTransform () const

Returns the current transformation matrix of the node in the world coordinates.
### Return value

Current transformation matrix of the node in the world coordinates.
## void setTransform ( const Math:: Mat4 & transform )

Sets a new transformation matrix of the node in its parent coordinates.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation matrix of the node in local coordinates.

## Math:: Mat4 getTransform () const

Returns the current transformation matrix of the node in its parent coordinates.
### Return value

Current transformation matrix of the node in local coordinates.
## int getNumProperties () const

Returns the current total number of properties associated with the node.
### Return value

Current total number of properties associated with the node.
## Ptr < Node > getPossessor () const

Returns the current possessor of the node. the following nodes can be possessors:
- NodeReference
- WorldCluster
- WorldClutter
- WorldLayer

This function can only be applied to a root node inside a node reference.
### Return value

Current node possessor, if it exists; otherwise, NULL.
## int getNumChildren () const

Returns the current number of children of the node.
### Return value

Current number of child nodes.
## Ptr < Node > getRootNode () const

Returns the current root node for the node. This method searches for the root node among all node's parents and [possessors](#getPossessor_Node) up the hierarchy. If a node does not have a parent or possessor the node itself will be returned.
### Return value

Current root node for the node.
## void setParent ( const Ptr < Node >& parent )

Sets a new parent of the node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>&* **parent** - The parent of the node or **NULL** (**0**), if the node has no parent.

## Ptr < Node > getParent () const

Returns the current parent of the node.
### Return value

Current parent of the node or **NULL** (**0**), if the node has no parent.
## int getNumAncestors () const

Returns the current number of ancestors of the node.
### Return value

Current number of ancestors of the node.
## void setName ( const char * name )

Sets a new name of the node.
### Arguments

- *const char ** **name** - The name of the node.

## const char * getName () const

Returns the current name of the node.
### Return value

Current name of the node.
## void setQuery ( bool query )

Sets a new value indicating if occlusion query is used for the node. The default is false (not used).
### Arguments

- *bool* **query** - Set **true** to enable occlusion query is used for the node; **false** - to disable it.

## bool isQuery () const

Returns the current value indicating if occlusion query is used for the node. The default is false (not used).
### Return value

**true** if occlusion query is used for the node; otherwise **false**.
## void setClutterInteractionEnabled ( bool enabled )

Sets a new value indicating if interaction with [World Clutters](../../../api/library/worlds/class.worldclutter_cpp.md) and [Mesh Clutters](../../../api/library/objects/class.objectmeshclutter_cpp.md) is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of clutters is not necessary. Especially when the world contains a significant number of such nodes.


### Arguments

- *bool* **enabled** - Set **true** to enable interaction with [World Clutters](../../../api/library/worlds/class.worldclutter_cpp.md) and [Mesh Clutters](../../../api/library/objects/class.objectmeshclutter_cpp.md); **false** - to disable it.

## bool isClutterInteractionEnabled () const

Returns the current value indicating if interaction with [World Clutters](../../../api/library/worlds/class.worldclutter_cpp.md) and [Mesh Clutters](../../../api/library/objects/class.objectmeshclutter_cpp.md) is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of clutters is not necessary. Especially when the world contains a significant number of such nodes.


### Return value

**true** if interaction with [World Clutters](../../../api/library/worlds/class.worldclutter_cpp.md) and [Mesh Clutters](../../../api/library/objects/class.objectmeshclutter_cpp.md) is enabled ; otherwise **false**.
## void setGrassInteractionEnabled ( bool enabled )

Sets a new value indicating if interaction with [Grass](../../../api/library/objects/class.objectgrass_cpp.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of grass is not necessary. Especially when the world contains a significant number of such nodes.


### Arguments

- *bool* **enabled** - Set **true** to enable interaction with [Grass](../../../api/library/objects/class.objectgrass_cpp.md) nodes; **false** - to disable it.

## bool isGrassInteractionEnabled () const

Returns the current value indicating if interaction with [Grass](../../../api/library/objects/class.objectgrass_cpp.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of grass is not necessary. Especially when the world contains a significant number of such nodes.


### Return value

**true** if interaction with [Grass](../../../api/library/objects/class.objectgrass_cpp.md) nodes is enabled ; otherwise **false**.
## void setTriggerInteractionEnabled ( bool enabled )

Sets a new value indicating if interaction with [WorldTrigger](../../../api/library/worlds/class.worldtrigger_cpp.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when node interaction with [World Triggers](../../../api/library/worlds/class.worldtrigger_cpp.md) is not necessary. Especially when the world contains a significant number of such nodes.


### Arguments

- *bool* **enabled** - Set **true** to enable interaction with [World Triggers](../../../api/library/worlds/class.worldtrigger_cpp.md); **false** - to disable it.

## bool isTriggerInteractionEnabled () const

Returns the current value indicating if interaction with [WorldTrigger](../../../api/library/worlds/class.worldtrigger_cpp.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when node interaction with [World Triggers](../../../api/library/worlds/class.worldtrigger_cpp.md) is not necessary. Especially when the world contains a significant number of such nodes.


### Return value

**true** if interaction with [World Triggers](../../../api/library/worlds/class.worldtrigger_cpp.md) is enabled ; otherwise **false**.
## void setImmovable ( bool immovable )

Sets a new value indicating if the node is an immovable (clutter) object, which means it is moved to a separate spatial tree for immovable (static) objects optimizing node management. There are several restrictions on nodes considered immovable. Any action affecting the spatial tree is prohibited and causes a warning: you cannot change the node state (enabled/disabled), surfaces, bounds, trasformation, visibility distance, as well as move the node, assign a non-dummy physical body or even disable the *Immovable* flag as it also leads to rebiulding of the spatial tree.
> **Notice:** You can disable these warnings by using the [*World::setMovingImmovableNodeMode()*](../../../api/library/engine/class.world_cpp.md#setMovingImmovableNodeMode_int_void) method, if necessary.


### Arguments

- *bool* **immovable** - Set **true** to enable the feature of the clutter (immovable) object for the node; **false** - to disable it.

## bool isImmovable () const

Returns the current value indicating if the node is an immovable (clutter) object, which means it is moved to a separate spatial tree for immovable (static) objects optimizing node management. There are several restrictions on nodes considered immovable. Any action affecting the spatial tree is prohibited and causes a warning: you cannot change the node state (enabled/disabled), surfaces, bounds, trasformation, visibility distance, as well as move the node, assign a non-dummy physical body or even disable the *Immovable* flag as it also leads to rebiulding of the spatial tree.
> **Notice:** You can disable these warnings by using the [*World::setMovingImmovableNodeMode()*](../../../api/library/engine/class.world_cpp.md#setMovingImmovableNodeMode_int_void) method, if necessary.


### Return value

**true** if the feature of the clutter (immovable) object for the node; otherwise **false**.
## void setHandled ( bool handled )

Sets a new value indicating if the node handle is displayed. This option is valid only for invisible nodes, such as light and sound sources, particle systems and world-managing nodes ( [WorldOccluder](../../../api/library/worlds/class.worldoccluder_cpp.md), triggers, expressions, etc.)
### Arguments

- *bool* **handled** - Set **true** to enable displaying of the node handle; **false** - to disable it.

## bool isHandled () const

Returns the current value indicating if the node handle is displayed. This option is valid only for invisible nodes, such as light and sound sources, particle systems and world-managing nodes ( [WorldOccluder](../../../api/library/worlds/class.worldoccluder_cpp.md), triggers, expressions, etc.)
### Return value

**true** if displaying of the node handle is enabled ; otherwise **false**.
## void setEnabled ( bool enabled )

Sets a new value indicating if the node and its parent nodes are enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable the node; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the node and its parent nodes are enabled.
### Return value

**true** if the node is enabled ; otherwise **false**.
## bool isExtern () const

Returns the current value indicating if the node is an extern node (its type is one of the following: *[NODE_EXTERN](#NODE_EXTERN), [OBJECT_EXTERN](#OBJECT_EXTERN), [WORLD_EXTERN](#WORLD_EXTERN)*).
### Return value

**true** if the node is an extern node; otherwise **false**.
## bool isField () const

Returns the current value indicating if the node is a field node (its type is one of the *[FIELD_*](#FIELD_ANIMATION)*).
### Return value

**true** if the node is a field node; otherwise **false**.
## bool isParticlesField () const

Returns the current value indicating if the node is a particles field node (its type is one of the *[PARTICLES_FIELD_*](#PARTICLES_FIELD_BEGIN)*).
### Return value

**true** if the node is a particles field node; otherwise **false**.
## bool isSound () const

Returns the current value indicating if the node is a sound node (its type is *[SOUND_*](#SOUND_BEGIN)*).
### Return value

**true** if the node is a sound node; otherwise **false**.
## bool isObstacle () const

Returns the current value indicating if the node is an obstacle node (its type is *[OBSTACLE_*](#OBSTACLE_BEGIN)*).
### Return value

**true** if the node is an obstacle node; otherwise **false**.
## bool isExperimentalNavigation () const

Returns the current value indicating if a given node belongs to the experimental navigation system, that is, if its type falls within the [EXPERIMENTAL_NAVIGATION_BEGIN](#EXPERIMENTAL_NAVIGATION_BEGIN) .. [EXPERIMENTAL_NAVIGATION_END](#EXPERIMENTAL_NAVIGATION_END) range.
### Return value

**true** if the node belongs to the experimental navigation system; otherwise **false**.
## bool isNavigation () const

Returns the current value indicating if a given node is a navigation node, that is, if its type falls within the [NAVIGATION_BEGIN](#NAVIGATION_BEGIN) .. [NAVIGATION_END](#NAVIGATION_END) range. The range covers the navigation areas only. Nodes of the experimental navigation system occupy a range of their own and are reported by [IsExperimentalNavigation](#IsExperimentalNavigation).
### Return value

**true** if the node is a navigation node; otherwise **false**.
## bool isPhysical () const

Returns the current value indicating if the node is a physical node (its type is *[PHYSICAL_*](#PHYSICAL_BEGIN)*).
### Return value

**true** if the node is a physical node; otherwise **false**.
## bool isPlayer () const

Returns the current value indicating if the node is a player node (its type is *[PLAYER_*](#PLAYER_BEGIN)*).
### Return value

**true** if the node is a player node; otherwise **false**.
## bool isObject () const

Returns the current value indicating if the node is an object node (its type is *[OBJECT_*](#OBJECT_BEGIN)*).
### Return value

**true** if the node is an object node; otherwise **false**.
## bool isDecal () const

Returns the current value indicating if the node is a decal node (its type is *[DECAL_*](#DECAL_BEGIN)*).
### Return value

**true** if the node is a decal node; otherwise **false**.
## bool isLight () const

Returns the current value indicating if the node is a light source (its type is *[LIGHT_*](#LIGHT_BEGIN)*).
### Return value

**true** if the node is a light source; otherwise **false**.
## bool isGeodetic () const

Returns the current value indicating if the node is a geodetic-related node.
### Return value

**true** if the node is a geodetic-related node; otherwise **false**.
## bool isWorld () const

Returns the current value indicating if the node is a world node (its type is *[WORLD_*](#WORLD_BEGIN)*).
### Return value

**true** if the node is a world node; otherwise **false**.
## bool isImmovableSupported () const

Returns the current value indicating if the node can be moved to a separate spatial tree for immovable (static) objects optimizing node management.
### Return value

**true** if the node can be immovable; otherwise **false**.
## bool isSurfacesCollisionSupported () const

Returns the current value indicating if collisions with node surfaces are supported.
### Return value

**true** if collisions with node surfaces are supported; otherwise **false**.
## bool isSurfacesIntersectionSupported () const

Returns the current value indicating if intersections with node surfaces are supported.
### Return value

**true** if intersections with node surfaces are supported; otherwise **false**.
## const char * getTypeName () const

Returns the current name of the node type.
### Return value

Current name of the node type.
## Node::TYPE getType () const

Returns the current type of the node.
### Return value

Current node type identifier.
## void setID ( int id )

Sets a new runtime ID of the node. It may differ from the file ID, which is obtained via *[*getIDFromFile()*](#getIDFromFile_int)*.
> **Notice:** See also *[*Unigine::World::getNodeByID()*](../../../api/library/engine/class.world_cpp.md#getNodeByID_int_Node)* function.


### Arguments

- *int* **id** - The runtime ID of the node.

## int getID () const

Returns the current runtime ID of the node. It may differ from the file ID, which is obtained via *[*getIDFromFile()*](#getIDFromFile_int)*.
> **Notice:** See also *[*Unigine::World::getNodeByID()*](../../../api/library/engine/class.world_cpp.md#getNodeByID_int_Node)* function.


### Return value

Current runtime ID of the node.
## int getIDFromFile () const

Returns the current ID of the node loaded from `*.node` or `*.world` file. It may differ from the runtime ID of the node, which is obtained via *[*getID()*](#getID_int)*.
### Return value

Current ID of the node loaded from `*.node` or `*.world` file.
## void setSaveToWorldEnabled ( bool enabled )

Sets a new value indicating if saving to `*.world` file is enabled for the node and all its children (if any).
### Arguments

- *bool* **enabled** - Set **true** to enable saving to `*.world` file for the node and all its children (if any); **false** - to disable it.

## bool isSaveToWorldEnabled () const

Returns the current value indicating if saving to `*.world` file is enabled for the node and all its children (if any).
### Return value

**true** if saving to `*.world` file for the node and all its children (if any) is enabled ; otherwise **false**.
## bool isSaveToWorldEnabledSelf () const

Returns the current value indicating if saving to `*.world` file is enabled for the node.
### Return value

**true** if saving to `*.world` file for the node is enabled ; otherwise **false**.
## void setShowInEditorEnabled ( bool enabled )

Sets a new value indicating if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) is enabled for the node.
> **Notice:** The node shall be displayed in the hierarchy only if this option is enabled for all of its ancestors as well.


### Arguments

- *bool* **enabled** - Set **true** to enable displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) for the node; **false** - to disable it.

## bool isShowInEditorEnabled () const

Returns the current value indicating if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) is enabled for the node.
> **Notice:** The node shall be displayed in the hierarchy only if this option is enabled for all of its ancestors as well.


### Return value

**true** if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) for the node is enabled ; otherwise **false**.
## bool isShowInEditorEnabledSelf () const

Returns the current value indicating if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) is enabled for the node.
### Return value

**true** if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) for the node is enabled ; otherwise **false**.
## int getNumWorldTriggers () const

Returns the current number of World Triggers inside which the node is located at the moment.
### Return value

Current number of World Triggers inside which the node is located at the moment, or 0 if the node is not currently inside any World Trigger.
## Math:: WorldBoundSphere getSpatialBoundSphere () const

Returns the current bounding sphere with world coordinates that participates in physics calculations, but doesn't take children into account. this bounding sphere is used by the spatial tree.
### Return value

Current bounding sphere with world coordinates.
## Math:: WorldBoundBox getSpatialBoundBox () const

Returns the current bounding box with world coordinates that participates in physics calculations, but doesn't take children into account. this bounding box is used by the spatial tree.
### Return value

Current bounding box with world coordinates.
## bool isLandscapeLayer () const

Returns the current value indicating if the node is a landscape layer (its type is [*LANDSCAPE_LAYER_**](#LANDSCAPE_LAYER_BEGIN)).
### Return value

**true** if the node is a landscape layer is enabled ; otherwise **false**.
## Math:: Mat4 getIWorldTransform () const

Returns the current inverse transformation matrix of the node for transformations in the world coordinates.
### Return value

Current inverse transformation matrix.
## Math:: Vec3 getOldWorldPosition () const

Returns the current old (previous frame) position of the node in the world coordinates.
### Return value

Current old (previous frame) position of the node in the world coordinates.
## void setLifetime ( Node::LIFETIME lifetime )

Sets a new lifetime management type for the root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)) of the node, or for the node itself (if it is not a child and not possessed by any other node).
> **Notice:** Lifetime of each node in the hierarchy is defined by it's root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)). Thus, lifetime management type set for a child node that differs from the one set for the root is ignored.


### Arguments

- *[Node::LIFETIME](../../../api/library/nodes/class.node_cpp.md#LIFETIME)* **lifetime** - The lifetime management type for the root node (see the [*LIFETIME*](#LIFETIME) enum).

## Node::LIFETIME getLifetime () const

Returns the current lifetime management type for the root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)) of the node, or for the node itself (if it is not a child and not possessed by any other node).
> **Notice:** Lifetime of each node in the hierarchy is defined by it's root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)). Thus, lifetime management type set for a child node that differs from the one set for the root is ignored.


### Return value

Current lifetime management type for the root node (see the [*LIFETIME*](#LIFETIME) enum).
## Event<const Ptr < Node > &> getEventTransformChanged () const

event triggered when the node's transformation has changed. This event is triggered immediately when a change occurs, regardless of where it was made, without waiting for the next frame. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TransformChanged event handler
void transformchanged_event_handler(const Ptr<Node> & node)
{
	Log::message("\Handling TransformChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections transformchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventTransformChanged().connect(transformchanged_event_connections, transformchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventTransformChanged().connect(transformchanged_event_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling TransformChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
transformchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection transformchanged_event_connection;

// subscribe to the TransformChanged event with a handler function keeping the connection
publisher->getEventTransformChanged().connect(transformchanged_event_connection, transformchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
transformchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
transformchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the TransformChanged event via the connection
transformchanged_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A TransformChanged event handler implemented as a class member
	void event_handler(const Ptr<Node> & node)
	{
		Log::message("\Handling TransformChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventTransformChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId transformchanged_handler_id;

// subscribe to the TransformChanged event with a lambda handler function and keeping connection ID
transformchanged_handler_id = publisher->getEventTransformChanged().connect(e_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling TransformChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventTransformChanged().disconnect(transformchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TransformChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventTransformChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventTransformChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &, int> getEventPropertyNodeSlotsChanged () const

event triggered when the number of the node's property slots is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**, int **num_slots**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PropertyNodeSlotsChanged event handler
void propertynodeslotschanged_event_handler(const Ptr<Node> & node,  int num_slots)
{
	Log::message("\Handling PropertyNodeSlotsChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertynodeslotschanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventPropertyNodeSlotsChanged().connect(propertynodeslotschanged_event_connections, propertynodeslotschanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventPropertyNodeSlotsChanged().connect(propertynodeslotschanged_event_connections, [](const Ptr<Node> & node,  int num_slots) {
		Log::message("\Handling PropertyNodeSlotsChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
propertynodeslotschanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection propertynodeslotschanged_event_connection;

// subscribe to the PropertyNodeSlotsChanged event with a handler function keeping the connection
Node::getEventPropertyNodeSlotsChanged().connect(propertynodeslotschanged_event_connection, propertynodeslotschanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
propertynodeslotschanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
propertynodeslotschanged_event_connection.setEnabled(true);

// ...

// remove subscription to the PropertyNodeSlotsChanged event via the connection
propertynodeslotschanged_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A PropertyNodeSlotsChanged event handler implemented as a class member
	void event_handler(const Ptr<Node> & node,  int num_slots)
	{
		Log::message("\Handling PropertyNodeSlotsChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventPropertyNodeSlotsChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId propertynodeslotschanged_handler_id;

// subscribe to the PropertyNodeSlotsChanged event with a lambda handler function and keeping connection ID
propertynodeslotschanged_handler_id = Node::getEventPropertyNodeSlotsChanged().connect(e_connections, [](const Ptr<Node> & node,  int num_slots) {
		Log::message("\Handling PropertyNodeSlotsChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventPropertyNodeSlotsChanged().disconnect(propertynodeslotschanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PropertyNodeSlotsChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventPropertyNodeSlotsChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventPropertyNodeSlotsChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &, const Ptr < Property > &, int> getEventPropertyNodeAdd () const

event triggered when a new property is assigned to the node. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**, const Ptr<Property> & **property**, int **property_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PropertyNodeAdd event handler
void propertynodeadd_event_handler(const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index)
{
	Log::message("\Handling PropertyNodeAdd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertynodeadd_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventPropertyNodeAdd().connect(propertynodeadd_event_connections, propertynodeadd_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventPropertyNodeAdd().connect(propertynodeadd_event_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index) {
		Log::message("\Handling PropertyNodeAdd event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
propertynodeadd_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection propertynodeadd_event_connection;

// subscribe to the PropertyNodeAdd event with a handler function keeping the connection
Node::getEventPropertyNodeAdd().connect(propertynodeadd_event_connection, propertynodeadd_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
propertynodeadd_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
propertynodeadd_event_connection.setEnabled(true);

// ...

// remove subscription to the PropertyNodeAdd event via the connection
propertynodeadd_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A PropertyNodeAdd event handler implemented as a class member
	void event_handler(const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index)
	{
		Log::message("\Handling PropertyNodeAdd event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventPropertyNodeAdd().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId propertynodeadd_handler_id;

// subscribe to the PropertyNodeAdd event with a lambda handler function and keeping connection ID
propertynodeadd_handler_id = Node::getEventPropertyNodeAdd().connect(e_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index) {
		Log::message("\Handling PropertyNodeAdd event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventPropertyNodeAdd().disconnect(propertynodeadd_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PropertyNodeAdd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventPropertyNodeAdd().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventPropertyNodeAdd().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &, const Ptr < Property > &, int> getEventPropertyNodeRemove () const

event triggered when a property is removed from the list of the node's properties. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**, const Ptr<Property> & **property**, int **property_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PropertyNodeRemove event handler
void propertynoderemove_event_handler(const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index)
{
	Log::message("\Handling PropertyNodeRemove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertynoderemove_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventPropertyNodeRemove().connect(propertynoderemove_event_connections, propertynoderemove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventPropertyNodeRemove().connect(propertynoderemove_event_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index) {
		Log::message("\Handling PropertyNodeRemove event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
propertynoderemove_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection propertynoderemove_event_connection;

// subscribe to the PropertyNodeRemove event with a handler function keeping the connection
Node::getEventPropertyNodeRemove().connect(propertynoderemove_event_connection, propertynoderemove_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
propertynoderemove_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
propertynoderemove_event_connection.setEnabled(true);

// ...

// remove subscription to the PropertyNodeRemove event via the connection
propertynoderemove_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A PropertyNodeRemove event handler implemented as a class member
	void event_handler(const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index)
	{
		Log::message("\Handling PropertyNodeRemove event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventPropertyNodeRemove().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId propertynoderemove_handler_id;

// subscribe to the PropertyNodeRemove event with a lambda handler function and keeping connection ID
propertynoderemove_handler_id = Node::getEventPropertyNodeRemove().connect(e_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index) {
		Log::message("\Handling PropertyNodeRemove event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventPropertyNodeRemove().disconnect(propertynoderemove_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PropertyNodeRemove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventPropertyNodeRemove().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventPropertyNodeRemove().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &, const Ptr < Property > &, int> getEventPropertyChangeEnabled () const

event triggered when the node's property *enabled* state is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**, const Ptr<Property> & **property**, int **property_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PropertyChangeEnabled event handler
void propertychangeenabled_event_handler(const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index)
{
	Log::message("\Handling PropertyChangeEnabled event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertychangeenabled_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventPropertyChangeEnabled().connect(propertychangeenabled_event_connections, propertychangeenabled_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventPropertyChangeEnabled().connect(propertychangeenabled_event_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index) {
		Log::message("\Handling PropertyChangeEnabled event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
propertychangeenabled_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection propertychangeenabled_event_connection;

// subscribe to the PropertyChangeEnabled event with a handler function keeping the connection
Node::getEventPropertyChangeEnabled().connect(propertychangeenabled_event_connection, propertychangeenabled_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
propertychangeenabled_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
propertychangeenabled_event_connection.setEnabled(true);

// ...

// remove subscription to the PropertyChangeEnabled event via the connection
propertychangeenabled_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A PropertyChangeEnabled event handler implemented as a class member
	void event_handler(const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index)
	{
		Log::message("\Handling PropertyChangeEnabled event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventPropertyChangeEnabled().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId propertychangeenabled_handler_id;

// subscribe to the PropertyChangeEnabled event with a lambda handler function and keeping connection ID
propertychangeenabled_handler_id = Node::getEventPropertyChangeEnabled().connect(e_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property,  int property_index) {
		Log::message("\Handling PropertyChangeEnabled event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventPropertyChangeEnabled().disconnect(propertychangeenabled_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PropertyChangeEnabled events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventPropertyChangeEnabled().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventPropertyChangeEnabled().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &, int, int> getEventPropertyNodeSwap () const

event triggered when two properties swap their positions in the list of the node's properties. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**, int **index_from**, int **index_to**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PropertyNodeSwap event handler
void propertynodeswap_event_handler(const Ptr<Node> & node,  int index_from,  int index_to)
{
	Log::message("\Handling PropertyNodeSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertynodeswap_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventPropertyNodeSwap().connect(propertynodeswap_event_connections, propertynodeswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventPropertyNodeSwap().connect(propertynodeswap_event_connections, [](const Ptr<Node> & node,  int index_from,  int index_to) {
		Log::message("\Handling PropertyNodeSwap event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
propertynodeswap_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection propertynodeswap_event_connection;

// subscribe to the PropertyNodeSwap event with a handler function keeping the connection
Node::getEventPropertyNodeSwap().connect(propertynodeswap_event_connection, propertynodeswap_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
propertynodeswap_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
propertynodeswap_event_connection.setEnabled(true);

// ...

// remove subscription to the PropertyNodeSwap event via the connection
propertynodeswap_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A PropertyNodeSwap event handler implemented as a class member
	void event_handler(const Ptr<Node> & node,  int index_from,  int index_to)
	{
		Log::message("\Handling PropertyNodeSwap event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventPropertyNodeSwap().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId propertynodeswap_handler_id;

// subscribe to the PropertyNodeSwap event with a lambda handler function and keeping connection ID
propertynodeswap_handler_id = Node::getEventPropertyNodeSwap().connect(e_connections, [](const Ptr<Node> & node,  int index_from,  int index_to) {
		Log::message("\Handling PropertyNodeSwap event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventPropertyNodeSwap().disconnect(propertynodeswap_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PropertyNodeSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventPropertyNodeSwap().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventPropertyNodeSwap().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &, const Ptr < Property > &> getEventPropertySurfaceAdd () const

event triggered when a property is assigned to the object's surface. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**, const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PropertySurfaceAdd event handler
void propertysurfaceadd_event_handler(const Ptr<Node> & node,  const Ptr<Property> & property)
{
	Log::message("\Handling PropertySurfaceAdd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertysurfaceadd_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventPropertySurfaceAdd().connect(propertysurfaceadd_event_connections, propertysurfaceadd_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventPropertySurfaceAdd().connect(propertysurfaceadd_event_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property) {
		Log::message("\Handling PropertySurfaceAdd event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
propertysurfaceadd_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection propertysurfaceadd_event_connection;

// subscribe to the PropertySurfaceAdd event with a handler function keeping the connection
Node::getEventPropertySurfaceAdd().connect(propertysurfaceadd_event_connection, propertysurfaceadd_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
propertysurfaceadd_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
propertysurfaceadd_event_connection.setEnabled(true);

// ...

// remove subscription to the PropertySurfaceAdd event via the connection
propertysurfaceadd_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A PropertySurfaceAdd event handler implemented as a class member
	void event_handler(const Ptr<Node> & node,  const Ptr<Property> & property)
	{
		Log::message("\Handling PropertySurfaceAdd event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventPropertySurfaceAdd().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId propertysurfaceadd_handler_id;

// subscribe to the PropertySurfaceAdd event with a lambda handler function and keeping connection ID
propertysurfaceadd_handler_id = Node::getEventPropertySurfaceAdd().connect(e_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property) {
		Log::message("\Handling PropertySurfaceAdd event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventPropertySurfaceAdd().disconnect(propertysurfaceadd_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PropertySurfaceAdd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventPropertySurfaceAdd().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventPropertySurfaceAdd().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &, const Ptr < Property > &> getEventPropertySurfaceRemove () const

event triggered when a property is removed from the object's surface. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**, const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PropertySurfaceRemove event handler
void propertysurfaceremove_event_handler(const Ptr<Node> & node,  const Ptr<Property> & property)
{
	Log::message("\Handling PropertySurfaceRemove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertysurfaceremove_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventPropertySurfaceRemove().connect(propertysurfaceremove_event_connections, propertysurfaceremove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventPropertySurfaceRemove().connect(propertysurfaceremove_event_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property) {
		Log::message("\Handling PropertySurfaceRemove event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
propertysurfaceremove_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection propertysurfaceremove_event_connection;

// subscribe to the PropertySurfaceRemove event with a handler function keeping the connection
Node::getEventPropertySurfaceRemove().connect(propertysurfaceremove_event_connection, propertysurfaceremove_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
propertysurfaceremove_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
propertysurfaceremove_event_connection.setEnabled(true);

// ...

// remove subscription to the PropertySurfaceRemove event via the connection
propertysurfaceremove_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A PropertySurfaceRemove event handler implemented as a class member
	void event_handler(const Ptr<Node> & node,  const Ptr<Property> & property)
	{
		Log::message("\Handling PropertySurfaceRemove event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventPropertySurfaceRemove().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId propertysurfaceremove_handler_id;

// subscribe to the PropertySurfaceRemove event with a lambda handler function and keeping connection ID
propertysurfaceremove_handler_id = Node::getEventPropertySurfaceRemove().connect(e_connections, [](const Ptr<Node> & node,  const Ptr<Property> & property) {
		Log::message("\Handling PropertySurfaceRemove event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventPropertySurfaceRemove().disconnect(propertysurfaceremove_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PropertySurfaceRemove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventPropertySurfaceRemove().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventPropertySurfaceRemove().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &> getEventCacheNodeAdd () const

event triggered when a node is added to cache. Occurs once upon calling [NodeReference::create()](../../../api/library/nodes/class.nodereference_cpp.md#NodeReference_constchar) or [*World::loadNode()*](../../../api/library/engine/class.world_cpp.md#loadNode_cstr_int_Node). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CacheNodeAdd event handler
void cachenodeadd_event_handler(const Ptr<Node> & node)
{
	Log::message("\Handling CacheNodeAdd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections cachenodeadd_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventCacheNodeAdd().connect(cachenodeadd_event_connections, cachenodeadd_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventCacheNodeAdd().connect(cachenodeadd_event_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling CacheNodeAdd event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
cachenodeadd_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection cachenodeadd_event_connection;

// subscribe to the CacheNodeAdd event with a handler function keeping the connection
Node::getEventCacheNodeAdd().connect(cachenodeadd_event_connection, cachenodeadd_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
cachenodeadd_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
cachenodeadd_event_connection.setEnabled(true);

// ...

// remove subscription to the CacheNodeAdd event via the connection
cachenodeadd_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A CacheNodeAdd event handler implemented as a class member
	void event_handler(const Ptr<Node> & node)
	{
		Log::message("\Handling CacheNodeAdd event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventCacheNodeAdd().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId cachenodeadd_handler_id;

// subscribe to the CacheNodeAdd event with a lambda handler function and keeping connection ID
cachenodeadd_handler_id = Node::getEventCacheNodeAdd().connect(e_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling CacheNodeAdd event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventCacheNodeAdd().disconnect(cachenodeadd_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CacheNodeAdd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventCacheNodeAdd().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventCacheNodeAdd().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &> getEventNodeLoad () const

event triggered when a node is loaded from a file. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the NodeLoad event handler
void nodeload_event_handler(const Ptr<Node> & node)
{
	Log::message("\Handling NodeLoad event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeload_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventNodeLoad().connect(nodeload_event_connections, nodeload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventNodeLoad().connect(nodeload_event_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeLoad event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
nodeload_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection nodeload_event_connection;

// subscribe to the NodeLoad event with a handler function keeping the connection
Node::getEventNodeLoad().connect(nodeload_event_connection, nodeload_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
nodeload_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
nodeload_event_connection.setEnabled(true);

// ...

// remove subscription to the NodeLoad event via the connection
nodeload_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A NodeLoad event handler implemented as a class member
	void event_handler(const Ptr<Node> & node)
	{
		Log::message("\Handling NodeLoad event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventNodeLoad().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId nodeload_handler_id;

// subscribe to the NodeLoad event with a lambda handler function and keeping connection ID
nodeload_handler_id = Node::getEventNodeLoad().connect(e_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeLoad event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventNodeLoad().disconnect(nodeload_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all NodeLoad events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventNodeLoad().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventNodeLoad().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &> getEventNodeRemove () const

event triggered when the node is deleted. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the NodeRemove event handler
void noderemove_event_handler(const Ptr<Node> & node)
{
	Log::message("\Handling NodeRemove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections noderemove_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventNodeRemove().connect(noderemove_event_connections, noderemove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventNodeRemove().connect(noderemove_event_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeRemove event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
noderemove_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection noderemove_event_connection;

// subscribe to the NodeRemove event with a handler function keeping the connection
Node::getEventNodeRemove().connect(noderemove_event_connection, noderemove_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
noderemove_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
noderemove_event_connection.setEnabled(true);

// ...

// remove subscription to the NodeRemove event via the connection
noderemove_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A NodeRemove event handler implemented as a class member
	void event_handler(const Ptr<Node> & node)
	{
		Log::message("\Handling NodeRemove event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventNodeRemove().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId noderemove_handler_id;

// subscribe to the NodeRemove event with a lambda handler function and keeping connection ID
noderemove_handler_id = Node::getEventNodeRemove().connect(e_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeRemove event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventNodeRemove().disconnect(noderemove_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all NodeRemove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventNodeRemove().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventNodeRemove().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &> getEventNodeChangeEnabled () const

event triggered when the node's *enabled* state is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the NodeChangeEnabled event handler
void nodechangeenabled_event_handler(const Ptr<Node> & node)
{
	Log::message("\Handling NodeChangeEnabled event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodechangeenabled_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventNodeChangeEnabled().connect(nodechangeenabled_event_connections, nodechangeenabled_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventNodeChangeEnabled().connect(nodechangeenabled_event_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeChangeEnabled event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
nodechangeenabled_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection nodechangeenabled_event_connection;

// subscribe to the NodeChangeEnabled event with a handler function keeping the connection
Node::getEventNodeChangeEnabled().connect(nodechangeenabled_event_connection, nodechangeenabled_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
nodechangeenabled_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
nodechangeenabled_event_connection.setEnabled(true);

// ...

// remove subscription to the NodeChangeEnabled event via the connection
nodechangeenabled_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A NodeChangeEnabled event handler implemented as a class member
	void event_handler(const Ptr<Node> & node)
	{
		Log::message("\Handling NodeChangeEnabled event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventNodeChangeEnabled().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId nodechangeenabled_handler_id;

// subscribe to the NodeChangeEnabled event with a lambda handler function and keeping connection ID
nodechangeenabled_handler_id = Node::getEventNodeChangeEnabled().connect(e_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling NodeChangeEnabled event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventNodeChangeEnabled().disconnect(nodechangeenabled_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all NodeChangeEnabled events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventNodeChangeEnabled().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventNodeChangeEnabled().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &, const Ptr < Node > &> getEventNodeClone () const

event triggered when copying a node via [Node::clone()](../../../api/library/nodes/class.node_cpp.md#clone_Node). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node_clone**, const Ptr<Node> & **node_original**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the NodeClone event handler
void nodeclone_event_handler(const Ptr<Node> & node_clone,  const Ptr<Node> & node_original)
{
	Log::message("\Handling NodeClone event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeclone_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventNodeClone().connect(nodeclone_event_connections, nodeclone_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventNodeClone().connect(nodeclone_event_connections, [](const Ptr<Node> & node_clone,  const Ptr<Node> & node_original) {
		Log::message("\Handling NodeClone event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
nodeclone_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection nodeclone_event_connection;

// subscribe to the NodeClone event with a handler function keeping the connection
Node::getEventNodeClone().connect(nodeclone_event_connection, nodeclone_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
nodeclone_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
nodeclone_event_connection.setEnabled(true);

// ...

// remove subscription to the NodeClone event via the connection
nodeclone_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A NodeClone event handler implemented as a class member
	void event_handler(const Ptr<Node> & node_clone,  const Ptr<Node> & node_original)
	{
		Log::message("\Handling NodeClone event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventNodeClone().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId nodeclone_handler_id;

// subscribe to the NodeClone event with a lambda handler function and keeping connection ID
nodeclone_handler_id = Node::getEventNodeClone().connect(e_connections, [](const Ptr<Node> & node_clone,  const Ptr<Node> & node_original) {
		Log::message("\Handling NodeClone event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventNodeClone().disconnect(nodeclone_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all NodeClone events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventNodeClone().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventNodeClone().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Node > &, const Ptr < Node > &> getEventNodeSwap () const

event triggered when swapping a node via [Node::swap()](../../../api/library/nodes/class.node_cpp.md#swap_Node_void). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **first_node**, const Ptr<Node> & **second_node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the NodeSwap event handler
void nodeswap_event_handler(const Ptr<Node> & first_node,  const Ptr<Node> & second_node)
{
	Log::message("\Handling NodeSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeswap_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node::getEventNodeSwap().connect(nodeswap_event_connections, nodeswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node::getEventNodeSwap().connect(nodeswap_event_connections, [](const Ptr<Node> & first_node,  const Ptr<Node> & second_node) {
		Log::message("\Handling NodeSwap event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
nodeswap_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection nodeswap_event_connection;

// subscribe to the NodeSwap event with a handler function keeping the connection
Node::getEventNodeSwap().connect(nodeswap_event_connection, nodeswap_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
nodeswap_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
nodeswap_event_connection.setEnabled(true);

// ...

// remove subscription to the NodeSwap event via the connection
nodeswap_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A NodeSwap event handler implemented as a class member
	void event_handler(const Ptr<Node> & first_node,  const Ptr<Node> & second_node)
	{
		Log::message("\Handling NodeSwap event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Node::getEventNodeSwap().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId nodeswap_handler_id;

// subscribe to the NodeSwap event with a lambda handler function and keeping connection ID
nodeswap_handler_id = Node::getEventNodeSwap().connect(e_connections, [](const Ptr<Node> & first_node,  const Ptr<Node> & second_node) {
		Log::message("\Handling NodeSwap event (lambda).\n");
	}
);

// remove the subscription later using the ID
Node::getEventNodeSwap().disconnect(nodeswap_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all NodeSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node::getEventNodeSwap().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Node::getEventNodeSwap().setEnabled(true);

```

</details>

### Return value

Event instance.
## bool isCache () const

Returns the current value indicating whether the node or any of its parent nodes are stored in the cache.
### Return value

**true** if the node in the cache is enabled ; otherwise **false**.
## const char * getSrcFilePath () const

Returns the current path to the source of the node. For example, a relative path to the `*.world` file with a description of this node, or the identifier of the source `*.node` in the format `guid://...`
### Return value

Current path to the source of the node.
## String getHierarchyPath () const

Returns the current [nodes hierarchy](../../../principles/world_structure/index.md#nodes_hierarchy). Displays the node name and the names of all its parent nodes as specified in *World Hierarchy* window.
### Return value

Current node name and the names of all its parent nodes.
## String getInfo () const

Returns the current the information about the given node: type, name, ID, file path, hierarchy.
### Return value

Current node information.
---

## Ptr < Node > getAncestor ( int num ) const

Returns a node ancestor by its number.
### Arguments

- *int* **num** - Ancestor ID.

### Return value

Ancestor node.
## Ptr < Node > getChild ( int num ) const

Returns a node child by its number.
### Arguments

- *int* **num** - Child ID.

### Return value

Child node.
## bool isChild ( const Ptr < Node > & n ) const

Checks if a given node is a child of the node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **n** - Node to check.

### Return value

true if the given node is a child; otherwise, false.
## void setChildIndex ( const Ptr < Node > & n , int index )

Sets the index for a given child node of the node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **n** - Child node.
- *int* **index** - Node index.

## int getChildIndex ( const Ptr < Node > & n )

Returns the index of a given child node of the node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **n** - Child node.

### Return value

Node index.
## void setData ( const char * name , const char * data )

Sets user data associated with the node.
- If the node was loaded from the `*.node` file, data is saved directly into the data tag of this file.
- If the node is loaded from the `*.world` file, data is saved into the Node data tag of the `*.world` file.
- If the node is loaded from the `*.world` file as a NodeReference, data will be saved to the NodeReference data tag of the `*.world` file.


### Arguments

- *const char ** **name** - String containing a key identifying user data to be stored in the `*.node` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.
- *const char ** **data** - New user data. Data can contain an XML formatted string.

## const char * getData ( const char * name )

Returns user data associated with the node.
- If the node was loaded from the `*.node` file, data from the data tag of this file is returned.
- If the node is loaded from the `*.world` file, data from the Node data tag of the `*.world` file is returned.
- If the node is loaded from the `*.world` file as a NodeReference, data from the NodeReference data tag of the `*.world` file is returned.


### Arguments

- *const char ** **name** - String containing a key identifying user data stored in the `*.node` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

### Return value

User string data. Data can be an xml formatted string.
## void updateEnabled ( )

Updates node's internal state according to the current "*enabled*" state.
## bool isEnabledSelf ( ) const

Returns a value indicating if the node is enabled.
### Return value

true if the node is enabled; otherwise, false.
## void getHierarchy ( Vector < Ptr < Node >> & OUT_hierarchy )

Retrieves the whole hierarchy of the node and puts it to the hierarchy buffer.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_hierarchy** - Hierarchy buffer. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Ptr < Node > getNode ( int id )

Returns a node pointer.
### Arguments

- *int* **id** - Node identifier.

### Return value

Node pointer.
## bool isNode ( const Ptr < Node > & node )

Check the node pointer.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node pointer.

### Return value

true if the node is valid; otherwise, false.
## bool isNode ( int id )

Check the node pointer.
### Arguments

- *int* **id** - Node pointer.

### Return value

true if the node is valid; otherwise, false.
## int addProperty ( const char * name )

Inherits a new property from the one with the given name and adds it to the list of properties associated with the node. The inherited property will be internal, such properties are saved in a `*.world` or `*.node` file.
### Arguments

- *const char ** **name** - Name of the property to be added.

### Return value

Index of the new node property if it was added successfully; otherwise, -1.
## int addProperty ( const UGUID & guid )

Inherits a new property from the one with the given GUID and adds it to the list of properties associated with the node. The inherited property will be internal, such properties are saved in a `*.world` or `*.node` file.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to be added.

### Return value

Index of the new node property if it was added successfully; otherwise, -1.
## int addProperty ( const Ptr < Property > & property )

Inherits a new property from the specified one and adds it to the list of properties associated with the node. The inherited property will be internal, such properties are saved in a `*.world` or `*.node` file.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Property to be added.

### Return value

Index of the new node property if it was added successfully; otherwise, -1.
## bool insertProperty ( int num , const char * name )

Inserts the property with the specified name at the specified position.
### Arguments

- *int* **num** - Position at which a new property is to be inserted, in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *const char ** **name** - Name of the property to be inserted.

### Return value

true if the property with the specified name was successfully inserted at the specified position; otherwise, false.
## bool insertProperty ( int num , const UGUID & guid )

Inserts the property with the specified GUID at the specified position.
### Arguments

- *int* **num** - Position at which a new property is to be inserted, in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to be inserted.

### Return value

true if the property with the specified GUID was successfully inserted at the specified position; otherwise, false.
## bool insertProperty ( int num , const Ptr < Property > & property )

Inserts the specified property at the specified position.
### Arguments

- *int* **num** - Position at which a new property is to be inserted, in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Property to be added.

### Return value

true if the specified property was successfully inserted at the specified position; otherwise, false.
## bool insertProperty ( int num , const UGUID & guid , const UGUID & new_guid )

### Arguments

- *int* **num**
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid**
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_guid**

## bool insertProperty ( int num , const Ptr < Property > & property , const UGUID & new_guid )

### Arguments

- *int* **num**
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property**
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_guid**

## bool setProperty ( const char * name )

Updates the first node property (the one with a 0 index) in the list of properties associated with the node. A new internal property inherited from the one with the specified name will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *const char ** **name** - Name of the property to be set.

### Return value

true if the node property is updated successfully; otherwise, false.
## bool setProperty ( const UGUID & guid )

Updates the first node property (the one with a 0 index) in the list of properties associated with the node. A new internal property inherited from the one with the specified GUID will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to be set.

### Return value

true if the node property is updated successfully; otherwise, false.
## bool setProperty ( const Ptr < Property > & property )

Updates the first node property (the one with a 0 index) in the list of properties associated with the node. A new internal property inherited from the one specified will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Property to be set.

### Return value

true if the node property is updated successfully; otherwise, false.
## bool setProperty ( int num , const char * name )

Updates the node property with the specified number. A new internal property inherited from the one with the specified name will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *const char ** **name** - Name of the property to be set.

### Return value

true if the specified node property is updated successfully; otherwise, false.
## bool setProperty ( int num , const UGUID & guid )

Updates the node property with the specified number. A new internal property inherited from the one with the specified GUID will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to be set.

### Return value

true if the specified node property is updated successfully; otherwise, false.
## bool setProperty ( int num , const Ptr < Property > & property )

Updates the node property with the specified number. A new internal property inherited from the specified one will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Property to be set.

### Return value

true if the specified node property is updated successfully; otherwise, false.
## bool setProperty ( int num , const UGUID & guid , const UGUID & new_guid )

### Arguments

- *int* **num**
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid**
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_guid**

## bool setProperty ( int num , const Ptr < Property > & property , const UGUID & new_guid )

### Arguments

- *int* **num**
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property**
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_guid**

## void setPropertyEnabled ( int num , bool enable )

Enables or disables the node property with the specified number.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *bool* **enable** - true to enable the specified node property, false to disable it.

## bool isPropertyEnabled ( int num ) const

Returns a value indicating if the node property with the specified number is enabled.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

true if the specified property is enabled; otherwise, false.
## void swapProperty ( int from_num , int to_num )

Swaps two properties with specified numbers in the list of properties associated with the node.
> **Notice:** The order of properties in the list determines the execution sequence of logic of corresponding [components](../../../principles/component_system/index.md) (if any).


### Arguments

- *int* **from_num** - Number of the first node property to be swapped, in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *int* **to_num** - Number of the second node property to be swapped, in the range from 0 to the [total number of node properties](#getNumProperties_int).

## void removeProperty ( int num )

Removes the node property with the specified number.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

## void removeProperty ( const char * name )

Removes the node property that has the specified name.
> **Notice:** If several properties with the same name are associated with the node, only the first one will be removed.


### Arguments

- *const char ** **name** - Name of the node property to be removed.

## void removeProperty ( const UGUID & guid )

Removes the node property that has the GUID or parent GUID equal to the specified one.
> **Notice:** If several such properties are associated with the node, only the first one will be removed.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to be removed (or GUID of its parent).

## void removeProperty ( const Ptr < Property > & property )

Removes the specified node property or a node property inherited from it.
> **Notice:** If several such properties are associated with the node, only the first one will be removed.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Node property to be removed.

## void clearProperties ( )

Clears the list of properties associated with the node.
## Ptr < Property > getProperty ( int num ) const

Returns a node property with the specified number if it exists.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

Node property smart pointer, if exists; otherwise, NULL.
## const char * getPropertyName ( int num ) const

Returns the name of a node property with the specified number.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

Property name, if exists; otherwise, NULL.
## int findProperty ( const char * name ) const

Searches for a property with the specified name among the ones assigned to the node.
### Arguments

- *const char ** **name** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a node property to be found.

### Return value

Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int) if such a property exists; otherwise -1.
## int findProperty ( const UGUID & guid ) const

Searches for a property with the specified [GUID](../../../api/library/filesystem/class.uguid_cpp.md) among the ones assigned to the node.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a node property to be found.

### Return value

Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int) if such a property exists; otherwise -1.
## int findProperty ( const Ptr < Property > & property ) const

Searches for a specified property among the ones assigned to the node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Node property to be found.

### Return value

Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int) if such a property exists; otherwise -1.
## bool hasQueryForce ( ) const

Returns a value indicating if the *[Culled By Occlusion Query](../../../editor2/node_parameters/transformation_common/index.md#query)*option is force-enabled for the node by the Engine.
### Return value

true if the *[Culled By Occlusion Query](../../../editor2/node_parameters/transformation_common/index.md#query)*option is force-enabled for the node by the Engine; otherwise, false.
## void setRotation ( const Math:: quat & rot , bool identity = 0 )

Sets the node rotation.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **rot** - Quaternion representing node rotation in the local space.
- *bool* **identity** - Flag indicating if node's scale is to be ignored or taken into account: > **Notice:** - It is recommended to set this flag for all non-scaled nodes to improve performance and accuracy. > - **Scaling of nodes should be avoided whenever possible**, as it requires addidional calculations and may lead to error accumulation.

  - false - node's scale is taken into account. In this case additional calculations are performed to extract current node's scale and apply it when building the final transformation matrix. These additional operations reduce performance and may lead to error accumulation.
  - true - node's scale is ignored (assumed to be equal to **1** along all axes). Thus, the number of calculations performed for each rotation is reduced and error accumulation is minimal.

## Math:: quat getRotation ( ) const

Returns the node rotation.
### Return value

Quaternion representing node rotation in the local space.
## void setWorldRotation ( const Math:: quat & rot , bool identity = 0 )

Sets the node rotation in the world space.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **rot** - Node rotation in the world space.
- *bool* **identity** - Flag indicating if node's scale is to be ignored or taken into account: > **Notice:** - It is recommended to set this flag for all non-scaled nodes to improve performance and accuracy. > - **Scaling of nodes should be avoided whenever possible**, as it requires addidional calculations and may lead to error accumulation.

  - false - node's scale is taken into account. In this case additional calculations are performed to extract current node's scale and apply it when building the final transformation matrix. These additional operations reduce performance and may lead to error accumulation.
  - true - node's scale is ignored (assumed to be equal to **1** along all axes). Thus, the number of calculations performed for each rotation is reduced and error accumulation is minimal.

## Math:: quat getWorldRotation ( ) const

Returns the node rotation in the world space.
### Return value

Node rotation in the world space.
## void setTransformWithoutChildren ( const Math:: Mat4 & transform )

Sets the transformation matrix for the node in local coordinates (transformations of all node's children are not affected). This method can be used to change node's transformation relative to its children.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - New transformation matrix to be set for the node (local coordinates).

## Node::TYPE getTypeID ( const char * type )

Returns the ID of a node type with a given name.
### Arguments

- *const char ** **type** - Node type name.

### Return value

Node type ID, if such type exists; otherwise, -1.
## const char * getTypeName ( Node::TYPE type )

Returns the name of a node type with a given ID.
### Arguments

- *[Node::TYPE](../../../api/library/nodes/class.node_cpp.md#TYPE)* **type** - Node type ID.

### Return value

Node type name.
## void setVariable ( const char * name , const Variable & v )

Sets the value of a variable with a given name. If such variable does not exist it will be added with a specified value.
```cpp
NodeDummyPtr container;
if(container->hasVariable("key1")) {
	container->setVariable("key1", Variable(42));
}
Variable value = container->getVariable("key1");
container->removeVariable("key1");

```


### Arguments

- *const char ** **name** - Variable name.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - Variable value.

## Variable getVariable ( const char * name ) const

Returns the variable with a given name.
```cpp
NodeDummyPtr container;
if(container->hasVariable("key1")) {
	container->setVariable("key1", Variable(42));
}
Variable value = container->getVariable("key1");
container->removeVariable("key1");

```


### Arguments

- *const char ** **name** - Variable name.

### Return value

Variable if it exists; otherwise, variable with 0 value.
## void setWorldParent ( const Ptr < Node > & n )

Sets the new parent of the node. Transformations of the current node will be done in the world coordinates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **n** - New parent node or NULL (0).

## void setWorldTransformWithoutChildren ( const Math:: Mat4 & transform )

Sets the transformation matrix for the node in world coordinates (transformations of all node's children are not affected). This method can be used to change node's transformation relative to its children.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - New transformation matrix to be set for the node (world coordinates).

## Math:: vec3 getBodyWorldVelocity ( const Math:: Vec3 & point ) const

Returns linear velocity of a point of the node's physical body in the world space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point**

### Return value

Linear velocity in the world space.
## void addChild ( const Ptr < Node > & n )

Adds a child to the node. Transformations of the new child will be done in the coordinates of the parent.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **n** - New child node.

## void addWorldChild ( const Ptr < Node > & n )

Adds a child to the node. Transformations of the new child will be done in the world coordinates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **n** - New child node.

## Ptr < Node > clone ( ) const

Clones the node.
### Return value

Cloned node.
## int findAncestor ( int type ) const

Returns the ID of node's ancestor of a given type.
### Arguments

- *int* **type** - Ancestor type identifier. One of the [*NODE_**](#NODE_DUMMY) pre-defined variables.

### Return value

Ancestor ID if it exists; otherwise -1.
## int findAncestor ( const char * name ) const

Returns the ID of node's ancestor with a given name.
### Arguments

- *const char ** **name** - Ancestor name.

### Return value

Ancestor ID if it exists; otherwise -1.
## int findChild ( const char * name ) const

Searches for a child node with a given name among the children of the node.
### Arguments

- *const char ** **name** - Name of the child node.

### Return value

Child node number, if it is found; otherwise, -1.
## Ptr < Node > findNode ( const char * name , int recursive = 0 ) const

Searches for a node with a given name among the children of the node.
### Arguments

- *const char ** **name** - Name of the child node to search for.
- *int* **recursive** - **1** if the search is recursive (i.e. performed for children of child nodes); otherwise, **0**.

### Return value

Child node, if it is found; otherwise, NULL.
## void findNodes ( const char * name , Vector < Ptr < Node >> & OUT_nodes , int recursive = 0 ) const

Searches for a node with a given name among the children of the node and puts them to the specified output *nodes* buffer.
### Arguments

- *const char ** **name** - Name of the node to search for.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Output buffer to which all found nodes with the specified name will be put. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **recursive** - **1** if the search is recursive (i.e. performed for children of child nodes); otherwise, **0**.

## int hasVariable ( const char * name )

Returns a value indicating if the node has a variable parameter with a given name.
```cpp
NodeDummyPtr container;
if(container->hasVariable("key1")) {
	container->setVariable("key1", Variable(42));
}
Variable value = container->getVariable("key1");
container->removeVariable("key1");

```


### Arguments

- *const char ** **name** - Variable name.

### Return value

**1** if the node has a variable parameter with a given name; otherwise, **0**.
## int hasVariable ( )

Returns a value indicating if the node has a single unnamed variable parameter.
### Return value

1 if the node has a single unnamed variable parameter; otherwise, 0.
## bool loadWorld ( const Ptr < Xml > & xml )

Loads a node state from the Xml.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - Xml smart pointer.

### Return value

true if the node state is loaded successfully; otherwise, false.
## void removeChild ( const Ptr < Node > & n )

Removes a child node (added by the *[addChild()](#addChild_Node_void)* method) from the list of children.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **n** - Child node to remove.

## void removeVariable ( const char * name )

Removes a variable parameter with a given name.
```cpp
NodeDummyPtr container;
if(container->hasVariable("key1")) {
	container->setVariable("key1", Variable(42));
}
Variable value = container->getVariable("key1");
container->removeVariable("key1");

```


### Arguments

- *const char ** **name** - Variable parameter name.

### Return value

## void removeWorldChild ( const Ptr < Node > & n )

Removes a child node (added by the *[addWorldChild()](#addWorldChild_Node_void)* method) from the list of children.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **n** - Child node to remove.

## void renderVisualizer ( )

Renders a bounding box / sphere of the object.
> **Notice:** You should enable the engine visualizer by the `show_visualizer 1` console command.


## bool saveState ( const Ptr < Stream > & stream ) const

Saves a node state to a binary stream.
**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// initialize a node and set its state
NodeDummyPtr node = NodeDummy::create();
node->setPosition(Vec3(1, 1, 0));

// save state
BlobPtr blob_state = Blob::create();
node->saveState(blob_state);

// change state
node->setPosition(Vec3(0, 0, 0));

// restore state
blob_state->seekSet(0);		// returning the carriage to the start of the blob
node->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true if node state is successfully saved; otherwise, false.
## bool restoreState ( const Ptr < Stream > & stream )

Restores a node state from a binary stream.
**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```cpp
// initialize a node and set its state
NodeDummyPtr node = NodeDummy::create();
node->setPosition(Vec3(1, 1, 0));

// save state
BlobPtr blob_state = Blob::create();
node->saveState(blob_state);

// change state
node->setPosition(Vec3(0, 0, 0));

// restore state
blob_state->seekSet(0);		// returning the carriage to the start of the blob
node->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true if node state is successfully restored; otherwise, false.
## bool saveWorld ( const Ptr < Xml > & xml ) const

Saves the node into the Xml.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - Xml smart pointer.

### Return value

true if the node is successfully saved; otherwise, false.
## void swap ( const Ptr < Node > & n ) const

Swaps two nodes.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **n** - Node to swap.

## Math:: vec3 toLocal ( const Math:: Vec3 & p ) const

Converts a given vector in the world space to the node's local space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p** - Vector in the world space.

### Return value

Vector in the local space.
## Math:: Vec3 toWorld ( const Math:: vec3 & p ) const

Converts a given vector in the local space to the world space.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **p** - Vector in the local space.

### Return value

Vector in the world space.
## void translate ( const Math:: Vec3 & t )

Translates the node relative to its local coordinate system: the parent node transformation isn't taken into account.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **t** - Translation vector.

## void translate ( Math::Scalar x , Math::Scalar y , Math::Scalar z )

Translates the node relative to its local coordinate system: the parent node transformation isn't taken into account.
### Arguments

- *Math::Scalar* **x** - Node translation along the X axis, in units.
- *Math::Scalar* **y** - Node translation along the Y axis, in units.
- *Math::Scalar* **z** - Node translation along the Z axis, in units.

## void worldTranslate ( const Math:: Vec3 & t )

Translates the node in the world space using the specified vector.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **t** - Translation vector.

## void worldTranslate ( Math::Scalar x , Math::Scalar y , Math::Scalar z )

Translates the node in the world space using the values specified for the corresponding axes.
### Arguments

- *Math::Scalar* **x** - Node translation along the X axis, in units.
- *Math::Scalar* **y** - Node translation along the Y axis, in units.
- *Math::Scalar* **z** - Node translation along the Z axis, in units.

## void worldLookAt ( const Math:: Vec3 & target , const Math:: vec3 & up )

Reorients the node to "look" at the target point and sets the given up vector:
- If the node is a [Player-related](#isPlayer_int) one, it will "look" at the target point along the negative Z axis. The Y axis will be oriented along the specified up vector.
- Other nodes will "look" at the target point along the Y axis. The Z axis will be oriented along the specified up vector.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **target** - Coordinates of the target point in the world space.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **up** - Up vector of the node in the world space. By default, the up vector is oriented along the Z axis.

## void worldLookAt ( const Math:: Vec3 & target )

Reorients the node to "look" at the target point. The up vector is oriented along the Z axis.
- If the node is a [Player-related](#isPlayer_int) one, it will "look" at the target point along the negative Z axis. The Y axis will be oriented along the world Z axis.
- Other nodes will "look" at the target point along the Y axis.


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **target** - Coordinates of the target point in the world space.

## void rotate ( const Math:: quat & r )

Rotates the node relative to its local coordinate system: the parent node transformation isn't taken into account. Rotation is determined by the specified [quaternion](../../../api/library/math/class.quat_cpp.md).
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **r** - Rotation quaternion.

## void rotate ( const Math:: vec3 & angles )

Rotates the node in the local space. Rotation is determined by Euler angles passed as a [vec3](../../../api/library/math/class.vec3_cpp.md) vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **angles**

## void rotate ( float angle_x , float angle_y , float angle_z )

Rotates the node in the world space according to specified Euler angles.
### Arguments

- *float* **angle_x** - Pitch angle, in degrees.
- *float* **angle_y** - Roll angle, in degrees.
- *float* **angle_z** - Yaw angle, in degrees.

## void worldRotate ( const Math:: quat & r )

Rotates the node in the world space. Rotation is determined by the specified [quaternion](../../../api/library/math/class.quat_cpp.md).
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **r** - Rotation quaternion.

## void worldRotate ( const Math:: vec3 & angles )

Rotates the node in the world space. Rotation is determined by Euler angles passed as a [vec3](../../../api/library/math/class.vec3_cpp.md) vector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **angles** - Vector containing Euler angles (Pitch, Yaw, Roll).

## void worldRotate ( float angle_x , float angle_y , float angle_z )

Rotates the node in the world space according to specified Euler angles.
### Arguments

- *float* **angle_x** - Pitch angle, in degrees.
- *float* **angle_y** - Roll angle, in degrees.
- *float* **angle_z** - Yaw angle, in degrees.

## void setDirection ( const Math:: vec3 & dir , const Math:: vec3 & up , MathLib::AXIS axis = AXIS_NZ )

Updates the direction vector of the node and reorients this node: the specified axis of the node becomes oriented along the specified vector in local coordinates. For example, after running the code below, you will get the X axis of the node pointed along the Y axis in local coordinates.
```cpp
// get the node
NodePtr node = World::getNodeByName("material_ball");
// set the X axis to be pointed along the Y axis in local coordinates
node->setDirection(vec3(0.0f,1.0f,0.0f),vec3(0.0f,0.0f,1.0f),Math::AXIS_X);

```


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **dir** - New direction vector in local coordinates. The direction vector always has unit length.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **up** - New up vector in local coordinates. If you skip this argument, the Z axis (in local coordinates) will be used. Note that the specified up vector is a hint vector only: the node's up vector points in the direction hinted by the specified up vector. The node's up vector matches the specified up vector (*up*) only if it is perpendicular to the specified direction vector (*dir*).
- *MathLib::AXIS* **axis** - Axis along which the direction vector should be pointed. The default is the negative Z axis.

## Math:: vec3 getDirection ( MathLib::AXIS axis = AXIS_NZ ) const

Returns the normalized direction vector pointing along the given node axis in local coordinates (i.e. relative to the node's parent). By default, the direction vector pointing along the negative Z axis of the node (in local coordinates) is returned. The direction vector always has a unit length.
```cpp
node->getDirection(node->isPlayer() ? Math::AXIS_NZ : Math::AXIS_Y); // forward direction vector
node->getDirection(node->isPlayer() ? Math::AXIS_Z : Math::AXIS_NY); // backward direction vector
node->getDirection(node->isPlayer() ? Math::AXIS_Y : Math::AXIS_Z); // upward direction vector
node->getDirection(node->isPlayer() ? Math::AXIS_NY : Math::AXIS_NZ); // down direction vector
node->getDirection(Math::AXIS_X); // right direction vector
node->getDirection(Math::AXIS_NX); // left direction vector

```


### Arguments

- *MathLib::AXIS* **axis** - Axis along which the direction vector points. The default is the negative Z axis.

### Return value

Direction vector in local coordinates.
## void setWorldDirection ( const Math:: vec3 & dir , const Math:: vec3 & up , MathLib::AXIS axis = AXIS_NZ )

Updates the direction vector of the node and reorients this node: the specified axis of the node becomes oriented along the specified vector in world coordinates. For example, after running the code below, you will get the X axis of the node pointed along the Y axis in world coordinates:
```cpp
// get the node
NodePtr node = World::getNodeByName("material_ball");
// set the X axis to be pointed along the Y axis in world coordinates
node->setWorldDirection(vec3(0.0f,1.0f,0.0f),vec3(0.0f,0.0f,1.0f), Math::AXIS_X);

```


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **dir** - New direction vector in world coordinates. The direction vector always has unit length.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **up** - New up vector in world coordinates. If you skip this argument, the Z axis (in local coordinates) will be used. Note that the specified up vector is a hint vector only: the node's up vector points in the direction hinted by the specified up vector. The node's up vector matches the specified up vector (*up*) only if it is perpendicular to the specified direction vector (*dir*).
- *MathLib::AXIS* **axis** - Axis along which the direction vector should be pointed. The default is the negative Z axis.

## Math:: vec3 getWorldDirection ( MathLib::AXIS axis = AXIS_NZ ) const

Returns the normalized direction vector pointing along the given node axis in world coordinates. By default, the direction vector pointing along the negative Z axis of the node is returned. The direction vector always has a unit length.
```cpp
node->getWorldDirection(node->isPlayer() ? Math::AXIS_NZ : Math::AXIS_Y); // forward direction vector
node->getWorldDirection(node->isPlayer() ? Math::AXIS_Z : Math::AXIS_NY); // backward direction vector
node->getWorldDirection(node->isPlayer() ? Math::AXIS_Y : Math::AXIS_Z); // upward direction vector
node->getWorldDirection(node->isPlayer() ? Math::AXIS_NY : Math::AXIS_NZ); // down direction vector
node->getWorldDirection(Math::AXIS_X); // right direction vector
node->getWorldDirection(Math::AXIS_NX); // left direction vector

```


### Arguments

- *MathLib::AXIS* **axis** - Axis along which the direction vector points. The default is the negative Z axis.

### Return value

Direction vector in world coordinates.
## Ptr < Node > getCloneNode ( const Ptr < Node > & original_node )

Returns a node cloned from the specified original node.
> **Notice:** This method is intended for use only inside the [node clone callback](#getEventNodeClone_Event).


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **original_node** - Original node that was cloned.

### Return value

Clone of the specified original node if it exists; otherwise the original node itself.
## Ptr < Property > getCloneProperty ( const Ptr < Property > & original_property )

Returns a node property cloned from the specified original property.
> **Notice:** This method is intended for use only inside the [node clone callback](#getEventNodeClone_Event).


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **original_property** - Original node property that was cloned.

### Return value

Clone of the specified original node property if it exists; otherwise the original node property itself.
## void setSaveToWorldEnabledRecursive ( bool enable )

Sets a value indicating if saving to `*.world` file is enabled for the node and all its children (if any).
### Arguments

- *bool* **enable** - true to enable saving to `*.world` file for the node and all its children (if any); 0 to disable.

## void setShowInEditorEnabledRecursive ( bool enable )

Sets a value indicating if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) is enabled for the node and all its children (if any).
### Arguments

- *bool* **enable** - true to enable displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) for the node and all its children (if any); 0 to disable.

## Node::LIFETIME getLifetimeSelf ( ) const

Returns the lifetime management type set for the node itself.
> **Notice:** Lifetime of each node in the hierarchy is defined by it's root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)). Setting lifetime management type for a child node different from the one set for the root has no effect.


### Return value

Lifetime management type for the node (see the [*LIFETIME*](#LIFETIME) enum).
## Math:: WorldBoundBox getHierarchyBoundBox ( bool only_enabled_nodes = false ) const

Returns a bounding box with local coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding box recalculation when transforming nodes.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding box with world coordinates.
## Math:: WorldBoundSphere getHierarchyBoundSphere ( bool only_enabled_nodes = false ) const

Returns a bounding sphere with local coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding sphere recalculation when transforming nodes.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding sphere with world coordinates.
## Math:: WorldBoundBox getHierarchyWorldBoundBox ( bool only_enabled_nodes = false ) const

Returns a bounding box with world coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding box recalculation when transforming nodes.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding box with world coordinates.
## Math:: WorldBoundSphere getHierarchyWorldBoundSphere ( bool only_enabled_nodes = false ) const

Returns a bounding sphere with world coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding sphere recalculation when transforming nodes.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding sphere with world coordinates.
## Math:: WorldBoundBox getHierarchySpatialBoundBox ( bool only_enabled_nodes = false ) const

Returns a bounding box with world coordinates that takes all children and physics into account. This bounding box is used by the spatial tree.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding box with world coordinates.
## Math:: WorldBoundSphere getHierarchySpatialBoundSphere ( bool only_enabled_nodes = false ) const

Returns a bounding sphere with world coordinates that takes all children and physics into account. This bounding sphere is used by the spatial tree.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding sphere with world coordinates.
## virtual void updateSpatialTree ( )

Updates node bounds in the [spatial tree](../../../principles/world_management/index.md#outdoor) in the current frame. This method can be used in case you use some custom logic affecting node bounds or position and need to have your changes to be taken into account in the current frame, as well as to process such changes for your custom nodes ( *[ObjectExtern](../../../api/library/objects/class.objectextern_cpp.md), [NodeExtern](../../../api/library/nodes/class.nodeextern_cpp.md)*) which are otherwise ignored. Calling this method enables you to apply changes for this node fast without complete tree recalculation. But you should be aware that node bounds fast-updated this way **might be inaccurate** (they can only be expanded, as shrinking will require tree recalculation). In case you need to have 100% accurate bounds in the current frame, call the *[World::updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method. You can also simply tell the spatial tree to update node bounds in the next frame via the *[updateSpatialTreeDelayed()](../../...md#updateSpatialTreeDelayed_void)* method.
## void updateSpatialTreeDelayed ( )

Mark node bounds in the spatial tree to be updated in the next frame (all bounds will be 100% accurate in this case unlike for the *[updateSpatialTree()](../../...md#updateSpatialTree_void)* method). This method can be used in case you use some custom logic affecting node bounds or position, as well as to process such changes for your custom nodes ( *[ObjectExtern](../../../api/library/objects/class.objectextern_cpp.md), [NodeExtern](../../../api/library/nodes/class.nodeextern_cpp.md)*) which are otherwise ignored. The changes will only be applied in the next frame, in case you need to have your changes to be taken into account right in the current frame use the *[World::updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* method for 100% accurate bounds (slow), or the fast *[updateSpatialTree()](../../...md#updateSpatialTree_void)* method which only expands node bounds if necessary.
## Ptr < WorldTrigger > getWorldTrigger ( int num )

Returns one of the World Triggers inside which the node is located at the moment by its number. For any node in the world, you can [check whether it is currently inside any World Trigger](#getNumWorldTriggers_int) and access any of such triggers by simply calling this method.
### Arguments

- *int* **num** - Number of the World Trigger in the list of World Triggers inside which the node is located at the moment.

### Return value

World Trigger with the specified number inside which the node is located at the moment.
## UGUID getLostNodePropertyGUID ( int num ) const

Returns the [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a lost property assigned to the node. If for some reason a property assigned to the specified slot of the node is missing, this method can be used to get it's GUID.
### Arguments

- *int* **num** - Target property slot number.

### Return value

Lost property [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
## void renderBounds ( bool render_node_bound = true , bool render_instance_bound = false )

Renders the node bounds. The method is applied for checking the actual size of the CPU-rendered node bounds that may differ from the GPU-rendered mesh size, if the latter has been modified by the shader. For nodes that consist of multiple mesh instances (Clutter, Cluster) rendering of each individual mesh bound is also available.
### Arguments

- *bool* **render_node_bound** - true to enable rendering of the node bounds, false to disable it.
- *bool* **render_instance_bound** - true to enable bound rendering for each individual mesh instance (applicable for Clutter and Cluster nodes), false to disable it.

## int getIDFromFile ( ) const

Returns the node ID from the `*.node` or a `*.world` file if the node has been loaded from this file.
### Return value

Node ID from the `*.node` or a `*.world` file. For the node created via code, -1 is returned.
## void applyReplacePaths ( )

Restores the engine's ability to replace baked textures (lightmap, shadow map) inside Node References in runtime. This method is to be applied if hierarchy inside a Node Reference or a path to the baked texture has been modified thus causing rendering of an unsuitable lightmap or a shadow map.
## void getNodes ( Vector < Ptr < Node >> & OUT_nodes )

Takes a node collection, clears it, and then adds all existing nodes to it. This includes nodes from the world and other sources, such as cached nodes or nodes currently being loaded via AsyncQueue.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Node сollection. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool hasData ( const char * name ) const

Checks if there is user data associated with the node.
### Arguments

- *const char ** **name** - String containing a key identifying user data stored in the `*.node` file.

### Return value

true if the given node has user data; otherwise, false.
## void removeData ( const char * name )

Removes user data associated with the node.
### Arguments

- *const char ** **name** - String containing a key identifying user data stored in the `*.node` file.
