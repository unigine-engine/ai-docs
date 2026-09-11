# Unigine::Math::quat Struct (CPP)

**Header:** #include <UnigineMathLibQuat.h>


This class represents a quaternion type. Quaternions represent a rotation. Typically, they are used for smooth interpolation between two angles, and for avoiding the gimbal lock problem that can occur with euler angles.


Quaternions add a fourth element to the [x, y, z] values that define a vector, resulting in arbitrary 4-D vectors. The following example illustrates how each element of a unit quaternion relates to an axis-angle rotation, where q represents a unit quaternion (x, y, z, w), axis is normalized, and theta is the desired counterclockwise (CCW) rotation around the axis:


- q.x = sin(theta/2) * axis.x
- q.y = sin(theta/2) * axis.y
- q.z = sin(theta/2) * axis.z
- q.w = cos(theta/2)


### Usage Example


The following example creates a quaternion for node rotation: 45 degrees per second along X axis.


> **Notice:** It's supposed that you have already created [node](../../../api/library/nodes/class.node_cpp.md) instance to rotate.


```cpp
// AppWorldLogic.cpp file

// Declaring a pointer for a World light source node
NodePtr node;

int AppWorldLogic::init()
{
	/* ... */

	// Trying to find a World Node source in the current world
	node = World::getNodeByType(Node::LIGHT_WORLD);

	return 1;
}

int AppWorldLogic::update()
{
	/* ... */

	// get delta time value
	float delta_time = Game::getIFps();

	// create quat for 45 degrees per second rotation along X axis
	Unigine::Math::quat rotation_delta = Unigine::Math::quat(1.0f, 0.0f, 0.0f, 45.0f * delta_time);

	// rotate the node if it exists
	if (node)
		node->worldRotate(rotation_delta);

	/* ... */
}

```


In the example above, the quaternion was initialized by using four values: 3 axis components (*x,y,z*) and angle (*w* component of the quaternion). **1** value of the X axis component shows that the rotation will be performed along X axis.


### See Also


- An article on [Quaternions and Spatial Rotation](https://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation) on Wikipedia.


## quat Struct

### Members

---

## quat ( float x_ , float y_ , float z_ , float w_ , ConstexprTag )

Constructor. Initializes the quaternion using given constant float values.
### Arguments

- *float* **x_** - X component of the quaternion.
- *float* **y_** - Y component of the quaternion.
- *float* **z_** - Z component of the quaternion.
- *float* **w_** - W component of the quaternion.
- *ConstexprTag*  - Auxiliary tag.

## quat ( )

Default constructor. Produces an identity quaternion (**0.0**, **0.0**, **0.0**, **1.0**).
## quat ( float x , float y , float z , float angle )

Constructor. Initializes the quaternion using the given rotation axis component values and angle.
### Arguments

- *float* **x** - X component of the rotation axis vector.
- *float* **y** - Y component of the rotation axis vector.
- *float* **z** - Z component of the rotation axis vector.
- *float* **angle** - The angle of rotation around the axis.

## quat ( float angle_x , float angle_y , float angle_z )

Constructor. Initializes the quaternion using given angles for each axis.
### Arguments

- *float* **angle_x** - Rotation angle along the X axis, in degrees.
- *float* **angle_y** - Rotation angle along the Y axis, in degrees.
- *float* **angle_z** - Rotation angle along the Z axis, in degrees.

## quat ( const vec3& axis , float angle )

Constructor. Initializes the quaternion using given rotation axis and angle.
### Arguments

- *const vec3&* **axis** - Rotation axis.
- *float* **angle** - Rotation angle, in degrees.

## quat ( const vec3& col0 , const vec3& col1 , const vec3& col2 )

Constructor. Initializes the quaternion using three given matrix columns represented by [vec3](../../../api/library/math/class.vec3_cpp.md) vectors.
### Arguments

- *const vec3&* **col0** - First matrix column.
- *const vec3&* **col1** - Second matrix column.
- *const vec3&* **col2** - Third matrix column.

## quat ( const quat& q )

Constructor. Initializes the quaternion by copying a given source quaternion.
### Arguments

- *const quat&* **q** - Source quaternion.

## explicit quat ( const float* q )

Constructor. Initializes the vector using a given pointer to the quaternion.
### Arguments

- *const float** **q** - Pointer to the quaternion.

## quat ( const vec4& v )

Constructor. Initializes the quaternion using a given four-component [vec4](../../../api/library/math/class.vec4_cpp.md) source vector.
### Arguments

- *const vec4&* **v** - Four-component source vector.

## quat ( const mat3& m )

Constructor. Initializes the quaternion using a given [mat3](../../../api/library/math/class.mat3_cpp.md) source matrix (3x3).
### Arguments

- *const mat3&* **m** - Source matrix (3x3).

## explicit quat ( const mat4& m )

Constructor. Initializes the quaternion using a given [mat4](../../../api/library/math/class.mat4_cpp.md) source matrix (4x4).
### Arguments

- *const mat4&* **m** - Source matrix (4x4).

## explicit quat ( const dmat4& m )

Constructor. Initializes the quaternion using a given [dmat4](../../../api/library/math/class.dmat4_cpp.md) source matrix (3x4).
### Arguments

- *const dmat4&* **m** - Source matrix (3x4).

## quat ( const __m128& v )


Constructor. Initializes the quaternion using a given __m128 variable (128-bit).


> **Notice:** We do not recommend to use this method unless you have a clear understanding of SSE2.


### Arguments

- *const __m128&* **v** - 128-bit variable.

## void set ( const mat3& m )

Sets the quaternion using a given [mat3](../../../api/library/math/class.mat3_cpp.md) source matrix (3x3).
### Arguments

- *const mat3&* **m** - Source matrix (3x3).

## void set ( const mat4& m )

Sets the quaternion using a given [mat4](../../../api/library/math/class.mat4_cpp.md) source matrix (4x4).
### Arguments

- *const mat4&* **m** - Source matrix (4x4).

## void set ( const dmat4& m )

Sets the quaternion using a given [dmat4](../../../api/library/math/class.dmat4_cpp.md) source matrix (3x4).
### Arguments

- *const dmat4&* **m** - Source matrix (3x4).

## void set ( const vec3& axis , float angle )

Sets the quaternion using given rotation axis and angle.
### Arguments

- *const vec3&* **axis** - Rotation axis.
- *float* **angle** - Rotation angle, in degrees.

## void set ( float axis_x , float axis_y , float axis_z , float angle )

Sets the quaternion using the axis coordinates and the angle.
### Arguments

- *float* **axis_x** - X coordinate of the axis.
- *float* **axis_y** - Y coordinate of the axis.
- *float* **axis_z** - Z coordinate of the axis.
- *float* **angle** - Angle value, in degrees.

## void set ( float angle_x , float angle_y , float angle_z )

Sets the quaternion using given angles for each axis.
### Arguments

- *float* **angle_x** - Rotation angle along the X axis, in degrees.
- *float* **angle_y** - Rotation angle along the Y axis, in degrees.
- *float* **angle_z** - Rotation angle along the Z axis, in degrees.

## void set ( const vec3& col0 , const vec3& col1 , const vec3& col2 )

Sets the quaternion using three given matrix columns represented by [vec3](../../../api/library/math/class.vec3_cpp.md) vectors.
### Arguments

- *const vec3&* **col0** - First matrix column.
- *const vec3&* **col1** - Second matrix column.
- *const vec3&* **col2** - Third matrix column.

## void set ( const float* q )

Sets the quaternion using a given pointer to the source quaternion.
### Arguments

- *const float** **q** - Pointer to the source quaternion.

## void get ( vec3& axis , float& angle ) const

Returns the rotation axis and angle of the quaternion and puts the values to corresponding variables: axis.x = x, axis.y = y, axis.z = z, angle = w.
### Arguments

- *vec3&* **axis** - Rotation axis.
- *float&* **angle** - Rotation angle, in degrees.

## void get ( float* qq ) const

Returns the quaternion: qq[0]=x, qq[1]=y, qq[2]=z, qq[3]=w.
### Arguments

- *float** **qq** - Pointer to the quaternion.

## float * get ( )

Returns a pointer to the quaternion.
### Return value

Pointer to the quaternion.
## const float * get ( ) const

Returns a constant pointer to the quaternion.
### Return value

Constant pointer to the quaternion.
## float getAngle ( const vec3& axis ) const

Returns the rotation angle of the quaternion for a given rotation axis.
### Arguments

- *const vec3&* **axis** - Rotation axis.

### Return value

Rotation angle, in degrees, within the **[-180, 180]** range.
## vec3 getBinormal ( ) const

Returns the quaternion binormal vector with respect to orientation.
### Return value

Quaternion binormal vector.
## mat3 getMat3 ( ) const


Returns the rotation matrix for the quaternion.


```text
For the quaternion (x, y, z, w) the corresponding rotation matrix M is defined as follows:
    | 1 - 2y� - 2z�    2xy + 2wz      	2xz - 2wy     |
M=  | 2xy - 2wz        1 - 2x� - 2z�    2yz + 2wx     |
    | 2xz + 2wy        2yz - 2wx        1 - 2x� - 2y� |

```


### Return value

Rotation matrix for the quaternion.
## vec3 getNormal ( ) const

Returns the quaternion normal vector.
### Return value

Quaternion normal vector.
## vec3 getTangent ( ) const

Returns the quaternion tangent vector.
### Return value

Quaternion tangent vector.
## vec4 getTangent4 ( ) const

Returns the quaternion tangent vector and binormal orientation as a four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector.
### Return value

Four-component vector representing guaternion tangent vector and binormal orientation.
## quat & normalize ( )

Returns normalized quaternion.
### Return value

Normalized quaternion.
## quat & normalizeValid ( )

Normalizes a quaternion, makes its magnitude equal to 1. When normalized, a quaternion keeps the same direction but its length is equal to 1. Check for the zero quaternion is performed: if the argument is a zero quaternion, then a zero quaternion is returned.
### Return value

Normalized quaternion.
## quat & normalizeFast ( )

Returns normalized quaternion, calculated using the fast inverse square root algorithm.
### Return value

Normalized quaternion.
## quat & normalizeValidFast ( )

Returns normalized quaternion, calculated using the fast inverse square root algorithm. Check for the zero quaternion is performed: if the argument is a zero quaternion, then a zero quaternion is returned.
### Return value

Normalized quaternion.
## float * operator float * ( )

Performs type conversion to float *.
## const float * operator const float * ( ) const

Performs type conversion to const float *.
## void * operator void * ( )

Performs type conversion to void *.
## const void * operator const void * ( ) const

Performs type conversion to const void *.
## float & operator[] ( int i )

Performs array access to the quaternion item reference by using given item index.
### Arguments

- *int* **i** - Quaternion item index.

### Return value

Quaternion item reference.
## float operator[] ( int i ) const

Performs array access to the quaternion item by using given item index.
### Arguments

- *int* **i** - Quaternion item index.

### Return value

Quaternion item.
## quat & operator= ( const quat& q )

Performs quaternion assignment. Destination quaternion = Source quaternion.
### Arguments

- *const quat&* **q** - Source quaternion.

### Return value

Result.
## quat operator- ( ) const

Performs quaternion negation. The sign of each component of the quaternion is flipped.
### Return value

Resulting quaternion.
## quat & operator*= ( float v )

Performs scalar multiplication.
### Arguments

- *float* **v** - Scalar value.

### Return value

Resulting quaternion.
## quat & operator*= ( const quat& q )

Performs quaternion multiplication.
### Arguments

- *const quat&* **q** - Quaternion.

### Return value

Resulting quaternion.
## quat & operator+= ( const quat& q )

Performs quaternion addition.
### Arguments

- *const quat&* **q** - Quaternion.

### Return value

Resulting quaternion.
## quat & operator-= ( const quat& q )

Performs quaternion subtraction.
### Arguments

- *const quat&* **q** - Quaternion.

### Return value

Resulting quaternion.
## quat & abs ( quat & ret , const quat & q )

Ensures that the returned quaternion has a non-negative scalar part (w). If it is negative, the entire quaternion is negated; otherwise, it remains unchanged.
### Arguments

- *[quat](../../../api/library/math/class.quat_cpp.md) &* **ret** - Value to store the result.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Resulting quaternion.
## quat abs ( const quat & q )

Ensures that the returned quaternion has a non-negative scalar part (w). If it is negative, the entire quaternion is negated; otherwise, it remains unchanged.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Resulting quaternion.
## vec3 & log ( vec3 & ret , const quat & q )

Converts a quaternion into a rotation vector in 3D space by computing the quaternion's logarithm. It extracts the axis of rotation and scales it by the angle, storing the result in the argument vector *ret*.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Value to store the result.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Resulting vector.
## vec3 log ( const quat & q )

Returns the rotation vector in 3D space by computing the quaternion's logarithm (extracts the axis of rotation and scales it by the angle).
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Resulting vector.
## quat & log ( quat & ret , const vec3 & v )

Converts a 3D rotation vector into a quaternion. If the length of the input vector is very small, the quaternion is close to an identity quaternion. Otherwise, the function computes the sine and cosine of the half angle and constructs the quaternion to represent the rotation described by the vector.
### Arguments

- *[quat](../../../api/library/math/class.quat_cpp.md) &* **ret** - Value to store the result.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Rotation vector.

### Return value

Resulting quaternion.
## quat log ( const vec3 & q )

Converts a 3D rotation vector into a quaternion. If the length of the input vector is very small, the quaternion is close to an identity quaternion. Otherwise, the function computes the sine and cosine of the half angle and constructs the quaternion to represent the rotation described by the vector.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **q** - Rotation vector.

### Return value

Resulting quaternion.
## unsigned int hash ( ) const

Returns a hash for the quaternion.
### Return value

Hash generated for the quaternion.
