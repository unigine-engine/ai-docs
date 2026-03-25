# Unigine.TerrainGlobalLod Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage a single [LOD](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalLod Class

### Members

---

## void setClearDistance ( float distance )

Sets the clear distance of the LOD. Starting from this distance the tiles of the LOD are removed from memory.
### Arguments

- *float* **distance** - Clear distance, in units.

## float getClearDistance ( )

Returns the clear distance of the LOD. Starting from this distance the tiles of the LOD are removed from memory.
### Return value

Current clear distance, in units.
## void setEnabled ( int enabled )

Enables or disables the LOD.
### Arguments

- *int* **enabled** - **1** to enable the LOD, 0 to disable it.

## int isEnabled ( )

Returns a value indicating if the LOD is enabled.
### Return value

**1** if the LOD is enabled; otherwise, 0.
## void setLoadDistance ( float distance )

Sets the load distance for the LOD. Starting from this distance the tiles of the LOD are loaded into memory.
### Arguments

- *float* **distance** - Load distance, in units.

## float getLoadDistance ( )

Returns the current load distance for the LOD. Starting from this distance the tiles of the LOD are loaded into memory.
### Return value

Current load distance, in units.
## void setPath ( string path )

Sets the path to the folder where the LOD is stored.
### Arguments

- *string* **path** - Path to the folder where the LOD is stored.

## string getPath ( )

Returns the path to the folder where the LOD is stored.
### Return value

Path to the folder where the LOD is stored.
## void setTileDensity ( float density )

Sets the density of LOD tiles.
### Arguments

- *float* **density** - LOD tile density, in meters per pixel.

## float getTileDensity ( )

Returns the current density of LOD tiles.
### Return value

Current LOD tile density, in meters per pixel.
## Tileset getTileset ( )

Returns the [tileset](../../../api/library/objects/class.tileset_usc.md) for the LOD.
### Return value

LOD [tileset](../../../api/library/objects/class.tileset_usc.md).
## void setViewportMask ( int mask )

Sets the bit mask for rendering into the viewport. The LOD is rendered, if its mask matches the player's one.
### Arguments

- *int* **mask** - Viewport mask, an integer value each bit of which is a mask.

## int getViewportMask ( )

Returns the current bit mask for rendering into the viewport. The LOD is rendered, if its mask matches the player's one.
### Return value

Viewport mask, an integer value each bit of which is a mask.
## void setVisibleDistance ( float distance )

Sets the visibility distance. Starting from this distance the tiles of the LOD become visible.
### Arguments

- *float* **distance** - Visibility distance, in units.

## float getVisibleDistance ( )

Returns the current visibility distance. Starting from this distance the tiles of the LOD become visible.
### Return value

Current visibility distance, in units.
## int renamePath ( string new_path )

Sets a new path to the folder where the LOD is stored.
### Arguments

- *string* **new_path** - New path to be set.

### Return value

**1** if the new path was set successfully; otherwise, 0.
## void reload ( )

Reloads the LOD.
## int getType ( )

Returns the type of the LOD. This method is used to define whether it is a height LOD used for collision and intersection detection or an ordinary albedo, normal or detail mask LOD.
### Return value

LOD type, one of the [TERRAIN_GLOBAL_LOD*](#TERRAIN_GLOBAL_LOD) values.
## string getTypeName ( )

Returns the name of the terrain global LOD type. This method is used to define whether it is a height LOD used for collision and intersection detection or an ordinary albedo, normal or detail mask LOD.
### Return value

Name of the terrain global LOD type. One of the following values:
- TerrainGlobalLod
- TerrainGlobalLodHeight
