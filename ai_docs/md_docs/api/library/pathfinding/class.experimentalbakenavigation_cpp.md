# Unigine::ExperimentalBakeNavigation Class (CPP)

**Header:** #include <UnigineExperimentalNavigation.h>

> **Notice:** This class is a singleton.


Builds navigation meshes out of the geometry of the scene. Baking voxelizes everything the bake mask of a [navigation mesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md) selects, works out which surfaces an agent of the configured size can stand and walk on, and turns the result into convex polygons arranged in tiles.


Each operation comes in two forms:


- **Force** � runs to completion before returning. Meant for tools and loading screens.
- **Async** � spreads the tiles over worker threads and hands back an [ExperimentalNavigationBakeQuery](../../../api/library/pathfinding/class.experimentalnavigationbakequery_cpp.md) to watch.


At runtime only the asynchronous form is practical � a full bake takes far longer than a frame.


Rebaking a whole mesh because one crate moved would be wasteful, so there is a second entry point: invalidation marks a region as out of date and only the tiles that intersect it are rebuilt.


## ExperimentalBakeNavigation Class

### Members

## bool isBaking () const

Returns the current value indicating if a bake is running right now.
### Return value

**true** if a bake is in progress; otherwise **false**.
## void setNumWorkers ( int workers )

Sets a new number of worker threads a bake is allowed to spread its tiles over. Capping it leaves room for the rest of the application while a bake runs in the background. Mapped to the *navigation_bake_num_workers* console variable.
### Arguments

- *int* **workers** - The number of workers. The default value is 0, which means every worker of the background pool; the figure this resolves to is reported by [getNumWorkersAuto()](#getNumWorkersAuto_int).

## int getNumWorkers () const

Returns the current number of worker threads a bake is allowed to spread its tiles over. Capping it leaves room for the rest of the application while a bake runs in the background. Mapped to the *navigation_bake_num_workers* console variable.
### Return value

Current number of workers. The default value is 0, which means every worker of the background pool; the figure this resolves to is reported by [getNumWorkersAuto()](#getNumWorkersAuto_int).
---

## Ptr < ExperimentalNavigationBakeQuery > bakeAsync ( const Ptr < ExperimentalNavigationMesh > & navigation_mesh )

Starts baking a navigation mesh on the workers and returns at once.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)> &* **navigation_mesh** - Navigation mesh to be baked.

### Return value

Query to watch the bake with.
## Ptr < ExperimentalNavigationBakeQuery > bakeAsync ( const Vector < Ptr < ExperimentalNavigationMesh >> & navigation_meshes )

Starts baking several navigation meshes on the workers. One query reports the progress of the whole batch, so a single progress bar covers all of them.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)>> &* **navigation_meshes** - Navigation meshes to be baked.

### Return value

Query covering the whole batch.
## Ptr < ExperimentalNavigationBakeQuery > bakeAsync ( const Ptr < NavigationMesh > & navigation_mesh )

Starts baking a [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md) node on the workers and returns at once. The surface is built by the same pipeline and then converted into the triangle mesh that node navigates over, so its walkable space no longer has to be modeled by hand. The bake is configured through [BakeSettings](../../../api/library/pathfinding/class.experimentalnavigationbakesettings_cpp.md) of that node, and the result is written to the mesh asset its **Mesh Path** points at.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md)> &* **navigation_mesh** - Navigation mesh to be baked.

### Return value

Query to watch the bake with.
## Ptr < ExperimentalNavigationBakeQuery > bakeAsync ( const Vector < Ptr < NavigationMesh >> & navigation_meshes )

Starts baking several [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md) nodes on the workers. One query reports the progress of the whole batch.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md)>> &* **navigation_meshes** - Navigation meshes to be baked.

### Return value

Query covering the whole batch.
## Ptr < ExperimentalNavigationBakeQuery > bakeAsync ( int navigation_mask )

Starts baking every navigation mesh in the world whose navigation mask shares a bit with the given one.
### Arguments

- *int* **navigation_mask** - Mask selecting the navigation meshes to be baked.

### Return value

Query covering every selected navigation mesh.
## bool bakeForce ( const Ptr < ExperimentalNavigationMesh > & navigation_mesh )

Bakes a navigation mesh and returns when it is done. The call blocks for as long as the bake takes, which on a large mesh is far longer than a frame.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)> &* **navigation_mesh** - Navigation mesh to be baked.

### Return value

true if the mesh was baked; otherwise, false.
## bool bakeForce ( const Vector < Ptr < ExperimentalNavigationMesh >> & navigation_meshes )

Bakes several navigation meshes and returns when all of them are done.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)>> &* **navigation_meshes** - Navigation meshes to be baked.

### Return value

true if every mesh was baked; otherwise, false.
## bool bakeForce ( const Ptr < NavigationMesh > & navigation_mesh )

Bakes a [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md) node and blocks until it is done. The same conversion as in the asynchronous overload applies.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md)> &* **navigation_mesh** - Navigation mesh to be baked.

### Return value

true if the mesh was baked; otherwise, false.
## bool bakeForce ( const Vector < Ptr < NavigationMesh >> & navigation_meshes )

Bakes several [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md) nodes and blocks until the whole batch is done.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md)>> &* **navigation_meshes** - Navigation meshes to be baked.

### Return value

true if every mesh was baked; otherwise, false.
## bool bakeForce ( int navigation_mask )

Bakes every navigation mesh in the world whose navigation mask shares a bit with the given one, and returns when all of them are done.
### Arguments

- *int* **navigation_mask** - Mask selecting the navigation meshes to be baked.

### Return value

true if every selected mesh was baked; otherwise, false.
## int getNumWorkersAuto ( )

Returns how many workers a bake actually gets when the worker count is left at the automatic value. Use it to see the real figure behind the automatic 0.
### Return value

Number of workers the automatic mode resolves to.
## void invalidateAsync ( const Math:: WorldBoundBox & bounds )

Marks a region of the world as out of date and queues the tiles that intersect it for a rebuild. The work is paced by the invalidation budget, so a door opening or a wall collapsing does not stall the frame.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Region that has gone out of date, in world coordinates.

## void invalidateAsync ( const Math:: WorldBoundBox & bounds , int navigation_mask )

Marks a region as out of date for the navigation meshes matching the given mask only. Use it when the change concerns some of the meshes covering the place and not the others.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Region that has gone out of date, in world coordinates.
- *int* **navigation_mask** - Mask selecting the navigation meshes to be affected.

## void invalidateForce ( const Math:: WorldBoundBox & bounds )

Rebuilds the tiles intersecting a region and returns when they are ready. Use it when the very next query has to see the change.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Region that has gone out of date, in world coordinates.

## void invalidateForce ( const Math:: WorldBoundBox & bounds , int navigation_mask )

Rebuilds the tiles intersecting a region for the navigation meshes matching the given mask, and returns when they are ready.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Region that has gone out of date, in world coordinates.
- *int* **navigation_mask** - Mask selecting the navigation meshes to be affected.

## bool isInitialized ( )

Returns a value indicating if the baking subsystem is initialized.
### Return value

true if the baking subsystem is initialized; otherwise, false.
## void stop ( )

Stops everything that is being baked right now. Tiles already built are kept; the queued ones are dropped.
## void waitForce ( )

Blocks the calling thread until every running bake is finished.
