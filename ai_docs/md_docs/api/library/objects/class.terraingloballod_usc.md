# Unigine.TerrainGlobalLod Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage a single [LOD](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalLod Class

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
## void setPath ( string path )

Sets a new path to the folder where the lod is stored.
### Arguments

- *string* **path** - The path to the folder where the lod is stored

## const char * getPath () const

Returns the current path to the folder where the lod is stored.
### Return value

Current path to the folder where the lod is stored
## void setEnabled ( int enabled )

Sets a new value indicating if the lod is enabled.
### Arguments

- *int* **enabled** - The value indicating if the lod is enabled

## int isEnabled () const

Returns the current value indicating if the lod is enabled.
### Return value

Current value indicating if the lod is enabled
## const char * getTypeName () const

Returns the current Name of the terrain global LOD type. One of the following values:
- TerrainGlobalLod
- TerrainGlobalLodHeight


### Return value

Current Name of the terrain global LOD type
## int getType () const

Returns the current LOD type. One of the [TERRAIN_GLOBAL_LOD*](#TERRAIN_GLOBAL_LOD) variables.
### Return value

Current LOD type
---

## Tileset getTileset ( )

Returns the [tileset](../../../api/library/objects/class.tileset_usc.md) for the LOD.
### Return value

LOD [tileset](../../../api/library/objects/class.tileset_usc.md).
## int renamePath ( string new_path )

Sets a new path to the folder where the LOD is stored.
### Arguments

- *string* **new_path** - New path to be set.

### Return value

**1** if the new path was set successfully; otherwise, 0.
## void reload ( )

Reloads the LOD.
