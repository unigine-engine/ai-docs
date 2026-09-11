# Unigine::Path Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Interface for path loading, manipulating and saving.


The **path** is a spline along which an object can be moved. Such splines can be created, for example, in 3ds Max and then exported to a `*.path` file. Or, they can be created in the code by means of the *Path* class and then saved to the `*.path` file.


> **Warning:** There is no connection between functions of the *Path* class and pathfinding-related functions.


### Creating Simple Path from Code


As previously stated, the `*.path` asset can be created using the code. In general, the implementation includes the following steps:


- Create a new instance of the *Path* class.
- Add points to the path.
- Save the calculated path to the `*.path` file.


The following code creates a simple path between two control points and saves it to the `*.path` file.


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

## static Path ( )

Constructor. Creates an empty path.
## static Path ( string name )

Constructor. Creates an empty path of the specified name.
### Arguments

- *string* **name** - Name of the path.

## vec3 getAngularVelocity ( float time , int loop = 0 )

Returns the angular velocity of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Angular velocity. If the number of frames is equal to 0 or 1, the function returns the (0,0,0) vector.
## int getClosestFrame ( Vec3 position )

Returns the number of the path frame, which is the closest to the given point.
### Arguments

- *Vec3* **position** - Coordinates of the point.

### Return value

The closest frame number.
## float getClosestTime ( Vec3 position )

Returns the path time in the path point which is the closest to the given point.
### Arguments

- *Vec3* **position** - Coordinates of the point.

### Return value

Path time in seconds.
## void setFramePosition ( int num , Vec3 pos )

Sets the position coordinates for the path frame.
### Arguments

- *int* **num** - The frame number.
- *Vec3* **pos** - Coordinates of the frame to be set.

## Vec3 getFramePosition ( int num )

Returns the position coordinates of the path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Coordinates of the frame.
## void setFrameRotation ( int num , quat rot )

Sets the rotation quaternion for the given path frame.
### Arguments

- *int* **num** - The frame number.
- *quat* **rot** - Frame rotation quaternion to be set.

## quat getFrameRotation ( int num )

Returns the rotation quaternion of the given path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame rotation quaternion.
## void setFrameScale ( int num , vec3 scale )

Sets the scaling vector for the path frame.
### Arguments

- *int* **num** - The frame number.
- *vec3* **scale** - Frame scaling vector to be set.

## vec3 getFrameScale ( int num )

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
## void setFrameTransform ( int num , Mat4 transform )

Sets the transformation matrix for the path frame.
### Arguments

- *int* **num** - The frame number.
- *Mat4* **transform** - Transformation matrix to be set.

## Mat4 getFrameTransform ( int num )

Returns the transformation matrix of the path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame transformation matrix.
## Vec3 getLinearVelocity ( float time , int loop = 0 )

Returns the linear velocity of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Linear velocity. If the amount of frames is equal to 0 or 1, the function returns the (0,0,0) vector.
## Vec3 getPosition ( float time , int loop = 0 )

Returns the position of the object moving along the path at the specified time. If the path transformation is non-looped and the specified time is bigger than path transformation, the last path position will be returned. If the path transformation is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object position coordinates at the specified time.
## quat getRotation ( float time , int loop = 0 )

Returns the rotation of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object rotation at the specified time.
## vec3 getScale ( float time , int loop = 0 )

Returns the scale of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path transformation, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *int* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object scale at the specified time.
## Mat4 getTransform ( float time , int loop = 0 )

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

Clears the current path.
## int load ( string name )

Loads the path with the given name and *.path extension.
### Arguments

- *string* **name** - Path name.

### Return value

1 if the path is loaded successfully; otherwise, 0.
## void removeFrame ( int num )

Removes the specified frame.
### Arguments

- *int* **num** - Frame number.

## int save ( string name )

Saves the path under the given name with the `*.path` extension.
### Arguments

- *string* **name** - Path name.

### Return value

1 if the path is saved successfully; otherwise, 0.
