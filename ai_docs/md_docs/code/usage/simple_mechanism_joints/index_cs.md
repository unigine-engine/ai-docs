# Creating a Simple Mechanism Using Various Types of Joints (CS)


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


```csharp
// method creating a named dummy body of a specified size at pos
ObjectDummy createBodyDummy(String name, vec3 size, Mat4 transform)
{
	// creating a dummy object
	ObjectDummy dummy = new ObjectDummy();

	// setting parameters
	dummy.WorldTransform = transform;
	dummy.Name = name;

	//assigning a dummy body to the dummy object and adding a box shape	to it
	new BodyDummy(dummy);
	dummy.Body.AddShape(new ShapeBox(size), MathLib.Translate(0.0f, 0.0f, 0.0f));

	return dummy;
}

/// method, creating a named box having a specified size, color and transformation with a body and a shape
ObjectMeshDynamic createBodyBox(String name, vec3 size, float mass, vec4 color, Mat4 transform)
{
	// creating geometry and setting up its parameters (name and transformation)
	ObjectMeshDynamic OMD = Primitives.CreateBox(size);
	OMD.WorldTransform = transform;
	OMD.SetMaterialParameterFloat4("albedo_color", color, 0);
	OMD.SetCollision(true, 0);
	OMD.Name = name;

	// adding physics, i.e. a rigid body and a box shape with specified mass
	BodyRigid body = new BodyRigid(OMD);

	body.AddShape(new ShapeBox(size), MathLib.Translate(new vec3(0.0f)));
	OMD.Body.GetShape(0).Mass = mass;

	return OMD;
}

/// method, creating a named cylinder having a specified size, color and transformation with a body and a shape
ObjectMeshDynamic createBodyCylinder(String name, float radius, float height, float mass, vec4 color, Mat4 transform)
{
	// creating geometry and setting up its parameters (name and transformation)
	ObjectMeshDynamic OMD = Primitives.CreateCylinder(radius, height, 1, 32);
	OMD.WorldTransform = transform;
	OMD.SetMaterialParameterFloat4("albedo_color", color, 0);
	OMD.SetCollision(true, 0);
	OMD.Name = name;

	// adding physics, i.e. a rigid body and a cylinder shape with specified mass
	BodyRigid body = new BodyRigid(OMD);
	body.AddShape(new ShapeCylinder(radius, height), MathLib.Translate(new vec3(0.0f)));
	OMD.Body.GetShape(0).Mass = mass;

	return OMD;
}


```


Now using these functions we can create our mechanism. We are going to use *[MeshDynamic](../../../api/library/objects/class.objectmeshdynamic_cs.md)* objects for the parts and *[Dummy](../../../api/library/objects/class.objectdummy_cs.md)* objects for mounting points.


```csharp
// creating parts of the mechanism
Mat4 transform = new Mat4(MathLib.Translate(0.0f, 0.0f, 10.0f) * MathLib.RotateY(90.0f));

piston = createBodyBox("piston", new vec3(1.0f, 2.0f, 0.5f), 15.0f, new vec4(1.0f, 0.1f, 0.1f, 1.0f), transform * new Mat4(MathLib.Translate(0.0f, 3.5f, 0.0f)));
guide_bar1 = createBodyBox("guide_bar1", new vec3(1.0f, 9.0f, 0.5f), 15.0f, new vec4(0.0f, 0.1f, 0.7f, 1.0f), transform * new Mat4(MathLib.Translate(1.0f, 3.0f, 0.0f)));
guide_bar2 = createBodyBox("guide_bar2", new vec3(1.0f, 9.0f, 0.5f), 15.0f, new vec4(0.0f, 0.1f, 0.7f, 1.0f), transform * new Mat4(MathLib.Translate(-1.0f, 3.0f, 0.0f)));
wheel = createBodyCylinder("wheel", 3.0f, 0.25f, 25.0f, new vec4(0.1f, 0.1f, 0.1f, 1.0f), transform * new Mat4(MathLib.Translate(0.0f, -15.0f, -0.5f)));
rod = createBodyCylinder("rod", 0.1f, 15.0f, 5.0f, new vec4(0.1f, 1.1f, 0.1f, 1.0f), transform * new Mat4(MathLib.Translate(0.0f, -5.0f, 0.0f) * MathLib.RotateX(90.0f)));

//creating mounting points
dummy1 = createBodyDummy("dummy1", new vec3(1.0f, 1.0f, 1.0f), transform * new Mat4(MathLib.Translate(0.0f, -15.0f, -1.5f)));
dummy2 = createBodyDummy("dummy2", new vec3(1.0f, 1.0f, 0.5f), transform * new Mat4(MathLib.Translate(0.0f, 7.0f, 0.0f)));


```


## Adding and Setting Up Joints


Now that we have created all parts of our mechanism with physical bodies and shapes, let us link them together with [joints](../../../principles/physics/joints/index.md).


First, we are going to attach the wheel to the first mounting point(dummy1). The wheel is going to rotate around its axis. Let us use a [cylindrical joint](../../../api/library/physics/class.jointcylindrical_cs.md) here. As the center of the wheel is aligned with the center of dummy1, we may use a simple constructor *[JointCylindrical()](../../../api/library/physics/class.jointcylindrical_cs.md#JointCylindrical_constPtrBody_constPtrBody)* and specify only bodies, the anchor point will be placed automatically between their centers of mass.


Then we must set the coordinates (in the world space) of the axis of wheel rotation. In our case it is (1.0f, 0.0f, 0.0f). And finally set other joint parameters.


```csharp
// creating a cylindrical joint
jc = new JointCylindrical(dummy1.Body, wheel.Body);

// setting rotation axis in world coordinates
jc.WorldAxis = new vec3(1.0f, 0.0f, 0.0f);

// setting common joint constraint parameters
jc.LinearRestitution = 0.4f;
jc.AngularRestitution = 0.4f;
jc.LinearSoftness = 0.4f;
jc.AngularSoftness = 0.4f;

// setting linear and angular damping
jc.LinearDamping = 4.0f;
jc.AngularDamping = 2.0f;

// setting small linear limits as we are not going to use this degree of freedom to the full extent
jc.LinearLimitFrom = -0.0005f;
jc.LinearLimitTo = 0.0005f;

// setting the number of iterations
jc.NumIterations = 16;


```


Now let us attach the rod to the wheel and to the piston. This is where we need a [hinge joint](../../../api/library/physics/class.jointhinge_cs.md). For both of these joints we have to specify anchor point and joint axis coordinates in the *[JointHinge()](../../../api/library/physics/class.jointhinge_cs.md#JointHinge_constPtrBody_constPtrBody_constMathVec3_constMathvec3)* constructor.


```csharp
// creating hinge joints
jh = new JointHinge(wheel.Body, rod.Body, new Vec3(0.0f, -12.5f, 10.0f), new vec3(1.0f, 0.0f, 0.0f));
jh2 = new JointHinge(rod.Body, piston.Body, new Vec3(0.0f, 2.5f, 10.0f), new vec3(1.0f, 0.0f, 0.0f));

// setting the number of iterations
jh.NumIterations = 8;
jh2.NumIterations = 8;


```


The next thing we are going to do is to attach two guide bars to the second mounting point(dummy2) using a pair of [fixed joints](../../../api/library/physics/class.jointfixed_cs.md). For both of these joints we will specify anchor point coordinates in the *[JointFixed()](../../../api/library/physics/class.jointfixed_cs.md#JointFixed_constPtrBody_constPtrBody_constMathVec3)* constructor.


```csharp
// creating fixed joints
jf1 = new JointFixed(dummy2.Body, guide_bar1.Body, new Vec3(0.0f, 7.0f, 9.0f));
jf2 = new JointFixed(dummy2.Body, guide_bar2.Body, new Vec3(0.0f, 7.0f, 11.0f));

// setting the number of iterations
jf1.NumIterations = 1;
jf2.NumIterations = 1;


```


And the last joint we are going to use is a [prismatic joint](../../../api/library/physics/class.jointprismatic_cs.md) to attach the piston to the second mounting point *(dummy2)*. Here we will specify joint axis coordinates, linear limits to determine the range of motion for the piston and linear softness.


```csharp
// creating a prismatic joint
jp = new JointPrismatic(piston.Body, dummy2.Body);
jp.WorldAxis = new vec3(0.0f, 1.0f, 0.0f);

// setting linear limits [-5.0; 0.0] and softness
jp.LinearLimitFrom = -5.0f;
jp.LinearLimitTo = 0.0f;
jp.LinearSoftness = 0.5f;

// setting the number of iterations
jp.NumIterations = 8;


```


## Using Joint Motors


To animate the mechanism we are going to use the [motor](../../../principles/physics/joints/index.md#motors) of our cylindrical joint. In order to make it move we must set angular velocity and torque:


```csharp
// setting up motor parameters for a cylindrical joint to animate the whole mechanism
jc.AngularVelocity = 1000.0f;
jc.AngularTorque = 150.0f;


```


## Putting it All Together


Let's sum up all described above. The final code for our tutorial will be as follows:


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#region Math Variables
#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Mat4 = Unigine.dmat4;
#else
using Vec3 = Unigine.vec3;
using Mat4 = Unigine.mat4;
#endif
#endregion

public partial class SimpleMechanismJoints : Component
{

	PlayerSpectator player;

	// parts of the mechanism
	ObjectDummy dummy1;
	ObjectDummy dummy2;
	ObjectMeshDynamic rod;
	ObjectMeshDynamic wheel;
	ObjectMeshDynamic piston;
	ObjectMeshDynamic guide_bar1;
	ObjectMeshDynamic guide_bar2;

	// joints of the mechanism
	JointCylindrical jc;
	JointHinge jh;
	JointHinge jh2;
	JointFixed jf1;
	JointFixed jf2;
	JointPrismatic jp;

	// method creating a named dummy body of a specified size at pos
	ObjectDummy createBodyDummy(String name, vec3 size, Mat4 transform)
	{
		// creating a dummy object
		ObjectDummy dummy = new ObjectDummy();

		// setting parameters
		dummy.WorldTransform = transform;
		dummy.Name = name;

		//assigning a dummy body to the dummy object and adding a box shape	to it
		new BodyDummy(dummy);
		dummy.Body.AddShape(new ShapeBox(size), MathLib.Translate(0.0f, 0.0f, 0.0f));

		return dummy;
	}

	/// method, creating a named box having a specified size, color and transformation with a body and a shape
	ObjectMeshDynamic createBodyBox(String name, vec3 size, float mass, vec4 color, Mat4 transform)
	{
		// creating geometry and setting up its parameters (name and transformation)
		ObjectMeshDynamic OMD = Primitives.CreateBox(size);
		OMD.WorldTransform = transform;
		OMD.SetMaterialParameterFloat4("albedo_color", color, 0);
		OMD.SetCollision(true, 0);
		OMD.Name = name;

		// adding physics, i.e. a rigid body and a box shape with specified mass
		BodyRigid body = new BodyRigid(OMD);

		body.AddShape(new ShapeBox(size), MathLib.Translate(new vec3(0.0f)));
		OMD.Body.GetShape(0).Mass = mass;

		return OMD;
	}

	/// method, creating a named cylinder having a specified size, color and transformation with a body and a shape
	ObjectMeshDynamic createBodyCylinder(String name, float radius, float height, float mass, vec4 color, Mat4 transform)
	{
		// creating geometry and setting up its parameters (name and transformation)
		ObjectMeshDynamic OMD = Primitives.CreateCylinder(radius, height, 1, 32);
		OMD.WorldTransform = transform;
		OMD.SetMaterialParameterFloat4("albedo_color", color, 0);
		OMD.SetCollision(true, 0);
		OMD.Name = name;

		// adding physics, i.e. a rigid body and a cylinder shape with specified mass
		BodyRigid body = new BodyRigid(OMD);
		body.AddShape(new ShapeCylinder(radius, height), MathLib.Translate(new vec3(0.0f)));
		OMD.Body.GetShape(0).Mass = mass;

		return OMD;
	}

	private void Init()
	{
		// setting up physics parameters
		Physics.Gravity = new vec3(0.0f, 0.0f, -9.8f * 2.0f);
		Physics.FrozenLinearVelocity = 0.1f;
		Physics.FrozenAngularVelocity = 0.1f;

		// setting up player
		player = new PlayerSpectator();

		player.Position = new Vec3(22.0f, -2.0f, 10.0f);
		player.SetDirection(new vec3(-10.0f, -2.0f, 0.0f), new vec3(0.0f, 0.0f, -1.0f));
		Game.Player = player;

		// creating parts of the mechanism
		Mat4 transform = new Mat4(MathLib.Translate(0.0f, 0.0f, 10.0f) * MathLib.RotateY(90.0f));

		piston = createBodyBox("piston", new vec3(1.0f, 2.0f, 0.5f), 15.0f, new vec4(1.0f, 0.1f, 0.1f, 1.0f), transform * new Mat4(MathLib.Translate(0.0f, 3.5f, 0.0f)));
		guide_bar1 = createBodyBox("guide_bar1", new vec3(1.0f, 9.0f, 0.5f), 15.0f, new vec4(0.0f, 0.1f, 0.7f, 1.0f), transform * new Mat4(MathLib.Translate(1.0f, 3.0f, 0.0f)));
		guide_bar2 = createBodyBox("guide_bar2", new vec3(1.0f, 9.0f, 0.5f), 15.0f, new vec4(0.0f, 0.1f, 0.7f, 1.0f), transform * new Mat4(MathLib.Translate(-1.0f, 3.0f, 0.0f)));
		wheel = createBodyCylinder("wheel", 3.0f, 0.25f, 25.0f, new vec4(0.1f, 0.1f, 0.1f, 1.0f), transform * new Mat4(MathLib.Translate(0.0f, -15.0f, -0.5f)));
		rod = createBodyCylinder("rod", 0.1f, 15.0f, 5.0f, new vec4(0.1f, 1.1f, 0.1f, 1.0f), transform * new Mat4(MathLib.Translate(0.0f, -5.0f, 0.0f) * MathLib.RotateX(90.0f)));

		//creating mounting points
		dummy1 = createBodyDummy("dummy1", new vec3(1.0f, 1.0f, 1.0f), transform * new Mat4(MathLib.Translate(0.0f, -15.0f, -1.5f)));
		dummy2 = createBodyDummy("dummy2", new vec3(1.0f, 1.0f, 0.5f), transform * new Mat4(MathLib.Translate(0.0f, 7.0f, 0.0f)));

		// creating a cylindrical joint
		jc = new JointCylindrical(dummy1.Body, wheel.Body);

		// setting rotation axis in world coordinates
		jc.WorldAxis = new vec3(1.0f, 0.0f, 0.0f);

		// setting common joint constraint parameters
		jc.LinearRestitution = 0.4f;
		jc.AngularRestitution = 0.4f;
		jc.LinearSoftness = 0.4f;
		jc.AngularSoftness = 0.4f;

		// setting linear and angular damping
		jc.LinearDamping = 4.0f;
		jc.AngularDamping = 2.0f;

		// setting small linear limits as we are not going to use this degree of freedom to the full extent
		jc.LinearLimitFrom = -0.0005f;
		jc.LinearLimitTo = 0.0005f;

		// setting the number of iterations
		jc.NumIterations = 16;

		// creating hinge joints
		jh = new JointHinge(wheel.Body, rod.Body, new Vec3(0.0f, -12.5f, 10.0f), new vec3(1.0f, 0.0f, 0.0f));
		jh2 = new JointHinge(rod.Body, piston.Body, new Vec3(0.0f, 2.5f, 10.0f), new vec3(1.0f, 0.0f, 0.0f));

		// setting the number of iterations
		jh.NumIterations = 8;
		jh2.NumIterations = 8;

		// creating fixed joints
		jf1 = new JointFixed(dummy2.Body, guide_bar1.Body, new Vec3(0.0f, 7.0f, 9.0f));
		jf2 = new JointFixed(dummy2.Body, guide_bar2.Body, new Vec3(0.0f, 7.0f, 11.0f));

		// setting the number of iterations
		jf1.NumIterations = 1;
		jf2.NumIterations = 1;

		// creating a prismatic joint
		jp = new JointPrismatic(piston.Body, dummy2.Body);
		jp.WorldAxis = new vec3(0.0f, 1.0f, 0.0f);

		// setting linear limits [-5.0; 0.0] and softness
		jp.LinearLimitFrom = -5.0f;
		jp.LinearLimitTo = 0.0f;
		jp.LinearSoftness = 0.5f;

		// setting the number of iterations
		jp.NumIterations = 8;

		// setting up motor parameters for a cylindrical joint to animate the whole mechanism
		jc.AngularVelocity = 1000.0f;
		jc.AngularTorque = 150.0f;

	}

}

```
