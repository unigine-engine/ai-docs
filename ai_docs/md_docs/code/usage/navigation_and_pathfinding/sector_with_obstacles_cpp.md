# Creating 2D Routes within Navigation Area with Obstacles (CPP)


The example guides you through the process of setting up a scene with a simple navigation area and calculating a 2D route within it.


## Preparing Scene


Before calculating routes, we should create a navigation area within which this logic will be executed. Our navigation area will be represented by a single navigation sector with obstacles. Also, we will add some auxiliary nodes that will serve as the start and destination points of the route.


1. [Create an empty project](../../../sdk/projects/index_cpp.md#creation) via SDK Browser.
2. Open it in UnigineEditor and remove the unnecessary default nodes.
3. In the Menu bar, choose *Create -> Navigation -> Navigation Sector* and place the node above the plane. > **Notice:** To facilitate working with the navigation sectors, activate gizmos for *Navigation* nodes in the *[Helpers Panel](../../../editor2/using_visual_helpers/index.md)*. ![](2D_nav_sector_cuboid.png)
4. Adjust the *Size* of the sector in the *Parameters* window. ![](2D_nav_sector_size_values.png) ![](2D_nav_sector_size.png)
5. Add 2 nodes that will be used as the start and destination points of the route. We will create 2 boxes (*Create -> Primitives -> Box*), rename them ***start*** and ***finish***, and place inside the navigation sector as pictured below. ![](2D_start_dest_points.png)
6. Create several primitives and place them inside the navigation area. We will add a capsule and two boxes. ![](2D_add_primitives.png)
7. Make them dynamic: switch from *Immovable* to *Dynamic* in the *Parameters* window. ![](2D_switch_dynamic.png)
8. For each primitive, create an obstacle of the required type: in the *World Hierarchy* window, right-click the primitive, choose *Create -> Navigation*, and select the obstacle. The created obstacle will be added as a child to the primitive node in the hierarchy. > **Notice:** It will allow you to change the node and obstacle transformations at the same time without any extra configuration. ![](2D_obstacles_hierarchy.png)
9. Adjust the size of the created obstacles in the *Parameters* window if necessary. ![](2D_add_obstacles.png)


## Creating Component for Route Calculation


The created navigation sector only provides the area within which routes are calculated. The routes themselves must be created from the code. So, let's create the corresponding C++ component for 2D route calculation.


Add a new `Route2D` class inherited from the `ComponentBase` class (the `*.h` and `*.cpp` files) to the project. The class name will be used as the property name.


## Implementing Component Logic


1. In the `Route2D.h` file, declare a component class, parameters and a route: ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UniginePathFinding.h> using namespace Unigine; using namespace Math; // derive the component from the ComponentBase class class Route2D : public ComponentBase { public: // declare constructor and destructor and define a property name. The Route2D.prop file containing all parameters listed below will be saved in your project's data folder COMPONENT_DEFINE(Route2D, ComponentBase); // declare methods to be called at the corresponding stages of the execution sequence COMPONENT_INIT(init); COMPONENT_UPDATE(update); COMPONENT_SHUTDOWN(shutdown); // declare parameters of the component PROP_PARAM(Node, startPoint, NULL); PROP_PARAM(Node, finishPoint, NULL); PROP_PARAM(Color, routeColor, vec4_zero); void init(); void update(); void shutdown(); private: // declare a route PathRoutePtr route; }; ```

  - Two parameters that will accept nodes between which a route should be calculated.
  - Route color.
2. In the `Route2D.cpp` file, register the component. ```cpp #include "Route2D.h" REGISTER_COMPONENT(Route2D); ```
3. Create a route and set the radius and height for the point which will move along the route in the *init()* method. Before creation, check if the nodes to be used as the start and finish points are specified. ```cpp #include "Route2D.h" #include <UnigineNode.h> #include <UnigineConsole.h> #include <UnigineVisualizer.h> #include <UnigineLog.h> REGISTER_COMPONENT(Route2D); void Route2D::init() { // check if the start and destination nodes are correctly specified via the component interface if (startPoint && finishPoint) { // create a new route route = PathRoute::create(); // set a radius and height for the point which will move along the route route->setRadius(0.1f); route->setHeight(0.1f); } } ```
4. To enable displaying the calculated route at run time, turn on the *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)*. Additionally, you can output console messages to the application screen. Add the following logic to the *init()* function: ```cpp Console::setOnscreen(true); Visualizer::setEnabled(true); ```
5. In the *update()* function, calculate the route from the start to destination node: ```cpp void Route2D::update() { if (startPoint && finishPoint) { route->create2D(startPoint->getWorldPosition(), finishPoint->getWorldPosition()); if (route->isReached()) { // if the destination point is reached, render the root in a specified color route->renderVisualizer(routeColor); } else Log::message("PathRoute not reached yet\n"); } } ``` > **Notice:** Here the route is recalculated each frame. However, it is not optimal for application performance. Instead, you can calculate the route once per several frames: pass a [delay](../../../api/library/pathfinding/class.pathroute_cpp.md#create2D_Vec3_Vec3_int_void) to the *create2D()* function as the third argument.
6. Implement the *shutdown()* function to disable the *Visualizer* and onscreen console messages: ```cpp void Route2D::shutdown() { Console::setOnscreen(false); Visualizer::setEnabled(false); } ```
7. The component is registered automatically by the Component System upon its initialization. However, you should add the following to the *AppSystemLogic::init()* method: ```cpp #include "AppSystemLogic.h" #include <UnigineComponentSystem.h> int AppSystemLogic::init() { // initialize ComponentSystem and register all components Unigine::ComponentSystem::get()->initialize(); return 1; } ```
8. Build the project and run it once to generate the property for the `Route2D` component. It will be located in the `data/ComponentSystem` folder.


Here is the full code of the component:


<details>
<summary>Route2D.h | Close</summary>

```cpp
#pragma once

#include <UnigineComponentSystem.h>
#include <UniginePathFinding.h>

using namespace Unigine;
using namespace Math;

// derive the component from the ComponentBase class
class Route2D : public ComponentBase
{
public:

	// declare constructor and destructor and define a property name. The Route2D.prop file containing all parameters listed below will be saved in your project's data folder
	COMPONENT_DEFINE(Route2D, ComponentBase);
	// declare methods to be called at the corresponding stages of the execution sequence
	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);
	COMPONENT_SHUTDOWN(shutdown);

	// declare parameters of the component
	PROP_PARAM(Node, startPoint, NULL);
	PROP_PARAM(Node, finishPoint, NULL);
	PROP_PARAM(Color, routeColor, vec4_zero);

	void init();
	void update();
	void shutdown();

private:
	// declare a route
	PathRoutePtr route;
};


```

</details>


<details>
<summary>Route2D.cpp | Close</summary>

```cpp
#include "Route2D.h"

#include <UnigineNode.h>
#include <UnigineConsole.h>
#include <UnigineVisualizer.h>
#include <UnigineLog.h>

REGISTER_COMPONENT(Route2D);

void Route2D::init() {
	// check if the start and destination nodes are correctly specified via the component interface
	if (startPoint && finishPoint)
	{
		// create a new route
		route = PathRoute::create();

		// set a radius and height for the point which will move along the route
		route->setRadius(0.1f);
		route->setHeight(0.1f);
		Console::setOnscreen(true);
		Visualizer::setEnabled(true);
	}
}

void Route2D::update() {

	if (startPoint && finishPoint)
	{
		route->create2D(startPoint->getWorldPosition(), finishPoint->getWorldPosition());
		if (route->isReached())
		{
			// if the destination point is reached, render the root in a specified color
			route->renderVisualizer(routeColor);
		}
		else
			Log::message("PathRoute not reached yet\n");
	}
}
void Route2D::shutdown() {

	Console::setOnscreen(false);
	Visualizer::setEnabled(false);
}

```

</details>


## Assigning Component


When the component logic is implemented and the property is generated, you should assign it to a node.


1. In UnigineEditor, select *Create -> Node -> Dummy* and place it in the navigation area.
2. Select the dummy node and assign the `Route2D` property to it in the *Parameters* window.
3. In the component parameters, specify the ***start*** and ***finish*** static meshes in the *Start Point* and *Finish Point* fields. ![](2D_component_parameters.png)
4. Change the *Route Color*, if necessary.


## Making Obstacles Move Dynamically


Let's add a bit of complexity to the logic and make the nodes that are used as obstacles dynamically change.


1. Add a new *NodeRotator* class inherited from the *ComponentBase* class (the `*.h` and `*.cpp` files) to the project.
2. Implement rotation logic: ```cpp #include <UnigineComponentSystem.h> using namespace Unigine; using namespace Math; class NodeRotator : public ComponentBase { public: COMPONENT_DEFINE(NodeRotator, ComponentBase); COMPONENT_UPDATE(update); // declare a parameter of the component PROP_PARAM(Vec3, angularVelocity, vec3_zero); void update(); }; ``` ```cpp #include "NodeRotator.h" #include <UnigineGame.h> REGISTER_COMPONENT(NodeRotator); void NodeRotator::update() { // calculate the delta of rotation vec3 delta = angularVelocity * Game::getIFps(); // update node rotation node->setRotation(node->getRotation() * quat(delta.x, delta.y, delta.z)); } ```
3. Build the project and run it once again to generate the property for the `NodeRotator` component.
4. Assign the component to the ***capsule*** primitive that should rotate and specify the *Angular Velocity*: ![](2D_component_rotator.png) The obstacle will rotate as well.
5. Group the ***sphere*** primitives and assign the component to the parent dummy node. It will make the spheres rotate around this parent node (as in the case of a sphere, rotation around its own axis won't affect the route calculation). ![](2D_group_of_spheres.png)


## Visualizing Navigation Area


To clearly show how the path is built inside the navigation area, let's implement the `AreaVisualizer` component that enables displaying the navigation area gizmo at run time:


1. Add a new *AreaVisualizer* class inherited from the *ComponentBase* class (the `*.h` and `*.cpp` files) to the project.
2. Implement the logic: ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UniginePathFinding.h> using namespace Unigine; class AreaVisualizer : public ComponentBase { public: COMPONENT_DEFINE(AreaVisualizer, ComponentBase); COMPONENT_UPDATE(update); void update(); }; ``` ```cpp #include "AreaVisualizer.h" #include <UnigineVisualizer.h> REGISTER_COMPONENT(AreaVisualizer); void AreaVisualizer::update() { // display the navigation area gizmo node->renderVisualizer(); } ```
3. Build the project and run it once again to generate the property for the `AreaVisualizer` component.
4. Assign the component to the navigation sector.


## Trying Out


Launch the application to check the result.


![](2D_run_result.png)
