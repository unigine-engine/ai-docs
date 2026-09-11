# Unigine::Obstacle Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class creates obstacles detected and bypassed during pathfinding.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_usc.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## Obstacle Class

### Members

## void setObstacleMask ( int mask )

Sets a new obstacle mask. The obstacle mask of the obstacle box/sphere/capsule must [match](../../../principles/bit_masking/index.md) the obstacle mask of the route that is calculated during pathfinding. Otherwise, the obstacle is not taken into account during pathfinding.
### Arguments

- *int* **mask** - The integer value each bit of which is used to set a mask.

## int getObstacleMask () const

Returns the current obstacle mask. The obstacle mask of the obstacle box/sphere/capsule must [match](../../../principles/bit_masking/index.md) the obstacle mask of the route that is calculated during pathfinding. Otherwise, the obstacle is not taken into account during pathfinding.
### Return value

Current integer value each bit of which is used to set a mask.
