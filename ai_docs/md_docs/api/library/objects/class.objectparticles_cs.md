# ObjectParticles Class (CS)

**Inherits from:** Object


This class is used to create [particle systems](../../../objects/effects/particles/index.md). The particles are approximated with a sphere. They can be of different [types](#setParticlesType_int_void) (see the [details](../../../objects/effects/particles/index.md#particle_type)) and [radius](#getRadiusOverTimeModifier_ParticleModifierScalar) (that can [change](#getGrowthOverTimeModifier_ParticleModifierScalar) with time). They are emitted from different [emitters](#setEmitterType_int_void) (see the [details](../../../objects/effects/particles/index.md#emitter_shape)) with a specified [spawn rate](#setSpawnRate_float_void). The particles disappear after the set [life time period](#setLife_float_float_void) or [culled](#setCulling_int_void) when hitting other nodes. They either [collide](#setCollisionEnabled_int_void) with the outer surface of the approximation sphere or [intersect](#setPhysicsIntersectionEnabled_int_void) only by the its center.


The particle flow [direction](#getDirectionOverTimeModifier_ParticleModifierVector) can be influenced by:

- [Gravity](#getGravityOverTimeModifier_ParticleModifierVector)
- [Physicals](../../../api/library/physics/class.physical_cs.md) nodes


The particle system can also [initialized](#setWarming_int_void) before it actually appears, so that it starts to be rendered with already spawned particles.


### Usage Example


Particles parameters are set via [Particle Modifiers](../../../api/library/objects/class.particlemodifier_cs.md). Based on the modifier's type, a parameter could be a scalar(**0.8f**) or a vector (**vec4.BLUE**). It can be:


- a constant value
- a random value varying between a minimum and maximum limits
- a value defined by a [curve](../../../api/library/common/class.curve2d_cs.md)
- a random value between the upper and lower limits defined by the two [curves](../../../api/library/common/class.curve2d_cs.md) at each point of the lifetime


See [here](../../../api/library/objects/class.particlemodifier_cs.md#MODE) for more information on different modes for modifiers.


<details>
<summary>Particle System Example</summary>

```csharp
public partial class ParticleSystemCreator : Component
{
	ObjectParticles particles;
	Curve2d curve;

	private void Init()
	{
		particles = new ObjectParticles();
		particles.WorldTransform = new Mat4(new quat(0.0f, 0.0f, 0.0f, 0.0f));
		particles.GetMaterialInherit(0).SetParameterFloat4("albedo_color", vec4.GREEN);
		// enable the emitter and specify its settings
		particles.EmitterEnabled = true;
		particles.SpawnRate = 2000.0f;
		particles.SetLife(5.0f, 0.5f);
		// create a new 2d curve object
		curve = new Curve2d();
		curve.AddKey(new vec2(0.0f, 0.15f));
		curve.AddKey(new vec2(0.5f, 0.25f));
		curve.AddKey(new vec2(1.0f, 0.5f));
		curve.AddKey(new vec2(1.5f, 0.35f));
		// change the modifier's mode to the curve mode
		particles.RadiusOverTimeModifier.Mode = ParticleModifier.MODE.CURVE;
		// set the curve to define the modifier
		particles.RadiusOverTimeModifier.Curve = curve;
		// set parameters using scalar values
		particles.GrowthOverTimeModifier.ConstantMin = 0.0f;
		particles.GrowthOverTimeModifier.ConstantMax = 0.2f;
		particles.VelocityOverTimeModifier.Constant = 0.3f;
		// set the parameter using a vector value
		particles.GravityOverTimeModifier.Constant = new vec3(0.0f, 0.0f, 4.0f);

	}

	private void Update()
	{
		float time = Game.Time;
		particles.WorldTransform = new Mat4(MathLib.RotateZ(time * 64.0f) * MathLib.Translate(15.0f, 0.0f, 0.0f));

	}

	private void Shutdown()
	{
		particles.DeleteLater();
	}
}


```

</details>


If you launch the application, you get the following particle system:


![](particles.png)


### Synchronizing Particles


For image consistency in multi-channel rendering use cases, Particle Systems can have more deterministic behavior, i.e. when a particle is spawned on one PC, it can travel to another screen seamlessly.


To synchronize the particle systems across several applications, it is required to define which application is the Master one — it will count all particles and provide all related info via the network to Slaves — applications that only receive data and reproduce them.


```csharp
public partial class ParticleSystemSync : Component
{
	public ObjectParticles particles; // particles that are going to be synchronized

	bool is_master = true; // or false, if the application is a Slave
	Socket socket; // example of a socket used to send the particles data

	private void Init()
	{
		// create and open a stream
		socket = new Socket(0);
		socket.Open("127.255.255.255", 8889);

		// For every type of the application, define the particles operation mode
		if (is_master)
			particles.SyncMode = ObjectParticles.SYNC_MODE.MASTER;
		else
			particles.SyncMode = ObjectParticles.SYNC_MODE.SLAVE;

	}

	private void Update()
	{
			if (is_master)
		{
			Blob data = new Blob();
			particles.TakeSyncData(data);
			socket.Write(data.GetData(), data.GetSize());
		}
		else
		{
			Blob data = new Blob();
			socket.ReadStream(data, 1048576); // 1Mb, maximum size of the packet
			data.SeekSet(0); // Moving the pointer to the first symbol,
							// because after reading the data from the socket,
							// the pointer is at the end of the data.
			particles.ApplySyncData(data);
		}

	}

	private void Shutdown()
	{
		// closing the socket
		socket.Close();
	}
}


```


## ObjectParticles Class

### Enums

## SYNC_MODE

Synchronization mode to be used for the particle system.
| Name | Description |
|---|---|
| **NONE** = 0 | In this mode, the particle system neither provides nor takes any synchronization data. |
| **MASTER** = 1 | This mode enables storing of the particle system data used for synchronization by the slave system. |
| **SLAVE** = 2 | This mode makes a particle system take the stored synchronization data from the master particle system. |

## SCREEN_SIZE_MODE

Screen size mode for emitted particles. Can be used to limit maximum and minimum sizes of particles.
| Name | Description |
|---|---|
| **NONE** = 0 | Minimum and maximum sizes of particles on the screen are not limited. |
| **WIDTH** = 1 | Minimum and maximum sizes of particles on the screen are limited relative to screen width. |
| **HEIGHT** = 2 | Minimum and maximum sizes of particles on the screen are limited relative to screen height. |

### Properties

## 🔒︎ WorldBoundBox WorldBoundBoxParticles

The estimated world bounding box considering the changes of the particle system (velocity, length, etc.).
## 🔒︎ BoundBox BoundBoxSimulation

The exact bounding box of the particle system.
## 🔒︎ BoundBox BoundBoxParticles

The estimated bounding box considering the changes of the particle system (velocity, length, etc.).
## 🔒︎ vec3 WorldOffset

The current world offset of the local origin of coordinates of the particle system. the offset of the origin of coordinates is changed depending on the position of the particle system so that the particles are simulated near their emitter.
## 🔒︎ int NumContacts

The total number of particles collisions with other objects.
## vec3 EmitterVelocity

The current emitter velocity, which is added to the initial velocity of spawned particles. if the value equals 0, the actual velocity of emitter node will be used.
## vec3 EmitterSize

The current emitter size.
## int EmitterSync

The value indicating if a particle system emitter is synchronized to a parent particle system.
## int EmitterSequence

The current rendering order of the particle system inside the particles hierarchy.
## bool EmitterContinuous

The value indicating if additional spawn points are generated when the emitter is moved, which provides a continuous flow of particles.
## bool EmitterShift

The value indicating if the emitter spawns particles only when it is moving. the further it has moved, if compared to its position in the previous frame, the more particles will be spawned. if the emitter is not moving, there are no particles at all.
## bool EmitterBased

The value indicating if particles follow emitter transformations, i.e. the direction of their flow changes after the emitter.
## bool EmitterEnabled

The value indicating if particle emission is enabled.
## int ProceduralParenting

The current type of relationship between the particle system and a [decal](../../../api/library/decals/class.decalortho_cs.md) / [field](../../../api/library/fields/class.fieldheight_cs.md) node that uses the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


## int ProceduralPositioning

The value indicating the procedural position mode.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


## bool ProceduralRendering

The value indicating if the procedural rendering enabled or not. this feature enables rendering of particles into an orthographic decal or a field height, and can be used, for example, to create ship wake waves.
## int EmitterType

The type of the emitter.
## float Roughness

The current roughness of the particle surface.
## float Restitution

The current restitution value for particles.
## float PhysicalMass

The current mass of the particles. this value matters only for computing physical interactions.
## int PhysicalMask

The bit mask for interactions with physicals. two objects interact, if they both have matching masks.
## 🔒︎ int NumParticles

The current number of particles.
## float SpawnThreshold

The current velocity threshold for spark and random emitters. they spawn particles if velocity of the parent particles is high enough.
## float SpawnScale

The current spawn scale that enables to modulate smooth and gradual initialization of the particle system starting with the given spawn state and up to the specified spawn rate.
## float SpawnRate

The current particle spawn rate.
## ivec2 TextureAtlasSize

The **NxN** size of the texture atlas for the particles.
## int NumberPerSpawn

The current number of particles to be spawned simultaneously each time according to the [spawn rate](#setSpawnRate_float_void).
## bool ClearOnEnable

The value indicating if particle system is to be re-initialized each time it is enabled.
## int Culling

The value indicating if particles would disappear upon collision or intersection.
## bool CollisionEnabled

The value indicating if collision is detected by the outer surface of the sphere that approximates the particles. This method is slower than sphere center-based intersection detection, but more precise.
## int CollisionMask

The *[Collision](../../../principles/bit_masking/index.md#collision_mask)* Mask to be used for particles. Particles will collide with an object, if they both have matching masks.
## bool PhysicsIntersectionEnabled

The value indicating if collision is detected by the center of the sphere that approximates the particles ([physics intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)). This method is faster than sphere-based collision detection, but less precise. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
## int PhysicsIntersectionMask

The *[Physics Intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)* Mask to be used for particles. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
## int TextureAtlas

The value indicating if a diffuse texture for the particles is used as a **NxN** texture atlas.
## int VariationY

The value indicating if the initial orientation of particles diffuse texture is randomly varied along the y axis.
## int VariationX

The value indicating if the initial orientation of particles diffuse texture is randomly varied along the x axis.
## int DepthSort

The value indicating if depth sorting of particles is enabled. the depth sorting is required, if particles use alpha blending.
## float MaxWarmingTime

The Max time value for particles simulation during the warming, in seconds.
## int Warming

The value indicating if the warm start is enabled for the particles. it means that the particle system starts to be rendered with already emitted particles, rather then from a zero point.
## int ParticlesType

The type of emitted particles.
## uint Seed

The seed value used for the particles' random generator.
## ObjectParticles.SYNC_MODE SyncMode

The synchronization mode used for the particle system.
## float UpdateDistanceLimit

The distance from the camera within which the object should be updated.
## int FPSInvisible

The update rate value when the object is not rendered at all.
## int FPSVisibleShadow

The update rate value when only object shadows are rendered.
## int FPSVisibleCamera

The update rate value when the object is rendered to the viewport.
## 🔒︎ ParticleModifierScalar LinearDampingOverTimeModifier

The current linear damping of particles.
## 🔒︎ ParticleModifierVector PositionOverTimeModifier

The Modifier, that controls position of particles.
## 🔒︎ ParticleModifierVector DirectionOverTimeModifier

The Modifier, that controls direction of emission of particles.
## 🔒︎ ParticleModifierScalar VelocityOverTimeModifier

The Modifier, that controls linear velocity of particles.
## 🔒︎ ParticleModifierScalar LengthFlatteningOverTimeModifier

The Modifier, that controls flattening of Length particles.
## 🔒︎ ParticleModifierScalar LengthStretchOverTimeModifier

The Modifier, that controls stretching of Length particles.
## 🔒︎ ParticleModifierScalar GrowthOverTimeModifier

The Modifier, that controls particle growth.
## 🔒︎ ParticleModifierScalar RadiusOverTimeModifier

The Modifier, that controls particle radius values.
## 🔒︎ ParticleModifierScalar RotationOverTimeModifier

The Modifier, that controls particle angular velocity values.
## 🔒︎ ParticleModifierScalar AngleOverTimeModifier

The Modifier, that controls orientation angle values.
## int EmitterLimitPerSpawn

The Current number of particles emitted per spawn.
## 🔒︎ ParticleModifierVector GravityOverTimeModifier

The Modifier, that controls gravity of particles.
## int ParticlesFieldMask

The bit mask enabling you to control interactions with *[Particles Fields](../../../api/library/objects/class.particlesfield_cs.md)*. A *Particles Field* will interact with particles generated by a Particles System if they both have matching *Particles Field* masks (one bit at least).
## float ScreenMaxSize

The maximum screen size for particles (maximum fraction of the screen a single particle can occupy):
- The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
- The maximum value of **1** means the particle occupies the whole screen.

 Any particle shall occupy no more than the specified fraction of the screen, no matter how close the camera approaches it.
## float ScreenMinSize

The minimum screen size for particles (minimum fraction of the screen a single particle can occupy):
- The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
- The maximum value of **1** means the particle occupies the whole screen.

 Any particle shall occupy at least the specified fraction of the screen.
## ObjectParticles.SCREEN_SIZE_MODE ScreenSizeMode

The screen size mode for particles. This mode defines whether the maximum and minimum sizes of emitted particles should be limited relative to screen size or not (e.g., to avoid cases when snowflakes or raindrops obscure the view if they are too close to the camera or when they become invisible as the distance to the camera increases). Three modes are available:
- **[NONE](#SCREEN_SIZE_MODE_NONE)** - minimum and maximum sizes of particles on the screen are not limited.
- **[WIDTH](#SCREEN_SIZE_MODE_WIDTH)** - minimum and maximum sizes of particles on the screen are limited relative to screen width.
- **[HEIGHT](#SCREEN_SIZE_MODE_HEIGHT)** - minimum and maximum sizes of particles on the screen are limited relative to screen height.


### Members

---

## ObjectParticles ( )

Constructor. Creates a particle system.
## vec3 GetContactNormal ( int num )

Returns the point of the particles collision with other objects.
### Arguments

- *int* **num** - Collision point number.

### Return value

Collision point coordinates.
## Object GetContactObject ( int num )

Returns the object that collided with particles collided in a given collision point.
### Arguments

- *int* **num** - The collision point number.

### Return value

The object participated in collision.
## vec3 GetContactPoint ( int num )

Returns the normal vector for the collision point of the particles with other objects.
### Arguments

- *int* **num** - The collision point number.

### Return value

Normal vector coordinates.
## vec3 GetContactVelocity ( int num )

Returns the velocity in the collision point of the particles with other objects.
### Arguments

- *int* **num** - The collision point number.

### Return value

Velocity values for each of space dimensions.
## void SetDelay ( float mean , float spread )

Sets delay of particle system initialization relative to the parent particle one.
### Arguments

- *float* **mean** - A mean value in seconds. If a negative value is provided, 0 will be used instead.
- *float* **spread** - A spread value in seconds.

## float GetDelayMean ( )

Returns the mean value of particles initialization delay relative to the parent particle system.
### Return value

The mean value in seconds.
## float GetDelaySpread ( )

Returns the spread value of particles initialization delay relative to the parent particle system.
### Return value

The spread value in seconds.
## void SetDuration ( float mean , float spread )

Sets a duration of each particle emission in seconds.
### Arguments

- *float* **mean** - Mean value in seconds. If a negative value is provided, 0 will be used instead.
- *float* **spread** - Spread value in seconds.

## float GetDurationMean ( )

Returns the current mean value of particle emission intervals.
### Return value

The mean value in seconds.
## float GetDurationSpread ( )

Returns the current spread value of particle emission intervals.
### Return value

The spread value in seconds.
## void SetLife ( float mean , float spread )

Sets a lifetime duration of particles in seconds.
### Arguments

- *float* **mean** - A mean value in seconds. If a too small value is provided, **1E-6** will be used instead.
- *float* **spread** - A spread value in seconds.

## float GetLifeMean ( )

Returns the current mean value of particle lifetime duration.
### Return value

The mean value in seconds.
## float GetLifeSpread ( )

Returns the current spread value of particle lifetime duration.
### Return value

The spread value in seconds.
## vec3 GetParticlePosition ( int num )

Returns the position of a given particle.
### Arguments

- *int* **num** - The particle number.

### Return value

Position coordinates for the particle.
## float GetParticleRadius ( int num )

Returns the radius of a given particle.
### Arguments

- *int* **num** - The particle number.

### Return value

Radius of the particle.
## void GetParticleTransforms ( mat4[] OUT_transforms )

Returns transformation matrices for spawned particles.
### Arguments

- *mat4[]* **OUT_transforms** - Array to which the transformation matrices will be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## vec3 GetParticleVelocity ( int num )

Returns the velocity vector for a specified particle.
### Arguments

- *int* **num** - The particle number.

### Return value

The velocity vector.
## void SetPeriod ( float mean , float spread )

Sets an interval of emitter inactivity in seconds.
### Arguments

- *float* **mean** - A mean value in seconds. If a negative value is provided, 0 will be used instead.
- *float* **spread** - A spread value in seconds.

## float GetPeriodMean ( )

Returns the current mean value of emitter inactivity intervals.
### Return value

The mean value in seconds.
## float GetPeriodSpread ( )

Returns the current spread value of emitter inactivity intervals.
### Return value

The spread value in seconds.
## void SetProceduralTextureResolution ( vec3 res )

Sets the resolution of the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Arguments

- *vec3* **res** - Resolution of the texture.

## vec3 GetProceduralTextureResolution ( )

Returns the resolution of the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Return value

Resolution of the texture.
## void AddEmitterSpark ( vec3 point , vec3 normal , vec3 velocity )

Adds a spark emitter in the given point.
### Arguments

- *vec3* **point** - Point for sparks emission.
- *vec3* **normal** - Normal vector at the point of spark emission.
- *vec3* **velocity** - Velocity in the point of spark emission (velocity of source particles or node by contact).

## void ClearParticles ( )

Deletes all particles spawned by the emitter.
## static int type ( )

Returns the type of the object.
### Return value

[Object Particles](../../../api/library/nodes/class.node_cs.md#OBJECT_PARTICLES) type identifier.
## bool SaveStateSelf ( Stream stream )

Saves the object's state to the stream.
> **Notice:** This method saves all object's parameters


Saving into the stream requires creating a blob to save into. To restore the saved state the [RestoreStateSelf()](#restoreStateSelf_Stream_int) method is used:


```csharp
// initialize a object and set its state
//...//

// save state
Blob blob_state = new Blob();
object.SaveStateSelf(blob_state);

// change the state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
object.RestoreStateSelf(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true on success; otherwise, false.
## bool RestoreStateSelf ( Stream stream )

Restores the object's state from the stream.
> **Notice:** This method restores all object's parameters.


Restoring from the stream requires creating a blob to save into and saving the state using the [saveStateSelf()](#saveStateSelf_Stream_int) method:


```csharp
// initialize a object and set its state
//...//

// save state
Blob blob_state = new Blob();
object.SaveStateSelf(blob_state);

// change the state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
object.RestoreStateSelf(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream instance.

### Return value

true on success; otherwise, false.
## void TakeSyncData ( Stream stream )

Writes particle synchronization data to the specified stream. This method should be used by the particle system with the master [sync mode](#setSyncMode_int_void).
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which particle synchronization data is to be written.

## void ApplySyncData ( Stream stream )

Reads particle synchronization data from the specified stream and applies it to the particle system. This method should be used by the particle system with the slave [sync mode](#setSyncMode_int_void).
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream with particle synchronization data to be applied.

## ParticleModifierScalar GetLinearDampingOverTimeModifier ( )

Returns the modifier used to control how the linear damping of particles changes over time.
### Return value

Modifier, that controls linear damping of particles.
