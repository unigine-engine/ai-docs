# Unigine::NavigationSector Class (CPP)

**Header:** #include <UniginePathFinding.h>

**Inherits from:** Navigation


> **Warning:** 3D navigation feature is experimental and not recommended for production use.


This class is used to create a cuboid-shaped navigation area, within which the 2D and 3D routes can be calculated.


#### See Also


- Article on [Navigation Sector](../../../objects/navigations/navigation/navigation_sector/index.md)
- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md) usage example demonstrating how to create routes and recalculate them considering obstacles
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

## void setSize ( const Math:: vec3 & size )

Sets a new size of the navigation sector.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The box dimensions.

## Math:: vec3 getSize () const

Returns the current size of the navigation sector.
### Return value

Current box dimensions.
---

## static NavigationSectorPtr create ( const Math:: vec3 & arg1 )

Constructor. Creates a navigation sector of the specified size.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **arg1** - Box dimensions.

## static int type ( )

Returns the type of the node.
### Return value

[Navigation](../../../api/library/pathfinding/class.navigation_cpp.md) type identifier.
