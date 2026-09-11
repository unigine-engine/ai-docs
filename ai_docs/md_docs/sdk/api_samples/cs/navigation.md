# Navigation

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Navigation Mesh 2D

This sample demonstrates how to calculate and visualize 2D navigation paths using the **[Navigation Mesh](../../../objects/navigations/navigation/navigation_mesh/index.md)** object and *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* class via the C# API. It shows how to build a route between two points on a navigation mesh and renders the result for debugging or visualization purposes.


This setup is useful for prototyping AI navigation, testing route validity, and analyzing the structure of navigable areas in 2D gameplay scenarios.


The main logic is implemented in the **PathRoute2D** component, which initializes a *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* class instance and uses *[PathRoute.Create2D()](../../../api/library/pathfinding/class.pathroute_cpp.md#create2D_Vec3_Vec3_int_void)* to compute the path from a start node to a finish node. If the route is successfully resolved, the path is drawn on screen using *[RenderVisualizer()](../../../api/library/pathfinding/class.pathroute_cpp.md#renderVisualizer_vec4_void)*. The radius parameter is set manually to ensure the generated path accounts for the navigation agent's size, avoiding collisions with nearby geometry.


The sample includes a second component, **NavigationMeshVisualizer**, that renders the **Navigation Mesh** during runtime to help visualize navigable areas.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/navigation/navigation_mesh_2d*
## Navigation Mesh 2D Demo

This sample demonstrates how to implement dynamic 2D pathfinding using a **[Navigation Mesh](../../../objects/navigations/navigation/navigation_mesh/index.md)** object, with autonomous robots navigating toward randomly positioned targets. Each robot uses a *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* class instance to calculate a valid route within the navigation mesh and moves along it in real time.


This setup is useful for prototyping simple AI behavior such as patrolling or target chasing, where agents continuously search for and move toward dynamic goals.


The main logic is implemented in the **PathRoute2DWithTarget** component. On initialization, it creates a coin from a **[Node Reference](../../../objects/nodes/reference/index.md)** and places it at a random valid location inside the Navigation Mesh. A *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* instance is initialized with a defined agent radius to ensure the generated path accounts for the agent's size, avoiding collisions with nearby geometry.


At runtime, the component continuously checks whether the robot is near its current target. If so, the target is moved to a new valid position, and a new path is generated using *[Create2D()](../../../api/library/pathfinding/class.pathroute_cpp.md#create2D_Vec3_Vec3_int_void)*. If the route is valid, the path is drawn on screen using *[RenderVisualizer()](../../../api/library/pathfinding/class.pathroute_cpp.md#renderVisualizer_vec4_void)* and the robot moves forward along it and smoothly adjusts its orientation using quaternion interpolation.


The sample includes a second component, **NavigationMeshVisualizer**, that renders the actual mesh structure during runtime to help visualize navigable areas.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/navigation/navigation_mesh_2d_demo*
## Navigation Obstacles 2D

This sample demonstrates how to use dynamic **[Obstacles](../../../objects/navigations/obstacle/index.md)** in combination with a **[Navigation Mesh](../../../objects/navigations/navigation/navigation_mesh/index.md)** to influence 2D pathfinding in runtime. When an obstacle overlaps the navigation mesh, it temporarily modifies the traversable area, forcing the pathfinding algorithm to recalculate a valid route around it.


This example is useful for prototyping interactive environments, where navigation must adapt to moving objects, barriers, or other gameplay elements affecting traversal.


The main logic is implemented in the **PathRoute2D** component, which initializes a *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* class instance and uses *[PathRoute.Create2D()](../../../api/library/pathfinding/class.pathroute_cpp.md#create2D_Vec3_Vec3_int_void)* to compute the path from a start node to a finish node. If the route is successfully resolved, the path is drawn on screen using *[RenderVisualizer()](../../../api/library/pathfinding/class.pathroute_cpp.md#renderVisualizer_vec4_void)*. The radius parameter is set manually to ensure the generated path accounts for the navigation agent's size, avoiding collisions with nearby geometry.


To demonstrate dynamic behavior, several **Obstacles** are moved using the **Rotator** component, which continuously rotates them during runtime. This setup allows you to observe how the path is recalculated when obstacles shift position and alter the available navigation space.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/navigation/navigation_obstacles_2d*
## Navigation Sectors 2D

This sample demonstrates how to calculate and visualize 2D navigation paths using the **[Navigation Sector](../../../objects/navigations/navigation/navigation_sector/index.md)** objects and *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* class. Unlike navigation meshes, sectors allow defining modular navigable areas that can be enabled, disabled, or moved dynamically at runtime.


This 2D version is well-suited for top-down navigation, grid-based layouts, or layered 2D gameplay. For more complex 3D navigation scenarios, see the sample.


The main logic is implemented in the **PathRoute2D** component, which creates a *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* class instance and uses *[Create2D()](../../../api/library/pathfinding/class.pathroute_cpp.md#create2D_Vec3_Vec3_int_void)* to compute a path through the active navigation sectors. If the route is successfully resolved, the path is drawn on screen using *[RenderVisualizer()](../../../api/library/pathfinding/class.pathroute_cpp.md#renderVisualizer_vec4_void)*. The radius parameter is set manually to ensure the generated path accounts for the agent's size, avoiding collisions with nearby geometry.


To help visualize active navigation areas, the **NavigationSectorVisualizer** component renders the geometry of all sectors during runtime.


Sectors are especially useful when navigation space needs to change at runtime - for example, if parts of the environment become inaccessible. Pathfinding requires sectors to be properly connected (their edges must overlap).


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/navigation/navigation_sectors_2d*
## Navigation Sectors 3D

This sample demonstrates how to calculate and visualize 3D navigation paths using the **[Navigation Sector](../../../objects/navigations/navigation/navigation_sector/index.md)** objects and *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* class via the C# API. Unlike navigation meshes, sectors allow defining modular navigable areas that can be enabled, disabled, or moved dynamically at runtime.


This setup is useful for multilevel structures or modular environments where the layout changes dynamically. For simpler 2D navigation scenarios, see the sample.


The main logic is implemented in the **PathRoute3D** component, which creates a *PathRoute* class instance and uses *[Create3D()](../../../api/library/pathfinding/class.pathroute_cpp.md#create3D_Vec3_Vec3_int_void)* to compute a path through the active navigation sectors. If the route is successfully resolved, the path is drawn on the screen using *[RenderVisualizer()](../../../api/library/pathfinding/class.pathroute_cpp.md#renderVisualizer_vec4_void)*. The radius parameter is set manually to ensure the generated path accounts for the agent's size, avoiding collisions with nearby geometry.


To help visualize active navigation areas, the **NavigationSectorVisualizer** component renders the geometry of all sectors during runtime.


Sectors are especially useful when navigation space needs to change at runtime - for example, if parts of the environment become inaccessible. Pathfinding requires sectors to be properly connected (their edges must overlap).


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/navigation/navigation_sectors_3d*
## Navigation Sectors 3D Demo

This sample demonstrates how to implement 3D pathfinding logic using **[Navigation Sector](../../../objects/navigations/navigation/navigation_sector/index.md)** and *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* class via the C# API. Robots autonomously fly and collect coins, which are dynamically placed at random locations within the navigation sector volume.


The main logic is implemented in the **PathRoute3DWithTarget** component. A *[PathRoute](../../../api/library/pathfinding/class.pathroute_cpp.md)* object is created to calculate a valid 3D path from the robot's current position to the target using *[PathRoute.Create3D()](../../../api/library/pathfinding/class.pathroute_cpp.md#create3D_Vec3_Vec3_int_void)*. Once a valid path is generated, the robot rotates toward the next point in the path and moves forward. If the path becomes invalid - for example, if the target ends up in an unreachable area, then the system selects a new target location and recalculates the route.


Target positions are chosen at random inside the volume of a *Navigation Sector*, using *[Inside3D()](../../../api/library/pathfinding/class.navigation_cpp.md#inside3D_Vec3_float_int)* for validation. The route is automatically updated as the robot approaches the target. If the route is successfully resolved, the path is drawn on screen using *[RenderVisualizer()](../../../api/library/pathfinding/class.pathroute_cpp.md#renderVisualizer_vec4_void)*.


To help visualize active navigation areas, the **NavigationSectorVisualizer** component renders the geometry of all sectors during runtime.


This setup is well-suited for implementing autonomous navigation in 3D volume, where both the moving objects and their targets can change position during runtime within a defined navigable area.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/navigation/navigation_sectors_3d_demo*
