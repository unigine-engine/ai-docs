# Unigine::PathRouteIntersection Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


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
## void setPoint ( Vec3 point )

Sets a new coordinates of the intersection point.
### Arguments

- *Vec3* **point** - The coordinates of the intersection point.

## Vec3 getPoint () const

Returns the current coordinates of the intersection point.
### Return value

Current coordinates of the intersection point.
---

## static PathRouteIntersection ( )

The PathRouteIntersection constructor.
