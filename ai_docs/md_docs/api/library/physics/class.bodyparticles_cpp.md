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

## int getNumParticles () const

Returns the current total number of particles that constitute the body.
### Return value

Current total number of particles in the body
## void setRigidity ( float rigidity )

Sets a new rigidity of the body's inner joints movement, i.e. how much interpolated linear and angular positions of inner joints affect the result.
### Arguments

- *float* **rigidity** - The rigidity of the body's inner joints movement

## float getRigidity () const

Returns the current rigidity of the body's inner joints movement, i.e. how much interpolated linear and angular positions of inner joints affect the result.
### Return value

Current rigidity of the body's inner joints movement
## void setRestitution ( float restitution )

Sets a new restitution of the body by bouncing.
### Arguments

- *float* **restitution** - The restitution of the body by bouncing

## float getRestitution () const

Returns the current restitution of the body by bouncing.
### Return value

Current restitution of the body by bouncing
## void setRadius ( float radius )

Sets a new radius of the particles forming the body and represented as sphere shapes.
### Arguments

- *float* **radius** - The radius of the particles forming the body

## float getRadius () const

Returns the current radius of the particles forming the body and represented as sphere shapes.
### Return value

Current radius of the particles forming the body
## void setNumIterations ( int iterations )

Sets a new number of iterations used to solve inner joints between particles.
### Arguments

- *int* **iterations** - The number of iterations used to solve inner joints

## int getNumIterations () const

Returns the current number of iterations used to solve inner joints between particles.
### Return value

Current number of iterations used to solve inner joints
## void setMass ( float mass )

Sets a new mass of the body.
### Arguments

- *float* **mass** - The mass of the body

## float getMass () const

Returns the current mass of the body.
### Return value

Current mass of the body
## void setLinearThreshold ( float threshold )

Sets a new linear stretching of the body's inner joints. when passing this threshold, the joints break.
### Arguments

- *float* **threshold** - The linear stretching threshold of the body's inner joints

## float getLinearThreshold () const

Returns the current linear stretching of the body's inner joints. when passing this threshold, the joints break.
### Return value

Current linear stretching threshold of the body's inner joints
## void setLinearStretch ( float stretch )

Sets a new scale for the length of linear joints (relative the source mesh topology).
### Arguments

- *float* **stretch** - The scale for the length of linear joints

## float getLinearStretch () const

Returns the current scale for the length of linear joints (relative the source mesh topology).
### Return value

Current scale for the length of linear joints
## void setLinearRestitution ( float restitution )

Sets a new restitution of the body's inner joints by linear stretching.
### Arguments

- *float* **restitution** - The restitution of the body's inner joints by linear stretching

## float getLinearRestitution () const

Returns the current restitution of the body's inner joints by linear stretching.
### Return value

Current restitution of the body's inner joints by linear stretching
## void setLinearDamping ( float damping )

Sets a new value indicating how much the linear velocity of the particles decreases over time.
### Arguments

- *float* **damping** - The damping of the particles linear velocity

## float getLinearDamping () const

Returns the current value indicating how much the linear velocity of the particles decreases over time.
### Return value

Current damping of the particles linear velocity
## void setFriction ( float friction )

Sets a new friction of the body by its contact with other surfaces.
### Arguments

- *float* **friction** - The friction of the body against other surfaces

## float getFriction () const

Returns the current friction of the body by its contact with other surfaces.
### Return value

Current friction of the body against other surfaces
## void setDistance ( float distance )

Sets a new distance of body simulation.
### Arguments

- *float* **distance** - The distance of body simulation

## float getDistance () const

Returns the current distance of body simulation.
### Return value

Current distance of body simulation
## void setCollision ( int collision )

Sets a new value indicating if collision with a body is enabled or not.
### Arguments

- *int* **collision** - The collision flag for the body

## int getCollision () const

Returns the current value indicating if collision with a body is enabled or not.
### Return value

Current collision flag for the body
## void setCollisionMask ( int mask )

Sets a new collision bit mask for the body. two objects collide, if they both have matching masks.
### Arguments

- *int* **mask** - The collision bit mask for the body

## int getCollisionMask () const

Returns the current collision bit mask for the body. two objects collide, if they both have matching masks.
### Return value

Current collision bit mask for the body
## void setAngularThreshold ( float threshold )

Sets a new threshold for angular folding of particles triangles connected by inner joints. when passing this threshold, the joints break.
### Arguments

- *float* **threshold** - The angular folding threshold of the inner joints

## float getAngularThreshold () const

Returns the current threshold for angular folding of particles triangles connected by inner joints. when passing this threshold, the joints break.
### Return value

Current angular folding threshold of the inner joints
## void setAngularRestitution ( float restitution )

Sets a new restitution of the body's inner joints, when triangles formed by particles are folded relative to each other.
### Arguments

- *float* **restitution** - The restitution of the body's inner joints by angular folding

## float getAngularRestitution () const

Returns the current restitution of the body's inner joints, when triangles formed by particles are folded relative to each other.
### Return value

Current restitution of the body's inner joints by angular folding
## void setIterationsMode ( BodyParticles::ITERATIONS_MODE mode )

Sets a new mode used to calculate the number of iterations for solving inner joints between particles: one of the [ITERATIONS_MODE_*](#ITERATIONS_MODE_OVERRIDE) values.
### Arguments

- *[BodyParticles::ITERATIONS_MODE](../../../api/library/physics/class.bodyparticles_cpp.md#ITERATIONS_MODE)* **mode** - The iterations calculation mode

## BodyParticles::ITERATIONS_MODE getIterationsMode () const

Returns the current mode used to calculate the number of iterations for solving inner joints between particles: one of the [ITERATIONS_MODE_*](#ITERATIONS_MODE_OVERRIDE) values.
### Return value

Current iterations calculation mode
---

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
