# ObjectIntersection Class (CS)


This class is used to store the result of the object intersection (coordinates of the intersection point, as well as surface and instance indices).


## ObjectIntersection Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **OBJECT_INTERSECTION** = 0 | [ObjectIntersection](../../../api/library/objects/class.objectintersection_cs.md) (stores only the point of intersection, surface and triangle indices). |
| **OBJECT_INTERSECTION_NORMAL** = 1 | [ObjectIntersectionNormal](../../../api/library/objects/class.objectintersectionnormal_cs.md) (stores the point of intersection, surface and triangle indices + normal coordinates at the point of intersection). |
| **OBJECT_INTERSECTION_TEX_COORD** = 2 | [ObjectIntersectionTexCoord](../../../api/library/objects/class.objectintersectiontexcoord_cs.md) (stores the point of intersection, surface and triangle indices + normal and texture coordinates at the point of intersection). |
| **NUM_OBJECT_INTERSECTIONS** = 3 | Number of object intersection types. |

### Properties

## int Instance

The number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cs.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_cs.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_cs.md)*

## int Index

The number of the intersected triangle.
## vec3 Point

The coordinates of the intersection point.
## 🔒︎ string TypeName

The object intersection type name.
## 🔒︎ ObjectIntersection.TYPE Type

The object [intersection type identifier](#OBJECT_INTERSECTION).
### Members

---

## ObjectIntersection ( )

The ObjectIntersection constructor.
