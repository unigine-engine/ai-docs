# Unigine::PathRouteIntersection Class (CPP)

**Header:** #include <UniginePathFinding.h>


## PathRouteIntersection Class

### Members

## void setIndex ( int index )

Sets a new index of the intersected triangle.
### Arguments

- *int* **index** - The index of the intersected triangle.

## int getIndex () const

Returns the current index of the intersected triangle.
### Return value

Current index of the intersected triangle.
## void setPoint ( const Math:: Vec3 & point )

Sets a new coordinates of the intersection point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **point** - The coordinates of the intersection point.

## Math:: Vec3 getPoint () const

Returns the current coordinates of the intersection point.
### Return value

Current coordinates of the intersection point.
---

## static PathRouteIntersectionPtr create ( )

The PathRouteIntersection constructor.
