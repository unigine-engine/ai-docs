# Unigine::JointParticles Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Joint


This class is used to pin [cloth body](../../../api/library/physics/class.bodycloth_usc.md) or [rope body](../../../api/library/physics/class.bodyrope_usc.md) to [rigid bodies](../../../api/library/physics/class.bodyrigid_usc.md), [ragdolls](../../../api/library/physics/class.bodyragdoll_usc.md) or [dummy bodies](../../../api/library/physics/class.bodydummy_usc.md).


### Example


The following code illustrates connection of a [rope body](../../../api/library/physics/class.bodyrope_usc.md) (rope) and a [dummy body](../../../api/library/physics/class.bodydummy_usc.md) (dummy) using a particles joint. The anchor is placed at the position of a dummy body.


```cpp
//the anchor point is placed at the position of a dummy body, pinning area size is (0.5f, 0.5f, 1.5f)
JointParticles joint = class_remove(new JointParticles(dummy, rope, dummy.getObject().getPosition(), Vec3(0.5f, 0.5f, 1.5f)));

// setting pinning threshold
joint.setThreshold(0.001f);

// setting number of iterations
joint.setNumIterations(4);

```


### See Also


Usage examples:


- [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_usc.md)
- [Creating Pylons and Wires Using Ropes](../../../code/usage/ropes_creating_pylons_and_wires/index_usc.md)


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
## void setSize ( vec3 size )

Sets a new size of the area of pinned vertices of cloth or rope body to another body.
### Arguments

- *vec3* **size** - The size of the pinned area.

## vec3 getSize () const

Returns the current size of the area of pinned vertices of cloth or rope body to another body.
### Return value

Current size of the pinned area.
---

## static JointParticles ( )

Constructor. Creates a particle joint with an anchor at the origin of the world coordinates.
## static JointParticles ( Body body0 , Body body1 )

Constructor. Creates a particle joint connecting two given bodies. An anchor is placed in the center of the body to which the cloth or rope is pinned.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - First body to be connected with the joint. It can be one of the following:

  - [BodyRigid](../../../api/library/physics/class.bodyrigid_usc.md)
  - [BodyRagdoll](../../../api/library/physics/class.bodyragdoll_usc.md)
  - [BodyDummy](../../../api/library/physics/class.bodydummy_usc.md)
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - Second body to be connected with the joint. It can be one of the following:

  - [BodyCloth](../../../api/library/physics/class.bodycloth_usc.md)
  - [BodyRope](../../../api/library/physics/class.bodyrope_usc.md)

## static JointParticles ( Body body0 , Body body1 , Vec3 anchor , vec3 size )

Constructor. Creates a particles joint connecting two given bodies with specified pinning area size and an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - First body to be connected with the joint. It can be one of the following:

  - [BodyRigid](../../../api/library/physics/class.bodyrigid_usc.md)
  - [BodyRagdoll](../../../api/library/physics/class.bodyragdoll_usc.md)
  - [BodyDummy](../../../api/library/physics/class.bodydummy_usc.md)
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - Second body to be connected with the joint. It can be one of the following:

  - [BodyCloth](../../../api/library/physics/class.bodycloth_usc.md)
  - [BodyRope](../../../api/library/physics/class.bodyrope_usc.md)
- *Vec3* **anchor** - Anchor coordinates.
- *vec3* **size** - Area for pinning vertices of cloth or rope body to another body.

## float getParticleMass ( int num )

Returns the mass of the pinned particle of the cloth or rope body.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle mass.
## vec3 getParticlePosition ( int num )

Returns the position of the pinned particle of the cloth or rope body.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle position.
## void clearParticles ( )

Unpins the cloth or rope body completely.
