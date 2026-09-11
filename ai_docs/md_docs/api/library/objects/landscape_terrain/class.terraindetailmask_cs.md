# Unigine.TerrainDetailMask Class (CS)


This class is used to manage detail masks of the [Landscape Terrain Object](../../../../objects/objects/terrain/landscape_terrain/index.md). Each detail mask can have an unlimited number of [details](../../../../api/library/objects/landscape_terrain/class.terraindetail_cs.md), defining its appearance. Detail masks are rendered in accordance with their rendering order (the one with the highest order shall be rendered above all others).


## TerrainDetailMask Class

### Properties

## string Name

The name of the detail mask.
## bool Enabled

The value indicating if the terrain detail mask is enabled.
## 🔒︎ int RenderOrder

The rendering order of the detail mask in the [0; 19] range. Rendering order of masks can be changed via the [*swapRenderOrder()*](#swapRenderOrder_TerrainDetailMask_void) method.
## 🔒︎ int NumDetails

The number of details of this detail mask.
## 🔒︎ int Index

The index of the detail mask in the [0; 19] range.
## float Dithering

The dither amount for the detail mask of the [landscape terrain](../../../../objects/objects/terrain/landscape_terrain/index.md), in the [0.0f; 1.0f] range. Dithering enables reduction of graphical artefacts in case of increased Mask Contrast values set for details. This value is multiplied by the [global dither amount](../../../../api/library/rendering/class.render_cs.md#setLandscapeTerrainMaskDithering_float_void).
## vec4 MaskByAlbedo

The albedo color used as a mask, as a four-component vector (R,G,B,A).
## bool ExperimentalNavigation

The value indicating if the terrain covered by this detail mask is taken in when an [ExperimentalNavigationMesh](../../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md) is baked. It is how a landscape is made walkable selectively � grass and sand yes, cliffs and lava no � without any extra geometry.
## int ExperimentalNavigationArea

The area stamped onto the navigation mesh polygons baked from the terrain this mask covers. The name, cost, and flags behind the index come from the registry of the [ExperimentalNavigation](../../../../api/library/pathfinding/class.experimentalnavigation_cs.md) singleton, so a swamp mask can be made expensive to cross by setting the cost once.
## int ExperimentalNavigationBakeMask

The [Bake mask](../../../../principles/bit_masking/index.md#bake_mask) of the detail mask. The terrain it covers is taken in only by the navigation meshes whose own bake mask shares at least one bit with this one.
## float ExperimentalNavigationMinValue

The weakest value of the detail mask that still counts as navigable terrain. A detail mask fades out at its edges, and this threshold decides where the walkable surface ends: raising it pulls the navigable area towards the centre of the painted region, lowering it lets faint traces of the mask count.
## float DefaultValue

The Value currently used for the mask as default.
### Members

---

## void SwapRenderOrder ( TerrainDetailMask mask )

Swap rendering order of this detail mask with the specified one.
### Arguments

- *[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md)* **mask** - Target detail mask.

## TerrainDetail AddDetail ( )

Adds a new detail for this mask.
### Return value

New detail added for this mask.
## TerrainDetail GetDetail ( int num )

Returns a detail by its index.
### Arguments

- *int* **num** - Detail index.

### Return value

Detail with the specified index (if it exists); otherwise, an assertion failure error is reported.
## int IsDetail ( TerrainDetail detail )

Checks if the specified detail belongs to this detail mask.
### Arguments

- *[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_cs.md)* **detail** - Detail to be checked.

### Return value

1 if the specified terrain detail belongs to this mask; otherwise, 0.
## int FindDetailIndex ( string name )

Returns a detail index by its name.
### Arguments

- *string* **name** - Detail name.

### Return value

Index of the detail having the specified name (if it exists); otherwise, -1.
## TerrainDetail FindDetail ( string name )

Returns a detail attached to the detail mask by its name.
### Arguments

- *string* **name** - Detail name.

### Return value

Detail with the specified name (if it exists); otherwise, NULL.
## void SetDetailIndex ( TerrainDetail detail , int index )

Replaces a detail with a given index with the specified detail.
### Arguments

- *[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_cs.md)* **detail** - Detail to be set instead of the one with the given index.
- *int* **index** - Index of the detail to be replaced with the specified one.

## int GetDetailIndex ( TerrainDetail detail )

Returns the index of the specified detail.
### Arguments

- *[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_cs.md)* **detail** - Detail for which an index is to be found.

### Return value

Index of the specified detail (if it exists); otherwise, -1.
## void SwapDetail ( int num_0 , int num_1 )

Swaps the two details with given indices.
### Arguments

- *int* **num_0** - First detail index.
- *int* **num_1** - Second detail index.
