# Unigine::WorldIntersectionTexCoord Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WorldIntersectionNormal


This class stores the texture coordinates of the intersection point. You should use this class when you need additional information about the texture coordinates at the intersection point (it also stores the coordinates of the intersection, the index of the intersected triangle, the index of the intersected surface, and normal coordinates at the intersection point).


#### Usage Example


The following example shows how you can get texture coordinates at the intersection point (vec4) by using the *WorldIntersectionTexCoord* class. In this example the line is an invisible traced line from the point of the camera (*vec3 **p0***) to the point of the mouse pointer (*vec3 **p1***). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *getPlayerMouseDirection()* function from `core/scripts/utils.h`.
- Create an instance of the *WorldIntersectionTexCoord* class to get the intersection information.
- Check, if there is a intersection with an object. The [*engine.world.getIntersection()*](../../../api/library/engine/class.world_usc.md#getIntersection_vec3_vec3_int_Variable_Object) function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *WorldIntersectionTexCoord* class instance gets the texture coordinates of the intersection point. You can get the texture coordinates by using the [*getTexCoord()*](#getTexCoord_vec4) function


```cpp
#include <core/scripts/utils.h>
/* ... */
// define two vec3 coordinates
vec3 p0,p1;
// get the mouse direction from camera (p0) to cursor pointer (p1)
getPlayerMouseDirection(p0,p1);

// create an instance of the WorldIntersectionTexCoord class to get the result
WorldIntersection intersection = new WorldIntersection();

// create an instance for intersected object and check the intersection
Object object = engine.world.getIntersection(p0,p1,1,intersection);

// if the intersection has been occurred, change the parameter and the texture of the object's material
if(object != NULL)
{
  forloop(int i=0; object.getNumSurfaces())
  {
  object.setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f),i);
  }
  // show the texture coordinates in console
  log.message("Texture coordinates: (%f %f %f %f)\n",
		intersection.getTexCoord().x,
		intersection.getTexCoord().y,
		intersection.getTexCoord().z,
		intersection.getTexCoord().w);
}
/* ... */

```


## WorldIntersectionTexCoord Class

### Members

## void setTexCoord ( vec4 coord )

Sets a new texture coordinates of the intersection point.
### Arguments

- *vec4* **coord** - The texture coordinates of the intersection point.

## vec4 getTexCoord () const

Returns the current texture coordinates of the intersection point.
### Return value

Current texture coordinates of the intersection point.
---

## static WorldIntersectionTexCoord ( )

The WorldIntersectionTexCoord constructor.
