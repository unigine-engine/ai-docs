# Unigine::WorldIntersection Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class stores the result of the world intersection (the coordinates of the intersection, the index of the intersected triangle and the index of the intersected surface).


#### Usage Example


The following example shows how you can get the intersection information by using the *WorldIntersection* class. In this example, the line is an invisible traced line from the point of the camera (*vec3 **p0***) to the point of the mouse pointer (*vec3 **p1***). The executing sequence is the following:


- Define and initialize two points (p0 and p1) by using the *getPlayerMouseDirection()* function from `core/scripts/utils.h`.
- Create an instance of the *WorldIntersection* class to get the intersection information.
- Check, if there is a intersection with an object. The [*engine.world.getIntersection()*](../../../api/library/engine/class.world_usc.md#getIntersection_vec3_vec3_int_Variable_Object) function returns an intersected object when the object intersects with the traced line.
- In this example, when the object intersects with the traced line, all the surfaces of the intersected object change their material parameters. The *WorldIntersection* class instance gets the coordinates of the intersection point, the index of the surface and the index of the intersected triangle. You can get all these fields by using [*getIndex()*](#getIndex_int), [*getPoint()*](#getPoint_Vec3) and [*getSurface()*](#getSurface_int) functions


```cpp
#include <core/scripts/utils.h>
/* ... */
// define two vec3 coordinates
vec3 p0,p1;
// get the mouse direction from camera (p0) to cursor pointer (p1)
getPlayerMouseDirection(p0,p1);

// create an instance of the WorldIntersection class to get the result
WorldIntersection intersection = new WorldIntersection();

// create an instance for intersected object and check the intersection
Object object = engine.world.getIntersection(p0,p1,1,intersection);

// if the intersection has been occurred, change the parameter of the object's material
if(object != NULL)
{
  forloop(int i=0; object.getNumSurfaces())
  {
    object.setMaterialParameterFloat4("diffuse_color", vec4(1.0f, 0.0f, 0.0f, 1.0f),i);
    object.setMaterialTexture("diffuse","", i);

    // show intersection details in console
    log.message("point: %s index: %i surface: %i \n", typeinfo(intersection.getPoint()), intersection.getIndex(), intersection.getSurface());
  }

}
/* ... */

```


## WorldIntersection Class

### Members

## void setSurface ( int surface )

Sets a new intersected surface number.
### Arguments

- *int* **surface** - The intersected surface number.

## int getSurface () const

Returns the current intersected surface number.
### Return value

Current intersected surface number.
## void setInstance ( int instance )

Sets a new number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
>
>
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_usc.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_usc.md)*


### Arguments

- *int* **instance** - The intersected instance number.

## int getInstance () const

Returns the current number of the intersected instance.
> **Notice:** Intersected instance number can be obtained for the following classes:
>
>
> - *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_usc.md)*
> - *[ObjectMeshCluster](../../../api/library/objects/class.objectmeshcluster_usc.md)*
> - *[ObjectMeshSplineCluster](../../../api/library/objects/class.objectmeshsplinecluster_usc.md)*


### Return value

Current intersected instance number.
## void setIndex ( int index )

Sets a new number of the intersected triangle.
### Arguments

- *int* **index** - The number of the intersected triangle.

## int getIndex () const

Returns the current number of the intersected triangle.
### Return value

Current number of the intersected triangle.
## void setPoint ( Vec3 point )

Sets a new coordinates of the intersection point.
### Arguments

- *Vec3* **point** - The coordinates of the intersection point.

## Vec3 getPoint () const

Returns the current coordinates of the intersection point.
### Return value

Current coordinates of the intersection point.
## const char * getTypeName () const

Returns the current *World Intersection* type name.
### Return value

Current *World Intersection* type name.
## int getType () const

Returns the current [*World Intersection* type identifier](#WORLD_INTERSECTION).
### Return value

Current *World Intersection* type identifier.
---

## static WorldIntersection ( )

The WorldIntersection constructor.
