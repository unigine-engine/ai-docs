# Unigine.TerrainGlobalLodHeight Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** TerrainGlobalLod


This class is inherited from the [TerrainGlobalLod](../../../api/library/objects/class.terraingloballod_cpp.md) class and used to manage a single height [LOD](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object. Height LODs are used for collision and intersection detection.


## TerrainGlobalLodHeight Class

### Members

---

## void setCastShadows ( int shadows )

Enables or disables casting shadows from non-world lights for the height LOD.
### Arguments

- *int* **shadows** - **1** to enable casting shadows, 0 to disable it.

## int isCastShadows ( )

Returns a value indicating if shadow casting for the height LOD is enabled.
### Return value

**1** if shadow casting for the height LOD is enabled; otherwise, 0.
## void setCollision ( int collision )

Enables or disables collision detection for the height LOD.
### Arguments

- *int* **collision** - **1** to enable collision detection, 0 to disable it.

## int isCollision ( )

Returns a value indicating if collision detection for the height LOD is enabled.
### Return value

**1** if collision detection for the height LOD is enabled; otherwise, 0.
## void setCollisionMask ( int mask )

Sets the collision mask for the height LOD. A collision of an object with the height LOD will be detected, if they both have matching masks.
### Arguments

- *int* **mask** - Collision mask, an integer value each bit of which is a mask.

## int getCollisionMask ( )

Returns the current collision mask for the height LOD. A collision of an object with the height LOD will be detected, if they both have matching masks.
### Return value

Collision mask, an integer value each bit of which is a mask.
## void setIntersection ( int intersection )

Enables or disables intersection detection for the height LOD.
### Arguments

- *int* **intersection** - **1** to enable intersection detection, 0 to disable it.

## int isIntersection ( )

Returns a value indicating if intersection detection for the height LOD is enabled.
### Return value

**1** if intersection detection for the height LOD is enabled; otherwise, 0.
## void setIntersectionMask ( int mask )

Sets the intersection mask for the height LOD. An intersection of an object with the height LOD will be detected, if they both have matching masks.
### Arguments

- *int* **mask** - Intersection mask, an integer value each bit of which is a mask.

## int getIntersectionMask ( )

Returns the current intersection mask for the height LOD. An intersection of an object with the height LOD will be detected, if they both have matching masks.
### Return value

Intersection mask, an integer value each bit of which is a mask.
