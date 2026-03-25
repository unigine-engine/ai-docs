# Obstacle Box


The **Obstacle Box** node is a cuboid-shaped obstacle that is detected and bypassed by other objects during pathfinding. The *Obstacle Box* can be added, for example:


- For the cuboid-shaped nodes (buildings, old-fashioned cars, fences and so on) that are placed inside a navigation area and should be bypassed
- For the areas (rivers, swimming pools and so on) that should be bypassed


![](box_obstacle_building.png)

*AnObstacle Boxand a building*


### See also


- The *[ObstacleBox](../../../../api/library/pathfinding/class.obstaclebox_cpp.md)* class to manage box obstacles via API
- The *[PathRoute](../../../../api/library/pathfinding/class.pathroute_cpp.md)* class to create 2D and 3D routes among obstacles
- The article on [Creating Routes](../../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md)
- A set of articles on [Navigation Areas](../../../../objects/navigations/navigation/index.md)
- A set of samples located in the `<UnigineSDK>/data/samples/paths` folder:

  - `obstacle_00`
  - `route_01`
  - `route_02`


## Adding Obstacle Box


To add an *Obstacle Box* to the scene via UnigineEditor:


1. [Run](../../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click *Create -> Navigation -> Obstacle Box*. ![](add_box_obstacle.png)
3. Click somewhere in the world to place the obstacle. ![](added_box_obstacle.png)


A new *Obstacle Box* is added to UnigineEditor, and you can edit it via the *[Parameters](../../../../editor2/node_parameters/index.md)* window. See also the [example](../../../../objects/navigations/obstacle/index.md#example) on *Obstacle Box* usage.


## Editing Obstacle Box


In the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the *Obstacle Box*:


![](edit_box_obstacle.png)


| Obstacle Mask | The *Obstacle* mask of the *Obstacle Box* must [match](../../../../principles/bit_masking/index.md) the *Obstacle* mask of the route that is calculated during pathfinding. Otherwise, the obstacle is not taken into account during pathfinding. Also by using the *Obstacle* mask, you can specify *Obstacle Boxes* that should be ignored during pathfinding. |
|---|---|
| Size | Size of the *Obstacle Box* along the axes, in units. |
