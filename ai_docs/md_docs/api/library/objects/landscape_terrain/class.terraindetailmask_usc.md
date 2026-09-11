# Unigine.TerrainDetailMask Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage detail masks of the [Landscape Terrain Object](../../../../objects/objects/terrain/landscape_terrain/index.md). Each detail mask can have an unlimited number of [details](../../../../api/library/objects/landscape_terrain/class.terraindetail_usc.md), defining its appearance. Detail masks are rendered in accordance with their rendering order (the one with the highest order shall be rendered above all others).


## TerrainDetailMask Class

### Members

## void setName ( string name )

Sets a new name of the detail mask.
### Arguments

- *string* **name** - The name of the detail mask

## const char * getName () const

Returns the current name of the detail mask.
### Return value

Current name of the detail mask
## void setEnabled ( int enabled )

Sets a new value indicating if the terrain detail mask is enabled.
### Arguments

- *int* **enabled** - The value indicating if the terrain detail mask is enabled

## int isEnabled () const

Returns the current value indicating if the terrain detail mask is enabled.
### Return value

Current value indicating if the terrain detail mask is enabled
## int getRenderOrder () const

Returns the current rendering order of the detail mask in the [0; 19] range. Rendering order of masks can be changed via the [*swapRenderOrder()*](#swapRenderOrder_TerrainDetailMask_void) method.
### Return value

Current rendering order of the detail mask in the [0; 19] range
## int getNumDetails () const

Returns the current number of details of this detail mask.
### Return value

Current number of details of this detail mask
## int getIndex () const

Returns the current index of the detail mask in the [0; 19] range.
### Return value

Current index of the detail mask in the [0; 19] range
## void setDithering ( float dithering )

Sets a new dither amount for the detail mask of the [landscape terrain](../../../../objects/objects/terrain/landscape_terrain/index.md), in the [0.0f; 1.0f] range. Dithering enables reduction of graphical artefacts in case of increased Mask Contrast values set for details. This value is multiplied by the [global dither amount](../../../../api/library/rendering/class.render_usc.md#setLandscapeTerrainMaskDithering_float_void).
### Arguments

- *float* **dithering** - The dither amount for the detail mask of the landscape terrain

## float getDithering () const

Returns the current dither amount for the detail mask of the [landscape terrain](../../../../objects/objects/terrain/landscape_terrain/index.md), in the [0.0f; 1.0f] range. Dithering enables reduction of graphical artefacts in case of increased Mask Contrast values set for details. This value is multiplied by the [global dither amount](../../../../api/library/rendering/class.render_usc.md#setLandscapeTerrainMaskDithering_float_void).
### Return value

Current dither amount for the detail mask of the landscape terrain
## void setMaskByAlbedo ( vec4 albedo )

Sets a new albedo color used as a mask, as a four-component vector (R,G,B,A).
### Arguments

- *vec4* **albedo** - The albedo color used as a mask, as a four-component vector (R,G,B,A)

## vec4 getMaskByAlbedo () const

Returns the current albedo color used as a mask, as a four-component vector (R,G,B,A).
### Return value

Current albedo color used as a mask, as a four-component vector (R,G,B,A)
## void setExperimentalNavigation ( int navigation )

Sets a new value indicating if the terrain covered by this detail mask is taken in when an [ExperimentalNavigationMesh](../../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md) is baked. It is how a landscape is made walkable selectively � grass and sand yes, cliffs and lava no � without any extra geometry.
### Arguments

- *int* **navigation** - The navigation markup for the terrain the mask covers

## int isExperimentalNavigation () const

Returns the current value indicating if the terrain covered by this detail mask is taken in when an [ExperimentalNavigationMesh](../../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md) is baked. It is how a landscape is made walkable selectively � grass and sand yes, cliffs and lava no � without any extra geometry.
### Return value

Current navigation markup for the terrain the mask covers
## void setExperimentalNavigationArea ( int area )

Sets a new area stamped onto the navigation mesh polygons baked from the terrain this mask covers. The name, cost, and flags behind the index come from the registry of the [ExperimentalNavigation](../../../../api/library/pathfinding/class.experimentalnavigation_usc.md) singleton, so a swamp mask can be made expensive to cross by setting the cost once.
### Arguments

- *int* **area** - The area index. The default value is 63.

## int getExperimentalNavigationArea () const

Returns the current area stamped onto the navigation mesh polygons baked from the terrain this mask covers. The name, cost, and flags behind the index come from the registry of the [ExperimentalNavigation](../../../../api/library/pathfinding/class.experimentalnavigation_usc.md) singleton, so a swamp mask can be made expensive to cross by setting the cost once.
### Return value

Current area index. The default value is 63.
## void setExperimentalNavigationBakeMask ( int mask )

Sets a new [Bake mask](../../../../principles/bit_masking/index.md#bake_mask) of the detail mask. The terrain it covers is taken in only by the navigation meshes whose own bake mask shares at least one bit with this one.
### Arguments

- *int* **mask** - The bake mask. The default value is 1.

## int getExperimentalNavigationBakeMask () const

Returns the current [Bake mask](../../../../principles/bit_masking/index.md#bake_mask) of the detail mask. The terrain it covers is taken in only by the navigation meshes whose own bake mask shares at least one bit with this one.
### Return value

Current bake mask. The default value is 1.
## void setExperimentalNavigationMinValue ( float value )

Sets a new weakest value of the detail mask that still counts as navigable terrain. A detail mask fades out at its edges, and this threshold decides where the walkable surface ends: raising it pulls the navigable area towards the centre of the painted region, lowering it lets faint traces of the mask count.
### Arguments

- *float* **value** - The threshold value. Negative values are clamped to 0. The default value is 0.5.

## float getExperimentalNavigationMinValue () const

Returns the current weakest value of the detail mask that still counts as navigable terrain. A detail mask fades out at its edges, and this threshold decides where the walkable surface ends: raising it pulls the navigable area towards the centre of the painted region, lowering it lets faint traces of the mask count.
### Return value

Current threshold value. Negative values are clamped to 0. The default value is 0.5.
## void setDefaultValue ( float value )

Sets a new Value currently used for the mask as default.
### Arguments

- *float* **value** - The Value currently used for the mask as default

## float getDefaultValue () const

Returns the current Value currently used for the mask as default.
### Return value

Current Value currently used for the mask as default
---

## void swapRenderOrder ( TerrainDetailMask mask )

Swap rendering order of this detail mask with the specified one.
### Arguments

- *[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_usc.md)* **mask** - Target detail mask.

## TerrainDetail addDetail ( )

Adds a new detail for this mask.
### Return value

New detail added for this mask.
## TerrainDetail getDetail ( int num )

Returns a detail by its index.
### Arguments

- *int* **num** - Detail index.

### Return value

Detail with the specified index (if it exists); otherwise, an assertion failure error is reported.
## int isDetail ( TerrainDetail detail )

Checks if the specified detail belongs to this detail mask.
### Arguments

- *[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_usc.md)* **detail** - Detail to be checked.

### Return value

1 if the specified terrain detail belongs to this mask; otherwise, 0.
## int findDetailIndex ( string name )

Returns a detail index by its name.
### Arguments

- *string* **name** - Detail name.

### Return value

Index of the detail having the specified name (if it exists); otherwise, -1.
## TerrainDetail findDetail ( string name )

Returns a detail attached to the detail mask by its name.
### Arguments

- *string* **name** - Detail name.

### Return value

Detail with the specified name (if it exists); otherwise, NULL.
## void setDetailIndex ( TerrainDetail detail , int index )

Replaces a detail with a given index with the specified detail.
### Arguments

- *[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_usc.md)* **detail** - Detail to be set instead of the one with the given index.
- *int* **index** - Index of the detail to be replaced with the specified one.

## int getDetailIndex ( TerrainDetail detail )

Returns the index of the specified detail.
### Arguments

- *[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_usc.md)* **detail** - Detail for which an index is to be found.

### Return value

Index of the specified detail (if it exists); otherwise, -1.
## void swapDetail ( int num_0 , int num_1 )

Swaps the two details with given indices.
### Arguments

- *int* **num_0** - First detail index.
- *int* **num_1** - Second detail index.
