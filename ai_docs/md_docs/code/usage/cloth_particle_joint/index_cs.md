# Creating and Attaching a Cloth (CS)


This example shows how to create a cloth pinned to two [dummy bodies](../../../principles/physics/bodies/dummy/index.md) using the [particles joints](../../../principles/physics/joints/index.md#particles). The cloth falls down and rests on a sphere, which illustrates the cloth ability to change its form.


![Falling cloth](cloth.gif)


To implement this, we need to perform the following:


- Create a cloth and set its parameters.
- Create two *Dummy Objects* that can hold the cloth. They also should have a body so that we can connect a cloth to them using joints.
- Create a sphere that is not a physical body (so that it would not drop and roll away), but is a collider, so our cloth will not fall through.


We are going to create functions for each participant of the example and then use these functions in *init()* to create the required objects.


## Creating a Cloth


We create a plane that will represent a [cloth](../../../principles/physics/bodies/cloth/index.md) � the *[Dynamic Mesh](../../../objects/objects/mesh_dynamic/index.md)* should be used to allow the cloth change at run time. Here we use the *[Primitives](../../../api/library/rendering/class.primitives_cs.md)* class to create a plane. You can also try to use your mesh instead, just make sure it complies with the [triangulation requirements](../../../principles/physics/bodies/cloth/index.md#requirements).


Then we assign the *Cloth* body to the created *Dynamic Mesh* and specify the required *Cloth* body parameters (mass, friction, restitution, etc) and the object parameters (transformation, color, name).


The whole function is as follows:


```csharp
ObjectMeshDynamic createBodyCloth(String name, float width, float height, float step, float mass, float friction, float restitution, float rigidity, float lrestitution, float arestitution, int num_iterations, vec4 color, Mat4 tm)
{
	// creating a dynamic mesh object with a plane surface
	ObjectMeshDynamic OMD = Primitives.CreatePlane(width, height, step);

	//assigning a cloth body to the dynamic mesh object and setting rope parameters
	BodyCloth body = new BodyCloth(OMD);

	body.Mass = mass;
	body.Friction = friction;
	body.Restitution = restitution;
	body.LinearRestitution = lrestitution;
	body.AngularRestitution = arestitution;
	body.Rigidity = rigidity;
	body.NumIterations = num_iterations;

	// setting object's parameters and transformation
	OMD.WorldTransform = tm;
	OMD.SetMaterialParameterFloat4("albedo_color", color, 0);
	OMD.Name = name;

	return OMD;
}


```


Using this function we create a cloth in the *init()* method.


## Hanging the Cloth in the Air


We need to fix one edge of the cloth in the air, otherwise it will unpredictably drop down, and there might be no contact with the sphere at all. This task is easily solved by using [Dummy Object](../../../objects/objects/dummy/index.md). We also assign the [Dummy](../../../principles/physics/bodies/dummy/index.md) body to it, as joints may connect bodies only.


```csharp
ObjectDummy createBodyDummy(String name, Vec3 size, Vec3 pos)
{
	// creating a dummy object
	ObjectDummy dummy = new ObjectDummy();

	// setting parameters
	dummy.WorldTransform = new Mat4(MathLib.Translate(pos));
	dummy.Name = name;

	//assigning a dummy body to the dummy object
	new BodyDummy(dummy);

	return dummy;
}


```


Using this function we create two points in the ***init()*** method and pin the cloth to them using the [Particles joint](../../../principles/physics/joints/index.md#particles):


```csharp
// creating 2 dummy bodies to which the cloth will be attached
dummy1 = createBodyDummy("fixpoint1", new Vec3(1.0f, 1.0f, 1.0f), new Vec3(-10.0f, -10.0f, 25.0f));
dummy2 = createBodyDummy("fixpoint2", new Vec3(1.0f, 1.0f, 1.0f), new Vec3(-10.0f, 10.0f, 25.0f));

// creating 2 particles joints to attach the cloth to dummy bodies
new JointParticles(dummy1.Body, cloth.Body, dummy1.Position, new vec3(1.0f));
new JointParticles(dummy2.Body, cloth.Body, dummy2.Position, new vec3(1.0f));


```


## Creating a Sphere


A sphere is used as a prop to demonstrate how the cloth would cover it, thus there's no need to make it physical. We only need to enable [collision for its surface](../../../principles/physics/collision/index.md#collision_types), otherwise the cloth would pass through the sphere without any interaction.


```csharp
ObjectMeshDynamic createSphere(String name, float radius, vec4 color, Vec3 pos)
{
	// creating a sphere dynamic mesh
	ObjectMeshDynamic OMD = Primitives.CreateSphere(radius);

	// setting parameters
	OMD.SetMaterialParameterFloat4("albedo_color", color, 0);
	OMD.WorldTransform = new Mat4(MathLib.Translate(pos));
	OMD.Name = name;
	OMD.SetCollision(true,0);

	return OMD;
}


```


Using this function we create a sphere in the *init()* method.


## Code Sample


The complete code sample is provided below.


<details>
<summary>ClothParticlesJoint.cs | close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#region Math Variables
#if UNIGINE_DOUBLE
using Scalar = System.Double;
using Vec3 = Unigine.dvec3;
using Mat4 = Unigine.dmat4;
#else
using Scalar = System.Single;
using Vec3 = Unigine.vec3;
using Mat4 = Unigine.mat4;
#endif
#endregion

public partial class ClothParticlesJoint : Component
{
	ObjectMeshDynamic cloth;
	ObjectMeshDynamic sphere;
	ObjectDummy dummy1;
	ObjectDummy dummy2;
	PlayerSpectator player;

	// method, creating a named sphere with a specified radius and color a specified position
	ObjectMeshDynamic createSphere(String name, float radius, vec4 color, Vec3 pos)
	{
		// creating a sphere dynamic mesh
		ObjectMeshDynamic OMD = Primitives.CreateSphere(radius);

		// setting parameters
		OMD.SetMaterialParameterFloat4("albedo_color", color, 0);
		OMD.WorldTransform = new Mat4(MathLib.Translate(pos));
		OMD.Name = name;
		OMD.SetCollision(true,0);

		return OMD;
	}

	// method, creating a named dummy body of a specified size a specified position
	ObjectDummy createBodyDummy(String name, Vec3 size, Vec3 pos)
	{
		// creating a dummy object
		ObjectDummy dummy = new ObjectDummy();

		// setting parameters
		dummy.WorldTransform = new Mat4(MathLib.Translate(pos));
		dummy.Name = name;

		//assigning a dummy body to the dummy object
		new BodyDummy(dummy);

		return dummy;
	}

	// method, creating a named cloth with specified parameters
	ObjectMeshDynamic createBodyCloth(String name, float width, float height, float step, float mass, float friction, float restitution, float rigidity, float lrestitution, float arestitution, int num_iterations, vec4 color, Mat4 tm)
	{
		// creating a dynamic mesh object with a plane surface
		ObjectMeshDynamic OMD = Primitives.CreatePlane(width, height, step);

		//assigning a cloth body to the dynamic mesh object and setting rope parameters
		BodyCloth body = new BodyCloth(OMD);

		body.Mass = mass;
		body.Friction = friction;
		body.Restitution = restitution;
		body.LinearRestitution = lrestitution;
		body.AngularRestitution = arestitution;
		body.Rigidity = rigidity;
		body.NumIterations = num_iterations;

		// setting object's parameters and transformation
		OMD.WorldTransform = tm;
		OMD.SetMaterialParameterFloat4("albedo_color", color, 0);
		OMD.Name = name;

		return OMD;
	}

	private void Init()
	{
		player = new PlayerSpectator();

		player.Position = new Vec3(30.0f, 0.0f, 30.5f);
		player.SetDirection(new vec3(-1.0f, 0.0f, -0.4f), new vec3(0.0f, 0.0f, -1.0f));
		Game.Player = player;

		cloth = createBodyCloth("MyCloth", 20.0f, 20.0f, 1.0f, 10.0f, 0.05f, 0.05f, 0.05f, 0.2f, 0.05f, 8, new vec4(0.3f, 0.3f, 1.0f, 1.0f), new Mat4(MathLib.Translate(new Vec3(0.0f, 0.0f, 25.0f))));

		// creating a sphere
		sphere = createSphere("MySphere", 3.0f, new vec4(1.0f, 0.1f, 0.1f, 1.0f), new Vec3(-1.0f, 0.0f, 16.0f));

		// creating 2 dummy bodies to which the cloth will be attached
		dummy1 = createBodyDummy("fixpoint1", new Vec3(1.0f, 1.0f, 1.0f), new Vec3(-10.0f, -10.0f, 25.0f));
		dummy2 = createBodyDummy("fixpoint2", new Vec3(1.0f, 1.0f, 1.0f), new Vec3(-10.0f, 10.0f, 25.0f));

		// creating 2 particles joints to attach the cloth to dummy bodies
		new JointParticles(dummy1.Body, cloth.Body, dummy1.Position, new vec3(1.0f));
		new JointParticles(dummy2.Body, cloth.Body, dummy2.Position, new vec3(1.0f));
	}
	}


```

</details>
