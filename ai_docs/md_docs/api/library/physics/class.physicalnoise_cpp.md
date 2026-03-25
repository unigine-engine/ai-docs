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

---

## static PhysicalNoisePtr create ( const Math:: vec3 & size )

Constructor. Creates a physical noise node of the specified size.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Physical noise box size in units.

## void setForce ( float force )

Sets the value of the force multiplier.
### Arguments

- *float* **force** - Force multiplier. The higher the value is, the higher the value of the resulting force that affects an object inside the physical noise node will be.

## float getForce ( )

Returns the value of the force multiplier.
### Return value

Force multiplier. The higher the value is, the higher the value of the resulting force that affects an object inside the physical noise node will be.
## void setFrequency ( int frequency )

Sets the number of octaves for the Perlin noise texture generation.
> **Notice:** It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.


### Arguments

- *int* **frequency** - Number of octaves for the Perlin noise texture generation. The minimum value is **1**, the maximum value is **16**. The higher the value is, the more details the noise texture has.

## int getFrequency ( )

Returns the number of octaves for the Perlin noise texture generation.
> **Notice:** It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.


### Return value

Number of octaves for the Perlin noise texture generation. The minimum value is **1**, the maximum value is **16**. The higher the value is, the more details the noise texture has.
## Ptr < Image > getImage ( )

Returns the noise texture image.
### Return value

Noise texture image.
## void setImageSize ( int size )

Sets the size of the noise texture in pixels.
### Arguments

- *int* **size** - Size of the noise texture in pixels.

## int getImageSize ( )

Returns the size of the noise texture in pixels.
### Return value

Size of the noise texture in pixels.
## void setNoiseScale ( float scale )

Sets the scale of the noise texture.
> **Notice:** It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.


### Arguments

- *float* **scale** - Scale of the noise texture. The minimum value is **0**, the maximum value is **1**.

## float getNoiseScale ( )

Returns the scale of the noise texture.
### Return value

Scale of the noise texture. The minimum value is 0, the maximum value is 1.
## void setOffset ( const Math:: vec3 & offset )

Sets the sampling offset that will be used for pixel sampling from the noise texture.
> **Notice:** This parameter can be used to animate a force field in run-time.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **offset** - Sampling offset along the X, Y and Z axes.

## Math:: vec3 getOffset ( )

Returns the sampling offset that is used for pixel sampling from the noise texture.
> **Notice:** This parameter can be used to animate a force field in run-time.


### Return value

Sampling offset along the X, Y and Z axes.
## void setSize ( const Math:: vec3 & size )

Sets the size for the physical noise node.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Size of the physical noise box in units. If a negative value is provided, 0 will be used instead.

## Math:: vec3 getSize ( )

Returns the current size of the physical noise node.
### Return value

Size of the physical noise box in units.
## void setStep ( const Math:: vec3 & step )

Sets the sampling step that is used for pixel sampling from the noise texture.
> **Notice:** This parameter can be used to animate a force field in run-time.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **step** - Sampling step size along the X, Y and Z axes.

## Math:: vec3 getStep ( )

Returns the sampling step that is used for pixel sampling from the noise texture.
> **Notice:** This parameter can be used to animate a force field in run-time.


### Return value

Sampling step size along the X, Y and Z axes.
## void setThreshold ( const Math:: vec3 & threshold )

Sets a threshold distance set for the physical noise node.  The threshold determines the distance of gradual change from zero to full force value. This values are relative to the size of the physical noise box. It means that the threshold values should be less than the size of the physical noise box.
![](../../../objects/effects/physicals/threshold.png)


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **threshold** - Threshold distance along the X, Y and Z axes.

## Math:: vec3 getThreshold ( )

 Returns the threshold distance set for the physical noise node. The threshold determines the distance of gradual change from zero to full force value. This values are relative to the size of the physical noise box. It means that the threshold values should be less than the size of the physical noise box.
### Return value

## static int type ( )

Returns the type of the node.
### Return value

[PhysicalNoise](../../../api/library/nodes/class.node_cpp.md#PHYSICAL_NOISE) type identifier.
