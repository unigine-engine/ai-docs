# Unigine::WorldIntersectionTexCoord Class (CPP)

**Header:** #include <UnigineWorld.h>

**Inherits from:** WorldIntersectionNormal


This class stores the texture coordinates of the intersection point. You should use this class when you need additional information about the texture coordinates at the intersection point (it also stores the coordinates of the intersection, the index of the intersected triangle, the index of the intersected surface, and normal coordinates at the intersection point).


#### Usage Example


The following example shows how you can get texture coordinates at the intersection point (vec4) by using the *WorldIntersectionTexCoord* class. In this example the line is an invisible traced line from the point of the camera (*vec3 **p0***) to the point of the mouse pointer (*vec3 **p1***). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *[Player::getDirectionFromScreen()](../../../api/library/players/class.player_cpp.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the *WorldIntersectionTexCoord* class to get the intersection information.
- Check, if there is a intersection with an object. The [*World::getIntersection()*](../../../api/library/engine/class.world_cpp.md#getIntersection_vec3_vec3_int_Variable_Object) function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *WorldIntersectionTexCoord* class instance gets the texture coordinates of the intersection point. You can get the texture coordinates by using the [*getTexCoord()*](#getTexCoord_vec4) function.


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

// create an instance of the WorldIntersectionTexCoord class to get the result
WorldIntersectionTexCoordPtr intersection = WorldIntersectionTexCoord::create();

// create an instance for intersected object and check the intersection
ObjectPtr object = World::getIntersection(p0, p1, 1, intersection);

// if the intersection has occurred, change the parameter of the object's material
if (object)
{
	for (int i = 0; i < object->getNumSurfaces(); i++)
	{
		object->setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f), i);

		// show intersection details in console
		Log::message("Texture coordinates: (%f %f %f %f)\n",
			intersection->getTexCoord().x,
			intersection->getTexCoord().y,
			intersection->getTexCoord().z,
			intersection->getTexCoord().w);
	}
}
/* ... */


```


## WorldIntersectionTexCoord Class

### Members

## void setTexCoord ( const Math:: vec4 & coord )

Sets a new texture coordinates of the intersection point.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **coord** - The texture coordinates of the intersection point.

## Math:: vec4 getTexCoord () const

Returns the current texture coordinates of the intersection point.
### Return value

Current texture coordinates of the intersection point.
---

## static WorldIntersectionTexCoordPtr create ( )

The WorldIntersectionTexCoord constructor.
