# Unigine::PhysicsIntersectionNormal Class (CS)

**Inherits from:** PhysicsIntersection


This class stores all information on the point of physics intersection (coordinates of the intersection, the shape of the object, the index of the surface) plus the normal coordinates at this point.


#### Usage Example


The following example shows how you can get the normal of the intersection point by using the *PhysicsIntersectionNormal* class. In this example the line is an invisible traced line from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *[Player.GetDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the *PhysicsIntersectionNormal* class to get the normal of the intersection point.
- Check if there is a intersection with an object.
- When the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *PhysicsIntersectionNormal* class instance gets the normal of the intersection point. You can get it by using *[Normal](#getNormal_vec3)* property.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#if UNIGINE_DOUBLE
    using Vec3 = Unigine.dvec3;
    using Vec4 = Unigine.dvec4;
    using Mat4 = Unigine.dmat4;
#else
    using Vec3 = Unigine.vec3;
    using Vec4 = Unigine.vec4;
    using Mat4 = Unigine.mat4;
#endif

public partial class PhysicsIntersectionNormalClass : Component
{
	private void Init()
	{
		// create a mesh instance with a box surface
		Mesh mesh = new Mesh();
		mesh.AddBoxSurface("box", new vec3(2.2f));

		// create a new dynamic mesh from the Mesh instance
		ObjectMeshDynamic dynamic_mesh = new ObjectMeshDynamic(mesh);

		dynamic_mesh.WorldTransform = MathLib.Translate(new Vec3(0.0f, 0.0f, 2.0f));

		// assign a body and a shape to the dynamic mesh
		BodyRigid body = new BodyRigid(dynamic_mesh);
		ShapeBox shape = new ShapeBox(body, new vec3(2.2f));
	}

	private void Update()
	{
		// initialize points of the mouse direction
		Vec3 p0, p1;

		// get the current player (camera)
		Player player = Game.Player;

		// get the size of the current application window
		EngineWindow main_window = WindowManager.MainWindow;
		if (!main_window)
		{
			Engine.Quit();
			return;
		}

		ivec2 main_size = main_window.Size;

		// get the current X and Y coordinates of the mouse pointer
		int mouse_x = Gui.GetCurrent().MouseX;
		int mouse_y = Gui.GetCurrent().MouseY;
		// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
		player.GetDirectionFromScreen(out p0, out p1, mouse_x, mouse_y, 0, 0, main_size.x, main_size.y);

		// create the instance of the PhysicsIntersectionNormal object to save the information about the intersection
		PhysicsIntersectionNormal intersection = new PhysicsIntersectionNormal();
		// get an intersection
		Unigine.Object obj = Physics.GetIntersection(p0, p1, 1, intersection);

		// if the intersection has occurred, change the parameter of the object's material
		if (obj != null)
		{
			for (int i = 0; i < obj.NumSurfaces; i++)
			{
				obj.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 1.0f, 0.0f, 1.0f), i);
			}

			// if the intersected object has a shape, show the information about the intersection
			Shape shape = intersection.Shape;
			if (shape != null)
			{
				Log.Message("Normal coordinates: ({0} {1} {2})\n",
						intersection.Normal.x,
						intersection.Normal.y,
						intersection.Normal.z);
			}
		}
	}
}

```


## PhysicsIntersectionNormal Class

### Properties

## vec3 Normal

The normal of the intersection point.
### Members

---

## PhysicsIntersectionNormal ( )

The PhysicsIntersectionNormal constructor.
