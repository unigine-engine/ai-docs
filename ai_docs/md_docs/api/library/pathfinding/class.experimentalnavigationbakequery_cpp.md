# Unigine::ExperimentalNavigationBakeQuery Class (CPP)

**Header:** #include <UnigineExperimentalNavigation.h>


Handle of a bake running in the background. It is returned by the asynchronous bake methods of the [ExperimentalBakeNavigation](../../../api/library/pathfinding/class.experimentalbakenavigation_cpp.md) singleton and is the only way to watch a bake, drive a progress bar, or stop one that is no longer needed.


Baking a large world takes tens of seconds and consists of many independent tiles, so the query reports progress on several levels at once: which mesh is being worked on, how many tiles are already built and how many are still queued, and whether any of them failed. A bake that finishes with failed tiles ends up [partial](#STATUS_PARTIAL) rather than failed � the navigation mesh is usable, with holes where the tiles did not build.


## ExperimentalNavigationBakeQuery Class

### Enums

## STATUS

| Name | Description |
|---|---|
| **STATUS_RUNNING** = 0 | The bake is still in progress. |
| **STATUS_READY** = 1 | The bake finished and every tile was built. |
| **STATUS_PARTIAL** = 2 | The bake finished, but some tiles failed to build. The navigation mesh is usable and has holes where those tiles are; their number is reported by [NumFailedTiles](#NumFailedTiles). |
| **STATUS_FAILED** = 3 | The bake could not be carried out at all. |
| **STATUS_CANCELLED** = 4 | The bake was stopped by [cancel()](#cancel_void). Whatever had been built before that stays in the navigation mesh. |

### Members

## float getElapsedTime () const

Returns the current time the bake has been running.
### Return value

Current elapsed time, in seconds.
## bool isReady () const

Returns the current value indicating if the bake has finished, whatever its outcome.
### Return value

**true** if the bake has finished; otherwise **false**.
## bool isSamplingTerrain () const

Returns the current value indicating if the bake is currently sampling terrain. Terrain sampling is a distinct stage that runs before the tiles are built and can take a noticeable share of the total time, which is worth showing separately in a progress bar.
### Return value

**true** if the bake is sampling terrain; otherwise **false**.
## const char * getMeshName () const

Returns the current name of the navigation mesh the bake is working on right now. With a batch of meshes queued, this is what tells the user where the process has got to.
### Return value

Current name of the navigation mesh being baked.
## int getNumBakedMeshes () const

Returns the current number of navigation meshes the bake has already finished.
### Return value

Current number of finished navigation meshes.
## int getNumBuiltTiles () const

Returns the current number of tiles the bake has already built.
### Return value

Current number of built tiles.
## int getNumFailedMeshes () const

Returns the current number of navigation meshes that could not be baked at all. Distinct from the failed tiles below: a failed mesh produced nothing, a failed tile is a hole in an otherwise usable mesh.
### Return value

Current number of failed navigation meshes.
## int getNumFailedTiles () const

Returns the current number of tiles that could not be built. A non-zero value means the resulting navigation mesh has holes in it.
### Return value

Current number of failed tiles.
## int getNumMeshes () const

Returns the current number of navigation meshes the bake was started for.
### Return value

Current number of queued navigation meshes.
## int getNumPendingTiles () const

Returns the current number of tiles still waiting to be built.
### Return value

Current number of pending tiles.
## float getProgress () const

Returns the current share of the work already done, counting both terrain sampling and tile building.
### Return value

Current progress, in the [0;1] range.
## ExperimentalNavigationBakeQuery::STATUS getStatus () const

Returns the current current state of the bake.
### Return value

Current status, one of the [STATUS_*](#STATUS_RUNNING) values.
---

## void cancel ( )

Stops the bake. Tiles already built are kept, the queued ones are dropped, and the query settles on [STATUS_CANCELLED](#STATUS_CANCELLED).
## void waitForce ( )

Blocks the calling thread until the bake finishes. Returns immediately if it is already over.
