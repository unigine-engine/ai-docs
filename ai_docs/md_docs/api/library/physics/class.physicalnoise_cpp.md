# Unigine.PhysicalNoise Class (CPP)

**Header:** #include <UniginePhysicals.h>

**Inherits from:** Physical


The *PhysicalNoise* class is used to simulate a force field affecting physical bodies and particles based on a volumetric noise texture.  It creates an additional distribution flow specifying the force and the displacement direction for bodies and particles at each point of the force field.


> **Notice:** - The physical noise can affect only a [*cloth*](../../../principles/physics/bodies/cloth/index.md), a [*rope*](../../../api/library/physics/class.bodyrope_cpp.md) or a [*rigid*](../../../principles/physics/bodies/rigid/index.md) body. Also you should remember that a rigid body requires a [shape](../../../principles/physics/shapes/index.md) to be assigned.
> - The physical noise will affect particles only if their physical mass is nonzero.


### Usage Example


In this example a physical noise node and 50 boxes, each with a body and a shape, are created. Generated boxes fall down under the set gravity and are affected by the physical noise as they get into it.


In the **AppWorldLogic.cpp** file let us add the following code:


```cpp
// AppWorldLogic.cpp
/* .. */
#include <UnigineGame.h>
#include "AppWorldLogic.h"
#include <UniginePhysicals.h>
#include <UniginePrimitives.h>
#include <UnigineVisualizer.h>

using namespace Unigine;
using namespace Math;

// declaring a PhysicalNoise node
PhysicalNoisePtr physical_noise;

/// function, creating a named box having a specified size, color and transformation with a body and a shape
ObjectMeshDynamicPtr createBodyBox(const char* name, vec3 size, float mass, vec4 color, Mat4 transform)
{
	// creating geometry and setting up its parameters (name, color and transformation)
	ObjectMeshDynamicPtr box = Primitives::createBox(size);
	box->setWorldTransform(transform);
	box->setMaterialParameterFloat4("albedo_color", color, 0);
	box->setName(name);

	// adding physics, i.e. a rigid body and a box shape with the specified mass
	BodyRigidPtr body = BodyRigid::create(box);
	body->addShape(ShapeBox::create(size), translate(vec3(0.0f)));
	box->getBody()->getShape(0)->setMass(mass);

	// setting the physical mask for the body
	body->setPhysicalMask(1);

	return box;
}

/* .. */

int AppWorldLogic::init()
{
	// setting up physics parameters (gravity, linear and angular velocity)
	Physics::setGravity(vec3(0.0f, 0.0f, -1.0f));
	Physics::setFrozenLinearVelocity(0.1f);
	Physics::setFrozenAngularVelocity(0.1f);

	// setting up player's parameters
	Game::getPlayer()->setWorldPosition(Vec3(0.0f, 90.0f, 70.0f));
	Game::getPlayer()->setDirection(vec3(0.0f, -1.0f, -0.7f), vec3(0.0f, 0.0f, -1.0f));

	// creating a physical noise node with a size of 60x60x60
	physical_noise = PhysicalNoise::create(vec3(60.0f));

	// setting the force multiplier equal to 50
	physical_noise->setForce(50.0f);

	// setting the threshold distance
	physical_noise->setThreshold(vec3(0.0f));

	// setting the physical mask
	physical_noise->setPhysicalMask(1);

	//setting up noise texture generation parameters (scale, frequency, size)
	physical_noise->setNoiseScale(0.2f);
	physical_noise->setFrequency(4);
	physical_noise->setImageSize(16);

	// setting the sampling step equal to 20
	physical_noise->setStep(vec3(20.0f));

	// enabling the Visualizer to show our physical noise
	Visualizer::setEnabled(1);

	//generating 50 boxes with rigid bodies and shapes assigned
	for (int i = 0; i < 50; i++) {
		Vec3 position = Vec3(Game::getRandomDouble(-50.0f, 50.0f), Game::getRandomDouble(-50.0f, 50.0f), 40.0f);
		vec4 color = vec4(Game::getRandomFloat(0.0f, 1.0f), Game::getRandomFloat(0.0f, 1.0f), Game::getRandomFloat(0.0f, 1.0f), Game::getRandomFloat(0.0f, 1.0f));
		createBodyBox("box", vec3_one, 1.0f, color, translate(position));
	}

	return 1;
}

int AppWorldLogic::update()
{
	// rendering visualizer for the physical noise node
	physical_noise->renderVisualizer();

	return 1;
}


```


### See Also


- Article on [*Physical Noise*](../../../objects/effects/physicals/physical_noise/index.md) to learn more about the parameters
- UnigineScript sample:


## PhysicalNoise Class

### Members

## void setThreshold ( const Math:: vec3 & threshold )

Sets a new threshold distance set for the physical noise node. the threshold determines the distance of gradual change from zero to full force value. this values are relative to the size of the physical noise box. it means that the threshold values should be less than the size of the physical noise box.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **threshold** - The threshold distance for the physical noise node

## Math:: vec3 getThreshold () const

Returns the current threshold distance set for the physical noise node. the threshold determines the distance of gradual change from zero to full force value. this values are relative to the size of the physical noise box. it means that the threshold values should be less than the size of the physical noise box.
### Return value

Current threshold distance for the physical noise node
## void setStep ( const Math:: vec3 & step )

Sets a new sampling step that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **step** - The sampling step for pixel sampling from the noise texture

## Math:: vec3 getStep () const

Returns the current sampling step that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
### Return value

Current sampling step for pixel sampling from the noise texture
## void setSize ( const Math:: vec3 & size )

Sets a new size of the physical noise node.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The size of the physical noise node

## Math:: vec3 getSize () const

Returns the current size of the physical noise node.
### Return value

Current size of the physical noise node
## void setNoiseScale ( float scale )

Sets a new scale of the noise texture.
### Arguments

- *float* **scale** - The scale of the noise texture

## float getNoiseScale () const

Returns the current scale of the noise texture.
### Return value

Current scale of the noise texture
## void setOffset ( const Math:: vec3 & offset )

Sets a new sampling offset that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **offset** - The sampling offset for pixel sampling from the noise texture

## Math:: vec3 getOffset () const

Returns the current sampling offset that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
### Return value

Current sampling offset for pixel sampling from the noise texture
## void setImageSize ( int size )

Sets a new size of the noise texture in pixels.
### Arguments

- *int* **size** - The size of the noise texture in pixels

## int getImageSize () const

Returns the current size of the noise texture in pixels.
### Return value

Current size of the noise texture in pixels
## void setFrequency ( int frequency )

Sets a new number of octaves for the perlin noise texture generation. It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.
### Arguments

- *int* **frequency** - The number of octaves for the noise texture generation

## int getFrequency () const

Returns the current number of octaves for the perlin noise texture generation. It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.
### Return value

Current number of octaves for the noise texture generation
## void setForce ( float force )

Sets a new value of the force multiplier.
### Arguments

- *float* **force** - The force multiplier

## float getForce () const

Returns the current value of the force multiplier.
### Return value

Current force multiplier
---

## static PhysicalNoisePtr create ( const Math:: vec3 & size )

Constructor. Creates a physical noise node of the specified size.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Physical noise box size in units.

## Ptr < Image > getImage ( )

Returns the noise texture image.
### Return value

Noise texture image.
## static int type ( )

Returns the type of the node.
### Return value

[PhysicalNoise](../../../api/library/nodes/class.node_cpp.md#PHYSICAL_NOISE) type identifier.
