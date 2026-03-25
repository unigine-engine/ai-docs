# Unigine::ObstacleBox Class (CPP)

**Header:** #include <UniginePathFinding.h>

**Inherits from:** Obstacle


This class is used to create a [cuboid-shaped obstacle](../../../objects/navigations/obstacle/obstacle_box/index.md) that is detected and bypassed by other objects during pathfinding.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## ObstacleBox Class

### Members

## void setSize ( const Math:: vec3 & size )

Sets a new size of the obstacle box.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The box dimensions.

## Math:: vec3 getSize () const

Returns the current size of the obstacle box.
### Return value

Current box dimensions.
---

## static ObstacleBoxPtr create ( const Math:: vec3 & arg1 )

Constructor. Creates a new cuboid-shaped obstacle of a specified size.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **arg1** - Box dimensions.

## static int type ( )

Returns the type of the node.
### Return value

[Obstacle](../../../api/library/pathfinding/class.obstacle_cpp.md) type identifier.
