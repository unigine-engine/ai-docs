# Unigine::ObstacleSphere Class (CPP)

**Header:** #include <UniginePathFinding.h>

**Inherits from:** Obstacle


This class is used to create a [sphere-shaped obstacle](../../../objects/navigations/obstacle/obstacle_sphere/index.md) that is detected and bypassed by other objects during pathfinding.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## ObstacleSphere Class

### Members

## void setRadius ( float radius )

Sets a new radius of the obstacle sphere.
### Arguments

- *float* **radius** - The radius of the sphere. If a negative value is provided, **0** is used instead.

## float getRadius () const

Returns the current radius of the obstacle sphere.
### Return value

Current radius of the sphere. If a negative value is provided, **0** is used instead.
---

## static ObstacleSpherePtr create ( float radius )

Constructor. Creates a new sphere-shaped obstacle of a specified size.
### Arguments

- *float* **radius** - Radius of the sphere.

## static int type ( )

Returns the type of the node.
### Return value

[Obstacle](../../../api/library/pathfinding/class.obstacle_cpp.md) type identifier.
