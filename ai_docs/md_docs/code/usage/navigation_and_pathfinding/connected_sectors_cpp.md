# Creating Routes within Connected Navigation Sectors (CPP)


The example guides you through the process of setting up a scene with a navigation area of a complex form and calculating 2D and 3D routes within it.


In UNIGINE, only *[Navigation Sectors](../../../objects/navigations/navigation/navigation_sector/index.md)* can be used for calculation of both 2D and 3D routes. The navigation sectors can be easily rearranged, disabled, or enabled on the fly. Moreover, you can specify the sectors that can participate in pathfinding and exclude others. In order to form a unified navigation area, the sectors must intersect with each other.


Let's consider these features in detail.


## Preparing Scene


Our scene will include a navigation area that consists of multiple intersecting navigation sectors and primitives indicating the start and destination points of a route.


1. [Create](../../../sdk/projects/index_cpp.md#creation) [an empty C++ project](../../../code/cpp/application.md) via *SDK Browser*.
2. Open it in UnigineEditor and remove the unnecessary default nodes.
3. In the Menu bar, choose *Create -> Navigation -> Navigation Sector* and place the node above the plane. > **Notice:** To facilitate working with the navigation sectors, activate gizmos for *Navigation* nodes in the *[Helpers Panel](../../../editor2/using_visual_helpers/index.md)*. ![](2D_nav_sector_cuboid.png)
4. Add 8 more navigation sectors to the scene by cloning (**Ctrl+D**) the existing sector and place them as follows: > **Notice:** You can position the sectors manually using manipulators or by specifying the exact position via the *Parameters* window. ![](2D_nav_sector_add_cuboids.png)
5. In the *Parameters* window, adjust the positions of the nodes along the Z axis so that they are all positioned at the same level above the plane.
6. Add a new sector and adjust its *Size* in the *Parameters* window to give it a parallelepiped shape. ![](2D_parallelepiped_size.png) > **Notice:** At this step, you can approximately set the size of the sector. However, you may need to adjust it later to prevent excluding the navigation sector from pathfinding.
7. Connect the cuboid-shaped navigation sectors: place the new sector between them. ![](2D_nav_sector_parallelepiped.png) > **Notice:** For 2D routes, the height difference between the intersecting sectors must not exceed the [maximum height](../../../api/library/pathfinding/class.pathroute_cpp.md#setMaxHeight_float_void) set for the 2D route; otherwise, these sectors are discarded from pathfinding. In addition, the intersection area must exceed the radius and height of the route. So, it may be necessary to adjust the size and position of the sector to correct the intersection area.
8. Add 11 more navigation sectors that connect the cuboid-shaped sectors by cloning (**Ctrl+D**) the existing sector and place them as follows: ![](2D_nav_sector_network.png)
9. Organize the created navigation sectors in a hierarchy. It will allow you to manage the navigation area as a single node. Select all the navigation sectors, right-click, and choose *Group* in the drop-down list or press **Ctrl+G**. ![](2D_nav_sector_hierarchy.png)
10. Add 2 nodes to be used as the start and destination points of the route. We will create 2 boxes (*Create -> Primitives -> Box*), rename them ***start*** and ***finish***, and then place them inside the navigation sector as pictured below. ![](2D_connected_sectors_points.png)


## Creating Component for 2D Route Calculation


The created navigation sectors only provide the area within which routes are calculated. The routes themselves must be created from the code. So, let's create the corresponding C++ component for 2D route calculation.


> **Notice:** If you have completed the previous guide on [creating routes within a simple navigation sector](../../../code/usage/navigation_and_pathfinding/sector_with_obstacles_cpp.md), you can skip this step and copy the implemented `Route2D` component to the `source` folder of your project (both the `*.h` and `*.cpp` files).


Add a new `Route2D` class inherited from the `ComponentBase` class (the `*.h` and `*.cpp` files) to the project. The class name will be used as the property name.


## Implementing Component Logic


> **Notice:** If you have copied the `Route2D` component on the previous step, you can skip this one.


1. In the `Route2D.h` file, declare a component class, parameters, and a route: ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UniginePathFinding.h> using namespace Unigine; using namespace Math; // derive the component from the ComponentBase class class Route2D : public ComponentBase { public: // declare constructor and destructor and define a property name. The Route2D.prop file containing all parameters listed below will be saved in your project's data folder COMPONENT_DEFINE(Route2D, ComponentBase); // declare methods to be called at the corresponding stages of the execution sequence COMPONENT_INIT(init); COMPONENT_UPDATE(update); COMPONENT_SHUTDOWN(shutdown); // declare parameters of the component PROP_PARAM(Node, startPoint, NULL); PROP_PARAM(Node, finishPoint, NULL); PROP_PARAM(Color, routeColor, vec4_zero); void init(); void update(); void shutdown(); private: // declare a route PathRoutePtr route; }; ```

  - Two parameters that will accept nodes between which a route should be calculated.
  - Route color.
2. In the `Route2D.cpp` file, register the component. ```cpp #include "Route2D.h" REGISTER_COMPONENT(Route2D); ```
3. Create a route and set the radius and height for the point which will move along the route in the *init()* method. Before creation, check if the nodes to be used as the start and finish points are specified. ```cpp #include "Route2D.h" #include <UnigineNode.h> #include <UnigineConsole.h> #include <UnigineVisualizer.h> #include <UnigineLog.h> REGISTER_COMPONENT(Route2D); void Route2D::init() { // check if the start and destination nodes are correctly specified via the component interface if (startPoint && finishPoint) { // create a new route route = PathRoute::create(); // set a radius and height for the point which will move along the route route->setRadius(0.1f); route->setHeight(0.1f); } } ```
4. To enable displaying the calculated route at run time, turn on the *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)*. Additionally, you can output console messages to the application screen. Add the following logic to the *init()* function: ```cpp Console::setOnscreen(true); Visualizer::setEnabled(true); ```
5. In the *update()* function, calculate the route from the start to destination node: ```cpp void Route2D::update() { if (startPoint && finishPoint) { route->create2D(startPoint->getWorldPosition(), finishPoint->getWorldPosition()); if (route->isReached()) { // if the destination point is reached, render the root in a specified color route->renderVisualizer(routeColor); } else Log::message("PathRoute not reached yet\n"); } } ``` > **Notice:** Here the route is recalculated each frame. However, it is not optimal for application performance. Instead, you can calculate the route once per several frames: pass a [delay](../../../api/library/pathfinding/class.pathroute_cpp.md#create2D_Vec3_Vec3_int_void) to the *create2D()* function as the third argument.
6. Implement the *shutdown()* function to disable the visualizer and onscreen console messages: ```cpp void Route2D::shutdown() { Console::setOnscreen(false); Visualizer::setEnabled(false); } ```
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


## Visualizing Navigation Area


To clearly show how the path is built inside the navigation area, let's implement the `AreaVisualizer` component that enables displaying the navigation area gizmo at run time:


1. Add a new *AreaVisualizer* class inherited from the *ComponentBase* class (the `*.h` and `*.cpp` files) to the project.
2. Implement the logic: ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UniginePathFinding.h> using namespace Unigine; class AreaVisualizer : public ComponentBase { public: COMPONENT_DEFINE(AreaVisualizer, ComponentBase); COMPONENT_UPDATE(update); void update(); }; ``` ```cpp #include "AreaVisualizer.h" #include <UnigineVisualizer.h> REGISTER_COMPONENT(AreaVisualizer); void AreaVisualizer::update() { // display the navigation area gizmo node->renderVisualizer(); } ```
3. Build the project and run it once again to generate the property for the `AreaVisualizer` component.
4. Assign the component to each navigation sector forming the navigation area.


## Trying Out


Launch the application to check the result.


> **Notice:** If the route is not reached, try to modify the route parameters (a point height and/or radius) or adjust the size of the sector(s) or intersection area(s), as the point moving along the route must fit the size of the navigation area.


![](2D_route_0.png)


## Excluding Sectors from Pathfinding


Sometimes, it might be necessary to ignore some navigation sectors during pathfinding. For this purpose, you can set the *[Navigation](../../../objects/navigations/navigation/navigation_sector/index.md#edit)* mask for both the navigation sector and the route so that they don't match.


1. Select one of the navigation sectors participating in pathfinding. ![](2D_nav_sector_select.png)
2. Change its *Navigation Mask* in the *Parameters* window. ![](2D_nav_sector_mask.png)
3. Run the application to check how the route is recalculated. ![](2D_route_0.png) ![](2D_route_1.png)


## Modifying Component for 3D Route Calculation


The navigation sector also enables the calculation of 3D routes, with some features that differ from the 2D routes:


- For 3D routes, the point moves in 3 dimensions.
- Only the radius set for the point matters: if the radius set for the point is greater than the size of the navigation sector, it will be discarded.
- The maximum height set for the route determines the upper limit of the point's vertical movement.


You can force the `Route2D` component to calculate a 3D route within the same navigation area by changing a single line of the code. Replace the *create2D()* function call with the following:


```cpp
route->create3D(startPoint->getWorldPosition(), finishPoint->getWorldPosition());

```


Then build the project and run it once again to re-generate the property for the `Route2D` component.


Run the application to check the result.


![](3D_route_connected_sectors.png)
