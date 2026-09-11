# ObjectIntersectionTexCoord Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** ObjectIntersectionNormal


This class is used to store the texture coordinates of the object intersection.


## ObjectIntersectionTexCoord Class

### Members

## void setTexCoord ( vec4 coord )

Sets a new texture coordinates of the intersection point (where vec4.xy is for the first UV channel, vec4.zw is for the second UV channel).
### Arguments

- *vec4* **coord** - The texture coordinates of the intersection point

## vec4 getTexCoord () const

Returns the current texture coordinates of the intersection point (where vec4.xy is for the first UV channel, vec4.zw is for the second UV channel).
### Return value

Current texture coordinates of the intersection point
---

## static ObjectIntersectionTexCoord ( )

The ObjectIntersectionTexCoord constructor.
