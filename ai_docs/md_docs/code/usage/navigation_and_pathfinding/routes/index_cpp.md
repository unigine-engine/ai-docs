# Creating Routes (CPP)


UNIGINE has a built-in pathfinding system that includes [navigation areas](../../../../api/library/pathfinding/class.navigation_cpp.md), [obstacles](../../../../api/library/pathfinding/class.obstacle_cpp.md) and functions of the *[PathRoute](../../../../api/library/pathfinding/class.pathroute_cpp.md)* class that are used to calculate the optimal routes among obstacles within navigation areas.


> **Warning:** 3D navigation feature is experimental and not recommended for production use.


Via UnigineEditor, you can only add a navigation area (a sector or a mesh) to the scene and place obstacles. The 2D or 3D route that is calculated within the navigation area should be created from the code.


## Creating a Route within Navigation Area


To create a [route](../../../../api/library/pathfinding/class.pathroute_cpp.md#desc) within a navigation area, in which no obstacles are placed, you can use the following:


```cpp
// declare points between which a route should be calculated
Unigine::Math::Vec3 p0 = Unigine::Math::Vec3(-60.0f, -60.0f, 5.0f);
Unigine::Math::Vec3 p1 = Unigine::Math::Vec3(60.0f, 60.0f, 5.0f);


```


```cpp
// create a new route
route = PathRoute::create();
// set a radius for the point which will move along the route
route->setRadius(1.2f);


```


```cpp
// create a 3D route
route->create3D(p0,p1);

```


> **Notice:** You can create a 2D route the same way by calling the *[create2D()](../../../../api/library/pathfinding/class.pathroute_cpp.md#create2D_Vec3_Vec3_int_void)* function.


To visualize the calculated route, call the *[renderVisualizer()](../../../../api/library/pathfinding/class.pathroute_cpp.md#renderVisualizer_vec4_void)* function of the *PathRoute* class:


```cpp
route->renderVisualizer(vec4(1.0f));
```


To visualize the navigation area, call the *[renderVisualizer()](../../../../api/library/nodes/class.node_cpp.md#renderVisualizer_void)* functions of the Node class:


```cpp
sector->renderVisualizer();
```


> **Notice:** You should enable the engine visualizer by calling *[Visualizer::setEnabled(1);](../../../../api/library/engine/class.visualizer_cpp.md#setEnabled_int_void)*


You can affect route calculation via UnigineEditor by adjusting parameters of the navigation sector or mesh.


## Creating a Route within Navigation Area with Obstacles


Creating the route within a navigation area with [obstacles](../../../../objects/navigations/obstacle/index.md) is similar to creating the route within an empty navigation area. Moreover, the route will be recalculated if the obstacle changes its transformation.


If the obstacle is connected with a dynamically changing node that should be bypassed, this node should be set as a parent node for the obstacle. This will enable simultaneous changing transformation of the node and the obstacle. For example:


```cpp
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineObjects.h>
#include <UniginePathFinding.h>

class AppWorldLogic : public Unigine::WorldLogic
{

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	int init() override;

	int update() override;
	int postUpdate() override;
	int updatePhysics() override;

	int shutdown() override;

private:

	// declare the required variables
	Unigine::ObstacleBoxPtr box_obstacle;
	Unigine::ObjectMeshStaticPtr box;
	Unigine::PathRoutePtr route;

	// declare points between which a route should be calculated
	Unigine::Math::Vec3 p0 = Unigine::Math::Vec3(-60.0f, -60.0f, 5.0f);
	Unigine::Math::Vec3 p1 = Unigine::Math::Vec3(60.0f, 60.0f, 5.0f);

};

#endif // __APP_WORLD_LOGIC_H__

```


```cpp
#include "AppWorldLogic.h"
#include <UnigineEditor.h>
#include <UnigineGame.h>
#include <UnigineVisualizer.h>
#include <UnigineLog.h>

using namespace Unigine;
using namespace Math;

// World logic, it takes effect only when the world is loaded.
// These methods are called right after corresponding world script's (UnigineScript) methods.

AppWorldLogic::AppWorldLogic()
{
}

AppWorldLogic::~AppWorldLogic()
{
}

int AppWorldLogic::init()
{
	// enable the engine visualizer
	Visualizer::setEnabled(1);

	// create a navigation sector within which pathfinding will be performed
	NavigationSectorPtr navigation = NavigationSector::create(vec3(128.0f, 128.0f, 8.0f));
	navigation->setWorldTransform(translate(Vec3(1.0f, 1.0f, 5.0f)));

	// create the ObjectMeshStatic that should be bypassed
	box = ObjectMeshStatic::create("core/meshes/box.mesh");
	box->setPosition(Vec3(2.0f, 2.2f, 1.5f));
	box->setScale(vec3(2.0f, 2.0f, 2.0f));

	// create an obstacle
	box_obstacle = ObstacleBox::create(vec3(1.2f, 1.2f, 1.2f));
	box_obstacle->setPosition(Vec3(0.0f, 0.0f, 0.0f));

	// add the obstacle as the child node to the mesh in order to change their transformation simultaneously
	box->addChild(box_obstacle);

	// create a new route
	route = PathRoute::create();
	// set a radius for the point which will move along the route
	route->setRadius(1.2f);

	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// start of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppWorldLogic::update()
{
	// get the frame duration
	float ifps = Game::getIFps();
	// and define the angle of the object's rotation
	float angle = ifps * 90.0f;

	// change transformation of the mesh
	box->setTransform(box->getTransform() * Mat4(rotateZ(angle)));
	// render the bounding box of the obstacle
	box_obstacle->renderVisualizer();

	// recalculate the route in the current frame and render its visualizer
	route->create2D(p0, p1);
	if (route->isReached()) route->renderVisualizer(vec4(1.0f));
	else Log::message("PathRoute failed");

	return 1;
}

int AppWorldLogic::postUpdate()
{
	// The engine calls this function after updating each render frame: correct behavior after the state of the node has been updated.
	return 1;
}

int AppWorldLogic::updatePhysics()
{
	// Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations.
	// The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value.
	// WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress.
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// end of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppWorldLogic::shutdown()
{
	// Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks.
	return 1;
}

```


> **Notice:** In the example above, the route is recalculated each frame. However, it is non-optimal for application performance. You can calculate the route, for example, once per 10 frames.


As a result, you will have a simple navigation sector, in which the dynamically changing obstacle box is placed.


![](obstacle_sample.gif)

*Here the obstacle is highlighted with red*
