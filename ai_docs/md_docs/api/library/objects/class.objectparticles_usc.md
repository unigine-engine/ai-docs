# ObjectParticles Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create [particle systems](../../../objects/effects/particles/index.md). The particles are approximated with a sphere. They can be of different [types](#setParticlesType_int_void) (see the [details](../../../objects/effects/particles/index.md#particle_type)) and [radius](#getRadiusOverTimeModifier_ParticleModifierScalar) (that can [change](#getGrowthOverTimeModifier_ParticleModifierScalar) with time). They are emitted from different [emitters](#setEmitterType_int_void) (see the [details](../../../objects/effects/particles/index.md#emitter_shape)) with a specified [spawn rate](#setSpawnRate_float_void). The particles disappear after the set [life time period](#setLife_float_float_void) or [culled](#setCulling_int_void) when hitting other nodes. They either [collide](#setCollisionEnabled_int_void) with the outer surface of the approximation sphere or [intersect](#setPhysicsIntersectionEnabled_int_void) only by the its center.


The particle flow [direction](#getDirectionOverTimeModifier_ParticleModifierVector) can be influenced by:

- [Gravity](#getGravityOverTimeModifier_ParticleModifierVector)
- [Physicals](../../../api/library/physics/class.physical_usc.md) nodes


The particle system can also [initialized](#setWarming_int_void) before it actually appears, so that it starts to be rendered with already spawned particles.


### Synchronizing Particles


For image consistency in multi-channel rendering use cases, Particle Systems can have more deterministic behavior, i.e. when a particle is spawned on one PC, it can travel to another screen seamlessly.


To synchronize the particle systems across several applications, it is required to define which application is the Master one — it will count all particles and provide all related info via the network to Slaves — applications that only receive data and reproduce them.


```cpp
bool is_master = true; // or false, if the application is a Slave
ObjectParticles particles; // particles that are going to be synchronized
Socket socket; // example of a socket used to send the particles data

void init()
{
	// For every type of the application, define the particles operation mode
	if (is_master)
		particles.setSyncMode(OBJECT_PARTICLES_SYNC_MODE_MASTER);
	else
		particles.setSyncMode(OBJECT_PARTICLES_SYNC_MODE_SLAVE);
}

void update()
{
	if (is_master)
	{
		Blob data = new Blob();
		particles.takeSyncData(data);
		socket.write(data.getData(), data.getSize());


	}
	else
	{
		Blob data = new Blob();
		socket.readStream(data, 1048576); // 1Mb, maximum size of the packet
		data.seekSet(0); // Moving the pointer to the first symbol,
		 				  // because after reading the data from the socket,
						  // the pointer is at the end of the data.
		particles.applySyncData(data);
	}
}

```


## ObjectParticles Class

### Members

---

## static ObjectParticles ( )

Constructor. Creates a particle system.
## BoundBox getBoundBoxParticles ( )

Returns the estimated bounding box considering the changes of the particle system (velocity, length, etc.).
### Return value

Bounding box
## BoundBox getBoundBoxSimulation ( )

Returns the exact bounding box of the particle system.
### Return value

Bounding box
## void setClearOnEnable ( int enable )

Enables or disables re-initialization of the particle system each time it is enabled. When this option is disabled, turning on the particle system will restore the state it had before it was turned off.
### Arguments

- *int* **enable** - **1** to re-initialize particle system each time it is enabled; otherwise, **0**.

## int isClearOnEnable ( )

Returns a value indicating if particle system is to be re-initialized each time it is enabled.
### Return value

**1** if particle system is to be re-initialized each time it is enabled; otherwise, **0**.
## void setCollisionEnabled ( int enabled )

Enables or disables collision detection for spheres that approximate each particle. This method is slower than intersection detection, but more precise.
### Arguments

- *int* **enabled** - **1** to enable sphere-based collision detection for particles, **0** to disable it.

## int isCollisionEnabled ( )

Returns a value indicating if collision detection for spheres that approximate each particle. This method is slower than sphere center-based intersection detection, but more precise.
### Return value

**1** if the sphere-based collision detection for particles is enabled; otherwise, **0**.
## void setCollisionMask ( int mask )

Sets a new *[Collision](../../../principles/bit_masking/index.md#collision_mask)* Mask to be used for particles. Particles will collide with an object, if they both have matching masks.
### Arguments

- *int* **mask** - New *[Collision](../../../principles/bit_masking/index.md#collision_mask)* Mask to be used for particles.

## int getCollisionMask ( )

Returns the current *[Collision](../../../principles/bit_masking/index.md#collision_mask)* Mask to be used for particles. Particles will collide with an object, if they both have matching masks.
### Return value

*[Collision](../../../principles/bit_masking/index.md#collision_mask)* Mask currently used for particles.
## void setPhysicsIntersectionEnabled ( int enabled )

Enables or disables detecting collision by the center of the sphere that approximates the particles. This method is faster than collision detection, but less precise. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
### Arguments

- *int* **enabled** - **1** to detect intersections, **0** not to detect.

## int isPhysicsIntersectionEnabled ( )

Returns a value indicating if collisions are to be detected by the center of the sphere that approximates the particles. This method is faster than sphere-based collision detection, but less precise. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
### Return value

**1** if the sphere center-based intersection detection is enabled; otherwise, **0**.
## void setPhysicsIntersectionMask ( int mask )

Sets a new *[Physics Intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)* Mask to be used for particles. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
### Arguments

- *int* **mask** - New *[Physics Intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)* Mask to be used for particles.

## int getPhysicsIntersectionMask ( )

Returns the current *[Physics Intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)* Mask for particles. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
### Return value

Current *[Physics Intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)* Mask used for particles.
## vec3 getContactNormal ( int num )

Returns the normal vector for the collision point of the particles with other objects.
### Arguments

- *int* **num** - Collision point number.

### Return value

Normal vector coordinates.
## Object getContactObject ( int num )

Returns the object that collided with particles collided in a given collision point.
### Arguments

- *int* **num** - The collision point number.

### Return value

The object participated in collision.
## Vec3 getContactPoint ( int num )

Returns the point of the particles collision with other objects.
### Arguments

- *int* **num** - The collision point number.

### Return value

Collision point coordinates.
## vec3 getContactVelocity ( int num )

Returns the velocity in the collision point of the particles with other objects.
### Arguments

- *int* **num** - The collision point number.

### Return value

Velocity values for each of space dimensions.
## void setCulling ( int culling )

Sets a value indicating if particles should disappear upon collision or intersection.
### Arguments

- *int* **culling** - 1 to make particles disappear; 0 to continue rendering of particles after collision/intersection.

## int getCulling ( )

Returns a value indicating if particles would disappear upon collision or intersection.
### Return value

1 if particles would disappear; otherwise, 0.
## void setDelay ( float mean , float spread )

Sets delay of particle system initialization relative to the parent particle one.
### Arguments

- *float* **mean** - A mean value in seconds. If a negative value is provided, 0 will be used instead.
- *float* **spread** - A spread value in seconds.

## float getDelayMean ( )

Returns the mean value of particles initialization delay relative to the parent particle system.
### Return value

The mean value in seconds.
## float getDelaySpread ( )

Returns the spread value of particles initialization delay relative to the parent particle system.
### Return value

The spread value in seconds.
## void setDepthSort ( int sort )

Enables or disables depth sorting of particles. Depth sorting is required, if particles use alpha blending.
### Arguments

- *int* **sort** - **1** to enable the depth sorting, **0** to disable it.

## int getDepthSort ( )

Returns a value indicating if depth sorting of particles is enabled. Depth sorting is required, if particles use alpha blending.
### Return value

**1** if the depth sorting is enabled; otherwise, **0**.
## void setDuration ( float mean , float spread )

Sets a duration of each particle emission in seconds.
### Arguments

- *float* **mean** - Mean value in seconds. If a negative value is provided, 0 will be used instead.
- *float* **spread** - Spread value in seconds.

## float getDurationMean ( )

Returns the current mean value of particle emission intervals.
### Return value

The mean value in seconds.
## float getDurationSpread ( )

Returns the current spread value of particle emission intervals.
### Return value

The spread value in seconds.
## void setEmitterBased ( int based )

Sets a value indicating if particles should follow emitter transformations, i.e. the direction of their flow should change after the emitter.
### Arguments

- *int* **based** - **1** for particles to follow emitter transformations; **0** for them to flow independently.

## int isEmitterBased ( )

Returns a value indicating if particles follow emitter transformations, i.e. the direction of their flow changes after the emitter.
### Return value

**1** if particles follow emitter transformations; otherwise, **0**.
## void setEmitterContinuous ( int continuous )

Sets a value indicating if additional spawn points should be generated when the emitter is moved, which provides a continuous flow of particles.
### Arguments

- *int* **continuous** - **1** to create the continuous flow of particles; **0** to create the discrete flow with sparse generation points.

## int isEmitterContinuous ( )

Returns a value indicating if additional spawn points are generated when the emitter is moved, which provides a continuous flow of particles.
### Return value

**1** if particles are created in the continuous flow; otherwise, **0**.
## void setEmitterEnabled ( int enabled )

Enables or disables particle emission.
### Arguments

- *int* **enabled** - **1** to enable particle emission, **0** to disable it.

## int isEmitterEnabled ( )

Returns a value indicating if particle emission is enabled.
### Return value

**1** if emission is enabled; otherwise, **0**.
## void setEmitterSequence ( int sequence )

Sets the rendering order of the particle system inside the particles hierarchy.
### Arguments

- *int* **sequence** - The rendering priority. Particle systems with the lowest order number are rendered first.

## int getEmitterSequence ( )

Returns the current rendering order of the particle system inside the particles hierarchy.
### Return value

The current rendering priority.
## void setEmitterShift ( int shift )

Sets a value indicating if the emitter spawns particles only when it is moving. The further it has moved, if compared to its position in the previous frame, the more particles will be spawned. If the emitter is not moving, there are no particles at all.
### Arguments

- *int* **shift** - **1** to enable the shift-based spawning; **0** to disable it.

## int isEmitterShift ( )

Returns a value indicating if the emitter spawns particles only when it is moving. The further it has moved, if compared to its position in the previous frame, the more particles will be spawned. If the emitter is not moving, there are no particles at all.
### Return value

**1** if the shift-based spawning is enabled; **0** if it is not.
## void setEmitterSize ( vec3 size )

Sets a size of the emitter.
### Arguments

- *vec3* **size** - New emitter size. Depending on the type of the emitter, this value is interpreted as follows: If negative values are provided, 0 will be used instead of them.

  - [OBJECT_PARTICLES_EMITTER_POINT](#EMITTER_POINT), [OBJECT_PARTICLES_EMITTER_RANDOM](#EMITTER_RANDOM)  or [OBJECT_PARTICLES_EMITTER_SPARK](#EMITTER_SPARK): all vector components are ignored.
  - [OBJECT_PARTICLES_EMITTER_SPHERE](#EMITTER_SPHERE): the first vector component is the radius of the sphere.
  - [OBJECT_PARTICLES_EMITTER_CYLINDER](#EMITTER_CYLINDER): the first vector component is the radius of the cylinder, the second vector component is the height of the cylinder.
  - [OBJECT_PARTICLES_EMITTER_BOX](#EMITTER_BOX): all vector components are interpreted as box dimensions (*x*, *y*, *z*).

## vec3 getEmitterSize ( )

Returns the current emitter size.
### Return value

Current size. Depending on the type of the emitter, this value is interpreted as follows:
- [OBJECT_PARTICLES_EMITTER_POINT](#EMITTER_POINT), [OBJECT_PARTICLES_EMITTER_SPARK](#EMITTER_SPARK) or [OBJECT_PARTICLES_EMITTER_RANDOM](#EMITTER_RANDOM)  : all vector components should be ignored.
- [OBJECT_PARTICLES_EMITTER_SPHERE](#EMITTER_SPHERE): the first vector component is the radius of the sphere.
- [OBJECT_PARTICLES_EMITTER_CYLINDER](#EMITTER_CYLINDER): the first vector component is the radius of the cylinder, the second vector component is the height of the cylinder.
- [OBJECT_PARTICLES_EMITTER_BOX](#EMITTER_BOX): all vector components are interpreted as box dimensions (*x*, *y*, *z*).


## void setEmitterSync ( int sync )

Sets a value indicating if a particle system emitter needs to be synchronized to a parent particle system.
### Arguments

- *int* **sync** - 1 to synchronize the emitter; otherwise, 0.

## int getEmitterSync ( )

Returns a value indicating if a particle system emitter is synchronized to a parent particle system.
### Return value

1 if it is synchronized; otherwise, 0.
## void setEmitterType ( int type )

Sets a type of the emitter.
### Arguments

- *int* **type** - One of the *OBJECT_PARTICLES_EMITTER_** variables.

## int getEmitterType ( )

Returns the [type (shape) of the emitter](../../../objects/effects/particles/index.md#emitter_shape). The default is **[OBJECT_PARTICLES_EMITTER_POINT](#EMITTER_POINT)**.
### Return value

One of the [OBJECT_PARTICLES_EMITTER_*](#EMITTER_BOX) variables.
## void setEmitterVelocity ( vec3 velocity )

Sets the emitter velocity, which is added to the [initial velocity](#getVelocityOverTimeModifier_ParticleModifierScalar) of spawned particles. If the value is equal to 0, the actual velocity of emitter node will be used.
### Arguments

- *vec3* **velocity** - Emitter velocity, in units per second.

## vec3 getEmitterVelocity ( )

Returns the current emitter velocity, which is added to the initial velocity of spawned particles. If the value equals 0, the actual velocity of emitter node will be used.
### Return value

The emitter velocity in units per second.
## void setLife ( float mean , float spread )

Sets a lifetime duration of particles in seconds.
### Arguments

- *float* **mean** - A mean value in seconds. If a too small value is provided, **1E-6** will be used instead.
- *float* **spread** - A spread value in seconds.

## float getLifeMean ( )

Returns the current mean value of particle lifetime duration.
### Return value

The mean value in seconds.
## float getLifeSpread ( )

Returns the current spread value of particle lifetime duration.
### Return value

The spread value in seconds.
## void setMaxWarmingTime ( float time )

Sets max time for particles simulation during the warming, in seconds.
### Arguments

- *float* **time** - Time, in seconds.

## float getMaxWarmingTime ( )

Returns max time value for particles simulation during the warming, in seconds.
### Return value

Time, in seconds.
## int getNumContacts ( )

Returns the total number of particles collisions with other objects.
### Return value

Number of collisions.
## int getNumParticles ( )

Returns the current number of particles.
### Return value

The number of particles.
## Vec3 getParticlePosition ( int num )

Returns the position of a given particle.
### Arguments

- *int* **num** - The particle number.

### Return value

Position coordinates for the particle.
## float getParticleRadius ( int num )

Returns the radius of a given particle.
### Arguments

- *int* **num** - The particle number.

### Return value

Radius of the particle.
## void setParticlesType ( int type )

Sets a type of particles to emit.
### Arguments

- *int* **type** - One of the *OBJECT_PARTICLES_TYPE_** variables.

## int getParticlesType ( )

Returns the type of emitted particles.
### Return value

One of the [OBJECT_PARTICLES_TYPE_*](#TYPE_BILLBOARD) variables.
## void getParticleTransforms ( )

Returns transformation matrices for spawned particles.
### Arguments

## vec3 getParticleVelocity ( int num )

Returns the velocity vector for a specified particle.
### Arguments

- *int* **num** - The particle number.

### Return value

The velocity vector.
## void setPeriod ( float mean , float spread )

Sets an interval of emitter inactivity in seconds.
### Arguments

- *float* **mean** - A mean value in seconds. If a negative value is provided, 0 will be used instead.
- *float* **spread** - A spread value in seconds.

## float getPeriodMean ( )

Returns the current mean value of emitter inactivity intervals.
### Return value

The mean value in seconds.
## float getPeriodSpread ( )

Returns the current spread value of emitter inactivity intervals.
### Return value

The spread value in seconds.
## void setPhysicalMask ( int mask )

Sets the bit mask for interactions with [physicals](../../../api/library/physics/class.physical_usc.md). Two objects interact, if they both have matching masks.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getPhysicalMask ( )

Returns the bit mask for interactions with physicals. Two objects interact, if they both have matching masks.
### Return value

Integer, each bit of which is a mask.
## void setPhysicalMass ( float mass )

Sets the mass of the particles. This value matters only for computing physical interactions.
### Arguments

- *float* **mass** - The mass of the particles.

## float getPhysicalMass ( )

Returns the current mass of the particles. This value matters only for computing physical interactions.
### Return value

Particles mass.
## void setProceduralRendering ( int rendering )

Enables particle system rendering to procedural texture to be used by an [orthographic decal](../../../api/library/decals/class.decalortho_usc.md) or a [field height](../../../api/library/fields/class.fieldheight_usc.md). For example, ship wake waves are simulated using this feature.
### Arguments

- *int* **rendering** - **1** to enable rendering to procedural texture, **0** to disable.

## int isProceduralRendering ( )

Returns the value indicating if the procedural rendering enabled or not. This feature enables rendering of particles into an orthographic decal or a field height, and can be used, for example, to create ship wake waves.
### Return value

**1** if the procedural rendering is enabled; otherwise, **0**.
## void setProceduralParenting ( int parenting )

Sets the type of relationship between the particle system and a [decal](../../../api/library/decals/class.decalortho_usc.md) / [field](../../../api/library/fields/class.fieldheight_usc.md) node that uses the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Arguments

- *int* **parenting** - Relationship type to be used for rendering the particle system to a procedural texture:

  - 0 - a decal/field node that uses the procedural texture is a child of the particle system.
  - 1 - a decal/field node that uses the procedural texture is a parent of the particle system.

## int getProceduralParenting ( )

Returns the current type of relationship between the particle system and a [decal](../../../api/library/decals/class.decalortho_usc.md) / [field](../../../api/library/fields/class.fieldheight_usc.md) node that uses the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Return value

Relationship type to be used for rendering the particle system to a procedural texture:
- 0 - a decal/field node that uses the procedural texture is a child of the particle system.
- 1 - a decal/field node that uses the procedural texture is a parent of the particle system.


## void setProceduralPositioning ( int positioning )

Sets positioning mode to be used for child nodes using the procedural texture to which the particle system is rendered.
> **Notice:** - Positioning mode can be set only when the particle system is a parent of a decal/field node that uses the procedural texture ([parenting mode](#setProceduralParenting_int_void) is set to 0)
> - [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Arguments

- *int* **positioning** - Mode of the procedural positioning. Can be one of the following:

  - PROCEDURAL_POSITIONING_MANUAL = 0 - position of a child decal/field node, that uses the procedural texture, can be changed manually.
  - PROCEDURAL_POSITIONING_AUTO = 1 - position of a child decal/field node, that uses the procedural texture, is automatically defined by the position of particle system and cannot be changed manually.

## int getProceduralPositioning ( )

Returns the value indicating the procedural position mode.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Return value

Mode of the procedural positioning. Can be one of the following:
- PROCEDURAL_POSITIONING_MANUAL = 0
- PROCEDURAL_POSITIONING_AUTO = 1


## void setProceduralTextureResolution ( vec3 res )

Sets the resolution of the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Arguments

- *vec3* **res** - Resolution of the texture.

## vec3 getProceduralTextureResolution ( )

Returns the resolution of the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Return value

Resolution of the texture.
## void setRestitution ( float restitution )

Sets a restitution value for particles.
### Arguments

- *float* **restitution** - A new restitution value. The provided value will be saturated in the range **[0; 1]**.

## float getRestitution ( )

Returns the current restitution value for particles.
### Return value

The current restitution value.
## void setRoughness ( float roughness )

Sets a roughness of the particle surface.
### Arguments

- *float* **roughness** - A new roughness value. The provided value will be saturated in the range **[0; 1]**.

## float getRoughness ( )

Returns the current roughness of the particle surface.
### Return value

The current roughness.
## void setSeed ( unsigned int seed )

Sets a seed value for the particles' random generator.
### Arguments

- *unsigned int* **seed** - Seed value.

## unsigned int getSeed ( )

Returns a seed value used for the particles' random generator.
### Return value

Seed value.
## void setNumberPerSpawn ( int spawn )

Sets the number of particles to be spawned simultaneously each time according to the [spawn rate](#setSpawnRate_float_void).
### Arguments

- *int* **spawn** - Number of particles to be spawned simultaneously.

## int getNumberPerSpawn ( )

Returns the current number of particles to be spawned simultaneously each time according to the [spawn rate](#setSpawnRate_float_void).
### Return value

Current number of particles to be spawned simultaneously.
## void setSpawnRate ( float rate )

Sets a rate at which particles are created.
### Arguments

- *float* **rate** - A new spawn rate. If a too small value is provided, **1E-6** will be used instead.

## float getSpawnRate ( )

Returns the current particle spawn rate.
### Return value

The current spawn rate.
## void setSpawnScale ( float scale )

Sets a spawn scale that enables to modulate smooth and gradual initialization of the particle system starting with the given spawn state and up to the specified spawn rate.
### Arguments

- *float* **scale** - A spawn scale. The provided value is clipped to range **[0;1]**. By the value of 0, there are no spawned particles at the start. By the value of 1, the system is initialized with the specified spawn rate.

## float getSpawnScale ( )

Returns the current spawn scale that enables to modulate smooth and gradual initialization of the particle system starting with the given spawn state and up to the specified spawn rate.
### Return value

The current spawn scale.
## void setSpawnThreshold ( float threshold )

Sets the velocity threshold for [spark](#EMITTER_SPARK) and [random](#EMITTER_RANDOM) emitters. They spawn particles if velocity of the parent particles is high enough.
### Arguments

- *float* **threshold** - A velocity threshold for the parent particles.

## float getSpawnThreshold ( )

Returns the current velocity threshold for spark and random emitters. They spawn particles if velocity of the parent particles is high enough.
### Return value

The current velocity threshold of the parent particles.
## void setTextureAtlas ( int atlas )

Sets a value indicating if a diffuse texture for the particles is a **NxN** texture atlas.
### Arguments

- *int* **atlas** - Positive number if a texture atlas is used; 0 if an ordinary diffuse texture is assigned.

## int getTextureAtlas ( )

Returns a value indicating if a diffuse texture for the particles is used as a **NxN** texture atlas.
### Return value

Positive number if a texture atlas is used; otherwise, 0.
## void setVariationX ( int variationx )

Sets a value indicating if the initial orientation of particles diffuse texture should be randomly varied along the X axis.
### Arguments

- *int* **variationx** - 1 to add random variation along the X axis, 0 not to add.

## int getVariationX ( )

Returns a value indicating if the initial orientation of particles diffuse texture is randomly varied along the X axis.
### Return value

1 if there is random variation along the **X** axis, 0 if there is not.
## void setVariationY ( int variationy )

Sets a value indicating if the initial orientation of particles diffuse texture should be randomly varied along the Y axis.
### Arguments

- *int* **variationy** - 1 to add random variation along the Y axis, 0 not to add.

## int getVariationY ( )

Returns a value indicating if the initial orientation of particles diffuse texture is randomly varied along the Y axis.
### Return value

1 if there is random variation along the **Y** axis, 0 if there is not.
## void setWarming ( int warming )

Enables the warm start for the particles. It means that the particle system starts to be rendered with already emitted particles, rather then from a zero point.
### Arguments

- *int* **warming** - Positive number to enable the warm start; 0 to disable.

## int getWarming ( )

Returns a value indicating if the warm start is enabled for the particles. It means that the particle system starts to be rendered with already emitted particles, rather then from a zero point.
### Return value

1 if warm start is enabled; 0 if disabled.
## WorldBoundBox getWorldBoundBoxParticles ( )

Returns the estimated world bounding box considering the changes of the particle system (velocity, length, etc.).
## Vec3 getWorldOffset ( )

Returns the current world offset of the local origin of coordinates of the particle system. The offset of the origin of coordinates is changed depending on the position of the particle system so that the particles are simulated near their emitter.
### Return value

Offset coordinates values.
## void addEmitterSpark ( Vec3 point , vec3 normal , vec3 velocity )

Adds a spark emitter in the given point.
### Arguments

- *Vec3* **point** - Point for sparks emission.
- *vec3* **normal** - Normal vector at the point of spark emission.
- *vec3* **velocity** - Velocity in the point of spark emission (velocity of source particles or node by contact).

## void clearParticles ( )

Deletes all particles spawned by the emitter.
## static int type ( )

Returns the type of the object.
### Return value

[Object Particles](../../../api/library/nodes/class.node_usc.md#OBJECT_PARTICLES) type identifier.
## int saveStateSelf ( Stream stream )

Saves the object's state to the stream.
> **Notice:** This method saves all object's parameters/


Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreStateSelf()](#restoreStateSelf_Stream_int) method is used:


```cpp
// initialize a object and set its state
//...//

// save state
Blob blob_state = new Blob();
object.saveStateSelf(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
object.restoreStateSelf(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** on success; otherwise, **0**.
## int restoreStateSelf ( Stream stream )

Restores the object's state from the stream.
> **Notice:** This method restores all object's parameters..


Restoring from the stream requires creating a blob to save into and saving the state using the [saveStateSelf()](#saveStateSelf_Stream_int) method:


```cpp
// initialize a object and set its state
//...//

// save state
Blob blob_state = new Blob();
object.saveStateSelf(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
object.restoreStateSelf(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream instance.

### Return value

**1** on success; otherwise, **0**.
## void setSyncMode ( int mode )

Sets synchronization mode to be used for the particle system.
### Arguments

- *int* **mode** - Synchronization mode to be set, one of the [SYNC_MODE](#SYNC_MODE) values.

## int getSyncMode ( )

Returns the current synchronization mode used for the particle system.
### Return value

Current synchronization mode, one of the [SYNC_MODE](#SYNC_MODE) values.
## void takeSyncData ( Stream stream )

Writes particle synchronization data to the specified stream. This method should be used by the particle system with the master [sync mode](#setSyncMode_int_void).
### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which particle synchronization data is to be written.

## void applySyncData ( Stream stream )

Reads particle synchronization data from the specified stream and applies it to the particle system. This method should be used by the particle system with the slave [sync mode](#setSyncMode_int_void).
### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream with particle synchronization data to be applied.

## void setFPSVisibleCamera ( int camera = -1 )

Sets the update rate value when the object is rendered to the viewport. The default value is infinity.
### Arguments

- *int* **camera** - Update rate value when the object is rendered.

## int getFPSVisibleCamera ( )

Returns the update rate value when the object is rendered to the viewport.
### Return value

Update rate value when the object is rendered.
## void setFPSVisibleShadow ( int shadow = 30 )

Sets the update rate value when only object shadows are rendered. The default value is 30 fps.
### Arguments

- *int* **shadow** - Update rate value when only object shadows are rendered.

## int getFPSVisibleShadow ( )

Returns the update rate value when only object shadows are rendered.
### Return value

Update rate value when only object shadows are rendered.
## void setFPSInvisible ( int invisible = 0 )

Sets the update rate value when the object is not rendered at all. The default value is 0 fps.
### Arguments

- *int* **invisible** - Update rate value when the object is not rendered at all.

## int getFPSInvisible ( )

Returns the update rate value when the object is not rendered at all.
### Return value

Update rate value when the object is not rendered at all.
## void setUpdateDistanceLimit ( float limit = 1000 )

Sets the distance from the camera within which the object should be updated. The default value is 1000 units.
### Arguments

- *float* **limit** - Distance from the camera within which the object should be updated.

## float getUpdateDistanceLimit ( )

Returns the distance from the camera within which the object should be updated.
### Return value

Distance from the camera within which the object should be updated.
## void setEmitterLimitPerSpawn ( int spawn )

Sets the [maximum number of particles](../../../objects/effects/particles/index.md#number_per_spawn) to be spawned simultaneously each time according to the Spawn Rate.
### Arguments

- *int* **spawn** - New number of particles emitted per spawn.

## int getEmitterLimitPerSpawn ( )

Returns the [maximum number of particles](../../../objects/effects/particles/index.md#number_per_spawn) to be spawned simultaneously each time according to the Spawn Rate.
### Return value

Current number of particles emitted per spawn.
## ParticleModifierScalar getAngleOverTimeModifier ( )

Returns the modifier used to control how the [orientation angle](../../../objects/effects/particles/index.md#angle) values change over time.
### Return value

Modifier, that controls orientation angle values.
## ParticleModifierScalar getRotationOverTimeModifier ( )

Returns the modifier used to control how the [particle angular velocity](../../../objects/effects/particles/index.md#angle) values change over time.
### Return value

Modifier, that controls particle angular velocity values.
## ParticleModifierScalar getRadiusOverTimeModifier ( )

Returns the modifier used to control how the [particle radius](../../../objects/effects/particles/index.md#radius) values change over time.
### Return value

Modifier, that controls particle radius values.
## ParticleModifierScalar getGrowthOverTimeModifier ( )

Returns the modifier used to control how the particle [radius value changes over time](../../../objects/effects/particles/index.md#increase_in_radius).
### Return value

Modifier, that controls particle growth.
## ParticleModifierScalar getLengthStretchOverTimeModifier ( )

Returns the modifier used to control how the [stretch](../../../objects/effects/particles/index.md#length_stretch) values of Length particles change over time.
### Return value

Modifier, that controls stretching of Length particles.
## ParticleModifierScalar getLengthFlatteningOverTimeModifier ( )

Returns the modifier used to control how the [flattening](../../../objects/effects/particles/index.md#length_flattening) values of Length particles change over time.
### Return value

Modifier, that controls flattening of Length particles.
## ParticleModifierScalar getVelocityOverTimeModifier ( )

Returns the modifier used to control how the [velocity](../../../objects/effects/particles/index.md#velocity) values of particles change over time.
### Return value

Modifier, that controls linear velocity of particles.
## ParticleModifierVector getDirectionOverTimeModifier ( )

Returns the modifier used to control how the [direction](../../../objects/effects/particles/index.md#direction) of emission changes over time.
### Return value

Modifier, that controls direction of emission of particles.
## ParticleModifierVector getPositionOverTimeModifier ( )

Returns the modifier used to control how particles positions change over time.
### Return value

Modifier, that controls position of particles.
## ParticleModifierVector getGravityOverTimeModifier ( )

Returns the modifier used to control how the gravity force that affects particles changes over time.
### Return value

Modifier, that controls gravity of particles.
## ParticleModifierScalar getLinearDampingOverTimeModifier ( )

Returns the modifier used to control how the linear damping of particles changes over time.
### Return value

Modifier, that controls linear damping of particles.
## void setTextureAtlasSize ( ivec2 size )

Sets the **NxN** size of the texture atlas for the particles.
### Arguments

- *ivec2* **size** - The size of the texture atlas to be used.

## ivec2 getTextureAtlasSize ( )

Returns the **NxN** size of the texture atlas for the particles.
### Return value

The size of the texture atlas.
## void setScreenSizeMode ( int mode )

Sets a new screen size mode for particles. This mode defines whether the maximum and minimum sizes of emitted particles should be limited relative to screen size or not (e.g., to avoid cases when snowflakes or raindrops obscure the view if they are too close to the camera or when they become invisible as the distance to the camera increases). Three modes are available:
- **[NONE](#SCREEN_SIZE_MODE_NONE)** - minimum and maximum sizes of particles on the screen are not limited.
- **[WIDTH](#SCREEN_SIZE_MODE_WIDTH)** - minimum and maximum sizes of particles on the screen are limited relative to screen width.
- **[HEIGHT](#SCREEN_SIZE_MODE_HEIGHT)** - minimum and maximum sizes of particles on the screen are limited relative to screen height.


### Arguments

- *int* **mode** - New screen size mode to be set for particles. One of the *[SCREEN_SIZE_MODE*](#SCREEN_SIZE_MODE)* values.

## int getScreenSizeMode ( )

Returns the current screen size mode for particles. This mode defines whether the maximum and minimum sizes of emitted particles should be limited relative to screen size or not (e.g., to avoid cases when snowflakes or raindrops obscure the view if they are too close to the camera or when they become invisible as the distance to the camera increases). Three modes are available:
- **[NONE](#SCREEN_SIZE_MODE_NONE)** - minimum and maximum sizes of particles on the screen are not limited.
- **[WIDTH](#SCREEN_SIZE_MODE_WIDTH)** - minimum and maximum sizes of particles on the screen are limited relative to screen width.
- **[HEIGHT](#SCREEN_SIZE_MODE_HEIGHT)** - minimum and maximum sizes of particles on the screen are limited relative to screen height.


### Return value

Current screen size mode for particles. One of the *[SCREEN_SIZE_MODE*](#SCREEN_SIZE_MODE)* values.
## void setScreenMinSize ( float size )

Sets a new minimum screen size for particles (minimum fraction of the screen a single particle can occupy).
### Arguments

- *float* **size** - New minimum screen size to be set for particles. Minimum fraction of the screen a single particle can occupy:

  - The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
  - The maximum value of **1** means the particle occupies the whole screen.

## float getScreenMinSize ( )

Returns the current minimum screen size for particles (minimum fraction of the screen a single particle can occupy). Any particle shall occupy at least the specified fraction of the screen.
### Return value

Current minimum screen size for particles. Minimum fraction of the screen a single particle can occupy:
- The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
- The maximum value of **1** means the particle occupies the whole screen.


## void setScreenMaxSize ( float size )

Sets a new maximum screen size for particles (maximum fraction of the screen a single particle can occupy). Any particle shall occupy no more than the specified fraction of the screen, no matter how close the camera approaches it.
### Arguments

- *float* **size** - New maximum screen size to be set for particles. Maximum fraction of the screen a single particle can occupy:

  - The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
  - The maximum value of **1** means the particle occupies the whole screen.

## float getScreenMaxSize ( )

Returns the current maximum screen size for particles (maximum fraction of the screen a single particle can occupy). Any particle shall occupy no more than the specified fraction of the screen, no matter how close the camera approaches it.
### Return value

Current maximum screen size for particles. Maximum fraction of the screen a single particle can occupy:
- The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
- The maximum value of **1** means the particle occupies the whole screen.


## void setParticlesFieldMask ( int mask )

Sets a new *Particles Field* bit mask enabling you to control interactions with *[Particles Fields](../../../api/library/objects/class.particlesfield_usc.md)*. A *Particles Field* will interact with particles generated by a Particles System if they both have matching *Particles Field* masks (one bit at least).
### Arguments

- *int* **mask** - New *Particles Field* bit mask to be set for the particle system. Integer, each bit of which is a mask.

## int getParticlesFieldMask ( )

Returns the current *Particles Field* bit mask enabling you to control interactions with *[Particles Fields](../../../api/library/objects/class.particlesfield_usc.md)*. A *Particles Field* will interact with particles generated by a Particles System if they both have matching *Particles Field* masks (one bit at least).
### Return value

Current *Particles Field* bit mask of the particle system. Integer, each bit of which is a mask.
