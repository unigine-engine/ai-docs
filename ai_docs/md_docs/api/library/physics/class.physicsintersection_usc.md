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

---

## static PhysicsIntersection ( )

The PhysicsIntersection constructor.
## void setPoint ( Vec3 point )

Sets new coordinates of the intersection point.
### Arguments

- *Vec3* **point** - Coordinates of the intersection point.

## Vec3 getPoint ( )

Returns coordinates of the intersection point.
### Return value

Coordinates of the intersection point.
## void setShape ( Shape shape )

Sets the new intersection shape.
### Arguments

- *[Shape](../../../api/library/physics/class.shape_usc.md)* **shape** - Intersection shape.

## Shape getShape ( )

Returns the intersection shape.
### Return value

Intersection shape.
## void setSurface ( int surface )

Sets the new intersection surface number.
### Arguments

- *int* **surface** - Intersection surface number.

## int getSurface ( )

Returns the intersected surface number.
### Return value

Intersected surface number.
## int getType ( )

Returns the type of physics intersection. The type defines information stored by the object (if the data on the normal at the intersection point is included or not).
### Return value

Physics intersection type, one of the [PHYSICS_INTERSECTION_*](#PHYSICS_INTERSECTION) values.
## string getTypeName ( )

Returns the name of the physics intersection type. The type defines information stored by the object (if the data on the normal at the intersection point is included or not).
### Return value

Name of the physics intersection type. One of the following values:
- PhysicsIntersection
- PhysicsIntersectionNormal
