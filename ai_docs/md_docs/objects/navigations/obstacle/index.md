# Obstacles


An **obstacle** is an invisible object which is placed inside a navigation area and is bypassed during pathfinding.


> **Notice:** If you change obstacle transformation, route will be automatically recalculated in order to avoid the obstacle.


The obstacles can be added to the scene:


- *As a single node* to indicate an area or a node that should be avoided during pathfinding. However, if you change transformation of the node, the obstacle transformation won't change.
- *As a child node* of a node that should be bypassed. In this case, transformation of the obstacle will change together with the node transformation and a route will always be calculated correctly.


There are 3 types of the obstacles:


- **[![](box.png)](../../../objects/navigations/obstacle/obstacle_box/index.md) �[Obstacle Box](../../../objects/navigations/obstacle/obstacle_box/index.md)** is a cuboid-shaped obstacle.
- **[![](sphere.png)](../../../objects/navigations/obstacle/obstacle_sphere/index.md) � [Obstacle Sphere](../../../objects/navigations/obstacle/obstacle_sphere/index.md)** is a sphere-shaped obstacle.
- **[![](capsule.png)](../../../objects/navigations/obstacle/obstacle_capsule/index.md) � [Obstacle Capsule](../../../objects/navigations/obstacle/obstacle_capsule/index.md)** is a capsule-shaped obstacle.


You should choose the most appropriate type depending on the form of the node that should be bypassed during pathfinding.


## Usage Example


Supposing, you need to add a node that changes its transformation each frame and should be bypassed during pathfinding. In this case, you should do the following:


1. Place the required node inside the navigation area within which routes will be calculated. [![](add_node_obstacle_sm.png)](add_node_obstacle.png) *A cuboid-shapedObjectMeshDynamicnode placed inside theNavigation Sector*
2. Add the obstacle of the required type to the scene and combine its position with the node's position.
3. Set the required size for the obstacle. ![](add_obstacle.png) *The obstacle box and the node.*
4. In the *[World Hierarchy](../../../editor2/organizing_nodes/index.md)* window, drag the obstacle node to [make it a child](../../../editor2/organizing_nodes/index.md#make_child_node) of the required node. ![](obstacle_child.png) > **Notice:** This will enable to simultaneously change transformation of the node and the obstacle. You can also perform it [via code](../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md#route_nav_obstacle).
5. Now you can [create a route](../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md#route_nav) from the script. The route will be automatically recalculated when the node transformation changes.


In the result, the route will be calculated as follows (the route is highlighted with white):


[![](route_with_obstacle_sm.png)](route_with_obstacle.png)

*The route that bypasses the node marked as the obstacle box*


### See Also


- The example on [Creating a Route within Navigation Area with Obstacles](../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md#route_nav_obstacle) via code.
- [Navigation](../../../sdk/api_samples/cs/navigation.md) samples in *C# Component Samples* suite
