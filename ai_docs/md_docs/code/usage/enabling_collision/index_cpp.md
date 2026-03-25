# Enabling Selective Surface-Based Collision (CPP)


![Surface-based collision example](collision_ex1.gif)

*Surface-based collision using collision masks*


This example shows how to enable collision detection for a surface using bitmasks. Two boxes (orange and yellow), each with a body and a box shape assigned, and a blue plane are created. We want the yellow box to collide with the surface of the blue plane and the orange box to pass through. So we set the following collision masks for the shapes of the boxes and for the surface of the plane.


| Element | Mask |
|---|---|
| Yellow box: shape | **0010** |
| Orange box: shape | **0001** |
| Plane: surface | **0010** |


> **Notice:** Surface-to-surface collisions cannot be enabled using collision masks.


In the **AppWorldLogic.h** file, define smart pointers for the objects of our scene.


```cpp
// AppWorldLogic.h

#include <UnigineObjects.h>
/* .. */

class AppWorldLogic : public Unigine::WorldLogic {

public:
	/* .. */

private:
	Unigine::ObjectMeshStaticPtr box1;
	Unigine::ObjectMeshStaticPtr box2;
	Unigine::ObjectMeshStaticPtr plane;
	Unigine::PlayerSpectatorPtr player;
};

```


Insert the following code into the **AppWorldLogic.cpp** file.

> **Notice:** Unchanged methods of the *AppWorldLogic* class are not listed here, so leave them as they are.


```cpp
#include "AppWorldLogic.h"
#include "UnigineGame.h"
#include "UnigineObjects.h"

/* .. */

using namespace Unigine;
using namespace Math;

/// function, creating a named box of a specified size and color at pos
ObjectMeshStaticPtr create_box(const char *name, const vec4& color, const vec3& size, const vec3& pos)
{
	// creating an auxiliary mesh with a box surface
	MeshPtr meshbox = Mesh::create();
	meshbox->addBoxSurface("box_surface", size);

	// creating a static mesh object using an auxiliary mesh and setting parameters
	ObjectMeshStaticPtr OM = ObjectMeshStatic::create(meshbox);

	OM->setWorldTransform(Mat4(translate(pos)));
	OM->setMaterialParameterFloat4("albedo_color", color, 0);
	OM->setCollision(1, 0);
	OM->setName(name);

	// assigning a rigid body with our object
	BodyRigid::create(OM);

	// creating a box shape and assigning it to the rigid body of our object
	OM->getBody()->addShape(ShapeBox::create(size), translate(0.0f, 0.0f, 0.0f));

	// clearing the auxiliary mesh
	meshbox->clear();

	return OM;
}

/// function, creating a named plane having a specified width and height at pos
ObjectMeshStaticPtr create_plane(const char *name, float width, float height, const vec3& pos)
{
	// creating an auxiliary mesh with a plane surface
	MeshPtr meshplane = Mesh::create();

	meshplane->addPlaneSurface("plane_surface", width, height, 1.0f);

	// creating a static mesh object using an auxiliary mesh and setting parameters
	ObjectMeshStaticPtr OM = ObjectMeshStatic::create(meshplane);

	OM->setWorldTransform(Mat4(translate(pos)));
	OM->setMaterialParameterFloat4("albedo_color", vec4(0.0f, 0.0f, 1.0f, 1.0f), 0);
	OM->setCollision(1, 0);
	OM->setName(name);

	// clearing the auxiliary mesh
	meshplane->clear();

	return OM;
}

int AppWorldLogic::init()
{
	// setting up a player
	player = PlayerSpectator::create();
	player->setPosition(Vec3(0.0f, -6.0f, 12.5f));
	player->setDirection(vec3(0.0f, 1.0f, -0.4f), vec3(0.0f, 0.0f, -1.0f));

	Game::setPlayer(player);

	// creating a scene: two boxes and a plane
	box1 = create_box("box1", vec4(1.0f, 1.0f, 0.0f, 1.0f), vec3(0.5f), vec3(1.5f, 0.0f, 12.0f));
	box2 = create_box("box2", vec4(1.0f, 0.5f, 0.1f, 1.0f), vec3(0.5f), vec3(-1.5f, 0.0f, 12.0f));
	plane = create_plane("plane", 10.0f, 6.0f, vec3(0.0f, 1.0f, 10.5f));

	// setting shape collision mask for the first box  [00000000000000000000000000000010]
	box1->getBody()->getShape(0)->setCollisionMask(2);

	// setting shape collision mask for the second box  [00000000000000000000000000000001]
	box2->getBody()->getShape(0)->setCollisionMask(1);

	// setting collision mask for the plane surface  [00000000000000000000000000000010]
	plane->setCollisionMask(2, 0);

	return 1;
}

/* .. */

```
