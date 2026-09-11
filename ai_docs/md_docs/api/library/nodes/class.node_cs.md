# Unigine.Node Class (CS)


In terms of Unigine, all of the objects added into the scene are called [nodes](../../../objects/nodes/index.md). Nodes can be of different types, determining their visual representation and behavior.


The node is created and stored in the world. All changes are saved into the `.world` file.


The node can be also [saved](../../../api/library/engine/class.world_cs.md#saveNode_cstr_Node_int_int) into an external `.node` file and then [imported](../../../api/library/engine/class.world_cs.md#loadNode_cstr_int_Node) into the world when necessary. Also it is possible to create a [reference](../../../api/library/nodes/class.nodereference_cs.md) to the exported node.


You can associate any [string data](#setData_cstr_cstr_void) (written directly into a *.node or a *.world file) or an arbitrary [user variable](#setVariable_Variable_void) with a node.


### See Also


- How to handle [ownership](../../../code/uniginescript/memory_management.md)
- How to work with the node's [matrix transformations](../../../code/fundamentals/matrix_transformations/index_cs.md)


### Creating a Node


The Node class doesn't provide node creation. You can create an instance of any class inherited from the Node class and then obtain the node via automatic upcasting.


For example:

1. Use the box mesh to create an instance of the [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md) class. This class is inherited from the Node class.
2. Get the node via upcasting.


```csharp
	void Init()
	{
		// create an instance of any class inherited from the Node class (e.g. ObjectMeshStatic)
		ObjectMeshStatic object_mesh = new ObjectMeshStatic("core/meshes/box.mesh");

		// declare a node and obtain the node from the created ObjectMeshStatic
		Node node = object_mesh;
	}

```


Now you can operate the ObjectMeshStatic instance as a node.


### Editing a Node and Saving Changes


The Node class contains common settings of the node. Also each node has special settings, which vary depending on the type of the node.

> **Notice:** The special settings of a node can be found in the article on the corresponding class.


Editing the node also includes editing materials and properties assigned to the node.


For the edited node to be saved in the `.world` file, you should enable the corresponding option via the *[setSaveToWorldEnabled()](#setSaveToWorldEnabled_int_void)* method.

> **Notice:** The node shall be saved to a `*.world` file only if this option is enabled for all of its ancestors as well.


For example:

1. Create a box mesh by using the [Mesh](../../../api/library/rendering/class.mesh_cs.md) class.
2. Save the mesh on the disk. It is required as the node we are going to save to the `.world` file need to reference to a mesh stored on the disk.
3. Use the saved `.mesh` file to create an instance of the [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md) class. This class is inherited from the Node class.
4. Get the node from the ObjectMeshStatic instance via upcasting.
5. Enable saving to `.world` file for the node (and all its children).
6. Edit the node and save the world by calling the `world_save`console command.


```csharp
	void Init()
	{
		// create a mesh
		Mesh mesh = new Mesh();
		mesh.AddBoxSurface("box_0", new vec3(1.0f));
		// save a mesh into a file on the disk
		mesh.Save("unigine_project/meshes/my_mesh.mesh");
		// declare a smart pointer for any type of the node inherited from the Node class (e.g. ObjectMeshStatic)
		// and call a constructor of the corresponding class
		ObjectMeshStatic object_mesh = new ObjectMeshStatic("unigine_project/meshes/my_mesh.mesh");

		// declare a smart pointer for the node,
		// obtain the node from the created ObjectMeshStatic,
		Node node = object_mesh;

		// enable saving the node (with all its children) to a *.world file
		node.SetSaveToWorldEnabledRecursive(true);

		// change the node name
		node.Name = "my_node";
		// change node transformation
		node.WorldTransform = MathLib.Translate(new Vec3(0.0f, 0.0f, 2.0f));

		// save node changes in the *.world file
		Console.Run("world_save");
	}


```


### Exporting and Importing a Node


To export a node stored in the world into the external `.node` file, you should pass it to the *[saveNode()](../../../api/library/engine/class.world_cs.md#saveNode_cstr_Node_int_int)* method of the World class.


To import the existing node stored in the `.node` file to the world, you should call the *[loadNode()](../../../api/library/engine/class.world_cs.md#loadNode_cstr_int_Node)* method of the World class.


For example:


1. Create a box mesh by using the [Mesh](../../../api/library/rendering/class.mesh_cs.md) class.
2. Save the mesh on the disk. It is required as the node we are going to export need to reference to a mesh stored on the disk.
3. Use the saved `.mesh` file to create an instance of the [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md) class. This class is inherited from the Node class.
4. Get the node from the ObjectMeshStatic instance via upcasting.
5. Export the node to an external `.node` file.
6. Import the prevoiusly exported node to check the result.


```csharp
	void Init()
	{

		// create a mesh
		Mesh mesh = new Mesh();
		mesh.AddBoxSurface("box_0", new vec3(1.0f));
		// save a mesh into a file on the disk
		mesh.Save("unigine_project/meshes/my_mesh.mesh");
		// create an instance of any class inherited from the Node class (e.g. ObjectMeshStatic)
		ObjectMeshStatic object_mesh = new ObjectMeshStatic("unigine_project/meshes/my_mesh.mesh");

		// declare a smart pointer for the node
		// and obtain the node pointer from the created NodeDummy
		Node node = object_mesh;
		// export the node into a *.node file
		World.SaveNode("unigine_project/nodes/my_node.node", node);
		// import the exported node to check the result
		Node imported_node = World.LoadNode("unigine_project/nodes/my_node.node");
		// set position of the node
		imported_node.Position = new Vec3(4.0f, 0.0f, 1.0f);
	}

```


### Deleting a Node


By default each new node's lifetime matches the lifetime of the **World** (i.e. such node shall be deleted when the world is closed). But you can also choose node's lifetime to be managed:


- **by the Engine** - is this case the node shall be deleted automatically on Engine shutdown.
- **manually** - is this case the node should be deleted manually by the user.


To delete a node you can use the following two methods:


- [*deleteLater()*](../../../api/library/common/class.ptr_cs.md#deleteLater_void) - performs delayed deletion, in this case the object will be deleted during the next swap stage of the main loop (rendering of the object ceases immediately, but it still exists in memory for a while, so you can get it from its parent, for example). This method simplifies object deletion from a secondary thread, so you can call it and forget about the details, letting the Engine take control over the process of deletion, which can be used for future optimizations.
- [*deleteForce()*](../../../api/library/common/class.ptr_cs.md#deleteForce_void) - performs immediate deletion, which might be necessary in some cases. Calling this method for main-loop-dependent objects (e.g., nodes) is safe only when performed from the Main thread.


```csharp
	void Init()
	{
		// create an instance of any class inherited from the Node class (e.g. ObjectMeshStatic)
		ObjectMeshStatic object_mesh = new ObjectMeshStatic("core/meshes/box.mesh");

		// declare a smart pointer for the node
		// and obtain the node pointer from the created ObjectMeshStatic
		Node node = object_mesh;

		// do something with the node
		// ...

		// delete the node
		node.DeleteLater();
	}

```


## Node Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **ANY_TYPE** = -1 | Any node type. |
| **NODE_BEGIN** = 0 | Begin of the nodes range. |
| **NODE_DUMMY** = 0 | Dummy node. See the [NodeDummy](../../../api/library/nodes/class.nodedummy_cs.md) class. |
| **NODE_LAYER** = 1 | Layer node. See the [NodeLayer](../../../api/library/nodes/class.nodelayer_cs.md) class. |
| **NODE_TRIGGER** = 2 | Dummy node that can fire callbacks on its enabling/disabling or repositioning. See the [NodeTrigger](../../../api/library/nodes/class.nodetrigger_cs.md) class. |
| **NODE_REFERENCE** = 3 | Node reference that refers to an external NODE file. See the [NodeReference](../../../api/library/nodes/class.nodereference_cs.md) class. |
| **NODE_EXTERN** = 4 | Extern node. See the [NodeExtern](../../../api/library/nodes/class.nodeextern_cs.md) class. |
| **NODE_SEQUENCE_PLAYER** = 5 | Sequence player node. See the [NodeSequencePlayer](../../../api/library/nodes/class.nodesequenceplayer_cs.md) class. |
| **NODE_SKELETON_POSE** = 6 | Skeleton pose node. See the [NodeSkeletonPose](../../../api/library/nodes/class.nodeskeletonpose_cs.md) class. |
| **NODE_END** = 6 | End of the nodes range. |
| **WORLD_BEGIN** = 7 | Begin of the world nodes range. |
| **WORLD_SPLINE_GRAPH** = 7 | World spline graph. See the [WorldSplineGraph](../../../api/library/worlds/class.worldsplinegraph_cs.md) class. |
| **WORLD_TRIGGER** = 8 | World trigger. See the [WorldTrigger](../../../api/library/worlds/class.worldtrigger_cs.md) class. |
| **WORLD_CLUTTER** = 9 | World clutter. See the [WorldClutter](../../../api/library/worlds/class.worldclutter_cs.md) class. |
| **WORLD_SWITCHER** = 10 | Node switcher (to switch off parts of the world). See the [WorldSwitcher](../../../api/library/worlds/class.worldswitcher_cs.md) class. |
| **WORLD_OCCLUDER** = 11 | World occluder. See the [WorldOccluder](../../../api/library/worlds/class.worldoccluder_cs.md) class. |
| **WORLD_OCCLUDER_MESH** = 12 | World mesh occluder. See the [WorldOccluderMesh](../../../api/library/worlds/class.worldoccludermesh_cs.md) class. |
| **WORLD_TRANSFORM_PATH** = 13 | Path defined transformer. See the [WorldTransformPath](../../../api/library/worlds/class.worldtransformpath_cs.md) |
| **WORLD_TRANSFORM_JOINT** = 14 | Joint defined transformer. See the [WorldTransformJoint](../../../api/library/worlds/class.worldtransformjoint_cs.md) class. |
| **WORLD_EXPRESSION** = 15 | Node which allows to execute arbitrary expression. See the [WorldExpression](../../../api/library/worlds/class.worldexpression_cs.md) class. |
| **WORLD_EXTERN** = 16 | External world. See the [WorldExtern](../../../api/library/worlds/class.worldextern_cs.md) class. |
| **WORLD_END** = 16 | End of the world nodes range. |
| **GEODETIC_BEGIN** = 17 | Begin of the geodetic nodes range. |
| **GEODETIC_PIVOT** = 17 | Geodetic Pivot node. See the [GeodeticPivot](../../../api/library/geodetics/class.geodeticpivot_cs.md) class. |
| **GEODETIC_END** = 17 | End of the geodetic nodes range. |
| **FIELD_BEGIN** = 18 | Begin of the field nodes range. |
| **FIELD_SPACER** = 18 | Field Spacer node. See the [FieldSpacer](../../../api/library/fields/class.fieldspacer_cs.md) class. |
| **FIELD_ANIMATION** = 19 | Field Animation node. See the [FieldAnimation](../../../api/library/fields/class.fieldanimation_cs.md) class. |
| **FIELD_HEIGHT** = 20 | Field Height node. See the [FieldHeight](../../../api/library/fields/class.fieldheight_cs.md) class. |
| **FIELD_SHORELINE** = 21 | Field Shoreline node. See the [FieldShoreline](../../../api/library/fields/class.fieldshoreline_cs.md) class. |
| **FIELD_WEATHER** = 22 | Field Weather node. See the [FieldWeather](../../../api/library/fields/class.fieldweather_cs.md) class. |
| **FIELD_END** = 22 | End of the field nodes range. |
| **PARTICLES_FIELD_BEGIN** = 23 | Beginning of the particles field range. |
| **PARTICLES_FIELD_SPACER** = 23 | Particles Field Spacer node. See the [ParticlesFieldSpacer](../../../api/library/objects/class.particlesfieldspacer_cs.md) class. |
| **PARTICLES_FIELD_DEFLECTOR** = 24 | Particles Field Deflector node. See the [ParticlesFieldDeflector](../../../api/library/objects/class.particlesfielddeflector_cs.md) class. |
| **PARTICLES_FIELD_END** = 24 | End of the particles field nodes range. |
| **LIGHT_BEGIN** = 25 | Begin of the light nodes range. |
| **LIGHT_VOXEL_PROBE** = 25 | Voxel probe. See the [LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_cs.md) class. |
| **LIGHT_ENVIRONMENT_PROBE** = 26 | Environment probe. See the [LightEnvironmentProbe](../../../api/library/lights/class.lightenvironmentprobe_cs.md) class. |
| **LIGHT_PLANAR_PROBE** = 27 | Planar probe. See the [LightPlanarProbe](../../../api/library/lights/class.lightplanarprobe_cs.md) class. |
| **LIGHT_OMNI** = 28 | Omni-directional light source. See the [LightOmni](../../../api/library/lights/class.lightomni_cs.md) class. |
| **LIGHT_PROJ** = 29 | Projected light source. See the [LightProj](../../../api/library/lights/class.lightproj_cs.md) class. |
| **LIGHT_WORLD** = 30 | World light source. See the [LightWorld](../../../api/library/lights/class.lightworld_cs.md) class. |
| **LIGHT_END** = 30 | End of the light nodes range. |
| **DECAL_BEGIN** = 31 | Begin of the decal nodes range. |
| **DECAL_PROJ** = 31 | Projected decal node. See the [DecalProj](../../../api/library/decals/class.decalproj_cs.md) class. |
| **DECAL_ORTHO** = 32 | Orthographic decal node. See the [DecalOrtho](../../../api/library/decals/class.decalortho_cs.md) class. |
| **DECAL_MESH** = 33 | Mesh decal node. See the [DecalMesh](../../../api/library/decals/class.decalmesh_cs.md) class. |
| **DECAL_END** = 33 | End of the decal nodes range. |
| **LANDSCAPE_LAYER_BEGIN** = 34 | Beginning of the landscape layers range. |
| **LANDSCAPE_LAYER_MAP** = 34 | Landscape Layer Map. See the [LandscapeLayerMap](../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) class. |
| **LANDSCAPE_LAYER_END** = 34 | End of the landscape layers range. |
| **OBJECT_BEGIN** = 35 | Begin of the object nodes range. |
| **OBJECT_DUMMY** = 35 | Dummy object. See the [ObjectDummy](../../../api/library/objects/class.objectdummy_cs.md) class. |
| **OBJECT_DYNAMIC** = 36 | Dynamic object. See the [ObjectDynamic](../../../api/library/objects/class.objectdynamic_cs.md) class. |
| **OBJECT_MESH_STATIC** = 37 | Static mesh object. See the [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md) class. |
| **OBJECT_MESH_CLUSTER** = 38 | [Mesh Cluster](../../../objects/objects/mesh_cluster/index.md) object. See the [ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cs.md) class. |
| **OBJECT_MESH_CLUTTER** = 39 | [Mesh Clutter](../../../objects/objects/mesh_clutter/index.md) object. See the [ObjectMeshClutter](../../../api/library/objects/class.objectmeshclutter_cs.md) class. |
| **OBJECT_MESH_SKINNED_LEGACY** = 40 | Legacy skinned mesh object. See the [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md) class. |
| **OBJECT_MESH_SKINNED** = 41 | Skinned mesh object. See the [ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md) class. |
| **OBJECT_MESH_DYNAMIC** = 42 | Dynamic mesh object. See the [ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md) class. |
| **OBJECT_MESH_SPLINE_CLUSTER** = 43 | Mesh Spline Cluster object. See the [ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cs.md) class. |
| **OBJECT_LANDSCAPE_TERRAIN** = 44 | LandscapeTerrain object. See the [ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md) class. |
| **OBJECT_TERRAIN_GLOBAL** = 45 | Terrain global object. See the [ObjectTerrainGlobal](../../../api/library/objects/class.objectterrainglobal_cs.md) class. |
| **OBJECT_GRASS** = 46 | Grass. See the [ObjectGrass](../../../api/library/objects/class.objectgrass_cs.md) class. |
| **OBJECT_PARTICLES** = 47 | Particles object. See the [ObjectParticles](../../../api/library/objects/class.objectparticles_cs.md) class. |
| **OBJECT_BILLBOARDS** = 48 | [Billboards](../../../objects/objects/billboards/index.md) object for rendering a high number of billboards. See the [ObjectBillboard](../../../api/library/objects/class.objectbillboards_cs.md) class. |
| **OBJECT_VOLUME_BOX** = 49 | Volume box object. See the [ObjectVolumeBox](../../../api/library/objects/class.objectvolumebox_cs.md) class. |
| **OBJECT_VOLUME_SPHERE** = 50 | Volume sphere object. See the [ObjectVolumeSphere](../../../api/library/objects/class.objectvolumesphere_cs.md) class. |
| **OBJECT_VOLUME_OMNI** = 51 | Volume omni light object. See the [ObjectVolumeOmni](../../../api/library/objects/class.objectvolumeomni_cs.md) class. |
| **OBJECT_VOLUME_PROJ** = 52 | Volume projected light object. See the [ObjectVolumeProj](../../../api/library/objects/class.objectvolumeproj_cs.md) class. |
| **OBJECT_GUI** = 53 | GUI object. See the [ObjectGui](../../../api/library/objects/class.objectgui_cs.md) class. |
| **OBJECT_GUI_MESH** = 54 | GUI mesh object. See the [ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cs.md) class. |
| **OBJECT_WATER_GLOBAL** = 55 | Water global object. See the [ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cs.md) class. |
| **OBJECT_WATER_MESH** = 56 | Water mesh object. See the [ObjectWaterMesh](../../../api/library/objects/class.objectwatermesh_cs.md) class. |
| **OBJECT_SKY** = 57 | Sky object. See the [ObjectSky](../../../api/library/objects/class.objectsky_cs.md) class. |
| **OBJECT_CLOUD_LAYER** = 58 | Cloud layer object. See the [ObjectCloudLayer](../../../api/library/objects/class.objectcloudlayer_cs.md) class. |
| **OBJECT_EXTERN** = 59 | Extern object. See the [ObjectExtern](../../../api/library/objects/class.objectextern_cs.md) class. |
| **OBJECT_TEXT** = 60 | Text object. See the [ObjectText](../../../api/library/objects/class.objecttext_cs.md) class. |
| **OBJECT_END** = 60 | End of the object nodes range. |
| **PLAYER_BEGIN** = 61 | Begin of the player nodes range. |
| **PLAYER_DUMMY** = 61 | Dummy player. See the [PlayerDummy](../../../api/library/players/class.playerdummy_cs.md) class. |
| **PLAYER_SPECTATOR** = 62 | Observing player. See the [PlayerSpectator](../../../api/library/players/class.playerspectator_cs.md) class. |
| **PLAYER_PERSECUTOR** = 63 | Persecuting player. See the [PlayerPersecutor](../../../api/library/players/class.playerpersecutor_cs.md) class. |
| **PLAYER_ACTOR** = 64 | Acting player. See the [PlayerActor](../../../api/library/players/class.playeractor_cs.md) class. |
| **PLAYER_END** = 64 | End of the player nodes range. |
| **PHYSICAL_BEGIN** = 65 | Begin of the physical nodes range. |
| **PHYSICAL_WIND** = 65 | Physical wind object. See the [PhysicalWind](../../../api/library/physics/class.physicalwind_cs.md) class. |
| **PHYSICAL_FORCE** = 66 | Physical force node that allows to simulate point forces applied to dynamic objects. See the [PhysicalForce](../../../api/library/physics/class.physicalforce_cs.md) class. |
| **PHYSICAL_NOISE** = 67 | Physical noise node that allows to simulate force field. See the [PhysicalNoise](../../../api/library/physics/class.physicalnoise_cs.md) class. |
| **PHYSICAL_WATER** = 68 | Physical water object that has no visual representation. See the [PhysicalWater](../../../api/library/physics/class.physicalwater_cs.md) class. |
| **PHYSICAL_TRIGGER** = 69 | Physical trigger. See the [PhysicalTrigger](../../../api/library/physics/class.physicaltrigger_cs.md) class. |
| **PHYSICAL_END** = 69 | End of the physical nodes range. |
| **NAVIGATION_BEGIN** = 70 | Begin of the navigation nodes range. |
| **NAVIGATION_SECTOR** = 70 | Sector within which pathfinding is performed. See the [NavigationSector](../../../api/library/pathfinding/class.navigationsector_cs.md) class. |
| **NAVIGATION_MESH** = 71 | Mesh-based navigation area across which pathfinding is performed. See the [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cs.md) class. |
| **NAVIGATION_END** = 71 | End of the navigation nodes range. |
| **EXPERIMENTAL_NAVIGATION_BEGIN** = 72 | Begin of the experimental navigation nodes range. |
| **EXPERIMENTAL_NAVIGATION_MESH** = 72 | Navigation mesh baked from the scene geometry, across which pathfinding is performed. See the [ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md) class. |
| **EXPERIMENTAL_NAVIGATION_MESH_INVOKER** = 73 | Node that keeps the tiles of a baked navigation mesh resident around itself. See the [ExperimentalNavigationMeshInvoker](../../../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cs.md) class. |
| **EXPERIMENTAL_NAVIGATION_MESH_AREA_VOLUME** = 74 | Volume that stamps an area onto the polygons of a baked navigation mesh. See the [ExperimentalNavigationMeshAreaVolume](../../../api/library/pathfinding/class.experimentalnavigationmeshareavolume_cs.md) class. |
| **EXPERIMENTAL_NAVIGATION_END** = 74 | End of the experimental navigation nodes range. |
| **OBSTACLE_BEGIN** = 75 | Begin of the obstacle nodes range. |
| **OBSTACLE_BOX** = 75 | Obstacle in the shape of a box avoided by pathfinding. See the [ObstacleBox](../../../api/library/pathfinding/class.obstaclebox_cs.md) class. |
| **OBSTACLE_SPHERE** = 76 | Obstacle in the shape of a sphere avoided by pathfinding. See the [ObstacleSphere](../../../api/library/pathfinding/class.obstaclesphere_cs.md) class. |
| **OBSTACLE_CAPSULE** = 77 | Obstacle in the shape of a capsule avoided by pathfinding. See the [ObstacleCapsule](../../../api/library/pathfinding/class.obstaclecapsule_cs.md) class. |
| **OBSTACLE_END** = 77 | End of the obstacle nodes range. |
| **SOUND_BEGIN** = 78 | Begin of the sound nodes range. |
| **SOUND_SOURCE** = 78 | Sound source. See the [SoundSource](../../../api/library/sounds/class.soundsource_cs.md) class. |
| **SOUND_REVERB** = 79 | Sound reverberation zone. See the [SoundReverb](../../../api/library/sounds/class.soundreverb_cs.md) class. |
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
| **DUMMY** = 0 | Dummy node. See the [NodeDummy](../../../api/library/nodes/class.nodedummy_cs.md) class. |
| **LAYER** = 1 | Layer node. See the [NodeLayer](../../../api/library/nodes/class.nodelayer_cs.md) class. |
| **TRIGGER** = 2 | Dummy node that can fire callbacks on its enabling/disabling or repositioning. See the [NodeTrigger](../../../api/library/nodes/class.nodetrigger_cs.md) class. |
| **REFERENCE** = 3 | Node reference that refers to an external NODE file. See the [NodeReference](../../../api/library/nodes/class.nodereference_cs.md) class. |
| **EXTERN** = 4 | Extern node. See the [NodeExtern](../../../api/library/nodes/class.nodeextern_cs.md) class. |

## LIFETIME

| Name | Description |
|---|---|
| **WORLD** = 0 | Node's lifetime is managed by the world. The node shall be deleted automatically on closing the world. |
| **ENGINE** = 1 | Node's lifetime is managed by the Engine. The node shall be deleted automatically on Engine shutdown. |
| **MANUAL** = 2 | Node's lifetime is managed by the user. The node should be deleted manually by the user. |

### Properties

## 🔒︎ GeodeticPivot GeodeticPivot

The pointer to geodetic pivot of the node.
## Variable Variable

The value of the single unnamed variable parameter of the node. If this variable does not exist it will be created with a specified value (on requesting the non-existent value 0 will be returned).
## vec3 WorldScale

The node scale in the world space.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


## vec3 WorldPosition

The node position in the world coordinates.
## vec3 Scale

The scale of the node.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


## vec3 Position

The node position.
## 🔒︎ vec3 BodyAngularVelocity

The angular velocity of the node's physical body in the world space.
## 🔒︎ vec3 BodyLinearVelocity

The linear velocity of the node's physical body in the local space.
## 🔒︎ BodyRigid ObjectBodyRigid

The [rigid body](../../../principles/physics/bodies/rigid/index.md) assigned to the node if it is an object node.
## 🔒︎ Body ObjectBody

The physical body assigned to the node if it is an object node.
## 🔒︎ WorldBoundSphere WorldBoundSphere

The bounding sphere of the node in world's coordinate system.
## 🔒︎ WorldBoundBox WorldBoundBox

The bounding box of the node in world's coordinate system.
## 🔒︎ BoundSphere BoundSphere

The bounding sphere of the node.
> **Notice:** The coordinates of the bounding sphere are in the node's local coordinate system. To get the bounding sphere in world coordinates, use the [*WorldBoundSphere*](#getWorldBoundSphere_WorldBoundSphere) property.


## 🔒︎ BoundBox BoundBox

The bounding box of the node.
> **Notice:** The coordinates of the bounding box are in the node's local coordinate system. To get the bounding box in world coordinates, use the [*WorldBoundBox()*](#getWorldBoundBox_WorldBoundBox) property.


## mat4 OldWorldTransform

The old (previous frame) transformation matrix for the node in the world coordinates.
## mat4 WorldTransform

The transformation matrix of the node in the world coordinates.
## mat4 Transform

The transformation matrix of the node in its parent coordinates.
## 🔒︎ int NumProperties

The total number of properties associated with the node.
## 🔒︎ Node Possessor

The possessor of the node. the following nodes can be possessors:
- NodeReference
- WorldCluster
- WorldClutter
- WorldLayer

This function can only be applied to a root node inside a node reference.
## 🔒︎ int NumChildren

The number of children of the node.
## 🔒︎ Node RootNode

The root node for the node. This method searches for the root node among all node's parents and [possessors](#getPossessor_Node) up the hierarchy. If a node does not have a parent or possessor the node itself will be returned.
## Node Parent

The parent of the node.
## 🔒︎ int NumAncestors

The number of ancestors of the node.
## string Name

The name of the node.
## bool Query

The value indicating if occlusion query is used for the node. The default is false (not used).
## bool ClutterInteractionEnabled

The value indicating if interaction with [World Clutters](../../../api/library/worlds/class.worldclutter_cs.md) and [Mesh Clutters](../../../api/library/objects/class.objectmeshclutter_cs.md) is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of clutters is not necessary. Especially when the world contains a significant number of such nodes.


## bool GrassInteractionEnabled

The value indicating if interaction with [Grass](../../../api/library/objects/class.objectgrass_cs.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of grass is not necessary. Especially when the world contains a significant number of such nodes.


## bool TriggerInteractionEnabled

The value indicating if interaction with [WorldTrigger](../../../api/library/worlds/class.worldtrigger_cs.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when node interaction with [World Triggers](../../../api/library/worlds/class.worldtrigger_cs.md) is not necessary. Especially when the world contains a significant number of such nodes.


## bool Immovable

The value indicating if the node is an immovable (clutter) object, which means it is moved to a separate spatial tree for immovable (static) objects optimizing node management. There are several restrictions on nodes considered immovable. Any action affecting the spatial tree is prohibited and causes a warning: you cannot change the node state (enabled/disabled), surfaces, bounds, trasformation, visibility distance, as well as move the node, assign a non-dummy physical body or even disable the *Immovable* flag as it also leads to rebiulding of the spatial tree.
> **Notice:** You can disable these warnings by using the [*World::setMovingImmovableNodeMode()*](../../../api/library/engine/class.world_cs.md#setMovingImmovableNodeMode_int_void) method, if necessary.


## bool Handled

The value indicating if the node handle is displayed. This option is valid only for invisible nodes, such as light and sound sources, particle systems and world-managing nodes ( [WorldOccluder](../../../api/library/worlds/class.worldoccluder_cs.md), triggers, expressions, etc.)
## bool Enabled

The value indicating if the node and its parent nodes are enabled.
## 🔒︎ bool IsExtern

The value indicating if the node is an extern node (its type is one of the following: *[NODE_EXTERN](#NODE_EXTERN), [OBJECT_EXTERN](#OBJECT_EXTERN), [WORLD_EXTERN](#WORLD_EXTERN)*).
## 🔒︎ bool IsField

The value indicating if the node is a field node (its type is one of the *[FIELD_*](#FIELD_ANIMATION)*).
## 🔒︎ bool IsParticlesField

The value indicating if the node is a particles field node (its type is one of the *[PARTICLES_FIELD_*](#PARTICLES_FIELD_BEGIN)*).
## 🔒︎ bool IsSound

The value indicating if the node is a sound node (its type is *[SOUND_*](#SOUND_BEGIN)*).
## 🔒︎ bool IsObstacle

The value indicating if the node is an obstacle node (its type is *[OBSTACLE_*](#OBSTACLE_BEGIN)*).
## 🔒︎ bool IsExperimentalNavigation

The value indicating if a given node belongs to the experimental navigation system, that is, if its type falls within the [EXPERIMENTAL_NAVIGATION_BEGIN](#EXPERIMENTAL_NAVIGATION_BEGIN) .. [EXPERIMENTAL_NAVIGATION_END](#EXPERIMENTAL_NAVIGATION_END) range.
## 🔒︎ bool IsNavigation

The value indicating if a given node is a navigation node, that is, if its type falls within the [NAVIGATION_BEGIN](#NAVIGATION_BEGIN) .. [NAVIGATION_END](#NAVIGATION_END) range. The range covers the navigation areas only. Nodes of the experimental navigation system occupy a range of their own and are reported by [IsExperimentalNavigation](#IsExperimentalNavigation).
## 🔒︎ bool IsPhysical

The value indicating if the node is a physical node (its type is *[PHYSICAL_*](#PHYSICAL_BEGIN)*).
## 🔒︎ bool IsPlayer

The value indicating if the node is a player node (its type is *[PLAYER_*](#PLAYER_BEGIN)*).
## 🔒︎ bool IsObject

The value indicating if the node is an object node (its type is *[OBJECT_*](#OBJECT_BEGIN)*).
## 🔒︎ bool IsDecal

The value indicating if the node is a decal node (its type is *[DECAL_*](#DECAL_BEGIN)*).
## 🔒︎ bool IsLight

The value indicating if the node is a light source (its type is *[LIGHT_*](#LIGHT_BEGIN)*).
## 🔒︎ bool IsGeodetic

The value indicating if the node is a geodetic-related node.
## 🔒︎ bool IsWorld

The value indicating if the node is a world node (its type is *[WORLD_*](#WORLD_BEGIN)*).
## 🔒︎ bool IsImmovableSupported

The value indicating if the node can be moved to a separate spatial tree for immovable (static) objects optimizing node management.
## 🔒︎ bool IsSurfacesCollisionSupported

The value indicating if collisions with node surfaces are supported.
## 🔒︎ bool IsSurfacesIntersectionSupported

The value indicating if intersections with node surfaces are supported.
## 🔒︎ string TypeName

The name of the node type.
## 🔒︎ Node.TYPE Type

The type of the node.
## int ID

The runtime ID of the node. It may differ from the file ID, which is obtained via *[*IDFromFile*](#getIDFromFile_int)*.
> **Notice:** See also *[*Unigine.World.GetNodeByID()*](../../../api/library/engine/class.world_cs.md#getNodeByID_int_Node)* function.


## 🔒︎ int IDFromFile

The ID of the node loaded from `*.node` or `*.world` file. It may differ from the runtime ID of the node, which is obtained via *[*ID*](#getID_int)*.
## bool SaveToWorldEnabled

The value indicating if saving to `*.world` file is enabled for the node and all its children (if any).
## 🔒︎ bool IsSaveToWorldEnabledSelf

The value indicating if saving to `*.world` file is enabled for the node.
## bool ShowInEditorEnabled

The value indicating if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) is enabled for the node.
> **Notice:** The node shall be displayed in the hierarchy only if this option is enabled for all of its ancestors as well.


## 🔒︎ bool IsShowInEditorEnabledSelf

The value indicating if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) is enabled for the node.
## 🔒︎ int NumWorldTriggers

The number of World Triggers inside which the node is located at the moment.
## 🔒︎ WorldBoundSphere SpatialBoundSphere

The bounding sphere with world coordinates that participates in physics calculations, but doesn't take children into account. this bounding sphere is used by the spatial tree.
## 🔒︎ WorldBoundBox SpatialBoundBox

The bounding box with world coordinates that participates in physics calculations, but doesn't take children into account. this bounding box is used by the spatial tree.
## 🔒︎ bool IsLandscapeLayer

The value indicating if the node is a landscape layer (its type is [*LANDSCAPE_LAYER_**](#LANDSCAPE_LAYER_BEGIN)).
## 🔒︎ mat4 IWorldTransform

The inverse transformation matrix of the node for transformations in the world coordinates.
## 🔒︎ vec3 OldWorldPosition

The old (previous frame) position of the node in the world coordinates.
## Node.LIFETIME Lifetime

The lifetime management type for the root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)) of the node, or for the node itself (if it is not a child and not possessed by any other node).
> **Notice:** Lifetime of each node in the hierarchy is defined by it's root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)). Thus, lifetime management type set for a child node that differs from the one set for the root is ignored.


## 🔒︎ Event< Node > EventTransformChanged

The event triggered when the node's transformation has changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TransformChanged event handler
void transformchanged_event_handler(Node node)
{
	Log.Message("\Handling TransformChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections transformchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventTransformChanged.Connect(transformchanged_event_connections, transformchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventTransformChanged.Connect(transformchanged_event_connections, (Node node) => {
		Log.Message("Handling TransformChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
transformchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TransformChanged event with a handler function
publisher.EventTransformChanged.Connect(transformchanged_event_handler);

// remove subscription to the TransformChanged event later by the handler function
publisher.EventTransformChanged.Disconnect(transformchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection transformchanged_event_connection;

// subscribe to the TransformChanged event with a lambda handler function and keeping the connection
transformchanged_event_connection = publisher.EventTransformChanged.Connect((Node node) => {
		Log.Message("Handling TransformChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
transformchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
transformchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
transformchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TransformChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventTransformChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventTransformChanged.Enabled = true;

```

</details>

## 🔒︎ Event< Node , int> EventPropertyNodeSlotsChanged

The event triggered when the number of the node's property slots is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**, int **num_slots**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PropertyNodeSlotsChanged event handler
void propertynodeslotschanged_event_handler(Node node,  int num_slots)
{
	Log.Message("\Handling PropertyNodeSlotsChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertynodeslotschanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventPropertyNodeSlotsChanged.Connect(propertynodeslotschanged_event_connections, propertynodeslotschanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventPropertyNodeSlotsChanged.Connect(propertynodeslotschanged_event_connections, (Node node,  int num_slots) => {
		Log.Message("Handling PropertyNodeSlotsChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
propertynodeslotschanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PropertyNodeSlotsChanged event with a handler function
Node.EventPropertyNodeSlotsChanged.Connect(propertynodeslotschanged_event_handler);

// remove subscription to the PropertyNodeSlotsChanged event later by the handler function
Node.EventPropertyNodeSlotsChanged.Disconnect(propertynodeslotschanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection propertynodeslotschanged_event_connection;

// subscribe to the PropertyNodeSlotsChanged event with a lambda handler function and keeping the connection
propertynodeslotschanged_event_connection = Node.EventPropertyNodeSlotsChanged.Connect((Node node,  int num_slots) => {
		Log.Message("Handling PropertyNodeSlotsChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
propertynodeslotschanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
propertynodeslotschanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
propertynodeslotschanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PropertyNodeSlotsChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventPropertyNodeSlotsChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventPropertyNodeSlotsChanged.Enabled = true;

```

</details>

## 🔒︎ Event< Node , Property , int> EventPropertyNodeAdd

The event triggered when a new property is assigned to the node. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**, Property **property**, int **property_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PropertyNodeAdd event handler
void propertynodeadd_event_handler(Node node,  Property property,  int property_index)
{
	Log.Message("\Handling PropertyNodeAdd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertynodeadd_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventPropertyNodeAdd.Connect(propertynodeadd_event_connections, propertynodeadd_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventPropertyNodeAdd.Connect(propertynodeadd_event_connections, (Node node,  Property property,  int property_index) => {
		Log.Message("Handling PropertyNodeAdd event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
propertynodeadd_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PropertyNodeAdd event with a handler function
Node.EventPropertyNodeAdd.Connect(propertynodeadd_event_handler);

// remove subscription to the PropertyNodeAdd event later by the handler function
Node.EventPropertyNodeAdd.Disconnect(propertynodeadd_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection propertynodeadd_event_connection;

// subscribe to the PropertyNodeAdd event with a lambda handler function and keeping the connection
propertynodeadd_event_connection = Node.EventPropertyNodeAdd.Connect((Node node,  Property property,  int property_index) => {
		Log.Message("Handling PropertyNodeAdd event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
propertynodeadd_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
propertynodeadd_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
propertynodeadd_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PropertyNodeAdd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventPropertyNodeAdd.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventPropertyNodeAdd.Enabled = true;

```

</details>

## 🔒︎ Event< Node , Property , int> EventPropertyNodeRemove

The event triggered when a property is removed from the list of the node's properties. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**, Property **property**, int **property_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PropertyNodeRemove event handler
void propertynoderemove_event_handler(Node node,  Property property,  int property_index)
{
	Log.Message("\Handling PropertyNodeRemove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertynoderemove_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventPropertyNodeRemove.Connect(propertynoderemove_event_connections, propertynoderemove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventPropertyNodeRemove.Connect(propertynoderemove_event_connections, (Node node,  Property property,  int property_index) => {
		Log.Message("Handling PropertyNodeRemove event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
propertynoderemove_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PropertyNodeRemove event with a handler function
Node.EventPropertyNodeRemove.Connect(propertynoderemove_event_handler);

// remove subscription to the PropertyNodeRemove event later by the handler function
Node.EventPropertyNodeRemove.Disconnect(propertynoderemove_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection propertynoderemove_event_connection;

// subscribe to the PropertyNodeRemove event with a lambda handler function and keeping the connection
propertynoderemove_event_connection = Node.EventPropertyNodeRemove.Connect((Node node,  Property property,  int property_index) => {
		Log.Message("Handling PropertyNodeRemove event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
propertynoderemove_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
propertynoderemove_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
propertynoderemove_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PropertyNodeRemove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventPropertyNodeRemove.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventPropertyNodeRemove.Enabled = true;

```

</details>

## 🔒︎ Event< Node , Property , int> EventPropertyChangeEnabled

The event triggered when the node's property *enabled* state is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**, Property **property**, int **property_index**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PropertyChangeEnabled event handler
void propertychangeenabled_event_handler(Node node,  Property property,  int property_index)
{
	Log.Message("\Handling PropertyChangeEnabled event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertychangeenabled_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventPropertyChangeEnabled.Connect(propertychangeenabled_event_connections, propertychangeenabled_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventPropertyChangeEnabled.Connect(propertychangeenabled_event_connections, (Node node,  Property property,  int property_index) => {
		Log.Message("Handling PropertyChangeEnabled event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
propertychangeenabled_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PropertyChangeEnabled event with a handler function
Node.EventPropertyChangeEnabled.Connect(propertychangeenabled_event_handler);

// remove subscription to the PropertyChangeEnabled event later by the handler function
Node.EventPropertyChangeEnabled.Disconnect(propertychangeenabled_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection propertychangeenabled_event_connection;

// subscribe to the PropertyChangeEnabled event with a lambda handler function and keeping the connection
propertychangeenabled_event_connection = Node.EventPropertyChangeEnabled.Connect((Node node,  Property property,  int property_index) => {
		Log.Message("Handling PropertyChangeEnabled event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
propertychangeenabled_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
propertychangeenabled_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
propertychangeenabled_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PropertyChangeEnabled events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventPropertyChangeEnabled.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventPropertyChangeEnabled.Enabled = true;

```

</details>

## 🔒︎ Event< Node , int, int> EventPropertyNodeSwap

The event triggered when two properties swap their positions in the list of the node's properties. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**, int **index_from**, int **index_to**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PropertyNodeSwap event handler
void propertynodeswap_event_handler(Node node,  int index_from,  int index_to)
{
	Log.Message("\Handling PropertyNodeSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertynodeswap_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventPropertyNodeSwap.Connect(propertynodeswap_event_connections, propertynodeswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventPropertyNodeSwap.Connect(propertynodeswap_event_connections, (Node node,  int index_from,  int index_to) => {
		Log.Message("Handling PropertyNodeSwap event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
propertynodeswap_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PropertyNodeSwap event with a handler function
Node.EventPropertyNodeSwap.Connect(propertynodeswap_event_handler);

// remove subscription to the PropertyNodeSwap event later by the handler function
Node.EventPropertyNodeSwap.Disconnect(propertynodeswap_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection propertynodeswap_event_connection;

// subscribe to the PropertyNodeSwap event with a lambda handler function and keeping the connection
propertynodeswap_event_connection = Node.EventPropertyNodeSwap.Connect((Node node,  int index_from,  int index_to) => {
		Log.Message("Handling PropertyNodeSwap event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
propertynodeswap_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
propertynodeswap_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
propertynodeswap_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PropertyNodeSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventPropertyNodeSwap.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventPropertyNodeSwap.Enabled = true;

```

</details>

## 🔒︎ Event< Node , Property > EventPropertySurfaceAdd

The event triggered when a property is assigned to the object's surface. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**, Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PropertySurfaceAdd event handler
void propertysurfaceadd_event_handler(Node node,  Property property)
{
	Log.Message("\Handling PropertySurfaceAdd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertysurfaceadd_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventPropertySurfaceAdd.Connect(propertysurfaceadd_event_connections, propertysurfaceadd_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventPropertySurfaceAdd.Connect(propertysurfaceadd_event_connections, (Node node,  Property property) => {
		Log.Message("Handling PropertySurfaceAdd event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
propertysurfaceadd_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PropertySurfaceAdd event with a handler function
Node.EventPropertySurfaceAdd.Connect(propertysurfaceadd_event_handler);

// remove subscription to the PropertySurfaceAdd event later by the handler function
Node.EventPropertySurfaceAdd.Disconnect(propertysurfaceadd_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection propertysurfaceadd_event_connection;

// subscribe to the PropertySurfaceAdd event with a lambda handler function and keeping the connection
propertysurfaceadd_event_connection = Node.EventPropertySurfaceAdd.Connect((Node node,  Property property) => {
		Log.Message("Handling PropertySurfaceAdd event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
propertysurfaceadd_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
propertysurfaceadd_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
propertysurfaceadd_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PropertySurfaceAdd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventPropertySurfaceAdd.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventPropertySurfaceAdd.Enabled = true;

```

</details>

## 🔒︎ Event< Node , Property > EventPropertySurfaceRemove

The event triggered when a property is removed from the object's surface. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**, Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PropertySurfaceRemove event handler
void propertysurfaceremove_event_handler(Node node,  Property property)
{
	Log.Message("\Handling PropertySurfaceRemove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections propertysurfaceremove_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventPropertySurfaceRemove.Connect(propertysurfaceremove_event_connections, propertysurfaceremove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventPropertySurfaceRemove.Connect(propertysurfaceremove_event_connections, (Node node,  Property property) => {
		Log.Message("Handling PropertySurfaceRemove event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
propertysurfaceremove_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PropertySurfaceRemove event with a handler function
Node.EventPropertySurfaceRemove.Connect(propertysurfaceremove_event_handler);

// remove subscription to the PropertySurfaceRemove event later by the handler function
Node.EventPropertySurfaceRemove.Disconnect(propertysurfaceremove_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection propertysurfaceremove_event_connection;

// subscribe to the PropertySurfaceRemove event with a lambda handler function and keeping the connection
propertysurfaceremove_event_connection = Node.EventPropertySurfaceRemove.Connect((Node node,  Property property) => {
		Log.Message("Handling PropertySurfaceRemove event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
propertysurfaceremove_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
propertysurfaceremove_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
propertysurfaceremove_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PropertySurfaceRemove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventPropertySurfaceRemove.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventPropertySurfaceRemove.Enabled = true;

```

</details>

## 🔒︎ Event< Node > EventCacheNodeAdd

The event triggered when a node is added to cache. Occurs once upon calling [NodeReference.create()](../../../api/library/nodes/class.nodereference_cs.md#NodeReference_constchar) or [*World.LoadNode()*](../../../api/library/engine/class.world_cs.md#loadNode_cstr_int_Node). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CacheNodeAdd event handler
void cachenodeadd_event_handler(Node node)
{
	Log.Message("\Handling CacheNodeAdd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections cachenodeadd_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventCacheNodeAdd.Connect(cachenodeadd_event_connections, cachenodeadd_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventCacheNodeAdd.Connect(cachenodeadd_event_connections, (Node node) => {
		Log.Message("Handling CacheNodeAdd event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
cachenodeadd_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CacheNodeAdd event with a handler function
Node.EventCacheNodeAdd.Connect(cachenodeadd_event_handler);

// remove subscription to the CacheNodeAdd event later by the handler function
Node.EventCacheNodeAdd.Disconnect(cachenodeadd_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection cachenodeadd_event_connection;

// subscribe to the CacheNodeAdd event with a lambda handler function and keeping the connection
cachenodeadd_event_connection = Node.EventCacheNodeAdd.Connect((Node node) => {
		Log.Message("Handling CacheNodeAdd event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
cachenodeadd_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
cachenodeadd_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
cachenodeadd_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CacheNodeAdd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventCacheNodeAdd.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventCacheNodeAdd.Enabled = true;

```

</details>

## 🔒︎ Event< Node > EventNodeLoad

The event triggered when a node is loaded from a file. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the NodeLoad event handler
void nodeload_event_handler(Node node)
{
	Log.Message("\Handling NodeLoad event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeload_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventNodeLoad.Connect(nodeload_event_connections, nodeload_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventNodeLoad.Connect(nodeload_event_connections, (Node node) => {
		Log.Message("Handling NodeLoad event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
nodeload_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the NodeLoad event with a handler function
Node.EventNodeLoad.Connect(nodeload_event_handler);

// remove subscription to the NodeLoad event later by the handler function
Node.EventNodeLoad.Disconnect(nodeload_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection nodeload_event_connection;

// subscribe to the NodeLoad event with a lambda handler function and keeping the connection
nodeload_event_connection = Node.EventNodeLoad.Connect((Node node) => {
		Log.Message("Handling NodeLoad event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
nodeload_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
nodeload_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
nodeload_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring NodeLoad events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventNodeLoad.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventNodeLoad.Enabled = true;

```

</details>

## 🔒︎ Event< Node > EventNodeRemove

The event triggered when the node is deleted. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the NodeRemove event handler
void noderemove_event_handler(Node node)
{
	Log.Message("\Handling NodeRemove event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections noderemove_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventNodeRemove.Connect(noderemove_event_connections, noderemove_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventNodeRemove.Connect(noderemove_event_connections, (Node node) => {
		Log.Message("Handling NodeRemove event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
noderemove_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the NodeRemove event with a handler function
Node.EventNodeRemove.Connect(noderemove_event_handler);

// remove subscription to the NodeRemove event later by the handler function
Node.EventNodeRemove.Disconnect(noderemove_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection noderemove_event_connection;

// subscribe to the NodeRemove event with a lambda handler function and keeping the connection
noderemove_event_connection = Node.EventNodeRemove.Connect((Node node) => {
		Log.Message("Handling NodeRemove event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
noderemove_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
noderemove_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
noderemove_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring NodeRemove events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventNodeRemove.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventNodeRemove.Enabled = true;

```

</details>

## 🔒︎ Event< Node > EventNodeChangeEnabled

The event triggered when the node's *enabled* state is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the NodeChangeEnabled event handler
void nodechangeenabled_event_handler(Node node)
{
	Log.Message("\Handling NodeChangeEnabled event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodechangeenabled_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventNodeChangeEnabled.Connect(nodechangeenabled_event_connections, nodechangeenabled_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventNodeChangeEnabled.Connect(nodechangeenabled_event_connections, (Node node) => {
		Log.Message("Handling NodeChangeEnabled event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
nodechangeenabled_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the NodeChangeEnabled event with a handler function
Node.EventNodeChangeEnabled.Connect(nodechangeenabled_event_handler);

// remove subscription to the NodeChangeEnabled event later by the handler function
Node.EventNodeChangeEnabled.Disconnect(nodechangeenabled_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection nodechangeenabled_event_connection;

// subscribe to the NodeChangeEnabled event with a lambda handler function and keeping the connection
nodechangeenabled_event_connection = Node.EventNodeChangeEnabled.Connect((Node node) => {
		Log.Message("Handling NodeChangeEnabled event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
nodechangeenabled_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
nodechangeenabled_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
nodechangeenabled_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring NodeChangeEnabled events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventNodeChangeEnabled.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventNodeChangeEnabled.Enabled = true;

```

</details>

## 🔒︎ Event< Node , Node > EventNodeClone

The event triggered when copying a node via [Node.Clone()](../../../api/library/nodes/class.node_cs.md#clone_Node). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **node_clone**, Node **node_original**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the NodeClone event handler
void nodeclone_event_handler(Node node_clone,  Node node_original)
{
	Log.Message("\Handling NodeClone event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeclone_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventNodeClone.Connect(nodeclone_event_connections, nodeclone_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventNodeClone.Connect(nodeclone_event_connections, (Node node_clone,  Node node_original) => {
		Log.Message("Handling NodeClone event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
nodeclone_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the NodeClone event with a handler function
Node.EventNodeClone.Connect(nodeclone_event_handler);

// remove subscription to the NodeClone event later by the handler function
Node.EventNodeClone.Disconnect(nodeclone_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection nodeclone_event_connection;

// subscribe to the NodeClone event with a lambda handler function and keeping the connection
nodeclone_event_connection = Node.EventNodeClone.Connect((Node node_clone,  Node node_original) => {
		Log.Message("Handling NodeClone event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
nodeclone_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
nodeclone_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
nodeclone_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring NodeClone events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventNodeClone.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventNodeClone.Enabled = true;

```

</details>

## 🔒︎ Event< Node , Node > EventNodeSwap

The event triggered when swapping a node via [Node.Swap()](../../../api/library/nodes/class.node_cs.md#swap_Node_void). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Node **first_node**, Node **second_node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the NodeSwap event handler
void nodeswap_event_handler(Node first_node,  Node second_node)
{
	Log.Message("\Handling NodeSwap event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections nodeswap_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Node.EventNodeSwap.Connect(nodeswap_event_connections, nodeswap_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Node.EventNodeSwap.Connect(nodeswap_event_connections, (Node first_node,  Node second_node) => {
		Log.Message("Handling NodeSwap event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
nodeswap_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the NodeSwap event with a handler function
Node.EventNodeSwap.Connect(nodeswap_event_handler);

// remove subscription to the NodeSwap event later by the handler function
Node.EventNodeSwap.Disconnect(nodeswap_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection nodeswap_event_connection;

// subscribe to the NodeSwap event with a lambda handler function and keeping the connection
nodeswap_event_connection = Node.EventNodeSwap.Connect((Node first_node,  Node second_node) => {
		Log.Message("Handling NodeSwap event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
nodeswap_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
nodeswap_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
nodeswap_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring NodeSwap events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Node.EventNodeSwap.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Node.EventNodeSwap.Enabled = true;

```

</details>

## 🔒︎ bool IsCache

The value indicating whether the node or any of its parent nodes are stored in the cache.
## 🔒︎ string SrcFilePath

The path to the source of the node. For example, a relative path to the `*.world` file with a description of this node, or the identifier of the source `*.node` in the format `guid://...`
## 🔒︎ string HierarchyPath

The [nodes hierarchy](../../../principles/world_structure/index.md#nodes_hierarchy). Displays the node name and the names of all its parent nodes as specified in *World Hierarchy* window.
## 🔒︎ string Info

The the information about the given node: type, name, ID, file path, hierarchy.
### Members

---

## Node GetAncestor ( int num )

Returns a node ancestor by its number.
### Arguments

- *int* **num** - Ancestor ID.

### Return value

Ancestor node.
## Node GetChild ( int num )

Returns a node child by its number.
### Arguments

- *int* **num** - Child ID.

### Return value

Child node.
## bool IsChild ( Node n )

Checks if a given node is a child of the node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **n** - Node to check.

### Return value

true if the given node is a child; otherwise, false.
## void SetChildIndex ( Node n , int index )

Sets the index for a given child node of the node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **n** - Child node.
- *int* **index** - Node index.

## int GetChildIndex ( Node n )

Returns the index of a given child node of the node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **n** - Child node.

### Return value

Node index.
## void SetData ( string name , string data )

Sets user data associated with the node.
- If the node was loaded from the `*.node` file, data is saved directly into the data tag of this file.
- If the node is loaded from the `*.world` file, data is saved into the Node data tag of the `*.world` file.
- If the node is loaded from the `*.world` file as a NodeReference, data will be saved to the NodeReference data tag of the `*.world` file.


### Arguments

- *string* **name** - String containing a key identifying user data to be stored in the `*.node` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.
- *string* **data** - New user data. Data can contain an XML formatted string.

## string GetData ( string name )

Returns user data associated with the node.
- If the node was loaded from the `*.node` file, data from the data tag of this file is returned.
- If the node is loaded from the `*.world` file, data from the Node data tag of the `*.world` file is returned.
- If the node is loaded from the `*.world` file as a NodeReference, data from the NodeReference data tag of the `*.world` file is returned.


### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.node` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

### Return value

User string data. Data can be an xml formatted string.
## void UpdateEnabled ( )

Updates node's internal state according to the current "*enabled*" state.
## bool IsEnabledSelf ( )

Returns a value indicating if the node is enabled.
### Return value

true if the node is enabled; otherwise, false.
## void GetHierarchy ( Node [] OUT_hierarchy )

Retrieves the whole hierarchy of the node and puts it to the hierarchy buffer.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_hierarchy** - Hierarchy buffer. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Node GetNode ( int id )

Returns a node pointer.
### Arguments

- *int* **id** - Node identifier.

### Return value

Node pointer.
## bool IsNode ( Node node )

Check the node pointer.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node pointer.

### Return value

true if the node is valid; otherwise, false.
## bool IsNode ( int id )

Check the node pointer.
### Arguments

- *int* **id** - Node pointer.

### Return value

true if the node is valid; otherwise, false.
## int AddProperty ( string name )

Inherits a new property from the one with the given name and adds it to the list of properties associated with the node. The inherited property will be internal, such properties are saved in a `*.world` or `*.node` file.
### Arguments

- *string* **name** - Name of the property to be added.

### Return value

Index of the new node property if it was added successfully; otherwise, -1.
## int AddProperty ( UGUID guid )

Inherits a new property from the one with the given GUID and adds it to the list of properties associated with the node. The inherited property will be internal, such properties are saved in a `*.world` or `*.node` file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to be added.

### Return value

Index of the new node property if it was added successfully; otherwise, -1.
## int AddProperty ( Property property )

Inherits a new property from the specified one and adds it to the list of properties associated with the node. The inherited property will be internal, such properties are saved in a `*.world` or `*.node` file.
### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property to be added.

### Return value

Index of the new node property if it was added successfully; otherwise, -1.
## bool InsertProperty ( int num , string name )

Inserts the property with the specified name at the specified position.
### Arguments

- *int* **num** - Position at which a new property is to be inserted, in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *string* **name** - Name of the property to be inserted.

### Return value

true if the property with the specified name was successfully inserted at the specified position; otherwise, false.
## bool InsertProperty ( int num , UGUID guid )

Inserts the property with the specified GUID at the specified position.
### Arguments

- *int* **num** - Position at which a new property is to be inserted, in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to be inserted.

### Return value

true if the property with the specified GUID was successfully inserted at the specified position; otherwise, false.
## bool InsertProperty ( int num , Property property )

Inserts the specified property at the specified position.
### Arguments

- *int* **num** - Position at which a new property is to be inserted, in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property to be added.

### Return value

true if the specified property was successfully inserted at the specified position; otherwise, false.
## bool InsertProperty ( int num , UGUID guid , UGUID new_guid )

### Arguments

- *int* **num**
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid**
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_guid**

## bool InsertProperty ( int num , Property property , UGUID new_guid )

### Arguments

- *int* **num**
- *[Property](../../../api/library/common/class.property_cs.md)* **property**
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_guid**

## bool SetProperty ( string name )

Updates the first node property (the one with a 0 index) in the list of properties associated with the node. A new internal property inherited from the one with the specified name will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *string* **name** - Name of the property to be set.

### Return value

true if the node property is updated successfully; otherwise, false.
## bool SetProperty ( UGUID guid )

Updates the first node property (the one with a 0 index) in the list of properties associated with the node. A new internal property inherited from the one with the specified GUID will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to be set.

### Return value

true if the node property is updated successfully; otherwise, false.
## bool SetProperty ( Property property )

Updates the first node property (the one with a 0 index) in the list of properties associated with the node. A new internal property inherited from the one specified will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property to be set.

### Return value

true if the node property is updated successfully; otherwise, false.
## bool SetProperty ( int num , string name )

Updates the node property with the specified number. A new internal property inherited from the one with the specified name will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *string* **name** - Name of the property to be set.

### Return value

true if the specified node property is updated successfully; otherwise, false.
## bool SetProperty ( int num , UGUID guid )

Updates the node property with the specified number. A new internal property inherited from the one with the specified GUID will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to be set.

### Return value

true if the specified node property is updated successfully; otherwise, false.
## bool SetProperty ( int num , Property property )

Updates the node property with the specified number. A new internal property inherited from the specified one will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property to be set.

### Return value

true if the specified node property is updated successfully; otherwise, false.
## bool SetProperty ( int num , UGUID guid , UGUID new_guid )

### Arguments

- *int* **num**
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid**
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_guid**

## bool SetProperty ( int num , Property property , UGUID new_guid )

### Arguments

- *int* **num**
- *[Property](../../../api/library/common/class.property_cs.md)* **property**
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_guid**

## void SetPropertyEnabled ( int num , bool enable )

Enables or disables the node property with the specified number.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *bool* **enable** - true to enable the specified node property, false to disable it.

## bool IsPropertyEnabled ( int num )

Returns a value indicating if the node property with the specified number is enabled.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

true if the specified property is enabled; otherwise, false.
## void SwapProperty ( int from_num , int to_num )

Swaps two properties with specified numbers in the list of properties associated with the node.
> **Notice:** The order of properties in the list determines the execution sequence of logic of corresponding [components](../../../principles/component_system/index.md) (if any).


### Arguments

- *int* **from_num** - Number of the first node property to be swapped, in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *int* **to_num** - Number of the second node property to be swapped, in the range from 0 to the [total number of node properties](#getNumProperties_int).

## void RemoveProperty ( int num )

Removes the node property with the specified number.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

## void RemoveProperty ( string name )

Removes the node property that has the specified name.
> **Notice:** If several properties with the same name are associated with the node, only the first one will be removed.


### Arguments

- *string* **name** - Name of the node property to be removed.

## void RemoveProperty ( UGUID guid )

Removes the node property that has the GUID or parent GUID equal to the specified one.
> **Notice:** If several such properties are associated with the node, only the first one will be removed.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to be removed (or GUID of its parent).

## void RemoveProperty ( Property property )

Removes the specified node property or a node property inherited from it.
> **Notice:** If several such properties are associated with the node, only the first one will be removed.


### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Node property to be removed.

## void ClearProperties ( )

Clears the list of properties associated with the node.
## Property GetProperty ( int num )

Returns a node property with the specified number if it exists.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

Node property smart pointer, if exists; otherwise, NULL.
## string GetPropertyName ( int num )

Returns the name of a node property with the specified number.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

Property name, if exists; otherwise, NULL.
## int FindProperty ( string name )

Searches for a property with the specified name among the ones assigned to the node.
### Arguments

- *string* **name** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a node property to be found.

### Return value

Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int) if such a property exists; otherwise -1.
## int FindProperty ( UGUID guid )

Searches for a property with the specified [GUID](../../../api/library/filesystem/class.uguid_cs.md) among the ones assigned to the node.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a node property to be found.

### Return value

Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int) if such a property exists; otherwise -1.
## int FindProperty ( Property property )

Searches for a specified property among the ones assigned to the node.
### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Node property to be found.

### Return value

Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int) if such a property exists; otherwise -1.
## bool HasQueryForce ( )

Returns a value indicating if the *[Culled By Occlusion Query](../../../editor2/node_parameters/transformation_common/index.md#query)*option is force-enabled for the node by the Engine.
### Return value

true if the *[Culled By Occlusion Query](../../../editor2/node_parameters/transformation_common/index.md#query)*option is force-enabled for the node by the Engine; otherwise, false.
## void SetRotation ( quat rot , bool identity = 0 )

Sets the node rotation.
### Arguments

- *quat* **rot** - Quaternion representing node rotation in the local space.
- *bool* **identity** - Flag indicating if node's scale is to be ignored or taken into account: > **Notice:** - It is recommended to set this flag for all non-scaled nodes to improve performance and accuracy. > - **Scaling of nodes should be avoided whenever possible**, as it requires addidional calculations and may lead to error accumulation.

  - false - node's scale is taken into account. In this case additional calculations are performed to extract current node's scale and apply it when building the final transformation matrix. These additional operations reduce performance and may lead to error accumulation.
  - true - node's scale is ignored (assumed to be equal to **1** along all axes). Thus, the number of calculations performed for each rotation is reduced and error accumulation is minimal.

## quat GetRotation ( )

Returns the node rotation.
### Return value

Quaternion representing node rotation in the local space.
## void SetWorldRotation ( quat rot , bool identity = 0 )

Sets the node rotation in the world space.
### Arguments

- *quat* **rot** - Node rotation in the world space.
- *bool* **identity** - Flag indicating if node's scale is to be ignored or taken into account: > **Notice:** - It is recommended to set this flag for all non-scaled nodes to improve performance and accuracy. > - **Scaling of nodes should be avoided whenever possible**, as it requires addidional calculations and may lead to error accumulation.

  - false - node's scale is taken into account. In this case additional calculations are performed to extract current node's scale and apply it when building the final transformation matrix. These additional operations reduce performance and may lead to error accumulation.
  - true - node's scale is ignored (assumed to be equal to **1** along all axes). Thus, the number of calculations performed for each rotation is reduced and error accumulation is minimal.

## quat GetWorldRotation ( )

Returns the node rotation in the world space.
### Return value

Node rotation in the world space.
## void SetTransformWithoutChildren ( mat4 transform )

Sets the transformation matrix for the node in local coordinates (transformations of all node's children are not affected). This method can be used to change node's transformation relative to its children.
### Arguments

- *mat4* **transform** - New transformation matrix to be set for the node (local coordinates).

## Node.TYPE GetTypeID ( string type )

Returns the ID of a node type with a given name.
### Arguments

- *string* **type** - Node type name.

### Return value

Node type ID, if such type exists; otherwise, -1.
## string GetTypeName ( Node.TYPE type )

Returns the name of a node type with a given ID.
### Arguments

- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **type** - Node type ID.

### Return value

Node type name.
## void setVariable ( )

Sets the value of a variable with a given name. If such variable does not exist it will be added with a specified value.
```csharp
	NodeDummy container;
	if(container.HasVariable("key1")) {
	container.SetVariable("key1", new Variable(42));
	}

	Variable value = container.GetVariable("key1");
	container.RemoveVariable("key1");

```


### Arguments

## Variable GetVariable ( )

Returns the variable with a given name.
```csharp
	NodeDummy container;
	if(container.HasVariable("key1")) {
	container.SetVariable("key1", new Variable(42));
	}

	Variable value = container.GetVariable("key1");
	container.RemoveVariable("key1");

```


### Arguments

### Return value

Variable if it exists; otherwise, variable with 0 value.
## void SetWorldParent ( Node n )

Sets the new parent of the node. Transformations of the current node will be done in the world coordinates.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **n** - New parent node or null.

## void SetWorldTransformWithoutChildren ( mat4 transform )

Sets the transformation matrix for the node in world coordinates (transformations of all node's children are not affected). This method can be used to change node's transformation relative to its children.
### Arguments

- *mat4* **transform** - New transformation matrix to be set for the node (world coordinates).

## vec3 GetBodyWorldVelocity ( vec3 point )

Returns linear velocity of a point of the node's physical body in the world space.
### Arguments

- *vec3* **point** - Target point.

### Return value

Linear velocity in the world space.
## void AddChild ( Node n )

Adds a child to the node. Transformations of the new child will be done in the coordinates of the parent.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **n** - New child node.

## void AddWorldChild ( Node n )

Adds a child to the node. Transformations of the new child will be done in the world coordinates.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **n** - New child node.

## Node Clone ( )

Clones the node.
### Return value

Cloned node.
## int FindAncestor ( int type )

Returns the ID of node's ancestor of a given type.
### Arguments

- *int* **type** - Ancestor type identifier. One of the [*NODE_**](#NODE_DUMMY) pre-defined variables.

### Return value

Ancestor ID if it exists; otherwise -1.
## int FindAncestor ( string name )

Returns the ID of node's ancestor with a given name.
### Arguments

- *string* **name** - Ancestor name.

### Return value

Ancestor ID if it exists; otherwise -1.
## int FindChild ( string name )

Searches for a child node with a given name among the children of the node.
### Arguments

- *string* **name** - Name of the child node.

### Return value

Child node number, if it is found; otherwise, -1.
## Node FindNode ( string name , int recursive = 0 )

Searches for a node with a given name among the children of the node.
### Arguments

- *string* **name** - Name of the child node to search for.
- *int* **recursive** - **1** if the search is recursive (i.e. performed for children of child nodes); otherwise, **0**.

### Return value

Child node, if it is found; otherwise, NULL.
## void FindNodes ( string name , Node [] OUT_nodes , int recursive = 0 )

Searches for a node with a given name among the children of the node and puts them to the specified output *nodes* buffer.
### Arguments

- *string* **name** - Name of the node to search for.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Output buffer to which all found nodes with the specified name will be put. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **recursive** - **1** if the search is recursive (i.e. performed for children of child nodes); otherwise, **0**.

## bool LoadWorld ( Xml xml )

Loads a node state from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml smart pointer.

### Return value

true if the node state is loaded successfully; otherwise, false.
## void RemoveChild ( Node n )

Removes a child node (added by the *[addChild()](#addChild_Node_void)* method) from the list of children.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **n** - Child node to remove.

## void RemoveWorldChild ( Node n )

Removes a child node (added by the *[addWorldChild()](#addWorldChild_Node_void)* method) from the list of children.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **n** - Child node to remove.

## void RenderVisualizer ( )

Renders a bounding box / sphere of the object.
> **Notice:** You should enable the engine visualizer by the `show_visualizer 1` console command.


## bool SaveState ( Stream stream )

Saves a node state to a binary stream.
**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```csharp
// initialize a node and set its state
NodeDummy node = new NodeDummy();
node.Position = new vec3(1, 1, 0);

// save state
Blob blob_state = new Blob();
node.SaveState(blob_state);

// change the node state
node.Position = new vec3(0, 0, 0);

// restore state
blob_state.SeekSet(0);	  // returning the carriage to the start of the blob
node.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to save node state data.

### Return value

true if node state is successfully saved; otherwise, false.
## bool RestoreState ( Stream stream )

Restores a node state from a binary stream.
**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```csharp
// initialize a node and set its state
NodeDummy node = new NodeDummy();
node.Position = new vec3(1, 1, 0);

// save state
Blob blob_state = new Blob();
node.SaveState(blob_state);

// change the node state
node.Position = new vec3(0, 0, 0);

// restore state
blob_state.SeekSet(0);		// returning the carriage to the start of the blob
node.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream with saved node state data.

### Return value

true if node state is successfully restored; otherwise, false.
## bool SaveWorld ( Xml xml )

Saves the node into the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml smart pointer.

### Return value

true if the node is successfully saved; otherwise, false.
## void Swap ( Node n )

Swaps two nodes.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **n** - Node to swap.

## vec3 ToLocal ( vec3 p )

Converts a given vector in the world space to the node's local space.
### Arguments

- *vec3* **p** - Vector in the world space.

### Return value

Vector in the local space.
## vec3 ToWorld ( vec3 p )

Converts a given vector in the local space to the world space.
### Arguments

- *vec3* **p** - Vector in the local space.

### Return value

Vector in the world space.
## void Translate ( vec3 t )

Translates the node relative to its local coordinate system: the parent node transformation isn't taken into account.
### Arguments

- *vec3* **t** - Translation vector.

## void Translate ( Scalar x , Scalar y , Scalar z )

Translates the node relative to its local coordinate system: the parent node transformation isn't taken into account.
### Arguments

- *Scalar* **x** - Node translation along the X axis, in units.
- *Scalar* **y** - Node translation along the Y axis, in units.
- *Scalar* **z** - Node translation along the Z axis, in units.

## void WorldTranslate ( vec3 t )

Translates the node in the world space using the specified vector.
### Arguments

- *vec3* **t** - Translation vector.

## void WorldTranslate ( Scalar x , Scalar y , Scalar z )

Translates the node in the world space using the values specified for the corresponding axes.
### Arguments

- *Scalar* **x** - Node translation along the X axis, in units.
- *Scalar* **y** - Node translation along the Y axis, in units.
- *Scalar* **z** - Node translation along the Z axis, in units.

## void WorldLookAt ( vec3 target , vec3 up )

Reorients the node to "look" at the target point and sets the given up vector:
- If the node is a [Player-related](#isPlayer_int) one, it will "look" at the target point along the negative Z axis. The Y axis will be oriented along the specified up vector.
- Other nodes will "look" at the target point along the Y axis. The Z axis will be oriented along the specified up vector.


### Arguments

- *vec3* **target** - Coordinates of the target point in the world space.
- *vec3* **up** - Up vector of the node in the world space. By default, the up vector is oriented along the Z axis.

## void WorldLookAt ( vec3 target )

Reorients the node to "look" at the target point. The up vector is oriented along the Z axis.
- If the node is a [Player-related](#isPlayer_int) one, it will "look" at the target point along the negative Z axis. The Y axis will be oriented along the world Z axis.
- Other nodes will "look" at the target point along the Y axis.


### Arguments

- *vec3* **target** - Coordinates of the target point in the world space.

## void Rotate ( quat r )

Rotates the node relative to its local coordinate system: the parent node transformation isn't taken into account. Rotation is determined by the specified [quaternion](../../../api/library/math/class.quat_cs.md).
### Arguments

- *quat* **r** - Rotation quaternion.

## void Rotate ( vec3 angles )

Rotates the node in the local space. Rotation is determined by Euler angles passed as a [vec3](../../../api/library/math/class.vec3_cs.md) vector.
### Arguments

- *vec3* **angles**

## void Rotate ( float angle_x , float angle_y , float angle_z )

Rotates the node in the world space according to specified Euler angles.
### Arguments

- *float* **angle_x** - Pitch angle, in degrees.
- *float* **angle_y** - Roll angle, in degrees.
- *float* **angle_z** - Yaw angle, in degrees.

## void WorldRotate ( quat r )

Rotates the node in the world space. Rotation is determined by the specified [quaternion](../../../api/library/math/class.quat_cs.md).
### Arguments

- *quat* **r** - Rotation quaternion.

## void WorldRotate ( vec3 angles )

Rotates the node in the world space. Rotation is determined by Euler angles passed as a [vec3](../../../api/library/math/class.vec3_cs.md) vector.
### Arguments

- *vec3* **angles** - Vector containing Euler angles (Pitch, Yaw, Roll).

## void WorldRotate ( float angle_x , float angle_y , float angle_z )

Rotates the node in the world space according to specified Euler angles.
### Arguments

- *float* **angle_x** - Pitch angle, in degrees.
- *float* **angle_y** - Roll angle, in degrees.
- *float* **angle_z** - Yaw angle, in degrees.

## void SetDirection ( vec3 dir , vec3 up , MathLib.AXIS axis = AXIS_NZ )

Updates the direction vector of the node and reorients this node: the specified axis of the node becomes oriented along the specified vector in local coordinates. For example, after running the code below, you will get the X axis of the node pointed along the Y axis in local coordinates.
```csharp
// get the node
Node node = World.GetNodeByName("material_ball");
// set the X axis to be pointed along the Y axis in local coordinates
node.SetDirection(new vec3(0.0f,1.0f,0.0f),new vec3(0.0f,0.0f,1.0f),MathLib.AXIS.X);

```


### Arguments

- *vec3* **dir** - New direction vector in local coordinates. The direction vector always has unit length.
- *vec3* **up** - New up vector in local coordinates. If you skip this argument, the Z axis (in local coordinates) will be used. Note that the specified up vector is a hint vector only: the node's up vector points in the direction hinted by the specified up vector. The node's up vector matches the specified up vector (*up*) only if it is perpendicular to the specified direction vector (*dir*).
- *MathLib.AXIS* **axis** - Axis along which the direction vector should be pointed. The default is the negative Z axis.

## vec3 GetDirection ( MathLib.AXIS axis = AXIS_NZ )

Returns the normalized direction vector pointing along the given node axis in local coordinates (i.e. relative to the node's parent). By default, the direction vector pointing along the negative Z axis of the node (in local coordinates) is returned. The direction vector always has a unit length.
```csharp
node.GetDirection(node.IsPlayer ? MathLib.AXIS.NZ : MathLib.AXIS.Y); // forward direction vector
node.GetDirection(node.IsPlayer ? MathLib.AXIS.Z : MathLib.AXIS.NY); // backward direction vector
node.GetDirection(node.IsPlayer ? MathLib.AXIS.Y : MathLib.AXIS.Z); // upward direction vector
node.GetDirection(node.IsPlayer ? MathLib.AXIS.NY : MathLib.AXIS.NZ); // down direction vector
node.GetDirection(MathLib.AXIS.X); // right direction vector
node.GetDirection(MathLib.AXIS.NX); // left direction vector

```


### Arguments

- *MathLib.AXIS* **axis** - Axis along which the direction vector points. The default is the negative Z axis.

### Return value

Direction vector in local coordinates.
## void SetWorldDirection ( vec3 dir , vec3 up , MathLib.AXIS axis = AXIS_NZ )

Updates the direction vector of the node and reorients this node: the specified axis of the node becomes oriented along the specified vector in world coordinates. For example, after running the code below, you will get the X axis of the node pointed along the Y axis in world coordinates:
```csharp
// get the node
Node node = World.GetNodeByName("material_ball");
// set the X axis to be pointed along the Y axis in world coordinates
node.SetWorldDirection(new vec3(0.0f,1.0f,0.0f),new vec3(0.0f,0.0f,1.0f),MathLib.AXIS.X);

```


### Arguments

- *vec3* **dir** - New direction vector in world coordinates. The direction vector always has unit length.
- *vec3* **up** - New up vector in world coordinates. If you skip this argument, the Z axis (in local coordinates) will be used. Note that the specified up vector is a hint vector only: the node's up vector points in the direction hinted by the specified up vector. The node's up vector matches the specified up vector (*up*) only if it is perpendicular to the specified direction vector (*dir*).
- *MathLib.AXIS* **axis** - Axis along which the direction vector should be pointed. The default is the negative Z axis.

## vec3 GetWorldDirection ( MathLib.AXIS axis = AXIS_NZ )

Returns the normalized direction vector pointing along the given node axis in world coordinates. By default, the direction vector pointing along the negative Z axis of the node is returned. The direction vector always has a unit length.
```csharp
node.GetWorldDirection(node.IsPlayer() ? MathLib.AXIS.NZ : MathLib.AXIS.Y); // forward direction vector
node.GetWorldDirection(node.IsPlayer() ? MathLib.AXIS.Z : MathLib.AXIS.NY); // backward direction vector
node.GetWorldDirection(node.IsPlayer() ? MathLib.AXIS.Y : MathLib.AXIS.Z); // upward direction vector
node.GetWorldDirection(node.IsPlayer() ? MathLib.AXIS.NY : MathLib.AXIS.NZ); // down direction vector
node.GetWorldDirection(MathLib.AXIS.X); // right direction vector
node.GetWorldDirection(MathLib.AXIS.NX); // left direction vector

```


### Arguments

- *MathLib.AXIS* **axis** - Axis along which the direction vector points. The default is the negative Z axis.

### Return value

Direction vector in world coordinates.
## Node GetCloneNode ( Node original_node )

Returns a node cloned from the specified original node.
> **Notice:** This method is intended for use only inside the [node clone callback](#getEventNodeClone_Event).


### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **original_node** - Original node that was cloned.

### Return value

Clone of the specified original node if it exists; otherwise the original node itself.
## Property GetCloneProperty ( Property original_property )

Returns a node property cloned from the specified original property.
> **Notice:** This method is intended for use only inside the [node clone callback](#getEventNodeClone_Event).


### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **original_property** - Original node property that was cloned.

### Return value

Clone of the specified original node property if it exists; otherwise the original node property itself.
## void SetSaveToWorldEnabledRecursive ( bool enable )

Sets a value indicating if saving to `*.world` file is enabled for the node and all its children (if any).
### Arguments

- *bool* **enable** - true to enable saving to `*.world` file for the node and all its children (if any); 0 to disable.

## void SetShowInEditorEnabledRecursive ( bool enable )

Sets a value indicating if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) is enabled for the node and all its children (if any).
### Arguments

- *bool* **enable** - true to enable displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) for the node and all its children (if any); 0 to disable.

## Node.LIFETIME GetLifetimeSelf ( )

Returns the lifetime management type set for the node itself.
> **Notice:** Lifetime of each node in the hierarchy is defined by it's root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)). Setting lifetime management type for a child node different from the one set for the root has no effect.


### Return value

Lifetime management type for the node (see the [*LIFETIME*](#LIFETIME) enum).
## WorldBoundBox GetHierarchyBoundBox ( bool only_enabled_nodes = false )

Returns a bounding box with local coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding box recalculation when transforming nodes.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding box with world coordinates.
## WorldBoundSphere GetHierarchyBoundSphere ( bool only_enabled_nodes = false )

Returns a bounding sphere with local coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding sphere recalculation when transforming nodes.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding sphere with world coordinates.
## WorldBoundBox GetHierarchyWorldBoundBox ( bool only_enabled_nodes = false )

Returns a bounding box with world coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding box recalculation when transforming nodes.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding box with world coordinates.
## WorldBoundSphere GetHierarchyWorldBoundSphere ( bool only_enabled_nodes = false )

Returns a bounding sphere with world coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding sphere recalculation when transforming nodes.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding sphere with world coordinates.
## WorldBoundBox GetHierarchySpatialBoundBox ( bool only_enabled_nodes = false )

Returns a bounding box with world coordinates that takes all children and physics into account. This bounding box is used by the spatial tree.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding box with world coordinates.
## WorldBoundSphere GetHierarchySpatialBoundSphere ( bool only_enabled_nodes = false )

Returns a bounding sphere with world coordinates that takes all children and physics into account. This bounding sphere is used by the spatial tree.
### Arguments

- *bool* **only_enabled_nodes** - Set true to obtain the result taking into account only the nodes in the hierarchy that are enabled, or false - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding sphere with world coordinates.
## virtual void UpdateSpatialTree ( )

Updates node bounds in the [spatial tree](../../../principles/world_management/index.md#outdoor) in the current frame. This method can be used in case you use some custom logic affecting node bounds or position and need to have your changes to be taken into account in the current frame, as well as to process such changes for your custom nodes ( *[ObjectExtern](../../../api/library/objects/class.objectextern_cs.md), [NodeExtern](../../../api/library/nodes/class.nodeextern_cs.md)*) which are otherwise ignored. Calling this method enables you to apply changes for this node fast without complete tree recalculation. But you should be aware that node bounds fast-updated this way **might be inaccurate** (they can only be expanded, as shrinking will require tree recalculation). In case you need to have 100% accurate bounds in the current frame, call the *[World.UpdateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method. You can also simply tell the spatial tree to update node bounds in the next frame via the *[UpdateSpatialTreeDelayed()](../../...md#updateSpatialTreeDelayed_void)* method.
## void UpdateSpatialTreeDelayed ( )

Mark node bounds in the spatial tree to be updated in the next frame (all bounds will be 100% accurate in this case unlike for the *[UpdateSpatialTree()](../../...md#updateSpatialTree_void)* method). This method can be used in case you use some custom logic affecting node bounds or position, as well as to process such changes for your custom nodes ( *[ObjectExtern](../../../api/library/objects/class.objectextern_cs.md), [NodeExtern](../../../api/library/nodes/class.nodeextern_cs.md)*) which are otherwise ignored. The changes will only be applied in the next frame, in case you need to have your changes to be taken into account right in the current frame use the *[World.UpdateSpatial()](../../../api/library/engine/class.world_cs.md#updateSpatial_void)* method for 100% accurate bounds (slow), or the fast *[UpdateSpatialTree()](../../...md#updateSpatialTree_void)* method which only expands node bounds if necessary.
## WorldTrigger GetWorldTrigger ( int num )

Returns one of the World Triggers inside which the node is located at the moment by its number. For any node in the world, you can [check whether it is currently inside any World Trigger](#getNumWorldTriggers_int) and access any of such triggers by simply calling this method.
### Arguments

- *int* **num** - Number of the World Trigger in the list of World Triggers inside which the node is located at the moment.

### Return value

World Trigger with the specified number inside which the node is located at the moment.
## UGUID GetLostNodePropertyGUID ( int num )

Returns the [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a lost property assigned to the node. If for some reason a property assigned to the specified slot of the node is missing, this method can be used to get it's GUID.
### Arguments

- *int* **num** - Target property slot number.

### Return value

Lost property [GUID](../../../api/library/filesystem/class.uguid_cs.md).
## void RenderBounds ( bool render_node_bound = true , bool render_instance_bound = false )

Renders the node bounds. The method is applied for checking the actual size of the CPU-rendered node bounds that may differ from the GPU-rendered mesh size, if the latter has been modified by the shader. For nodes that consist of multiple mesh instances (Clutter, Cluster) rendering of each individual mesh bound is also available.
### Arguments

- *bool* **render_node_bound** - true to enable rendering of the node bounds, false to disable it.
- *bool* **render_instance_bound** - true to enable bound rendering for each individual mesh instance (applicable for Clutter and Cluster nodes), false to disable it.

## void ApplyReplacePaths ( )

Restores the engine's ability to replace baked textures (lightmap, shadow map) inside Node References in runtime. This method is to be applied if hierarchy inside a Node Reference or a path to the baked texture has been modified thus causing rendering of an unsuitable lightmap or a shadow map.
## void GetNodes ( Node [] OUT_nodes )

Takes a node collection, clears it, and then adds all existing nodes to it. This includes nodes from the world and other sources, such as cached nodes or nodes currently being loaded via AsyncQueue.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Node сollection. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool HasData ( string name )

Checks if there is user data associated with the node.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.node` file.

### Return value

true if the given node has user data; otherwise, false.
## void RemoveData ( string name )

Removes user data associated with the node.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.node` file.
