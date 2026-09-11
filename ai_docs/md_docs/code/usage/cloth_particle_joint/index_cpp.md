# Creating and Attaching a Cloth (CPP)


This example shows how to create a cloth pinned to two [dummy bodies](../../../principles/physics/bodies/dummy/index.md) using the [particles joints](../../../principles/physics/joints/index.md#particles). The cloth falls down and rests on a sphere, which illustrates the cloth ability to change its form.


![Falling cloth](cloth.gif)


To implement this, we need to perform the following:


- Create a cloth and set its parameters.
- Create two *Dummy Objects* that can hold the cloth. They also should have a body so that we can connect a cloth to them using joints.
- Create a sphere that is not a physical body (so that it would not drop and roll away), but is a collider, so our cloth will not fall through.


We are going to create functions for each participant of the example and then use these functions in *init()* to create the required objects.


## Creating a Cloth


We create a plane that will represent a [cloth](../../../principles/physics/bodies/cloth/index.md) � the *[Dynamic Mesh](../../../objects/objects/mesh_dynamic/index.md)* should be used to allow the cloth change at run time. Here we use the *[Primitives](../../../api/library/rendering/class.primitives_cpp.md)* class to create a plane. You can also try to use your mesh instead, just make sure it complies with the [triangulation requirements](../../../principles/physics/bodies/cloth/index.md#requirements).


Then we assign the *Cloth* body to the created *Dynamic Mesh* and specify the required *Cloth* body parameters (mass, friction, restitution, etc) and the object parameters (transformation, color, name).


The whole function is as follows:


```cpp
ObjectMeshDynamicPtr createBodyCloth(const char* name, float width, float height, float step, float mass, float friction, float restitution, float rigidity, float lrestitution, float arestitution, int num_iterations, const vec4& color, const Mat4& tm)
{
	// creating a dynamic mesh object with a plane surface
	ObjectMeshDynamicPtr OMD = Primitives::createPlane(width, height, step);

	//assigning a cloth body to the dynamic mesh object and setting the cloth parameters
	BodyClothPtr body = BodyCloth::create(OMD);

	body->setMass(mass);
	body->setFriction(friction);
	body->setRestitution(restitution);
	body->setLinearRestitution(lrestitution);
	body->setAngularRestitution(arestitution);
	body->setRigidity(rigidity);
	body->setNumIterations(num_iterations);

	// setting object's parameters and transformation
	OMD->setWorldTransform(tm);
	OMD->setMaterialParameterFloat4("albedo_color", color, 0);
	OMD->setName(name);

	return OMD;
}


```


Using this function we create a cloth in the *init()* method.


## Hanging the Cloth in the Air


We need to fix one edge of the cloth in the air, otherwise it will unpredictably drop down, and there might be no contact with the sphere at all. This task is easily solved by using [Dummy Object](../../../objects/objects/dummy/index.md). We also assign the [Dummy](../../../principles/physics/bodies/dummy/index.md) body to it, as joints may connect bodies only.


```cpp
ObjectDummyPtr createBodyDummy(const char* name, const vec3& size, const vec3& pos)
{
	// creating a dummy object
	ObjectDummyPtr dummy = ObjectDummy::create();

	// setting parameters
	dummy->setWorldTransform(Mat4(translate(pos)));
	dummy->setName(name);

	//assigning a dummy body to the dummy object
	BodyDummy::create(dummy);


	return dummy;
}



	return dummy;
}

```


Using this function we create two points in the ***init()*** method and pin the cloth to them using the [Particles joint](../../../principles/physics/joints/index.md#particles):


```cpp
// creating 2 dummy bodies to which the cloth will be attached
dummy1 = createBodyDummy("fixpoint1", vec3(1.0f, 1.0f, 1.0f), vec3(-10.0f, -10.0f, 25.0f));
dummy2 = createBodyDummy("fixpoint2", vec3(1.0f, 1.0f, 1.0f), vec3(-10.0f, 10.0f, 25.0f));

// creating 2 particles joints to attach the cloth to dummy bodies
JointParticles::create(dummy1->getBody(), cloth->getBody(), dummy1->getPosition(), vec3(1.0f));
JointParticles::create(dummy2->getBody(), cloth->getBody(), dummy2->getPosition(), vec3(1.0f));


```


## Creating a Sphere


A sphere is used as a prop to demonstrate how the cloth would cover it, thus there's no need to make it physical. We only need to enable [collision for its surface](../../../principles/physics/collision/index.md#collision_types), otherwise the cloth would pass through the sphere without any interaction.


```cpp
ObjectMeshDynamicPtr createSphere(const char* name, float radius, const vec4& color, const vec3& pos)
{
	// creating a sphere dynamic mesh
	ObjectMeshDynamicPtr OMD = Primitives::createSphere(radius);

	// setting parameters

	OMD->setMaterialParameterFloat4("albedo_color", color, 0);
	OMD->setWorldTransform(Mat4(translate(pos)));
	OMD->setName(name);
	OMD->setCollision(1, 0);
	return OMD;
}


```


Using this function we create a sphere in the *init()* method.


## Code Sample


The complete code sample is provided below.


> **Notice:** Unchanged methods of the *AppWorldLogic* class are not listed here, so leave them as they are.


In the **AppWorldLogic.h** file, define smart pointers for the objects.


<details>
<summary>AppWorldLogic.h | close</summary>

```cpp
#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineObjects.h>
#include <UniginePlayers.h>

class AppWorldLogic: public Unigine::WorldLogic
{

private:
	Unigine::ObjectMeshDynamicPtr cloth;
	Unigine::ObjectMeshDynamicPtr sphere;
	Unigine::ObjectDummyPtr dummy1;
	Unigine::ObjectDummyPtr dummy2;
	Unigine::PlayerSpectatorPtr player;
};


```

</details>


Add the following code to the **AppWorldLogic.cpp** file.


<details>
<summary>AppWorldLogic.cpp | close</summary>

```cpp
#include "AppWorldLogic.h"
#include "UnigineGame.h"
#include "UniginePrimitives.h"
#include "UnigineObjects.h"

using namespace Unigine;
using namespace Math;

/// function, creating a named sphere with a specified radius and color at pos
ObjectMeshDynamicPtr createSphere(const char* name, float radius, const vec4& color, const vec3& pos)
{
	// creating a sphere dynamic mesh
	ObjectMeshDynamicPtr OMD = Primitives::createSphere(radius);

	// setting parameters

	OMD->setMaterialParameterFloat4("albedo_color", color, 0);
	OMD->setWorldTransform(Mat4(translate(pos)));
	OMD->setName(name);
	OMD->setCollision(1, 0);
	return OMD;
}

/// function, creating a named dummy body of a specified size at pos
ObjectDummyPtr createBodyDummy(const char* name, const vec3& size, const vec3& pos)
{
	// creating a dummy object
	ObjectDummyPtr dummy = ObjectDummy::create();

	// setting parameters
	dummy->setWorldTransform(Mat4(translate(pos)));
	dummy->setName(name);

	//assigning a dummy body to the dummy object
	BodyDummy::create(dummy);


	return dummy;
}

/// function, creating a named cloth with specified parameters
ObjectMeshDynamicPtr createBodyCloth(const char* name, float width, float height, float step, float mass, float friction, float restitution, float rigidity, float lrestitution, float arestitution, int num_iterations, const vec4& color, const Mat4& tm)
{
	// creating a dynamic mesh object with a plane surface
	ObjectMeshDynamicPtr OMD = Primitives::createPlane(width, height, step);

	//assigning a cloth body to the dynamic mesh object and setting the cloth parameters
	BodyClothPtr body = BodyCloth::create(OMD);

	body->setMass(mass);
	body->setFriction(friction);
	body->setRestitution(restitution);
	body->setLinearRestitution(lrestitution);
	body->setAngularRestitution(arestitution);
	body->setRigidity(rigidity);
	body->setNumIterations(num_iterations);

	// setting object's parameters and transformation
	OMD->setWorldTransform(tm);
	OMD->setMaterialParameterFloat4("albedo_color", color, 0);
	OMD->setName(name);

	return OMD;
}

int AppWorldLogic::init()
{
		player = PlayerSpectator::create();

	player->setPosition(Vec3(30.0f, 0.0f, 30.5f));
	player->setDirection(vec3(-1.0f, 0.0f, -0.4f), vec3(0.0f, 0.0f, -1.0f));
	Game::setPlayer(player);

	cloth = createBodyCloth("MyCloth", 20.0f, 20.0f, 1.0f, 10.0f, 0.05f, 0.05f, 0.05f, 0.2f, 0.05f, 8, vec4(0.3f, 0.3f, 1.0f, 1.0f), Mat4(translate(vec3(0.0f, 0.0f, 25.0f))));

	// creating a sphere
	sphere = createSphere("MySphere", 3.0f, vec4(1.0f, 0.1f, 0.1f, 1.0f), vec3(-1.0f, 0.0f, 16.0f));

		// creating 2 dummy bodies to which the cloth will be attached
	dummy1 = createBodyDummy("fixpoint1", vec3(1.0f, 1.0f, 1.0f), vec3(-10.0f, -10.0f, 25.0f));
	dummy2 = createBodyDummy("fixpoint2", vec3(1.0f, 1.0f, 1.0f), vec3(-10.0f, 10.0f, 25.0f));

	// creating 2 particles joints to attach the cloth to dummy bodies
	JointParticles::create(dummy1->getBody(), cloth->getBody(), dummy1->getPosition(), vec3(1.0f));
	JointParticles::create(dummy2->getBody(), cloth->getBody(), dummy2->getPosition(), vec3(1.0f));

	return 1;
}

/* .. */

```

</details>
