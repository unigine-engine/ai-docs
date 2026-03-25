# Creating Routes (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


UNIGINE has a built-in pathfinding system that includes [navigation areas](../../../../api/library/pathfinding/class.navigation_usc.md), [obstacles](../../../../api/library/pathfinding/class.obstacle_usc.md) and functions of the *[PathRoute](../../../../api/library/pathfinding/class.pathroute_usc.md)* class that are used to calculate the optimal routes among obstacles within navigation areas.


> **Warning:** 3D navigation feature is experimental and not recommended for production use.


Via UnigineEditor, you can only add a navigation area (a sector or a mesh) to the scene and place obstacles. The 2D or 3D route that is calculated within the navigation area should be created from the code.


## Creating a Route within Navigation Area


To create a [route](../../../../api/library/pathfinding/class.pathroute_usc.md#desc) within a navigation area, in which no obstacles are placed, you can use the following:


```cpp
// create a new route
PathRoute route = new PathRoute();
// set a radius for the point which will move along the route
route.setRadius(2.0f);

// declare points between which the route should be calculated
Vec3 p0 = Vec3(-60.0f,-60.0f,5.0f);
Vec3 p1 = Vec3( 60.0f, 60.0f,5.0f);

// create a 3D route
route.create3D(p0,p1);

```


> **Notice:** You can create a 2D route the same way by calling the *[create2D()](../../../../api/library/pathfinding/class.pathroute_usc.md#create2D_Vec3_Vec3_int_void)* function.


To visualize the calculated route, call the *[renderVisualizer()](../../../../api/library/pathfinding/class.pathroute_usc.md#renderVisualizer_vec4_void)* function of the *PathRoute* class:


```cpp
route.renderVisualizer(vec4(1.0f));
```


To visualize the navigation area, call the *[renderVisualizer()](../../../../api/library/nodes/class.node_usc.md#renderVisualizer_void)* functions of the Node class:


```cpp
sector.renderVisualizer();
```


> **Notice:** You should enable the engine visualizer by calling *[engine.visualizer.setEnabled(1);](../../../../api/library/engine/class.visualizer_usc.md#setEnabled_int_void)*


You can affect route calculation via UnigineEditor by adjusting parameters of the navigation sector or mesh.


## Creating a Route within Navigation Area with Obstacles


Creating the route within a navigation area with [obstacles](../../../../objects/navigations/obstacle/index.md) is similar to creating the route within an empty navigation area. Moreover, the route will be recalculated if the obstacle changes its transformation.


If the obstacle is connected with a dynamically changing node that should be bypassed, this node should be set as a parent node for the obstacle. This will enable simultaneous changing transformation of the node and the obstacle. For example:


```cpp
ObstacleBox box;
ObjectMeshStatic mesh;
PathRoute route;

Vec3 p0 = Vec3(-60.0f,-60.0f,5.0f);
Vec3 p1 = Vec3( 60.0f, 60.0f,5.0f);
/*
 */
int init() {

	// create a navigation sector within which pathfinding will be performed
	NavigationSector navigation = new NavigationSector(vec3(128.0f,128.0f,8.0f));
	navigation.setWorldTransform(translate(Vec3(1.0f,1.0f,5.0f)));

	// create a mesh that should be bypassed
	mesh = new ObjectMeshStatic("samples/common/meshes/box.mesh");
	mesh.setPosition(Vec3(2.0f,2.2f,1.5f));
	mesh.setScale(Vec3(2.0f,2.0f,2.0f));

	// create an obstacle
	box = new ObstacleBox(vec3(1.2f,1.2f,1.2f));
	box.setPosition(Vec3(0.0f,0.0f,0.0f));
	// add the obstacle as the child node to the mesh in order to change their transformation simultaneously
	mesh.addChild(box);

	// create a new route
	route = new PathRoute();
	// set a radius for the point which will move along the route
	route.setRadius(2.0f);

	return 1;
}
/*
 */
int update() {

	// get the frame duration
	float ifps = engine.game.getIFps();
	// and define the angle of the object's rotation
	float angle = ifps * 90.0f;

	// change transformation of the mesh
	mesh.setTransform(mesh.getTransform() * rotateZ(angle));

	box.renderVisualizer();

	// recalculate the route in the current frame and render its visualizer
	route.create2D(p0,p1);
	route.renderVisualizer(vec4(1.0f));

	return 1;
}

```


> **Notice:** In the example above, the route is recalculated each frame. However, it is non-optimal for application performance. You can calculate the route, for example, once per 10 frames.


As a result, you will have a simple navigation sector, in which the dynamically changing obstacle box is placed.


![](obstacle_sample.gif)

*Here the obstacle is highlighted with red*
