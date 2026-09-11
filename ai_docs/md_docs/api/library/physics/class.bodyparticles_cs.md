# Unigine::BodyParticles Class (CS)

**Inherits from:** Body


BodyParticles is a base class for [BodyCloth](../../../api/library/physics/class.bodycloth_cs.md) and [BodyRope](../../../api/library/physics/class.bodyrope_cs.md) classes. It uses a [mass-spring simulation model](../../../principles/physics/bodies/cloth/index.md#model), i.e. particles that are connected by inner joints. The particles are of [sphere shape](#setRadius_float_void) and characterized by a [position](#setParticlePosition_int_Vec3_void), [mass](#setParticleMass_int_float_void) and [velocity](#setParticleVelocity_int_vec3_void). The total [mass](#setMass_float_void) of the whole cloth is distributed among them. Particles can be acted upon by a [force](#addParticleForce_int_vec3_void) or an [impulse](#addParticleImpulse_int_vec3_void). The inner joints can be [stretched](../../../principles/physics/bodies/cloth/index.md#stretching) ([linear](#setLinearRestitution_float_void) and [angular](#setAngularRestitution_float_void) separately), or linear joints can also be [scaled](#setLinearStretch_float_void), which provides the same stretching effect. When stretched to the specified distance, joins are [torn](../../../principles/physics/bodies/cloth/index.md#tearing) (the distance is set separately for [linear](#setLinearThreshold_float_void) and [angular](#setAngularThreshold_float_void) joints).


### See Also


- The [Creating and Attaching a Cloth](../../../code/usage/cloth_particle_joint/index_cs.md) usage example demonstrating how to set rope parameters


## BodyParticles Class

### Enums

## ITERATIONS_MODE

Iterations mode. Determines the way the number of iterations for solving the constraints of the particles body is calculated.
| Name | Description |
|---|---|
| **OVERRIDE** = 0 | In this mode the resulting number of iterations is equal to the [Iterations](#setNumIterations_int_void) value set for the body. |
| **MULTIPLICATION** = 1 | In this mode the resulting number of iterations is equal to the [value set for the body](#setNumIterations_int_void) multiplied by the [global physics iterations number](../../../editor2/settings/physics_global/index.md#iterations). |

### Properties

## 🔒︎ int NumParticles

The total number of particles that constitute the body.
## float Rigidity

The rigidity of the body's inner joints movement, i.e. how much interpolated linear and angular positions of inner joints affect the result.
## float Restitution

The restitution of the body by bouncing.
## float Radius

The radius of the particles forming the body and represented as sphere shapes.
## int NumIterations

The number of iterations used to solve inner joints between particles.
## float Mass

The mass of the body.
## float LinearThreshold

The linear stretching of the body's inner joints. when passing this threshold, the joints break.
## float LinearStretch

The scale for the length of linear joints (relative the source mesh topology).
## float LinearRestitution

The restitution of the body's inner joints by linear stretching.
## float LinearDamping

The value indicating how much the linear velocity of the particles decreases over time.
## float Friction

The friction of the body by its contact with other surfaces.
## float Distance

The distance of body simulation.
## int Collision

The value indicating if collision with a body is enabled or not.
## int CollisionMask

The collision bit mask for the body. two objects collide, if they both have matching masks.
## float AngularThreshold

The threshold for angular folding of particles triangles connected by inner joints. when passing this threshold, the joints break.
## float AngularRestitution

The restitution of the body's inner joints, when triangles formed by particles are folded relative to each other.
## BodyParticles.ITERATIONS_MODE IterationsMode

The mode used to calculate the number of iterations for solving inner joints between particles: one of the [ITERATIONS_MODE_*](#ITERATIONS_MODE_OVERRIDE) values.
### Members

---

## void SetParticleMass ( int num , float mass )

Sets the mass for the specified particle.
### Arguments

- *int* **num** - Particle number.
- *float* **mass** - Particle mass.

## float GetParticleMass ( int num )

Returns the current mass of the specified particle.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle mass.
## void SetParticlePosition ( int num , vec3 position )

Sets the position of the specified body's particle.
### Arguments

- *int* **num** - Particle number.
- *vec3* **position** - Particle position in world coordinates.

## vec3 GetParticlePosition ( int num )

Returns the current position of the specified particle.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle position in world coordinates.
## void SetParticleVelocity ( int num , vec3 velocity )

Sets the velocity of the specified particle.
### Arguments

- *int* **num** - Particle number.
- *vec3* **velocity** - Particle velocity.

## vec3 GetParticleVelocity ( int num )

Returns the current velocity of the specified particle.
### Arguments

- *int* **num** - Particle number.

### Return value

Particle velocity.
## void AddParticleForce ( int num , vec3 force )

Applies a force to the given particle. Integrated forces are applied after calling the update.
### Arguments

- *int* **num** - Particle number.
- *vec3* **force** - Amount of force to apply.

## void AddParticleImpulse ( int num , vec3 impulse )

Applies an impulse to the given particle. Impulses immediately affect particles velocities.
### Arguments

- *int* **num** - Particle number.
- *vec3* **impulse** - Amount of impulse to apply.
