# Unigine::Navigation Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


> **Warning:** 3D navigation feature is experimental and not recommended for production use.


This class contains functions that enable to get or change parameters of a navigation area within which pathfinding is performed. The navigation area can be either a [navigation sector](../../../api/library/pathfinding/class.navigationsector_usc.md) or a [navigation mesh](../../../api/library/pathfinding/class.navigationmesh_usc.md).


For example, by using the functions of this class, you can [scale velocity](#setVelocity_float_void) of the point moving inside the navigation area. Or you can change the [danger factor](#setDangerous_float_void) of the area.


#### See Also


- Articles of the [Navigation Area](../../../objects/navigations/navigation/index.md) section
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## Navigation Class

### Members

## void setVelocity ( float velocity )

Sets a new scaling factor for velocity of the point that moves inside the navigation area along the calculated route.
### Arguments

- *float* **velocity** - The velocity scaling factor.

## float getVelocity () const

Returns the current scaling factor for velocity of the point that moves inside the navigation area along the calculated route.
### Return value

Current velocity scaling factor.
## void setQuality ( int quality )

Sets a new quality of optimization of the route that has already been calculated. the quality value specifies the number of iterations that are used for taking the shortcut.
### Arguments

- *int* **quality** - The quality value. If a negative value is provided, 0 is used instead.

## int getQuality () const

Returns the current quality of optimization of the route that has already been calculated. the quality value specifies the number of iterations that are used for taking the shortcut.
### Return value

Current quality value. If a negative value is provided, 0 is used instead.
## int getNumNavigations () const

Returns the current number of navigation areas that intersect the current one.
### Return value

Current number of connected navigation areas.
## void setNavigationMask ( int mask )

Sets a new navigation mask of the navigation area. the navigation mask of the navigation area must [match](../../../principles/bit_masking/index.md) the [navigation mask](../../../api/library/pathfinding/class.pathroute_usc.md#setNavigationMask_int_void) of the route that is calculated within it. Otherwise, the area will not participate in pathfinding.
### Arguments

- *int* **mask** - The integer value each bit of which is used to set a mask.

## int getNavigationMask () const

Returns the current navigation mask of the navigation area. the navigation mask of the navigation area must [match](../../../principles/bit_masking/index.md) the [navigation mask](../../../api/library/pathfinding/class.pathroute_usc.md#setNavigationMask_int_void) of the route that is calculated within it. Otherwise, the area will not participate in pathfinding.
### Return value

Current integer value each bit of which is used to set a mask.
## void setDangerous ( float dangerous )

Sets a new danger factor that indicates if the point that moves inside the navigation area should try to avoid this area.
> **Notice:** If the danger factor exceeds the [maximum danger factor](../../../api/library/pathfinding/class.pathroute_usc.md#setMaxDangerous_float_void) set for the route, the navigation area will be excluded from pathfinding calculations.


### Arguments

- *float* **dangerous** - The danger factor.

## float getDangerous () const

Returns the current danger factor that indicates if the point that moves inside the navigation area should try to avoid this area.
> **Notice:** If the danger factor exceeds the [maximum danger factor](../../../api/library/pathfinding/class.pathroute_usc.md#setMaxDangerous_float_void) set for the route, the navigation area will be excluded from pathfinding calculations.


### Return value

Current danger factor.
---

## Navigation getNavigation ( int num )

Returns the specified connected navigation area.
### Arguments

- *int* **num** - The navigation area number.

### Return value

The navigation area.
## int inside ( Navigation navigation )

Returns a value indicating if the specified Navigation area is a part of the Navigation area.
### Arguments

- *[Navigation](../../../api/library/pathfinding/class.navigation_usc.md)* **navigation** - Navigation area

## int inside2D ( Vec3 point , float radius )


Depending on the type of the navigation area, the function performs the following:


- For *navigation sectors*, it checks whether the given point is inside the navigation sector.  The height of the navigation sector (Z coordinate) is ignored.
- For *navigation meshes*, it checks whether the given point is inside the navigation mesh and the distance from the point to the mesh is in range [-height;height]. Here height is a height of the navigation mesh.


### Arguments

- *Vec3* **point** - Point coordinates.
- *float* **radius** - The radius of the point. The radius is used to exclude exceeding the navigation mesh by the point. If the radius is set, it is more likely that the point will be inside the navigation mesh. > **Notice:** When calling the function for [NavigationSector](../../../api/library/pathfinding/class.navigationsector_usc.md), this option is irrelevant.

### Return value

**1** if the point is inside the navigation area; otherwise, **0**.
## int inside3D ( Vec3 point , float radius )


Depending on the type of the navigation area, the function performs the following:


- For *navigation sectors*, it checks whether the given point is inside the navigation area.  Notice that the height of the navigation sector (Z coordinate) is also taken into account.
- For *navigation meshes*, it checks whether the given point is inside the navigation mesh and the distance from the point to the mesh is in range [0;height]. Here height is a height of the navigation mesh.


### Arguments

- *Vec3* **point** - Point coordinates.
- *float* **radius** - The radius of the point. The radius is used to exclude exceeding the navigation mesh by the point. If the radius is set, it is more likely that the point will be inside the navigation mesh. > **Notice:** When calling the function for [NavigationSector](../../../api/library/pathfinding/class.navigationsector_usc.md), this option is irrelevant.

### Return value

**1** it the point is inside the navigation area; otherwise, **0**.
