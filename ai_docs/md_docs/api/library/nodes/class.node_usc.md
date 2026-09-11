# Unigine.Node Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


In terms of Unigine, all of the objects added into the scene are called [nodes](../../../objects/nodes/index.md). Nodes can be of different types, determining their visual representation and behavior.


The node is created and stored in the world. All changes are saved into the `.world` file.


The node can be also [saved](../../../api/library/engine/class.world_usc.md#saveNode_cstr_Node_int_int) into an external `.node` file and then [imported](../../../api/library/engine/class.world_usc.md#loadNode_cstr_int_Node) into the world when necessary. Also it is possible to create a [reference](../../../api/library/nodes/class.nodereference_usc.md) to the exported node.


You can associate any [string data](#setData_cstr_cstr_void) (written directly into a *.node or a *.world file) or an arbitrary [user variable](#setVariable_Variable_void) with a node.


### See Also


- How to handle [ownership](../../../code/uniginescript/memory_management.md)
- How to work with the node's [matrix transformations](../../../code/fundamentals/matrix_transformations/index_usc.md)


### Creating a Node


The Node class doesn't provide creating of a node. You can create an instance of any class inherited from the Node class and then operate it as it is an instance of the Node class.

> **Notice:** Only UnigineScript provides such option. For C++ and C#, see the corresponding version of the article.


For example:

1. Use a mesh-file to create an instance of the [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_usc.md) class. This class is inherited from the Node class.
2. Operate the ObjectMeshStatic instance as a node.


```cpp
// unigine_project.cpp

#include <core/unigine.h>

int init() {
	// create an instance of any class inherited from the Node class (e.g. ObjectMeshStatic)
	ObjectMeshStatic object_mesh = new ObjectMeshStatic("core/meshes/box.mesh");

	// operate the ObjectMeshStatic as a node

	return 1;
}

```


### Editing a Node and Saving Changes


The Node class contains common settings of the node. Also each node has special settings, which vary depending on the type of the node.

> **Notice:** The special settings of a node can be found in the article on the corresponding class.


Editing the node also includes editing materials and properties assigned to the node.


For the edited node to be saved in the `.world` file, you should enable the corresponding option via the *[setSaveToWorldEnabled()](#setSaveToWorldEnabled_int_void)* method.

> **Notice:** The node shall be saved to a `*.world` file only if this option is enabled for all of its ancestors as well.


For example:

1. Create a box mesh by using the [Mesh](../../../api/library/rendering/class.mesh_usc.md) class.
2. Save the mesh on the disk. It is required as the node we are going to export need to reference to a mesh stored on the disk.
3. Use the saved `.mesh` file to create an instance of the [ObjectMeshDynamic](../../../api/library/objects/class.objectmeshdynamic_usc.md) class. This class is inherited from the Node class.
4. Edit the node and then save the world by calling the `world_save`console command.


```cpp
// unigine_project.cpp

#include <core/unigine.h>

int init() {

	// create a mesh
	Mesh mesh = new Mesh();
	mesh.addBoxSurface("box_0", vec3(1.0f));
	// save a mesh into a file on the disk
	mesh.save("unigine_project/meshes/my_mesh.mesh");
	// create an instance of any class inherited from the Node class (e.g. ObjectMeshDynamic)
	ObjectMeshDynamic object_mesh = new ObjectMeshDynamic("unigine_project/meshes/my_mesh.mesh");

	// change the node name
	object_mesh.setName("my_node");
	// change node transformation
	object_mesh.setWorldTransform(translate(Vec3(0.0f, 0.0f, 2.0f)));

	// save node changes in the .world file
	engine.console.run("world_save");

	return 1;
}

```


### Exporting and Importing a Node


To export a node stored in the world into the external `.node` file, you should pass it to the *[saveNode()](../../../api/library/engine/class.world_usc.md#saveNode_cstr_Node_int_int)* method of the World class.


To import the existing node stored in the `.node` file to the world, you should call the *[loadNode()](../../../api/library/engine/class.world_usc.md#loadNode_cstr_int_Node)* method of the World class.


For example:


1. Create a box mesh by using the [Mesh](../../../api/library/rendering/class.mesh_usc.md) class.
2. Save the mesh on the disk. It is required as the node we are going to export need to reference to a mesh stored on the disk.
3. Use the saved `.mesh` file to create an instance of the [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_usc.md) class. This class is inherited from the Node class.
4. Export the node to an external `.node` file.
5. Import the previously exported node and add it to the editor to check the result.


```cpp
// unigine_project.cpp

#include <core/unigine.h>

int init() {

	// create a mesh
	Mesh mesh = new Mesh();
	mesh.addBoxSurface("box_0", vec3(1.0f));
	// save a mesh into a file on the disk
	mesh.save("unigine_project/meshes/my_mesh.mesh");
	// create an instance of any class inherited from the Node class (e.g. ObjectMeshStatic)
	ObjectMeshStatic object_mesh = new ObjectMeshStatic("unigine_project/meshes/my_mesh.mesh");

	// export the node into a .node file
	engine.world.saveNode("unigine_project/nodes/my_node.node",object_mesh);
	// import the exported node to check the result
	Node imported_node = engine.world.loadNode("unigine_project/nodes/my_node.node");

	// set a position of the node
	imported_node.setPosition(Vec3(4.0f, 0.0f, 1.0f));

	return 1;
}

```


### Deleting a Node


By default each new node's lifetime matches the lifetime of the **World** (i.e. such node shall be deleted when the world is closed). But you can also choose node's lifetime to be managed:


- **by the Engine** - is this case the node shall be deleted automatically on Engine shutdown.
- **manually** - is this case the node should be deleted manually by the user.


To delete a node you can use the following two methods:


- [*deleteLater()*](../../../api/library/common/class.ptr_usc.md#deleteLater_void) - performs delayed deletion, in this case the object will be deleted during the next swap stage of the main loop (rendering of the object ceases immediately, but it still exists in memory for a while, so you can get it from its parent, for example). This method simplifies object deletion from a secondary thread, so you can call it and forget about the details, letting the Engine take control over the process of deletion, which can be used for future optimizations.
- [*deleteForce()*](../../../api/library/common/class.ptr_usc.md#deleteForce_void) - performs immediate deletion, which might be necessary in some cases. Calling this method for main-loop-dependent objects (e.g., nodes) is safe only when performed from the Main thread.


```cpp
// unigine_project.cpp

#include <core/unigine.h>

int init() {
	// create an instance of any class inherited from the Node class (e.g. ObjectMeshStatic)
	ObjectMeshStatic object_mesh = new ObjectMeshStatic("core/meshes/box.mesh");

	// do something with the node
	// ...

	// delete the node from the editor
	engine.editor.removeNode(object_mesh);

	return 1;
}

```


## Node Class

### Members

## GeodeticPivot getGeodeticPivot () const

Returns the current pointer to geodetic pivot of the node.
### Return value

Current geodetic pivot, or NULL if the node is not a child of a geodetic pivot node.
## void setVariable ( )

Sets a new value of the single unnamed variable parameter of the node. If this variable does not exist it will be created with a specified value (on requesting the non-existent value 0 will be returned).
### Arguments

- **variable** - The variable value.

## getVariable () const

Returns the current value of the single unnamed variable parameter of the node. If this variable does not exist it will be created with a specified value (on requesting the non-existent value 0 will be returned).
### Return value

Current variable value.
## void setWorldScale ( vec3 scale )

Sets a new node scale in the world space.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


### Arguments

- *vec3* **scale** - The node scale in the world space.

## vec3 getWorldScale () const

Returns the current node scale in the world space.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


### Return value

Current node scale in the world space.
## void setWorldPosition ( Vec3 position )

Sets a new node position in the world coordinates.
### Arguments

- *Vec3* **position** - The node position in the world coordinates.

## Vec3 getWorldPosition () const

Returns the current node position in the world coordinates.
### Return value

Current node position in the world coordinates.
## void setScale ( vec3 scale )

Sets a new scale of the node.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


### Arguments

- *vec3* **scale** - The node scale in the local space.

## vec3 getScale () const

Returns the current scale of the node.
> **Notice:** **Scaling of nodes should be avoided whenever possible** as it requires addidional calculations and may lead to error accumulation.


### Return value

Current node scale in the local space.
## void setPosition ( Vec3 position )

Sets a new node position.
### Arguments

- *Vec3* **position** - The node position in the local space.

## Vec3 getPosition () const

Returns the current node position.
### Return value

Current node position in the local space.
## vec3 getBodyAngularVelocity () const

Returns the current angular velocity of the node's physical body in the world space.
### Return value

Current angular velocity of the node's physical body in the world space.
## vec3 getBodyLinearVelocity () const

Returns the current linear velocity of the node's physical body in the local space.
### Return value

Current linear velocity of the node's physical body in the local space.
## BodyRigid getObjectBodyRigid () const

Returns the current [rigid body](../../../principles/physics/bodies/rigid/index.md) assigned to the node if it is an object node.
### Return value

Current [rigid body](../../../principles/physics/bodies/rigid/index.md) assigned to the node if it is an object node; otherwise, NULL (0).
## Body getObjectBody () const

Returns the current physical body assigned to the node if it is an object node.
### Return value

Current physical body assigned to the node if it is an object node; otherwise, NULL (0).
## WorldBoundSphere getWorldBoundSphere () const

Returns the current bounding sphere of the node in world's coordinate system.
### Return value

Current bounding sphere of the node in world's coordinate system.
## WorldBoundBox getWorldBoundBox () const

Returns the current bounding box of the node in world's coordinate system.
### Return value

Current [world bounding box](../../../api/library/math/bounds/class.worldboundbox_usc.md).
## BoundSphere getBoundSphere () const

Returns the current
### Return value

Current [bounding sphere](../../../api/library/math/bounds/class.boundsphere_usc.md) of the node.
## BoundBox getBoundBox () const

Returns the current
### Return value

Current [bounding box](../../../api/library/math/bounds/class.boundbox_usc.md) of the node.
## void setOldWorldTransform ( Mat4 transform )

Sets a new old (previous frame) transformation matrix for the node in the world coordinates.
### Arguments

- *Mat4* **transform** - The old (previous frame) transformation matrix for the node in the world coordinates.

## Mat4 getOldWorldTransform () const

Returns the current old (previous frame) transformation matrix for the node in the world coordinates.
### Return value

Current old (previous frame) transformation matrix for the node in the world coordinates.
## void setWorldTransform ( Mat4 transform )

Sets a new transformation matrix of the node in the world coordinates.
### Arguments

- *Mat4* **transform** - The transformation matrix of the node in the world coordinates.

## Mat4 getWorldTransform () const

Returns the current transformation matrix of the node in the world coordinates.
### Return value

Current transformation matrix of the node in the world coordinates.
## void setTransform ( Mat4 transform )

Sets a new transformation matrix of the node in its parent coordinates.
### Arguments

- *Mat4* **transform** - The transformation matrix of the node in local coordinates.

## Mat4 getTransform () const

Returns the current transformation matrix of the node in its parent coordinates.
### Return value

Current transformation matrix of the node in local coordinates.
## int getNumProperties () const

Returns the current total number of properties associated with the node.
### Return value

Current total number of properties associated with the node.
## Node getPossessor () const

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
## Node getRootNode () const

Returns the current root node for the node. This method searches for the root node among all node's parents and [possessors](#getPossessor_Node) up the hierarchy. If a node does not have a parent or possessor the node itself will be returned.
### Return value

Current root node for the node.
## void setParent ( Node parent )

Sets a new parent of the node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **parent** - The parent of the node or **NULL** (**0**), if the node has no parent.

## Node getParent () const

Returns the current parent of the node.
### Return value

Current parent of the node or **NULL** (**0**), if the node has no parent.
## int getNumAncestors () const

Returns the current number of ancestors of the node.
### Return value

Current number of ancestors of the node.
## void setName ( string name )

Sets a new name of the node.
### Arguments

- *string* **name** - The name of the node.

## const char * getName () const

Returns the current name of the node.
### Return value

Current name of the node.
## void setQuery ( )

Sets a new value indicating if occlusion query is used for the node. The default is false (not used).
### Arguments

- **query** - The occlusion query is used for the node

## isQuery () const

Returns the current value indicating if occlusion query is used for the node. The default is false (not used).
### Return value

Current occlusion query is used for the node
## void setClutterInteractionEnabled ( bool enabled )

Sets a new value indicating if interaction with [World Clutters](../../../api/library/worlds/class.worldclutter_usc.md) and [Mesh Clutters](../../../api/library/objects/class.objectmeshclutter_usc.md) is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of clutters is not necessary. Especially when the world contains a significant number of such nodes.


### Arguments

- *bool* **enabled** - Set **true** to enable interaction with [World Clutters](../../../api/library/worlds/class.worldclutter_usc.md) and [Mesh Clutters](../../../api/library/objects/class.objectmeshclutter_usc.md); **false** - to disable it.

## bool isClutterInteractionEnabled () const

Returns the current value indicating if interaction with [World Clutters](../../../api/library/worlds/class.worldclutter_usc.md) and [Mesh Clutters](../../../api/library/objects/class.objectmeshclutter_usc.md) is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of clutters is not necessary. Especially when the world contains a significant number of such nodes.


### Return value

**true** if interaction with [World Clutters](../../../api/library/worlds/class.worldclutter_usc.md) and [Mesh Clutters](../../../api/library/objects/class.objectmeshclutter_usc.md) is enabled ; otherwise **false**.
## void setGrassInteractionEnabled ( bool enabled )

Sets a new value indicating if interaction with [Grass](../../../api/library/objects/class.objectgrass_usc.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of grass is not necessary. Especially when the world contains a significant number of such nodes.


### Arguments

- *bool* **enabled** - Set **true** to enable interaction with [Grass](../../../api/library/objects/class.objectgrass_usc.md) nodes; **false** - to disable it.

## bool isGrassInteractionEnabled () const

Returns the current value indicating if interaction with [Grass](../../../api/library/objects/class.objectgrass_usc.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when cutting node out of grass is not necessary. Especially when the world contains a significant number of such nodes.


### Return value

**true** if interaction with [Grass](../../../api/library/objects/class.objectgrass_usc.md) nodes is enabled ; otherwise **false**.
## void setTriggerInteractionEnabled ( bool enabled )

Sets a new value indicating if interaction with [WorldTrigger](../../../api/library/worlds/class.worldtrigger_usc.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when node interaction with [World Triggers](../../../api/library/worlds/class.worldtrigger_usc.md) is not necessary. Especially when the world contains a significant number of such nodes.


### Arguments

- *bool* **enabled** - Set **true** to enable interaction with [World Triggers](../../../api/library/worlds/class.worldtrigger_usc.md); **false** - to disable it.

## bool isTriggerInteractionEnabled () const

Returns the current value indicating if interaction with [WorldTrigger](../../../api/library/worlds/class.worldtrigger_usc.md) nodes is enabled for the node.
> **Notice:** It is recommended to disable this option for better performance, when node interaction with [World Triggers](../../../api/library/worlds/class.worldtrigger_usc.md) is not necessary. Especially when the world contains a significant number of such nodes.


### Return value

**true** if interaction with [World Triggers](../../../api/library/worlds/class.worldtrigger_usc.md) is enabled ; otherwise **false**.
## void setImmovable ( )

Sets a new value indicating if the node is an immovable (clutter) object, which means it is moved to a separate spatial tree for immovable (static) objects optimizing node management. There are several restrictions on nodes considered immovable. Any action affecting the spatial tree is prohibited and causes a warning: you cannot change the node state (enabled/disabled), surfaces, bounds, trasformation, visibility distance, as well as move the node, assign a non-dummy physical body or even disable the *Immovable* flag as it also leads to rebiulding of the spatial tree.
> **Notice:** You can disable these warnings by using the [*World::setMovingImmovableNodeMode()*](../../../api/library/engine/class.world_usc.md#setMovingImmovableNodeMode_int_void) method, if necessary.


### Arguments

- **immovable** - The the feature of the clutter (immovable) object for the node

## isImmovable () const

Returns the current value indicating if the node is an immovable (clutter) object, which means it is moved to a separate spatial tree for immovable (static) objects optimizing node management. There are several restrictions on nodes considered immovable. Any action affecting the spatial tree is prohibited and causes a warning: you cannot change the node state (enabled/disabled), surfaces, bounds, trasformation, visibility distance, as well as move the node, assign a non-dummy physical body or even disable the *Immovable* flag as it also leads to rebiulding of the spatial tree.
> **Notice:** You can disable these warnings by using the [*World::setMovingImmovableNodeMode()*](../../../api/library/engine/class.world_usc.md#setMovingImmovableNodeMode_int_void) method, if necessary.


### Return value

Current the feature of the clutter (immovable) object for the node
## void setHandled ( bool handled )

Sets a new value indicating if the node handle is displayed. This option is valid only for invisible nodes, such as light and sound sources, particle systems and world-managing nodes ( [WorldOccluder](../../../api/library/worlds/class.worldoccluder_usc.md), triggers, expressions, etc.)
### Arguments

- *bool* **handled** - Set **true** to enable displaying of the node handle; **false** - to disable it.

## bool isHandled () const

Returns the current value indicating if the node handle is displayed. This option is valid only for invisible nodes, such as light and sound sources, particle systems and world-managing nodes ( [WorldOccluder](../../../api/library/worlds/class.worldoccluder_usc.md), triggers, expressions, etc.)
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
## getType () const

Returns the current type of the node.
### Return value

Current node type identifier.
## void setID ( int id )

Sets a new runtime ID of the node. It may differ from the file ID, which is obtained via .
> **Notice:** See also *[*engine.world.getNodeByID()*](../../../api/library/engine/class.world_usc.md#getNodeByID_int_Node)* function.


### Arguments

- *int* **id** - The runtime ID of the node.

## int getID () const

Returns the current runtime ID of the node. It may differ from the file ID, which is obtained via .
> **Notice:** See also *[*engine.world.getNodeByID()*](../../../api/library/engine/class.world_usc.md#getNodeByID_int_Node)* function.


### Return value

Current runtime ID of the node.
## int getIDFromFile () const

Returns the current ID of the node loaded from `*.node` or `*.world` file. It may differ from the runtime ID of the node, which is obtained via .
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
## WorldBoundSphere getSpatialBoundSphere () const

Returns the current bounding sphere with world coordinates that participates in physics calculations, but doesn't take children into account. this bounding sphere is used by the spatial tree.
### Return value

Current bounding sphere with world coordinates.
## WorldBoundBox getSpatialBoundBox () const

Returns the current bounding box with world coordinates that participates in physics calculations, but doesn't take children into account. this bounding box is used by the spatial tree.
### Return value

Current bounding box with world coordinates.
## bool isLandscapeLayer () const

Returns the current
### Return value

**true** if the node is a landscape layer is enabled ; otherwise **false**.
## Mat4 getIWorldTransform () const

Returns the current inverse transformation matrix of the node for transformations in the world coordinates.
### Return value

Current inverse transformation matrix.
## Vec3 getOldWorldPosition () const

Returns the current old (previous frame) position of the node in the world coordinates.
### Return value

Current old (previous frame) position of the node in the world coordinates.
## void setLifetime ( )

Sets a new lifetime management type for the root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)) of the node, or for the node itself (if it is not a child and not possessed by any other node).
> **Notice:** Lifetime of each node in the hierarchy is defined by it's root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)). Thus, lifetime management type set for a child node that differs from the one set for the root is ignored.


### Arguments

- **lifetime** - The

## getLifetime () const

Returns the current lifetime management type for the root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)) of the node, or for the node itself (if it is not a child and not possessed by any other node).
> **Notice:** Lifetime of each node in the hierarchy is defined by it's root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)). Thus, lifetime management type set for a child node that differs from the one set for the root is ignored.


### Return value

Current
## getEventTransformChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPropertyNodeSlotsChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPropertyNodeAdd () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPropertyNodeRemove () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPropertyChangeEnabled () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPropertyNodeSwap () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPropertySurfaceAdd () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPropertySurfaceRemove () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventCacheNodeAdd () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventNodeLoad () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventNodeRemove () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventNodeChangeEnabled () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventNodeClone () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventNodeSwap () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

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

## Node getAncestor ( int num )

Returns a node ancestor by its number.
### Arguments

- *int* **num** - Ancestor ID.

### Return value

Ancestor node.
## Node getChild ( int num )

Returns a node child by its number.
### Arguments

- *int* **num** - Child ID.

### Return value

Child node.
## int isChild ( Node n )

Checks if a given node is a child of the node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **n** - Node to check.

### Return value

**1** if the given node is a child; otherwise, **0**.
## void setChildIndex ( Node n , int index )

Sets the index for a given child node of the node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **n** - Child node.
- *int* **index** - Node index.

## int getChildIndex ( Node n )

Returns the index of a given child node of the node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **n** - Child node.

### Return value

Node index.
## void setData ( string name , string data )

Updates user data associated with the node.
- If the node was loaded from the `*.node` file, data is saved directly into the *data* tag of this file.
- If the node is loaded from the `*.world` file, data is saved into the Node *data* tag of the `*.world` file.
- If the node is loaded from the `*.world` file as a NodeReference, data will be saved to the NodeReference *data* tag of the `*.world` file.


### Arguments

- *string* **name** - String containing a key identifying user data to be stored in the `*.node` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.
- *string* **data** - New user data. Data can contain an XML formatted string.

## string getData ( string name )

Returns user string data associated with the node.
- If the node was loaded from the `*.node` file, data from the *data* tag of this file is returned.
- If the node is loaded from the `*.world` file, data from the Node *data* tag of the `*.world` file is returned.
- If the node is loaded from the `*.world` file as a NodeReference, data from the NodeReference *data* tag of the `*.world` file is returned.


> **Notice:** You can also use [*setVariable()*](#setVariable_Variable_void) to associate an arbitrary user variable with a node.


### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.node` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

### Return value

User string data. Data can contain an XML formatted string.
## void updateEnabled ( )

Updates node's internal state according to the current "*enabled*" state.
## int isEnabledSelf ( )

Returns a value indicating if the node is enabled.
### Return value

**1** if the node is enabled; otherwise, **0**.
## void getHierarchy ( )

Retrieves the whole hierarchy of the node and puts it to the hierarchy buffer.
### Arguments

## bool setProperty ( int num )

Updates the node property with the specified number. A new internal property inherited from the one with the specified name will be set. Such internal properties are saved in a `*.world` or `*.node` file.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

true if the specified node property is updated successfully; otherwise, false.
## void setPropertyEnabled ( int num , int enable )

Enables or disables the node property with the specified number.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *int* **enable** - **1** to enable the specified node property, **0** to disable it.

## int isPropertyEnabled ( int num )

Returns a value indicating if the node property with the specified number is enabled.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

**1** if the specified property is enabled; otherwise, **0**.
## void swapProperty ( int from_num , int to_num )

Swaps two properties with specified numbers in the list of properties associated with the node.
> **Notice:** The order of properties in the list determines the execution sequence of logic of corresponding [components](../../../principles/component_system/index.md) (if any).


### Arguments

- *int* **from_num** - Number of the first node property to be swapped, in the range from 0 to the [total number of node properties](#getNumProperties_int).
- *int* **to_num** - Number of the second node property to be swapped, in the range from 0 to the [total number of node properties](#getNumProperties_int).

## void clearProperties ( )

Clears the list of properties associated with the node.
## Property getProperty ( int num )

Returns a node property with the specified number if it exists.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

Node property.
## string getPropertyName ( int num )

Returns the name of a node property with the specified number.
### Arguments

- *int* **num** - Node property number in the range from 0 to the [total number of node properties](#getNumProperties_int).

### Return value

Property name, if exists; otherwise, NULL.
## int hasQueryForce ( )

Returns a value indicating if the *[Culled By Occlusion Query](../../../editor2/node_parameters/transformation_common/index.md#query)*option is force-enabled for the node by the Engine.
### Return value

**1** if the *[Culled By Occlusion Query](../../../editor2/node_parameters/transformation_common/index.md#query)*option is force-enabled for the node by the Engine; otherwise, **0**.
## void setRotation ( quat rot , int identity = 0 )

Sets the node rotation.
### Arguments

- *quat* **rot** - Quaternion representing node rotation in the local space.
- *int* **identity** - Flag indicating if node's scale is to be ignored or taken into account: > **Notice:** - It is recommended to set this flag for all non-scaled nodes to improve performance and accuracy. > - **Scaling of nodes should be avoided whenever possible**, as it requires addidional calculations and may lead to error accumulation.

  - 0 - node's scale is taken into account. In this case additional calculations are performed to extract current node's scale and apply it when building the final transformation matrix. These additional operations reduce performance and may lead to error accumulation.
  - 1 - node's scale is ignored (assumed to be equal to **1** along all axes). Thus, the number of calculations performed for each rotation is reduced and error accumulation is minimal.

## quat getRotation ( )

Returns the node rotation.
### Return value

Quaternion representing node rotation in the local space.
## void setWorldRotation ( quat rot , int identity = 0 )

Sets the node rotation in the world space.
### Arguments

- *quat* **rot** - Node rotation in the world space.
- *int* **identity** - Flag indicating if node's scale is to be ignored or taken into account: > **Notice:** - It is recommended to set this flag for all non-scaled nodes to improve performance and accuracy. > - **Scaling of nodes should be avoided whenever possible**, as it requires addidional calculations and may lead to error accumulation.

  - 0 - node's scale is taken into account. In this case additional calculations are performed to extract current node's scale and apply it when building the final transformation matrix. These additional operations reduce performance and may lead to error accumulation.
  - 1 - node's scale is ignored (assumed to be equal to **1** along all axes). Thus, the number of calculations performed for each rotation is reduced and error accumulation is minimal.

## quat getWorldRotation ( )

Returns the node rotation in the world space.
### Return value

Node rotation in the world space.
## void setTransformWithoutChildren ( Mat4 transform )

Sets the transformation matrix for the node in local coordinates (transformations of all node's children are not affected). This method can be used to change node's transformation relative to its children.
### Arguments

- *Mat4* **transform** - New transformation matrix to be set for the node (local coordinates).

## int getTypeID ( string type )

Returns the ID of a node type with a given name.
### Arguments

- *string* **type** - Node type name.

### Return value

Node type ID, if such type exists; otherwise, -1.
## string getTypeName ( int type )

Returns the name of a node type with a given ID.
### Arguments

- *int* **type** - Node type ID.

### Return value

Node type name.
## void setVariable ( string name , Variable v )

Sets the value of a variable with a given name. If such variable does not exist it will be added with a specified value.
```cpp
NodeDummy container = new NodeDummy();
if(container.hasVariable("key1") == 0) {
	container.setVariable("key1",42);
}
int value = container.getVariable("key1");
container.removeVariable("key1");

```


### Arguments

- *string* **name** - Variable name.
- *Variable* **v** - Variable value.

## Variable getVariable ( string name )

Returns the variable with a given name.
```cpp
NodeDummy container = new NodeDummy();
if(container.hasVariable("key1") == 0) {
	container.setVariable("key1",42);
}
int value = container.getVariable("key1");
container.removeVariable("key1");

```


### Arguments

- *string* **name** - Variable name.

### Return value

Variable if it exists; otherwise, variable with 0 value.
## void setWorldParent ( Node n )

Sets the new parent of the node. Transformations of the current node will be done in the world coordinates.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **n** - New parent node or NULL (0).

## void setWorldTransformWithoutChildren ( Mat4 transform )

Sets the transformation matrix for the node in world coordinates (transformations of all node's children are not affected). This method can be used to change node's transformation relative to its children.
### Arguments

- *Mat4* **transform** - New transformation matrix to be set for the node (world coordinates).

## vec3 getBodyWorldVelocity ( Vec3 point )

Returns linear velocity of a point of the node's physical body in the world space.
### Arguments

- *Vec3* **point** - Target point.

### Return value

Linear velocity in the world space.
## void addChild ( Node n )

Adds a child to the node. Transformations of the new child will be done in the coordinates of the parent.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **n** - New child node.

## void addWorldChild ( Node n )

Adds a child to the node. Transformations of the new child will be done in the world coordinates.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **n** - New child node.

## Node clone ( )

Clones the node.
### Return value

Copy of the node or **NULL** (**0**), if an error occurred.
## int findChild ( string name )

Searches for a child node with a given name among the children of the node.
### Arguments

- *string* **name** - Name of the child node.

### Return value

Child node number, if it is found; otherwise, -1.
## Node findNode ( string name , int recursive = 0 )

Searches for a node with a given name among the children of the node.
### Arguments

- *string* **name** - Name of the child node to search for.
- *int* **recursive** - **1** if the search is recursive (i.e. performed for children of child nodes); otherwise, **0**.

### Return value

Child node, if it is found; otherwise, NULL.
## void findNodes ( string name , Vector< Node >& OUT_nodes , int recursive = 0 )

Searches for a node with a given name among the children of the node and puts them to the specified output *nodes* buffer.
### Arguments

- *string* **name** - Name of the node to search for.
- *Vector<[Node](../../../api/library/nodes/class.node_usc.md)>&* **OUT_nodes** - Output buffer to which all found nodes with the specified name will be put. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **recursive** - **1** if the search is recursive (i.e. performed for children of child nodes); otherwise, **0**.

## int hasVariable ( string name )

Returns a value indicating if the node has a variable parameter with a given name.
```cpp
NodeDummy container = new NodeDummy();
if(container.hasVariable("key1") == 0) {
	container.setVariable("key1",42);
}
int value = container.getVariable("key1");
container.removeVariable("key1");

```


### Arguments

- *string* **name** - Variable name.

### Return value

**1** if the node has a variable parameter with a given name; otherwise, **0**.
## int hasVariable ( )

Returns a value indicating if the node has a single unnamed variable parameter.
### Return value

1 if the node has a single unnamed variable parameter; otherwise, 0.
## int loadWorld ( Xml xml )

Loads a node state from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml smart pointer.

### Return value

**1** if the node state is loaded successfully; otherwise, **0**.
## void removeChild ( Node n )

Removes a child node (added by the *[addChild()](#addChild_Node_void)* method) from the list of children.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **n** - Child node to remove.

## int removeVariable ( string name )

Removes a variable parameter with a given name.
```cpp
NodeDummy container = new NodeDummy();
if(container.hasVariable("key1") == 0) {
	container.setVariable("key1",42);
}
int value = container.getVariable("key1");
container.removeVariable("key1");

```


### Arguments

- *string* **name** - Variable parameter name.

### Return value

1 if the variable parameter is removed successfully; otherwise, 0.
## void removeWorldChild ( Node n )

Removes a child node (added by the *[addWorldChild()](#addWorldChild_Node_void)* method) from the list of children.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **n** - Child node to remove.

## void renderVisualizer ( )

Renders a bounding box / sphere of the object.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


## int saveState ( Stream stream )

Saves the state of a given node into a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be saved manually.
- To save the state from a [buffer](../../../api/library/common/class.blob_usc.md), [file](../../../api/library/filesystem/class.file_usc.md) or a message from a [socket](../../../api/library/networking/class.socket_usc.md), make sure the stream is [opened](../../../api/library/common/class.stream_usc.md#isOpened_int). For buffers and files, you also need to set the proper position for reading.


**Example** using saveState() and [restoreState()](#restoreState_Stream_int) methods:


```cpp
// initialize a node and set its state
NodeDummy node = new NodeDummy();
node.setPosition(vec3(1, 1, 0));

// save state
Blob blob_state = new Blob();
node.saveState(blob_state);

// change state
node.setPosition(vec3(0, 0, 0));

// restore state
blob_state.seekSet(0);	   // returning the carriage to the start of the blob
node.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to save node state data.

### Return value

**1** if node state is successfully saved; otherwise, **0**.
## int restoreState ( Stream stream )

Restores the state of a given node from a binary stream.
- If a node is a parent for other nodes, states of these child nodes need to be restored manually.
- To save the state into a [buffer](../../../api/library/common/class.blob_usc.md), [file](../../../api/library/filesystem/class.file_usc.md) or a message from a [socket](../../../api/library/networking/class.socket_usc.md), make sure the stream is [opened](../../../api/library/common/class.stream_usc.md#isOpened_int). If necessary, you can set a position for writing for buffers and files.


**Example** using [saveState()](#saveState_Stream_int) and restoreState() methods:


```cpp
// initialize a node and set its state
NodeDummy node = new NodeDummy();
node.setPosition(vec3(1, 1, 0));

// save state
Blob blob_state = new Blob();
node.saveState(blob_state);

// change state
node.setPosition(vec3(0, 0, 0));

// restore state
blob_state.seekSet(0);	   // returning the carriage to the start of the blob
node.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream with saved node state data.

### Return value

**1** if node state is successfully restored; otherwise, **0**.
## int saveWorld ( Xml xml )

Saves the node into the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Xml smart pointer.

### Return value

**1** if the node is successfully saved; otherwise, **0**.
## void swap ( Node n )

Swaps the nodes saving the pointers.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **n** - Node to swap.

## vec3 toLocal ( Vec3 p )

Converts a given vector in the world space to the node's local space.
### Arguments

- *Vec3* **p** - Vector in the world space.

### Return value

Vector in the local space.
## Vec3 toWorld ( vec3 p )

Converts a given vector in the local space to the world space.
### Arguments

- *vec3* **p** - Vector in the local space.

### Return value

Vector in the world space.
## void translate ( Vec3 t )

Translates the node relative to its local coordinate system: the parent node transformation isn't taken into account.
### Arguments

- *Vec3* **t** - Translation vector.

## void translate ( scalar x , scalar y , scalar z )

Translates the node relative to its local coordinate system: the parent node transformation isn't taken into account.
### Arguments

- *scalar* **x** - Node translation along the X axis, in units.
- *scalar* **y** - Node translation along the Y axis, in units.
- *scalar* **z** - Node translation along the Z axis, in units.

## void worldTranslate ( Vec3 t )

Translates the node in the world space using the specified vector.
### Arguments

- *Vec3* **t** - Translation vector.

## void worldTranslate ( scalar x , scalar y , scalar z )

Translates the node in the world space using the values specified for the corresponding axes.
### Arguments

- *scalar* **x** - Node translation along the X axis, in units.
- *scalar* **y** - Node translation along the Y axis, in units.
- *scalar* **z** - Node translation along the Z axis, in units.

## void worldLookAt ( )

Reorients the node to "look" at the target point and sets the given up vector:
- If the node is a [Player-related](#isPlayer_int) one, it will "look" at the target point along the negative Z axis. The Y axis will be oriented along the specified up vector.
- Other nodes will "look" at the target point along the Y axis. The Z axis will be oriented along the specified up vector.


### Arguments

## void worldLookAt ( )

Reorients the node to "look" at the target point. The up vector is oriented along the Z axis.
- If the node is a [Player-related](#isPlayer_int) one, it will "look" at the target point along the negative Z axis. The Y axis will be oriented along the world Z axis.
- Other nodes will "look" at the target point along the Y axis.


### Arguments

## void rotate ( quat r )

Rotates the node relative to its local coordinate system: the parent node transformation isn't taken into account. Rotation is determined by the specified [quaternion](../../../api/library/math/class.quat_usc.md).
### Arguments

- *quat* **r** - Rotation quaternion.

## void rotate ( float angle_x , float angle_y , float angle_z )

Rotates the node in the world space according to specified Euler angles.
### Arguments

- *float* **angle_x** - Pitch angle, in degrees.
- *float* **angle_y** - Roll angle, in degrees.
- *float* **angle_z** - Yaw angle, in degrees.

## void worldRotate ( quat r )

Rotates the node in the world space. Rotation is determined by the specified [quaternion](../../../api/library/math/class.quat_usc.md).
### Arguments

- *quat* **r** - Rotation quaternion.

## void worldRotate ( float angle_x , float angle_y , float angle_z )

Rotates the node in the world space according to specified Euler angles.
### Arguments

- *float* **angle_x** - Pitch angle, in degrees.
- *float* **angle_y** - Roll angle, in degrees.
- *float* **angle_z** - Yaw angle, in degrees.

## void setDirection ( )

Updates the direction vector of the node and reorients this node: the specified axis of the node becomes oriented along the specified vector in local coordinates. For example, after running the code below, you will get the X axis of the node pointed along the Y axis in local coordinates.
```cpp
// get the node
Node node = engine.world.getNodeByName("material_ball");
// set the X axis to be pointed along the Y axis in local coordinates
node.setDirection(vec3(0.0f,1.0f,0.0f),vec3(0.0f,0.0f,1.0f),AXIS_X);

```


### Arguments

## getDirection ( )

Returns the normalized direction vector pointing along the given node axis in local coordinates (i.e. relative to the node's parent). By default, the direction vector pointing along the negative Z axis of the node (in local coordinates) is returned. The direction vector always has a unit length.
```cpp
node.getDirection(node.isPlayer() ? AXIS_NZ : AXIS_Y); // forward direction vector
node.getDirection(node.isPlayer() ? AXIS_Z : AXIS_NY); // backward direction vector
node.getDirection(node.isPlayer() ? AXIS_Y : AXIS_Z); // upward direction vector
node.getDirection(node.isPlayer() ? AXIS_NY : AXIS_NZ); // down direction vector
node.getDirection(AXIS_X); // right direction vector
node.getDirection(AXIS_NX); // left direction vector

```


### Arguments

### Return value

Direction vector in local coordinates.
## void setWorldDirection ( )

Updates the direction vector of the node and reorients this node: the specified axis of the node becomes oriented along the specified vector in world coordinates. For example, after running the code below, you will get the X axis of the node pointed along the Y axis in world coordinates:
```cpp
// get the node
Node node = engine.world.getNodeByName("material_ball");
// set the X axis to be pointed along the Y axis in world coordinates
node.setWorldDirection(vec3(0.0f,1.0f,0.0f),vec3(0.0f,0.0f,1.0f),AXIS_X);

```


### Arguments

## getWorldDirection ( )

Returns the normalized direction vector pointing along the given node axis in world coordinates. By default, the direction vector pointing along the negative Z axis of the node is returned. The direction vector always has a unit length.
```cpp
node.getWorldDirection(node.isPlayer() ? AXIS_NZ : AXIS_Y); // forward direction vector
node.getWorldDirection(node.isPlayer() ? AXIS_Z : AXIS_NY); // backward direction vector
node.getWorldDirection(node.isPlayer() ? AXIS_Y : AXIS_Z); // upward direction vector
node.getWorldDirection(node.isPlayer() ? AXIS_NY : AXIS_NZ); // down direction vector
node.getWorldDirection(AXIS_X); // right direction vector
node.getWorldDirection(AXIS_NX); // left direction vector

```


### Arguments

### Return value

Direction vector in world coordinates.
## Node getCloneNode ( Node original_node )

Returns a node cloned from the specified original node.
> **Notice:** This method is intended for use only inside the [node clone callback](#getEventNodeClone_Event).


### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **original_node** - Original node that was cloned.

### Return value

Clone of the specified original node if it exists; otherwise the original node itself.
## Property getCloneProperty ( Property original_property )

Returns a node property cloned from the specified original property.
> **Notice:** This method is intended for use only inside the [node clone callback](#getEventNodeClone_Event).


### Arguments

- *[Property](../../../api/library/common/class.property_usc.md)* **original_property** - Original node property that was cloned.

### Return value

Clone of the specified original node property if it exists; otherwise the original node property itself.
## void setSaveToWorldEnabledRecursive ( int enable )

Sets a value indicating if saving to `*.world` file is enabled for the node and all its children (if any).
### Arguments

- *int* **enable** - **1** to enable saving to `*.world` file for the node and all its children (if any); 0 to disable.

## void setShowInEditorEnabledRecursive ( int enable )

Sets a value indicating if displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) is enabled for the node and all its children (if any).
### Arguments

- *int* **enable** - **1** to enable displaying in the *World Hierarchy* window of the [UnigineEditor](../../../editor2/index.md) for the node and all its children (if any); 0 to disable.

## int getLifetimeSelf ( )

Returns the lifetime management type set for the node itself.
> **Notice:** Lifetime of each node in the hierarchy is defined by it's root (either [parent](#getParent_Node) or [possessor](#getPossessor_Node)). Setting lifetime management type for a child node different from the one set for the root has no effect.


### Return value

One of the [*NODE_LIFETIME_**](#LIFETIME_WORLD) values.
## WorldBoundBox getHierarchyBoundBox ( int only_enabled_nodes = false )

Returns a bounding box with local coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding box recalculation when transforming nodes.
### Arguments

- *int* **only_enabled_nodes** - Set **1** to obtain the result taking into account only the nodes in the hierarchy that are enabled, or **0** - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding box with world coordinates.
## WorldBoundSphere getHierarchyBoundSphere ( int only_enabled_nodes = false )

Returns a bounding sphere with local coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding sphere recalculation when transforming nodes.
### Arguments

- *int* **only_enabled_nodes** - Set **1** to obtain the result taking into account only the nodes in the hierarchy that are enabled, or **0** - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding sphere with world coordinates.
## WorldBoundBox getHierarchyWorldBoundBox ( int only_enabled_nodes = false )

Returns a bounding box with world coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding box recalculation when transforming nodes.
### Arguments

- *int* **only_enabled_nodes** - Set **1** to obtain the result taking into account only the nodes in the hierarchy that are enabled, or **0** - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding box with world coordinates.
## WorldBoundSphere getHierarchyWorldBoundSphere ( int only_enabled_nodes = false )

Returns a bounding sphere with world coordinates that takes children into account, but doesn't participate in physics calculations. Exclusion of objects from the spatial tree significantly reduces the size of the tree and improves performance due to saving time on bounding sphere recalculation when transforming nodes.
### Arguments

- *int* **only_enabled_nodes** - Set **1** to obtain the result taking into account only the nodes in the hierarchy that are enabled, or **0** - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding sphere with world coordinates.
## WorldBoundBox getHierarchySpatialBoundBox ( int only_enabled_nodes = false )

Returns a bounding box with world coordinates that takes all children and physics into account. This bounding box is used by the spatial tree.
### Arguments

- *int* **only_enabled_nodes** - Set **1** to obtain the result taking into account only the nodes in the hierarchy that are enabled, or **0** - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding box with world coordinates.
## WorldBoundSphere getHierarchySpatialBoundSphere ( int only_enabled_nodes = false )

Returns a bounding sphere with world coordinates that takes all children and physics into account. This bounding sphere is used by the spatial tree.
### Arguments

- *int* **only_enabled_nodes** - Set **1** to obtain the result taking into account only the nodes in the hierarchy that are enabled, or **0** - to take into account all nodes in the hierarchy regardless of their *enabled* state.

### Return value

The bounding sphere with world coordinates.
## virtual void updateSpatialTree ( )

Updates node bounds in the [spatial tree](../../../principles/world_management/index.md#outdoor) in the current frame. This method can be used in case you use some custom logic affecting node bounds or position and need to have your changes to be taken into account in the current frame, as well as to process such changes for your custom nodes ( *[ObjectExtern](../../../api/library/objects/class.objectextern_usc.md), [NodeExtern](../../../api/library/nodes/class.nodeextern_usc.md)*) which are otherwise ignored. Calling this method enables you to apply changes for this node fast without complete tree recalculation. But you should be aware that node bounds fast-updated this way **might be inaccurate** (they can only be expanded, as shrinking will require tree recalculation). In case you need to have 100% accurate bounds in the current frame, call the *[World::updateSpatial()()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method. You can also simply tell the spatial tree to update node bounds in the next frame via the *[updateSpatialTreeDelayed()()](../../...md#updateSpatialTreeDelayed_void)* method.
## void updateSpatialTreeDelayed ( )

Mark node bounds in the spatial tree to be updated in the next frame (all bounds will be 100% accurate in this case unlike for the *[updateSpatialTree()()](../../...md#updateSpatialTree_void)* method). This method can be used in case you use some custom logic affecting node bounds or position, as well as to process such changes for your custom nodes ( *[ObjectExtern](../../../api/library/objects/class.objectextern_usc.md), [NodeExtern](../../../api/library/nodes/class.nodeextern_usc.md)*) which are otherwise ignored. The changes will only be applied in the next frame, in case you need to have your changes to be taken into account right in the current frame use the *[World::updateSpatial()()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method for 100% accurate bounds (slow), or the fast *[updateSpatialTree()()](../../...md#updateSpatialTree_void)* method which only expands node bounds if necessary.
## WorldTrigger getWorldTrigger ( int num )

Returns one of the World Triggers inside which the node is located at the moment by its number. For any node in the world, you can [check whether it is currently inside any World Trigger](#getNumWorldTriggers_int) and access any of such triggers by simply calling this method.
### Arguments

- *int* **num** - Number of the World Trigger in the list of World Triggers inside which the node is located at the moment.

### Return value

World Trigger with the specified number inside which the node is located at the moment.
## UGUID getLostNodePropertyGUID ( int num )

Returns the [GUID](../../../api/library/filesystem/class.uguid_usc.md) of a lost property assigned to the node. If for some reason a property assigned to the specified slot of the node is missing, this method can be used to get it's GUID.
### Arguments

- *int* **num** - Target property slot number.

### Return value

Lost property [GUID](../../../api/library/filesystem/class.uguid_usc.md).
## void renderBounds ( int render_node_bound = true , int render_instance_bound = false )

Renders the node bounds. The method is applied for checking the actual size of the CPU-rendered node bounds that may differ from the GPU-rendered mesh size, if the latter has been modified by the shader. For nodes that consist of multiple mesh instances (Clutter, Cluster) rendering of each individual mesh bound is also available.
### Arguments

- *int* **render_node_bound** - **1** to enable rendering of the node bounds, **0** to disable it.
- *int* **render_instance_bound** - **1** to enable bound rendering for each individual mesh instance (applicable for Clutter and Cluster nodes), **0** to disable it.

## int getIDFromFile ( )

Returns the node ID from the `*.node` or a `*.world` file if the node has been loaded from this file.
### Return value

Node ID from the `*.node` or a `*.world` file. For the node created via code, -1 is returned.
## void applyReplacePaths ( )

Restores the engine's ability to replace baked textures (lightmap, shadow map) inside Node References in runtime. This method is to be applied if hierarchy inside a Node Reference or a path to the baked texture has been modified thus causing rendering of an unsuitable lightmap or a shadow map.
## void getNodes ( Vector< Node >& OUT_nodes )

Takes a node collection, clears it, and then adds all existing nodes to it. This includes nodes from the world and other sources, such as cached nodes or nodes currently being loaded via AsyncQueue.
### Arguments

- *Vector<[Node](../../../api/library/nodes/class.node_usc.md)>&* **OUT_nodes** - Node сollection. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int hasData ( string name )

Checks if there is user data associated with the node.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.node` file.

### Return value

**1** if the given node has user data; otherwise, **0**.
## void removeData ( string name )

Removes user data associated with the node.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.node` file.
