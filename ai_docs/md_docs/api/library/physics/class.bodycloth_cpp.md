# Unigine::BodyCloth Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** BodyParticles


This class is used to simulate a flat deformable [cloth bodies](../../../principles/physics/bodies/cloth/index.md). They use a [mass-spring simulation model](../../../principles/physics/bodies/cloth/index.md#model): the cloth is formed from [particles](../../../api/library/physics/class.bodyparticles_cpp.md) (of sphere shape) that are located in the cloth mesh vertices and connected by inner joints.


### See Also


- The [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_cpp.md) usage example demonstrating how to create an object, assign a cloth body to it, and set its parameters
- UnigineScript samples:

  -
  -
  -
  -
  -
  -
  -
  -
  -


## BodyCloth Class

### Members

---

## static BodyClothPtr create ( )

Constructor. Creates a cloth body with default properties.
## static BodyClothPtr create ( const Ptr < Object > & object )

Constructor. Creates a cloth body with default properties for a given object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object represented with the new cloth body.

## int getNumIndices ( )

Returns the number of particle indices.
### Return value

Number of particle indices.
## int getParticleIndex ( int num )

Returns the particle index by its number.
### Arguments

- *int* **num** - The particle index number.

### Return value

The particle index.
## void setTwoSided ( int sided )

Set a value indicating if the cloth is one- or two-sided. (If two-sided, its material should not be [two-sided](../../../api/library/rendering/class.material_cpp.md#setTwoSided_int_void) at the same time).
### Arguments

- *int* **sided** - Positive value, if the cloth should be two-sided; **0** if one-sided.

## int getTwoSided ( )

Returns a value indicating if the cloth is one- or two-sided. (If two-sided, its material should not be [two-sided](../../../api/library/rendering/class.material_cpp.md#setTwoSided_int_void) at the same time).
### Return value

**1** if the cloth is rendered one-sided; **0** if one-sided.
