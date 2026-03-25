# Creating Pylons and Wires Using Ropes (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


![A Wire Attached to Pylons](pylons_wire.png)

*A Wire Attached to Pylons*


This example shows how to create a wire using a rope body and attach it to pylons. A tutorial teaching how to reproduce the same scene in UnigineEditor can be found here.


```cpp
#include <core/scripts/primitives.h>

ObjectMeshDynamic rope;
ObjectMeshDynamic pylon1;
ObjectMeshDynamic pylon2;
ObjectDummy dummy1;
ObjectDummy dummy2;

/// function, creating a named pylon with a specified radius and height at pos
int createPylon(Object &OMD, string name, float radius, float length, Vec3 pos)
{
	OMD = Unigine::createCylinder(radius, length, 1, 6);
	OMD.setWorldTransform(pos);

	OMD.setMaterialParameterFloat4("albedo_color", Vec4(0.1f, 0.1f, 0.0f, 1.0f), 0);
	OMD.setName(name);

	return 1;
}

/// function, creating a named rope with specified parameters at pos
int createBodyRope(Object &OMD, string name, float radius, float length, int segments, int slices, Vec3 pos)
{
	// creating a cylinder dynamic mesh
	OMD = Unigine::createCylinder(radius, length, segments, slices);
	OMD.setWorldTransform(pos);
	// setting parameters
	OMD.setMaterialParameterFloat4("albedo_color", Vec4(0.5f, 0.5f, 0.0f, 1.0f), 0);
	OMD.setName(name);

	//assigning a rope body to the dynamic mesh object and setting rope parameters
	BodyRope body = class_remove(new BodyRope(OMD));
	body.setMass(1.0f);
	body.setRadius(0.25f);
	body.setFriction(0.5f);
	body.setRestitution(0.05f);
	body.setRigidity(0.05f);
	body.setLinearStretch(0.5f);

	return 1;
}

/// function, creating a named dummy body of a specified size at pos
int createBodyDummy(Object &OMD, string name, Vec3 size, Vec3 pos)
{
	OMD.setWorldTransform(translate(pos));
	OMD.setName(name);

	//assigning a dummy body to the dummy object and adding a box shape	to it
	BodyDummy body = class_remove(new BodyDummy(OMD));
	ShapeBox shape = class_remove(new ShapeBox(size));
	body.addShape(shape, translate(0.0f, 0.0f, 0.0f));

	return 1;
}


int init()
{

	// setting up player
	Player player = new PlayerSpectator();
	player.setPosition(Vec3(0.0f,-23.401f,15.5f));
	player.setDirection(Vec3(0.0f,1.0f,-0.4f));
	engine.game.setPlayer(player);

	// creating 2 dummy objects
	dummy1 = new ObjectDummy();
	dummy2 = new ObjectDummy();

	// creating pylons
	createPylon(pylon1, "Pylon1", 0.3f, 17, translate(Vec3(-12.2f, 0.0f, 7.0f)));
	createPylon(pylon2, "Pylon2", 0.3f, 17, translate(Vec3(12.2f, 0.0f, 7.0f)));

	// creating dummy objects to attach a rope to and placing them on the top of each pylon
	createBodyDummy(dummy1, "fixpoint1", Vec3(0.5f, 0.5f, 0.5f), Vec3(-12.0f, 0.0f, 15.0f));
	createBodyDummy(dummy2, "fixpoint2", Vec3(0.5f, 0.5f, 0.5f), Vec3(12.0f, 0.0f, 15.0f));

	// creating a rope
	createBodyRope(rope, "MyRope", 0.05f, 24, 96, 6, translate(Vec3(0.0f, 0.0f, 15.0f))*rotateY(-90.0f));

	// creating 2 particles joints to attach the rope to dummy bodies
	class_remove(new JointParticles(dummy1.getBody(),rope.getBody(),dummy1.getPosition(),Vec3(0.55f)));
	class_remove(new JointParticles(dummy2.getBody(),rope.getBody(),dummy2.getPosition(),Vec3(0.55f)));

	return 1;
}

```
