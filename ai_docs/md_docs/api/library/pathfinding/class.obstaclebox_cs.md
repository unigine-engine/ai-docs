# Unigine::ObstacleBox Class (CS)

**Inherits from:** Obstacle


This class is used to create a [cuboid-shaped obstacle](../../../objects/navigations/obstacle/obstacle_box/index.md) that is detected and bypassed by other objects during pathfinding.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cs.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## ObstacleBox Class

### Properties

## vec3 Size

The size of the obstacle box.
### Members

---

## ObstacleBox ( vec3 arg1 )

Constructor. Creates a new cuboid-shaped obstacle of a specified size.
### Arguments

- *vec3* **arg1** - Box dimensions.

## static int type ( )

Returns the type of the node.
### Return value

[Obstacle](../../../api/library/pathfinding/class.obstacle_cs.md) type identifier.
