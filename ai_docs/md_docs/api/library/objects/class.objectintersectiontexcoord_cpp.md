# ObjectIntersectionTexCoord Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** ObjectIntersectionNormal


This class is used to store the texture coordinates of the object intersection.


## ObjectIntersectionTexCoord Class

### Members

## void setTexCoord ( const Math:: vec4 & coord )

Sets a new texture coordinates of the intersection point (where vec4.xy is for the first UV channel, vec4.zw is for the second UV channel).
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **coord** - The texture coordinates of the intersection point

## Math:: vec4 getTexCoord () const

Returns the current texture coordinates of the intersection point (where vec4.xy is for the first UV channel, vec4.zw is for the second UV channel).
### Return value

Current texture coordinates of the intersection point
---

## static ObjectIntersectionTexCoordPtr create ( )

The ObjectIntersectionTexCoord constructor.
