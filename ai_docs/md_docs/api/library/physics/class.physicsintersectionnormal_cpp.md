# Unigine::PhysicsIntersectionNormal Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** PhysicsIntersection


This class stores all information on the point of physics intersection (coordinates of the intersection, the shape of the object, the index of the surface) plus the normal coordinates at this point.


#### Usage Example


The following example shows how you can get the normal of the intersection point by using the *PhysicsIntersectionNormal* class. In this example the line is an invisible traced line from the point of the camera (vec3 p0) to the point of the mouse pointer (vec3 p1). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *[Player::getDirectionFromScreen()](../../../api/library/players/class.player_cpp.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
- Create an instance of the *PhysicsIntersectionNormal* class to get the normal of the intersection point.
- Check if there is a intersection with an object.
- When the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *PhysicsIntersectionNormal* class instance gets the normal of the intersection point. You can get it by using *[getNormal()](#getNormal_vec3)* function.


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

	// create the instance of the PhysicsIntersectionNormal object to save the information about the intersection
	PhysicsIntersectionNormalPtr intersection = PhysicsIntersectionNormal::create();
	// get an intersection
	ObjectPtr object = Physics::getIntersection(p0, p1, 1, intersection);

	// if the intersection has occurred, change the parameter of the object's material
	if (object)
	{
		for (int i = 0; i < object->getNumSurfaces(); i++)
		{
			object->setMaterialParameterFloat4("albedo_color", vec4(1.0f, 1.0f, 0.0f, 1.0f), i);
		}

		// if the intersected object has a shape, show the information about the intersection normal
		ShapePtr shape = intersection->getShape();
		if (shape)
		{
			Log::message("Normal coordinates: (%f %f %f)\n",

			intersection->getNormal().x,
			intersection->getNormal().y,
			intersection->getNormal().z);
		}
	}

	return 1;
}


```


## PhysicsIntersectionNormal Class

### Members

## void setNormal ( const Math:: vec3 & normal )

Sets a new normal of the intersection point.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **normal** - The normal of the intersection point

## Math:: vec3 getNormal () const

Returns the current normal of the intersection point.
### Return value

Current normal of the intersection point
---

## static PhysicsIntersectionNormalPtr create ( )

The PhysicsIntersectionNormal constructor.
