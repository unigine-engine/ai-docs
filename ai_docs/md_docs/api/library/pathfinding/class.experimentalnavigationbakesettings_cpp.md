# Unigine::ExperimentalNavigationBakeSettings Class (CPP)

**Header:** #include <UnigineExperimentalNavigationBakeSettings.h>


Everything a navigation mesh is built with: the size of a voxel, the agent the surface is carved for, how tiles are cut, and how far the result is simplified. The settings describe the bake that is going to happen, not the data already loaded. What the loaded data was actually built with is reported by the **Data** properties of [ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md), and editing a setting never changes them on its own.


The object is not created directly. Both navigation mesh nodes own one and hand it out: [ExperimentalNavigationMesh.BakeSettings](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md#BakeSettings) and [NavigationMesh.BakeSettings](../../../api/library/pathfinding/class.navigationmesh_cpp.md#BakeSettings). That is why a single editor panel configures both, and why the settings survive as long as the node.


Each setting has a matching reset function instead of a documented default constant. Baking is started through the [ExperimentalBakeNavigation](../../../api/library/pathfinding/class.experimentalbakenavigation_cpp.md) singleton.


> **Notice:** Settings are read when a bake starts and are snapshotted for its whole run, so changing them while a bake is in flight affects the next bake, not the current one.


## ExperimentalNavigationBakeSettings Class

### Enums

## PARTITIONING

| Name | Description |
|---|---|
| **PARTITIONING_WATERSHED** = 0 | The slowest partitioning and the one that yields the best-shaped polygons. The right choice for a mesh baked once ahead of time. |
| **PARTITIONING_MONOTONE** = 1 | A fast partitioning that never leaves holes, but tends to produce long thin polygons. A reasonable middle ground when bake time matters. |
| **PARTITIONING_CHUNKY** = 2 | The surface is cut into fixed chunks. The fastest option and the one to use when tiles are rebuilt at runtime, at the price of the coarsest polygons. |

### Members

## void setBakeSize ( const Math:: vec3 & size )

Sets a new dimensions of the region around the node that the bake covers.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The bake size, in units. The default value is (64, 64, 32).

## Math:: vec3 getBakeSize () const

Returns the current dimensions of the region around the node that the bake covers.
### Return value

Current bake size, in units. The default value is (64, 64, 32).
## void setCellSize ( float size )

Sets a new horizontal size of a voxel. It is the main quality-against-cost knob of the bake: halving it quadruples both the detail and the memory the voxelization takes.
### Arguments

- *float* **size** - The cell size, in units. The default value is 0.3.

## float getCellSize () const

Returns the current horizontal size of a voxel. It is the main quality-against-cost knob of the bake: halving it quadruples both the detail and the memory the voxelization takes.
### Return value

Current cell size, in units. The default value is 0.3.
## void setCellHeight ( float height )

Sets a new vertical size of a voxel. It sets how precisely heights are resolved during the bake, and with them the smallest step or ledge that can be detected.
### Arguments

- *float* **height** - The cell height, in units. The default value is 0.2.

## float getCellHeight () const

Returns the current vertical size of a voxel. It sets how precisely heights are resolved during the bake, and with them the smallest step or ledge that can be detected.
### Return value

Current cell height, in units. The default value is 0.2.
## void setAgentRadius ( float radius )

Sets a new radius of the agent the mesh is baked for. The walkable surface is pulled back from every wall by this distance, so an agent following the mesh never clips one.
### Arguments

- *float* **radius** - The agent radius, in units. The default value is 0.6.

## float getAgentRadius () const

Returns the current radius of the agent the mesh is baked for. The walkable surface is pulled back from every wall by this distance, so an agent following the mesh never clips one.
### Return value

Current agent radius, in units. The default value is 0.6.
## void setAgentHeight ( float height )

Sets a new height of the agent the mesh is baked for. Anything with less headroom than this is left out of the walkable surface.
### Arguments

- *float* **height** - The agent height, in units. The default value is 2.

## float getAgentHeight () const

Returns the current height of the agent the mesh is baked for. Anything with less headroom than this is left out of the walkable surface.
### Return value

Current agent height, in units. The default value is 2.
## void setMaxSlopeAngle ( float angle )

Sets a new steepest slope an agent is considered able to walk up. Everything steeper is left out of the walkable surface. It is a property of the bake, not of an individual agent � agents with different climbing ability need separate meshes.
### Arguments

- *float* **angle** - The maximum slope angle, in degrees. The default value is 45.

## float getMaxSlopeAngle () const

Returns the current steepest slope an agent is considered able to walk up. Everything steeper is left out of the walkable surface. It is a property of the bake, not of an individual agent � agents with different climbing ability need separate meshes.
### Return value

Current maximum slope angle, in degrees. The default value is 45.
## void setMaxStepHeight ( float height )

Sets a new tallest step an agent can climb without a ramp. Surfaces separated by less than this are joined into one walkable region, which is what makes staircases and kerbs passable.
### Arguments

- *float* **height** - The maximum step height, in units. The default value is 0.4.

## float getMaxStepHeight () const

Returns the current tallest step an agent can climb without a ramp. Surfaces separated by less than this are joined into one walkable region, which is what makes staircases and kerbs passable.
### Return value

Current maximum step height, in units. The default value is 0.4.
## void setTileResolution ( int resolution )

Sets a new width of a tile in cells. Together with the cell size it fixes how large a tile is in the world, and with it the granularity of streaming and of rebuilds: smaller tiles are cheaper to rebuild one at a time but produce more seams.
### Arguments

- *int* **resolution** - The tile resolution, in cells. The default value is 64.

## int getTileResolution () const

Returns the current width of a tile in cells. Together with the cell size it fixes how large a tile is in the world, and with it the granularity of streaming and of rebuilds: smaller tiles are cheaper to rebuild one at a time but produce more seams.
### Return value

Current tile resolution, in cells. The default value is 64.
## void setPartitioning ( ExperimentalNavigationMesh::PARTITIONING partitioning )

Sets a new algorithm that splits the walkable surface into regions before it is turned into polygons. It trades bake time against the quality of the resulting polygons.
### Arguments

- *[ExperimentalNavigationMesh::PARTITIONING](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md#PARTITIONING)* **partitioning** - The partitioning algorithm, one of the [PARTITIONING_*](#PARTITIONING_WATERSHED) values. The default value is [PARTITIONING_WATERSHED](#PARTITIONING_WATERSHED).

## ExperimentalNavigationMesh::PARTITIONING getPartitioning () const

Returns the current algorithm that splits the walkable surface into regions before it is turned into polygons. It trades bake time against the quality of the resulting polygons.
### Return value

Current partitioning algorithm, one of the [PARTITIONING_*](#PARTITIONING_WATERSHED) values. The default value is [PARTITIONING_WATERSHED](#PARTITIONING_WATERSHED).
## void setRegionMinSize ( float size )

Sets a new size below which an isolated region is discarded. It removes the specks of walkable surface that appear on top of furniture and ledges, which no agent could reach anyway.
### Arguments

- *float* **size** - The minimum region size, in units. The default value is 2.4.

## float getRegionMinSize () const

Returns the current size below which an isolated region is discarded. It removes the specks of walkable surface that appear on top of furniture and ledges, which no agent could reach anyway.
### Return value

Current minimum region size, in units. The default value is 2.4.
## void setRegionMergeSize ( float size )

Sets a new size below which a region is merged into a larger neighbour instead of being kept on its own. It cuts down the polygon count without losing walkable space.
### Arguments

- *float* **size** - The region merge size, in units. The default value is 6.

## float getRegionMergeSize () const

Returns the current size below which a region is merged into a larger neighbour instead of being kept on its own. It cuts down the polygon count without losing walkable space.
### Return value

Current region merge size, in units. The default value is 6.
## void setRegionChunkSize ( int size )

Sets a new size of a chunk used by chunky partitioning. Only meaningful when [Partitioning](#Partitioning) is [PARTITIONING_CHUNKY](#PARTITIONING_CHUNKY).
### Arguments

- *int* **size** - The chunk size, in cells. The default value is 16.

## int getRegionChunkSize () const

Returns the current size of a chunk used by chunky partitioning. Only meaningful when [Partitioning](#Partitioning) is [PARTITIONING_CHUNKY](#PARTITIONING_CHUNKY).
### Return value

Current chunk size, in cells. The default value is 16.
## void setMaxEdgeError ( float error )

Sets a new largest deviation allowed when the outline of a region is simplified into polygon edges. Higher values give fewer, coarser polygons.
### Arguments

- *float* **error** - The maximum edge error, in cells. The default value is 1.3.

## float getMaxEdgeError () const

Returns the current largest deviation allowed when the outline of a region is simplified into polygon edges. Higher values give fewer, coarser polygons.
### Return value

Current maximum edge error, in cells. The default value is 1.3.
## void setSimplificationElevationRatio ( float ratio )

Sets a new how strongly edge simplification is held back where the surface changes height. Raising it keeps more detail on slopes and stairs while flat ground stays coarse.
### Arguments

- *float* **ratio** - The elevation ratio. The default value is 0.

## float getSimplificationElevationRatio () const

Returns the current how strongly edge simplification is held back where the surface changes height. Raising it keeps more detail on slopes and stairs while flat ground stays coarse.
### Return value

Current elevation ratio. The default value is 0.
## void setDetailSampleDistance ( float distance )

Sets a new spacing at which the detail mesh samples the underlying surface. The detail mesh is what makes the navigation mesh follow the height of uneven ground instead of floating flat above it.
### Arguments

- *float* **distance** - The detail sample distance, in units. The default value is 6.

## float getDetailSampleDistance () const

Returns the current spacing at which the detail mesh samples the underlying surface. The detail mesh is what makes the navigation mesh follow the height of uneven ground instead of floating flat above it.
### Return value

Current detail sample distance, in units. The default value is 6.
## void setDetailSampleError ( float error )

Sets a new largest vertical deviation the detail mesh may have from the real surface. Raising it produces fewer triangles and a navigation mesh that follows the ground more loosely.
### Arguments

- *float* **error** - The detail sample error, in units. The default value is 1.

## float getDetailSampleError () const

Returns the current largest vertical deviation the detail mesh may have from the real surface. Raising it produces fewer triangles and a navigation mesh that follows the ground more loosely.
### Return value

Current detail sample error, in units. The default value is 1.
## void setTerrainSampleScale ( float scale )

Sets a new coarseness of terrain sampling relative to the cell size. Terrain is sampled rather than voxelized as geometry, and sampling it as finely as everything else would dominate the bake time of an open world.
### Arguments

- *float* **scale** - The terrain sample scale. The default value is 2.

## float getTerrainSampleScale () const

Returns the current coarseness of terrain sampling relative to the cell size. Terrain is sampled rather than voxelized as geometry, and sampling it as finely as everything else would dominate the bake time of an open world.
### Return value

Current terrain sample scale. The default value is 2.
## void setBakeMask ( int mask )

Sets a new mask that selects which scene geometry the bake takes in. It is what keeps decorative objects out of the navigation mesh and lets several meshes be baked from different parts of the same scene.
### Arguments

- *int* **mask** - The bake mask. The default value is 1.

## int getBakeMask () const

Returns the current mask that selects which scene geometry the bake takes in. It is what keeps decorative objects out of the navigation mesh and lets several meshes be baked from different parts of the same scene.
### Return value

Current bake mask. The default value is 1.
---

## void resetBakeSize ( )

Resets [BakeSize](#BakeSize) to its default value.
## void resetCellSize ( )

Resets [CellSize](#CellSize) to its default value.
## void resetCellHeight ( )

Resets [CellHeight](#CellHeight) to its default value.
## void resetAgentRadius ( )

Resets [AgentRadius](#AgentRadius) to its default value.
## void resetAgentHeight ( )

Resets [AgentHeight](#AgentHeight) to its default value.
## void resetMaxSlopeAngle ( )

Resets [MaxSlopeAngle](#MaxSlopeAngle) to its default value.
## void resetMaxStepHeight ( )

Resets [MaxStepHeight](#MaxStepHeight) to its default value.
## void resetTileResolution ( )

Resets [TileResolution](#TileResolution) to its default value.
## void resetPartitioning ( )

Resets [Partitioning](#Partitioning) to its default value.
## void resetRegionMinSize ( )

Resets [RegionMinSize](#RegionMinSize) to its default value.
## void resetRegionMergeSize ( )

Resets [RegionMergeSize](#RegionMergeSize) to its default value.
## void resetRegionChunkSize ( )

Resets [RegionChunkSize](#RegionChunkSize) to its default value.
## void resetMaxEdgeError ( )

Resets [MaxEdgeError](#MaxEdgeError) to its default value.
## void resetSimplificationElevationRatio ( )

Resets [SimplificationElevationRatio](#SimplificationElevationRatio) to its default value.
## void resetDetailSampleDistance ( )

Resets [DetailSampleDistance](#DetailSampleDistance) to its default value.
## void resetDetailSampleError ( )

Resets [DetailSampleError](#DetailSampleError) to its default value.
## void resetTerrainSampleScale ( )

Resets [TerrainSampleScale](#TerrainSampleScale) to its default value.
## void resetBakeMask ( )

Resets [BakeMask](#BakeMask) to its default value.
