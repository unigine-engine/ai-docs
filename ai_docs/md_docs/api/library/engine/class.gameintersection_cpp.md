# Unigine::GameIntersection Class (CPP)

**Header:** #include <UnigineGame.h>


Stores the result of the *[*Game::getIntersection()*](../../../api/library/engine/class.game_cpp.md#getIntersection_Vec3_Vec3_float_int_GameIntersection_Obstacle)* function - the point where the intersection with an [obstacle](../../../api/library/pathfinding/class.obstacle_cpp.md) has been occurred.


![](cylinder01.png)


### Usage Example


The following example shows how you can get the intersection point (vec3) of the cylinder between two points with an obstacle. In this example we specify a cylinder from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1) with the specified radius. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *[Player::getDirectionFromScreen()](../../../api/library/players/class.player_cpp.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)*.
2. Create an instance of the GameIntersection class to get the intersection point coordinates.
3. Check, if there is an intersection with an obstacle. The *Game::getIntersection()* function returns an intersected obstacle when the obstacle appears in the area of the cylinder.
4. After that *GameIntersection* instance gets the point of the nearest intersection point and you can get it by using the *getPoint()* function.


```cpp
// initialize points of the mouse direction
Vec3 p0, p1;

// get the current player (camera)
PlayerPtr player = Game::getPlayer();
if (player.get() == NULL)
	return 0;

// get width and height of the current application window
ivec2 main_size = ivec2_one;
EngineWindowPtr main_window = WindowManager::getMainWindow();
if (!main_window)
	Engine::get()->quit();

main_size = main_window->getSize();

// get the current X and Y coordinates of the mouse pointer
int mouse_x = Input::getMousePosition().x - main_window->getPosition().x;
int mouse_y = Input::getMousePosition().y - main_window->getPosition().y;

// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
player->getDirectionFromScreen(p0, p1, mouse_x, mouse_y, 0, 0, main_size.x, main_size.y);

// create an instance of the GameIntersection class
GameIntersectionPtr intersection = GameIntersection::create();

// try to get the intersection with an obstacle
// cylinder has radius 1.5f, intersection mask equals to 1
ObstaclePtr obstacle = Game::getIntersection(p0, p1, 1.5f, 1, intersection);

// check, if the intersection of mouse direction with any obstacle was occurred;
if (obstacle)
{
	// show the coordinates of the intersection in console
	Log::message("The intersection with the obstacle was here: (%f %f %f)\n", intersection->getPoint().x, intersection->getPoint().y, intersection->getPoint().z);
}
/* ... */


```


## GameIntersection Class

### Members

## void setPoint ( const const Math:: Vec3 && point )

Sets a new coordinates of the intersection point.
### Arguments

- *const const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &&* **point** - The coordinates of the intersection point.

## const Math:: Vec3 & getPoint () const

Returns the current coordinates of the intersection point.
### Return value

Current coordinates of the intersection point.
---

## static GameIntersectionPtr create ( )

The GameIntersection constructor.
