# Creating Pylons and Wires Using Ropes (CPP)


![A Wire Attached to Pylons](pylons_wire.png)

*A Wire Attached to Pylons*


This example shows how to create a wire using a rope body and attach it to pylons. A tutorial teaching how to reproduce the same scene in UnigineEditor can be found here.


In the **AppWorldLogic.h** file, define smart pointers for the objects of our scene.


```cpp
// AppWorldLogic.h
#include <UnigineObjects.h>

/* .. */

class AppWorldLogic : public Unigine::WorldLogic {

public:
	/* .. */

private:
	Unigine::ObjectDummyPtr dummy1;
	Unigine::ObjectDummyPtr dummy2;
	Unigine::ObjectMeshDynamicPtr pylon1;
	Unigine::ObjectMeshDynamicPtr pylon2;
	Unigine::ObjectMeshDynamicPtr rope;
	Unigine::PlayerSpectatorPtr player;
};

```


Insert the following code into the **AppWorldLogic.cpp** file.

> **Notice:** Unchanged methods of the *AppWorldLogic* class are not listed here, so leave them as they are.


```cpp
/* .. */
#include "UnigineGame.h"
#include "UniginePrimitives.h"
#include "UnigineObjects.h"

using namespace Unigine;
using namespace Math;

/* .. */

/// function, creating a named pylon with a specified radius and height at pos
ObjectMeshDynamicPtr create_pylon(const char *name, float radius, float length, const vec3& pos)
{
	// creating a cylinder dynamic mesh
	ObjectMeshDynamicPtr OM = Primitives::createCylinder(radius, length, 1, 6);

	// setting parameters
	OM->setWorldTransform(Mat4(translate(pos)));
	OM->setMaterialParameterFloat4("albedo_color", vec4(0.1f, 0.1f, 0.0f, 1.0f), 0);
	OM->setName(name);

	return OM;
}

/// function, creating a named dummy body of a specified size at pos
ObjectDummyPtr createBodyDummy(const char *name, const vec3& size, const vec3& pos)
{
	// creating a dummy object
	ObjectDummyPtr OMD = ObjectDummy::create();

	// setting parameters
	OMD->setWorldTransform(Mat4(translate(pos)));
	OMD->setName(name);

	//assigning a dummy body to the dummy object and adding a box shape	to it
	BodyDummy::create(OMD);
	OMD->getBody()->addShape(ShapeBox::create(size), translate(0.0f, 0.0f, 0.0f));

	return OMD;
}

/// function, creating a named rope with specified parameters at pos
ObjectMeshDynamicPtr createBodyRope(const char *name, float radius, float length, int segments, int slices, const Mat4& tm)
{
	// creating a cylinder dynamic mesh
	ObjectMeshDynamicPtr OMD = Primitives::createCylinder(radius, length, segments, slices);

	// setting parameters
	OMD->setWorldTransform(tm);
	OMD->setMaterialParameterFloat4("albedo_color", vec4(0.5f, 0.5f, 0.0f, 1.0f), 0);
	OMD->setName(name);

	//assigning a rope body to the dynamic mesh object and setting rope parameters
	BodyRopePtr body = BodyRope::create(OMD);
	body->setMass(1.0f);
	body->setRadius(0.25f);
	body->setFriction(0.5f);
	body->setRestitution(0.05f);
	body->setRigidity(0.05f);
	body->setLinearStretch(0.5f);

	return OMD;
}

/* .. */

int AppWorldLogic::init() {

	// setting up player
	player = PlayerSpectator::create();

	player->setPosition(Vec3(0.0f, -23.401f, 15.5f));
	player->setDirection(vec3(0.0f, 1.0f, -0.4f), vec3(0.0f, 0.0f, -1.0f));
	Game::setPlayer(player);

	// creating dummy objects to attach a rope to and placing them on the top of each pylon
	dummy1 = createBodyDummy("fixpoint1", vec3(0.5f, 0.5f, 0.5f), vec3(-12.0f, 0.0f, 15.0f));
	dummy2 = createBodyDummy("fixpoint2", vec3(0.5f, 0.5f, 0.5f), vec3(12.0f, 0.0f, 15.0f));

	// creating pylons
	pylon1 = create_pylon("Pylon1", 0.3f, 17, vec3(-12.2f, 0.0f, 7.0f));
	pylon2 = create_pylon("Pylon2", 0.3f, 17, vec3(12.2f, 0.0f, 7.0f));

	// creating a rope
	rope = createBodyRope("MyRope", 0.05f, 24, 96, 6, Mat4(translate(0.0f, 0.0f, 15.0f)*rotateY(-90.0f)));

	// creating 2 particles joints to attach the rope to dummy bodies
	JointParticles::create(dummy1->getBody(), rope->getBody(), dummy1->getPosition(), vec3(0.55f));
	JointParticles::create(dummy2->getBody(), rope->getBody(), dummy2->getPosition(), vec3(0.55f));

	return 1;
}

/* .. */


```
