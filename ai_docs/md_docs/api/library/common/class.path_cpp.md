# Unigine::Path Class (CPP)

**Header:** #include <UniginePath.h>


Interface for path loading, manipulating and saving.


The **path** is a spline along which an object can be moved. Such splines can be created, for example, in 3ds Max and then exported to a `*.path` file. Or, they can be created in the code by means of the *Path* class and then saved to the `*.path` file.


> **Warning:** There is no connection between functions of the *Path* class and pathfinding-related functions.


### Creating Simple Path from Code


As previously stated, the `*.path` asset can be created using the code. In general, the implementation includes the following steps:


- Create a new instance of the *Path* class.
- Add points to the path.
- Save the calculated path to the `*.path` file.


The following code creates a simple path between two control points and saves it to the `*.path` file.


```cpp
#include "AppWorldLogic.h"
#include <UniginePath.h>

using namespace Unigine;
using namespace Math;

AppWorldLogic::AppWorldLogic()
{}

AppWorldLogic::~AppWorldLogic()
{}

int AppWorldLogic::init()
{
	// specify control points
	Vector<Vec3> points;
	points.append({ 0.0, 0.0, 0.0 });
	points.append({ 10.0, 0.0, 0.0 });
	points.append({ 10.0, 10.0, 0.0 });
	points.append({ 0.0, 10.0, 0.0 });

	// create a new path
	PathPtr path = Path::create();

	// add the points to the path
	for (int i = 0; i < points.size(); i++)
	{
		path->addFrame();
		path->setFramePosition(i, points[i]);
		// normalized time of passing the point (0 - path start, 1 - path end)
		float t = (float)i/(points.size()-1);
		path->setFrameTime(i, t);
	}

	// save the path
	path->save("test_path.path");

	return 1;
}


```


> **Notice:** For simplicity in the example, we pass a point index as the second argument to the *[setFrameTime()](#setFrameTime_int_float_void)* method, so that it would take one second to pass the point.


## Path Class

### Members

## void setNumFrames ( int frames )

Sets a new number of the path frames.
### Arguments

- *int* **frames** - The number of the path frames.

## int getNumFrames () const

Returns the current number of the path frames.
### Return value

Current number of the path frames.
---

## static PathPtr create ( )

Constructor. Creates an empty path.
## static PathPtr create ( const char * name )

Constructor. Creates an empty path of the specified name.
### Arguments

- *const char ** **name** - Name of the path.

## static PathPtr create ( const Ptr < Path > & path )

Constructor. Creates a path out of the specified path.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Path](../../../api/library/common/class.path_cpp.md)> &* **path** - Pointer to the path.

## Math:: vec3 getAngularVelocity ( float time , int loop = 0 )

Returns the angular velocity of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Angular velocity. If the number of frames is equal to 0 or 1, the function returns the (0,0,0) vector.
## int getClosestFrame ( const Math:: Vec3 & position )

Returns the number of the path frame, which is the closest to the given point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Coordinates of the point.

### Return value

The closest frame number.
## float getClosestTime ( const Math:: Vec3 & position )

Returns the path time in the path point which is the closest to the given point.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Coordinates of the point.

### Return value

Path time in seconds.
## void setFramePosition ( int num , const Math:: Vec3 & pos )

Sets the position coordinates for the path frame.
### Arguments

- *int* **num** - The frame number.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **pos** - Coordinates of the frame to be set.

## Math:: Vec3 getFramePosition ( int num )

Returns the position coordinates of the path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Coordinates of the frame.
## void setFrameRotation ( int num , const Math:: quat & rot )

Sets the rotation quaternion for the given path frame.
### Arguments

- *int* **num** - The frame number.
- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **rot** - Frame rotation quaternion to be set.

## Math:: quat getFrameRotation ( int num )

Returns the rotation quaternion of the given path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame rotation quaternion.
## void setFrameScale ( int num , const Math:: vec3 & scale )

Sets the scaling vector for the path frame.
### Arguments

- *int* **num** - The frame number.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **scale** - Frame scaling vector to be set.

## Math:: vec3 getFrameScale ( int num )

Returns the scaling vector of the path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame scaling vector.
## void setFrameTime ( int num , float time )

Sets the time for the specified path frame.
### Arguments

- *int* **num** - The frame number.
- *float* **time** - Frame time to be set.

## float getFrameTime ( int num )

Returns the time of the specified path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame time.
## void setFrameTransform ( int num , const Math:: Mat4 & transform )

Sets the transformation matrix for the path frame.
### Arguments

- *int* **num** - The frame number.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix to be set.

## Math:: Mat4 getFrameTransform ( int num )

Returns the transformation matrix of the path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame transformation matrix.
## Math:: Vec3 getLinearVelocity ( float time , int loop = 0 )

Returns the linear velocity of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Linear velocity. If the amount of frames is equal to 0 or 1, the function returns the (0,0,0) vector.
## Math:: Vec3 getPosition ( float time , int loop = 0 )

Returns the position of the object moving along the path at the specified time. If the path transformation is non-looped and the specified time is bigger than path transformation, the last path position will be returned. If the path transformation is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object position coordinates at the specified time.
## Math:: quat getRotation ( float time , int loop = 0 )

Returns the rotation of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object rotation at the specified time.
## Math:: vec3 getScale ( float time , int loop = 0 )

Returns the scale of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path transformation, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object scale at the specified time.
## Math:: Mat4 getTransform ( float time , int loop = 0 )

Returns the transformation of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object transformation matrix at the specified time.
## int addFrame ( )

Creates a new frame and appends it to the array of path frames.
### Return value

Number of path frames.
## void clear ( )

Clears the path (including its times and frames).
## int load ( const char * name )

Loads the path with the given name and *.path extension.
### Arguments

- *const char ** **name** - Path name.

### Return value

Returns 1 if the operation was a success; otherwise, 0 is returned.
## void removeFrame ( int num )

Removes the specified frame.
### Arguments

- *int* **num** - Frame number.

## int save ( const char * name )

Saves the path under the given name with the `*.path` extension.
### Arguments

- *const char ** **name** - Path name.

### Return value

Returns 1 if the operation was a success; otherwise, 0 is returned.
