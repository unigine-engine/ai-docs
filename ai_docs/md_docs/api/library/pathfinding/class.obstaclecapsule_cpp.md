# Unigine::ObstacleCapsule Class (CPP)

**Header:** #include <UniginePathFinding.h>

**Inherits from:** Obstacle


This class is used to create a [capsule-shaped obstacle](../../../objects/navigations/obstacle/obstacle_capsule/index.md) that is detected and bypassed by other objects during pathfinding.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## ObstacleCapsule Class

### Members

## void setRadius ( float radius )

Sets a new radius of the obstacle capsule.
### Arguments

- *float* **radius** - The radius of the capsule. If a negative value is provided, **0** is used instead.

## float getRadius () const

Returns the current radius of the obstacle capsule.
### Return value

Current radius of the capsule. If a negative value is provided, **0** is used instead.
## void setHeight ( float height )

Sets a new height of the obstacle capsule.
### Arguments

- *float* **height** - The height of the capsule. If a negative value is provided, **0** is used instead.

## float getHeight () const

Returns the current height of the obstacle capsule.
### Return value

Current height of the capsule. If a negative value is provided, **0** is used instead.
---

## static ObstacleCapsulePtr create ( float radius , float height )

Constructor. Creates a new capsule-shaped obstacle of a specified size.
### Arguments

- *float* **radius** - Radius of the capsule.
- *float* **height** - Height of the capsule.

## static int type ( )

Returns the type of the node.
### Return value

[Obstacle](../../../api/library/pathfinding/class.obstacle_cpp.md) type identifier.
