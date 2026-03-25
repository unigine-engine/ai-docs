# Unigine::Game Class (CPP)

**Header:** #include <UnigineGame.h>

> **Notice:** This class is a singleton.


This class contains functions to control the game logic of the application. It provides functionality for:


- Assigning a player to the *[Engine Camera](../../../editor2/camera_settings/index.md)* viewport.
- Pausing, speeding up and slowing down rendering, physics or game logic.


### Usage Example


The example below creates a PlayerSpectator and sets it as the active Engine Camera. The player is rotated around Y axis with the specified speed, which is set via *[setScale()](#setScale_float_void)*:


- Pressing F slows down the game logic, so player's rotation slows down too.
- Pressing G speeds up the game logic and, therefore, player's rotation.


```cpp
#include "AppWorldLogic.h"
#include <UniginePlayers.h>
#include <UnigineGame.h>

using namespace Unigine;
using namespace Math;

	// declare a PlayerSpectator pointer
	PlayerSpectatorPtr player;

int AppWorldLogic::init()
{

	// create a new PlayerSpectator instance
	player = PlayerSpectator::create();

	// set necessary parameters: FOV, ZNear, ZFar, view direction vector and position.
	player->setFov(90.0f);
	player->setZNear(0.1f);
	player->setZFar(10000.0f);
	player->setViewDirection(vec3(0.0f, 1.0f, 0.0f));
	player->setWorldPosition(Vec3(-1.6f, -1.7f, 1.7f));

	// set the player to the Game singleton instance
	Game::setPlayer(player);

	return 1;
}

int AppWorldLogic::update()
{

	// slow down the game logic
	if (Input::isKeyDown(Input::KEY_F)) {
		Game::setScale(Game::getScale() / 2);
		Log::message("Game logic speed has been decreased. Frame duration is %f seconds\n", Game::getIFps());
	}

	// speed up the game logic
	if (Input::isKeyDown(Input::KEY_G)) {
		Game::setScale(Game::getScale() * 2);
		Log::message("Game logic speed has been increased. Frame duration is %f seconds\n", Game::getIFps());
	}

	// rotate the player 45 degrees per second around Y axis
	player->setWorldRotation(player->getWorldRotation() * quat(0.0f, 1.0f, 0.0f, 45.0f * Game::getIFps()));

	return 1;
}

int AppWorldLogic::shutdown()
{

	// clear the pointer
	player.clear();

	return 1;
}


```


### See Also


- The article on the *[GameIntersection](../../../api/library/engine/class.gameintersection_cpp.md)* class as a usage example of game intersections
- UnigineScript sample
- UnigineScript sample


## Game Class

### Members

---

## void setData ( const char * data )

Sets user data associated with the game logic. This string is written directly into a `*.world` file. Namely, into the *data* child tag of the *game* tag, for example:
```xml
<?xml version="1.0" encoding="utf-8"?>
<world version="2.16.0.2">

	<game>
		<data>User data</data>
	</game>

</world>


```


### Arguments

- *const char ** **data** - User data. Data can contain an XML formatted string.

## const char * getData ( ) const

Returns user data associated with the game logic. This string is written directly into a `*.world` file. Namely, into the *data* child tag of the *game* tag, for example:
```xml
<?xml version="1.0" encoding="utf-8"?>
<world version="2.16.0.2">

	<game>
		<data>User data</data>
	</game>

</world>


```


### Return value

User data. Data can contain an XML formatted string.
## void setEnabled ( bool enabled )

Pauses or resumes the game logic.
### Arguments

- *bool* **enabled** - **1** to resume the game logic, **0** to pause it.

## bool isEnabled ( ) const

Returns a value indicating if the game is paused or not.
### Return value

true if the game logic is not paused; otherwise, false.
## void setFrame ( int frame )

Sets the game frame with the given number as the current one.
### Arguments

- *int* **frame** - Frame number.

## int getFrame ( ) const

Returns the number of the current game frame.
```cpp
// get the current game frame
int loading_frames = Game::getFrame();
// perform asynchronous nodes loading
// ...
// calculate the number of game frames required for nodes loading
loading_frames = Game::getFrame() - loading_frames;


```


### Return value

Frame number.
## void setIFps ( float ifps )

Sets the [scaled](#setScale_float_void) inverse FPS value (the time in seconds it took to complete the last frame). This function sets a fixed FPS that does not depend on the real FPS the hardware is capable of. That is, it forces constant frame time increments between rendered frames, used for animation/expression update etc. To remove the FPS limitation, use -1.
The function is useful when grabbing the video reel with a fixed FPS value (for example, 25 frames per second).


### Arguments

- *float* **ifps** - Inverse FPS value (1/FPS) in seconds.**-1** removes the FPS limitation.

## float getIFps ( ) const

Returns the [scaled](#setScale_float_void) inverse FPS value (the time in seconds it took to complete the last frame). This value does not depend on the real FPS the hardware is capable of. -1 means no Inverse FPS value is set.
```cpp
NodePtr node;
// ...
// get an inverse FPS value
float ifps = Game::getIFps();

// move the node up by 0.1 unit every second instead of every frame
node->worldTranslate(Math::Vec3(0.0f, 0.0f, 0.1f * ifps));


```


### Return value

Scaled inverse FPS value (1/FPS) in seconds. If the game is paused, **0** is returned.
## Ptr < Obstacle > getIntersection ( Vec3 p0 , Vec3 p1 , float radius , int mask , const Vector < Ptr < Node >> & exclude , Math:: Vec3 * OUT_intersection )

Performs intersection to find if a pathfinding Obstacle is located within the cylinder between two points. The specified obstacles will be ignored.
> **Notice:** World space coordinates are used for this function.


![](cylinder01.png)


### Arguments

- *[Vec3](../../../api/library/math/class.vec3_cpp.md)* **p0** - Start point.
- *[Vec3](../../../api/library/math/class.vec3_cpp.md)* **p1** - End point.
- *float* **radius** - Radius of the intersection cylinder.
- *int* **mask** - Obstacle intersection mask. The obstacle is ignored if its mask does not match.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **exclude** - Array with excluded obstacles. These obstacle nodes are ignored when performing intersection.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) ** **OUT_intersection** - Intersection point. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Intersected obstacle.
## Ptr < Obstacle > getIntersection ( Vec3 p0 , Vec3 p1 , float radius , int mask , const Ptr < GameIntersection > & intersection )


Performs intersection to find if a pathfinding obstacle is located within the cylinder between two points.


> **Notice:** World space coordinates are used for this function.


![](cylinder01.png)


The following example shows how you can get the intersection point (vec3) of the cylinder between two points with an obstacle. In this example we specify a cylinder from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1) with the specified radius. The executing sequence is the following:

1. Define and initialize two points (p0 and p1) by using the *[Player::getDirectionFromScreen()](../../../api/library/players/class.player_cpp.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)*.
2. Create an instance of the GameIntersection class to get the intersection point coordinates.
3. Check, if there is an intersection with an obstacle. The *Game::getIntersection()* function returns an intersected obstacle when the obstacle appears in the area of the cylinder.
4. After that GameIntersection instance gets the point of the nearest intersection point and you can get it by using the *getPoint()* function.


```cpp
/* ... */
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
player->getDirectionFromScreen(p0, p1, 0, 0, mouse_x, mouse_y, main_size.x, main_size.y);

// create an instance of the GameIntersection class
GameIntersectionPtr intersection = GameIntersection::create();

// try to get the intersection with an obstacle
// cylinder has radius 1.5f, intersection mask equals to 1
ObstaclePtr obstacle = Game::getIntersection(p0, p1, 1.5f, 1, intersection);

// check if the intersection of mouse direction with any obstacle has occurred
if (obstacle)
{
	// show the coordinates of the intersection in console
	Log::message("The intersection with the obstacle was here: (%f %f %f)\n", intersection->getPoint().x, intersection->getPoint().y, intersection->getPoint().z);
}
/* ... */


```


### Arguments

- *[Vec3](../../../api/library/math/class.vec3_cpp.md)* **p0** - Start point.
- *[Vec3](../../../api/library/math/class.vec3_cpp.md)* **p1** - End point.
- *float* **radius** - Radius of the intersection cylinder.
- *int* **mask** - Obstacle intersection mask. The obstacle is ignored if its mask does not match.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[GameIntersection](../../../api/library/engine/class.gameintersection_cpp.md)> &* **intersection** - [GameIntersection](../../../api/library/engine/class.gameintersection_cpp.md) class instance to put the result into.

### Return value

Intersected obstacle.
## float getNoise1 ( float pos , float size , int frequency ) const

Returns a noise value calculated using a Perlin noise function.
### Arguments

- *float* **pos** - Float position.
- *float* **size** - Size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

Noise value.
## float getNoise2 ( const Math:: vec2 & pos , const Math:: vec2 & size , int frequency ) const

Returns a 2D noise value calculated using a Perlin noise function.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **pos** - vec2 point position.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **size** - vec2 size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

2D noise value.
## float getNoise3 ( const Math:: vec3 & pos , const Math:: vec3 & size , int frequency ) const

Returns a 3D noise value calculated using a Perlin noise function.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **pos** - vec3 point position.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - vec3 size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

3D noise value.
## void setPlayer ( const Ptr < Player > & player )

Assigns a new player to the *Engine Camera* viewport.
```cpp
// create a new player
PlayerDummyPtr player = PlayerDummy::create();
// set necessary parameters
player->setFov(60.0f);
player->setWorldPosition(Math::Vec3(-1.0f, -1.0f, 1.0f));
// set the player to the Game singleton instance
Game::setPlayer(player);


```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Player](../../../api/library/players/class.player_cpp.md)> &* **player** - Player to set as a current one.

## Ptr < Player > getPlayer ( ) const

Returns the current player assigned to the *Engine Camera* viewport.
```cpp
Vec3 p0, p1;

// get the current player (camera)
PlayerPtr player = Game::getPlayer();

if (player.get() == NULL)
	return 0;

// get width and height of the current application window's client area
Math::ivec2 winsize = WindowManager::getMainWindow()->getClientSize();
int width = winsize.x;
int height = winsize.y;

// get the current X and Y coordinates of the mouse pointer
int mouse_x = Gui::getCurrent()->getMouseX();
int mouse_y = Gui::getCurrent()->getMouseY();

// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
player->getDirectionFromScreen(p0, p1, mouse_x, mouse_y, 0, 0, width, height);


```


### Return value

Current player.
## unsigned int getRandom ( ) const

Returns a pseudo-random unsigned integer number.
### Return value

Random unsigned integer number.
## double getRandomDouble ( double from , double to )

Returns a pseudo-random double number within a given range (end-point not included).
### Arguments

- *double* **from** - The initial point of the range.
- *double* **to** - The end point of the range.

### Return value

Random double integer number.
## float getRandomFloat ( float from , float to )

Returns a pseudo-random float number within a given range (end-point not included).
### Arguments

- *float* **from** - The initial point of the range.
- *float* **to** - The end point of the range.

### Return value

Random float number.
## int getRandomInt ( int from , int to )

Returns a pseudo-random integer number within a given range (end-point not included).
### Arguments

- *int* **from** - The initial point of the range.
- *int* **to** - The end point of the range.

### Return value

Random integer number.
## void setScale ( float scale )


Sets a value that is used to scale frame duration. It scales up or down the speed of rendering, physics and game logic. This function can be used to create effects of slow/accelerated motion.


For example, if the scale equals **2**, the rate of simulation of all effects (such as particles) speeds up to two times faster. As for physics, in reality it will be simulated with the same fixed physics FPS, but the number of iterations will be two times higher. It is possible to scale the physics FPS separately via [*engine.physics.setScale()*](../../../api/library/physics/class.physics_cpp.md#setScale_float_void) function.


This function scales the value set by the [*setIFps()*](#setIFps_float_void).


### Arguments

- *float* **scale** - Scaling factor. The provided values is clamped within the range **[0;32]**.

## float getScale ( ) const

Returns a value used to scale the frame duration.
### Return value

Value to scale the frame duration.
## void setSeed ( int seed )

Sets the seed for pseudo-random number generator.
### Arguments

- *int* **seed** - Number used to initialize a pseudo-random sequence of numbers.

## int getSeed ( ) const

Returns the seed for pseudo-random number generator.
### Return value

Number used to initialize a pseudo-random sequence of numbers.
## void setTime ( float time )

Sets the time value for the game. The time is counted off starting from the world loading and does not take game pauses into account.
### Arguments

- *float* **time** - Time in seconds.

## float getTime ( ) const

Returns the current time spent in the game. It is counted off starting from the world loading and does not take game pauses into account.
### Return value

Time in seconds.
## void getMainPlayers ( const Vector < Ptr < Player > > & players )

Returns the array of pointers to players that are set as [main players](../../../api/library/players/class.player_cpp.md#setMainPlayer_int_void).
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Player](../../../api/library/players/class.player_cpp.md)> > &* **players** - Array of pointers to main players.

## Math:: vec4 getRandomColor ( ) const

Returns a random generated color vector: (R, G, B, A).
### Return value

Four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector representing a color: (R, G, B, A).
## void setPlayerListener ( const Ptr < Player > & listener )

Sets the player as listener.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Player](../../../api/library/players/class.player_cpp.md)> &* **listener** - Player to be set as listener.

## Ptr < Player > getPlayerListener ( ) const

Returns the player which is currently the listener.
### Return value

The player that is set as listener.
## void getListeners ( Vector < Ptr < Player > > & OUT_players )

Adds all potential listeners to the specified array.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Player](../../../api/library/players/class.player_cpp.md)> > &* **OUT_players** - List to store potential listeners. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
