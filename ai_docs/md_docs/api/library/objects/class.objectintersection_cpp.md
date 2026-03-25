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

---

## static ObjectIntersectionPtr create ( )

The ObjectIntersection constructor.
## void setIndex ( int index )

Sets the new intersection triangle number.
### Arguments

- *int* **index** - Intersection triangle number.

## int getIndex ( ) const

Returns the number of the intersected triangle.
### Return value

Intersected triangle number.
## void setInstance ( int instance )

Sets the new intersected instance number.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)*


### Arguments

- *int* **instance** - Intersected instance number.

## int getInstance ( ) const

Returns the number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cpp.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cpp.md)*


### Return value

Intersected instance number.
## void setPoint ( const Math:: Vec3 & point )

Sets new coordinates of the intersection point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Coordinates of the intersection point.

## Math:: Vec3 getPoint ( ) const

Returns coordinates of the intersection point.
### Return value

Coordinates of the intersection point.
## ObjectIntersection::TYPE getType ( ) const

Returns the object intersection type identifier.
### Return value

Object [intersection type identifier](#OBJECT_INTERSECTION).
## const char * getTypeName ( ) const

Returns the object intersection type name.
### Return value

Object intersection type name.
