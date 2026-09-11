# Unigine::Obstacle Class (CS)

**Inherits from:** Node


This class creates obstacles detected and bypassed during pathfinding.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cs.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## Obstacle Class

### Properties

## int ObstacleMask

The obstacle mask. The obstacle mask of the obstacle box/sphere/capsule must [match](../../../principles/bit_masking/index.md) the obstacle mask of the route that is calculated during pathfinding. Otherwise, the obstacle is not taken into account during pathfinding.
