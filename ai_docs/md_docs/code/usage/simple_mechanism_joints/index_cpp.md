# Creating a Simple Mechanism Using Various Types of Joints (CPP)


![A Simple Mechanism Using Joints](mechanism_joints.jpg)

*A Simple Mechanism Using Joints*


This example shows how to:


- [Create a simple mechanism](#geometry) using various types of [joints](../../../principles/physics/joints/index.md).
- [Animate the mechanism](#motors) using [joint motors](../../../principles/physics/joints/index.md#motors).


The **basic workflow** of creating and animating a simple mechanism is as follows:


1. Create geometry for all parts of the mechanism.
2. Assign [bodies](../../../principles/physics/bodies/index.md) and [collision shapes](../../../principles/physics/shapes/index.md) to the parts.
3. Set up masses for the parts. > **Notice:** It is very important to ensure mass balance � avoid connection of too heavy bodies to light ones, otherwise the joints may become unstable!
4. Connect all parts of the mechanism using appropriate types of [joints](../../../principles/physics/joints/index.md). Set up joint parameters.
5. Animate the mechanism using [joint motors](../../../principles/physics/joints/index.md#motors).


## Creating Geometry and Adding Some Physics


The first thing we are going to address in this tutorial is the geometry of our mechanism (see the picture above). We are going to create the following parts:


- Two blue guide bars
- a red piston
- a green rod
- a black wheel
- Two [dummy objects](../../../objects/objects/dummy/index.md) with [dummy bodies](../../../principles/physics/bodies/dummy/index.md) to attach the parts of our mechanism to.


We are also going to add some physical parameters to the geometry such as mass and collision shapes. So, we need a set of basic functions:


```cpp
// function creating a named dummy body of a specified size at pos
ObjectDummyPtr createBodyDummy(const char* name, const vec3& size, const Mat4& transform)
{
	// creating a dummy object
	ObjectDummyPtr dummy = ObjectDummy::create();

	// setting parameters
	dummy->setWorldTransform(transform);
	dummy->setName(name);

	//assigning a dummy body to the dummy object and adding a box shape	to it
	BodyDummy::create(dummy);
	dummy->getBody()->addShape(ShapeBox::create(size), translate(0.0f, 0.0f, 0.0f));

	return dummy;
}

// function creating a named box having a specified size, color and transformation with a body and a shape
ObjectMeshDynamicPtr createBodyBox(const char* name, const vec3& size, float mass, const vec4& color, const Mat4& transform)
{
	// creating geometry and setting up its parameters (name, material and transformation)
	ObjectMeshDynamicPtr OMD = Primitives::createBox(size);
	OMD->setWorldTransform(transform);
	OMD->setMaterialParameterFloat4("albedo_color", color, 0);
	OMD->setCollision(1, 0);
	OMD->setName(name);

	// adding physics, i.e. a rigid body and a box shape with specified mass
	BodyRigidPtr body = BodyRigid::create(OMD);
	body->addShape(ShapeBox::create(size), translate(vec3(0.0f)));
	OMD->getBody()->getShape(0)->setMass(mass);

	return OMD;
}

// function creating a named cylinder having a specified size, color and transformation with a body and a shape
ObjectMeshDynamicPtr createBodyCylinder(const char* name, float radius, float height, float mass, const vec4& color, const Mat4& transform)
{
	// creating geometry and setting up its parameters (name, material and transformation)
	ObjectMeshDynamicPtr OMD = Primitives::createCylinder(radius, height, 1, 32);
	OMD->setWorldTransform(transform);
	OMD->setMaterialParameterFloat4("albedo_color", color, 0);
	OMD->setCollision(1, 0);
	OMD->setName(name);

	// adding physics, i.e. a rigid body and a cylinder shape with specified mass
	BodyRigidPtr body = BodyRigid::create(OMD);
	body->addShape(ShapeCylinder::create(radius, height), translate(vec3(0.0f)));
	OMD->getBody()->getShape(0)->setMass(mass);

	return OMD;
}


```


Now using these functions we can create our mechanism. We are going to use *[MeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cpp.md)* objects for the parts and *[Dummy](../../../api/library/objects/class.objectdummy_cpp.md)* objects for mounting points.


```cpp
// creating parts of the mechanism
Mat4 transform = Mat4(translate(0.0f, 0.0f, 10.0f) * rotateY(90.0f));

piston = createBodyBox("piston", vec3(1.0f, 2.0f, 0.5f), 15.0f, vec4(1.0f, 0.1f, 0.1f, 1.0f), transform * Mat4(translate(0.0f, 3.5f, 0.0f)));
guide_bar1 = createBodyBox("guide_bar1", vec3(1.0f, 9.0f, 0.5f), 15.0f, vec4(0.0f, 0.1f, 0.7f, 1.0f), transform * Mat4(translate(1.0f, 3.0f, 0.0f)));
guide_bar2 = createBodyBox("guide_bar2", vec3(1.0f, 9.0f, 0.5f), 15.0f, vec4(0.0f, 0.1f, 0.7f, 1.0f), transform * Mat4(translate(-1.0f, 3.0f, 0.0f)));
wheel = createBodyCylinder("wheel", 3.0f, 0.25f, 25.0f, vec4(0.1f, 0.1f, 0.1f, 1.0f), transform * Mat4(translate(0.0f, -15.0f, -0.5f)));
rod = createBodyCylinder("rod", 0.1f, 15.0f, 5.0f, vec4(0.1f, 1.1f, 0.1f, 1.0f), transform * Mat4(translate(0.0f, -5.0f, 0.0f) * rotateX(90.0f)));

//creating mounting points
dummy1 = createBodyDummy("dummy1", vec3(1.0f, 1.0f, 1.0f), transform * Mat4(translate(0.0f, -15.0f, -1.5f)));
dummy2 = createBodyDummy("dummy2", vec3(1.0f, 1.0f, 0.5f), transform * Mat4(translate(0.0f, 7.0f, 0.0f)));


```


## Adding and Setting Up Joints


Now that we have created all parts of our mechanism with physical bodies and shapes, let us link them together with [joints](../../../principles/physics/joints/index.md).


First, we are going to attach the wheel to the first mounting point(dummy1). The wheel is going to rotate around its axis. Let us use a [cylindrical joint](../../../api/library/physics/class.jointcylindrical_cpp.md) here. As the center of the wheel is aligned with the center of dummy1, we may use a simple constructor *[JointCylindrical()](../../../api/library/physics/class.jointcylindrical_cpp.md#JointCylindrical_constPtrBody_constPtrBody)* and specify only bodies, the anchor point will be placed automatically between their centers of mass.


Then we must set the coordinates (in the world space) of the axis of wheel rotation. In our case it is (1.0f, 0.0f, 0.0f). And finally set other joint parameters.


```cpp
// creating a cylindrical joint
jc = JointCylindrical::create(dummy1->getBody(), wheel->getBody());

// setting rotation axis in world coordinates
jc->setWorldAxis(vec3(1.0f, 0.0f, 0.0f));

// setting common joint constraint parameters
jc->setLinearRestitution(0.4f);
jc->setAngularRestitution(0.4f);
jc->setLinearSoftness(0.4f);
jc->setAngularSoftness(0.4f);

// setting linear and angular damping
jc->setLinearDamping(4.0f);
jc->setAngularDamping(2.0f);

// setting small linear limits as we are not going to use this degree of freedom to the full extent
jc->setLinearLimitFrom(-0.0005f);
jc->setLinearLimitTo(0.0005f);

// setting the number of iterations
jc->setNumIterations(16);


```


Now let us attach the rod to the wheel and to the piston. This is where we need a [hinge joint](../../../api/library/physics/class.jointhinge_cpp.md). For both of these joints we have to specify anchor point and joint axis coordinates in the *[JointHinge()](../../../api/library/physics/class.jointhinge_cpp.md#JointHinge_constPtrBody_constPtrBody_constMathVec3_constMathvec3)* constructor.


```cpp
// creating hinge joints
jh = JointHinge::create(wheel->getBody(), rod->getBody(), Vec3(0.0f, -12.5f, 10.0f), vec3(1.0f, 0.0f, 0.0f));
jh2 = JointHinge::create(rod->getBody(), piston->getBody(), Vec3(0.0f, 2.5f, 10.0f), vec3(1.0f, 0.0f, 0.0f));

// setting the number of iterations
jh->setNumIterations(8);
jh2->setNumIterations(8);


```


The next thing we are going to do is to attach two guide bars to the second mounting point(dummy2) using a pair of [fixed joints](../../../api/library/physics/class.jointfixed_cpp.md). For both of these joints we will specify anchor point coordinates in the *[JointFixed()](../../../api/library/physics/class.jointfixed_cpp.md#JointFixed_constPtrBody_constPtrBody_constMathVec3)* constructor.


```cpp
// creating fixed joints
jf1 = JointFixed::create(dummy2->getBody(), guide_bar1->getBody(), Vec3(0.0f, 7.0f, 9.0f));
jf2 = JointFixed::create(dummy2->getBody(), guide_bar2->getBody(), Vec3(0.0f, 7.0f, 11.0f));

// setting the number of iterations
jf1->setNumIterations(1);
jf2->setNumIterations(1);


```


And the last joint we are going to use is a [prismatic joint](../../../api/library/physics/class.jointprismatic_cpp.md) to attach the piston to the second mounting point *(dummy2)*. Here we will specify joint axis coordinates, linear limits to determine the range of motion for the piston and linear softness.


```cpp
// creating a prismatic joint
jp = JointPrismatic::create(piston->getBody(), dummy2->getBody());
jp->setWorldAxis(vec3(0.0f, 1.0f, 0.0f));

// setting linear limits [-5.0; 0.0] and softness
jp->setLinearLimitFrom(-5.0f);
jp->setLinearLimitTo(0.0f);
jp->setLinearSoftness(0.5f);

// setting the number of iterations
jp->setNumIterations(8);


```


## Using Joint Motors


To animate the mechanism we are going to use the [motor](../../../principles/physics/joints/index.md#motors) of our cylindrical joint. In order to make it move we must set angular velocity and torque:


```cpp
// setting up motor parameters for a cylindrical joint to animate the whole mechanism
jc->setAngularVelocity(1000.0f);
jc->setAngularTorque(150.0f);


```


## Putting it All Together


Let's sum up all described above. The final code for our tutorial will be as follows:


In the **AppWorldLogic.h** file, define smart pointers for the objects of our scene.


```cpp
/* .. */
#include <UnigineObjects.h>
#include <UniginePlayers.h>

class AppWorldLogic : public Unigine::WorldLogic
{

public:
	/* .. */


```


Insert the following code into the **AppWorldLogic.cpp** file.

> **Notice:** Unchanged methods of the *AppWorldLogic* class are not listed here, so leave them as they are.


```cpp
/* .. */
#include "AppWorldLogic.h"
#include "UnigineGame.h"
#include "UniginePrimitives.h"

using namespace Unigine;
using namespace Math;

// joints of the mechanism
JointCylindricalPtr jc;
JointHingePtr jh;
JointHingePtr jh2;
JointFixedPtr jf1;
JointFixedPtr jf2;
JointPrismaticPtr jp;

// function creating a named dummy body of a specified size at pos
ObjectDummyPtr createBodyDummy(const char* name, const vec3& size, const Mat4& transform)
{
	// creating a dummy object
	ObjectDummyPtr dummy = ObjectDummy::create();

	// setting parameters
	dummy->setWorldTransform(transform);
	dummy->setName(name);

	//assigning a dummy body to the dummy object and adding a box shape	to it
	BodyDummy::create(dummy);
	dummy->getBody()->addShape(ShapeBox::create(size), translate(0.0f, 0.0f, 0.0f));

	return dummy;
}

// function creating a named box having a specified size, color and transformation with a body and a shape
ObjectMeshDynamicPtr createBodyBox(const char* name, const vec3& size, float mass, const vec4& color, const Mat4& transform)
{
	// creating geometry and setting up its parameters (name, material and transformation)
	ObjectMeshDynamicPtr OMD = Primitives::createBox(size);
	OMD->setWorldTransform(transform);
	OMD->setMaterialParameterFloat4("albedo_color", color, 0);
	OMD->setCollision(1, 0);
	OMD->setName(name);

	// adding physics, i.e. a rigid body and a box shape with specified mass
	BodyRigidPtr body = BodyRigid::create(OMD);
	body->addShape(ShapeBox::create(size), translate(vec3(0.0f)));
	OMD->getBody()->getShape(0)->setMass(mass);

	return OMD;
}

// function creating a named cylinder having a specified size, color and transformation with a body and a shape
ObjectMeshDynamicPtr createBodyCylinder(const char* name, float radius, float height, float mass, const vec4& color, const Mat4& transform)
{
	// creating geometry and setting up its parameters (name, material and transformation)
	ObjectMeshDynamicPtr OMD = Primitives::createCylinder(radius, height, 1, 32);
	OMD->setWorldTransform(transform);
	OMD->setMaterialParameterFloat4("albedo_color", color, 0);
	OMD->setCollision(1, 0);
	OMD->setName(name);

	// adding physics, i.e. a rigid body and a cylinder shape with specified mass
	BodyRigidPtr body = BodyRigid::create(OMD);
	body->addShape(ShapeCylinder::create(radius, height), translate(vec3(0.0f)));
	OMD->getBody()->getShape(0)->setMass(mass);

	return OMD;
}

int AppWorldLogic::init()
{
	// setting up physics parameters
	Physics::setGravity(vec3(0.0f, 0.0f, -9.8f * 2.0f));
	Physics::setFrozenLinearVelocity(0.1f);
	Physics::setFrozenAngularVelocity(0.1f);

	// setting up player
	player = PlayerSpectator::create();

	player->setPosition(Vec3(22.0f, -2.0f, 10.0f));
	player->setDirection(vec3(-10.0f, -2.0f, 0.0f), vec3(0.0f, 0.0f, -1.0f));
	Game::setPlayer(player);

	// creating parts of the mechanism
	Mat4 transform = Mat4(translate(0.0f, 0.0f, 10.0f) * rotateY(90.0f));

	piston = createBodyBox("piston", vec3(1.0f, 2.0f, 0.5f), 15.0f, vec4(1.0f, 0.1f, 0.1f, 1.0f), transform * Mat4(translate(0.0f, 3.5f, 0.0f)));
	guide_bar1 = createBodyBox("guide_bar1", vec3(1.0f, 9.0f, 0.5f), 15.0f, vec4(0.0f, 0.1f, 0.7f, 1.0f), transform * Mat4(translate(1.0f, 3.0f, 0.0f)));
	guide_bar2 = createBodyBox("guide_bar2", vec3(1.0f, 9.0f, 0.5f), 15.0f, vec4(0.0f, 0.1f, 0.7f, 1.0f), transform * Mat4(translate(-1.0f, 3.0f, 0.0f)));
	wheel = createBodyCylinder("wheel", 3.0f, 0.25f, 25.0f, vec4(0.1f, 0.1f, 0.1f, 1.0f), transform * Mat4(translate(0.0f, -15.0f, -0.5f)));
	rod = createBodyCylinder("rod", 0.1f, 15.0f, 5.0f, vec4(0.1f, 1.1f, 0.1f, 1.0f), transform * Mat4(translate(0.0f, -5.0f, 0.0f) * rotateX(90.0f)));

	//creating mounting points
	dummy1 = createBodyDummy("dummy1", vec3(1.0f, 1.0f, 1.0f), transform * Mat4(translate(0.0f, -15.0f, -1.5f)));
	dummy2 = createBodyDummy("dummy2", vec3(1.0f, 1.0f, 0.5f), transform * Mat4(translate(0.0f, 7.0f, 0.0f)));

	// creating hinge joints
	jh = JointHinge::create(wheel->getBody(), rod->getBody(), Vec3(0.0f, -12.5f, 10.0f), vec3(1.0f, 0.0f, 0.0f));
	jh2 = JointHinge::create(rod->getBody(), piston->getBody(), Vec3(0.0f, 2.5f, 10.0f), vec3(1.0f, 0.0f, 0.0f));

	// setting the number of iterations
	jh->setNumIterations(8);
	jh2->setNumIterations(8);

	// creating fixed joints
	jf1 = JointFixed::create(dummy2->getBody(), guide_bar1->getBody(), Vec3(0.0f, 7.0f, 9.0f));
	jf2 = JointFixed::create(dummy2->getBody(), guide_bar2->getBody(), Vec3(0.0f, 7.0f, 11.0f));

	// setting the number of iterations
	jf1->setNumIterations(1);
	jf2->setNumIterations(1);

	// creating a prismatic joint
	jp = JointPrismatic::create(piston->getBody(), dummy2->getBody());
	jp->setWorldAxis(vec3(0.0f, 1.0f, 0.0f));

	// setting linear limits [-5.0; 0.0] and softness
	jp->setLinearLimitFrom(-5.0f);
	jp->setLinearLimitTo(0.0f);
	jp->setLinearSoftness(0.5f);

	// setting the number of iterations
	jp->setNumIterations(8);

	// creating a cylindrical joint
	jc = JointCylindrical::create(dummy1->getBody(), wheel->getBody());

	// setting rotation axis in world coordinates
	jc->setWorldAxis(vec3(1.0f, 0.0f, 0.0f));

	// setting common joint constraint parameters
	jc->setLinearRestitution(0.4f);
	jc->setAngularRestitution(0.4f);
	jc->setLinearSoftness(0.4f);
	jc->setAngularSoftness(0.4f);

	// setting linear and angular damping
	jc->setLinearDamping(4.0f);
	jc->setAngularDamping(2.0f);

	// setting small linear limits as we are not going to use this degree of freedom to the full extent
	jc->setLinearLimitFrom(-0.0005f);
	jc->setLinearLimitTo(0.0005f);

	// setting the number of iterations
	jc->setNumIterations(16);

	// setting up motor parameters for a cylindrical joint to animate the whole mechanism
	jc->setAngularVelocity(1000.0f);
	jc->setAngularTorque(150.0f);

	return 1;
}

/* .. */

```
