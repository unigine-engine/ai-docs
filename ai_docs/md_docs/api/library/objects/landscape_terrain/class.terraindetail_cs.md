# Unigine.TerrainDetail Class (CS)


This class is used to manage details of the [Landscape Terrain Object](../../../../objects/objects/terrain/landscape_terrain/index.md). Details, define terrain's appearance, each of them can have an unlimited number of children. Details are attached to [detail masks](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md) and are rendered in accordance with their rendering order (the one with the highest order shall be rendered above all others).


## TerrainDetail Class

### Properties

## string Name

The Current name of the detail.
## bool Enabled

The true if the terrain detail is enabled; otherwise, false.
## 🔒︎ bool IsActive

The true if the terrain detail is active; otherwise, false.
## float MinVisibleHeight

The Minimum height value for the detail, in units.
## float MaxVisibleHeight

The Maximum height value for the detail, in units.
## float MinFadeHeight

The Fade in height range value for the detail, in units.
## float MaxFadeHeight

The Fade out height range value for the detail, in units.
## vec4 MaskByAlbedo

The Four-component vector (R, G, B, A) representing a color currently used as a mask for the detail.
## float MaskThreshold

The Current mask threshold value in the [0; 1] range.
## float MaskContrast

The Current mask contrast value in the [0; 1] range.
## TerrainDetailMask DetailMask

The [Detail mask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md) currently used for the detail.
## float MaxFadeTexelSize

The Fade out texel size range value for the detail, in units.
## float MinFadeTexelSize

The Fade in texel size range value for the detail, in units.
## float MaxVisibleTexelSize

The Maximum texel size value for the detail.
## float MinVisibleTexelSize

The Minimum texel size value for the detail.
## Material Material

The detail material used for the detail.
## UGUID MaterialGUID

The [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the material currently used for the detail.
## string MaterialFilePath

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
