# Unigine::PhysicsIntersection Class (CS)


This class stores the result of the physics intersection (coordinates of the intersection, the shape of the object, the index of the surface). If you need information on the normal at the intersection point, use the *[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cs.md)* class.


#### Usage Example


The following example shows how you can get the intersection information by using the *PhysicsIntersection* class. In this example we specify a line from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)*. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *[Player.GetDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
2. Create an instance of the *PhysicsIntersection* class to get the intersection information.
3. Check, if there is an intersection with an object with a shape or a collision object. The *[GetIntersection()](../../../api/library/physics/class.physics_cs.md#getIntersection_Vec3_Vec3_int_Variable)* function returns an intersected object when the object intersects with the traced line.
4. When the object intersects with the traced line, all surfaces of the intersected object change their material parameters. If the object has a shape, its information will be shown in console. The *PhysicsIntersection* class instance gets the coordinates of the intersection point and the *Shape* class object. You can get all these fields by using the *[Shape](../../../api/library/physics/class.physicsintersection_cs.md#getShape_Shape), [Point](../../../api/library/physics/class.physicsintersection_cs.md#getPoint_Vec3)* properties.


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

public partial class PhysicsIntersectionClass : Component
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

		// create the instance of the PhysicsIntersection object to save the information about the intersection
		PhysicsIntersection intersection = new PhysicsIntersection();
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
				Log.Message("physics intersection info: point: ({0} {1} {2}) shape: {3}\n", intersection.Point.x, intersection.Point.y, intersection.Point.z, shape.TypeName);
			}
		}

	}
}

```


## PhysicsIntersection Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **PHYSICS_INTERSECTION** = 0 | PhysicsIntersection object, which stores basic information on the intersection point (coordinates of the intersection, the shape of the object, the index of the surface). |
| **PHYSICS_INTERSECTION_NORMAL** = 1 | [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cs.md) object, which stores the same information as the PhysicsIntersection object plus additional information on the normal at the intersection point. |
| **NUM_PHYSICS_INTERSECTIONS** = 2 | Number of physics intersection types. |

### Properties

## int Surface

The intersected surface number.
## vec3 Point

The coordinates of the intersection point.
## Shape Shape

The intersected shape.
## 🔒︎ string TypeName

The name of the intersection object type.
## 🔒︎ PhysicsIntersection.TYPE Type

The intersection object type, one of the [PHYSICS_INTERSECTION*](#PHYSICS_INTERSECTION) values.
### Members

---

## PhysicsIntersection ( )

The PhysicsIntersection constructor.
