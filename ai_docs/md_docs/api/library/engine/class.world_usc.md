# Unigine::World Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class provides functionality for the [world script](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic). It contains methods required for loading the world with all its nodes, managing a spatial tree and handling nodes collisions and intersections.


Loading of nodes on demand is managed via the [engine.async Class](../../../api/library/filesystem/class.asyncqueue_usc.md).


> **Notice:** C++ methods running editor script functions are described in the [Engine class](../../../api/library/engine/class.engine_usc.md) reference.


### See also


- [engine.async Class](../../../api/library/filesystem/class.asyncqueue_usc.md) to manage loading nodes and other resources on demand
- The [Intersections](../../../code/usage/intersections/index_usc.md) article demonstrating how to use intersection-related functions
- The UnigineScript API sample `<UnigineSDK>/data/samples/systems/selection_00`


## World Class

### Members

## void setUnpackNodeReferences ( int references )

Sets a new value indicating if automatic unpacking of [node references](../../../api/library/nodes/class.nodereference_usc.md) at run time is enabled.
This option can be used to simplify hierarchy management, as when it is enabled all nodes contained in node references will be present in the world hierarchy. When disabled you have to check the hierarchy of each node reference individually (e.g. to find the number of children or manage some of them). The content of *NodeReference* nodes is unpacked only at run time and does not affect your `*.world` and `*.node` files. So, you can use all advantages of node references when building worlds in the UnigineEditor and manage a clear and straightforward hierarchy at run time.


> **Notice:** - This option is available only via code, can be enabled in the [System Script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) and works for all worlds used in your project.
> - **Auto-unpacking is enabled** in C# projects by default.


### Arguments

- *int* **references** - The automatic unpacking of *Node Reference* nodes at run time

## int isUnpackNodeReferences () const

Returns the current value indicating if automatic unpacking of [node references](../../../api/library/nodes/class.nodereference_usc.md) at run time is enabled.
This option can be used to simplify hierarchy management, as when it is enabled all nodes contained in node references will be present in the world hierarchy. When disabled you have to check the hierarchy of each node reference individually (e.g. to find the number of children or manage some of them). The content of *NodeReference* nodes is unpacked only at run time and does not affect your `*.world` and `*.node` files. So, you can use all advantages of node references when building worlds in the UnigineEditor and manage a clear and straightforward hierarchy at run time.


> **Notice:** - This option is available only via code, can be enabled in the [System Script](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) and works for all worlds used in your project.
> - **Auto-unpacking is enabled** in C# projects by default.


### Return value

Current automatic unpacking of *Node Reference* nodes at run time
## void setAutoReloadNodeReferences ( int references )

Sets a new value indicating if automatic reloading of *Node Reference* nodes is enabled.
If enabled, all *[NodeReference](../../../api/library/nodes/class.nodereference_usc.md)* nodes will reload their `*.node` files, when the *[saveNode()](#saveNode_cstr_Node_int_int)* method is called.


> **Notice:** This option can be used if you modify and save reference nodes at runtime. Otherwise you'll have to manually update pointers for all *[NodeReferences](../../../api/library/nodes/class.nodereference_usc.md)* referring to the changed node.


### Arguments

- *int* **references** - The automatic reloading of *Node Reference* nodes

## int isAutoReloadNodeReferences () const

Returns the current value indicating if automatic reloading of *Node Reference* nodes is enabled.
If enabled, all *[NodeReference](../../../api/library/nodes/class.nodereference_usc.md)* nodes will reload their `*.node` files, when the *[saveNode()](#saveNode_cstr_Node_int_int)* method is called.


> **Notice:** This option can be used if you modify and save reference nodes at runtime. Otherwise you'll have to manually update pointers for all *[NodeReferences](../../../api/library/nodes/class.nodereference_usc.md)* referring to the changed node.


### Return value

Current automatic reloading of *Node Reference* nodes
## void setUpdateGridSize ( float size )

Sets a new size of the grid to be used for spatial tree update. The default value is an average one, and can be adjusted when necessary depending on the scene.
### Arguments

- *float* **size** - The grid size, in units. The default value is 1000 units.

## float getUpdateGridSize () const

Returns the current size of the grid to be used for spatial tree update. The default value is an average one, and can be adjusted when necessary depending on the scene.
### Return value

Current grid size, in units. The default value is 1000 units.
## void setDistance ( float distance )

Sets a new distance at which (and farther) nothing will be rendered or simulated.
### Arguments

- *float* **distance** - The distance at which (and farther) nothing will be rendered or simulated, in units.

## float getDistance () const

Returns the current distance at which (and farther) nothing will be rendered or simulated.
### Return value

Current distance at which (and farther) nothing will be rendered or simulated, in units.
## void setBudget ( float budget )

Sets a new value of the world generation budget for grass and clutter objects. New objects are not created when time is out of the budget.
### Arguments

- *float* **budget** - The budget value in seconds. The default value is 1/60.

## float getBudget () const

Returns the current value of the world generation budget for grass and clutter objects. New objects are not created when time is out of the budget.
### Return value

Current budget value in seconds. The default value is 1/60.
## int isLoaded () const

Returns the current value indicating if the current world is fully loaded.
### Return value

Current the world is fully loaded
## void setScriptName ( string name )

Sets a new name of the [world script](../../../principles/world_structure/index.md) `*.usc` file.
### Arguments

- *string* **name** - The name of the [world script](../../../principles/world_structure/index.md) `*.usc` file.

## const char * getScriptName () const

Returns the current name of the [world script](../../../principles/world_structure/index.md) `*.usc` file.
### Return value

Current name of the [world script](../../../principles/world_structure/index.md) `*.usc` file.
## void setPath ( string path )

Sets a new path to the [`*.world`-file](../../../principles/world_structure/index.md) where the world is stored.
### Arguments

- *string* **path** - The path to the [`*.world`-file](../../../principles/world_structure/index.md) where the world is stored.

## const char * getPath () const

Returns the current path to the [`*.world`-file](../../../principles/world_structure/index.md) where the world is stored.
### Return value

Current path to the [`*.world`-file](../../../principles/world_structure/index.md) where the world is stored.
## void setScriptExecute ( int execute )

Sets a new value indicating if the world script (`*.usc` file) associated with the world should be executed.
### Arguments

- *int* **execute** - The a logic script associated with the world is to be loaded with it

## int isScriptExecute () const

Returns the current value indicating if the world script (`*.usc` file) associated with the world should be executed.
### Return value

Current a logic script associated with the world is to be loaded with it
## void setPhysicsSettings ( string settings )

Sets a new name of the `*.physics` file containing default [physics settings](../../../editor2/settings/physics_global/index.md) used by the World.
### Arguments

- *string* **settings** - The name of the `*.physics` file containing default [physics settings](../../../editor2/settings/physics_global/index.md) used by the World.

## const char * getPhysicsSettings () const

Returns the current name of the `*.physics` file containing default [physics settings](../../../editor2/settings/physics_global/index.md) used by the World.
### Return value

Current name of the `*.physics` file containing default [physics settings](../../../editor2/settings/physics_global/index.md) used by the World.
## void setSoundSettings ( string settings )

Sets a new name of the `*.sound` file containing default [sound settings](../../../editor2/settings/sound_global/index.md) used by the World.
### Arguments

- *string* **settings** - The name of the `*.sound` file containing default [sound settings](../../../editor2/settings/sound_global/index.md) used by the World.

## const char * getSoundSettings () const

Returns the current name of the `*.sound` file containing default [sound settings](../../../editor2/settings/sound_global/index.md) used by the World.
### Return value

Current name of the `*.sound` file containing default [sound settings](../../../editor2/settings/sound_global/index.md) used by the World.
## void setRenderSettings ( string settings )

Sets a new name of the `*.render` file containing default [render settings](../../../editor2/settings/render_settings/index.md) used by the World.
### Arguments

- *string* **settings** - The name of the `*.render` file containing default [render settings](../../../editor2/settings/render_settings/index.md) used by the World.

## const char * getRenderSettings () const

Returns the current name of the `*.render` file containing default [render settings](../../../editor2/settings/render_settings/index.md) used by the World.
### Return value

Current name of the `*.render` file containing default [render settings](../../../editor2/settings/render_settings/index.md) used by the World.
## const char * getLoadWorldRequestPath () const

Returns the current path to the world to be loaded.
### Return value

Current path to the world to be loaded.
## int isLoadWorldRequested () const

Returns the current value indicating if another world is going to be loaded in the next frame.
### Return value

Current another world is going to be loaded in the next frame
## void setMovingImmovableNodeMode ( )

***Console*:**`world_moving_immovable_node_mode`Sets a new  mode of handling attempts to move nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag enabled.
> **Notice:** Please be aware that there are two cases when you may disable warnings and allow movement of *Immovable* nodes:
> - At run-time for procedural generation of levels. This may cause some freezing but won't affect performance much. Upon completion of the generation process you should enable warnings again.
> - On world initialization, this will change world loading time but won't affect overall performance.


### Arguments

- **mode** - The handling mode for attempts to move nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag enabled. One of the following values:

  - **0** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is prohibited.
  - **1** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is accompanied by a warning in the Console. (by default)
  - **2** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is allowed (no warnings displayed).

## getMovingImmovableNodeMode () const

***Console*:**`world_moving_immovable_node_mode`Returns the current  mode of handling attempts to move nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag enabled.
> **Notice:** Please be aware that there are two cases when you may disable warnings and allow movement of *Immovable* nodes:
> - At run-time for procedural generation of levels. This may cause some freezing but won't affect performance much. Upon completion of the generation process you should enable warnings again.
> - On world initialization, this will change world loading time but won't affect overall performance.


### Return value

Current handling mode for attempts to move nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag enabled. One of the following values:
- **0** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is prohibited.
- **1** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is accompanied by a warning in the Console. (by default)
- **2** - movement of nodes having the *[Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter)* flag is allowed (no warnings displayed).

## void setExperimentalNavigationSettings ( string settings )

Sets a new path to the file holding the navigation settings of the world � the registry of areas and flags that the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_usc.md) singleton exposes. Keeping it in a file lets several worlds share one set of area definitions instead of each carrying its own copy.
### Arguments

- *string* **settings** - The path to the navigation settings file.

## String getExperimentalNavigationSettings () const

Returns the current path to the file holding the navigation settings of the world � the registry of areas and flags that the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_usc.md) singleton exposes. Keeping it in a file lets several worlds share one set of area definitions instead of each carrying its own copy.
### Return value

Current path to the navigation settings file.
## void setAsyncLoadNodeReferences ( bool references )

Sets a new value indicating if asynchronous loading of Node References is enabled.
### Arguments

- *bool* **references** - Set **true** to enable asynchronous loading of Node References; **false** - to disable it.

## bool isAsyncLoadNodeReferences () const

Returns the current value indicating if asynchronous loading of Node References is enabled.
### Return value

**true** if asynchronous loading of Node References is enabled ; otherwise **false**.
## static getEventNodeRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventNodeAdded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPostWorldShutdown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPreWorldShutdown () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPostWorldInit () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPreWorldInit () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPostNodeSave () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPreNodeSave () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPostWorldClear () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPreWorldClear () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPostWorldSave () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPreWorldSave () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPostWorldLoad () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPreWorldLoad () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## void engine.world. set ( string function , Variable value )

Set a variable in a world script (this function can be called directly from any other script).
### Arguments

- *string* **function** - Variable name.
- *Variable* **value** - Value of the variable.

## Variable engine.world. get ( string function )

Returns a variable from the world script. Instances of user-defined classes cannot be requested in such a manner.
### Arguments

- *string* **function** - Variable name with a namespace, if needed.

### Return value

Requested instance.
## int engine.world. getCollisionObjects ( Variable v , Variable value )


Searches for all [collider objects](../../../principles/physics/collision/index.md#collider) within a given bounding volume. Intersection is performed with node surfaces (polygons).


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *Variable* **v** - Variable. Can be one of the following:

  - BoundSphere bs - The bounding sphere.
  - BoundBox bb - The bounding box.
  - BoundFrustum bf - The bounding frustum.
- *Variable* **value** - Array into which the result will be placed.

### Return value

Number of nodes found.
## int engine.world. getCollisionObjects ( vec3 p0 , vec3 p1 , int[] ret )


Performs tracing from the p0 point to the p1 point to find all [collider objects](../../../principles/physics/collision/index.md#collider) intersecting the line. This function detects intersection with surfaces (polygons) of mesh and terrain objects.


Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_usc.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int[]* **ret** - Array into which the result will be placed.

### Return value

Number of nodes found.
## int engine.world. getCollisionObjectVariables ( Variable v , Variable value )


Searches for all [collider objects](../../../principles/physics/collision/index.md#collider) which have set user [variables](../../../api/library/nodes/class.node_usc.md#setVariable_Variable_void). Intersection is performed with node surfaces (polygons). The search is performed within a given bounding volume.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *Variable* **v** - Variable. Can be one of the following:

  - BoundSphere bs - The bounding sphere.
  - BoundBox bb - The bounding box.
  - BoundFrustum bf - The bounding frustum.
- *Variable* **value** - Array into which the result will be placed.

### Return value

Number of nodes found.
## int engine.world. getCollisionObjectVariables ( vec3 p0 , vec3 p1 , int[] ret )


Performs tracing from the p0 point to the p1 point to find all [collider objects](../../../principles/physics/collision/index.md#collider) which have set user [variables](../../../api/library/nodes/class.node_usc.md#setVariable_Variable_void). This function detects intersection with surfaces (polygons) of mesh and terrain objects.


Collisions with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Collision](../../../api/library/objects/class.object_usc.md#setCollision_int_int_void) flag is enabled.
3. The surface has a material assigned.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int[]* **ret** - Array into which the result will be placed.

### Return value

Number of nodes found.
## void engine.world. setData ( string name , string data )

Sets user data associated with the world with the specified key. In the `*.world` file, the data is set in the data tag with the specified key.
### Arguments

- *string* **name** - String containing a key identifying user data to be stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.
- *string* **data** - New user data.

## string engine.world. getData ( string name )

Returns user string data associated with the world by the specified key. This string is written directly into the data tag of the `*.world` file with the specified key.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

### Return value

User string data.
## int engine.world. hasData ( string name )

Checks whether user string data associated with the world by the specified key is stored in the data tag of the `*.world` file.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

### Return value

**1** if user string data associated with the world by the specified key is stored in the data tag of the `*.world` file; otherwise, **0**.
## void engine.world. removeData ( string name )

Removes user string data associated with the world by the specified key. This string is stored in the data tag of the `*.world` file with the specified key.
### Arguments

- *string* **name** - String containing a key identifying user data stored in the `*.world` file. > **Notice:** The "editor_data" key is reserved for the UnigineEditor.

## int engine.world. isFunction ( string name , int num_args )

Returns a value indicating if the given function with the specified number of arguments exists in the world script.
### Arguments

- *string* **name** - Function name.
- *int* **num_args** - Number of function arguments.

### Return value

1 if the function exists; otherwise, 0.
## Object engine.world. getIntersection ( vec3 p0 , vec3 p1 , vec3 mask , int[] exclude , Variable value )


Performs tracing from the p0 point to the p1 point to find the list of objects intersecting the line. This function detects intersection with surfaces (polygons) of meshes. An intersection can be found found only if an object is matching the intersection mask.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_usc.md#setIntersection_int_int_void) flag is enabled.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *vec3* **mask** - Intersection mask. If **0** is passed, the function will return **NULL**.
- *int[]* **exclude** - The list of objects IDs to be excluded.
- *Variable* **value** - Variable. Can be one of the following: > **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.

  - WorldIntersection intersection - The [WorldIntersection](../../../api/library/worlds/class.worldintersection_usc.md) class instance.
  - WorldIntersectionNormal normal - The [WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_usc.md) class instance.
  - WorldIntersectionTexCoord texcoord - The [WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_usc.md) class instance.

### Return value

The first intersected object, if found; otherwise, 0.
## Object engine.world. getIntersection ( vec3 p0 , vec3 p1 , int mask , Variable value )


Performs tracing from the p0 point to the p1 point to find the nearest object which intersects the line. This function detects intersection with surfaces (polygons) of meshes. An intersection is found only if an object is matching the intersection mask.


![](worldintersection.png)


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_usc.md#setIntersection_int_int_void) flag is enabled.


**Usage Example**


The following example shows how you can get the intersection information by using the WorldIntersection class. In this example the line is an invisible traced line from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *Unigine::getPlayerMouseDirection()* function from `core/scripts/utils.h`.
- Create an instance of the WorldIntersection class to get the intersection information.
- Check, if there is a intersection with an object. The *engine.World.getIntersection()* function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The WorldIntersection class instance gets the coordinates of the intersection point, the index of the surface and the index of the intersected triangle. You can get all these fields by using [*getIndex()*](../../../api/library/worlds/class.worldintersection_usc.md#getIndex_int), [*getPoint()*](../../../api/library/worlds/class.worldintersection_usc.md#getPoint_Vec3) and [*getSurface()*](../../../api/library/worlds/class.worldintersection_usc.md#getSurface_int) functions


```cpp
#include <core/scripts/utils.h>
/* ... */
// define two vec3 coordinates
vec3 p0,p1;
// get the mouse direction from camera (p0) to cursor pointer (p1)
Unigine::getPlayerMouseDirection(p0,p1);

// create an instance of the WorldIntersection class to get the result
WorldIntersection wis = new WorldIntersection();

// create an instance for intersected object
Object object = engine.World.getIntersection(p0,p1,1,wis);

// if the intersection has been occurred, change the parameter and the texture of the object's material
if(object != NULL)
{
	forloop(int i=0; object.getNumSurfaces())
	{
		object.setMaterialParameterFloat4("diffuse_color", vec4(1.0f, 0.0f, 0.0f, 1.0f),i);
		object.setMaterialTexture("diffuse","", i);

		// show intersection details in console
		log.message("point: %s index: %i surface: %i \n", typeinfo(wis.getPoint()), wis.getIndex(), wis.getSurface());
	}

}
/* ... */

```


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int* **mask** - Intersection mask. If **0** is passed, the function will return **NULL**.
- *Variable* **value** - Variable. Can be one of the following: > **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.

  - WorldIntersection intersection - The [WorldIntersection](../../../api/library/worlds/class.worldintersection_usc.md) class instance.
  - WorldIntersectionNormal normal - The [WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_usc.md) class instance.
  - WorldIntersectionTexCoord texcoord - The [WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_usc.md) class instance.

### Return value

The first intersected object, if found; otherwise, 0.
## int engine.world. getIntersectionNodes ( Variable value , int type , int[] ret )


Searches for all nodes (or nodes filtered by type) within a given bounding volume. Intersection is performed with node surfaces (polygons). The search is performed within a given bounding volume.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *Variable* **value** - Variable. Can be one of the following:

  - BoundSphere bs - The bounding sphere.
  - BoundBox bb - The bounding box.
  - BoundFrustum bf - The bounding frustum.
- *int* **type** - Node type (one of the [NODE_*](../../../api/library/nodes/class.node_usc.md#DECAL_BEGIN) variables); -1 is not to use a filter.
- *int[]* **ret** - Array into which the result will be placed.

### Return value

Number of nodes found.
## int engine.world. getIntersectionNodeVariables ( Variable value , int type , int[] ret )


Searches for all nodes (or nodes filtered by type) which have set user [variables](../../../api/library/nodes/class.node_usc.md#setVariable_Variable_void). Intersection is performed with node surfaces (polygons). The search is performed within a given bounding volume.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *Variable* **value** - Variable. Can be one of the following:

  - BoundSphere bs - The bounding sphere.
  - BoundBox bb - The bounding box.
  - BoundFrustum bf - The bounding frustum.
- *int* **type** - Node type (one of the [NODE_*](../../../api/library/nodes/class.node_usc.md#DECAL_BEGIN) variables); -1 is not to use a filter.
- *int[]* **ret** - Array into which the result will be placed.

### Return value

Number of nodes found.
## int engine.world. getIntersectionObjects ( Variable value , int[] ret )


Searches for all objects within a given bounding volume. Intersection is performed with node surfaces (polygons).


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *Variable* **value** - Variable. Can be one of the following:

  - BoundSphere bs - The bounding sphere.
  - BoundBox bb - The bounding box.
  - BoundFrustum bf - The bounding frustum.
- *int[]* **ret** - Array into which the result will be placed.

### Return value

Number of nodes found.
## int engine.world. getIntersectionObjects ( vec3 p0 , vec3 p1 , int[] ret )


Performs tracing from the p0 point to the p1 point to find all objects intersecting the line. This function detects intersection with surfaces (polygons) of mesh and terrain objects.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_usc.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int[]* **ret** - Array into which the result will be placed.

### Return value

Number of nodes found.
## int engine.world. getIntersectionObjectVariables ( Variable v , Variable value )


Searches for the [data](#setData_cstr_cstr_void) associated with all objects (or objects filtered by type) within a given bounding volume. Intersection is performed with object surfaces (polygons).


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *Variable* **v** - Variable. Can be one of the following:

  - BoundSphere bs - The bounding sphere.
  - BoundBox bb - The bounding box.
  - BoundFrustum bf - The bounding frustum.
- *Variable* **value** - Array into which the result will be placed.

### Return value

Number of nodes found.
## int engine.world. getIntersectionObjectVariables ( vec3 p0 , vec3 p1 , int[] ret )


Performs tracing from the p0 point to the p1 point to find all objects which have set user [variables](../../../api/library/nodes/class.node_usc.md#setVariable_Variable_void). This function detects intersection with surfaces (polygons) of meshes.


Intersections with the surface can be found only if the following conditions are fulfilled:


1. The surface is enabled.
2. Per-surface [Intersection](../../../api/library/objects/class.object_usc.md#setIntersection_int_int_void) flag is enabled.


> **Notice:** As a new node becomes a part of the BSP tree only after the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method is called (the engine calls the method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed), all engine subsystems can process this node only in the next frame. If you need to get the node in the very first frame, call the *[updateSpatial()](../../../api/library/engine/class.world_usc.md#updateSpatial_void)* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


### Arguments

- *vec3* **p0** - Coordinates of the line start point.
- *vec3* **p1** - Coordinates of the line end point.
- *int[]* **ret** - Array into which the result will be placed.

### Return value

Number of nodes found.
## int engine.world. loadWorld ( string path )

Loads a world from the specified file path and replaces the current world with it. The world is not loaded immediately � loading starts at the [beginning](../../../code/fundamentals/execution_sequence/main_loop.md#update) of the next frame, while the current world is unloaded at the [end](../../../code/fundamentals/execution_sequence/main_loop.md#swap) of the current frame.
### Arguments

- *string* **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).

### Return value

**1** if the world is loaded successfully; otherwise, **0**.
## int engine.world. loadWorld ( string path , int partial_path )

Loads a world from the specified file path and replaces the current world with it. The world is not loaded immediately � loading starts at the [beginning](../../../code/fundamentals/execution_sequence/main_loop.md#update) of the next frame, while the current world is unloaded at the [end](../../../code/fundamentals/execution_sequence/main_loop.md#swap) of the current frame.
### Arguments

- *string* **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).
- *int* **partial_path** - **1** if the path to the world file is partial; or **0** if it is a full path.

### Return value

**1** if the world is loaded successfully; otherwise, **0**.
## int engine.world. loadWorldForce ( string path )

Loads a world from the specified file path and replaces the current world with it. The world is loaded immediately, breaking the Execution Sequence, therefore should be used either before [Engine::update()](../../../code/fundamentals/execution_sequence/main_loop.md#update) or after [Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap). If called in Engine::update(), the Execution Sequence will be as follows: update() before calling loadWorldForce(), loadWorldForce(), shutdown(), continuation of update() from the place of interruption, postUpdate(), swap(), init(), etc. This function is recommended for the Editor-related use.
### Arguments

- *string* **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).

### Return value

**1** if the world is loaded successfully; otherwise, **0**.
## int engine.world. loadWorldForce ( string path , int partial_path )

Loads a world from the specified file path and replaces the current world with it. The world is loaded immediately, breaking the Execution Sequence, therefore should be used either before [Engine::update()](../../../code/fundamentals/execution_sequence/main_loop.md#update) or after [Engine::swap()](../../../code/fundamentals/execution_sequence/main_loop.md#swap). If called in *Engine::update()*, the Execution Sequence will be as follows: *update()* before calling *loadWorldForce(), loadWorldForce(), shutdown()*, continuation of *update()* from the place of interruption, *postUpdate(), swap(), init()*, etc. This function is recommended for the Editor-related use.
### Arguments

- *string* **path** - Path to the [file describing the world](../../../principles/world_structure/index.md).
- *int* **partial_path** - **1** if the path to the world file is partial; or **0** if it is a full path.

### Return value

**1** if the world is loaded successfully; otherwise, **0**.
## int engine.world. saveWorld ( )

Saves the World.
### Return value

**1**, if the world has been saved successfully; otherwise **0**.
## int engine.world. saveWorld ( string path )

Saves the world to the specified location.
### Arguments

- *string* **path** - Path to where the world is going to be saved.

### Return value

**1**, if the world has been saved successfully; otherwise **0**.
## int engine.world. reloadWorld ( )

Reloads the World.
### Return value

**1**, if the world has been reloaded successfully; otherwise **0**.
## int engine.world. quitWorld ( )

Closes the World.
### Return value

**1**, if the world has been quit successfully; otherwise **0**.
## int engine.world. addWorld ( string name )

Loads a world from a file and adds it to the current World.
### Arguments

- *string* **name** - Name of the [file describing the world](../../../principles/world_structure/index.md).

### Return value

**1** if the world is loaded and added successfully; otherwise, **0**.
## bool engine.world. isNode ( int id )

Checks if a node with a given ID exists in the World.
### Arguments

- *int* **id** - Node ID.

### Return value

**1** if the node with the given ID exists; otherwise, **0**.
## void engine.world. getNodes ( Node [] OUT_nodes , int expand_node_reference = true , int expand_world_clutter = true )

 Collects all instances of all nodes (either loaded from the `*.world` file or created dynamically at run time), including [cache](../../../principles/world_management/index.md#node_cache), [Node Reference internals](../../../api/library/nodes/class.nodereference_usc.md#unpacking), World Clutters contents (if the corresponding flags are set) and puts them to the specified output list.
> **Notice:** If you need only root nodes to be returned, use [getRootNodes()](#getRootNodes_VECNode_void) instead


### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)[]* **OUT_nodes** - Array with node smart pointers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **expand_node_reference** - **1** to get nodes contained in *NodeReferences*; otherwise, **0**.
- *int* **expand_world_clutter** - **1** to get nodes contained in *WorldClutters*; otherwise, **0**.

## int engine.world. isVariable ( string name )

Returns a value indicating if the given variable exists in the world script.
### Arguments

- *string* **name** - Variable name.

### Return value

1 if the variable exists; otherwise, 0.
## Variable engine.world. call ( Variable function )

Executes a function of the world script from an external script. The function should not take any arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.

### Return value

Value returned by the function.
## Variable engine.world. call ( Variable function , Variable arg0 )

Executes a function of the world script from an external script. The function should take one argument.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.world. call ( Variable function , Variable arg0 , Variable arg1 )

Executes a function of the world script from an external script. The function should take two arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.world. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 )

Executes a function of the world script from an external script. The function should take three arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.world. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 , Variable arg3 )

Executes a function of the world script from an external script. The function should take four arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.
- *Variable* **arg3** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.world. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 , Variable arg3 , Variable arg4 )

Executes a function of the world script from an external script. The function should take five arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.
- *Variable* **arg3** - Argument of the function.
- *Variable* **arg4** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.world. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 , Variable arg3 , Variable arg4 , Variable arg5 )

Executes a function of the world script from an external script. The function should take six arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.
- *Variable* **arg3** - Argument of the function.
- *Variable* **arg4** - Argument of the function.
- *Variable* **arg5** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.world. call ( Variable function , int id = [] )

Executes a function of the world script from an external script. The function takes an array of arguments (up to 8 arguments are supported).
### Arguments

- *Variable* **function** - Name of the function to execute.
- *int* **id** - Array of up to 8 arguments.

### Return value

Value returned by the function.
## engine.world. loadNode ( bool cache = true )

Loads a node (or a hierarchy of nodes) from a `.node / .fbx` file. If the node is loaded successfully, it is managed by the current world (its *[Lifetime](../../../api/library/nodes/class.node_usc.md#getLifetime_int)* is *[World](../../../api/library/nodes/class.node_usc.md#LIFETIME)*).
[Cached nodes](../../../principles/world_management/index.md#node_cache) remain in the memory. If you don't intend to load more node references from a certain `*.node` asset, set the **cache** argument to 0 or you can delete cached nodes from the list of world nodes afterwards by using the *[destroyCacheNode()](#destroyCacheNode_cstr_int)* method.


### Arguments

- *bool* **cache** - true to use caching of nodes, false not to use.

### Return value

Loaded node; NULL if the node cannot be loaded.
## void engine.world. updateSpatial ( )


Updates the node [BSP (binary space partitioning) tree](../../../principles/world_management/index.md#outdoor).


The engine calls this method automatically each frame after the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* code is executed. As a new node becomes a part of the BSP tree only after this method is called, all engine subsystems (renderer, physics, sound, pathfinding, collisions, intersections, etc.) can process this node only in the next frame. If you need the subsystem to process the node in the very first frame, you can call the *updateSpatial()* method manually. The engine will call this method automatically after the *update()* code is executed anyways.


## Node engine.world. getNodeByID ( int node_id )

Returns a node by its identifier if it exists.
### Arguments

- *int* **node_id** - Node ID.

### Return value

## Node engine.world. getNodeByName ( string name )


Returns a node by its name if it exists. If the world contains multiple nodes having the same name, only the first one found shall be returned. To get all nodes having the same name, use the [*getNodesByName()*](#getNodesByName_cstr_VECNode_void) method.


> **Notice:** method filters out isolated node hierarchies and cache nodes, so it does not return nodes having a possessor (*NodeReference / Clutter / Cluster*) among its predecessors or nodes from cache.


### Arguments

- *string* **name** - Node name.

### Return value

## Node engine.world. getNodeByType ( int type )

Returns the first node of the specified type in the World. Hidden and system nodes are ignored.
### Arguments

- *int* **type** - Node type identifier, one of the [NODE_*](../../../api/library/nodes/class.node_usc.md#NODE_BEGIN) values.

### Return value

## void engine.world. clearBindings ( )

Clears internal buffers with pointers and instances. This function is used for proper cloning of objects with hierarchies, for example, bodies and joints. Should be called before cloning.
## int engine.world. getRootNodeIndex ( Node node )

Returns the index for the specified root node, that belongs to the world hierarchy.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Root node, for which an index is to be obtained.

### Return value

Index of the specified root node if it exists; otherwise, -1.
## void engine.world. setRootNodeIndex ( Node node , int index )

Sets a new index for the specified root node, that belongs to the world hierarchy.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Root node, for which a new index is to be set.
- *int* **index** - New index to be set for the specified root node.

## void engine.world. setNodeIdSeed ( unsigned int seed )

Sets a seed value for random generation of a node ID. This method is used for deterministic generation.
### Arguments

- *unsigned int* **seed** - A seed value.

## void engine.world. setNodeIdRange ( int from , int to )

Sets a range for random generation of a node ID. This method can be used, for example, to generate IDs for nodes divided in several groups: within a group, IDs will be generated in a separate range.
### Arguments

- *int* **from** - Beginning of the range.
- *int* **to** - End of the range.

## int engine.world. removeNodeFile ( string file_path )

### Arguments

- *string* **file_path** - Path to the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache with related *Node References* removed from the scene; otherwise, false.
## int engine.world. reloadNodeFile ( string file_path )

### Arguments

- *string* **file_path** - Path to the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache and reloaded from the source file; otherwise, false.
## int engine.world. destroyCacheNode ( string file_path )

### Arguments

- *string* **file_path** - Path to the `*.node` file.

### Return value

true if nodes for the given `*.node` file were successfully removed from cache; otherwise, false.
