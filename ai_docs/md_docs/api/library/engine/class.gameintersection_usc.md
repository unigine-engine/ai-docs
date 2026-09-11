# Unigine::GameIntersection Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Stores the result of the *[*engine.game.getIntersection()*](../../../api/library/engine/class.game_usc.md#getIntersection_Vec3_Vec3_float_int_GameIntersection_Obstacle)* function - the point where the intersection with an [obstacle](../../../api/library/pathfinding/class.obstacle_usc.md) has been occurred.


![](cylinder01.png)


### Usage Example


The following example shows how you can get the intersection point (vec3) of the cylinder between two points with an obstacle. In this example the cylinder is an invisible traced cylinder from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1) with the specific radius. The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *Unigine::getPlayerMouseDirection()* function from `core/scripts/utils.h`.
- Create an instance of the GameIntersection class to get the intersection point coordinates.
- Check, if there is a intersection with an obstacle. The *engine.game.getIntersection()* function returns an intersected obstacle when the obstacle appears in the area of the cylinder.
- After that *GameIntersection* instance gets the point of the nearest intersection point and you can get it by using the *getPoint()* function.


```cpp
#include <core/scripts/utils.h>
/* ... */
// define two vec3 coordinates
vec3 p0,p1;
// get the mouse direction from camera (p0) to cursor pointer (p1)
Unigine::getPlayerMouseDirection(p0,p1);

// create an instance of the GameIntersection class
GameIntersection intersection = new GameIntersection();

// try to get the intersection with an obstacle.
// cylinder has radius 0.1f, intersection mask equals to 1
Obstacle obstacle = engine.game.getIntersection(p0,p1,0.1f, 1, intersection);

// check, if the intersection of mouse direction with any obstacle was occurred;
if(obstacle !=NULL)
{
  // show the coordinates of the intersection in console
  log.message("The intersection with obstacle was here: %s\n", typeinfo(intersection.getPoint()));
}
/* ... */

```


## GameIntersection Class

### Members

## void setPoint ( Vec3 point )

Sets a new coordinates of the intersection point.
### Arguments

- *Vec3* **point** - The coordinates of the intersection point.

## Vec3 getPoint () const

Returns the current coordinates of the intersection point.
### Return value

Current coordinates of the intersection point.
---

## static GameIntersection ( )

The GameIntersection constructor.
