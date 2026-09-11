# ObjectIntersectionNormal Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** ObjectIntersection


This class is used to store the normal of the object intersection point.


## ObjectIntersectionNormal Class

### Members

## void setNormal ( const Math:: vec3 & normal )

Sets a new normal of the intersection point.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **normal** - The normal of the intersection point

## Math:: vec3 getNormal () const

Returns the current normal of the intersection point.
### Return value

Current normal of the intersection point
---

## static ObjectIntersectionNormalPtr create ( )

The ObjectIntersectionNormal constructor.
