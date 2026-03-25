# Unigine::ObstacleSphere Class (CS)

**Inherits from:** Obstacle


This class is used to create a [sphere-shaped obstacle](../../../objects/navigations/obstacle/obstacle_sphere/index.md) that is detected and bypassed by other objects during pathfinding.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cs.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## ObstacleSphere Class

### Properties

## float Radius

The radius of the obstacle sphere.
### Members

---

## ObstacleSphere ( float radius )

Constructor. Creates a new sphere-shaped obstacle of a specified size.
### Arguments

- *float* **radius** - Radius of the sphere.

## static int type ( )

Returns the type of the node.
### Return value

[Obstacle](../../../api/library/pathfinding/class.obstacle_cs.md) type identifier.
