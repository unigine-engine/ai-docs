# Unigine::ExperimentalNavigationMeshInvoker Class (CPP)

**Header:** #include <UnigineExperimentalNavigation.h>

**Inherits from:** Node


A node that keeps navigation mesh tiles resident around itself. In a world too large to hold a whole navigation mesh in memory, only the tiles near something that needs them are loaded; an invoker marks such a place. Attach one to the player, to each active non-player character, or to a camera, and the tiles follow it.


Loading and unloading use two distances rather than one on purpose: the gap between them is the hysteresis band that stops tiles from being reloaded every time the invoker steps back and forth across a single threshold. Tile traffic is paced by the streaming budget of the [ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cpp.md) singleton.


## ExperimentalNavigationMeshInvoker Class

### Members

## void setClearDistance ( float distance )

Sets a new distance beyond which the tiles around the invoker are unloaded. It should stay larger than the load distance � the gap between the two is what keeps a tile from being loaded and dropped repeatedly as the invoker moves back and forth.
### Arguments

- *float* **distance** - The clear distance, in units. The default value is 160.

## float getClearDistance () const

Returns the current distance beyond which the tiles around the invoker are unloaded. It should stay larger than the load distance � the gap between the two is what keeps a tile from being loaded and dropped repeatedly as the invoker moves back and forth.
### Return value

Current clear distance, in units. The default value is 160.
## void setLoadDistance ( float distance )

Sets a new distance within which the tiles around the invoker are kept loaded. It has to cover everything the agents near this invoker will ask about before they get there.
### Arguments

- *float* **distance** - The load distance, in units. The default value is 128.

## float getLoadDistance () const

Returns the current distance within which the tiles around the invoker are kept loaded. It has to cover everything the agents near this invoker will ask about before they get there.
### Return value

Current load distance, in units. The default value is 128.
## void setNavigationMask ( int mask )

Sets a new mask that selects the navigation meshes this invoker streams. A mesh is served only when its own navigation mask shares at least one bit with this one, so invokers can be dedicated to separate meshes.
### Arguments

- *int* **mask** - The navigation mask. The default value is 1.

## int getNavigationMask () const

Returns the current mask that selects the navigation meshes this invoker streams. A mesh is served only when its own navigation mask shares at least one bit with this one, so invokers can be dedicated to separate meshes.
### Return value

Current navigation mask. The default value is 1.
## int getNumUsedNavigationMeshes () const

Returns the current number of navigation meshes this invoker currently streams tiles for.
### Return value

Current number of served navigation meshes.
---

## static ExperimentalNavigationMeshInvokerPtr create ( )

The ExperimentalNavigationMeshInvoker constructor. Creates an invoker with the default distances.
## Ptr < ExperimentalNavigationMesh > getUsedNavigationMesh ( int num )

Returns a navigation mesh this invoker streams tiles for.
### Arguments

- *int* **num** - Navigation mesh number.

### Return value

Navigation mesh served by the invoker.
## bool prefetchTilesForce ( const Math:: WorldBoundBox & bounds )

Loads the tiles of a region through this invoker and returns when they are resident. Use it before teleporting the invoker somewhere far away, so that the first query at the destination does not fail for lack of data.
### Arguments

- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Region whose tiles are needed, in world coordinates.

### Return value

true if every tile of the region is resident afterwards; otherwise, false.
