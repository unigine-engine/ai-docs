# Unigine::NavigationSector Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Navigation


> **Warning:** 3D navigation feature is experimental and not recommended for production use.


This class is used to create a cuboid-shaped navigation area, within which the 2D and 3D routes can be calculated.


#### See Also


- Article on [Navigation Sector](../../../objects/navigations/navigation/navigation_sector/index.md)
- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_usc.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- C++ samples:

  -
  -
- C# samples:

  -
  -
  -
- UnigineScript samples:

  -
  -
  -
  -
  -
  -


## NavigationSector Class

### Members

## void setSize ( vec3 size )

Sets a new size of the navigation sector.
### Arguments

- *vec3* **size** - The box dimensions.

## vec3 getSize () const

Returns the current size of the navigation sector.
### Return value

Current box dimensions.
---

## static NavigationSector ( vec3 arg1 )

Constructor. Creates a navigation sector of the specified size.
### Arguments

- *vec3* **arg1** - Box dimensions.

## static int type ( )

Returns the type of the node.
### Return value

[Navigation](../../../api/library/pathfinding/class.navigation_usc.md) type identifier.
