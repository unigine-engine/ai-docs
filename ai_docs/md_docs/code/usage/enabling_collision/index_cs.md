# Enabling Selective Surface-Based Collision (CS)


![Surface-based collision example](collision_ex1.gif)

*Surface-based collision using collision masks*


This example shows how to enable collision detection for a surface using bitmasks. Two boxes (orange and yellow), each with a body and a box shape assigned, and a blue plane are created. We want the yellow box to collide with the surface of the blue plane and the orange box to pass through. So we set the following collision masks for the shapes of the boxes and for the surface of the plane.


| Element | Mask |
|---|---|
| Yellow box: shape | **0010** |
| Orange box: shape | **0001** |
| Plane: surface | **0010** |


> **Notice:** Surface-to-surface collisions cannot be enabled using collision masks.


```csharp
// AppWorldLogic.cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{

        ObjectMeshStatic box1;
        ObjectMeshStatic box2;
        ObjectMeshStatic plane;
		PlayerSpectator player;

        /// method, creating a named box of a specified size and color at pos
        ObjectMeshStatic create_box(String name, vec4 color, vec3 size, vec3 pos)
        {
	        // creating an auxiliary mesh with a box surface
	        Mesh meshbox = new Mesh();
	        meshbox.AddBoxSurface("box_surface", size);

	        // creating a static mesh object using an auxiliary mesh and setting parameters
	        ObjectMeshStatic OM = new ObjectMeshStatic(meshbox);

	        OM.WorldTransform = new dmat4(MathLib.Translate(pos));
	        OM.SetMaterialParameterFloat4("albedo_color", color, 0);
			OM.SetCollision(1, 0);
	        OM.Name = name;

	        // assigning a rigid body with our object
	        new BodyRigid(OM);

	        // creating a box shape and assigning it to the rigid body of our object
	        OM.Body.AddShape(new ShapeBox(size), MathLib.Translate(0.0f, 0.0f, 0.0f));

	        // clearing the auxiliary mesh
	        meshbox.Clear();

	        return OM;
        }

        /// method, creating a named plane having a specified width and height at pos
        ObjectMeshStatic create_plane(String name, float width, float height, vec3 pos)
        {
	        // creating an auxiliary mesh with a plane surface
	        Mesh meshplane = new Mesh();

	        meshplane.AddPlaneSurface("plane_surface", width, height, 1.0f);

        	// creating a static mesh object using an auxiliary mesh and setting parameters
	        ObjectMeshStatic OM = new ObjectMeshStatic(meshplane);

	        OM.WorldTransform = new dmat4(MathLib.Translate(pos));
	        OM.SetMaterialParameterFloat4("albedo_color", new vec4(0.0f, 0.0f, 1.0f, 1.0f), 0);
			OM.SetCollision(1, 0);
	        OM.Name = name;

	        // clearing the auxiliary mesh
	        meshplane.Clear();

	        return OM;
        }

		/* .. */

		public override bool Init()
		{

            // setting up a player
	        player = new PlayerSpectator();
	        player.Position = new dvec3(0.0f, -6.0f, 12.5f);
	        player.SetDirection(new vec3(0.0f, 1.0f, -0.4f), new vec3(0.0f, 0.0f, -1.0f));
	        Game.Player = player;

	        // creating a scene: two boxes and a plane
	        box1 = create_box("box1", new vec4(1.0f, 1.0f, 0.0f, 1.0f), new vec3(0.5f), new vec3(1.5f, 0.0f, 12.0f));
	        box2 = create_box("box2", new vec4(1.0f, 0.5f, 0.1f, 1.0f), new vec3(0.5f), new vec3(-1.5f, 0.0f, 12.0f));
	        plane = create_plane("plane", 10.0f, 6.0f, new vec3(0.0f, 1.0f, 10.5f));

	        // setting shape collision mask for the first box  [00000000000000000000000000000010]
	        box1.Body.GetShape(0).CollisionMask = 2;

	        // setting shape collision mask for the second box  [00000000000000000000000000000001]
	        box2.Body.GetShape(0).CollisionMask = 1;

	        // setting collision mask for the plane surface  [00000000000000000000000000000010]
	        plane.SetCollisionMask(2, 0);

			return true;
		}

		/* .. */

	}
}

```
