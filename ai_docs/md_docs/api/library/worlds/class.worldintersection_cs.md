# Unigine::WorldIntersection Class (CS)


This class stores the result of the world intersection (the coordinates of the intersection, the index of the intersected triangle and the index of the intersected surface).


#### Usage Example


The following example shows how you can get the intersection information by using the *WorldIntersection* class. In this example, the line is an invisible traced line from the point of the camera (*vec3 **p0***) to the point of the mouse pointer (*vec3 **p1***). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *[Player.getDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the *WorldIntersection* class to get the intersection information.
- Check, if there is a intersection with an object. The [*World.getIntersection()*](../../../api/library/engine/class.world_cs.md#getIntersection_vec3_vec3_int_Variable_Object) function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *WorldIntersection* class instance gets the coordinates of the intersection point and the index of the intersected triangle. You can get all these fields by using [*getIndex()*](#getIndex_int) and [*getPoint()*](#getPoint_Vec3) functions


```csharp
/* ... */
// initialize points of the mouse direction
Vec3 p0, p1;

// get the current player (camera)
Player player = Game.Player;
if (player == null)
	return;

// get size (width and height) of the current application window
EngineWindow main_window = WindowManager.MainWindow;
if (!main_window)
	Engine.Quit();

ivec2 main_size = main_window.Size;

// get the current X and Y coordinates of the mouse pointer
int mouse_x = Input.MousePosition.x - main_window.Position.x;
int mouse_y = Input.MousePosition.y - main_window.Position.y;

// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
player.GetDirectionFromScreen(out p0, out p1, mouse_x, mouse_y, 0, 0, main_size.x, main_size.y);

// create an instance of the WorldIntersection class to get the result
WorldIntersection intersection = new WorldIntersection();

// create an instance for intersected object and check the intersection
Unigine.Object obj = World.GetIntersection(p0,p1,1,intersection);

// if the intersection has been occurred, change the parameter of the object's material
if(obj != null)
{
	for (int i = 0; i < obj.NumSurfaces; i++)
	{
		obj.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 0.0f, 0.0f, 1.0f),i);

		// show intersection details in console
		Log.Message("point: ({0} {1} {2}) index: {3} \n", intersection.Point.x, intersection.Point.y, intersection.Point.z, intersection.Index);
	}
}
/* ... */


```


## WorldIntersection Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **WORLD_INTERSECTION** = 0 | The intersection point (coordinates), the index of the intersected triangle of the object and the index of the intersected surface. |
| **WORLD_INTERSECTION_NORMAL** = 1 | The normal of the intersection point. |
| **WORLD_INTERSECTION_TEX_COORD** = 2 | The texture coordinates of the intersection point. |
| **NUM_WORLD_INTERSECTIONS** = 3 | Total number of world intersections. |

### Properties

## int Surface

The intersected surface number.
## int Instance

The number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
>
>
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cs.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cs.md)*


## int Index

The number of the intersected triangle.
## vec3 Point

The coordinates of the intersection point.
## 🔒︎ string TypeName

The *World Intersection* type name.
## 🔒︎ WorldIntersection.TYPE Type

The [*World Intersection* type identifier](#WORLD_INTERSECTION).
### Members

---

## WorldIntersection ( )

The WorldIntersection constructor.
