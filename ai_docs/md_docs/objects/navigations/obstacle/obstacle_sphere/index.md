# Obstacle Sphere


The **Obstacle Sphere** is a sphere-shaped obstacle that is detected and bypassed by other objects during pathfinding. The *Obstacle Sphere* can be added, for example:


- For the sphere-shaped nodes (huge boulders, bushes and so on) that are placed inside a navigation area and should be bypassed
- For the areas (lakes and so on) that should be bypassed


![](sphere_obstacle_bush.png)

*AnObstacle Sphereand a bush*


### See also


- The *[ObstacleSphere](../../../../api/library/pathfinding/class.obstaclesphere_cpp.md)* class to manage sphere-shaped obstacles via API
- The *[PathRoute](../../../../api/library/pathfinding/class.pathroute_cpp.md)* class to create 2D and 3D routes among obstacles
- The article on [Creating Routes](../../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md)
- A set of articles on [Navigation Areas](../../../../objects/navigations/navigation/index.md)
- A set of samples located in the `<UnigineSDK>/data/samples/paths` folder:

  - `obstacle_00`
  - `route_01`
  - `route_02`


## Adding Obstacle Sphere


To add a sphere obstacle to the scene via UnigineEditor:


1. [Run](../../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click *Create -> Navigation -> Obstacle Sphere*. ![](add_sphere_obstacle.png)
3. Click somewhere in the world to place the obstacle. ![](added_sphere_obstacle.png)


A new *Obstacle Sphere* is added to UnigineEditor and you can edit it via the *[Parameters](../../../../editor2/node_parameters/index.md)* window. See also the [example](../../../../objects/navigations/obstacle/index.md#example) on obstacle usage.


## Editing Obstacle Sphere


On the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the *Obstacle Sphere*:


![](edit_sphere_obstacle.png)


| Obstacle Mask | The *Obstacle* mask of the *Obstacle Sphere* must [match](../../../../principles/bit_masking/index.md) the *Obstacle* mask of the route that is calculated during pathfinding. Otherwise, the obstacle is not taken into account during pathfinding. Also by using the *Obstacle* mask, you can specify *Obstacle Spheres* that should be ignored during pathfinding. |
|---|---|
| Radius | Radius of the *Obstacle Sphere*, in units. |
