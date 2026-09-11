# ObjectParticles Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create [particle systems](../../../objects/effects/particles/index.md). The particles are approximated with a sphere. They can be of different [types](#setParticlesType_int_void) (see the [details](../../../objects/effects/particles/index.md#particle_type)) and [radius](#getRadiusOverTimeModifier_ParticleModifierScalar) (that can [change](#getGrowthOverTimeModifier_ParticleModifierScalar) with time). They are emitted from different [emitters](#setEmitterType_int_void) (see the [details](../../../objects/effects/particles/index.md#emitter_shape)) with a specified [spawn rate](#setSpawnRate_float_void). The particles disappear after the set [life time period](#setLife_float_float_void) or [culled](#setCulling_int_void) when hitting other nodes. They either [collide](#setCollisionEnabled_int_void) with the outer surface of the approximation sphere or [intersect](#setPhysicsIntersectionEnabled_int_void) only by the its center.


The particle flow [direction](#getDirectionOverTimeModifier_ParticleModifierVector) can be influenced by:

- [Gravity](#getGravityOverTimeModifier_ParticleModifierVector)
- [Physicals](../../../api/library/physics/class.physical_cpp.md) nodes


The particle system can also [initialized](#setWarming_int_void) before it actually appears, so that it starts to be rendered with already spawned particles.


### Usage Example


In the following example, we create a new particle system, specify its settings by means of C++ API.

 Prior KnowledgeIt is supposed that you have already [created an empty C++ project](../../../code/cpp/application.md) by using UNIGINE SDK Browser.
Particles parameters are set via [Particle Modifiers](../../../api/library/objects/class.particlemodifier_cpp.md). Based on the modifier's type, a parameter could be a scalar (radius, velocity, etc.) or a vector (direction, position, color, etc.). The modifier's mode defines a parameter by:


- a constant value
- a random value varying between a minimum and maximum limits
- a value defined by a [curve](../../../api/library/common/class.curve2d_cpp.md)
- a random value between the upper and lower limits defined by the two [curves](../../../api/library/common/class.curve2d_cpp.md) at each point of the lifetime


See [here](../../../api/library/objects/class.particlemodifier_cpp.md#MODE) for more information on different modes for modifiers.


<details>
<summary>Particle System Example</summary>

```cpp
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineObjects.h>

class AppWorldLogic : public Unigine::WorldLogic
{
	public:

	private:
		// define smart pointers to particles and sun nodes
		Unigine::ObjectParticlesPtr particles;
		Unigine::NodePtr sun;
		Unigine::Curve2dPtr curve;
};

#endif // __APP_WORLD_LOGIC_H__

```


```cpp
#include "AppWorldLogic.h"
#include "UnigineEditor.h"
#include "UnigineGame.h"

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{
	particles = ObjectParticles::create();

	// set world transform to the particle system, specify its material and material albedo parameter
	particles->setWorldTransform(Mat4(quat(0.0f, 0.0f, 0.0f, 0.0f)));
	particles->getMaterialInherit(0)->setParameterFloat4("albedo_color", vec4(0.8f, 1.0f, 0.0f, 1.0f));

	// enable the emitter and specify its settings
	particles->setEmitterEnabled(1);
	particles->setSpawnRate(2000.0f);
	particles->setLife(5.0f, 0.5f);

	// create a new 2d curve object
	curve = Curve2d::create();
	curve->addKey(vec2(0.0f, 0.15f));
	curve->addKey(vec2(0.5f, 0.25f));
	curve->addKey(vec2(1.0f, 0.5f));
	curve->addKey(vec2(1.5f, 0.35f));
	// change the modifier's mode to the curve mode
	particles->getRadiusOverTimeModifier()->setMode(ParticleModifier::MODE_CURVE);
	// set the curve to define the modifier
	particles->getRadiusOverTimeModifier()->setCurve(curve);

	// set parameters using scalar values
	particles->getGrowthOverTimeModifier()->setConstantMin(0.0f);
	particles->getGrowthOverTimeModifier()->setConstantMax(0.2f);
	particles->getVelocityOverTimeModifier()->setConstant(0.3f);
	// set the parameter using a vector value
	particles->getGravityOverTimeModifier()->setConstant(vec3(0.0f, 0.0f, 4.0f));

	// disable the sun node
	sun = World::getNodeByName("sun");
	sun->setEnabled(0);

	return 1;
}

int AppWorldLogic::update()
{

	// set transformation for particle system
	float time = Game::getTime();
	particles->setWorldTransform(Mat4(rotateZ(time * 64.0f) * translate(15.0f, 0.0f, 0.0f)));

	return 1;
}


```

</details>


If you launch the application, you get the following particle system:


![](particles.png)


### Synchronizing Particles


For image consistency in multi-channel rendering use cases, Particle Systems can have more deterministic behavior, i.e. when a particle is spawned on one PC, it can travel to another screen seamlessly.


To synchronize the particle systems of several applications, it is required to define which application is the Master one � it will count all particles and provide all related info via the network to Slaves � applications that only receive data and reproduce them.


```cpp
// define smart pointer to particles
ObjectParticlesPtr particles;

bool is_master = true; // or false, if the application is a Slave
SocketPtr socket; // example of a socket used to send the particles data

int AppWorldLogic::init()
{
	particles = ObjectParticles::create();
	//and set the required parameters of the particles system

	// create and open a stream
	socket = Socket::create(Socket::SOCKET_TYPE_STREAM);
	socket->open("127.255.255.255", 8889);

	// For every type of the application, define the particles operation mode
	if (is_master)
		particles->setSyncMode(ObjectParticles::SYNC_MODE_MASTER);
	else
		particles->setSyncMode(ObjectParticles::SYNC_MODE_SLAVE);

	return 1;
}

int AppWorldLogic::update()
{


	if (is_master)
	{
		BlobPtr data = Blob::create();
		particles->takeSyncData(data);
		socket->write(data->getData(), data->getSize());
	}
	else
	{
		BlobPtr data = Blob::create();
		socket->readStream(data, 1048576); // 1Mb, maximum size of the packet
		data->seekSet(0); // Moving the pointer to the first symbol,
						  // because after reading the data from the socket,
						  // the pointer is at the end of the data.
		particles->applySyncData(data);
	}

	return 1;
}

int AppWorldLogic::shutdown()
{
	// closing the socket
	socket->close();

	// destroying the socket
	socket.clear();
	return 1;
}


```


## ObjectParticles Class

### Enums

## SYNC_MODE

Synchronization mode to be used for the particle system.
| Name | Description |
|---|---|
| **SYNC_MODE_NONE** = 0 | In this mode, the particle system neither provides nor takes any synchronization data. |
| **SYNC_MODE_MASTER** = 1 | This mode enables storing of the particle system data used for synchronization by the slave system. |
| **SYNC_MODE_SLAVE** = 2 | This mode makes a particle system take the stored synchronization data from the master particle system. |

## SCREEN_SIZE_MODE

Screen size mode for emitted particles. Can be used to limit maximum and minimum sizes of particles.
| Name | Description |
|---|---|
| **SCREEN_SIZE_MODE_NONE** = 0 | Minimum and maximum sizes of particles on the screen are not limited. |
| **SCREEN_SIZE_MODE_WIDTH** = 1 | Minimum and maximum sizes of particles on the screen are limited relative to screen width. |
| **SCREEN_SIZE_MODE_HEIGHT** = 2 | Minimum and maximum sizes of particles on the screen are limited relative to screen height. |

### Members

## Math:: WorldBoundBox getWorldBoundBoxParticles () const

Returns the current estimated world bounding box considering the changes of the particle system (velocity, length, etc.).
### Return value

Current estimated world bounding box considering the changes of the particle system (velocity, length, etc
## Math:: BoundBox getBoundBoxSimulation () const

Returns the current exact bounding box of the particle system.
### Return value

Current exact bounding box of the particle system
## Math:: BoundBox getBoundBoxParticles () const

Returns the current estimated bounding box considering the changes of the particle system (velocity, length, etc.).
### Return value

Current estimated bounding box considering the changes of the particle system (velocity, length, etc
## Math:: Vec3 getWorldOffset () const

Returns the current world offset of the local origin of coordinates of the particle system. the offset of the origin of coordinates is changed depending on the position of the particle system so that the particles are simulated near their emitter.
### Return value

Current world offset of the local origin of coordinates of the particle system
## int getNumContacts () const

Returns the current total number of particles collisions with other objects.
### Return value

Current total number of particles collisions with other objects
## void setEmitterVelocity ( const Math:: vec3 & velocity )

Sets a new emitter velocity, which is added to the [initial velocity](#getVelocityOverTimeModifier_ParticleModifierScalar) of spawned particles. if the value equals 0, the actual velocity of emitter node will be used.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **velocity** - The emitter velocity, which is added to the initial velocity of spawned particles

## Math:: vec3 getEmitterVelocity () const

Returns the current emitter velocity, which is added to the [initial velocity](#getVelocityOverTimeModifier_ParticleModifierScalar) of spawned particles. if the value equals 0, the actual velocity of emitter node will be used.
### Return value

Current emitter velocity, which is added to the initial velocity of spawned particles
## void setEmitterSize ( const Math:: vec3 & size )

Sets a new emitter size. Depending on the type of the emitter, this value is interpreted as follows:
- [EMITTER_POINT](#EMITTER_POINT), [EMITTER_SPARK](#EMITTER_SPARK), [EMITTER_RANDOM](#EMITTER_RANDOM): all vector components are ignored.
- [EMITTER_SPHERE](#EMITTER_SPHERE): the first vector component is the radius of the sphere.
- [EMITTER_CYLINDER](#EMITTER_CYLINDER): the first vector component is the radius of the cylinder, the second vector component is the height of the cylinder.
- [EMITTER_BOX](#EMITTER_BOX): all vector components are interpreted as box dimensions (*x*, *y*, *z*).

 If negative values are provided, 0 will be used instead of them.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The emitter size

## Math:: vec3 getEmitterSize () const

Returns the current emitter size. Depending on the type of the emitter, this value is interpreted as follows:
- [EMITTER_POINT](#EMITTER_POINT), [EMITTER_SPARK](#EMITTER_SPARK), [EMITTER_RANDOM](#EMITTER_RANDOM): all vector components are ignored.
- [EMITTER_SPHERE](#EMITTER_SPHERE): the first vector component is the radius of the sphere.
- [EMITTER_CYLINDER](#EMITTER_CYLINDER): the first vector component is the radius of the cylinder, the second vector component is the height of the cylinder.
- [EMITTER_BOX](#EMITTER_BOX): all vector components are interpreted as box dimensions (*x*, *y*, *z*).

 If negative values are provided, 0 will be used instead of them.
### Return value

Current emitter size
## void setEmitterSync ( int sync )

Sets a new value indicating if a particle system emitter is synchronized to a parent particle system.
### Arguments

- *int* **sync** - The value indicating if a particle system emitter is synchronized to a parent particle system

## int getEmitterSync () const

Returns the current value indicating if a particle system emitter is synchronized to a parent particle system.
### Return value

Current value indicating if a particle system emitter is synchronized to a parent particle system
## void setEmitterSequence ( int sequence )

Sets a new rendering order of the particle system inside the particles hierarchy. Particle systems with the lowest order number are rendered first.
### Arguments

- *int* **sequence** - The rendering order of the particle system inside the particles hierarchy

## int getEmitterSequence () const

Returns the current rendering order of the particle system inside the particles hierarchy. Particle systems with the lowest order number are rendered first.
### Return value

Current rendering order of the particle system inside the particles hierarchy
## void setEmitterContinuous ( bool continuous )

Sets a new value indicating if additional spawn points are generated when the emitter is moved, which provides a continuous flow of particles.
### Arguments

- *bool* **continuous** - value indicating if additional spawn points are generated when the emitter is moved, which provides a continuous flow of particles

## bool isEmitterContinuous () const

Returns the current value indicating if additional spawn points are generated when the emitter is moved, which provides a continuous flow of particles.
### Return value

value indicating if additional spawn points are generated when the emitter is moved, which provides a continuous flow of particles
## void setEmitterShift ( bool shift )

Sets a new value indicating if the emitter spawns particles only when it is moving. the further it has moved, if compared to its position in the previous frame, the more particles will be spawned. if the emitter is not moving, there are no particles at all.
### Arguments

- *bool* **shift** - value indicating if the emitter spawns particles only when it is moving

## bool isEmitterShift () const

Returns the current value indicating if the emitter spawns particles only when it is moving. the further it has moved, if compared to its position in the previous frame, the more particles will be spawned. if the emitter is not moving, there are no particles at all.
### Return value

value indicating if the emitter spawns particles only when it is moving
## void setEmitterBased ( bool based )

Sets a new value indicating if particles follow emitter transformations, i.e. the direction of their flow changes after the emitter.
### Arguments

- *bool* **based** - value indicating if particles follow emitter transformations

## bool isEmitterBased () const

Returns the current value indicating if particles follow emitter transformations, i.e. the direction of their flow changes after the emitter.
### Return value

value indicating if particles follow emitter transformations
## void setEmitterEnabled ( bool enabled )

Sets a new value indicating if particle emission is enabled.
### Arguments

- *bool* **enabled** - value indicating if particle emission is enabled

## bool isEmitterEnabled () const

Returns the current value indicating if particle emission is enabled.
### Return value

value indicating if particle emission is enabled
## void setProceduralParenting ( int parenting )

Sets a new type of relationship between the particle system and a [decal](../../../api/library/decals/class.decalortho_cpp.md) / [field](../../../api/library/fields/class.fieldheight_cpp.md) node that uses the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.

### Arguments

- *int* **parenting** - The type of relationship between the particle system and a decal / field node that uses the procedural texture. Procedural rendering must be enabled

## int getProceduralParenting () const

Returns the current type of relationship between the particle system and a [decal](../../../api/library/decals/class.decalortho_cpp.md) / [field](../../../api/library/fields/class.fieldheight_cpp.md) node that uses the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.

### Return value

Current type of relationship between the particle system and a decal / field node that uses the procedural texture. Procedural rendering must be enabled
## void setProceduralPositioning ( int positioning )

Sets a new value indicating the procedural position mode. Can be one of the following:
- PROCEDURAL_POSITIONING_MANUAL = 0 - position of a child decal/field node, that uses the procedural texture, can be changed manually.
- PROCEDURAL_POSITIONING_AUTO = 1 - position of a child decal/field node, that uses the procedural texture, is automatically defined by the position of particle system and cannot be changed manually.


> **Notice:** - Positioning mode can be set only when the particle system is a parent of a decal/field node that uses the procedural texture ([parenting mode](#setProceduralParenting_int_void) is set to 0).
> - [Procedural rendering](#setProceduralRendering_int_void) must be enabled.

### Arguments

- *int* **positioning** - The value indicating the procedural position mode

## int getProceduralPositioning () const

Returns the current value indicating the procedural position mode. Can be one of the following:
- PROCEDURAL_POSITIONING_MANUAL = 0 - position of a child decal/field node, that uses the procedural texture, can be changed manually.
- PROCEDURAL_POSITIONING_AUTO = 1 - position of a child decal/field node, that uses the procedural texture, is automatically defined by the position of particle system and cannot be changed manually.


> **Notice:** - Positioning mode can be set only when the particle system is a parent of a decal/field node that uses the procedural texture ([parenting mode](#setProceduralParenting_int_void) is set to 0).
> - [Procedural rendering](#setProceduralRendering_int_void) must be enabled.

### Return value

Current value indicating the procedural position mode
## void setProceduralRendering ( bool rendering )

Sets a new value indicating if the procedural rendering enabled or not. this feature enables rendering of particles into an [orthographic decal](../../../api/library/decals/class.decalortho_cpp.md) or a [field height](../../../api/library/fields/class.fieldheight_cpp.md), and can be used, for example, to create ship wake waves.
### Arguments

- *bool* **rendering** - value indicating if the procedural rendering enabled or not

## bool isProceduralRendering () const

Returns the current value indicating if the procedural rendering enabled or not. this feature enables rendering of particles into an [orthographic decal](../../../api/library/decals/class.decalortho_cpp.md) or a [field height](../../../api/library/fields/class.fieldheight_cpp.md), and can be used, for example, to create ship wake waves.
### Return value

value indicating if the procedural rendering enabled or not
## void setEmitterType ( int type )

Sets a new [type](../../../objects/effects/particles/index.md#emitter_shape) of the emitter. One of the [OBJECT_PARTICLES_EMITTER_*](#EMITTER_BOX) variables.
### Arguments

- *int* **type** - The type of the emitter

## int getEmitterType () const

Returns the current [type](../../../objects/effects/particles/index.md#emitter_shape) of the emitter. One of the [OBJECT_PARTICLES_EMITTER_*](#EMITTER_BOX) variables.
### Return value

Current type of the emitter
## void setRoughness ( float roughness )

Sets a new roughness of the particle surface.
### Arguments

- *float* **roughness** - The roughness of the particle surface

## float getRoughness () const

Returns the current roughness of the particle surface.
### Return value

Current roughness of the particle surface
## void setRestitution ( float restitution )

Sets a new restitution value for particles. The provided value will be saturated in the range **[0; 1]**.
### Arguments

- *float* **restitution** - The restitution value for particles

## float getRestitution () const

Returns the current restitution value for particles. The provided value will be saturated in the range **[0; 1]**.
### Return value

Current restitution value for particles
## void setPhysicalMass ( float mass )

Sets a new mass of the particles. this value matters only for computing physical interactions.
### Arguments

- *float* **mass** - The mass of the particles

## float getPhysicalMass () const

Returns the current mass of the particles. this value matters only for computing physical interactions.
### Return value

Current mass of the particles
## void setPhysicalMask ( int mask )

Sets a new bit mask for interactions with [physicals](../../../api/library/physics/class.physical_cpp.md). two objects interact, if they both have matching masks.
### Arguments

- *int* **mask** - The bit mask for interactions with physicals

## int getPhysicalMask () const

Returns the current bit mask for interactions with [physicals](../../../api/library/physics/class.physical_cpp.md). two objects interact, if they both have matching masks.
### Return value

Current bit mask for interactions with physicals
## int getNumParticles () const

Returns the current number of particles.
### Return value

Current number of particles
## void setSpawnThreshold ( float threshold )

Sets a new velocity threshold for spark and random emitters. they spawn particles if velocity of the parent particles is high enough.
### Arguments

- *float* **threshold** - The velocity threshold for spark and random emitters

## float getSpawnThreshold () const

Returns the current velocity threshold for spark and random emitters. they spawn particles if velocity of the parent particles is high enough.
### Return value

Current velocity threshold for spark and random emitters
## void setSpawnScale ( float scale )

Sets a new spawn scale that enables to modulate smooth and gradual initialization of the particle system starting with the given spawn state and up to the specified spawn rate. The provided value is clipped to range **[0;1]**. By the value of 0, there are no spawned particles at the start. By the value of 1, the system is initialized with the specified spawn rate.
### Arguments

- *float* **scale** - The spawn scale that enables to modulate smooth and gradual initialization of the particle system starting with the given spawn state and up to the specified spawn rate

## float getSpawnScale () const

Returns the current spawn scale that enables to modulate smooth and gradual initialization of the particle system starting with the given spawn state and up to the specified spawn rate. The provided value is clipped to range **[0;1]**. By the value of 0, there are no spawned particles at the start. By the value of 1, the system is initialized with the specified spawn rate.
### Return value

Current spawn scale that enables to modulate smooth and gradual initialization of the particle system starting with the given spawn state and up to the specified spawn rate
## void setSpawnRate ( float rate )

Sets a new particle spawn rate.
### Arguments

- *float* **rate** - The particle spawn rate

## float getSpawnRate () const

Returns the current particle spawn rate.
### Return value

Current particle spawn rate
## void setTextureAtlasSize ( const Math:: ivec2 & size )

Sets a new **NxN** size of the texture atlas for the particles.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md)&* **size** - The **NxN** size of the texture atlas for the particles

## Math:: ivec2 getTextureAtlasSize () const

Returns the current **NxN** size of the texture atlas for the particles.
### Return value

Current **NxN** size of the texture atlas for the particles
## void setNumberPerSpawn ( int spawn )

Sets a new number of particles to be spawned simultaneously each time according to the [spawn rate](#setSpawnRate_float_void).
### Arguments

- *int* **spawn** - The number of particles to be spawned simultaneously each time according to the spawn rate

## int getNumberPerSpawn () const

Returns the current number of particles to be spawned simultaneously each time according to the [spawn rate](#setSpawnRate_float_void).
### Return value

Current number of particles to be spawned simultaneously each time according to the spawn rate
## void setClearOnEnable ( bool enable )

Sets a new value indicating if particle system is to be re-initialized each time it is enabled. When this option is disabled, turning on the particle system will restore the state it had before it was turned off.
### Arguments

- *bool* **enable** - value indicating if particle system is to be re-initialized each time it is enabled

## bool isClearOnEnable () const

Returns the current value indicating if particle system is to be re-initialized each time it is enabled. When this option is disabled, turning on the particle system will restore the state it had before it was turned off.
### Return value

value indicating if particle system is to be re-initialized each time it is enabled
## void setCulling ( int culling )

Sets a new value indicating if particles would disappear upon collision or intersection.
### Arguments

- *int* **culling** - The value indicating if particles would disappear upon collision or intersection

## int getCulling () const

Returns the current value indicating if particles would disappear upon collision or intersection.
### Return value

Current value indicating if particles would disappear upon collision or intersection
## void setCollisionEnabled ( bool enabled )

Sets a new value indicating if collision is detected by the outer surface of the sphere that approximates the particles. This method is slower than sphere center-based intersection detection, but more precise.
### Arguments

- *bool* **enabled** - value indicating if collision is detected by the outer surface of the sphere that approximates the particles

## bool isCollisionEnabled () const

Returns the current value indicating if collision is detected by the outer surface of the sphere that approximates the particles. This method is slower than sphere center-based intersection detection, but more precise.
### Return value

value indicating if collision is detected by the outer surface of the sphere that approximates the particles
## void setCollisionMask ( int mask )

Sets a new *[Collision](../../../principles/bit_masking/index.md#collision_mask)* Mask to be used for particles. Particles will collide with an object, if they both have matching masks.
### Arguments

- *int* **mask** - The collision mask used for particles

## int getCollisionMask () const

Returns the current *[Collision](../../../principles/bit_masking/index.md#collision_mask)* Mask to be used for particles. Particles will collide with an object, if they both have matching masks.
### Return value

Current collision mask used for particles
## void setPhysicsIntersectionEnabled ( bool enabled )

Sets a new value indicating if collision is detected by the center of the sphere that approximates the particles ([physics intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)). This method is faster than sphere-based collision detection, but less precise. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
### Arguments

- *bool* **enabled** - value indicating if collision is detected by the center of the sphere that approximates the particles (physics intersection)

## bool isPhysicsIntersectionEnabled () const

Returns the current value indicating if collision is detected by the center of the sphere that approximates the particles ([physics intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)). This method is faster than sphere-based collision detection, but less precise. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
### Return value

value indicating if collision is detected by the center of the sphere that approximates the particles (physics intersection)
## void setPhysicsIntersectionMask ( int mask )

Sets a new *[Physics Intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)* Mask to be used for particles. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
### Arguments

- *int* **mask** - The physics intersection mask used for particles

## int getPhysicsIntersectionMask () const

Returns the current *[Physics Intersection](../../../principles/bit_masking/index.md#physics_intersection_mask)* Mask to be used for particles. Physics intersections are detected only for matching [bit masks](../../../principles/bit_masking/index.md#physics_intersection_mask).
### Return value

Current physics intersection mask used for particles
## void setTextureAtlas ( int atlas )

Sets a new value indicating if a diffuse texture for the particles is used as a **NxN** texture atlas.
### Arguments

- *int* **atlas** - The value indicating if a diffuse texture for the particles is used as a NxN texture atlas

## int getTextureAtlas () const

Returns the current value indicating if a diffuse texture for the particles is used as a **NxN** texture atlas.
### Return value

Current value indicating if a diffuse texture for the particles is used as a NxN texture atlas
## void setVariationY ( int y )

Sets a new value indicating if the initial orientation of particles diffuse texture is randomly varied along the y axis.
### Arguments

- *int* **y** - The value indicating if the initial orientation of particles diffuse texture is randomly varied along the y axis

## int getVariationY () const

Returns the current value indicating if the initial orientation of particles diffuse texture is randomly varied along the y axis.
### Return value

Current value indicating if the initial orientation of particles diffuse texture is randomly varied along the y axis
## void setVariationX ( int x )

Sets a new value indicating if the initial orientation of particles diffuse texture is randomly varied along the x axis.
### Arguments

- *int* **x** - The value indicating if the initial orientation of particles diffuse texture is randomly varied along the x axis

## int getVariationX () const

Returns the current value indicating if the initial orientation of particles diffuse texture is randomly varied along the x axis.
### Return value

Current value indicating if the initial orientation of particles diffuse texture is randomly varied along the x axis
## void setDepthSort ( int sort )

Sets a new value indicating if depth sorting of particles is enabled. the depth sorting is required, if particles use alpha blending.
### Arguments

- *int* **sort** - The value indicating if depth sorting of particles is enabled

## int getDepthSort () const

Returns the current value indicating if depth sorting of particles is enabled. the depth sorting is required, if particles use alpha blending.
### Return value

Current value indicating if depth sorting of particles is enabled
## void setMaxWarmingTime ( float time )

Sets a new Max time value for particles simulation during the warming, in seconds.
### Arguments

- *float* **time** - The Max time value for particles simulation during the warming, in seconds

## float getMaxWarmingTime () const

Returns the current Max time value for particles simulation during the warming, in seconds.
### Return value

Current Max time value for particles simulation during the warming, in seconds
## void setWarming ( int warming )

Sets a new value indicating if the warm start is enabled for the particles. it means that the particle system starts to be rendered with already emitted particles, rather then from a zero point.
### Arguments

- *int* **warming** - The value indicating if the warm start is enabled for the particles

## int getWarming () const

Returns the current value indicating if the warm start is enabled for the particles. it means that the particle system starts to be rendered with already emitted particles, rather then from a zero point.
### Return value

Current value indicating if the warm start is enabled for the particles
## void setParticlesType ( int type )

Sets a new type of emitted particles. One of the [OBJECT_PARTICLES_TYPE_*](#TYPE_BILLBOARD) variables.
### Arguments

- *int* **type** - The type of emitted particles

## int getParticlesType () const

Returns the current type of emitted particles. One of the [OBJECT_PARTICLES_TYPE_*](#TYPE_BILLBOARD) variables.
### Return value

Current type of emitted particles
## void setSeed ( unsigned int seed )

Sets a new seed value used for the particles' random generator.
### Arguments

- *unsigned int* **seed** - The seed value used for the particles' random generator

## unsigned int getSeed () const

Returns the current seed value used for the particles' random generator.
### Return value

Current seed value used for the particles' random generator
## void setSyncMode ( ObjectParticles::SYNC_MODE mode )

Sets a new synchronization mode used for the particle system. One of the [SYNC_MODE](#SYNC_MODE) values.
### Arguments

- *[ObjectParticles::SYNC_MODE](../../../api/library/objects/class.objectparticles_cpp.md#SYNC_MODE)* **mode** - The synchronization mode used for the particle system

## ObjectParticles::SYNC_MODE getSyncMode () const

Returns the current synchronization mode used for the particle system. One of the [SYNC_MODE](#SYNC_MODE) values.
### Return value

Current synchronization mode used for the particle system
## void setUpdateDistanceLimit ( float limit )

Sets a new distance from the camera within which the object should be updated. The default value is 1000 units.
### Arguments

- *float* **limit** - The distance from the camera within which the object should be updated

## float getUpdateDistanceLimit () const

Returns the current distance from the camera within which the object should be updated. The default value is 1000 units.
### Return value

Current distance from the camera within which the object should be updated
## void setFPSInvisible ( int fpsinvisible )

Sets a new update rate value when the object is not rendered at all. The default value is 0 fps.
### Arguments

- *int* **fpsinvisible** - The update rate value when the object is not rendered at all

## int getFPSInvisible () const

Returns the current update rate value when the object is not rendered at all. The default value is 0 fps.
### Return value

Current update rate value when the object is not rendered at all
## void setFPSVisibleShadow ( int shadow )

Sets a new update rate value when only object shadows are rendered. The default value is 30 fps.
### Arguments

- *int* **shadow** - The update rate value when only object shadows are rendered

## int getFPSVisibleShadow () const

Returns the current update rate value when only object shadows are rendered. The default value is 30 fps.
### Return value

Current update rate value when only object shadows are rendered
## void setFPSVisibleCamera ( int camera )

Sets a new update rate value when the object is rendered to the viewport. The default value is infinity.
### Arguments

- *int* **camera** - The update rate value when the object is rendered to the viewport

## int getFPSVisibleCamera () const

Returns the current update rate value when the object is rendered to the viewport. The default value is infinity.
### Return value

Current update rate value when the object is rendered to the viewport
## Ptr <ParticleModifierScalar> getLinearDampingOverTimeModifier () const

Returns the current linear damping of particles.
### Return value

Current linear damping of particles
## Ptr <ParticleModifierVector> getPositionOverTimeModifier () const

Returns the current modifier that controls position of particles.
### Return value

Current modifier that controls position of particles
## Ptr <ParticleModifierVector> getDirectionOverTimeModifier () const

Returns the current modifier that controls [direction](../../../objects/effects/particles/index.md#direction) of emission of particles.
### Return value

Current modifier that controls direction of emission of particles
## Ptr <ParticleModifierScalar> getVelocityOverTimeModifier () const

Returns the current modifier that controls linear [velocity](../../../objects/effects/particles/index.md#velocity) of particles.
### Return value

Current modifier that controls linear velocity of particles
## Ptr <ParticleModifierScalar> getLengthFlatteningOverTimeModifier () const

Returns the current modifier that controls [flattening](../../../objects/effects/particles/index.md#length_flattening) of Length particles.
### Return value

Current modifier that controls flattening of Length particles
## Ptr <ParticleModifierScalar> getLengthStretchOverTimeModifier () const

Returns the current modifier that controls [stretching](../../../objects/effects/particles/index.md#length_stretch) of Length particles.
### Return value

Current modifier that controls stretching of Length particles
## Ptr <ParticleModifierScalar> getGrowthOverTimeModifier () const

Returns the current modifier that controls particle [growth](../../../objects/effects/particles/index.md#increase_in_radius).
### Return value

Current modifier that controls particle growth
## Ptr <ParticleModifierScalar> getRadiusOverTimeModifier () const

Returns the current modifier that controls [particle radius](../../../objects/effects/particles/index.md#radius) values.
### Return value

Current modifier that controls particle radius values
## Ptr <ParticleModifierScalar> getRotationOverTimeModifier () const

Returns the current modifier that controls [particle angular velocity](../../../objects/effects/particles/index.md#angle) values.
### Return value

Current modifier that controls particle angular velocity values
## Ptr <ParticleModifierScalar> getAngleOverTimeModifier () const

Returns the current modifier that controls [orientation angle](../../../objects/effects/particles/index.md#angle) values.
### Return value

Current modifier that controls orientation angle values
## void setEmitterLimitPerSpawn ( int spawn )

Sets a new [number of particles](../../../objects/effects/particles/index.md#number_per_spawn) emitted per spawn.
### Arguments

- *int* **spawn** - The number of particles emitted per spawn

## int getEmitterLimitPerSpawn () const

Returns the current [number of particles](../../../objects/effects/particles/index.md#number_per_spawn) emitted per spawn.
### Return value

Current number of particles emitted per spawn
## Ptr <ParticleModifierVector> getGravityOverTimeModifier () const

Returns the current modifier that controls gravity of particles.
### Return value

Current modifier that controls gravity of particles
## void setParticlesFieldMask ( int mask )

Sets a new bit mask enabling you to control interactions with *[Particles Fields](../../../api/library/objects/class.particlesfield_cpp.md)*. A *Particles Field* will interact with particles generated by a Particles System if they both have matching *Particles Field* masks (one bit at least).
### Arguments

- *int* **mask** - The bit mask enabling you to control interactions with Particles Fields

## int getParticlesFieldMask () const

Returns the current bit mask enabling you to control interactions with *[Particles Fields](../../../api/library/objects/class.particlesfield_cpp.md)*. A *Particles Field* will interact with particles generated by a Particles System if they both have matching *Particles Field* masks (one bit at least).
### Return value

Current bit mask enabling you to control interactions with Particles Fields
## void setScreenMaxSize ( float size )

Sets a new maximum screen size for particles (maximum fraction of the screen a single particle can occupy):
- The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
- The maximum value of **1** means the particle occupies the whole screen.

 Any particle shall occupy no more than the specified fraction of the screen, no matter how close the camera approaches it.
### Arguments

- *float* **size** - The maximum screen size for particles (maximum fraction of the screen a single particle can occupy):

## float getScreenMaxSize () const

Returns the current maximum screen size for particles (maximum fraction of the screen a single particle can occupy):
- The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
- The maximum value of **1** means the particle occupies the whole screen.

 Any particle shall occupy no more than the specified fraction of the screen, no matter how close the camera approaches it.
### Return value

Current maximum screen size for particles (maximum fraction of the screen a single particle can occupy):
## void setScreenMinSize ( float size )

Sets a new minimum screen size for particles (minimum fraction of the screen a single particle can occupy):
- The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
- The maximum value of **1** means the particle occupies the whole screen.

 Any particle shall occupy at least the specified fraction of the screen.
### Arguments

- *float* **size** - The minimum screen size for particles (minimum fraction of the screen a single particle can occupy):

## float getScreenMinSize () const

Returns the current minimum screen size for particles (minimum fraction of the screen a single particle can occupy):
- The minimum value of **0** means the particle has a zero size and therefore is invisible on the screen (occupies no space at all).
- The maximum value of **1** means the particle occupies the whole screen.

 Any particle shall occupy at least the specified fraction of the screen.
### Return value

Current minimum screen size for particles (minimum fraction of the screen a single particle can occupy):
## void setScreenSizeMode ( ObjectParticles::SCREEN_SIZE_MODE mode )

Sets a new screen size mode for particles. This mode defines whether the maximum and minimum sizes of emitted particles should be limited relative to screen size or not (e.g., to avoid cases when snowflakes or raindrops obscure the view if they are too close to the camera or when they become invisible as the distance to the camera increases). Three modes are available:
- **[NONE](#SCREEN_SIZE_MODE_NONE)** - minimum and maximum sizes of particles on the screen are not limited.
- **[WIDTH](#SCREEN_SIZE_MODE_WIDTH)** - minimum and maximum sizes of particles on the screen are limited relative to screen width.
- **[HEIGHT](#SCREEN_SIZE_MODE_HEIGHT)** - minimum and maximum sizes of particles on the screen are limited relative to screen height.

. One of the *[SCREEN_SIZE_MODE](#SCREEN_SIZE_MODE)* values.
### Arguments

- *[ObjectParticles::SCREEN_SIZE_MODE](../../../api/library/objects/class.objectparticles_cpp.md#SCREEN_SIZE_MODE)* **mode** - The screen size mode for particles

## ObjectParticles::SCREEN_SIZE_MODE getScreenSizeMode () const

Returns the current screen size mode for particles. This mode defines whether the maximum and minimum sizes of emitted particles should be limited relative to screen size or not (e.g., to avoid cases when snowflakes or raindrops obscure the view if they are too close to the camera or when they become invisible as the distance to the camera increases). Three modes are available:
- **[NONE](#SCREEN_SIZE_MODE_NONE)** - minimum and maximum sizes of particles on the screen are not limited.
- **[WIDTH](#SCREEN_SIZE_MODE_WIDTH)** - minimum and maximum sizes of particles on the screen are limited relative to screen width.
- **[HEIGHT](#SCREEN_SIZE_MODE_HEIGHT)** - minimum and maximum sizes of particles on the screen are limited relative to screen height.

. One of the *[SCREEN_SIZE_MODE](#SCREEN_SIZE_MODE)* values.
### Return value

Current screen size mode for particles
---

## static ObjectParticlesPtr create ( )

Constructor. Creates a particle system.
## Math:: vec3 getContactNormal ( int num ) const

Returns the point of the particles collision with other objects.
### Arguments

- *int* **num** - Collision point number.

### Return value

Collision point coordinates.
## Ptr < Object > getContactObject ( int num ) const

Returns the object that collided with particles collided in a given collision point.
### Arguments

- *int* **num** - The collision point number.

### Return value

The object participated in collision.
## Math:: Vec3 getContactPoint ( int num ) const

Returns the normal vector for the collision point of the particles with other objects.
### Arguments

- *int* **num** - The collision point number.

### Return value

Normal vector coordinates.
## Math:: vec3 getContactVelocity ( int num ) const

Returns the velocity in the collision point of the particles with other objects.
### Arguments

- *int* **num** - The collision point number.

### Return value

Velocity values for each of space dimensions.
## void setDelay ( float mean , float spread )

Sets delay of particle system initialization relative to the parent particle one.
### Arguments

- *float* **mean** - A mean value in seconds. If a negative value is provided, 0 will be used instead.
- *float* **spread** - A spread value in seconds.

## float getDelayMean ( ) const

Returns the mean value of particles initialization delay relative to the parent particle system.
### Return value

The mean value in seconds.
## float getDelaySpread ( ) const

Returns the spread value of particles initialization delay relative to the parent particle system.
### Return value

The spread value in seconds.
## void setDuration ( float mean , float spread )

Sets a duration of each particle emission in seconds.
### Arguments

- *float* **mean** - Mean value in seconds. If a negative value is provided, 0 will be used instead.
- *float* **spread** - Spread value in seconds.

## float getDurationMean ( ) const

Returns the current mean value of particle emission intervals.
### Return value

The mean value in seconds.
## float getDurationSpread ( ) const

Returns the current spread value of particle emission intervals.
### Return value

The spread value in seconds.
## void setLife ( float mean , float spread )

Sets a lifetime duration of particles in seconds.
### Arguments

- *float* **mean** - A mean value in seconds. If a too small value is provided, **1E-6** will be used instead.
- *float* **spread** - A spread value in seconds.

## float getLifeMean ( ) const

Returns the current mean value of particle lifetime duration.
### Return value

The mean value in seconds.
## float getLifeSpread ( ) const

Returns the current spread value of particle lifetime duration.
### Return value

The spread value in seconds.
## Math:: Vec3 getParticlePosition ( int num ) const

Returns the position of a given particle.
### Arguments

- *int* **num** - The particle number.

### Return value

Position coordinates for the particle.
## float getParticleRadius ( int num ) const

Returns the radius of a given particle.
### Arguments

- *int* **num** - The particle number.

### Return value

Radius of the particle.
## void getParticleTransforms ( Vector < Math:: Mat4 > & OUT_transforms ) const

Returns transformation matrices for spawned particles.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)> &* **OUT_transforms** - Array to which the transformation matrices will be added. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Math:: vec3 getParticleVelocity ( int num ) const

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

## float getPeriodMean ( ) const

Returns the current mean value of emitter inactivity intervals.
### Return value

The mean value in seconds.
## float getPeriodSpread ( ) const

Returns the current spread value of emitter inactivity intervals.
### Return value

The spread value in seconds.
## void setProceduralTextureResolution ( const Math:: vec3 & res )

Sets the resolution of the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **res** - Resolution of the texture.

## Math:: vec3 getProceduralTextureResolution ( ) const

Returns the resolution of the procedural texture.
> **Notice:** [Procedural rendering](#setProceduralRendering_int_void) must be enabled.


### Return value

Resolution of the texture.
## void addEmitterSpark ( const Math:: Vec3 & point , const Math:: vec3 & normal , const Math:: vec3 & velocity )

Adds a spark emitter in the given point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point for sparks emission.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **normal** - Normal vector at the point of spark emission.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **velocity** - Velocity in the point of spark emission (velocity of source particles or node by contact).

## void clearParticles ( )

Deletes all particles spawned by the emitter.
## static int type ( )

Returns the type of the object.
### Return value

[Object Particles](../../../api/library/nodes/class.node_cpp.md#OBJECT_PARTICLES) type identifier.
## bool saveStateSelf ( const Ptr < Stream > & stream ) const

Saves the object's state to the stream.
> **Notice:** This method saves all object's parameters.


Saving into the stream requires creating a blob to save into. To restore the saved state the [restoreStateSelf()](#restoreStateSelf_Stream_int) method is used:


```cpp
// initialize an object and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
object->saveStateSelf(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
object->restoreStateSelf(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## bool restoreStateSelf ( const Ptr < Stream > & stream )

Restores the object's state from the stream.
> **Notice:** This method restores all object's parameters.


Restoring from the stream requires creating a blob to save into and saving the state using the [saveStateSelf()](#saveStateSelf_Stream_int) method:


```cpp
// initialize an object and set its state
//...//

// save state
BlobPtr blob_state = Blob::create();
object->saveStateSelf(blob_state);

// change state
//...//

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
object->restoreStateSelf(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream smart pointer.

### Return value

true on success; otherwise, false.
## void takeSyncData ( const Ptr < Stream > & stream )

Writes particle synchronization data to the specified stream. This method should be used by the particle system with the master [sync mode](#setSyncMode_int_void).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which particle synchronization data is to be written.

## void applySyncData ( const Ptr < Stream > & stream )

Reads particle synchronization data from the specified stream and applies it to the particle system. This method should be used by the particle system with the slave [sync mode](#setSyncMode_int_void).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream with particle synchronization data to be applied.

## Ptr <ParticleModifierScalar> getLinearDampingOverTimeModifier ( ) const

Returns the modifier used to control how the linear damping of particles changes over time.
### Return value

Modifier, that controls linear damping of particles.
