# ObjectIntersection Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to store the result of the object intersection (coordinates of the intersection point, as well as surface and instance indices).


## ObjectIntersection Class

### Members

## void setInstance ( int instance )

Sets a new number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_usc.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_usc.md)*

### Arguments

- *int* **instance** - The number of the intersected instance

## int getInstance () const

Returns the current number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_usc.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_usc.md)*

### Return value

Current number of the intersected instance
## void setIndex ( int index )

Sets a new number of the intersected triangle.
### Arguments

- *int* **index** - The number of the intersected triangle

## int getIndex () const

Returns the current number of the intersected triangle.
### Return value

Current number of the intersected triangle
## void setPoint ( Vec3 point )

Sets a new coordinates of the intersection point.
### Arguments

- *Vec3* **point** - The coordinates of the intersection point

## Vec3 getPoint () const

Returns the current coordinates of the intersection point.
### Return value

Current coordinates of the intersection point
## const char * getTypeName () const

Returns the current object intersection type name.
### Return value

Current object intersection type name
## int getType () const

Returns the current object [intersection type identifier](#OBJECT_INTERSECTION).
### Return value

Current object intersection type identifier
---

## static ObjectIntersection ( )

The ObjectIntersection constructor.
