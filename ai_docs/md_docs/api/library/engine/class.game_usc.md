# Unigine::Game Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class contains functions to control the game logic of the application. It provides functionality for:


- Assigning a player to the *[Engine Camera](../../../editor2/camera_settings/index.md)* viewport.
- Pausing, speeding up and slowing down rendering, physics or game logic.


### Usage Example


The example below creates a *PlayerSpectator* and sets it as the active Engine Camera. The player is rotated around Y axis with the specified speed, which is set via *[setScale()](#setScale_float_void)*:


- Pressing F slows down the game logic, so player's rotation slows down too.
- Pressing G speeds up the game logic and, therefore, player's rotation.


```cpp
#include <core/unigine.h>

// declare a PlayerSpectator
PlayerSpectator player;

int init() {

	// create a new PlayerSpectator instance
	player = new PlayerSpectator();

	// set necessary parameters: FOV, ZNear, ZFar, view direction vector and position.
	player.setFov(90.0f);
	player.setZNear(0.1f);
	player.setZFar(10000.0f);
	player.setViewDirection(vec3(0.0f, 1.0f, 0.0f));
	player.setWorldPosition(dvec3(-1.6f, -1.7f, 1.7f));

	// set the player to the Game singleton instance
	engine.game.setPlayer(player);

	return 1;
}

int update() {

	// slow down the game logic
	if (engine.app.clearKeyState('f')) {
		engine.game.setScale(0.2f);
		log.message("Game logic speed has been decreased. Frame duration is %f seconds\n", engine.game.getFTime());
	}

	// speed up the game logic
	if (engine.app.clearKeyState('g')) {
		engine.game.setScale(2.0f);
		log.message("Game logic speed has been increased. Frame duration is %f seconds\n", engine.game.getFTime());
	}

	// rotate the player 45 degrees per second around Y axis
	player.setWorldRotation(player.getWorldRotation() * quat(0.0f, 1.0f, 0.0f, 45.0f * engine.game.getIFps()));

	return 1;
}

```


### See Also


- The article on the *[GameIntersection](../../../api/library/engine/class.gameintersection_usc.md)* class as a usage example of game intersections
- UnigineScript sample
- UnigineScript sample


## Game Class

### Members

## void setPlayer ( Player player )

Sets a new player assigned to the *Engine Camera* viewport.
```cpp
// create a new player
PlayerDummy dummy = new PlayerDummy();

// set necessary parameters
dummy.setPosition(Vec3(-20.0f,0.0f,15.0f));
dummy.setDirection(vec3(1.0f,0.0f,-0.8f));
// set the player to the Engine Camera viewport
engine.game.setPlayer(dummy);

```


### Arguments

- *[Player](../../../api/library/players/class.player_usc.md)* **player** - The

## Player getPlayer () const

Returns the current player assigned to the *Engine Camera* viewport.
```cpp
// create a new player
PlayerDummy dummy = new PlayerDummy();

// set necessary parameters
dummy.setPosition(Vec3(-20.0f,0.0f,15.0f));
dummy.setDirection(vec3(1.0f,0.0f,-0.8f));
// set the player to the Engine Camera viewport
engine.game.setPlayer(dummy);

```


### Return value

Current
## void setPlayerListener ( Player listener )

Sets a new *Player* used as sound listener.
### Arguments

- *[Player](../../../api/library/players/class.player_usc.md)* **listener** - The *Player* used as sound listener.

## Player getPlayerListener () const

Returns the current *Player* used as sound listener.
### Return value

Current *Player* used as sound listener.
## void setSeed ( int seed )

Sets a new seed for pseudo-random number generator.
### Arguments

- *int* **seed** - The number used to initialize a pseudo-random sequence of numbers.

## int getSeed () const

Returns the current seed for pseudo-random number generator.
### Return value

Current number used to initialize a pseudo-random sequence of numbers.
## void setTime ( float time )

Sets a new time spent in the game. The time is measured off starting from the world loading and does not take game pauses into account.
### Arguments

- *float* **time** - The time, in seconds.

## float getTime () const

Returns the current time spent in the game. The time is measured off starting from the world loading and does not take game pauses into account.
### Return value

Current time, in seconds.
## void setScale ( float scale )

Sets a new value used to scale frame duration.
It scales up or down the speed of rendering, physics and game logic. This function can be used to create effects of slow/accelerated motion.


For example, if the scale equals **2**, the rate of simulation of all effects (such as particles) speeds up to two times faster. As for physics, in reality it will be simulated with the same fixed physics FPS, but the number of iterations will be two times higher. It is possible to scale the physics FPS separately via **[engine.physics.setScale()()](../../../api/library/physics/class.physics_usc.md#setScale_float_void)**.


This function scales the value set by the **[setIFps()()](../../...md#setIFps_float_void)**.


### Arguments

- *float* **scale** - The value used to scale the frame duration. The provided value is clamped within the range [0;32].

## float getScale () const

Returns the current value used to scale frame duration.
It scales up or down the speed of rendering, physics and game logic. This function can be used to create effects of slow/accelerated motion.


For example, if the scale equals **2**, the rate of simulation of all effects (such as particles) speeds up to two times faster. As for physics, in reality it will be simulated with the same fixed physics FPS, but the number of iterations will be two times higher. It is possible to scale the physics FPS separately via **[engine.physics.setScale()()](../../../api/library/physics/class.physics_usc.md#setScale_float_void)**.


This function scales the value set by the **[setIFps()()](../../...md#setIFps_float_void)**.


### Return value

Current value used to scale the frame duration. The provided value is clamped within the range [0;32].
## void setIFps ( float ifps )

Sets a new [scaled](#setScale_float_void) inverse FPS value (the time in seconds it took to complete the last frame).
This value does not depend on the real FPS the hardware is capable of. It enables you to force constant frame time increments between rendered frames, used for animation/expression update etc. Setting -1 removes the FPS limitation. Getting **0** means the game is paused.


This value is useful when grabbing a video reel with a fixed FPS value (for example, 25 frames per second).


```cpp
Node node;
// ...
// get an inverse FPS value
float ifps = engine.game.getIFps();

// move the node up by 0.1 unit every second instead of every frame
node.worldTranslate(Vec3(0.0f, 0.0f, 0.1f*ifps));

```


### Arguments

- *float* **ifps** - The inverse FPS value (1/FPS) in seconds.**-1** means that FPS limitation is removed.

## float getIFps () const

Returns the current [scaled](#setScale_float_void) inverse FPS value (the time in seconds it took to complete the last frame).
This value does not depend on the real FPS the hardware is capable of. It enables you to force constant frame time increments between rendered frames, used for animation/expression update etc. Setting -1 removes the FPS limitation. Getting **0** means the game is paused.


This value is useful when grabbing a video reel with a fixed FPS value (for example, 25 frames per second).


```cpp
Node node;
// ...
// get an inverse FPS value
float ifps = engine.game.getIFps();

// move the node up by 0.1 unit every second instead of every frame
node.worldTranslate(Vec3(0.0f, 0.0f, 0.1f*ifps));

```


### Return value

Current inverse FPS value (1/FPS) in seconds.**-1** means that FPS limitation is removed.
## void setFrame ( int frame )

Sets a new number of the current game frame.
```cpp
// get the current game frame
int loading_frames = engine.game.getFrame();
// perform asynchronous nodes loading
// ...
// calculate the number of game frames required for nodes loading
loading_frames = engine.game.getFrame() - loading_frames;

```


### Arguments

- *int* **frame** - The number of the current game frame.

## int getFrame () const

Returns the current number of the current game frame.
```cpp
// get the current game frame
int loading_frames = engine.game.getFrame();
// perform asynchronous nodes loading
// ...
// calculate the number of game frames required for nodes loading
loading_frames = engine.game.getFrame() - loading_frames;

```


### Return value

Current number of the current game frame.
## void setData ( string data )

Sets a new user data associated with the game logic.
Data can contain an XML formatted string. This string is written directly into a `*.world` file. Namely, into the *data* child tag of the *game* tag, for example:


```xml
<?xml version="1.0" encoding="utf-8"?>
<world version="2.21.0.0">

	<game>
		<data>User data</data>
	</game>

</world>


```


### Arguments

- *string* **data** - The

## const char * getData () const

Returns the current user data associated with the game logic.
Data can contain an XML formatted string. This string is written directly into a `*.world` file. Namely, into the *data* child tag of the *game* tag, for example:


```xml
<?xml version="1.0" encoding="utf-8"?>
<world version="2.21.0.0">

	<game>
		<data>User data</data>
	</game>

</world>


```


### Return value

Current
## void setEnabled ( bool enabled )

Sets a new value indicating if the game is paused or not.
### Arguments

- *bool* **enabled** - true if the game logic is not paused; otherwise, false.

## bool isEnabled () const

Returns the current value indicating if the game is paused or not.
### Return value

true if the game logic is not paused; otherwise, false.
## vec4 getRandomColor () const

Returns the current random generated color vector: (R, G, B, A).
### Return value

Current random four-component [vec4](../../../api/library/math/class.vec4_usc.md) vector representing a color: (R, G, B, A).
## unsigned int getRandom () const

Returns the current pseudo-random unsigned integer number.
### Return value

Current pseudo-random unsigned integer number.
---

## Obstacle engine.game. getIntersection ( Vec3 p0 , Vec3 p1 , float radius , int mask , int[] exclude , GameIntersection OUT_intersection )

Performs intersection search to find if a pathfinding Obstacle is located within the cylinder between two specified points.
The specified obstacles will be ignored.


> **Notice:** World space coordinates are used for this function.


![](cylinder01.png)


### Arguments

- *Vec3* **p0** - Start point.
- *Vec3* **p1** - End point.
- *float* **radius** - Radius of the intersection cylinder.
- *int* **mask** - Obstacle *Intersection* mask. The obstacle is ignored if its mask does not match.
- *int[]* **exclude** - Array with excluded obstacles. These obstacle nodes are ignored when performing intersection.
- *[GameIntersection](../../../api/library/engine/class.gameintersection_usc.md)* **OUT_intersection** - [GameIntersection](../../../api/library/engine/class.gameintersection_usc.md) class instance to put the result into. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Intersected obstacle.
## Obstacle engine.game. getIntersection ( Vec3 p0 , Vec3 p1 , float radius , int mask , GameIntersection intersection )


Performs an intersection search to determine whether a pathfinding obstacle is located within the cylinder defined by two specified points.


> **Notice:** World space coordinates are used for this function.


![](cylinder01.png)


The following example shows how you can get the intersection point (vec3) of the cylinder between two points with an obstacle. In this example the cylinder is an invisible traced cylinder from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1) with the specific radius. The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *getPlayerMouseDirection()* function from `core/scripts/utils.h`.
- Create an instance of the GameIntersection class to get the intersection point coordinates.
- Check, if there is a intersection with an obstacle. The *engine.game.getIntersection()* function returns an intersected obstacle when the obstacle appears in the area of the cylinder.
- After that GameIntersection instance gets the point of the nearest intersection point and you can get it by using the *getPoint()* function.


```cpp
#include <core/scripts/utils.h>
/* ... */
// define two vec3 coordinates
vec3 p0,p1;
// get the mouse direction from camera (p0) to cursor pointer (p1)
getPlayerMouseDirection(p0,p1);

// create an instance of the GameIntersection class
GameIntersection intersection = new GameIntersection();

// try to get the intersection with an obstacle.
// cylinder has radius 0.1f, Intersection mask equals to 1
Obstacle obstacle = engine.game.getIntersection(p0,p1,0.1f, 1, intersection);

// check, if the intersection of mouse direction with any obstacle was occurred;
if(obstacle !=NULL)
{
  // show the coordinates of the intersection in console
  log.message("The intersection with obstacle was here: %s\n", typeinfo(intersection.getPoint()));
}
/* ... */

```


### Arguments

- *Vec3* **p0** - Start point.
- *Vec3* **p1** - End point.
- *float* **radius** - Radius of the intersection cylinder.
- *int* **mask** - Obstacle *Intersection* mask. The obstacle is ignored if its mask does not match.
- *[GameIntersection](../../../api/library/engine/class.gameintersection_usc.md)* **intersection** - [GameIntersection](../../../api/library/engine/class.gameintersection_usc.md) class instance to put the result into.

### Return value

Intersected obstacle.
## Variable engine.game. getNoise ( Variable pos , Variable size , int frequency )


Returns a noise value calculated using a Perlin noise function. Variable can be of the *int* or *vec3* type.


```cpp
Image image;
int size = 64;
float time = engine.game.getTime();
vec3 position;
position.z = time;
forloop(int y = 0; size) {
	position.y = y * 0.05f;
	forloop(int x = 0; size) {
		position.x = x * 0.05f;
		// generate Perlin noise for the image pixels
		float n = engine.game.getNoise(position,vec3(32.0f,32.0f,32.0f),6);
		image.set2D(x,y,n,-n,n * n);
	}
}

```


### Arguments

- *Variable* **pos** - Position.
- *Variable* **size** - Size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

Noise value.
## float engine.game. getNoise1 ( float pos , float size , int frequency )

Returns a noise value calculated using a Perlin noise function.
### Arguments

- *float* **pos** - Float position.
- *float* **size** - Size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

Noise value.
## float engine.game. getNoise2 ( vec2 pos , vec2 size , int frequency )

Returns a 2D noise value calculated using a Perlin noise function.
### Arguments

- *vec2* **pos** - vec2 point position.
- *vec2* **size** - vec2 size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

2D noise value.
## float engine.game. getNoise3 ( vec3 pos , vec3 size , int frequency )

Returns a 3D noise value calculated using a Perlin noise function.
### Arguments

- *vec3* **pos** - vec3 point position.
- *vec3* **size** - vec3 size of the noise.
- *int* **frequency** - Noise frequency.

### Return value

3D noise value.
## Variable engine.game. getRandom ( Variable from , Variable to )


Returns a pseudo-random number of the given type (end-point not included). Variable can be of one of the following types: *int, float, vec3, vec4, dvec3, dvec4, ivec3, ivec4*.


```cpp
// create a WidgetLabel
label = new WidgetLabel(gui,"Text sample");
// specify widget settings
label.setFontOutline(1);
label.setFontSize(9);

// get pseudo-random values
int x = engine.game.getRandom(0,engine.app.getWidth() - 128);
int y = engine.game.getRandom(0,engine.app.getHeight() - 128);
// use the generated values to set widget position
label.setPosition(x,y);

```


### Arguments

- *Variable* **from** - The initial point of the range.
- *Variable* **to** - The end point of the range.

### Return value

Random number.
## double engine.game. getRandomDouble ( double from , double to )

Returns a pseudo-random *double* number within a given range (end-point not included).
### Arguments

- *double* **from** - The initial point of the range.
- *double* **to** - The end point of the range.

### Return value

Random *double* integer number.
## float engine.game. getRandomFloat ( float from , float to )

Returns a pseudo-random *float* number within a given range (end-point not included).
### Arguments

- *float* **from** - The initial point of the range.
- *float* **to** - The end point of the range.

### Return value

Random *float* number.
## int engine.game. getRandomInt ( int from , int to )

Returns a pseudo-random integer number within a given range (end-point not included).
### Arguments

- *int* **from** - The initial point of the range.
- *int* **to** - The end point of the range.

### Return value

Random integer number.
