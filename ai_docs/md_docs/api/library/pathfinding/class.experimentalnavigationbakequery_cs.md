# Unigine::ExperimentalNavigationBakeQuery Class (CS)


Handle of a bake running in the background. It is returned by the asynchronous bake methods of the [ExperimentalBakeNavigation](../../../api/library/pathfinding/class.experimentalbakenavigation_cs.md) singleton and is the only way to watch a bake, drive a progress bar, or stop one that is no longer needed.


Baking a large world takes tens of seconds and consists of many independent tiles, so the query reports progress on several levels at once: which mesh is being worked on, how many tiles are already built and how many are still queued, and whether any of them failed. A bake that finishes with failed tiles ends up [partial](#STATUS_PARTIAL) rather than failed � the navigation mesh is usable, with holes where the tiles did not build.


## ExperimentalNavigationBakeQuery Class

### Enums

## STATUS

| Name | Description |
|---|---|
| **RUNNING** = 0 | The bake is still in progress. |
| **READY** = 1 | The bake finished and every tile was built. |
| **PARTIAL** = 2 | The bake finished, but some tiles failed to build. The navigation mesh is usable and has holes where those tiles are; their number is reported by [NumFailedTiles](#NumFailedTiles). |
| **FAILED** = 3 | The bake could not be carried out at all. |
| **CANCELLED** = 4 | The bake was stopped by [cancel()](#cancel_void). Whatever had been built before that stays in the navigation mesh. |

### Properties

## 🔒︎ float ElapsedTime

The time the bake has been running.
## 🔒︎ bool IsReady

The value indicating if the bake has finished, whatever its outcome.
## 🔒︎ bool IsSamplingTerrain

The value indicating if the bake is currently sampling terrain. Terrain sampling is a distinct stage that runs before the tiles are built and can take a noticeable share of the total time, which is worth showing separately in a progress bar.
## 🔒︎ string MeshName

The name of the navigation mesh the bake is working on right now. With a batch of meshes queued, this is what tells the user where the process has got to.
## 🔒︎ int NumBakedMeshes

The number of navigation meshes the bake has already finished.
## 🔒︎ int NumBuiltTiles

The number of tiles the bake has already built.
## 🔒︎ int NumFailedMeshes

The number of navigation meshes that could not be baked at all. Distinct from the failed tiles below: a failed mesh produced nothing, a failed tile is a hole in an otherwise usable mesh.
## 🔒︎ int NumFailedTiles

The number of tiles that could not be built. A non-zero value means the resulting navigation mesh has holes in it.
## 🔒︎ int NumMeshes

The number of navigation meshes the bake was started for.
## 🔒︎ int NumPendingTiles

The number of tiles still waiting to be built.
## 🔒︎ float Progress

The share of the work already done, counting both terrain sampling and tile building.
## 🔒︎ ExperimentalNavigationBakeQuery.STATUS Status

The current state of the bake.
### Members

---

## void Cancel ( )

Stops the bake. Tiles already built are kept, the queued ones are dropped, and the query settles on [STATUS_CANCELLED](#STATUS_CANCELLED).
## void WaitForce ( )

Blocks the calling thread until the bake finishes. Returns immediately if it is already over.
