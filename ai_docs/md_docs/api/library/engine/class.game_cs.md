# Unigine::Game Class (CS)

> **Notice:** This class is a singleton.


This class contains functions to control the game logic of the application. It provides functionality for:


- Assigning a player to the *[Engine Camera](../../../editor2/camera_settings/index.md)* viewport.
- Pausing, speeding up and slowing down rendering, physics or game logic.


### Usage Example


The example below creates a *PlayerSpectator* and sets it as the active Engine Camera. The player is rotated around Y axis with the specified speed, which is set via *[setScale()](#setScale_float_void)*:


- Pressing F slows down the game logic, so player's rotation slows down too.
- Pressing G speeds up the game logic and, therefore, player's rotation.


```csharp
// declare a PlayerSpectator
PlayerSpectator player;

private void Init()
{
	// create a new PlayerSpectator instance
	player = new PlayerSpectator();

	// set necessary parameters: FOV, ZNear, ZFar, view direction vector and position.
	player.Fov = 90.0f;
	player.ZNear = 0.1f;
	player.ZFar = 10000.0f;
	player.ViewDirection = new vec3(0.0f, 1.0f, 0.0f);
	player.WorldPosition = new Vec3(-1.6f, -1.7f, 1.7f);

	// set the player to the Game singleton instance
	Game.Player = player;
}

private void Update()
{
	// slow down the game logic
	if (Input.IsKeyPressed(Input.KEY.F)) {
		Game.Scale /= 2;
		Log.Message("Game logic speed has been decreased. Frame duration is {0} seconds\n", Game.IFps);
	}

	// speed up the game logic
	if (Input.IsKeyPressed(Input.KEY.G)) {
		Game.Scale *= 2;
		Log.Message("Game logic speed has been increased. Frame duration is {0} seconds\n", Game.IFps);
	}

	// rotate the player 45 degrees per second around Y axis
	player.SetWorldRotation(player.GetWorldRotation() * new quat(0.0f, 1.0f, 0.0f, 45.0f * Game.IFps));
}


```


### See Also


- The article on the *[GameIntersection](../../../api/library/engine/class.gameintersection_cs.md)* class as a usage example of game intersections
- UnigineScript sample
- UnigineScript sample


## Game Class

### Properties

## Player Player

The player assigned to the *Engine Camera* viewport.
```csharp
Vec3 p0, p1;

// get the current player (camera)
Player player = Game.Player;
if (player == null)
	return;

// get width and height of the current application window
EngineWindow main_window = WindowManager.MainWindow;
if (!main_window)
{
	Engine.Quit();
	return;
}
ivec2 main_size = main_window.ClientSize;

// get the current X and Y coordinates of the mouse pointer
int mouse_x = Gui.GetCurrent().MouseX;
int mouse_y = Gui.GetCurrent().MouseY;

// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
player.GetDirectionFromScreen(out p0, out p1, mouse_x, mouse_y, 0, 0, main_size.x, main_size.y);


```


## Player PlayerListener

The *Player* used as sound listener.
## int Seed

The seed for pseudo-random number generator.
## float Time

The time spent in the game. The time is measured off starting from the world loading and does not take game pauses into account.
## float Scale

The value used to scale frame duration.
It scales up or down the speed of rendering, physics and game logic. This function can be used to create effects of slow/accelerated motion.


For example, if the scale equals **2**, the rate of simulation of all effects (such as particles) speeds up to two times faster. As for physics, in reality it will be simulated with the same fixed physics FPS, but the number of iterations will be two times higher. It is possible to scale the physics FPS separately via **[Physics.Scale](../../../api/library/physics/class.physics_cs.md#setScale_float_void)**.


This function scales the value set by the **[IFps](../../...md#setIFps_float_void)**.


## float IFps

The [scaled](#setScale_float_void) inverse FPS value (the time in seconds it took to complete the last frame).
This value does not depend on the real FPS the hardware is capable of. It enables you to force constant frame time increments between rendered frames, used for animation/expression update etc. Setting -1 removes the FPS limitation. Getting **0** means the game is paused.


This value is useful when grabbing a video reel with a fixed FPS value (for example, 25 frames per second).


```csharp
Node node;
// ...
// get an inverse FPS value
float ifps = Game.IFps;

// move the node up by 0.1 unit every second instead of every frame
node.WorldTranslate(new Vec3(0.0f, 0.0f, 0.1f*ifps));


```


## int Frame

The number of the current game frame.
```csharp
// get the current game frame
int loading_frames = Game.Frame;
// perform asynchronous nodes loading
// ...
// calculate the number of game frames required for nodes loading
loading_frames = Game.Frame - loading_frames;


```


## string Data

The user data associated with the game logic.
Data can contain an XML formatted string. This string is written directly into a `*.world` file. Namely, into the *data* child tag of the *game* tag, for example:


```xml
<?xml version="1.0" encoding="utf-8"?>
<world version="2.21.0.0">

	<game>
		<data>User data</data>
	</game>

</world>


```


## bool Enabled

The value indicating if the game is paused or not.
## 🔒︎ vec4 RandomColor

The random generated color vector: (R, G, B, A).
## 🔒︎ uint Random

The pseudo-random unsigned integer number.
### Members

---

## Obstacle GetIntersection ( vec3 p0 , vec3 p1 , float radius , int mask , Node [] exclude , vec3[] OUT_intersection )

Performs intersection search to find if a pathfinding Obstacle is located within the cylinder between two specified points.
The specified obstacles will be ignored.


> **Notice:** World space coordinates are used for this function.


![](cylinder01.png)


### Arguments

- *vec3* **p0** - Start point.
- *vec3* **p1** - End point.
- *float* **radius** - Radius of the intersection cylinder.
- *int* **mask** - Obstacle *Intersection* mask. The obstacle is ignored if its mask does not match.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **exclude** - Array with excluded obstacles. These obstacle nodes are ignored when performing intersection.
- *vec3[]* **OUT_intersection** - Intersection point. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Intersected obstacle.
## Obstacle GetIntersection ( vec3 p0 , vec3 p1 , float radius , int mask , GameIntersection intersection )


Performs an intersection search to determine whether a pathfinding obstacle is located within the cylinder defined by two specified points.


> **Notice:** World space coordinates are used for this function.


![](cylinder01.png)


The following example shows how you can get the intersection point (vec3) of the cylinder between two points with an obstacle. In this example we specify a cylinder from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1) with the specified radius. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *[Player.GetDirectionFromScreen()](../../../api/library/players/class.player_cs.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
2. Create an instance of the GameIntersection class to get the intersection point coordinates.
3. Check, if there is an intersection with an obstacle. The *Game.GetIntersection()* function returns an intersected obstacle when the obstacle appears in the area of the cylinder.
4. After that GameIntersection instance gets the point of the nearest intersection point and you can get it by using the *Point* property.


```csharp
/* ... */
// initialize points of the mouse direction
Vec3 p0, p1;

// get the current player (camera)
Player player = Game.Player;
if (player == null)
	return;
// get the size of the current application window
EngineWindow main_window = WindowManager.MainWindow;
if (!main_window)
{
	Engine.Quit();
	return;
}

ivec2 main_size = main_window.Size;

/// get the current X and Y coordinates of the mouse pointer
int mouse_x = Input.MousePosition.x - main_window.Position.x;
int mouse_y = Input.MousePosition.y - main_window.Position.y;

// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
player.GetDirectionFromScreen(out p0, out p1, 0, 0, mouse_x, mouse_y, main_size.x, main_size.y);

// create an instance of the GameIntersection class
GameIntersection intersection = new GameIntersection();

// try to get the intersection with an obstacle
// cylinder has radius 1.5f, Intersection mask equals to 1
Obstacle obstacle = Game.GetIntersection(p0, p1, 1.5f, 1, intersection);

// check, if the intersection of mouse direction with any obstacle was occurred;
if (obstacle != null)
{
	// show the coordinates of the intersection in console
	Log.Message("The intersection with the obstacle was here: ({0} {1} {2})\n", intersection.Point.x, intersection.Point.y, intersection.Point.z);
}
/* ... */


```


### Arguments

- *vec3* **p0** - Start point.
- *vec3* **p1** - End point.
- *float* **radius** - Radius of the intersection cylinder.
- *int* **mask** - Obstacle *Intersection* mask. The obstacle is ignored if its mask does not match.
- *[GameIntersection](../../../api/library/engine/class.gameintersection_cs.md)* **intersection** - [GameIntersection](../../../api/library/engine/class.gameintersection_cs.md) class instance to put the result into.

### Return value

Intersected obstacle.
## float GetNoise1 ( float pos , float size , int frequency )

Returns a noise value calculated using a Perlin noise function.
### Arguments

- *float* **pos** - Float position.
- *float* **size** - Size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

Noise value.
## float GetNoise2 ( vec2 pos , vec2 size , int frequency )

Returns a 2D noise value calculated using a Perlin noise function.
### Arguments

- *vec2* **pos** - vec2 point position.
- *vec2* **size** - vec2 size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

2D noise value.
## float GetNoise3 ( vec3 pos , vec3 size , int frequency )

Returns a 3D noise value calculated using a Perlin noise function.
### Arguments

- *vec3* **pos** - vec3 point position.
- *vec3* **size** - vec3 size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

3D noise value.
## double GetRandomDouble ( double from , double to )

Returns a pseudo-random *double* number within a given range (end-point not included).
### Arguments

- *double* **from** - The initial point of the range.
- *double* **to** - The end point of the range.

### Return value

Random *double* integer number.
## float GetRandomFloat ( float from , float to )

Returns a pseudo-random *float* number within a given range (end-point not included).
### Arguments

- *float* **from** - The initial point of the range.
- *float* **to** - The end point of the range.

### Return value

Random *float* number.
## int GetRandomInt ( int from , int to )

Returns a pseudo-random integer number within a given range (end-point not included).
### Arguments

- *int* **from** - The initial point of the range.
- *int* **to** - The end point of the range.

### Return value

Random integer number.
## void GetMainPlayers ( Player [] players )

Returns the array of pointers to players that are set as [main players](../../../api/library/players/class.player_cs.md#setMainPlayer_int_void).
### Arguments

- *[Player](../../../api/library/players/class.player_cs.md)[]* **players** - Array of pointers to main players.

## void GetListeners ( Player [] OUT_players )

Adds all potential listeners to the specified array.
### Arguments

- *[Player](../../../api/library/players/class.player_cs.md)[]* **OUT_players** - List to store potential listeners. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
