# Unigine::WorldIntersectionTexCoord Class (CS)

**Inherits from:** WorldIntersectionNormal


This class stores the texture coordinates of the intersection point. You should use this class when you need additional information about the texture coordinates at the intersection point (it also stores the coordinates of the intersection, the index of the intersected triangle, the index of the intersected surface, and normal coordinates at the intersection point).


#### Usage Example


The following example shows how you can get texture coordinates at the intersection point (vec4) by using the *WorldIntersectionTexCoord* class. In this example the line is an invisible traced line from the point of the camera (*vec3 **p0***) to the point of the mouse pointer (*vec3 **p1***). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *[Player.getDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the *WorldIntersectionTexCoord* class to get the intersection information.
- Check, if there is a intersection with an object. The [*World.getIntersection()*](../../../api/library/engine/class.world_cs.md#getIntersection_vec3_vec3_int_Variable_Object) function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *WorldIntersectionTexCoord* class instance gets the texture coordinates of the intersection point. You can get the texture coordinates by using the [*getTexCoord()*](#getTexCoord_vec4) function.


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

// create an instance of the WorldIntersectionTextCoord class to get the result
WorldIntersectionTexCoord intersection = new WorldIntersectionTexCoord();

// create an instance for intersected object and check the intersection
Unigine.Object obj = World.GetIntersection(p0,p1,1,intersection);

// if the intersection has been occurred, change the parameter of the object's material
if(obj != null)
{
	for (int i = 0; i < obj.NumSurfaces; i++)
	{
		obj.SetMaterialParameterFloat4("albedo_color", new vec4(1.0f, 0.0f, 0.0f, 1.0f),i);

		// show intersection details in console
		Log.Message("Texture coordinates ({0} {1} {2} {3})\n",
			intersection.TexCoord.x,
			intersection.TexCoord.y,
			intersection.TexCoord.z,
			intersection.TexCoord.w);
	}
}
/* ... */


```


## WorldIntersectionTexCoord Class

### Properties

## vec4 TexCoord

The texture coordinates of the intersection point.
### Members

---

## WorldIntersectionTexCoord ( )

The WorldIntersectionTexCoord constructor.
