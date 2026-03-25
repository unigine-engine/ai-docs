# Creating and Attaching a Cloth (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This example shows how to create a cloth pinned to two [dummy bodies](../../../principles/physics/bodies/dummy/index.md) using the [particles joints](../../../principles/physics/joints/index.md#particles). The cloth falls down and rests on a sphere, which illustrates the cloth ability to change its form.


![Falling cloth](cloth.gif)


To implement this, we need to perform the following:


- Create a cloth and set its parameters.
- Create two *Dummy Objects* that can hold the cloth. They also should have a body so that we can connect a cloth to them using joints.
- Create a sphere that is not a physical body (so that it would not drop and roll away), but is a collider, so our cloth will not fall through.


We are going to create functions for each participant of the example and then use these functions in *init()* to create the required objects.


## Code Sample


The complete code sample is provided below.


> **Notice:** Unchanged methods of the *AppWorldLogic* class are not listed here, so leave them as they are.


<details>
<summary>Cloth sample | close</summary>

```cpp
#include <core/scripts/primitives.h>

ObjectMeshDynamic MyCloth;
ObjectMeshDynamic MySphere;
ObjectDummy dummy1;
ObjectDummy dummy2;

// function, creating a named sphere with a specified radius and color at a specified position
Object createSphere(string name, float radius, Vec4 color, Vec3 pos)
{
	// creating a dynamic mesh object with a sphere surface
	ObjectMeshDynamic sphere = Unigine::createSphere(radius);

	// setting object's parameters and transformation
	sphere.setWorldTransform(translate(pos));
	sphere.setMaterialParameterFloat4("albedo_color", color, 0);
	sphere.setName(name);

	return sphere;
}

// function, creating a named cloth body with specified parameters
Object createBodyCloth(string name, float width, float height, float step, float mass, float friction, float restitution, float rigidity, float lrestitution, float arestitution, int num_iterations, Vec4 color, Vec3 pos)
{
	// creating a dynamic mesh object with a plane surface and passing it to Editor
	ObjectMeshDynamic cloth = Unigine::createPlane(width,height,step);

	//assigning a cloth body to the dynamic mesh object and setting cloth parameters
	BodyCloth body = class_remove(new BodyCloth(cloth));
	body.setMass(mass);
	body.setFriction(friction);
	body.setRestitution(restitution);
	body.setLinearRestitution(lrestitution);
	body.setAngularRestitution(arestitution);
	body.setRigidity(rigidity);
	body.setNumIterations(num_iterations);

	// setting object's parameters and transformation
	cloth.setMaterialParameterFloat4("albedo_color", color, 0);
	cloth.setWorldTransform(pos);
	cloth.setName(name);

	return cloth;
}

// function, creating a named dummy body of a specified size at a specified position
Object createBodyDummy(string name, Vec3 size, Vec3 pos)
{
	// creating a dummy object and passing it to Editor
	ObjectDummy dummy = new ObjectDummy();

	// setting object's parameters
	dummy.setWorldTransform(translate(pos));
	dummy.setName(name);

	//assigning a dummy body to the dummy object and adding a box shape	to it
	BodyDummy body = class_remove(new BodyDummy(dummy));
	ShapeBox shape = class_remove(new ShapeBox(size));
	body.addShape(shape, translate(0.0f, 0.0f, 0.0f));

	return dummy;
}

int init() {

	// setting up player
	PlayerSpectator player = new PlayerSpectator();
	player.setPosition(Vec3(30.0f,0.0f, 30.5f));
	player.setDirection(Vec3(-1.0f, 0.0f, -0.4f));
	engine.game.setPlayer(player);

	// creating a cloth
	MyCloth = createBodyCloth("MyCloth", 20.0f, 20.0f, 1.0f, 10.0f, 0.05f, 0.05f, 0.05f, 0.2f, 0.05f, 8, Vec4(1.0f, 0.1f, 0.1f, 1.0f), translate(Vec3(0.0f, 0.0f, 25.0f)));

	// creating a sphere
	MySphere = createSphere("MySphere", 3.0f, Vec4(1.0f, 0.1f, 0.1f, 1.0f), Vec3(-1.0f, 0.0f, 16.0f));

	// creating 2 dummy bodies to which the cloth will be attached
	dummy1 = createBodyDummy("fixpoint1", Vec3(1.0f, 1.0f, 1.0f), Vec3(-10.0f, -10.0f, 25.0f));
	dummy2 = createBodyDummy("fixpoint2", Vec3(1.0f, 1.0f, 1.0f), Vec3(-10.0f, 10.0f, 25.0f));

	// creating 2 particles joints to attach the cloth to dummy bodies
	class_remove(new JointParticles(dummy1.getBody(),MyCloth.getBody(),dummy1.getPosition(),Vec3(1.0f)));
	class_remove(new JointParticles(dummy2.getBody(),MyCloth.getBody(),dummy2.getPosition(),Vec3(1.0f)));

	return 1;
}

```

</details>
