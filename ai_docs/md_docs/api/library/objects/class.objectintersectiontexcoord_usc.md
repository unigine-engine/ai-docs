# ObjectIntersectionTexCoord Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** ObjectIntersectionNormal


This class is used to store the texture coordinates of the object intersection.


## ObjectIntersectionTexCoord Class

### Members

---

## static ObjectIntersectionTexCoord ( )

The ObjectIntersectionTexCoord constructor.
## void setTexCoord ( vec4 coord )

Sets new texture coordinates of the intersection point.
### Arguments

- *vec4* **coord** - Texture coordinates of the intersection point.

## vec4 getTexCoord ( )

Returns texture coordinates of the intersection point.
### Return value

Texture coordinates of the intersection point (where vec4.xy is for the first UV channel, vec4.zw is for the second UV channel).
