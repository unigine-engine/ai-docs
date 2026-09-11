# Unigine.TerrainDetail Class (CS)


This class is used to manage details of the [Landscape Terrain Object](../../../../objects/objects/terrain/landscape_terrain/index.md). Details, define terrain's appearance, each of them can have an unlimited number of children. Details are attached to [detail masks](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md) and are rendered in accordance with their rendering order (the one with the highest order shall be rendered above all others).


## TerrainDetail Class

### Properties

## string Name

The name of the detail.
## bool Enabled

The value indicating if the terrain detail is enabled.
## 🔒︎ bool IsActive

The value indicating if the terrain detail is active.
## float MinVisibleHeight

The minimum height value for the detail, in units, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by height. The default value is -inf.
## float MaxVisibleHeight

The maximum height value for the detail, in units.
## float MinFadeHeight

The fade in height range value for the detail, in units. Over this height range below the [minimum height value](#setMinVisibleHeight_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
## float MaxFadeHeight

The fade out height range value for the detail, in units. Over this height range below the [maximum height value](#setMaxVisibleHeight_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
## vec4 MaskByAlbedo

The four-component vector (R, G, B, A) representing a color used as a mask for the detail. In this case, all areas on the terrain having selected color will be covered by the detail.
## float MaskThreshold

The mask threshold value in the [0; 1] range. Control blending of the detail according to the mask. The Threshold parameter controls the spread intensity of the layer. Lower values provide bigger spread.
## float MaskContrast

The mask contrast value in the [0; 1] range.
## TerrainDetailMask DetailMask

The [detail mask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md) used for the detail.
## float MaxFadeTexelSize

The fade out texel size range value for the detail, in units. Over this range below the [maximum texel size value](#setMaxVisibleTexelSize_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by texel size.
## float MinFadeTexelSize

The fade in texel size range value for the detail, in units. Over this range below the [minimum texel size value](#setMinVisibleTexelSize_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by texel size.
## float MaxVisibleTexelSize

The maximum texel size value for the detail.
## float MinVisibleTexelSize

The minimum texel size value for the detail.
## Material Material

The detail material used for the detail.
## UGUID MaterialGUID

The [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the material currently used for the detail.
## String MaterialFilePath

The path of the material file currently used for the detail.
### Members

---

## TerrainDetail Copy ( TerrainDetail dest_detail )

Copies the detail to the specified destination detail (with all its children).
### Arguments

- *[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_cs.md)* **dest_detail** - Destination detail to which the detail is to be copied.

### Return value

Destination detail.
## TerrainDetail Clone ( )

Clones the terrain detail (with all its children).
### Return value

Cloned detail.
