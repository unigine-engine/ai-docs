# ObjectIntersectionNormal Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** ObjectIntersection


This class is used to store the normal of the object intersection point.


## ObjectIntersectionNormal Class

### Members

## void setNormal ( vec3 normal )

Sets a new normal of the intersection point.
### Arguments

- *vec3* **normal** - The normal of the intersection point

## vec3 getNormal () const

Returns the current normal of the intersection point.
### Return value

Current normal of the intersection point
---

## static ObjectIntersectionNormal ( )

The ObjectIntersectionNormal constructor.
