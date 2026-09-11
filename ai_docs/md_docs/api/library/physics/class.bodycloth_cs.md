# Unigine::BodyCloth Class (CS)

**Inherits from:** BodyParticles


This class is used to simulate a flat deformable [cloth bodies](../../../principles/physics/bodies/cloth/index.md). They use a [mass-spring simulation model](../../../principles/physics/bodies/cloth/index.md#model): the cloth is formed from [particles](../../../api/library/physics/class.bodyparticles_cs.md) (of sphere shape) that are located in the cloth mesh vertices and connected by inner joints.


### See Also


- The [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_cs.md) usage example demonstrating how to create an object, assign a cloth body to it, and set its parameters
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

### Properties

## 🔒︎ int NumIndices

The number of particle indices in the cloth body.
## int TwoSided

The value indicating if the cloth is one- or two-sided (1 - two-sided, 0 - one-sided). If two-sided, its material should not be [two-sided](../../../api/library/rendering/class.material_cs.md#setTwoSided_int_void) at the same time.
### Members

---

## BodyCloth ( )

Constructor. Creates a cloth body with default properties.
## BodyCloth ( Object object )

Constructor. Creates a cloth body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object represented with the new cloth body.

## int GetParticleIndex ( int num )

Returns the particle index by its number.
### Arguments

- *int* **num** - The particle index number.

### Return value

The particle index.
