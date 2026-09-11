# Unigine.TerrainGlobalLod Class (CS)


This class is used to manage a single [LOD](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalLod Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **TERRAIN_GLOBAL_LOD** = 0 | Albedo, normal or detail mask LOD of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object. |
| **TERRAIN_GLOBAL_LOD_HEIGHT** = 1 | [Height LOD](../../../api/library/objects/class.terraingloballodheight_cs.md) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object. This type of LOD is used for collision and intersection detection. |
| **NUM_TERRAIN_GLOBAL_LODS** = 2 | Total number of LOD types of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) objectю |

### Properties

## float ClearDistance

The clear distance of the lod. starting from this distance the tiles of the lod are removed from memory.
## float LoadDistance

The load distance for the lod. starting from this distance the tiles of the lod are loaded into memory.
## float VisibleDistance

The visibility distance. starting from this distance the tiles of the lod become visible.
## int ViewportMask

The bit mask for rendering into the viewport. the lod is rendered, if its mask matches the player's one.
## float TileDensity

The density of lod tiles.
## string Path

The path to the folder where the lod is stored.
## bool Enabled

The value indicating if the lod is enabled.
## 🔒︎ string TypeName

The Name of the terrain global LOD type. One of the following values:
- TerrainGlobalLod
- TerrainGlobalLodHeight


## 🔒︎ TerrainGlobalLod.TYPE Type

The LOD type. One of the [TERRAIN_GLOBAL_LOD*](#TERRAIN_GLOBAL_LOD) variables.
### Members

---

## Tileset GetTileset ( )

Returns the [tileset](../../../api/library/objects/class.tileset_cs.md) for the LOD.
### Return value

LOD [tileset](../../../api/library/objects/class.tileset_cs.md).
## int RenamePath ( string new_path )

Sets a new path to the folder where the LOD is stored.
### Arguments

- *string* **new_path** - New path to be set.

### Return value

**1** if the new path was set successfully; otherwise, 0.
## void Reload ( )

Reloads the LOD.
