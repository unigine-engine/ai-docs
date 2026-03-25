# Unigine::JointParticles Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** Joint


This class is used to pin [cloth body](../../../api/library/physics/class.bodycloth_cpp.md) or [rope body](../../../api/library/physics/class.bodyrope_cpp.md) to [rigid bodies](../../../api/library/physics/class.bodyrigid_cpp.md), [ragdolls](../../../api/library/physics/class.bodyragdoll_cpp.md) or [dummy bodies](../../../api/library/physics/class.bodydummy_cpp.md).


### Example


The following code illustrates connection of a [rope body](../../../api/library/physics/class.bodyrope_cpp.md) (rope) and a [dummy body](../../../api/library/physics/class.bodydummy_cpp.md) (dummy) using a particles joint. The anchor is placed at the position of a dummy body.


```cpp
include <UniginePhysics.h>

/* .. */

//the anchor point is placed at the position of a dummy body, pinning area size is (0.5f, 0.5f, 1.5f)
JointParticlesPtr joint = JointParticles::create(dummy, rope, dummy->getObject()->getPosition(), Vec3(0.5f, 0.5f, 1.5f));

// setting pinning threshold
joint->setThreshold(0.001f);

// setting number of iterations
joint->setNumIterations(4);

```


### See Also


Usage examples:


- [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_cpp.md)
- [Creating Pylons and Wires Using Ropes](../../../code/usage/ropes_creating_pylons_and_wires/index_cpp.md)


## JointParticles Class

### Members

## int getNumParticles () const

Returns the current total number of pinned particles of the cloth or rope body.
### Return value

Current number of pinned particles.
## void setThreshold ( float threshold )

Sets a new threshold that determines the distance for pinning vertices of cloth or rope body to another body. If vertices are closer than the threshold, they are pinned together; otherwise, particles stay loose.
### Arguments

- *float* **threshold** - The threshold of pinning distance.

## float getThreshold () const

Returns the current threshold that determines the distance for pinning vertices of cloth or rope body to another body. If vertices are closer than the threshold, they are pinned together; otherwise, particles stay loose.
### Return value

Current threshold of pinning distance.
## void setSize ( const Math:: vec3 & size )

Sets a new size of the area of pinned vertices of cloth or rope body to another body.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The size of the pinned area.

## Math:: vec3 getSize () const

Returns the current size of the area of pinned vertices of cloth or rope body to another body.
### Return value

Current size of the pinned area.
---

## static JointParticlesPtr create ( )

Constructor. Creates a particle joint with an anchor at the origin of the world coordinates.
## static JointParticlesPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 )

Constructor. Creates a particle joint connecting two given bodies. An anchor is placed in the center of the body to which the cloth or rope is pinned.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - First body to be connected with the joint. It can be one of the following:

  - [BodyRigid](../../../api/library/physics/class.bodyrigid_cpp.md)
  - [BodyRagdoll](../../../api/library/physics/class.bodyragdoll_cpp.md)
  - [BodyDummy](../../../api/library/physics/class.bodydummy_cpp.md)
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Second body to be connected with the joint. It can be one of the following:

  - [BodyCloth](../../../api/library/physics/class.bodycloth_cpp.md)
  - [BodyRope](../../../api/library/physics/class.bodyrope_cpp.md)

## static JointParticlesPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 , const Math:: Vec3 & anchor , const Math:: vec3 & size )

Constructor. Creates a particles joint connecting two given bodies with specified pinning area size and an anchor placed at specified coordinates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - First body to be connected with the joint. It can be one of the following:

  - [BodyRigid](../../../api/library/physics/class.bodyrigid_cpp.md)
  - [BodyRagdoll](../../../api/library/physics/class.bodyragdoll_cpp.md)
  - [BodyDummy](../../../api/library/physics/class.bodydummy_cpp.md)
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Second body to be connected with the joint. It can be one of the following:

  - [BodyCloth](../../../api/library/physics/class.bodycloth_cpp.md)
  - [BodyRope](../../../api/library/physics/class.bodyrope_cpp.md)
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **anchor** - Anchor coordinates.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Area for pinning vertices of cloth or rope body to another body.

## float getParticleMass ( int num )

Returns the mass of the pinned particle of the cloth or rope body.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle mass.
## Math:: vec3 getParticlePosition ( int num )

Returns the position of the pinned particle of the cloth or rope body.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle position.
## void clearParticles ( )

Unpins the cloth or rope body completely.
