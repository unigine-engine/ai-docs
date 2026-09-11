# Unigine.TerrainGlobalLodHeight Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** TerrainGlobalLod


This class is inherited from the [TerrainGlobalLod](../../../api/library/objects/class.terraingloballod_usc.md) class and used to manage a single height [LOD](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object. Height LODs are used for collision and intersection detection.


## TerrainGlobalLodHeight Class

### Members

## void setCollisionMask ( int mask )

Sets a new collision mask for the height lod, an integer value each bit of which is a mask. a collision of an object with the height lod will be detected, if they both have matching masks.
### Arguments

- *int* **mask** - The collision mask for the height lod

## int getCollisionMask () const

Returns the current collision mask for the height lod, an integer value each bit of which is a mask. a collision of an object with the height lod will be detected, if they both have matching masks.
### Return value

Current collision mask for the height lod
## void setIntersectionMask ( int mask )

Sets a new intersection mask for the height lod, an integer value each bit of which is a mask. an intersection of an object with the height lod will be detected, if they both have matching masks.
### Arguments

- *int* **mask** - The intersection mask for the height lod

## int getIntersectionMask () const

Returns the current intersection mask for the height lod, an integer value each bit of which is a mask. an intersection of an object with the height lod will be detected, if they both have matching masks.
### Return value

Current intersection mask for the height lod
## void setCastShadows ( int shadows )

Sets a new value indicating if shadow casting for the height lod is enabled.
### Arguments

- *int* **shadows** - The value indicating if shadow casting for the height lod is enabled

## int isCastShadows () const

Returns the current value indicating if shadow casting for the height lod is enabled.
### Return value

Current value indicating if shadow casting for the height lod is enabled
## void setCollision ( int collision )

Sets a new value indicating if collision detection for the height lod is enabled.
### Arguments

- *int* **collision** - The value indicating if collision detection for the height lod is enabled

## int isCollision () const

Returns the current value indicating if collision detection for the height lod is enabled.
### Return value

Current value indicating if collision detection for the height lod is enabled
## void setIntersection ( int intersection )

Sets a new value indicating if intersection detection for the height lod is enabled.
### Arguments

- *int* **intersection** - The value indicating if intersection detection for the height lod is enabled

## int isIntersection () const

Returns the current value indicating if intersection detection for the height lod is enabled.
### Return value

Current value indicating if intersection detection for the height lod is enabled
