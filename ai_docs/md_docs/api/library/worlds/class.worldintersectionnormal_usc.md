# Unigine::WorldIntersectionNormal Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WorldIntersection


This class stores the normal at the intersection point. You should use this class when you need additional information about the normal at the intersection point (it also stores the coordinates of the intersection, the index of the intersected triangle, and the index of the intersected surface).


#### Usage Example


The following example shows how you can get the intersection normal (*vec3*) by using the WorldIntersectionNormal class. In this example the line is an invisible traced line from the point of the camera (*vec3 **p0***) to the point of the mouse pointer (*vec3 **p1***). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *getPlayerMouseDirection()* function from `core/scripts/utils.h`.
- Create an instance of the WorldIntersectionNormal class to get the intersection information.
- Check, if there is a intersection with an object. The *[engine.world.getIntersection()](../../../api/library/engine/class.world_usc.md#getIntersection_vec3_vec3_int_Variable_Object)* function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *WorldIntersectionNormal* class instance gets the normal of the intersection point. You can get the normal by using the [*getNormal()*](#getNormal_vec3) function.


```cpp
#include <core/scripts/utils.h>
/* ... */
// define two vec3 coordinates
vec3 p0,p1;
// get the mouse direction from camera (p0) to cursor pointer (p1)
getPlayerMouseDirection(p0,p1);

// create an instance of the WorldIntersectionNormal class to get the result
WorldIntersectionNormal intersection = new WorldIntersectionNormal();

// create an instance for intersected object and check the intersection
Object object = engine.world.getIntersection(p0,p1,1,intersection);

// if the intersection has been occurred, change the parameter of the object's material
if(object != NULL)
{
  forloop(int i=0; object.getNumSurfaces())
  {
  object.setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f),i);
  }
  // show the normal in console
  log.message("normal: %s \n", typeinfo(intersection.getNormal()));
}
/* ... */

```


## WorldIntersectionNormal Class

### Members

## void setNormal ( vec3 normal )

Sets a new normal at the intersection point.
### Arguments

- *vec3* **normal** - The normal at the intersection point.

## vec3 getNormal () const

Returns the current normal at the intersection point.
### Return value

Current normal at the intersection point.
---

## static WorldIntersectionNormal ( )

The WorldIntersectionNormal constructor.
