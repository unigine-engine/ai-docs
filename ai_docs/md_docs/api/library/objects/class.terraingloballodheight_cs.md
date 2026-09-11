# Unigine.TerrainGlobalLodHeight Class (CS)

**Inherits from:** TerrainGlobalLod


This class is inherited from the [TerrainGlobalLod](../../../api/library/objects/class.terraingloballod_cs.md) class and used to manage a single height [LOD](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object. Height LODs are used for collision and intersection detection.


## TerrainGlobalLodHeight Class

### Properties

## int CollisionMask

The collision mask for the height lod, an integer value each bit of which is a mask. a collision of an object with the height lod will be detected, if they both have matching masks.
## int IntersectionMask

The intersection mask for the height lod, an integer value each bit of which is a mask. an intersection of an object with the height lod will be detected, if they both have matching masks.
## bool CastShadows

The value indicating if shadow casting for the height lod is enabled.
## bool Collision

The value indicating if collision detection for the height lod is enabled.
## bool Intersection

The value indicating if intersection detection for the height lod is enabled.
