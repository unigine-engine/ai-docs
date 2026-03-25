# Unigine.TerrainDetailMask Class (CPP)

**Header:** #include <UnigineObjects.h>


This class is used to manage detail masks of the [Landscape Terrain Object](../../../../objects/objects/terrain/landscape_terrain/index.md). Each detail mask can have an unlimited number of [details](../../../../api/library/objects/landscape_terrain/class.terraindetail_cpp.md), defining its appearance. Detail masks are rendered in accordance with their rendering order (the one with the highest order shall be rendered above all others).


## TerrainDetailMask Class

### Members

---

## void setName ( const char * name )

Sets a new name for the detail mask.
### Arguments

- *const char ** **name** - New terrain detail mask name to be set.

## const char * getName ( )

Returns the name of the detail mask.
### Return value

Current name of the detail mask.
## void setEnabled ( bool enabled )

Sets a value indicating if the terrain detail mask is enabled.
### Arguments

- *bool* **enabled** - true to enable the terrain detail mask, false - to disable it.

## bool isEnabled ( )

Returns a value indicating if the terrain detail mask is enabled.
### Return value

true if the terrain detail mask is enabled; otherwise, false.
## int getRenderOrder ( )

Returns rendering order of the detail mask. Rendering order of masks can be changed via the [*swapRenderOrder()*](#swapRenderOrder_TerrainDetailMask_void)method.
### Return value

Rendering order of the detail mask in the **[0; 19]** range.
## void swapRenderOrder ( const Ptr < TerrainDetailMask > & mask )

Swap rendering order of this detail mask with the specified one.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md)> &* **mask** - Target detail mask.

## Ptr < TerrainDetail > addDetail ( )

Adds a new detail for this mask.
### Return value

New detail added for this mask.
## int getNumDetails ( )

Returns the number of details of this detail mask.
### Return value

Number of details of this detail mask.
## Ptr < TerrainDetail > getDetail ( int num )

Returns a detail by its index.
### Arguments

- *int* **num** - Detail index.

### Return value

Detail with the specified index (if it exists); otherwise, an assertion failure error is reported.
## int isDetail ( const Ptr < TerrainDetail > & detail )

Checks if the specified detail belongs to this detail mask.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_cpp.md)> &* **detail** - Detail to be checked.

### Return value

1 if the specified terrain detail belongs to this mask; otherwise, 0.
## int findDetailIndex ( const char * name )

Returns a detail index by its name.
### Arguments

- *const char ** **name** - Detail name.

### Return value

Index of the detail having the specified name (if it exists); otherwise, -1.
## Ptr < TerrainDetail > findDetail ( const char * name )

Returns a detail attached to the detail mask by its name.
### Arguments

- *const char ** **name** - Detail name.

### Return value

Detail with the specified name (if it exists); otherwise, nullptr.
## void setDetailIndex ( const Ptr < TerrainDetail > & detail , int index )

Replaces a detail with a given index with the specified detail.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_cpp.md)> &* **detail** - Detail to be set instead of the one with the given index.
- *int* **index** - Index of the detail to be replaced with the specified one.

## int getDetailIndex ( const Ptr < TerrainDetail > & detail )

Returns the index of the specified detail.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_cpp.md)> &* **detail** - Detail for which an index is to be found.

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

Sets a new dither amount for the detail mask of the [landscape terrain](../../../../objects/objects/terrain/landscape_terrain/index.md). Dithering enables reduction of graphical artefacts in case of increased Mask Contrast values set for details. This value is multiplied by the [global dither amount](../../../../api/library/rendering/class.render_cpp.md#setLandscapeTerrainMaskDithering_float_void).
### Arguments

- *float* **dithering** - New dither amount to be set for the detail mask in the [0.0f; 1.0f] range.

## float getDithering ( ) const

Returns the current dither amount for the detail mask of the [landscape terrain](../../../../objects/objects/terrain/landscape_terrain/index.md). Dithering enables reduction of graphical artefacts in case of increased Mask Contrast values set for details. This value is multiplied by the [global dither amount](../../../../api/library/rendering/class.render_cpp.md#setLandscapeTerrainMaskDithering_float_void).
### Return value

Current dither amount for the detail mask in the [0.0f; 1.0f] range.
## void setDefaultValue ( float value )

Sets a default (background) value to be used for the mask.
### Arguments

- *float* **value** - Value to be used for the mask as default.

## float getDefaultValue ( ) const

Returns the current default (background) value for the mask.
### Return value

Value currently used for the mask as default.
## void setMaskByAlbedo ( const Math:: vec4 & albedo )

Sets a new albedo color to be used as a mask.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md) &* **albedo** - Albedo color to be used as a mask, as a four-component vector (R,G,B,A)..

## Math:: vec4 getMaskByAlbedo ( ) const

Returns the albedo color currently used as a mask.
### Return value

Albedo color currently used as a mask, as a four-component vector (R,G,B,A).
