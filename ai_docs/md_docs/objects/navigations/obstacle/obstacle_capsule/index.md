# Obstacle Capsule


The **Obstacle Capsule** is a capsule-shaped obstacle that is detected and bypassed by other objects during pathfinding. The *Obstacle Capsule* can be added, for example, for the capsule-shaped nodes (trunks, columns, chimney shafts and so on) that are placed inside a navigation area and should be bypassed.


![](capsule_obstacle_fur.png)

*AnObstacle Capsuleand a fur*


The size of the *Obstacle Capsule* is set using the following parameters:


- **Radius** � the radius of the cylinder and hemispheres of the capsule.
- **Height** � the height of the cylinder of the capsule.


### See also


- The *[ObstacleCapsule](../../../../api/library/pathfinding/class.obstaclecapsule_cpp.md)* class to manage capsule obstacles via API
- The *[PathRoute](../../../../api/library/pathfinding/class.pathroute_cpp.md)* class to create 2D and 3D routes among obstacles
- The article on [Creating Routes](../../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md)
- A set of articles on [Navigation Areas](../../../../objects/navigations/navigation/index.md)
- A set of samples located in the `data/samples/paths` folder:

  - `obstacle_00`
  - `route_01`
  - `route_02`


## Adding Obstacle Capsule


To add an *Obstacle Capsule* to the scene via UnigineEditor:


1. [Run](../../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click *Create -> Navigation -> Obstacle Capsule*. ![](add_capsule_obstacle.png)
3. Click somewhere in the world to place the obstacle. ![](added_capsule_obstacle.png)


A new *Obstacle Capsule* is added to UnigineEditor and you can edit it via the *[Parameters](../../../../editor2/node_parameters/index.md)* window. See also the [example](../../../../objects/navigations/obstacle/index.md#example) on obstacle usage.


## Editing Obstacle Capsule


On the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the *Obstacle Capsule*:


![](edit_capsule_obstacle.png)


| Obstacle Mask | The *Obstacle* mask of the *Obstacle Capsule* must [match](../../../../principles/bit_masking/index.md) the *Obstacle* mask of the route that is calculated during pathfinding. Otherwise, the obstacle is not taken into account during pathfinding. Also by using the *Obstacle* mask, you can specify *Obstacle Capsule* that should be ignored during pathfinding. |
|---|---|
| Radius | Radius of the capsule, in units. |
| Height | Height of the capsule, in units. |
