# Unigine::NavigationSector Class (CS)

**Inherits from:** Navigation


> **Warning:** 3D navigation feature is experimental and not recommended for production use.


This class is used to create a cuboid-shaped navigation area, within which the 2D and 3D routes can be calculated.


#### See Also


- Article on [Navigation Sector](../../../objects/navigations/navigation/navigation_sector/index.md)
- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cs.md) usage example demonstrating how to create routes and recalculate them considering obstacles
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

### Properties

## vec3 Size

The size of the navigation sector.
### Members

---

## NavigationSector ( vec3 arg1 )

Constructor. Creates a navigation sector of the specified size.
### Arguments

- *vec3* **arg1** - Box dimensions.

## static int type ( )

Returns the type of the node.
### Return value

[Navigation](../../../api/library/pathfinding/class.navigation_cs.md) type identifier.
