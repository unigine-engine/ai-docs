# Intersections (CPP)


Unigine has different methods to detect intersections. Intersection is a shared point of the defined area (or line) and an object. This article describes different types of intersections and their usage.


There are three main types of intersections:


- **World intersection** � an intersection with [objects](../../../api/library/objects/class.object_cpp.md) and [nodes](../../../api/library/nodes/class.node_cpp.md).
- **Physics intersection** � an intersection with [shapes](../../../api/library/physics/class.shape_cpp.md) and [collision objects](../../../principles/physics/collision/index.md).
- **Game intersection** � an intersection with pathfinding nodes such as [obstacles](../../../api/library/pathfinding/class.obstacle_cpp.md).


The *[Shape](../../../api/library/physics/class.shape_cpp.md)* and *[Object](../../../api/library/objects/class.object_cpp.md)* classes have their own *getIntersection()* functions. These functions are used to detect intersections with a specific shape or a specific surface of the object.


### See Also


- **[C# Component Samples](../../../sdk/api_samples/cs/scene_management.md)** demonstrating the use of World Intersection
- **[C++ Samples](../../../sdk/api_samples/cpp/scene_management.md)** demonstrating different cases of intersection detection


## World Intersection


By using different overloaded *[World](../../../api/library/engine/class.world_cpp.md)* class *getIntersection()* functions you can find objects and nodes that intersect bounds of the specified bounding volume or identify the first intersection of the object with the invisible tracing line.


The *World* class functions for intersection search can be divided into 3 groups:


- [Functions to find nodes](#worldintersections_nodes) within a bounding volume
- [Functions to find objects](#worldintersections_objects) within a bounding volume or intersected with a traced line
- [Functions to find first intersected object](#worldintersections_object) with a traced line


> **Notice:** The following objects have individual parameters that control the accuracy of intersection detection:
>
>
> - *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md#setIntersectionPrecision_float_void)*
> - *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections)*


### Intersection with Nodes


To find the intersection of nodes with bounds of the specified volume, you should use functions that have a bounding volume and a vector of nodes in arguments:


- *[int getIntersection(const Math::WorldBoundBox & bb, Vector< Ptr<Node> > & nodes)](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundBox_VECNode_int)*
- *[int getIntersection(const Math::WorldBoundSphere & bs, Vector< Ptr<Node> > & nodes)](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundSphere_VECNode_int)*
- *[int getIntersection(const Math::WorldBoundBox & bb, int type, Vector< Ptr<Node> > & nodes)](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundBox_int_VECNode_int)*
- *[int getIntersection(const Math::WorldBoundSphere & bs, int type, Vector< Ptr<Node> > & nodes)](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundSphere_int_VECNode_int)*
- *[int getIntersection(const Math::WorldBoundFrustum & bf, int type, Vector< Ptr<Node> > & nodes)](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundFrustum_int_VECNode_int)*


![](world_nodes.png)

*Schematic visual representation of intersection with nodes in bounding volume*


These functions return the value indicating the result of the intersection search: **1** if the intersection was found; otherwise, **0**. Intersected nodes can be found in the vector that passed as an argument to the function.


To clarify the nodes search, specify the type of node to search.


#### Usage Example


In the example below, the engine checks intersections with a bounding box and shows the names of intersected objects in the console.


```cpp
#include "AppWorldLogic.h"
#include <UnigineObjects.h>
#include <UnigineEditor.h>

#include <UnigineVisualizer.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::update()
{

	// initialize a bounding box and vector for intersected nodes
	WorldBoundBox boundBox(Vec3(0.0f), Vec3(1.0f));
	Visualizer::renderBoundBox(boundBox, Mat4_identity, vec4_blue);

	Vector<NodePtr> nodes;

	// check the intersection with nodes
	int result = World::getIntersection(boundBox, nodes);
	if (result)
	{
		for (int i = 0; i < nodes.size(); i++)
		{
			Log::message("Intersected node: %s \n", nodes.get(i)->getName());
		}
		Log::message("The number of intersected nodes is: %i \n", nodes.size());
	}

	return 1;
}


```


As the sun has limitless bounds, if present in the scene, it always intersects with the initialized bounding box.


### Intersection with Objects


The following functions can be used to perform the intersection search with objects:


- *[int getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, Vector< Ptr<Object> > & objects, bool check_surface_flags)](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_VECObject_int_int)*
- *[int getIntersection(const Math::WorldBoundBox & bb, Vector< Ptr<Object> > & objects)](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundBox_VECObject_int)*
- *[int getIntersection(const Math::WorldBoundSphere & bs, Vector< Ptr<Object> > & objects)](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundSphere_VECObject_int)*
- *[int getIntersection(const Math::WorldBoundFrustum & bf, Vector< Ptr<Object> > & objects)](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundFrustum_VECObject_int)*
- *[bool getVisibleIntersection(const Math::Vec3& camera, const Math::WorldBoundFrustum& bf, Vector< Ptr<Object> > & objects, float max_distance)](../../../api/library/engine/class.world_cpp.md#getVisibleIntersection_Vec3_WorldBoundFrustum_VECObject_float_int)*
- *[bool getVisibleIntersection(const Math::Vec3& camera, const Math::WorldBoundFrustum& bf, Node::TYPE type, Vector< Ptr<Node> > & nodes, float max_distance)](../../../api/library/engine/class.world_cpp.md#getVisibleIntersection_Vec3_WorldBoundFrustum_int_VECNode_float_int)*


![](world_objects.png)

*Schematic visual representation of intersection with objects in bounding volume*


These functions return the value indicating the result of the intersection search: 1 if the intersection was found; otherwise, 0. You can pass the start (**vec3 p0**) and the end (**vec3 p1**) point of the intersecting line or pass the (*BoundBox, BoundFrustum, BoundSphere*) to get the intersection of objects with a line or with a bounding volume, respectively. Intersected nodes can be found in the vector that passed as an argument to the function.


For *WorldBoundFrustum*, there are [two modes of getting intersections](#frustrum_search):


- Intersections with the objects that are **visible** inside the frustum � *[getVisibleIntersection()](../../../api/library/engine/class.world_cpp.md#getVisibleIntersection_Vec3_WorldBoundFrustum_VECObject_float_int)*
- Intersections with all objects inside the frustum, both **visible** and **invisible** � *[getIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundFrustum_VECObject_int)*


#### Finding Objects Intersected by a Bounding Box


In the example below, the engine checks intersections with a bounding box and shows the names of intersected objects in the console.


In the *update()* method, the engine checks the intersection and shows the message about intersection.


```cpp
#include "AppWorldLogic.h"
#include <UnigineObjects.h>
#include <UnigineEditor.h>

#include <UnigineVisualizer.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::update()
{

	// initialize a bounding box and vector for intersected objects
	WorldBoundBox boundBox(Vec3(0.0f), Vec3(1.0f));
	Visualizer::renderBoundBox(boundBox, Mat4_identity, vec4_blue);

	Vector<ObjectPtr> objects;

	int result = World::getIntersection(boundBox, objects);
	if (result)
	{
		for (int i = 0; i < objects.size(); i++)
		{
			Log::message("Intersected object: %s \n", objects.get(i)->getName());
		}
		Log::message("The number of intersected objects is: %i \n", objects.size());
	}

	return 1;
}


```


#### Finding Objects Intersected by a Bounding Frustum


For *[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cpp.md)*, there are two modes of getting intersections:


- Intersections with the objects that are **visible** inside the frustum (within the rendering [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) and the object's [LOD](../../../principles/world_management/index.md#lods) is visible by the camera) � *[getVisibleIntersection()](../../../api/library/engine/class.world_cpp.md#getVisibleIntersection_Vec3_WorldBoundFrustum_VECObject_float_int)*
- Intersections with all objects inside the frustum, both **visible** and **invisible** (either occluded by something or out of the visibility distance) � *[getIntersection()](../../../api/library/engine/class.world_cpp.md#getIntersection_WorldBoundFrustum_VECObject_int)*


In the example below, the engine checks intersections of *WorldBoundFrustum* with all objects, both visible and invisible. The frustum itself is highlighted blue, and the objects that are inside the frustum are highlighted red for 20 seconds.


```cpp
#include "AppWorldLogic.h"
#include <UnigineObjects.h>
#include <UnigineEditor.h>

#include <UnigineVisualizer.h>

#include <UnigineInput.h>
#include <UnigineGame.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{
	Visualizer::setEnabled(true);


	return 1;
}

int AppWorldLogic::update()
{

	if (Input::isKeyDown(Input::KEY_SPACE))
	{
		// get a reference to the camera
		PlayerPtr player = Game::getPlayer();
		CameraPtr camera = player->getCamera();

		Math::ivec2 winsize = WindowManager::getMainWindow()->getClientSize();
		mat4 projection = camera->getAspectCorrectedProjection(float(winsize.y) / float(winsize.x));

		// bound frustrum for the intersection and a list to store intersected objects
		WorldBoundFrustum bf(projection, camera->getModelview());
		Visualizer::renderFrustum(projection, camera->getIModelview(), vec4_blue, 20.0f);

		Vector<ObjectPtr> objects;

		// perform the intersection search with the bound frustrum
		World::getIntersection(bf, objects);

		// draw the bound spheres of all objects' surfaces found by the search
		for (int i = 0; i < objects.size(); i++)
		{
			BoundSphere bs = objects[i]->getBoundSphere();
			Visualizer::renderBoundSphere(bs, objects[i]->getWorldTransform(), vec4_red, 20.0f);
		}
	}

	return 1;
}


```


To search only for intersections with the objects that are within the rendering [visibility distance](../../../editor2/settings/render_settings/visibility_distances/index.md) and the [LODs](../../../principles/world_management/index.md#lods) of which are visible, use the following method instead of *getIntersection()*:


```cpp
World::getVisibleIntersection(player->getWorldPosition(), bf, objects, 100.0f);


```


> **Notice:** The current rendering *[Distance Scale](../../../editor2/settings/render_settings/visibility_distances/index.md)* is also taken into account in the distance calculation.


### First Intersected Object


The following functions are used to find the nearest intersected object with the traced line. You should specify the start point and the end point of the line, and the function detects if there are any object on the way of this line.


- *[Ptr<Object> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, int mask, Math::Vec3 * ret_point, Math::vec3 * ret_normal, Math::vec4 * ret_texcoord, int * ret_index, int * ret_surface)](../../../api/library/engine/class.world_cpp.md)*
- *[Ptr<Object> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, int mask, const Vector< Ptr<Node> > & exclude, Math::Vec3 * ret_point, Math::vec3 * ret_normal, Math::vec4 * ret_texcoord, int * ret_index, int * ret_surface)](../../../api/library/engine/class.world_cpp.md)*
- *[Ptr<Object> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, int mask, const Ptr<WorldIntersection> & v)](../../../api/library/engine/class.world_cpp.md)*
- *[Ptr<Object> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, int mask, const Ptr<WorldIntersectionNormal> & v)](../../../api/library/engine/class.world_cpp.md)*
- *[Ptr<Object> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, int mask, const Ptr<WorldIntersectionTexCoord> & v)](../../../api/library/engine/class.world_cpp.md)*
- *[Ptr<Object> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, int mask, const Vector< Ptr<Node> > & exclude, const Ptr<WorldIntersection> & v)](../../../api/library/engine/class.world_cpp.md)*
- *[Ptr<Object> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, int mask, const Vector< Ptr<Node> > & exclude, const Ptr<WorldIntersectionNormal> & v)](../../../api/library/engine/class.world_cpp.md)*
- *[Ptr<Object> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, int mask, const Vector< Ptr<Node> > & exclude, const Ptr<WorldIntersectionTexCoord> & v)](../../../api/library/engine/class.world_cpp.md)*


![](worldintersection.png)

*Schematic visual representation of intersection with objects and traced line*


These functions return an intersection information and a pointer to the nearest object to the start point (**p0**). Information about the intersection can be presented in standard vectors or in the following format that you pass to functions as arguments:


- *WorldIntersection **intersection*** � the *[WorldIntersection](../../../api/library/worlds/class.worldintersection_cpp.md)* class instance. By using this class you can get the intersection point (coordinates), the index of the intersected triangle of the object and the index of the intersected surface.
- *WorldIntersectionNormal **normal*** � the *[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cpp.md)* class instance. By using this class you can get only the normal of the intersection point.
- *WorldIntersectionTexCoord **texcoord*** � the *[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cpp.md)* class instance. By using this class you can get only the texture coordinates of the intersection point.


These functions detect intersection with surfaces (polygons) of meshes. But there are some conditions to detect the intersection with the surface:


1. The surface is enabled.
2. The surface has a material assigned.
3. Per-surface **Intersection** flag is enabled. > **Notice:** You can set this flag to the object's surface by using the *[Object.setIntersection()](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void)* function.


To clarify the object search, perform the following:


- Use an *Intersection* mask. An intersection is found only if an object is matching the *Intersection* mask.
- Specify the list of objects (nodes) to exclude and pass to the function as an argument.


#### Usage Example


In the example below, the engine checks intersections with a raytraced line and shows the message in the console.


```cpp
#include "AppWorldLogic.h"
#include <UnigineObjects.h>
#include <UnigineEditor.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::update()
{

	WorldIntersectionPtr wi = WorldIntersection::create();
	ObjectPtr o;

	if (wi)
		o = World::getIntersection(Vec3(0.0f), Vec3(1.0f), 1, wi);

	if (o)
	{
		Log::message("Intersected object is: %s \n", o->getName());
	}
	return 1;

}


```


## Physics Intersection


Physics intersection function detects intersections with a physical shape or a fracture body. If the object has no body, this function detects intersection with surfaces (polygons) of the object having the *[Physics Intersection](../../../api/library/objects/class.object_cpp.md#setPhysicsIntersection_int_int_void)* flag enabled. When you need to find the intersection with the shape of the object (not with polygons), the intersection function of *[Physics](../../../api/library/physics/class.physics_cpp.md)* class is the best way to get it.


![](physics_shape.png)

*The picture above shows how thegetIntersection()function detects the shape that intersects with the line*


There are 4 functions to find physics intersections:


- *[Ptr<Object> getIntersection(const Math::Vec3 &p0, const Math::Vec3 &p1, int mask, const Vector<Ptr<Node>> &exclude, const Ptr<PhysicsIntersection> &intersection)](../../../api/library/physics/class.physics_cpp.md#getIntersection_Vec3_Vec3_int_VECNode_PhysicsIntersection_Object)*
- *[Ptr<Object> getIntersection(const Math::Vec3 &p0, const Math::Vec3 &p1, int mask, const Ptr<PhysicsIntersection> &intersection)](../../../api/library/physics/class.physics_cpp.md#getIntersection_Vec3_Vec3_int_PhysicsIntersection_Object)*
- *[Ptr<Object> getIntersection(const Math::Vec3 &p0, const Math::Vec3 &p1, int mask, const Ptr<PhysicsIntersectionNormal> &intersection)](../../../api/library/physics/class.physics_cpp.md#getIntersection_Vec3_Vec3_int_PhysicsIntersectionNormal_Object)*
- *[Ptr<Object> getIntersection(const Math::Vec3 &p0, const Math::Vec3 &p1, int mask, const Vector<Ptr<Node>> &exclude, const Ptr<PhysicsIntersectionNormal> &intersection)](../../../api/library/physics/class.physics_cpp.md#getIntersection_Vec3_Vec3_int_VECNode_PhysicsIntersectionNormal_Object)*


These functions perform tracing from the start *p0* point to the end *p1* point to find a collision object (or a shape) located on that line. Functions use world space coordinates.


Thus, to exclude some obstacles you should use these methods:


- Use a *Physics Intersection* mask. A physics intersection is detected only if the *Physics Intersection* mask of the surface/shape/body matches the *Intersection* mask passed as a function argument, otherwise it is ignored.
- Specify the list of objects to exclude and pass to the function as an argument.


### Usage Example


The following example shows how you can get the intersection information by using the *[PhysicsIntersection](../../../api/library/physics/class.physicsintersection_cpp.md)* class. In this example we specify a line from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)*. The executing sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *[Player::getDirectionFromScreen()](../../../api/library/players/class.player_cpp.md#getDirectionFromScreen_Vec3_Vec3_int_int_int_int_int_int_void)* function.
2. Create an instance of the *PhysicsIntersection* class to get the intersection information.
3. Check if there is an intersection with an object with a shape or a collision object. The *[getIntersection()](../../../api/library/physics/class.physics_cpp.md#getIntersection_Vec3_Vec3_int_Variable)* function returns an intersected object when the object intersects with the traced line.
4. When the object intersects with the traced line, all surfaces of the intersected object change their material parameters. If the object has a shape, its information will be shown in console. The *PhysicsIntersection* class instance gets the coordinates of the intersection point and the *[Shape](../../../api/library/physics/class.shape_cpp.md)* class object. You can get all these fields by using *[getShape()](../../../api/library/physics/class.physicsintersection_cpp.md#getShape_Shape), [getPoint()](../../../api/library/physics/class.physicsintersection_cpp.md#getPoint_Vec3)* functions.


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


## Game Intersection


The *GetIntersection()* functions of the *Game* class are used to check the intersection with obstacles (pathfinding nodes):


- *[Ptr<Obstacle> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, float radius, int mask, const Vector< Ptr<Node> > & exclude, Math::Vec3 * intersection)](../../../api/library/engine/class.game_cpp.md#getIntersection_Vec3_Vec3_float_int_VECNode_Vec3_Obstacle)*
- *[Ptr<Obstacle> getIntersection(const Math::Vec3 & p0, const Math::Vec3 & p1, float radius, int mask, const Ptr<GameIntersection> & intersection)](../../../api/library/engine/class.game_cpp.md#getIntersection_Vec3_Vec3_float_int_GameIntersection_Obstacle)*


The engine creates an invisible cylinder with specified radius between two points and checks if an obstacle is inside it.


![](cylinder01.png)

*Schematic visual representation of intersection with objects and cylinder volume*


These functions return an intersection information and a pointer to the nearest obstacle to the start point (**p0**). Information about the intersection will be presented in the *[GameIntersection](../../../api/library/engine/class.gameintersection_cpp.md)* class instance which you pass to the function as an argument or in the vector.


Use the mask and exclude arguments of the overloaded function to specify the obstacle search.


To clarify the obstacle search, perform the following:


- Use an obstacle *Intersection* mask. An intersection is found only if an object is matching the *Intersection* mask, otherwise it is ignored.
- Specify the list of obstacles to exclude and pass to the function as an argument.


### Usage Example


The following example shows how you can get the intersection point *(vec3)* of the cylinder between two points with an obstacle. We'll do the following:


1. Create an instance of the *ObstacleBox* class on the application initialization.
2. Define two points (p1 and p2) that specify the beginning and the end of the cylinder.
3. Create an instance of the *GameIntersection* class to get the intersection point coordinates.
4. Check if there is an intersection with an obstacle. The *Game::getIntersection()* function returns an intersected obstacle when the obstacle appears in the area of the cylinder.
5. When the *GameIntersection* instance intersects with an obstacle, you can get its name using the *getName()* function or any other details using the corresponding functions.


```cpp
#include "AppWorldLogic.h"
#include <UnigineObjects.h>
#include <UnigineEditor.h>

#include <UniginePathFinding.h>
#include <UnigineGame.h>

using namespace Unigine;
using namespace Math;

int AppWorldLogic::init()
{
	Visualizer::setEnabled(true);

		// create an obstacle
	obstacle_box = ObstacleBox::create(vec3(1.0f));
	obstacle_box->setName("main_obstacle");

	return 1;
}

int AppWorldLogic::update()
{

	// make the obstacle box move inside and outside the game intersection area
	Vec3 new_pos = Vec3(0, 0, 2 + Math::sin(Game::getTime()));
	obstacle_box->setWorldPosition(new_pos);
	Visualizer::renderPoint3D(new_pos, 0.15f, vec4(1, 0, 1, 1));

	// calculate the cylinder height (equals to the distance between the start and end points)
	Visualizer::renderPoint3D(p1, 0.15f, vec4(0, 0, 1, 1));
	Visualizer::renderPoint3D(p2, 0.15f, vec4(0, 1, 1, 1));

	// create an instance of the GameIntersection class
	GameIntersectionPtr intersection = GameIntersection::create();
	ObstaclePtr obstacle = Game::getIntersection(p1, p2, radius, 1, intersection);

	//visualize the cylinder that represents the game intersection area
	Visualizer::renderCylinder(radius, (p2 - p1).length(), setTo(p1 + (p2 - p1) / 2, p2, vec3_up, AXIS_Z), vec4(1, 1, 1, 1));

	// check if the intersection of the cylinder with the obstacle has occurred
	if (obstacle)
	{
		obstacle->renderVisualizer();
		Log::message("The name of the obstacle is: (%s)\n", obstacle->getName());

	}
	return 1;

}


```
