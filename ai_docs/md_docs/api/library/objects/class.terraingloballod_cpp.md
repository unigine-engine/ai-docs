# Unigine.TerrainGlobalLod Class (CPP)

**Header:** #include <UnigineObjects.h>


This class is used to manage a single [LOD](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalLod Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **TERRAIN_GLOBAL_LOD** = 0 | Albedo, normal or detail mask LOD of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object. |
| **TERRAIN_GLOBAL_LOD_HEIGHT** = 1 | [Height LOD](../../../api/library/objects/class.terraingloballodheight_cpp.md) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object. This type of LOD is used for collision and intersection detection. |
| **NUM_TERRAIN_GLOBAL_LODS** = 2 | Total number of LOD types of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) objectю |

### Members

## void setClearDistance ( float distance )

Sets a new clear distance of the lod. starting from this distance the tiles of the lod are removed from memory.
### Arguments

- *float* **distance** - The clear distance of the lod

## float getClearDistance () const

Returns the current clear distance of the lod. starting from this distance the tiles of the lod are removed from memory.
### Return value

Current clear distance of the lod
## void setLoadDistance ( float distance )

Sets a new load distance for the lod. starting from this distance the tiles of the lod are loaded into memory.
### Arguments

- *float* **distance** - The load distance for the lod

## float getLoadDistance () const

Returns the current load distance for the lod. starting from this distance the tiles of the lod are loaded into memory.
### Return value

Current load distance for the lod
## void setVisibleDistance ( float distance )

Sets a new visibility distance. starting from this distance the tiles of the lod become visible.
### Arguments

- *float* **distance** - The visibility distance

## float getVisibleDistance () const

Returns the current visibility distance. starting from this distance the tiles of the lod become visible.
### Return value

Current visibility distance
## void setViewportMask ( int mask )

Sets a new bit mask for rendering into the viewport. the lod is rendered, if its mask matches the player's one.
### Arguments

- *int* **mask** - The bit mask for rendering into the viewport

## int getViewportMask () const

Returns the current bit mask for rendering into the viewport. the lod is rendered, if its mask matches the player's one.
### Return value

Current bit mask for rendering into the viewport
## void setTileDensity ( float density )

Sets a new density of lod tiles.
### Arguments

- *float* **density** - The density of lod tiles

## float getTileDensity () const

Returns the current density of lod tiles.
### Return value

Current density of lod tiles
## void setPath ( const char * path )

Sets a new path to the folder where the lod is stored.
### Arguments

- *const char ** **path** - The path to the folder where the lod is stored

## const char * getPath () const

Returns the current path to the folder where the lod is stored.
### Return value

Current path to the folder where the lod is stored
## void setEnabled ( bool enabled )

Sets a new value indicating if the lod is enabled.
### Arguments

- *bool* **enabled** - value indicating if the lod is enabled

## bool isEnabled () const

Returns the current value indicating if the lod is enabled.
### Return value

value indicating if the lod is enabled
## const char * getTypeName () const

Returns the current Name of the terrain global LOD type. One of the following values:
- TerrainGlobalLod
- TerrainGlobalLodHeight


### Return value

Current Name of the terrain global LOD type
## TerrainGlobalLod::TYPE getType () const

Returns the current LOD type. One of the [TERRAIN_GLOBAL_LOD*](#TERRAIN_GLOBAL_LOD) variables.
### Return value

Current LOD type
---

## Ptr < Tileset > getTileset ( )

Returns the [tileset](../../../api/library/objects/class.tileset_cpp.md) for the LOD.
### Return value

LOD [tileset](../../../api/library/objects/class.tileset_cpp.md).
## int renamePath ( const char * new_path )

Sets a new path to the folder where the LOD is stored.
### Arguments

- *const char ** **new_path** - New path to be set.

### Return value

**1** if the new path was set successfully; otherwise, 0.
## void reload ( )

Reloads the LOD.
