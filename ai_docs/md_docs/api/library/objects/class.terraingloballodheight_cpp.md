# Unigine.TerrainGlobalLodHeight Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** TerrainGlobalLod


This class is inherited from the [TerrainGlobalLod](../../../api/library/objects/class.terraingloballod_cpp.md) class and used to manage a single height [LOD](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object. Height LODs are used for collision and intersection detection.


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
## void setCastShadows ( bool shadows )

Sets a new value indicating if shadow casting for the height lod is enabled.
### Arguments

- *bool* **shadows** - value indicating if shadow casting for the height lod is enabled

## bool isCastShadows () const

Returns the current value indicating if shadow casting for the height lod is enabled.
### Return value

value indicating if shadow casting for the height lod is enabled
## void setCollision ( bool collision )

Sets a new value indicating if collision detection for the height lod is enabled.
### Arguments

- *bool* **collision** - value indicating if collision detection for the height lod is enabled

## bool isCollision () const

Returns the current value indicating if collision detection for the height lod is enabled.
### Return value

value indicating if collision detection for the height lod is enabled
## void setIntersection ( bool intersection )

Sets a new value indicating if intersection detection for the height lod is enabled.
### Arguments

- *bool* **intersection** - value indicating if intersection detection for the height lod is enabled

## bool isIntersection () const

Returns the current value indicating if intersection detection for the height lod is enabled.
### Return value

value indicating if intersection detection for the height lod is enabled
