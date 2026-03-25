# Unigine.TerrainDetailMask Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage detail masks of the [Landscape Terrain Object](../../../../objects/objects/terrain/landscape_terrain/index.md). Each detail mask can have an unlimited number of [details](../../../../api/library/objects/landscape_terrain/class.terraindetail_usc.md), defining its appearance. Detail masks are rendered in accordance with their rendering order (the one with the highest order shall be rendered above all others).


## TerrainDetailMask Class

### Members

---

## void setName ( string name )

Sets a new name for the detail mask.
### Arguments

- *string* **name** - New terrain detail mask name to be set.

## string getName ( )

Returns the name of the detail mask.
### Return value

Current name of the detail mask.
## void setEnabled ( int enabled )

Sets a value indicating if the terrain detail mask is enabled.
### Arguments

- *int* **enabled** - **1** to enable the terrain detail mask, **0** - to disable it.

## int isEnabled ( )

Returns a value indicating if the terrain detail mask is enabled.
### Return value

**1** if the terrain detail mask is enabled; otherwise, **0**.
## int getRenderOrder ( )

Returns rendering order of the detail mask. Rendering order of masks can be changed via the [*swapRenderOrder()*](#swapRenderOrder_TerrainDetailMask_void)method.
### Return value

Rendering order of the detail mask in the **[0; 19]** range.
## void swapRenderOrder ( TerrainDetailMask mask )

Swap rendering order of this detail mask with the specified one.
### Arguments

- *[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_usc.md)* **mask** - Target detail mask.

## TerrainDetail addDetail ( )

Adds a new detail for this mask.
### Return value

New detail added for this mask.
## int getNumDetails ( )

Returns the number of details of this detail mask.
### Return value

Number of details of this detail mask.
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

## int getIndex ( )

Returns the index of the detail mask.
### Return value

Index of the detail mask in the **[0; 19]** range.
## void setDithering ( float dithering )

Sets a new dither amount for the detail mask of the [landscape terrain](../../../../objects/objects/terrain/landscape_terrain/index.md). Dithering enables reduction of graphical artefacts in case of increased Mask Contrast values set for details. This value is multiplied by the [global dither amount](../../../../api/library/rendering/class.render_usc.md#setLandscapeTerrainMaskDithering_float_void).
### Arguments

- *float* **dithering** - New dither amount to be set for the detail mask in the [0.0f; 1.0f] range.

## float getDithering ( )

Returns the current dither amount for the detail mask of the [landscape terrain](../../../../objects/objects/terrain/landscape_terrain/index.md). Dithering enables reduction of graphical artefacts in case of increased Mask Contrast values set for details. This value is multiplied by the [global dither amount](../../../../api/library/rendering/class.render_usc.md#setLandscapeTerrainMaskDithering_float_void).
### Return value

Current dither amount for the detail mask in the [0.0f; 1.0f] range.
## void setDefaultValue ( float value )

Sets a default (background) value to be used for the mask.
### Arguments

- *float* **value** - Value to be used for the mask as default.

## float getDefaultValue ( )

Returns the current default (background) value for the mask.
### Return value

Value currently used for the mask as default.
## void setMaskByAlbedo ( vec4 albedo )

Sets a new albedo color to be used as a mask.
### Arguments

- *vec4* **albedo** - Albedo color to be used as a mask, as a four-component vector (R,G,B,A)..

## vec4 getMaskByAlbedo ( )

Returns the albedo color currently used as a mask.
### Return value

Albedo color currently used as a mask, as a four-component vector (R,G,B,A).
