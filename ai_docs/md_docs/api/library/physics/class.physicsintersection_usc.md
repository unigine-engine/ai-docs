# Unigine::PhysicsIntersection Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class stores the result of the physics intersection (coordinates of the intersection, the shape of the object, the index of the surface). If you need information on the normal at the intersection point, use the *[PhysicsIntersectionNormal](../../../api/library/physics/class.physicsintersectionnormal_usc.md)* class.


#### Usage Example


The following example shows how you can get the intersection information by using the *PhysicsIntersection* class. In this example we specify a line from the point of the camera *(vec3 p0)* to the point of the mouse pointer *(vec3 p1)*. The execution sequence is the following:


1. Define and initialize two points (p0 and p1) by using the *getPlayerMouseDirection()* function from `core/scripts/utils.h`.
2. Create an instance of the *PhysicsIntersection* class to get the intersection information.
3. Check if there is a intersection with an object.
4. When the object intersects with the traced line, all surfaces of the intersected object change their material parameters. If the object has a shape, its information will be shown in console. The *PhysicsIntersection* class instance gets the coordinates of the intersection point, the index of the surface and the *Shape* class object. You can get all these fields by using *[getShape()](#getShape_Shape), [getPoint()](#getPoint_Vec3)* and *[getSurface()](#getSurface_int)* functions.


```cpp
#include <core/scripts/utils.h>
/* ... */
int update {
	// define two vec3 coordinates
	vec3 p0,p1;
	// get the mouse direction from camera (p0) to the cursor pointer (p1)
	Unigine::getPlayerMouseDirection(p0,p1);

	// create the instance of the PhysicsIntersection object to save the result
	PhysicsIntersection intersection = new PhysicsIntersection();
	// create an instance for intersected object and check the intersection
	Object object = engine.physics.getIntersection(p0,p1,1,intersection);

	// if the intersection has been occurred, change the parameter of the object's material
	if(object != NULL)
	{
		forloop(int i=0; object.getNumSurfaces())
		{
			object.setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f),i);
		}

		// if the intersected object has a shape, show the information about the intersection
		Shape shape = intersection.getShape();
		if (shape != NULL)
		{
			log.message("physics intersection info: point: %s shape: %s surface: %i \n", typeinfo(intersection.getPoint()), typeinfo(shape.getType()), intersection.getSurface());
		}
	}
	return 1;
}
/* ... */

```


## PhysicsIntersection Class

### Members

## void setSurface ( int surface )

Sets a new intersected surface number.
### Arguments

- *int* **surface** - The intersected surface number

## int getSurface () const

Returns the current intersected surface number.
### Return value

Current intersected surface number
## void setPoint ( Vec3 point )

Sets a new coordinates of the intersection point.
### Arguments

- *Vec3* **point** - The coordinates of the intersection point

## Vec3 getPoint () const

Returns the current coordinates of the intersection point.
### Return value

Current coordinates of the intersection point
## void setShape ( Shape shape )

Sets a new intersected shape.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape** - The intersected shape

## Shape getShape () const

Returns the current intersected shape.
### Return value

Current intersected shape
## const char * getTypeName () const

Returns the current name of the intersection object type.
### Return value

Current name of the intersection object type
## int getType () const

Returns the current intersection object type, one of the [PHYSICS_INTERSECTION*](#PHYSICS_INTERSECTION) values.
### Return value

Current intersection object type
---

## static PhysicsIntersection ( )

The PhysicsIntersection constructor.
