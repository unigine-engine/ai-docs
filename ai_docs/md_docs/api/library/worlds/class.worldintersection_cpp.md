# Unigine::WorldIntersection Class (CPP)

**Header:** #include <UnigineWorld.h>


This class stores the result of the world intersection (the coordinates of the intersection, the index of the intersected triangle and the index of the intersected surface).


#### Usage Example


The following example shows how you can get the intersection information by using the WorldIntersection class. In this example, the line is an invisible traced line from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1). The executing sequence is the following:

- Define and initialize two points (p0 and p1) by using the *[Player::getDirectionFromScreen()](../../../api/library/players/class.player_cpp.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the WorldIntersection class to get the intersection information.
- Check, if there is a intersection with an object. The [*World::getIntersection()*](../../../api/library/engine/class.world_cpp.md#getIntersection_vec3_vec3_int_Variable_Object) function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The WorldIntersection class instance gets the coordinates of the intersection point and the index of the intersected triangle. You can get all these fields by using [*getIndex()*](#getIndex_int) and [*getPoint()*](#getPoint_Vec3) functions


```cpp
/* ... */
// initialize points of the mouse direction
Vec3 p0, p1;

// get the current player (camera)
PlayerPtr player = Game::getPlayer();
if (player.get() == NULL)
	return 0;

// get the size (width and height) of the current application window
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

// create an instance of the WorldIntersection class to get the result
WorldIntersectionPtr intersection = WorldIntersection::create();

// create an instance for intersected object and check the intersection
ObjectPtr object = World::getIntersection(p0, p1, 1, intersection);

// if the intersection has occurred, change the parameter of the object's material
if (object)
{
	for (int i = 0; i < object->getNumSurfaces(); i++)
	{
		object->setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f), i);

		// show intersection details in console
		Log::message("point: (%f %f %f) index: %i \n", intersection->getPoint().x, intersection->getPoint().y, intersection->getPoint().z, intersection->getIndex());
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

### Members

---

## static WorldIntersectionPtr create ( )

The WorldIntersection constructor.
## void setIndex ( int index )

Sets the new intersection triangle number.
### Arguments

- *int* **index** - Intersection triangle number.

## int getIndex ( ) const

Returns the number of the intersected triangle.
### Return value

Intersected triangle number.
## void setInstance ( int instance )

Sets the new intersected instance number.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)*


### Arguments

- *int* **instance** - Intersected instance number.

## int getInstance ( ) const

Returns the number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)*


### Return value

Intersected instance number.
## void setPoint ( const Math:: Vec3 & point )

Sets new coordinates of the intersection point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the intersection point.

## Math:: Vec3 getPoint ( ) const

Returns coordinates of the intersection point.
### Return value

Coordinates of the intersection point.
## void setSurface ( int surface )

Sets the new intersection surface number.
### Arguments

- *int* **surface** - Intersection surface number.

## int getSurface ( ) const

Returns the intersected surface number.
### Return value

Intersected surface number.
## WorldIntersection::TYPE getType ( ) const

Returns the world intersection type identifier.
### Return value

World [intersection type identifier](#WORLD_INTERSECTION).
## const char * getTypeName ( ) const

Returns the world intersection type name.
### Return value

World intersection type name.
