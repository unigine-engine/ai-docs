# Creating Routes (CS)


UNIGINE has a built-in pathfinding system that includes [navigation areas](../../../../api/library/pathfinding/class.navigation_cs.md), [obstacles](../../../../api/library/pathfinding/class.obstacle_cs.md) and functions of the *[PathRoute](../../../../api/library/pathfinding/class.pathroute_cs.md)* class that are used to calculate the optimal routes among obstacles within navigation areas.


> **Warning:** 3D navigation feature is experimental and not recommended for production use.


Via UnigineEditor, you can only add a navigation area (a sector or a mesh) to the scene and place obstacles. The 2D or 3D route that is calculated within the navigation area should be created from the code.


## Creating a Route within Navigation Area


To create a [route](../../../../api/library/pathfinding/class.pathroute_cs.md#desc) within a navigation area, in which no obstacles are placed, you can use the following:


You can affect route calculation via UnigineEditor by adjusting parameters of the navigation sector or mesh.


## Creating a Route within Navigation Area with Obstacles


Creating the route within a navigation area with [obstacles](../../../../objects/navigations/obstacle/index.md) is similar to creating the route within an empty navigation area. Moreover, the route will be recalculated if the obstacle changes its transformation.


If the obstacle is connected with a dynamically changing node that should be bypassed, this node should be set as a parent node for the obstacle. This will enable simultaneous changing transformation of the node and the obstacle. For example:


```csharp
#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Vec4 = Unigine.dvec4;
using Mat4 = Unigine.dmat4;
#else
	using Vec3 = Unigine.vec3;
	using Vec4 = Unigine.vec4;
	using Mat4 = Unigine.mat4;
#endif

using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class Route : Component
{
	// declare the required variables
	ObstacleBox box_obstacle;
	ObjectMeshStatic box;
	PathRoute route;

	// declare points between which a route should be calculated
	Vec3 p0 = new Vec3(-60.0f, -60.0f, 5.0f);
	Vec3 p1 = new Vec3(60.0f, 60.0f, 5.0f);

	private void Init()
	{
		// enable the engine visualizer
		Visualizer.Enabled = true;

		// create a navigation sector within which pathfinding will be performed
		NavigationSector navigation = new NavigationSector(new vec3(128.0f, 128.0f, 8.0f));
		navigation.WorldTransform = MathLib.Translate(new Vec3(1.0f, 1.0f, 5.0f));

		// create the ObjectMeshStatic that should be bypassed
		box = new ObjectMeshStatic("core/meshes/box.mesh");

		box.Position = new Vec3(2.0f, 2.2f, 1.5f);
		box.Scale = new vec3(2.0f, 2.0f, 2.0f);

		// create an obstacle
		box_obstacle = new ObstacleBox(new vec3(1.2f, 1.2f, 1.2f));

		box_obstacle.Position = new Vec3(0.0f, 0.0f, 0.0f);
		// add the obstacle as the child node to the mesh in order to change their transformation simultaneously
		box.AddChild(box_obstacle);

		// create a new route
		route = new PathRoute();
		// set a radius for the point which will move along the route
		route.Radius = 1.2f;
	}

	private void Update()
	{
		 // get the frame duration
		float ifps = Game.IFps;
		// and define the angle of the object's rotation
		float angle = ifps * 90.0f;

		// change transformation of the mesh
		box.Transform = box.Transform * new Mat4(MathLib.RotateZ(angle));
		// render the bounding box of the obstacle
		box_obstacle.RenderVisualizer();

		// recalculate the route in the current frame and render its visualizer
		route.Create2D(p0, p1);
		route.RenderVisualizer(new vec4(1.0f));

	}
}

```


> **Notice:** In the example above, the route is recalculated each frame. However, it is non-optimal for application performance. You can calculate the route, for example, once per 10 frames.


As a result, you will have a simple navigation sector, in which the dynamically changing obstacle box is placed.


![](obstacle_sample.gif)

*Here the obstacle is highlighted with red*
