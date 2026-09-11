# Unigine.PhysicalNoise Class (CS)

**Inherits from:** Physical


The *PhysicalNoise* class is used to simulate a force field affecting physical bodies and particles based on a volumetric noise texture.  It creates an additional distribution flow specifying the force and the displacement direction for bodies and particles at each point of the force field.


> **Notice:** - The physical noise can affect only a [*cloth*](../../../principles/physics/bodies/cloth/index.md), a [*rope*](../../../api/library/physics/class.bodyrope_cs.md) or a [*rigid*](../../../principles/physics/bodies/rigid/index.md) body. Also you should remember that a rigid body requires a [shape](../../../principles/physics/shapes/index.md) to be assigned.
> - The physical noise will affect particles only if their physical mass is nonzero.


### Usage Example


In this example a physical noise node and 50 boxes, each with a body and a shape, are created. Generated boxes fall down under the set gravity and are affected by the physical noise as they get into it.


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

public partial class PhysicalNoiseClass : Component
{
	// declaring a PhysicalNoise node
	PhysicalNoise physical_noise;

	/// function, creating a named box having a specified size, color and transformation with a body and a shape
	ObjectMeshDynamic createBodyBox(string name, vec3 size, float mass, vec4 color, Mat4 transform)
	{
		// creating geometry and setting up its parameters (name, color and transformation)
		ObjectMeshDynamic box = Primitives.CreateBox(size);
		box.WorldTransform = transform;
		box.SetMaterialParameterFloat4("albedo_color", color, 0);
		box.Name = name;

		// adding physics, i.e. a rigid body and a box shape with specified mass
		BodyRigid body = new BodyRigid(box);
		body.AddShape(new ShapeBox(size), MathLib.Translate(new vec3(0.0f)));
		box.Body.GetShape(0).Mass = mass;

		// setting the physical mask for the body
		body.PhysicalMask = 1;

		return box;
	}

	/* .. */

	private void Init()
	{
		// setting up physics parameters (gravity, linear and angular velocity)
		Physics.Gravity = new vec3(0.0f, 0.0f, -1.0f);
		Physics.FrozenLinearVelocity = 0.1f;
		Physics.FrozenAngularVelocity = 0.1f;

		// setting up player's parameters
		Game.Player.WorldPosition = new Vec3(0.0f, 90.0f, 70.0f);
		Game.Player.SetDirection(new vec3(0.0f, -1.0f, -0.7f), new vec3(0.0f, 0.0f, -1.0f));

		// creating a physical noise node with a size of 60x60x60
		physical_noise = new PhysicalNoise(new vec3(60.0f));

		// setting the force multiplier
		physical_noise.Force = 50.0f;

		// setting the threshold distance
		physical_noise.Threshold = new vec3(0.0f);

		// setting the physical mask
		physical_noise.PhysicalMask = 1;

		//setting up noise texture generation parameters (scale, frequency, size)
		physical_noise.NoiseScale = 0.2f;
		physical_noise.Frequency = 4;
		physical_noise.ImageSize = 16;

		// setting the sampling step equal to 20
		physical_noise.Step = new vec3(20.0f);

		// enabling the Visualizer to show our physical noise
		Visualizer.Enabled = true;

		//generating 50 boxes with rigid bodies and shapes assigned
		for (int i = 0; i < 50; i++) {
			Vec3 position = new Vec3(Game.GetRandomDouble(-50.0f, 50.0f), Game.GetRandomDouble(-50.0f, 50.0f), 40.0f);
			vec4 color = new vec4(Game.GetRandomFloat(0.0f, 1.0f), Game.GetRandomFloat(0.0f, 1.0f), Game.GetRandomFloat(0.0f, 1.0f), Game.GetRandomFloat(0.0f, 1.0f));
			createBodyBox("box", new vec3(1.0f), 1.0f, color, MathLib.Translate(position));
		}
	}

	private void Update()
	{
		// rendering visualizer for the physical noise node
        physical_noise.RenderVisualizer();

	}
}

```


### See Also


- Article on [*Physical Noise*](../../../objects/effects/physicals/physical_noise/index.md) to learn more about the parameters
- UnigineScript sample:


## PhysicalNoise Class

### Properties

## vec3 Threshold

The threshold distance set for the physical noise node. the threshold determines the distance of gradual change from zero to full force value. this values are relative to the size of the physical noise box. it means that the threshold values should be less than the size of the physical noise box.
## vec3 Step

The sampling step that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
## vec3 Size

The size of the physical noise node.
## float NoiseScale

The scale of the noise texture.
## vec3 Offset

The sampling offset that is used for pixel sampling from the noise texture. This parameter can be used to animate a force field in run-time.
## int ImageSize

The size of the noise texture in pixels.
## int Frequency

The number of octaves for the perlin noise texture generation. It is not recommended to change this parameter in run-time as the noise texture will be regenerated and the performance will decrease.
## float Force

The value of the force multiplier.
### Members

---

## PhysicalNoise ( vec3 size )

Constructor. Creates a physical noise node of the specified size.
### Arguments

- *vec3* **size** - Physical noise box size in units.

## Image GetImage ( )

Returns the noise texture image.
### Return value

Noise texture image.
## static int type ( )

Returns the type of the node.
### Return value

[PhysicalNoise](../../../api/library/nodes/class.node_cs.md#PHYSICAL_NOISE) type identifier.
