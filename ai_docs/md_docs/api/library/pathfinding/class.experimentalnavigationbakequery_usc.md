# Unigine::ExperimentalNavigationBakeQuery Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Handle of a bake running in the background. It is returned by the asynchronous bake methods of the [ExperimentalBakeNavigation](../../../api/library/pathfinding/class.experimentalbakenavigation_usc.md) singleton and is the only way to watch a bake, drive a progress bar, or stop one that is no longer needed.


Baking a large world takes tens of seconds and consists of many independent tiles, so the query reports progress on several levels at once: which mesh is being worked on, how many tiles are already built and how many are still queued, and whether any of them failed. A bake that finishes with failed tiles ends up [partial](#STATUS_PARTIAL) rather than failed � the navigation mesh is usable, with holes where the tiles did not build.


## ExperimentalNavigationBakeQuery Class

### Members

## float getElapsedTime () const

Returns the current time the bake has been running.
### Return value

Current elapsed time, in seconds.
## int isReady () const

Returns the current value indicating if the bake has finished, whatever its outcome.
### Return value

Current the bake has finished
## int isSamplingTerrain () const

Returns the current value indicating if the bake is currently sampling terrain. Terrain sampling is a distinct stage that runs before the tiles are built and can take a noticeable share of the total time, which is worth showing separately in a progress bar.
### Return value

Current the bake is sampling terrain
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
## int getStatus () const

Returns the current current state of the bake.
### Return value

Current status, one of the [STATUS_*](#STATUS_RUNNING) values.
---

## void cancel ( )

Stops the bake. Tiles already built are kept, the queued ones are dropped, and the query settles on [STATUS_CANCELLED](#STATUS_CANCELLED).
## void waitForce ( )

Blocks the calling thread until the bake finishes. Returns immediately if it is already over.
