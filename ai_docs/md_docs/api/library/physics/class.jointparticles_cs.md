# Unigine::JointParticles Class (CS)

**Inherits from:** Joint


This class is used to pin [cloth body](../../../api/library/physics/class.bodycloth_cs.md) or [rope body](../../../api/library/physics/class.bodyrope_cs.md) to [rigid bodies](../../../api/library/physics/class.bodyrigid_cs.md), [ragdolls](../../../api/library/physics/class.bodyragdoll_cs.md) or [dummy bodies](../../../api/library/physics/class.bodydummy_cs.md).


### Example


The following code illustrates connection of a [rope body](../../../api/library/physics/class.bodyrope_cs.md) (rope) and a [dummy body](../../../api/library/physics/class.bodydummy_cs.md) (dummy) using a particles joint. The anchor is placed at the position of a dummy body.


```csharp
	//the anchor point is placed at the position of a dummy body, pinning area size is (0.5f, 0.5f, 1.5f)
	JointParticles joint = new JointParticles(dummy, rope, dummy.Object.Position, new vec3(0.5f, 0.5f, 1.5f));

	// setting pinning threshold
	joint.Threshold = 0.001f;

	// setting number of iterations
	joint.NumIterations = 4;

```


### See Also


Usage examples:


- [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_cs.md)
- [Creating Pylons and Wires Using Ropes](../../../code/usage/ropes_creating_pylons_and_wires/index_cs.md)


## JointParticles Class

### Properties

## 🔒︎ int NumParticles

The total number of pinned particles of the cloth or rope body.
## float Threshold

The threshold that determines the distance for pinning vertices of cloth or rope body to another body. If vertices are closer than the threshold, they are pinned together; otherwise, particles stay loose.
## vec3 Size

The size of the area of pinned vertices of cloth or rope body to another body.
### Members

---

## JointParticles ( )

Constructor. Creates a particle joint with an anchor at the origin of the world coordinates.
## JointParticles ( Body body0 , Body body1 )

Constructor. Creates a particle joint connecting two given bodies. An anchor is placed in the center of the body to which the cloth or rope is pinned.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint. It can be one of the following:

  - [BodyRigid](../../../api/library/physics/class.bodyrigid_cs.md)
  - [BodyRagdoll](../../../api/library/physics/class.bodyragdoll_cs.md)
  - [BodyDummy](../../../api/library/physics/class.bodydummy_cs.md)
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint. It can be one of the following:

  - [BodyCloth](../../../api/library/physics/class.bodycloth_cs.md)
  - [BodyRope](../../../api/library/physics/class.bodyrope_cs.md)

## JointParticles ( Body body0 , Body body1 , vec3 anchor , vec3 size )

Constructor. Creates a particles joint connecting two given bodies with specified pinning area size and an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint. It can be one of the following:

  - [BodyRigid](../../../api/library/physics/class.bodyrigid_cs.md)
  - [BodyRagdoll](../../../api/library/physics/class.bodyragdoll_cs.md)
  - [BodyDummy](../../../api/library/physics/class.bodydummy_cs.md)
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint. It can be one of the following:

  - [BodyCloth](../../../api/library/physics/class.bodycloth_cs.md)
  - [BodyRope](../../../api/library/physics/class.bodyrope_cs.md)
- *vec3* **anchor** - Anchor coordinates.
- *vec3* **size** - Area for pinning vertices of cloth or rope body to another body.

## float GetParticleMass ( int num )

Returns the mass of the pinned particle of the cloth or rope body.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle mass.
## vec3 GetParticlePosition ( int num )

Returns the position of the pinned particle of the cloth or rope body.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle position.
## void ClearParticles ( )

Unpins the cloth or rope body completely.
