# Creating 2D Routes within Navigation Area with Obstacles (CS)


The example guides you through the process of setting up a scene with a simple navigation area and calculating a 2D route within it.


## Preparing Scene


Before calculating routes, we should create a navigation area within which this logic will be executed. Our navigation area will be represented by a single navigation sector with obstacles. Also, we will add some auxiliary nodes that will serve as the start and destination points of the route.


1. [Create an empty project](../../../sdk/projects/index_cs.md#creation) via SDK Browser.
2. Open it in UnigineEditor and remove the unnecessary default nodes.
3. In the Menu bar, choose *Create -> Navigation -> Navigation Sector* and place the node above the plane. > **Notice:** To facilitate working with the navigation sectors, activate gizmos for *Navigation* nodes in the *[Helpers Panel](../../../editor2/using_visual_helpers/index.md)*. ![](2D_nav_sector_cuboid.png)
4. Adjust the *Size* of the sector in the *Parameters* window. ![](2D_nav_sector_size_values.png) ![](2D_nav_sector_size.png)
5. Add 2 nodes that will be used as the start and destination points of the route. We will create 2 boxes (*Create -> Primitives -> Box*), rename them ***start*** and ***finish***, and place inside the navigation sector as pictured below. ![](2D_start_dest_points.png)
6. Create several primitives and place them inside the navigation area. We will add a capsule and two boxes. ![](2D_add_primitives.png)
7. Make them dynamic: switch from *Immovable* to *Dynamic* in the *Parameters* window. ![](2D_switch_dynamic.png)
8. For each primitive, create an obstacle of the required type: in the *World Hierarchy* window, right-click the primitive, choose *Create -> Navigation*, and select the obstacle. The created obstacle will be added as a child to the primitive node in the hierarchy. > **Notice:** It will allow you to change the node and obstacle transformations at the same time without any extra configuration. ![](2D_obstacles_hierarchy.png)
9. Adjust the size of the created obstacles in the *Parameters* window if necessary. ![](2D_add_obstacles.png)


## Creating Component for Route Calculation


The created navigation sector only provides the area within which routes are calculated. The routes themselves must be created from the code. So, let's create the corresponding C# component for 2D route calculation:


1. Create the `components` folder in the `data` directory of your project: right-click in the Asset Browser and select *Create Folder*.
2. In the created folder, create a new component: right-click and select *Create Code -> C# Component* and specify a name for the component. ![](2D_path_route_component.png)
3. Open the component in IDE to implement pathfinding logic.


## Implementing Component Logic


1. Declare component parameters: ```csharp public class Route2D : Component { // a node that will serve as a start point public Node startPoint = null; // a node that will serve as a destination point public Node finishPoint = null; // route color [ParameterColor] public vec4 routeColor = vec4.ZERO; // ... } ```

  - Two parameters that will accept nodes between which a route should be calculated
  - Route color
2. Create a route and set the radius and height for the point which will move along the route in the *Init()* method. Before creation, check if the nodes to be used as the start and finish points are specified. ```csharp // a route private PathRoute route = null; private void Init() { // check if the start and destination nodes are correctly specified via the component interface if (startPoint && finishPoint) { // create a new route route = new PathRoute(); // set a radius and height for the point which will move along the route route.Radius = 0.1f; route.Height = 0.1f; } } ```
3. To enable displaying the calculated route at run time, turn on the *[Visualizer](../../../api/library/engine/class.visualizer_cs.md)*. Additionally, you can output console messages to the application screen. Add the following logic to the *Init()* function: ```csharp // enable the onscreen console messages to display info on route calculation Unigine.Console.Onscreen = true; // enable visualization of the calculated route Visualizer.Enabled = true; ```
4. In the *Update()* function, calculate the route from the start to destination node: ```csharp private void Update() { // check if the start and destination nodes are correctly specified via the component interface if (startPoint && finishPoint) { // calculate the path from the start to destination point // a destination point of the route is reached route.Create2D(startPoint.WorldPosition, finishPoint.WorldPosition); if (route.IsReached) { // if the destination point is reached, render the root in a specified color route.RenderVisualizer(routeColor); } else Log.Message($"{node.Name} PathRoute not reached yet\n"); } } ``` > **Notice:** Here the route is recalculated each frame. However, it is not optimal for application performance. Instead, you can calculate the route once per several frames: pass a [delay](../../../api/library/pathfinding/class.pathroute_cs.md#create2D_Vec3_Vec3_int_void) to the *Create2D()* function as the third argument.
5. Implement the *Shutdown()* function to disable the visualizer and onscreen console messages: ```csharp private void Shutdown() { Unigine.Console.Onscreen = false; Visualizer.Enabled = false; } ```


Here is the full code of the component:


<details>
<summary>Route2D.cs | Close</summary>

`Route2D.cs`


```csharp
using System.Collections;
using System.Collections.Generic;
using Unigine;

public class Route2D : Component
{
	// a node that will serve as a start point
	public Node startPoint = null;
	// a node that will serve as a destination point
	public Node finishPoint = null;

	// route color
	[ParameterColor]
	public vec4 routeColor = vec4.ZERO;
	// a route
	private PathRoute route = null;

	private void Init()
	{
		// check if the start and destination nodes are correctly specified via the component interface
		if (startPoint && finishPoint)
		{
			// create a new route
			route = new PathRoute();

			// set a radius and height for the point which will move along the route
			route.Radius = 0.1f;
			route.Height = 0.1f;
			// enable the onscreen console messages to display info on route calculation
			Unigine.Console.Onscreen = true;
			// enable visualization of the calculated route
			Visualizer.Enabled = true;
		}
	}
	private void Update()
	{
		// check if the start and destination nodes are correctly specified via the component interface
		if (startPoint && finishPoint)
		{
			// calculate the path from the start to destination point
			// a destination point of the route is reached
			route.Create2D(startPoint.WorldPosition, finishPoint.WorldPosition);
			if (route.IsReached)
			{
				// if the destination point is reached, render the root in a specified color
				route.RenderVisualizer(routeColor);
			}
			else
				Log.Message($"{node.Name} PathRoute not reached yet\n");
		}
	}

	private void Shutdown()
	{
		Unigine.Console.Onscreen = false;
		Visualizer.Enabled = false;
	}
}

```

</details>


## Assigning Component


When the component logic is implemented, you should assign it to a node.


1. In UnigineEditor, select *Create -> Node -> Dummy* and place it in the navigation area.
2. Select the dummy node and assign the `Route2D.cs` component to it in the *Parameters* window.
3. In the component parameters, specify the ***start*** and ***finish*** static meshes in the *Start Point* and *Finish Point* fields. ![](2D_component_parameters.png)
4. Change the *Route Color*, if necessary.


## Making Obstacles Move Dynamically


Let's add a bit of complexity to the logic and make the nodes that are used as obstacles dynamically change.


1. In the `components` folder, create the `NodeRotator` component.
2. Implement rotation logic: ```csharp public partial class NodeRotator : Component { // parameter that sets an angular velocity of the node public vec3 angularVelocity = vec3.ZERO; private void Update() { // calculate the delta of rotation vec3 delta = angularVelocity * Game.IFps; // update node rotation node.SetRotation(node.GetRotation() * new quat(delta.x, delta.y, delta.z)); } } ```
3. Assign the component to the ***capsule*** primitive that should rotate and specify the *Angular Velocity*: ![](2D_component_rotator.png) The obstacle will rotate as well.
4. Group the ***sphere*** primitives and assign the component to the parent dummy node. It will make the spheres rotate around this parent node (as in the case of a sphere, rotation around its own axis won't affect the route calculation). ![](2D_group_of_spheres.png)


## Visualizing Navigation Area


To clearly show how the path is built inside the navigation area, let's implement the `AreaVisualizer` component that enables displaying the navigation area gizmo at run time:


1. In the `components` folder, create the `AreaVisualizer` component.
2. Implement the logic: ```csharp public partial class AreaVisualizer : Component { private NavigationSector navigationSector = null; private void Init() { // get the navigation sector to which the component is assigned navigationSector = node as NavigationSector; // enable rendering of the visualizer if (navigationSector) Visualizer.Enabled = true; } private void Update() { // display the navigation area gizmo if (navigationSector) navigationSector.RenderVisualizer(); } private void Shutdown() { // disable rendering of the visualizer Visualizer.Enabled = false; } } ```
3. Assign the component to the navigation sector.


## Trying Out


Click **Run** to run the component logic and check the result.


![](2D_run_result.png)
