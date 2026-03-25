# Unigine::ObstacleBox Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Obstacle


This class is used to create a [cuboid-shaped obstacle](../../../objects/navigations/obstacle/obstacle_box/index.md) that is detected and bypassed by other objects during pathfinding.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_usc.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## ObstacleBox Class

### Members

## void setSize ( vec3 size )

Sets a new size of the obstacle box.
### Arguments

- *vec3* **size** - The box dimensions.

## vec3 getSize () const

Returns the current size of the obstacle box.
### Return value

Current box dimensions.
---

## static ObstacleBox ( vec3 arg1 )

Constructor. Creates a new cuboid-shaped obstacle of a specified size.
### Arguments

- *vec3* **arg1** - Box dimensions.

## static int type ( )

Returns the type of the node.
### Return value

[Obstacle](../../../api/library/pathfinding/class.obstacle_usc.md) type identifier.
