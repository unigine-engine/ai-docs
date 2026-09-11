# ObjectIntersection Class (CPP)

**Header:** #include <UnigineObjects.h>


This class is used to store the result of the object intersection (coordinates of the intersection point, as well as surface and instance indices).


## ObjectIntersection Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **OBJECT_INTERSECTION** = 0 | [ObjectIntersection](../../../api/library/objects/class.objectintersection_cpp.md) (stores only the point of intersection, surface and triangle indices). |
| **OBJECT_INTERSECTION_NORMAL** = 1 | [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cpp.md) (stores the point of intersection, surface and triangle indices + normal coordinates at the point of intersection). |
| **OBJECT_INTERSECTION_TEX_COORD** = 2 | [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cpp.md) (stores the point of intersection, surface and triangle indices + normal and texture coordinates at the point of intersection). |
| **NUM_OBJECT_INTERSECTIONS** = 3 | Number of object intersection types. |

### Members

## void setInstance ( int instance )

Sets a new number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)*

### Arguments

- *int* **instance** - The number of the intersected instance

## int getInstance () const

Returns the current number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)*

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
## void setPoint ( const Math:: Vec3 & point )

Sets a new coordinates of the intersection point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **point** - The coordinates of the intersection point

## Math:: Vec3 getPoint () const

Returns the current coordinates of the intersection point.
### Return value

Current coordinates of the intersection point
## const char * getTypeName () const

Returns the current object intersection type name.
### Return value

Current object intersection type name
## ObjectIntersection::TYPE getType () const

Returns the current object [intersection type identifier](#OBJECT_INTERSECTION).
### Return value

Current object intersection type identifier
---

## static ObjectIntersectionPtr create ( )

The ObjectIntersection constructor.
