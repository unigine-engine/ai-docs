# Unigine::WorldIntersectionNormal Class (CS)

**Inherits from:** WorldIntersection


This class stores the normal at the intersection point. You should use this class when you need additional information about the normal at the intersection point (it also stores the coordinates of the intersection, the index of the intersected triangle, and the index of the intersected surface).


#### Usage Example


The following example shows how you can get the intersection information by using the *WorldIntersection* class. In this example, the line is an invisible traced line from the point of the camera (*vec3 **p0***) to the point of the mouse pointer (*vec3 **p1***). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *[Player.getDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the *WorldIntersectionNormal*class to get the intersection information.
- Check, if there is a intersection with an object. The [*World.getIntersection()*](../../../api/library/engine/class.world_cs.md#getIntersection_vec3_vec3_int_Variable_Object) function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *WorldIntersectionNormal* class instance gets the normal of the intersection point. You can get the normal by using the [*getNormal()*](#getNormal_vec3) function.


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

// create an instance of the WorldIntersectionNormal class to get the result
WorldIntersectionNormal intersection = new WorldIntersectionNormal();

// create an instance for intersected object and check the intersection
Unigine.Object obj = World.GetIntersection(p0,p1,1,intersection);

// if the intersection has been occurred, change the parameter of the object's material
if(obj != null)
{
	for (int i = 0; i < obj.NumSurfaces; i++)
	{
		obj.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 0.0f, 0.0f, 1.0f),i);

		// show intersection details in console
		Log.Message("Normal: type {0} coordinates ({1} {2} {3})\n", intersection.Type,
			intersection.Normal.x,
			intersection.Normal.y,
			intersection.Normal.z);
	}
}
/* ... */


```


## WorldIntersectionNormal Class

### Properties

## vec3 Normal

The normal at the intersection point.
### Members

---

## WorldIntersectionNormal ( )

The WorldIntersectionNormal constructor.
