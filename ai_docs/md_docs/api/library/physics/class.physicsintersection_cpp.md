# Unigine::PhysicsIntersection Class (CPP)

**Header:** #include <UniginePhysics.h>


This class stores the result of the physics intersection (coordinates of the intersection, the shape of the object, the index of the surface). If you need information on the normal at the intersection point, use the *[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cpp.md)* class.


#### Usage Example


The following example shows how you can get the intersection information by using the *PhysicsIntersection* class. In this example, we specify a line from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)*. The execution sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *[Player::getDirectionFromScreen()](../../../api/library/players/class.player_cpp.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
2. Create an instance of the *PhysicsIntersection* class to get the intersection information.
3. Check if there is an intersection with an object with a shape or a collision object. The *[getIntersection()](../../../api/library/physics/class.physics_cpp.md#getIntersection_Vec3_Vec3_int_Variable)* function returns an intersected object when the object intersects with the traced line.
4. When the object intersects with the traced line, all surfaces of the intersected object change their material parameters. If the object has a shape, its information will be shown in console. The *PhysicsIntersection* class instance gets the coordinates of the intersection point and the *Shape* class object. You can get all these fields by using *[getShape()](../../../api/library/physics/class.physicsintersection_cpp.md#getShape_Shape), [getPoint()](../../../api/library/physics/class.physicsintersection_cpp.md#getPoint_Vec3)* functions.


```cpp
#include "AppWorldLogic.h"
#include <UnigineObjects.h>
#include <UnigineEditor.h>
#include <UnigineGame.h>
#include <UniginePhysics.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{
	// create a Mesh instance with a box surface
	MeshPtr mesh = Mesh::create();
	mesh->addBoxSurface("box", vec3(0.2f));

	// create a new dynamic mesh from the Mesh instance
	ObjectMeshDynamicPtr dynamic_mesh = ObjectMeshDynamic::create(mesh);

	dynamic_mesh->setWorldTransform(translate(Vec3(0.0f, 0.0f, 2.0f)));

	// assign a body and a shape to the dynamic mesh
	BodyRigidPtr body = BodyRigid::create(dynamic_mesh);
	ShapeBoxPtr shape = ShapeBox::create(body, vec3(0.2f));

	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// start of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppWorldLogic::update()
{
	// initialize points of the mouse direction
	Vec3 p0, p1;

	// get the current player (camera)
	PlayerPtr player = Game::getPlayer();
	if (player.get() == NULL)
		return 0;
	// get width and height of the main application window
	Math::ivec2 winsize = WindowManager::getMainWindow()->getClientSize();
	int width = winsize.x;
	int height = winsize.y;
	// get the current X and Y coordinates of the mouse pointer
	int mouse_x = Gui::getCurrent()->getMouseX();
	int mouse_y = Gui::getCurrent()->getMouseY();
	// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
	player->getDirectionFromScreen(p0, p1, mouse_x, mouse_y, 0, 0, width, height);

	// create the instance of the PhysicsIntersection object to save the information about the intersection
	PhysicsIntersectionPtr intersection = PhysicsIntersection::create();
	// get an intersection
	ObjectPtr object = Physics::getIntersection(p0, p1, 1, intersection);

	// if the intersection has occurred, change the parameter of the object's material
	if (object)
	{
		for (int i = 0; i < object->getNumSurfaces(); i++)
		{
			object->setMaterialParameterFloat4("albedo_color", vec4(1.0f, 1.0f, 0.0f, 1.0f), i);
		}

		// if the intersected object has a shape, show the information about the intersection
		ShapePtr shape = intersection->getShape();
		if (shape)
		{
			Log::message("physics intersection info: point: (%f %f %f) shape: %s\n", intersection->getPoint().x, intersection->getPoint().y, intersection->getPoint().z, shape->getTypeName());
		}
	}

	return 1;
}


```


## PhysicsIntersection Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **PHYSICS_INTERSECTION** = 0 | PhysicsIntersection object, which stores basic information on the intersection point (coordinates of the intersection, the shape of the object, the index of the surface). |
| **PHYSICS_INTERSECTION_NORMAL** = 1 | [PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_cpp.md) object, which stores the same information as the PhysicsIntersection object plus additional information on the normal at the intersection point. |
| **NUM_PHYSICS_INTERSECTIONS** = 2 | Number of physics intersection types. |

### Members

## void setSurface ( int surface )

Sets a new intersected surface number.
### Arguments

- *int* **surface** - The intersected surface number

## int getSurface () const

Returns the current intersected surface number.
### Return value

Current intersected surface number
## void setPoint ( const Math:: Vec3 & point )

Sets a new coordinates of the intersection point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **point** - The coordinates of the intersection point

## Math:: Vec3 getPoint () const

Returns the current coordinates of the intersection point.
### Return value

Current coordinates of the intersection point
## void setShape ( const Ptr < Shape >& shape )

Sets a new intersected shape.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Shape](../../../api/library/physics/class.shape_cpp.md)>&* **shape** - The intersected shape

## Ptr < Shape > getShape () const

Returns the current intersected shape.
### Return value

Current intersected shape
## const char * getTypeName () const

Returns the current name of the intersection object type.
### Return value

Current name of the intersection object type
## PhysicsIntersection::TYPE getType () const

Returns the current intersection object type, one of the [PHYSICS_INTERSECTION*](#PHYSICS_INTERSECTION) values.
### Return value

Current intersection object type
---

## static PhysicsIntersectionPtr create ( )

The PhysicsIntersection constructor.
