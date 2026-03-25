# ObjectIntersection Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to store the result of the object intersection (coordinates of the intersection point, as well as surface and instance indices).


## ObjectIntersection Class

### Members

---

## static ObjectIntersection ( )

The ObjectIntersection constructor.
## void setIndex ( int index )

Sets the new intersection triangle number.
### Arguments

- *int* **index** - Intersection triangle number.

## int getIndex ( )

Returns the number of the intersected triangle.
### Return value

Intersected triangle number.
## void setInstance ( int instance )

Sets the new intersected instance number.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_usc.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_usc.md)*


### Arguments

- *int* **instance** - Intersected instance number.

## int getInstance ( )

Returns the number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_usc.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_usc.md)*


### Return value

Intersected instance number.
## void setPoint ( Vec3 point )

Sets new coordinates of the intersection point.
### Arguments

- *Vec3* **point** - Coordinates of the intersection point.

## Vec3 getPoint ( )

Returns coordinates of the intersection point.
### Return value

Coordinates of the intersection point.
## int getType ( )

Returns the object intersection type identifier.
### Return value

Object [intersection type identifier](#OBJECT_INTERSECTION).
## string getTypeName ( )

Returns the object intersection type name.
### Return value

Object intersection type name.
