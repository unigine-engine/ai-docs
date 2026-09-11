# Unigine::Path Class (CS)


Interface for path loading, manipulating and saving.


The **path** is a spline along which an object can be moved. Such splines can be created, for example, in 3ds Max and then exported to a `*.path` file. Or, they can be created in the code by means of the *Path* class and then saved to the `*.path` file.


> **Warning:** There is no connection between functions of the *Path* class and pathfinding-related functions.


### Creating Simple Path from Code


As previously stated, the `*.path` asset can be created using the code. In general, the implementation includes the following steps:


- Create a new instance of the *Path* class.
- Add points to the path.
- Save the calculated path to the `*.path` file.


The following code creates a simple path between two control points and saves it to the `*.path` file.


```csharp
void Init()
{
	// specify control points
	vec3[] points = new vec3[4];
	points[0] = new vec3(0.0, 0.0, 0.0);
	points[1] = new vec3(10.0, 0.0, 0.0);
	points[2] = new vec3(10.0, 10.0, 0.0);
	points[3] = new vec3(0.0, 10.0, 0.0);

	// create a new path
	Path path = new Path();

	// add the points to the path
	for (int i = 0; i < points.Length; i++)
	{
		path.AddFrame();
		path.SetFramePosition(i, points[i]);
		// normalized time of passing the point (0 - path start, 1 - path end)
		float t = (float)i/(points.Length-1);
		path.SetFrameTime(i, t);
	}

	// save the path
	path.Save("test_path.path");
}


```


> **Notice:** For simplicity in the example, we pass a point index as the second argument to the *[setFrameTime()](#setFrameTime_int_float_void)* method, so that it would take one second to pass the point.


## Path Class

### Properties

## int NumFrames

The number of the path frames.
### Members

---

## Path ( )

Constructor. Creates an empty path.
## Path ( string name )

Constructor. Creates an empty path of the specified name.
### Arguments

- *string* **name** - Name of the path.

## Path ( Path path )

Constructor. Creates a path out of the specified path.
### Arguments

- *[Path](../../../api/library/common/class.path_cs.md)* **path** - Path instance.

## vec3 GetAngularVelocity ( float time , bool loop = 0 )

Returns the angular velocity of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *bool* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Angular velocity. If the number of frames is equal to 0 or 1, the function returns the (0,0,0) vector.
## int GetClosestFrame ( vec3 position )

Returns the number of the path frame, which is the closest to the given point.
### Arguments

- *vec3* **position** - Coordinates of the point.

### Return value

The closest frame number.
## float GetClosestTime ( vec3 position )

Returns the path time in the path point which is the closest to the given point.
### Arguments

- *vec3* **position** - Coordinates of the point.

### Return value

Path time in seconds.
## void SetFramePosition ( int num , vec3 pos )

Sets the position coordinates for the path frame.
### Arguments

- *int* **num** - The frame number.
- *vec3* **pos** - Coordinates of the frame to be set.

## vec3 GetFramePosition ( int num )

Returns the position coordinates of the path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Coordinates of the frame.
## void SetFrameRotation ( int num , quat rot )

Sets the rotation quaternion for the given path frame.
### Arguments

- *int* **num** - The frame number.
- *quat* **rot** - Frame rotation quaternion to be set.

## quat GetFrameRotation ( int num )

Returns the rotation quaternion of the given path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame rotation quaternion.
## void SetFrameScale ( int num , vec3 scale )

Sets the scaling vector for the path frame.
### Arguments

- *int* **num** - The frame number.
- *vec3* **scale** - Frame scaling vector to be set.

## vec3 GetFrameScale ( int num )

Returns the scaling vector of the path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame scaling vector.
## void SetFrameTime ( int num , float time )

Sets the time for the specified path frame.
### Arguments

- *int* **num** - The frame number.
- *float* **time** - Frame time to be set.

## float GetFrameTime ( int num )

Returns the time of the specified path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame time.
## void SetFrameTransform ( int num , mat4 transform )

Sets the transformation matrix for the path frame.
### Arguments

- *int* **num** - The frame number.
- *mat4* **transform** - Transformation matrix to be set.

## mat4 GetFrameTransform ( int num )

Returns the transformation matrix of the path frame.
### Arguments

- *int* **num** - The frame number.

### Return value

Frame transformation matrix.
## vec3 GetLinearVelocity ( float time , bool loop = 0 )

Returns the linear velocity of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *bool* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Linear velocity. If the amount of frames is equal to 0 or 1, the function returns the (0,0,0) vector.
## vec3 GetPosition ( float time , bool loop = 0 )

Returns the position of the object moving along the path at the specified time. If the path transformation is non-looped and the specified time is bigger than path transformation, the last path position will be returned. If the path transformation is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *bool* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object position coordinates at the specified time.
## quat GetRotation ( float time , bool loop = 0 )

Returns the rotation of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *bool* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object rotation at the specified time.
## vec3 GetScale ( float time , bool loop = 0 )

Returns the scale of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path transformation, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *bool* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object scale at the specified time.
## mat4 GetTransform ( float time , bool loop = 0 )

Returns the transformation of the object moving along the path at the specified time. If the path is non-looped and the specified time is bigger than the current path time, the last path position will be returned. If the path is looped, several loops can be used to count off time.
### Arguments

- *float* **time** - Time in seconds.
- *bool* **loop** - Flag indicating if the path is looped. The default is 0 (path isn't looped).

### Return value

Object transformation matrix at the specified time.
## int AddFrame ( )

Creates a new frame and appends it to the array of path frames.
### Return value

Number of path frames.
## void Clear ( )

Clears the path (including its times and frames).
## bool Load ( string name )

Loads the path with the given name and *.path extension.
### Arguments

- *string* **name** - Path name.

### Return value

Returns 1 if the operation was a success; otherwise, 0 is returned.
## void RemoveFrame ( int num )

Removes the specified frame.
### Arguments

- *int* **num** - Frame number.

## bool Save ( string name )

Saves the path under the given name with the `*.path` extension.
### Arguments

- *string* **name** - Path name.

### Return value

Returns 1 if the operation was a success; otherwise, 0 is returned.
