# Unigine::GameIntersection Class (CS)


Stores the result of the *[*Game.getIntersection()*](../../../api/library/engine/class.game_cs.md#getIntersection_Vec3_Vec3_float_int_GameIntersection_Obstacle)* function - the point where the intersection with an [obstacle](../../../api/library/pathfinding/class.obstacle_cs.md) has been occurred.


![](cylinder01.png)


### Usage Example


The following example shows how you can get the intersection point (vec3) of the cylinder between two points with an obstacle. In this example we specify a cylinder from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1) with the specified radius. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *[Player.getDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)*.
2. Create an instance of the GameIntersection class to get the intersection point coordinates.
3. Check, if there is an intersection with an obstacle. The *Game.getIntersection()* function returns an intersected obstacle when the obstacle appears in the area of the cylinder.
4. After that *GameIntersection* instance gets the point of the nearest intersection point and you can get it by using the *getPoint()* function.


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

// create an instance of the GameIntersection class
GameIntersection intersection = new GameIntersection();

// try to get the intersection with an obstacle
// cylinder has radius 1.5f, intersection mask equals to 1
Obstacle obstacle = Game.GetIntersection(p0, p1, 1.5f, 1, intersection);

// check, if the intersection of mouse direction with any obstacle was occurred;
if (obstacle != null)
{
	// show the coordinates of the intersection in console
	Log.Message("The intersection with the obstacle was here: ({0} {1} {2})\n", intersection.Point.x, intersection.Point.y, intersection.Point.z);
}
/* ... */


```


## GameIntersection Class

### Properties

## vec3 Point

The coordinates of the intersection point.
### Members

---

## GameIntersection ( )

The GameIntersection constructor.
