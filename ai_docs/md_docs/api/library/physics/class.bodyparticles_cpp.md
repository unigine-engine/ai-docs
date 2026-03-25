# Unigine::BodyParticles Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** Body


BodyParticles is a base class for [BodyCloth](../../../api/library/physics/class.bodycloth_cpp.md) and [BodyRope](../../../api/library/physics/class.bodyrope_cpp.md) classes. It uses a [mass-spring simulation model](../../../principles/physics/bodies/cloth/index.md#model), i.e. particles that are connected by inner joints. The particles are of [sphere shape](#setRadius_float_void) and characterized by a [position](#setParticlePosition_int_Vec3_void), [mass](#setParticleMass_int_float_void) and [velocity](#setParticleVelocity_int_vec3_void). The total [mass](#setMass_float_void) of the whole cloth is distributed among them. Particles can be acted upon by a [force](#addParticleForce_int_vec3_void) or an [impulse](#addParticleImpulse_int_vec3_void). The inner joints can be [stretched](../../../principles/physics/bodies/cloth/index.md#stretching) ([linear](#setLinearRestitution_float_void) and [angular](#setAngularRestitution_float_void) separately), or linear joints can also be [scaled](#setLinearStretch_float_void), which provides the same stretching effect. When stretched to the specified distance, joins are [torn](../../../principles/physics/bodies/cloth/index.md#tearing) (the distance is set separately for [linear](#setLinearThreshold_float_void) and [angular](#setAngularThreshold_float_void) joints).


### See Also


- The [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_cpp.md) usage example demonstrating how to set rope parameters


## BodyParticles Class

### Enums

## ITERATIONS_MODE

Iterations mode. Determines the way the number of iterations for solving the constraints of the particles body is calculated.
| Name | Description |
|---|---|
| **ITERATIONS_MODE_OVERRIDE** = 0 | In this mode the resulting number of iterations is equal to the [Iterations](#setNumIterations_int_void) value set for the body. |
| **ITERATIONS_MODE_MULTIPLICATION** = 1 | In this mode the resulting number of iterations is equal to the [value set for the body](#setNumIterations_int_void) multiplied by the [global physics iterations number](../../../editor2/settings/physics_global/index.md#iterations). |

### Members

---

## void setAngularRestitution ( float restitution )

Sets the restitution of the body's inner joints, when triangles formed by particles are folded angularly relative to each other.
### Arguments

- *float* **restitution** - Joints angular restitution. Provided value is saturated in range **[0;1.0]**.

## float getAngularRestitution ( ) const

Returns the current restitution of the body's inner joints, when triangles formed by particles are folded angularly relative to each other.
### Return value

Joints angular restitution.
## void setAngularThreshold ( float threshold )

Sets the threshold for angular folding of particles triangles connected by inner joints. When passing this threshold, the joints tear up.
### Arguments

- *float* **threshold** - Joints angular folding threshold. If a negative value is provided, **0** will be used instead.

## float getAngularThreshold ( ) const

Returns the current threshold for angular folding of particles triangles connected by inner joints. When passing this threshold, the joints tear up.
### Return value

Joints angular folding threshold.
## void setCollision ( int collision )

Sets a value indicating if collision with a body is enabled or not.
### Arguments

- *int* **collision** - Positive value to enable collision, **0** to disable it.

## int getCollision ( ) const

Returns a value indicating if collision with a body is enabled or not.
### Return value

Positive value if collision is enabled, **0** if disabled.
## void setCollisionMask ( int mask )

Sets a collision bit mask for the body. Two objects collide, if they both have matching masks.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getCollisionMask ( ) const

Returns a collision bit mask for the body. Two objects collide, if they both have matching masks.
### Return value

Integer, each bit of which is a mask.
## void setDistance ( float distance )

Sets the distance of body simulation.
### Arguments

- *float* **distance** - Distance of simulation. If a negative value is provided, **0** will be used instead.

## float getDistance ( ) const

Returns the current distance of body simulation.
### Return value

Distance of simulation.
## void setFriction ( float friction )

Sets the friction of the body by its contact with other surfaces.
### Arguments

- *float* **friction** - Body friction. If a negative value is provided, **0** will be used instead.

## float getFriction ( ) const

Returns the current friction of the body by its contact with other surfaces.
### Return value

Body friction.
## void setLinearDamping ( float damping )

Sets a value indicating how much the linear velocity of the particles decreases over time.
### Arguments

- *float* **damping** - Linear damping value. If a negative value is provided, **0** will be used instead.

## float getLinearDamping ( ) const

Returns a value indicating how much the linear velocity of the particles decreases over time.
### Return value

Linear damping value.
## void setLinearRestitution ( float restitution )

Sets the restitution of the body's inner joints by linear stretching.
### Arguments

- *float* **restitution** - Joints linear restitution. Provided value is saturated in range **[0;1.0]**.

## float getLinearRestitution ( ) const

Returns the current restitution of the body's inner joints by linear stretching.
### Return value

Joints linear restitution.
## void setLinearStretch ( float stretch )

Sets the scale for the length of linear joints (relative the source mesh topology).
### Arguments

- *float* **stretch** - Stretch scale for linear joints. If a negative value is provided, **0** will be used instead.

## float getLinearStretch ( ) const

Returns the current scale for the length of linear joints (relative the source mesh topology).
### Return value

Stretch scale for linear joints.
## void setLinearThreshold ( float threshold )

Sets the threshold for linear stretching of the body's inner joints. When passing this threshold, the joints tear up.
### Arguments

- *float* **threshold** - Linear stretching threshold. If a negative value is provided, **0** will be used instead.

## float getLinearThreshold ( ) const

Returns the current linear stretching of the body's inner joints. When passing this threshold, the joints tear up.
### Return value

Joints linear stretching threshold.
## void setMass ( float mass )

Sets a mass of the body.
### Arguments

- *float* **mass** - Mass of the body. If a negative value is provided, **0** will be used instead.

## float getMass ( ) const

Returns the current mass of the body.
### Return value

Mass of the body.
## void setNumIterations ( int iterations )

Sets the number of iterations used to solve inner joints between the particles. Note that if this value is too low, the precision of calculations will suffer.
### Arguments

- *int* **iterations** - Number of iterations. If a non-positive value is provided, **1** will be used instead.

## int getNumIterations ( ) const

Returns the current number of iterations used to solve inner joints between particles.
### Return value

Number of iterations.
## int getNumParticles ( ) const

Returns the total number of particles that constitute the body.
### Return value

The number of particles.
## void setParticleMass ( int num , float mass )

Sets the mass for the specified particle.
### Arguments

- *int* **num** - Particle number.
- *float* **mass** - Particle mass.

## float getParticleMass ( int num ) const

Returns the current mass of the specified particle.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle mass.
## void setParticlePosition ( int num , const Math:: Vec3 & position )

Sets the position of the specified body's particle.
### Arguments

- *int* **num** - Particle number.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Particle position in world coordinates.

## Math:: Vec3 getParticlePosition ( int num ) const

Returns the current position of the specified particle.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle position in world coordinates.
## void setParticleVelocity ( int num , const Math:: vec3 & velocity )

Sets the velocity of the specified particle.
### Arguments

- *int* **num** - Particle number.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Particle velocity.

## Math:: vec3 getParticleVelocity ( int num ) const

Returns the current velocity of the specified particle.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle velocity.
## void setRadius ( float radius )

Sets the radius of the particles forming the body and represented as sphere shapes.
### Arguments

- *float* **radius** - Radius of the sphere-shaped particles.

## float getRadius ( ) const

Returns the current radius of the particles forming the body and represented as sphere shapes.
### Return value

Radius of the sphere-shaped particles.
## void setRestitution ( float restitution )

Sets the restitution of the body by bouncing.
### Arguments

- *float* **restitution** - Body restitution. Provided value is saturated in range **[0;1.0]**.

## float getRestitution ( ) const

Returns the current restitution of the body by bouncing.
### Return value

Body restitution.
## void setRigidity ( float rigidity )

Sets rigidity of the body's inner joints movement, i.e. how much interpolated linear and angular velocities of all joints affect velocities of each separate joint.
### Arguments

- *float* **rigidity** - Rigidity of joints interaction. Provided value is saturated in range **[0;1.0]**:

  - By the value of **0**, joints move independently.
  - By the value of **1**, joints move uniformly, as interpolated velocity greatly changes velocities of each joint.

## float getRigidity ( ) const

Returns the current rigidity of the body's inner joints movement, i.e. how much interpolated linear and angular velocities of all joints affect velocities of each separate joint.
### Return value

Rigidity of joints movement:
- By the value of **0**, joints move independently.
- By the value of **1**, joints move uniformly, as interpolated velocity greatly changes velocities of each joint.


## void addParticleForce ( int num , const Math:: vec3 & force )

Applies a force to the given particle. Integrated forces are applied after calling the update.
### Arguments

- *int* **num** - Particle number.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **force** - Amount of force to apply.

## void addParticleImpulse ( int num , const Math:: vec3 & impulse )

Applies an impulse to the given particle. Impulses immediately affect particles velocities.
### Arguments

- *int* **num** - Particle number.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **impulse** - Amount of impulse to apply.

## void setIterationsMode ( BodyParticles::ITERATIONS_MODE mode )

Sets iteration mode to be used for the particles body. The mode determines how the number of iterations for solving the constraints of the particles body is calculated. This method adds flexibility in fine-tuning of performance and simulation quality for each particles body.
### Arguments

- *[BodyParticles::ITERATIONS_MODE](../../../api/library/physics/class.bodyparticles_cpp.md#ITERATIONS_MODE)* **mode** - Iteration mode to be used for the particles body:

  - **OVERRIDE** - the resulting number of iterations is equal to the [value set for the body](#setNumIterations_int_void).
  - **MULTIPLICATION** - the resulting number of iterations is equal to the [value set for the body](#setNumIterations_int_void) multiplied by the [global physics iterations number](../../../editor2/settings/physics_global/index.md#iterations).

## BodyParticles::ITERATIONS_MODE getIterationsMode ( ) const

Returns the current iteration mode to be used for the particles body. The mode determines how the number of iterations for solving the constraints of the particles body is calculated. This method adds flexibility in fine-tuning of performance and simulation quality for each particles body.
### Return value

Current iteration mode of the particles body:
- **OVERRIDE** - the resulting number of iterations is equal to the [value set for the body](#setNumIterations_int_void).
- **MULTIPLICATION** - the resulting number of iterations is equal to the [value set for the body](#setNumIterations_int_void) multiplied by the [global physics iterations number](../../../editor2/settings/physics_global/index.md#iterations).
