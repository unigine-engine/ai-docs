# Unigine::ExperimentalNavigationBakeSettings Class (CS)


Everything a navigation mesh is built with: the size of a voxel, the agent the surface is carved for, how tiles are cut, and how far the result is simplified. The settings describe the bake that is going to happen, not the data already loaded. What the loaded data was actually built with is reported by the **Data** properties of [ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md), and editing a setting never changes them on its own.


The object is not created directly. Both navigation mesh nodes own one and hand it out: [ExperimentalNavigationMesh.BakeSettings](../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md#BakeSettings) and [NavigationMesh.BakeSettings](../../../api/library/pathfinding/class.navigationmesh_cs.md#BakeSettings). That is why a single editor panel configures both, and why the settings survive as long as the node.


Each setting has a matching reset function instead of a documented default constant. Baking is started through the [ExperimentalBakeNavigation](../../../api/library/pathfinding/class.experimentalbakenavigation_cs.md) singleton.


> **Notice:** Settings are read when a bake starts and are snapshotted for its whole run, so changing them while a bake is in flight affects the next bake, not the current one.


## ExperimentalNavigationBakeSettings Class

### Enums

## PARTITIONING

| Name | Description |
|---|---|
| **WATERSHED** = 0 | The slowest partitioning and the one that yields the best-shaped polygons. The right choice for a mesh baked once ahead of time. |
| **MONOTONE** = 1 | A fast partitioning that never leaves holes, but tends to produce long thin polygons. A reasonable middle ground when bake time matters. |
| **CHUNKY** = 2 | The surface is cut into fixed chunks. The fastest option and the one to use when tiles are rebuilt at runtime, at the price of the coarsest polygons. |

### Properties

## vec3 BakeSize

The dimensions of the region around the node that the bake covers.
## float CellSize

The horizontal size of a voxel. It is the main quality-against-cost knob of the bake: halving it quadruples both the detail and the memory the voxelization takes.
## float CellHeight

The vertical size of a voxel. It sets how precisely heights are resolved during the bake, and with them the smallest step or ledge that can be detected.
## float AgentRadius

The radius of the agent the mesh is baked for. The walkable surface is pulled back from every wall by this distance, so an agent following the mesh never clips one.
## float AgentHeight

The height of the agent the mesh is baked for. Anything with less headroom than this is left out of the walkable surface.
## float MaxSlopeAngle

The steepest slope an agent is considered able to walk up. Everything steeper is left out of the walkable surface. It is a property of the bake, not of an individual agent � agents with different climbing ability need separate meshes.
## float MaxStepHeight

The tallest step an agent can climb without a ramp. Surfaces separated by less than this are joined into one walkable region, which is what makes staircases and kerbs passable.
## int TileResolution

The width of a tile in cells. Together with the cell size it fixes how large a tile is in the world, and with it the granularity of streaming and of rebuilds: smaller tiles are cheaper to rebuild one at a time but produce more seams.
## ExperimentalNavigationBakeSettings.PARTITIONING Partitioning

The algorithm that splits the walkable surface into regions before it is turned into polygons. It trades bake time against the quality of the resulting polygons.
## float RegionMinSize

The size below which an isolated region is discarded. It removes the specks of walkable surface that appear on top of furniture and ledges, which no agent could reach anyway.
## float RegionMergeSize

The size below which a region is merged into a larger neighbour instead of being kept on its own. It cuts down the polygon count without losing walkable space.
## int RegionChunkSize

The size of a chunk used by chunky partitioning. Only meaningful when [Partitioning](#Partitioning) is [PARTITIONING_CHUNKY](#PARTITIONING_CHUNKY).
## float MaxEdgeError

The largest deviation allowed when the outline of a region is simplified into polygon edges. Higher values give fewer, coarser polygons.
## float SimplificationElevationRatio

The how strongly edge simplification is held back where the surface changes height. Raising it keeps more detail on slopes and stairs while flat ground stays coarse.
## float DetailSampleDistance

The spacing at which the detail mesh samples the underlying surface. The detail mesh is what makes the navigation mesh follow the height of uneven ground instead of floating flat above it.
## float DetailSampleError

The largest vertical deviation the detail mesh may have from the real surface. Raising it produces fewer triangles and a navigation mesh that follows the ground more loosely.
## float TerrainSampleScale

The coarseness of terrain sampling relative to the cell size. Terrain is sampled rather than voxelized as geometry, and sampling it as finely as everything else would dominate the bake time of an open world.
## int BakeMask

The mask that selects which scene geometry the bake takes in. It is what keeps decorative objects out of the navigation mesh and lets several meshes be baked from different parts of the same scene.
### Members

---

## void ResetBakeSize ( )

Resets [BakeSize](#BakeSize) to its default value.
## void ResetCellSize ( )

Resets [CellSize](#CellSize) to its default value.
## void ResetCellHeight ( )

Resets [CellHeight](#CellHeight) to its default value.
## void ResetAgentRadius ( )

Resets [AgentRadius](#AgentRadius) to its default value.
## void ResetAgentHeight ( )

Resets [AgentHeight](#AgentHeight) to its default value.
## void ResetMaxSlopeAngle ( )

Resets [MaxSlopeAngle](#MaxSlopeAngle) to its default value.
## void ResetMaxStepHeight ( )

Resets [MaxStepHeight](#MaxStepHeight) to its default value.
## void ResetTileResolution ( )

Resets [TileResolution](#TileResolution) to its default value.
## void ResetPartitioning ( )

Resets [Partitioning](#Partitioning) to its default value.
## void ResetRegionMinSize ( )

Resets [RegionMinSize](#RegionMinSize) to its default value.
## void ResetRegionMergeSize ( )

Resets [RegionMergeSize](#RegionMergeSize) to its default value.
## void ResetRegionChunkSize ( )

Resets [RegionChunkSize](#RegionChunkSize) to its default value.
## void ResetMaxEdgeError ( )

Resets [MaxEdgeError](#MaxEdgeError) to its default value.
## void ResetSimplificationElevationRatio ( )

Resets [SimplificationElevationRatio](#SimplificationElevationRatio) to its default value.
## void ResetDetailSampleDistance ( )

Resets [DetailSampleDistance](#DetailSampleDistance) to its default value.
## void ResetDetailSampleError ( )

Resets [DetailSampleError](#DetailSampleError) to its default value.
## void ResetTerrainSampleScale ( )

Resets [TerrainSampleScale](#TerrainSampleScale) to its default value.
## void ResetBakeMask ( )

Resets [BakeMask](#BakeMask) to its default value.
