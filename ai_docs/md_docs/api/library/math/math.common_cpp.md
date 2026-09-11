# Math Common Functions (CPP)

**Header:** #include <UnigineMathLib.h>


This class represents a collection of common math functions.


> **Notice:** Math common functions are the members of the **Unigine::Math** namespace.


## Math Class

### Enums

## AXIS

| Name | Description |
|---|---|
| **AXIS_X** = = 0 | Positive X axis. |
| **AXIS_Y** = = 1 | Positive Y axis. |
| **AXIS_Z** = = 2 | Positive Z axis. |
| **AXIS_NX** = = 3 | Negative X axis. |
| **AXIS_NY** = = 4 | Negative Y axis. |
| **AXIS_NZ** = = 5 | Negative Z axis. |

### Members

---

## float abs ( float v )

Returns the absolute value of the argument.
### Arguments

- *float* **v** - Float value.

### Return value

Absolute value.
## double abs ( double v )

Returns the absolute value of the argument.
### Arguments

- *double* **v** - Value.

### Return value

Absolute value.
## int abs ( int v )

Returns the absolute value of the argument.
### Arguments

- *int* **v** - Value.

### Return value

Absolute value.
## long long abs ( long long v )

Returns the absolute value of the argument.
### Arguments

- *long long* **v** - Value.

### Return value

Absolute value.
## vec2 abs ( vec2 v )

Returns the absolute values of the vector components.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md)* **v** - Source vector.

### Return value

Vector with absolute values.
## vec3 abs ( vec3 v )

Returns the absolute values of the vector components.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md)* **v** - Source vector.

### Return value

Vector with absolute values.
## vec4 abs ( vec4 v )

Returns the absolute values of the vector components.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md)* **v** - Source vector.

### Return value

Vector with absolute values.
## dvec2 abs ( dvec2 v )

Returns the absolute values of the vector components.
### Arguments

- *[dvec2](../../../api/library/math/class.dvec2_cpp.md)* **v** - Source vector.

### Return value

Vector with absolute values.
## dvec3 abs ( dvec3 v )

Returns the absolute values of the vector components.
### Arguments

- *[dvec3](../../../api/library/math/class.dvec3_cpp.md)* **v** - Source vector.

### Return value

Vector with absolute values.
## dvec4 abs ( dvec4 v )

Returns the absolute values of the vector components.
### Arguments

- *[dvec4](../../../api/library/math/class.dvec4_cpp.md)* **v** - Source vector.

### Return value

Vector with absolute values.
## ivec2 abs ( ivec2 v )

Returns the absolute values of the vector components.
### Arguments

- *[ivec2](../../../api/library/math/class.ivec2_cpp.md)* **v** - Source vector.

### Return value

Vector with absolute values.
## ivec3 abs ( ivec3 v )

Returns the absolute values of the vector components.
### Arguments

- *[ivec3](../../../api/library/math/class.ivec3_cpp.md)* **v** - Source vector.

### Return value

Vector with absolute values.
## ivec4 abs ( ivec4 v )

Returns the absolute values of the vector components.
### Arguments

- *[ivec4](../../../api/library/math/class.ivec4_cpp.md)* **v** - Source vector.

### Return value

Vector with absolute values.
## float * add3 ( float *UNIGINE_RESTRICT ret , const float *UNIGINE_RESTRICT v0 , const float *UNIGINE_RESTRICT v1 )

Returns the result of a componentwise addition of three components of vectors by storing it in the array.
### Arguments

- *float *UNIGINE_RESTRICT* **ret** - Array to store the return value.
- *const float *UNIGINE_RESTRICT* **v0** - Pointer to vector.
- *const float *UNIGINE_RESTRICT* **v1** - Pointer to vector.

### Return value

Pointer to the array that stores the return value.
## float bezier ( const float * times , const float * values , float time )


Calculates the value of a cubic Bezier function for *t = time*.


![](cubic_bezier.gif)


A cubic Bezier curve is represented by 4 points. **Po** is the start point, **P1** and **P2** are control points 1 and 2 and **P3** is the end point. The start and end point denote the beginning and end points of the path and the control points determine how the path moves from the start to the finish. As can be seen from the image, the only variable changing is **t** which determines how far the path has progressed from P0 to P3. Cubic Bezier curves are used as timing functions particularly for keyframe interpolation.


### Arguments

- *const float ** **times** - Coordinates of the four points of the curve along the horizontal *T* (times) axis in the range **[0.0f, 1.0f]**.
- *const float ** **values** - Coordinates of the four points of the curve along the vertical *V* (values) axis in the range **[0.0f, 1.0f]**.
- *float* **time** - Time in the range **[0, 1]**, for which the value of the Bezier function is to be calculated.

### Return value

Value of the Bezier function.
## double bezier ( const float * times , const double * values , float time )


Calculates the value of a cubic Bezier function for *t = time*.


![](cubic_bezier.gif)


A cubic Bezier curve is represented by 4 points. **Po** is the start point, **P1** and **P2** are control points 1 and 2 and **P3** is the end point. The start and end point denote the beginning and end points of the path and the control points determine how the path moves from the start to the finish. As can be seen from the image, the only variable changing is **t** which determines how far the path has progressed from P0 to P3. Cubic Bezier curves are used as timing functions particularly for keyframe interpolation.


### Arguments

- *const float ** **times** - Coordinates of the four points of the curve along the horizontal *T* (times) axis in the range **[0.0f, 1.0f]**.
- *const double ** **values** - Coordinates of the four points of the curve along the vertical *V* (values) axis in the range **[0.0f, 1.0f]**.
- *float* **time** - Time in the range **[0, 1]**, for which the value of the Bezier function is to be calculated.

### Return value

Value of the Bezier function.
## vec4 blueNoise ( int x , int y )

Returns a blue noise value for the given pixel coordinates.
### Arguments

- *int* **x** - X coordinate of the pixel.
- *int* **y** - Y coordinate of the pixel.

### Return value

Blue noise value.
## float ceil ( float v )


Ceiling function that returns the smallest integer value that is not less than the argument.


```text
float a = ceil(3.141593); // a = 4.0
```


### Arguments

- *float* **v** - Argument.

### Return value

Smallest integer value not less than *v*.
## double ceil ( double v )


Ceiling function that returns the smallest integer value that is not less than the argument.


```text
double a = ceil(3.141593); // a = 4.0
```


### Arguments

- *double* **v** - Argument.

### Return value

Smallest integer value not less than *v*.
## const vec2 & ceil ( const vec2 & v )

Ceiling function that returns the vector storing the smallest integer values that are not less than the argument.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the smallest integer values not less than *v*.
## const vec3 & ceil ( const vec3 & v )

Ceiling function that returns the vector storing the smallest integer values that are not less than the argument.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the smallest integer values not less than *v*.
## const vec4 & ceil ( const vec4 & v )

Ceiling function that returns the vector storing the smallest integer values that are not less than the argument.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the smallest integer values not less than *v*.
## const dvec2 & ceil ( const dvec2 & v )

Ceiling function that returns the vector storing the smallest integer values that are not less than the argument.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the smallest integer values not less than *v*.
## const dvec3 & ceil ( const dvec3 & v )

Ceiling function that returns the vector storing the smallest integer values that are not less than the argument.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the smallest integer values not less than *v*.
## const dvec4 & ceil ( const dvec4 & v )

Ceiling function that returns the vector storing the smallest integer values that are not less than the argument.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the smallest integer values not less than *v*.
## int ceilInt ( float v )

Returns the smallest value that's greater than or equal to the argument, stored as an integer.
### Arguments

- *float* **v** - Value.

### Return value

Resulting *int* value.
## int ceilInt ( double v )

Returns the smallest value that's greater than or equal to the argument, stored as an integer.
### Arguments

- *double* **v** - Value.

### Return value

Resulting *int* value.
## double changeRange ( double value , const dvec4 & range )

Transforms the value from the source range to the corresponding value within target range.
### Arguments

- *double* **value** - The value within the source range.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **range** - The vector containing 4 values: values X and Y define the source range, values Z and W define the target range.

### Return value

The value within the target range.
## bool checkMask ( const int mask , const int bits )

Checks if any of the bits specified in bits are set in mask.
### Arguments

- *const int* **mask** - Bit mask to be checked.
- *const int* **bits** - Bits in the mask to be checked.

### Return value

true if there is at least one bit that is specified in both mask and bits, otherwise false.
## bool checkMask ( const unsigned int mask , const unsigned int bits )

Checks if any of the bits specified in bits are set in mask.
### Arguments

- *const unsigned int* **mask** - Bit mask to be checked.
- *const unsigned int* **bits** - Bits in the mask to be checked.

### Return value

true if there is at least one bit that is specified in both mask and bits, otherwise false.
## bool checkMask ( const unsigned int mask , const int bits )

Checks if any of the bits specified in bits are set in mask.
### Arguments

- *const unsigned int* **mask** - Bit mask to be checked.
- *const int* **bits** - Bits in the mask to be checked.

### Return value

true if there is at least one bit that is specified in both mask and bits, otherwise false.
## bool checkMask ( const int mask , const unsigned int bits )

Checks if any of the bits specified in bits are set in mask.
### Arguments

- *const int* **mask** - Bit mask to be checked.
- *const unsigned int* **bits** - Bits in the mask to be checked.

### Return value

true if there is at least one bit that is specified in both mask and bits, otherwise false.
## bool checkRange ( float value , float range_min , float range_max )

Checks if the input value is within the specified range.
### Arguments

- *float* **value** - Input value.
- *float* **range_min** - Minimum value of the range.
- *float* **range_max** - Maximum value of the range.

### Return value

true if the value is within the range, otherwise � false.
## bool checkRange ( double value , double range_min , double range_max )

Checks if the input value is within the specified range.
### Arguments

- *double* **value** - Input value.
- *double* **range_min** - Minimum value of the range.
- *double* **range_max** - Maximum value of the range.

### Return value

true if the value is within the range, otherwise � false.
## bool checkRange ( int value , int range_min , int range_max )

Checks if the input value is within the specified range.
### Arguments

- *int* **value** - Input value.
- *int* **range_min** - Minimum value of the range.
- *int* **range_max** - Maximum value of the range.

### Return value

true if the value is within the range, otherwise � false.
## bool checkRange ( long long value , long long range_min , long long range_max )

Checks if the input value is within the specified range.
### Arguments

- *long long* **value** - Input value.
- *long long* **range_min** - Minimum value of the range.
- *long long* **range_max** - Maximum value of the range.

### Return value

true if the value is within the range, otherwise � false.
## bool checkRange ( short value , short range_min , short range_max )

Checks if the input value is within the specified range.
### Arguments

- *short* **value** - Input value.
- *short* **range_min** - Minimum value of the range.
- *short* **range_max** - Maximum value of the range.

### Return value

true if the value is within the range, otherwise � false.
## bool checkRange ( char value , char range_min , char range_max )

Checks if the input value is within the specified range.
### Arguments

- *char* **value** - Input value.
- *char* **range_min** - Minimum value of the range.
- *char* **range_max** - Maximum value of the range.

### Return value

true if the value is within the range, otherwise � false.
## double clamp ( double v , double v0 , double v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *double* **v** - Value to be clamped.
- *double* **v0** - Minimum value.
- *double* **v1** - Maximum value.

### Return value

Clamped value.
## float clamp ( float v , float v0 , float v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *float* **v** - Value to be clamped.
- *float* **v0** - Minimum value.
- *float* **v1** - Maximum value.

### Return value

Clamped value.
## int clamp ( int v , int v0 , int v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *int* **v** - Value to be clamped.
- *int* **v0** - Minimum value.
- *int* **v1** - Maximum value.

### Return value

Clamped value.
## char clamp ( char v , char v0 , char v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *char* **v** - Value to be clamped.
- *char* **v0** - Minimum value.
- *char* **v1** - Maximum value.

### Return value

Clamped value.
## long long clamp ( long long v , long long v0 , long long v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *long long* **v** - Value to be clamped.
- *long long* **v0** - Minimum value.
- *long long* **v1** - Maximum value.

### Return value

Clamped value.
## dvec2 clamp ( const dvec2 & v , const dvec2 & v0 , const dvec2 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - Value to be clamped.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - Minimum value.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## ivec2 clamp ( const ivec2 & v , const ivec2 & v0 , const ivec2 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v** - The value.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - Minimum value.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## vec2 clamp ( const vec2 & v , const vec2 & v0 , const vec2 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - Value to be clamped.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - Minimum value.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## dvec3 clamp ( const dvec3 & v , const dvec3 & v0 , const dvec3 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Value to be clamped.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - Minimum value.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## ivec3 clamp ( const ivec3 & v , const ivec3 & v0 , const ivec3 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v** - Value to be clamped.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - Minimum value.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## vec3 clamp ( const vec3 & v , const vec3 & v0 , const vec3 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Value to be clamped.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Minimum value.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## bvec4 clamp ( const bvec4 & v , const bvec4 & v0 , const bvec4 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v** - Value to be clamped.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - Minimum value.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## dvec4 clamp ( const dvec4 & v , const dvec4 & v0 , const dvec4 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - Value to be clamped.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - Minimum value.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## ivec4 clamp ( const ivec4 & v , const ivec4 & v0 , const ivec4 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v** - Value to be clamped.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - Minimum value.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## vec4 clamp ( const vec4 & v , const vec4 & v0 , const vec4 & v1 )

Clamps a value within the specified *min* and *max* limits.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - Value to be clamped.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - Minimum value.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Maximum value.

### Return value

Clamped value.
## Type clamp ( Type v , Type v0 , Type v1 )

Clamps the value within the specified *min* and *max* limits.
### Arguments

- *Type* **v** - Value to be clamped.
- *Type* **v0** - Minimum value.
- *Type* **v1** - Maximum value.

### Return value

Clamped value.
## int compare ( int v0 , int v1 )

Compares two scalars of the int type.
### Arguments

- *int* **v0** - First int scalar.
- *int* **v1** - Second int scalar.

### Return value

1 if v0 is equal to v1; otherwise, 0.
## int compare ( float v0 , float v1 )

Checks if the two scalars of the float type are exactly equal.
### Arguments

- *float* **v0** - First float scalar.
- *float* **v1** - Second float scalar.

### Return value

1 if v0 is equal to v1; otherwise, 0.
## int compare ( double v0 , double v1 )

Checks if the two scalars of the double type are exactly equal.
### Arguments

- *double* **v0** - First double scalar.
- *double* **v1** - Second double scalar.

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( float v0 , float v1 , float epsilon )

Compares two values to determine if they can be considered equal within a given tolerance (epsilon).
### Arguments

- *float* **v0** - First scalar.
- *float* **v1** - Second scalar.
- *float* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( double v0 , double v1 , double epsilon )

Compares two values to determine if they can be considered equal within a given tolerance (epsilon).
### Arguments

- *double* **v0** - First scalar.
- *double* **v1** - Second scalar.
- *double* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const vec2 & v0 , const vec2 & v1 )

Compares two vectors according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.

### Return value

1 if v0 is equal to v1; otherwise, 0.
## int compare ( const vec2 & v0 , const vec2 & v1 , float epsilon )

Compares two vectors according to the specified degree of precision.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.
- *float* **epsilon** - Epsilon (degree of precision).

### Return value

1 if v0 is equal to v1; otherwise, 0.
## int compare ( const dvec2 & v0 , const dvec2 & v1 )

Compares two vectors according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second vector.

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const dvec2 & v0 , const dvec2 & v1 , double epsilon )

Compares two vectors according to the specified degree of precision.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second vector.
- *double* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const vec3 & v0 , const vec3 & v1 )

Compares two vectors according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const vec3 & v0 , const vec3 & v1 , float epsilon )

Compares two vectors according to the specified degree of precision.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.
- *float* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const dvec3 & v0 , const dvec3 & v1 )

Compares two vectors according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const dvec3 & v0 , const dvec3 & v1 , double epsilon )

Compares two vectors according to the specified degree of precision.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.
- *double* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const vec4 & v0 , const vec4 & v1 )

Compares two vectors according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const vec4 & v0 , const vec4 & v1 , float epsilon )

Compares two vectors according to the specified degree of precision.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.
- *float* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const dvec4 & v0 , const dvec4 & v1 )

Compares two vectors according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const dvec4 & v0 , const dvec4 & v1 , double epsilon )

Compares two vectors according to the specified degree of precision.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.
- *double* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the v0 is equal to v1; otherwise, 0.
## int compare ( const quat & q0 , const quat & q1 )

Compares two quaternions according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q0** - First quaternion.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q1** - Second quaternion.

### Return value

1 if the q0 is equal to q1; otherwise, 0.
## int compare ( const quat & q0 , const quat & q1 , float epsilon )

Compares two quaternions according to the specified degree of precision.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q0** - First quaternion.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q1** - Second quaternion.
- *float* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the q0 is equal to q1; otherwise, 0.
## int compare ( const mat2 & m0 , const mat2 & m1 )

Compares two matrices according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [mat2](../../../api/library/math/class.mat2_cpp.md) &* **m0** - First matrix.
- *const [mat2](../../../api/library/math/class.mat2_cpp.md) &* **m1** - Second matrix.

### Return value

1 if the m0 is equal to m1; otherwise, 0.
## int compare ( const mat2 & m0 , const mat2 & m1 , float epsilon )

Compares two matrices according to the specified degree of precision.
### Arguments

- *const [mat2](../../../api/library/math/class.mat2_cpp.md) &* **m0** - First matrix.
- *const [mat2](../../../api/library/math/class.mat2_cpp.md) &* **m1** - Second matrix.
- *float* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the m0 is equal to m1; otherwise, 0.
## int compare ( const mat3 & m0 , const mat3 & m1 )

Compares two matrices according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [mat3](../../../api/library/math/class.mat3_cpp.md) &* **m0** - First matrix.
- *const [mat3](../../../api/library/math/class.mat3_cpp.md) &* **m1** - Second matrix.

### Return value

1 if the m0 is equal to m1; otherwise, 0.
## int compare ( const mat3 & m0 , const mat3 & m1 , float epsilon )

Compares two matrices according to the specified degree of precision.
### Arguments

- *const [mat3](../../../api/library/math/class.mat3_cpp.md) &* **m0** - First matrix.
- *const [mat3](../../../api/library/math/class.mat3_cpp.md) &* **m1** - Second matrix.
- *float* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the m0 is equal to m1; otherwise, 0.
## int compare ( const mat4 & m0 , const mat4 & m1 )

Compares two matrices according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m0** - First matrix.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m1** - Second matrix.

### Return value

1 if the m0 is equal to m1; otherwise, 0.
## int compare ( const mat4 & m0 , const mat4 & m1 , float epsilon )

Compares two matrices according to the specified degree of precision.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m0** - First matrix.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m1** - Second matrix.
- *float* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the m0 is equal to m1; otherwise, 0.
## int compare ( const dmat4 & m0 , const dmat4 & m1 )

Compares two matrices according to the degree of precision equal to 1.0e-6f.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - First matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - Second matrix.

### Return value

1 if the m0 is equal to m1; otherwise, 0.
## int compare ( const dmat4 & m0 , const dmat4 & m1 , double epsilon )

Compares two matrices according to the specified degree of precision.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - First matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - Second matrix.
- *double* **epsilon** - Epsilon (degree of precision).

### Return value

1 if the m0 is equal to m1; otherwise, 0.
## quat conjugate ( const quat & q )

Returns the conjugate of a given quaternion.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Conjugate of a given quaternion.
## quat conjugate ( quat & ret , const quat & q )

Returns the conjugate of a given quaternion.
### Arguments

- *[quat](../../../api/library/math/class.quat_cpp.md) &* **ret** - Argument to store the result.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Conjugate of a given quaternion.
## float cross ( const vec2 & v0 , const vec2 & v1 )

Cross product of vectors.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.

### Return value

Cross product of the two 2d vectors: **v0.x * v1.y - v0.y*v1.x**.
## ivec3 cross ( const ivec3 & v0 , const ivec3 & v1 )

Cross product of vectors.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec3 cross ( const dvec3 & v0 , const dvec3 & v1 )

Cross product of vectors.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec3 cross ( const vec3 & v0 , const vec3 & v1 )

Cross product of vectors.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec3 & cross ( ivec3 & ret , const ivec3 & v0 , const ivec3 & v1 )

Cross product of vectors.
### Arguments

- *[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **ret** - Output vector, to which the resulting vector will be put.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec3 & cross ( vec3 & ret , const vec3 & v0 , const vec3 & v1 )

Cross product of vectors.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret** - Output vector, to which the resulting vector will be put.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec4 & cross ( vec4 & ret , const vec3 & v0 , const vec3 & v1 )

Cross product of vectors.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **ret** - Output vector, to which the resulting vector will be put.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec3 & cross ( dvec3 & ret , const dvec3 & v0 , const dvec3 & v1 )

Cross product of vectors.
### Arguments

- *[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret** - Output vector, to which the resulting vector will be put.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec4 & cross ( dvec4 & ret , const dvec3 & v0 , const dvec3 & v1 )

Cross product of vectors.
### Arguments

- *[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **ret** - Output vector, to which the resulting vector will be put.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## float * cross3 ( float *UNIGINE_RESTRICT ret , const float *UNIGINE_RESTRICT v0 , const float *UNIGINE_RESTRICT v1 )

Returns the cross product of three components of vectors by storing it in the array.
### Arguments

- *float *UNIGINE_RESTRICT* **ret** - Array to store the return value.
- *const float *UNIGINE_RESTRICT* **v0** - Pointer to vector.
- *const float *UNIGINE_RESTRICT* **v1** - Pointer to vector.

### Return value

Pointer to the array that stores the return value.
## float distance ( const vec2 & v0 , const vec2 & v1 )

Calculates the distance between the two given vectors. The distance is calculated as: **`length(v0 - v1)`**.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.

### Return value

Distance between the two given vectors.
## float distance ( const vec3 & v0 , const vec3 & v1 )

Calculates the distance between the two given vectors. The distance is calculated as: **`length(v0 - v1)`**.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Distance between the two given vectors.
## float distance ( const vec4 & v0 , const vec4 & v1 )

Calculates the distance between the two given vectors. The distance is calculated as: **`length(v0 - v1)`**.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

Distance between the two given vectors.
## float distance2 ( const vec2 & v0 , const vec2 & v1 )

Calculates the squared distance between the two given vectors. The squared distance is calculated as: **`length2(v0 - v1)`**. This method is much faster than *distance()* - the calculation is basically the same only without the slow Sqrt call. If you simply want to compare distances, then it is faster to compare squared distances against the squares of distances as the comparison gives the same result.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.

### Return value

Squared distance between the two given vectors.
## double distance2 ( const dvec2 & v0 , const dvec2 & v1 )

Calculates the squared distance between the two given vectors. The squared distance is calculated as: **`length2(v0 - v1)`**. This method is much faster than *distance()* - the calculation is basically the same only without the slow Sqrt call. If you simply want to compare distances, then it is faster to compare squared distances against the squares of distances as the comparison gives the same result.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second vector.

### Return value

Squared distance between the two given vectors.
## float distance2 ( const vec3 & v0 , const vec3 & v1 )

Calculates the squared distance between the two given vectors. The squared distance is calculated as: **`length2(v0 - v1)`**. This method is much faster than *distance()* - the calculation is basically the same only without the slow Sqrt call. If you simply want to compare distances, then it is faster to compare squared distances against the squares of distances as the comparison gives the same result.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Squared distance between the two given vectors.
## float distance2 ( const vec4 & v0 , const vec4 & v1 )

Calculates the squared distance between the two given vectors. The squared distance is calculated as: **`length2(v0 - v1)`**. This method is much faster than *distance()* - the calculation is basically the same only without the slow Sqrt call. If you simply want to compare distances, then it is faster to compare squared distances against the squares of distances as the comparison gives the same result.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

Squared distance between the two given vectors.
## float dot ( const vec2 & v0 , const vec2 & v1 )

Dot product of vectors.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## float dot ( const vec3 & v0 , const vec3 & v1 )

Dot product of vectors.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## double dot ( const dvec2 & v0 , const dvec2 & v1 )

Dot product of vectors.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## float dot ( const vec3 & v0 , const vec4 & v1 )

Dot product of vectors. In this case, w component of the four-component vector is added to the dot product of first three components of vectors.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## float dot ( const vec4 & v0 , const vec3 & v1 )

Dot product of vectors. In this case, w component of the four-component vector is added to the dot product of first three components of vectors.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## float dot ( const vec4 & v0 , const vec4 & v1 )

Dot product of vectors.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## int dot ( const ivec3 & v0 , const ivec3 & v1 )

Dot product of vectors.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## int dot ( const ivec2 & v0 , const ivec2 & v1 )

Dot product of vectors.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - First vector.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## int dot ( const ivec4 & v0 , const ivec3 & v1 )

Dot product of vectors. In this case, w component of the four-component vector is added to the dot product of first three components of vectors.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - First vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## int dot ( const ivec4 & v0 , const ivec4 & v1 )

Dot product of vectors.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - First vector.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## double dot ( const dvec3 & v0 , const dvec3 & v1 )

Dot product of vectors.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## double dot ( const dvec3 & v0 , const dvec4 & v1 )

Dot product of vectors. In this case, w component of the four-component vector is added to the dot product of first three components of vectors.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## double dot ( const dvec4 & v0 , const dvec3 & v1 )

Dot product of vectors. In this case, w component of the four-component vector is added to the dot product of first three components of vectors.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## double dot ( const dvec4 & v0 , const dvec4 & v1 )

Dot product of vectors.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## float dot2 ( const float * v , float x , float y )

Returns the dot product between a 2-component vector v and another 2-component vector defined by (x, y).
### Arguments

- *const float ** **v** - Pointer to the first vector.
- *float* **x** - X component of the second vector.
- *float* **y** - Y component of the second vector.

### Return value

Resulting scalar.
## double dot3 ( const dvec3 & v0 , const dvec4 & v1 )


Dot product of three components of vectors. *W* components of four-component vectors are ignored.


```cpp
float a = dot3(vec3(1, 2, 3), vec4(1, 2, 3, 4));
double b = dot3(dvec4(1, 2, 3, 4), dvec4(1, 2, 3, 4));
/*
result is:
a = 14.000000
b = 14.000000
*/

```


### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## double dot3 ( const dvec4 & v0 , const dvec3 & v1 )


Dot product of three components of vectors. *W* components of four-component vectors are ignored.


```cpp
float a = dot3(vec3(1, 2, 3), vec4(1, 2, 3, 4));
double b = dot3(dvec4(1, 2, 3, 4), dvec4(1, 2, 3, 4));
/*
result is:
a = 14.000000
b = 14.000000
*/

```


### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## double dot3 ( const dvec4 & v0 , const dvec4 & v1 )


Dot product of three components of vectors. *W* components of four-component vectors are ignored.


```cpp
float a = dot3(vec3(1, 2, 3), vec4(1, 2, 3, 4));
double b = dot3(dvec4(1, 2, 3, 4), dvec4(1, 2, 3, 4));
/*
result is:
a = 14.000000
b = 14.000000
*/

```


### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## float dot3 ( const vec3 & v0 , const vec4 & v1 )


Dot product of three components of vectors. *W* components of four-component vectors are ignored.


```cpp
float a = dot3(vec3(1, 2, 3), vec4(1, 2, 3, 4));
double b = dot3(dvec4(1, 2, 3, 4), dvec4(1, 2, 3, 4));
/*
result is:
a = 14.000000
b = 14.000000
*/

```


### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## float dot3 ( const vec4 & v0 , const vec3 & v1 )


Dot product of three components of vectors. *W* components of four-component vectors are ignored.


```cpp
float a = dot3(vec3(1, 2, 3), vec4(1, 2, 3, 4));
double b = dot3(dvec4(1, 2, 3, 4), dvec4(1, 2, 3, 4));
/*
result is:
a = 14.000000
b = 14.000000
*/

```


### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## float dot3 ( const vec4 & v0 , const vec4 & v1 )


Dot product of three components of vectors. *W* components of four-component vectors are ignored.


```cpp
float a = dot3(vec3(1, 2, 3), vec4(1, 2, 3, 4));
double b = dot3(dvec4(1, 2, 3, 4), dvec4(1, 2, 3, 4));
/*
result is:
a = 14.000000
b = 14.000000
*/

```


### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting scalar.
## float dot3 ( const float * v , float x , float y , float z )

Returns the dot product between a 3-component vector v and another 3-component vector defined by (x, y, z).
### Arguments

- *const float ** **v** - Pointer to the first vector.
- *float* **x** - X component of the second vector.
- *float* **y** - Y component of the second vector.
- *float* **z** - Z component of the second vector.

### Return value

Resulting scalar.
## float dtof ( double v )

Converts a double value to an integer value.
### Arguments

- *double* **v** - Double value.

### Return value

Float value.
## int dtoi ( double v )

Converts a double value to an integer value.
### Arguments

- *double* **v** - Double value.

### Return value

Integer value.
## long long dtol ( double v )

Converts a double value to a long value.
### Arguments

- *double* **v** - Double value.

### Return value

Long value.
## double floor ( double v )


Rounds an argument down to the nearest integer.


```text
float a = floor(2.3) // a = 2.0
```


### Arguments

- *double* **v** - Argument.

### Return value

Largest integer value not greater than *arg*.
## float floor ( float v )


Rounds an argument down to the nearest integer.


```text
double a = floor(2.3) // a = 2.0
```


### Arguments

- *float* **v** - Argument.

### Return value

Largest integer value not greater than *arg*.
## const vec2 & floor ( const vec2 & v )

Ceiling function that returns the vector storing the largest integer values that are not greater than the argument.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the largest integer values not greater than *v*.
## const vec3 & floor ( const vec3 & v )

Ceiling function that returns the vector storing the largest integer values that are not greater than the argument.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the largest integer values not greater than *v*.
## const vec4 & floor ( const vec4 & v )

Ceiling function that returns the vector storing the largest integer values that are not greater than the argument.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the largest integer values not greater than *v*.
## const dvec2 & floor ( const dvec2 & v )

Ceiling function that returns the vector storing the largest integer values that are not greater than the argument.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the largest integer values not greater than *v*.
## const dvec3 & floor ( const dvec3 & v )

Ceiling function that returns the vector storing the largest integer values that are not greater than the argument.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the largest integer values not greater than *v*.
## const dvec4 & floor ( const dvec4 & v )

Ceiling function that returns the vector storing the largest integer values that are not greater than the argument.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - Vector storing values.

### Return value

Vector storing the largest integer values not greater than *v*.
## int floorInt ( float v )

Returns the largest value that is less than or equal to the argument, stored as an integer.
### Arguments

- *float* **v** - Value.

### Return value

Resulting *int* value.
## int floorInt ( double v )

Returns the largest value that is less than or equal to the argument, stored as an integer.
### Arguments

- *double* **v** - Value.

### Return value

Resulting *int* value.
## float frac ( float v )


Returns the fractional part of the argument.


```text
float a = frac(3.141593); // a = 0.141593
```


### Arguments

- *float* **v** - Argument.

### Return value

Fractional part of the argument.
## double frac ( double v )


Returns the fractional part of the argument.


```text
double a = frac(3.141593); // a = 0.141593
```


### Arguments

- *double* **v** - Argument.

### Return value

Fractional part of the argument.
## vec3 frac ( const vec3 & v )

Returns the fractional part every component of the argument.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Argument.

### Return value

Fractional part of every component of the argument.
## vec4 frac ( const vec4 & v )

Returns the fractional part every component of the argument.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - Argument.

### Return value

Fractional part of every component of the argument.
## char ftoc ( float v )

Converts a float value to a char value.
### Arguments

- *float* **v** - Float value.

### Return value

Char value.
## int ftoi ( float v )

Converts a float value to an integer value.
### Arguments

- *float* **v** - Float value.

### Return value

Integer value.
## long long ftol ( float v )

Converts a float value to a long value.
### Arguments

- *float* **v** - Float value.

### Return value

Long value.
## float getAngle ( const quat & q0 , const quat & q1 )

Returns the angle (in degrees) between the given first and second quaternions. The angle returned is the unsigned acute angle between the two quaternions. This means the smaller of the two possible angles is used.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q0** - First quaternion (from which the angular difference is measured).
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q1** - Second quaternion (to which the angular difference is measured).

### Return value

Angle between the given quaternions, in degrees within the range [0.0; 180.0].
## float getAngle ( const vec3 & v0 , const vec3 & v1 )

Returns the angle (in degrees) between the given first and second vectors. The angle returned is the unsigned acute angle between the two vectors. This means the smaller of the two possible angles is used.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector (from which the angular difference is measured).
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector (to which the angular difference is measured).

### Return value

Angle between the given vectors, in degrees within the range [0.0; 180.0].
## float getAngle ( const vec3 & v0 , const vec3 & v1 , const vec3 & up )

Returns the signed angle (in degrees) between the given first and second vectors relative to the specified "up" vector.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector (from which the angular difference is measured).
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector (to which the angular difference is measured).
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **up** - Up vector, around which the other two vectors are rotated.

### Return value

Angle between the given vectors, in degrees within the range [-180.0; 180.0].
## bool getBit ( Type value , int bit )

Extracts a specific bit from an integer value and returns it as a boolean.
### Arguments

- *Type* **value** - Value.
- *int* **bit** - The bit of the value.

### Return value

true if the specified bit in the value is set, othewise false.
## float gradient4 ( float x , const vec4 & gradient )


Returns a gradient value for the specified argument using four key components. The gradient value is determined as follows:


```text
smoothstep(gradient.x, gradient.y, x) - smoothstep(gradient.z, gradient.w, x);
```


See the [smoothstep()](#smoothstep_float_float_float_float) method.


### Arguments

- *float* **x** - Argument.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **gradient** - Vector with four key components.

### Return value

Gradient value.
## unsigned int hashInteger ( unsigned int v )

Computes a 32-bit hash value from an input value.
### Arguments

- *unsigned int* **v** - Input value.

### Return value

Hash value.
## unsigned int hashInteger ( float v )

Computes a 32-bit hash value from an input value.
### Arguments

- *float* **v** - Input value.

### Return value

Hash value.
## unsigned int hashInteger ( int v )

Computes a 32-bit hash value from an input value.
### Arguments

- *int* **v** - Input value.

### Return value

Hash value.
## unsigned long long hashInteger ( unsigned long long v )

Computes a 64-bit hash value from an input value.
### Arguments

- *unsigned long long* **v** - Input value.

### Return value

Hash value.
## unsigned long long hashInteger ( double v )

Computes a 64-bit hash value from an input value.
### Arguments

- *double* **v** - Input value.

### Return value

Hash value.
## unsigned long long hashInteger ( long long v )

Computes a 64-bit hash value from an input value.
### Arguments

- *long long* **v** - Input value.

### Return value

Hash value.
## unsigned int hashMixer ( unsigned int hash_0 , unsigned int hash_1 )

Mixes two hash values.
### Arguments

- *unsigned int* **hash_0** - Input value.
- *unsigned int* **hash_1** - Input value.

### Return value

Mixed hash.
## unsigned long long hashMixer ( unsigned long long hash_0 , unsigned long long hash_1 )

Mixes two hash values.
### Arguments

- *unsigned long long* **hash_0** - Input value.
- *unsigned long long* **hash_1** - Input value.

### Return value

Mixed hash.
## unsigned int hashCombine ( unsigned int hash , unsigned int value )

Returns a hash obtained by mixing the hash provided as an argument with a hash obtained for the specified value.
### Arguments

- *unsigned int* **hash** - Input hash.
- *unsigned int* **value** - Input value.

### Return value

Combined hash value.
## unsigned int hashCombine ( unsigned int hash , float value )

Returns a hash obtained by mixing the hash provided as an argument with a hash obtained for the specified value.
### Arguments

- *unsigned int* **hash** - Input hash.
- *float* **value** - Input value.

### Return value

Combined hash value.
## unsigned int hashCombine ( unsigned int hash , int value )

Returns a hash obtained by mixing the hash provided as an argument with a hash obtained for the specified value.
### Arguments

- *unsigned int* **hash** - Input hash.
- *int* **value** - Input value.

### Return value

Combined hash value.
## unsigned long long hashCombine ( unsigned long long hash , unsigned long long value )

Returns a hash obtained by mixing the hash provided as an argument with a hash obtained for the specified value.
### Arguments

- *unsigned long long* **hash** - Input hash.
- *unsigned long long* **value** - Input value.

### Return value

Combined hash value.
## unsigned long long hashCombine ( unsigned long long hash , double value )

Returns a hash obtained by mixing the hash provided as an argument with a hash obtained for the specified value.
### Arguments

- *unsigned long long* **hash** - Input hash.
- *double* **value** - Input value.

### Return value

Combined hash value.
## unsigned long long hashCombine ( unsigned long long hash , long long value )

Returns a hash obtained by mixing the hash provided as an argument with a hash obtained for the specified value.
### Arguments

- *unsigned long long* **hash** - Input hash.
- *long long* **value** - Input value.

### Return value

Combined hash value.
## unsigned int hashCast64To32 ( unsigned long long value )

Casts the 64-bit hash value to the 32-bit hash value.
### Arguments

- *unsigned long long* **value** - Input 64-bit hash value.

### Return value

32-bit hash value.
## quat inverse ( const quat & q )

Returns inverse of the quaternion.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Return value.
## quat & inverse ( quat & ret , const quat & q )

Returns inverse of the quaternion.
### Arguments

- *[quat](../../../api/library/math/class.quat_cpp.md) &* **ret** - Argument to store the output.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Return value.
## float inverseLerp ( float v0 , float v1 , float v )

Returns the value calculated according to the following formula: (v - v0) / (v1 - v0) clamped within 0.0f and 1.0f.
### Arguments

- *float* **v0** - The value specifying the beginning of the interval.
- *float* **v1** - The value specifying the ending of the interval.
- *float* **v** - The value within the specified interval.

### Return value

Coefficient of the value within a specified interval.
## double inverseLerp ( double v0 , double v1 , double v )

Returns the value calculated according to the following formula: (v - v0) / (v1 - v0) clamped within 0.0 and 1.0.
### Arguments

- *double* **v0** - The value specifying the beginning of the interval.
- *double* **v1** - The value specifying the ending of the interval.
- *double* **v** - The value within the specified interval.

### Return value

Coefficient of the value within a specified interval.
## vec2 inverseLerp ( const vec2 & v0 , const vec2 & v1 , const vec2 & v )

Returns the vector with two float values calculated according to the following formula: (v - v0) / (v1 - v0) clamped within 0.0f and 1.0f.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - Vector storing the values that specify the beginnings of the intervals.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Vector storing the values that specify the endings of the intervals.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - The values within the specified intervals.

### Return value

Coefficients of the values within a specified intervals.
## vec3 inverseLerp ( const vec3 & v0 , const vec3 & v1 , const vec3 & v )

Returns the vector with three float values calculated according to the following formula: (v - v0) / (v1 - v0) clamped within 0.0f and 1.0f.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Vector storing the values that specify the beginnings of the intervals.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Vector storing the values that specify the endings of the intervals.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The values within the specified intervals.

### Return value

Coefficients of the values within a specified intervals.
## vec4 inverseLerp ( const vec4 & v0 , const vec4 & v1 , const vec4 & v )

Returns the vector with four float values calculated according to the following formula: (v - v0) / (v1 - v0) clamped within 0.0f and 1.0f.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - Vector storing the values that specify the beginnings of the intervals.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Vector storing the values that specify the endings of the intervals.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The values within the specified intervals.

### Return value

Coefficients of the values within a specified intervals.
## dvec2 inverseLerp ( const dvec2 & v0 , const dvec2 & v1 , const dvec2 & v )

Returns the vector with two double values calculated according to the following formula: (v - v0) / (v1 - v0) clamped within 0.0 and 1.0.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - Vector storing the values that specify the beginnings of the intervals.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Vector storing the values that specify the endings of the intervals.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The values within the specified intervals.

### Return value

Coefficients of the values within a specified intervals.
## dvec3 inverseLerp ( const dvec3 & v0 , const dvec3 & v1 , const dvec3 & v )

Returns the vector with three double values calculated according to the following formula: (v - v0) / (v1 - v0) clamped within 0.0 and 1.0.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - Vector storing the values that specify the beginnings of the intervals.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Vector storing the values that specify the endings of the intervals.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The values within the specified intervals.

### Return value

Coefficients of the values within a specified intervals.
## vec4 inverseLerp ( const dvec4 & v0 , const dvec4 & v1 , const dvec4 & v )

Returns the vector with four double values calculated according to the following formula: (v - v0) / (v1 - v0) clamped within 0.0 and 1.0.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - Vector storing the values that specify the beginnings of the intervals.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Vector storing the values that specify the endings of the intervals.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The values within the specified intervals.

### Return value

Coefficients of the values within a specified intervals.
## vec4 contrastLerp ( vec4 & point_a , vec4 & point_b , float coef_min_bound , float coef_max_bound , float coef )

Performs a smooth interpolation between two vectors (point_a and point_b) using a specified coefficient range to create a smooth transition effect.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **point_a** - Vector.
- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **point_b** - Vector.
- *float* **coef_min_bound** - The minimum value defining the range of the coefficient for the smoothstep function, creating a softened transition over the range.
- *float* **coef_max_bound** - The maximum value defining the range of the coefficient for the smoothstep function, creating a softened transition over the range.
- *float* **coef** - The coefficient value that determines the interpolation position between vectors.

### Return value

.
## bool isFinite ( float x )

Returns a value indicating that the given value is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *float* **x** - Value.

### Return value

true if the argument is a finite number; otherwise, false.
## bool isFinite ( double x )

Returns a value indicating that the given value is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *double* **x** - Value.

### Return value

true if the argument is a finite number; otherwise, false.
## bool isFinite ( Vector2 v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *Vector2* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isFinite ( Vector3 v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *Vector3* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isFinite ( Vector4 v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *Vector4* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isFinite ( vec2 v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md)* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isFinite ( vec3 v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md)* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isFinite ( vec4 v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md)* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isFinite ( quat v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *[quat](../../../api/library/math/class.quat_cpp.md)* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isFinite ( dvec2 v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *[dvec2](../../../api/library/math/class.dvec2_cpp.md)* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isFinite ( dvec3 v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *[dvec3](../../../api/library/math/class.dvec3_cpp.md)* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isFinite ( dvec4 v )

Returns a value indicating that any component of the argument is a finite number, meaning it is neither NaN nor infinity (positive or negative).
### Arguments

- *[dvec4](../../../api/library/math/class.dvec4_cpp.md)* **v** - Value.

### Return value

true if any component of the argument is a finite number; otherwise, false.
## bool isInf ( float x )

Returns a value indicating whether the argument evaluates to negative or positive infinity.
### Arguments

- *float* **x** - Value.

### Return value

true if the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( double x )

Returns a value indicating whether the argument evaluates to negative or positive infinity.
### Arguments

- *double* **x** - Value.

### Return value

true if the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( Vector2 v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *Vector2* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( Vector3 v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *Vector3* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( Vector4 v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *Vector4* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( vec2 v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md)* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( vec3 v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md)* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( vec4 v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md)* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( quat v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *[quat](../../../api/library/math/class.quat_cpp.md)* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( dvec2 v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *[dvec2](../../../api/library/math/class.dvec2_cpp.md)* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( dvec3 v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *[dvec3](../../../api/library/math/class.dvec3_cpp.md)* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isInf ( dvec4 v )

Returns a value indicating whether any component of the argument evaluates to negative or positive infinity.
### Arguments

- *[dvec4](../../../api/library/math/class.dvec4_cpp.md)* **v** - Value.

### Return value

true if any component of the argument evaluates to negative or positive infinity; otherwise, false.
## bool isNan ( float v )

Returns a value that indicates whether the argument is not a number (NaN).
### Arguments

- *float* **v** - Value.

### Return value

true if the argument is not a number (NaN); otherwise, false.
## bool isNan ( double v )

Returns a value that indicates whether the argument is not a number (NaN).
### Arguments

- *double* **v** - Value.

### Return value

true if the argument is not a number (NaN); otherwise, false.
## bool isNan ( Vector2 v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *Vector2* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## bool isNan ( Vector3 v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *Vector3* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## bool isNan ( Vector4 v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *Vector4* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## bool isNan ( vec2 v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *[vec2](../../../api/library/math/class.vec2_cpp.md)* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## bool isNan ( vec3 v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *[vec3](../../../api/library/math/class.vec3_cpp.md)* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## bool isNan ( vec4 v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md)* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## bool isNan ( quat v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *[quat](../../../api/library/math/class.quat_cpp.md)* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## bool isNan ( dvec2 v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *[dvec2](../../../api/library/math/class.dvec2_cpp.md)* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## bool isNan ( dvec3 v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *[dvec3](../../../api/library/math/class.dvec3_cpp.md)* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## bool isNan ( dvec4 v )

Returns a value that indicates whether the argument contains at least one component, which is not a number (NaN).
### Arguments

- *[dvec4](../../../api/library/math/class.dvec4_cpp.md)* **v** - Value.

### Return value

true if the argument contains at least one component, which is not a number (NaN); otherwise, false.
## float isrgb ( float x )

Converts sRGB color value to RGB format.
### Arguments

- *float* **x** - sRGB value to convert.

### Return value

RGB color value.
## vec2 isrgb ( const vec2 & color )

Converts sRGB color value to RGB format.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **color** - sRGB value to convert.

### Return value

RGB color value.
## vec3 isrgb ( const vec3 & color )

Converts sRGB color value to RGB format.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **color** - sRGB value to convert.

### Return value

RGB color value.
## vec4 isrgb ( const vec4 & color )

Converts sRGB color value and alpha to RGB format.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - sRGB value to convert.

### Return value

RGB color value.
## vec4 isrgbColor ( const vec4 & color )

Converts sRGB color value to RGB format without converting alpha.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - sRGB value to convert.

### Return value

RGB color value.
## double itod ( int v )

Converts an integer value to a double value.
### Arguments

- *int* **v** - Integer value.

### Return value

Double value.
## float itof ( int v )

Converts an integer value to a float value.
### Arguments

- *int* **v** - Integer value.

### Return value

Float value.
## Scalar itos ( int v )

Converts an integer value to a scalar value (float or double, depending on the precision).
### Arguments

- *int* **v** - Integer value.

### Return value

Scalar value (float or double, depending on the precision).
## float length ( const vec2 & v )

Calculates the length of a given vector.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - Vector.

### Return value

Vector length.
## double length ( const dvec2 & v )

Calculates the length of a given vector.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - Vector.

### Return value

Vector length.
## float length ( const vec3 & v )

Calculates the length of a given vector.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Vector.

### Return value

Vector length.
## double length ( const dvec3 & v )

Calculates the length of a given vector.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Vector.

### Return value

Vector length.
## float length ( const vec4 & v )

Calculates the length of a given vector.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - Vector.

### Return value

Vector length.
## double length ( const dvec4 & v )

Calculates the length of a given vector.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - Vector.

### Return value

Vector length.
## float length2 ( const vec2 & v )

Calculates the squared length of a given vector. This method is much faster than [length()](#length_const_vec2_ref_float) - the calculation is basically the same only without the slow Sqrt call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - Vector.

### Return value

Squared length of the vector (X 2 + Y 2 + Z 2).
## double length2 ( const dvec2 & v )

Calculates the squared length of a given vector. This method is much faster than [length()](#length_const_dvec2_ref_double) - the calculation is basically the same only without the slow Sqrt call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - Vector.

### Return value

Squared length of the vector (X 2 + Y 2 + Z 2).
## int length2 ( const ivec2 & v )

Calculates the squared length of a given vector. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v** - Vector.

### Return value

Squared length of the vector (X 2 + Y 2 + Z 2).
## float length2 ( const vec3 & v )

Calculates the squared length of a given vector. This method is much faster than [length()](#length_const_vec3_ref_float) - the calculation is basically the same only without the slow Sqrt call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Vector.

### Return value

Squared length of the vector (X 2 + Y 2 + Z 2).
## double length2 ( const dvec3 & v )

Calculates the squared length of a given vector. This method is much faster than [length()](#length_const_dvec3_ref_double) - the calculation is basically the same only without the slow Sqrt call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Vector.

### Return value

Squared length of the vector (X 2 + Y 2 + Z 2).
## int length2 ( const ivec3 & v )

Calculates the squared length of a given vector. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v** - Vector.

### Return value

Squared length of the vector (X 2 + Y 2 + Z 2).
## float length2 ( const vec4 & v )

Calculates the squared length of a given vector. This method is much faster than [length()](#length_const_vec4_ref_float) - the calculation is basically the same only without the slow Sqrt call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - Vector.

### Return value

Squared length of the vector (X 2 + Y 2 + Z 2).
## double length2 ( const dvec4 & v )

Calculates the squared length of a given vector. This method is much faster than [length()](#length_const_dvec4_ref_double) - the calculation is basically the same only without the slow Sqrt call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - Vector.

### Return value

Squared length of the vector (X 2 + Y 2 + Z 2).
## int length2 ( const ivec4 & v )

Calculates the squared length of a given vector. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v** - Vector.

### Return value

Squared length of the vector (X 2 + Y 2 + Z 2).
## float lerp ( float v0 , float v1 , float k )

Returns the interpolated value according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *float* **v0** - First float value.
- *float* **v1** - Second float value.
- *float* **k** - Interpolation coefficient.

### Return value

Interpolated value.
## double lerp ( double v0 , double v1 , double k )

Returns the interpolated value according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *double* **v0** - First double value.
- *double* **v1** - Second double value.
- *double* **k** - Interpolation coefficient.

### Return value

Interpolated value.
## int lerp ( int v0 , int v1 , int k )

Returns the interpolated value according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *int* **v0** - First int value.
- *int* **v1** - Second int value.
- *int* **k** - Interpolation coefficient.

### Return value

Interpolated value.
## long long lerp ( long long v0 , long long v1 , long long k )

Returns the interpolated value according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *long long* **v0** - First long long value.
- *long long* **v1** - Second long long value.
- *long long* **k** - Interpolation coefficient.

### Return value

Interpolated value.
## const vec2 & lerp ( const vec2 & v0 , const vec2 & v1 , float k )

Returns the interpolated vector according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.
- *float* **k** - Interpolation coefficient.

### Return value

Interpolated vector.
## vec3 lerp ( const vec3 & v0 , const vec3 & v1 , float k )

Returns the interpolated vector according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.
- *float* **k** - Interpolation coefficient.

### Return value

Interpolated vector.
## vec4 lerp ( const vec4 & v0 , const vec4 & v1 , float k )

Returns the interpolated vector according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.
- *float* **k** - Interpolation coefficient.

### Return value

Interpolated vector.
## dvec2 lerp ( const dvec2 & v0 , const dvec2 & v1 , double k )

Returns the interpolated vector according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second vector.
- *double* **k** - Interpolation coefficient.

### Return value

Interpolated vector.
## dvec3 lerp ( const dvec3 & v0 , const dvec3 & v1 , double k )

Returns the interpolated vector according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.
- *double* **k** - Interpolation coefficient.

### Return value

Interpolated vector.
## dvec4 lerp ( const dvec4 & v0 , const dvec4 & v1 , double k )

Returns the interpolated vector according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.
- *double* **k** - Interpolation coefficient.

### Return value

Interpolated vector.
## ivec2 lerp ( const ivec2 & v0 , const ivec2 & v1 , int k )

Returns the interpolated vector according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - First vector.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Second vector.
- *int* **k** - Interpolation coefficient.

### Return value

Interpolated vector.
## ivec3 lerp ( const ivec3 & v0 , const ivec3 & v1 , int k )

Returns the interpolated vector according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second vector.
- *int* **k** - Interpolation coefficient.

### Return value

Interpolated vector.
## ivec4 lerp ( const ivec4 & v0 , const ivec4 & v1 , int k )

Returns the interpolated vector according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - First vector.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - Second vector.
- *int* **k** - Interpolation coefficient.

### Return value

Interpolated vector.
## mat4 & lerp ( mat4 & ret , const mat4 & m0 , const mat4 & m1 , float k )

Returns the interpolated matrix according to the following formula: **m0 + (m 1 - m 0) * k**.
### Arguments

- *[mat4](../../../api/library/math/class.mat4_cpp.md) &* **ret** - The matrix to store the result.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m1** - The value of the second matrix.
- *float* **k** - Interpolation coefficient.

### Return value

The resulting matrix.
## dmat4 & lerp ( dmat4 & ret , const dmat4 & m0 , const dmat4 & m1 , double k )

Returns the interpolated matrix according to the following formula: **m0 + (m 1 - m 0) * k**.
### Arguments

- *[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ret** - The matrix to store the result.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.
- *double* **k** - Interpolation coefficient.

### Return value

The resulting matrix.
## dmat4 lerp ( const dmat4 & m0 , const dmat4 & m1 , double k )

Returns the interpolated matrix according to the following formula: **m0 + (m 1 - m 0) * k**.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.
- *double* **k** - Interpolation coefficient.

### Return value

The resulting matrix.
## Type lerp ( Type v0 , Type v1 , Type k )

Returns the interpolated value according to the following formula: **v0 + (v 1 - v 0) * k**.
### Arguments

- *Type* **v0** - First value.
- *Type* **v1** - Second value.
- *Type* **k** - Interpolation coefficient.

### Return value

Interpolated value.
## float lerpOne ( float v0 , float k )

Performs the interpolation: v0 * (1.0f - k) + k.
### Arguments

- *float* **v0** - Value for interpolation.
- *float* **k** - Interpolation coefficient.

### Return value

Interpolated value.
## double lerpOne ( double v0 , double k )

Performs the interpolation: v0 * (1.0f - k) + k.
### Arguments

- *double* **v0** - Value for interpolation.
- *double* **k** - Interpolation coefficient.

### Return value

Interpolated value.
## float lerpZero ( float v0 , float k )

Performs the interpolation of the following type: v0 * (1.0f - k).
### Arguments

- *float* **v0** - Value for interpolation.
- *float* **k** - Interpolation coefficient.

### Return value

Interpolated value.
## double lerpZero ( double v0 , double k )

Performs the interpolation of the following type: v0 * (1.0f - k).
### Arguments

- *double* **v0** - Value for interpolation.
- *double* **k** - Interpolation coefficient.

### Return value

Interpolated value.
## vec4 & lerp3 ( vec4 & v0 , vec4 & v1 , vec4 & v2 , float k )

Performs linear interpolation between three vectors.
### Arguments

- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.
- *[vec4](../../../api/library/math/class.vec4_cpp.md) &* **v2** - Third vector.
- *float* **k** - Interpolation coefficient in the range [0.0f, 1.0f].

### Return value

Interpolated vector.
## float ltof ( long long v )

Converts a long value to a float value.
### Arguments

- *long long* **v** - Long value.

### Return value

Float value.
## double ltod ( long long v )

Converts a long value to a double value.
### Arguments

- *long long* **v** - Long value.

### Return value

Double value.
## float logit ( float x )

Returns the logit of the argument - the inverse of the logistic sigmoid: **ln(x / (1 - x))**.
### Arguments

- *float* **x** - Argument, expected to be in the range of **0.0** to **1.0**, exclusive.

### Return value

Logit of the argument.
## double logit ( double x )

Returns the logit of the argument - the inverse of the logistic sigmoid: **ln(x / (1 - x))**.
### Arguments

- *double* **x** - Argument, expected to be in the range of **0.0** to **1.0**, exclusive.

### Return value

Logit of the argument.
## float max ( float v0 , float v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *float* **v0** - First value.
- *float* **v1** - Second value.

### Return value

Maximum value.
## double max ( double v0 , double v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *double* **v0** - First value.
- *double* **v1** - Second value.

### Return value

Maximum value.
## int max ( int v0 , int v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *int* **v0** - First value.
- *int* **v1** - Second value.

### Return value

Maximum value.
## long long max ( long long v0 , long long v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *long long* **v0** - First value.
- *long long* **v1** - Second value.

### Return value

Maximum value.
## vec2 max ( const vec2 & v0 , const vec2 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First value.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## vec3 max ( const vec3 & v0 , const vec3 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First value.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## vec4 max ( const vec4 & v0 , const vec4 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First value.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## dvec2 max ( const dvec2 & v0 , const dvec2 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First value.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## dvec3 max ( const dvec3 & v0 , const dvec3 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First value.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## dvec4 max ( const dvec4 & v0 , const dvec4 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First value.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## ivec2 max ( const ivec2 & v0 , const ivec2 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - First value.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## ivec3 max ( const ivec3 & v0 , const ivec3 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First value.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## ivec4 max ( const ivec4 & v0 , const ivec4 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - First value.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## bvec4 max ( const bvec4 & v0 , const bvec4 & v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - First value.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - Second value.

### Return value

Maximum value.
## Type max ( Type v0 , Type v1 )

Compares the arguments and returns the maximum value.
### Arguments

- *Type* **v0** - First value.
- *Type* **v1** - Second value.

### Return value

Maximum value.
## float min ( float v0 , float v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *float* **v0** - First value.
- *float* **v1** - Second value.

### Return value

Minimum value.
## double min ( double v0 , double v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *double* **v0** - First value.
- *double* **v1** - Second value.

### Return value

Minimum value.
## int min ( int v0 , int v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *int* **v0** - First value.
- *int* **v1** - Second value.

### Return value

Minimum value.
## long long min ( long long v0 , long long v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *long long* **v0** - First value.
- *long long* **v1** - Second value.

### Return value

Minimum value.
## vec2 min ( const vec2 & v0 , const vec2 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First value.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## vec3 min ( const vec3 & v0 , const vec3 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First value.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## vec4 min ( const vec4 & v0 , const vec4 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First value.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## dvec2 min ( const dvec2 & v0 , const dvec2 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First value.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## dvec3 min ( const dvec3 & v0 , const dvec3 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First value.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## dvec4 min ( const dvec4 & v0 , const dvec4 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First value.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## ivec2 min ( const ivec2 & v0 , const ivec2 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - First value.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## ivec3 min ( const ivec3 & v0 , const ivec3 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First value.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## ivec4 min ( const ivec4 & v0 , const ivec4 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - First value.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## bvec4 min ( const bvec4 & v0 , const bvec4 & v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - First value.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - Second value.

### Return value

Minimum value.
## Type min ( Type v0 , Type v1 )

Compares the arguments and returns the minimum value.
### Arguments

- *Type* **v0** - First value.
- *Type* **v1** - Second value.

### Return value

Minimum value.
## float * mul3 ( float *UNIGINE_RESTRICT ret , const float *UNIGINE_RESTRICT v0 , float v1 )

Returns the result of a componentwise multiplication of a 3-component vector with a scalar value.
### Arguments

- *float *UNIGINE_RESTRICT* **ret** - Array to store the return value.
- *const float *UNIGINE_RESTRICT* **v0** - 3-component vector.
- *float* **v1** - Scalar value.

### Return value

Pointer to the array that stores the return value.
## quat normalize ( const quat & v )

Normalizes a quaternion, makes its magnitude equal to 1. When normalized, a quaternion keeps the same oreintation but its magnitude is equal to 1.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **v** - A [quaternion](../../../api/library/math/class.quat_cpp.md) to be normalized.

### Return value

Normalized quaternion.
## vec2 normalize ( const vec2 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - A two-component [vec2](../../../api/library/math/class.vec2_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## vec3 normalize ( const vec3 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - A three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## vec4 normalize ( const vec4 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - A four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## dvec2 normalize ( const dvec2 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - A two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## dvec3 normalize ( const dvec3 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - A three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## dvec4 normalize ( const dvec4 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - A four-component [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## float normalizeAngle ( float angle )

Normalizes an input angle to the range (−180, 180).
### Arguments

- *float* **angle** - Angle value, in degrees.

### Return value

Normalized angle value, in degrees.
## quat normalizeValid ( const quat & v )

Normalizes a quaternion, makes its magnitude equal to 1. When normalized, a quaternion keeps the same oreintation but its magnitude is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **v** - A [quaternion](../../../api/library/math/class.quat_cpp.md) to be normalized.

### Return value

Normalized quaternion.
## vec2 normalizeValid ( const vec2 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - A two-component [vec2](../../../api/library/math/class.vec2_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## vec3 normalizeValid ( const vec3 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - A three-component [vec3](../../../api/library/math/class.vec3_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## vec4 normalizeValid ( const vec4 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - A four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## dvec2 normalizeValid ( const dvec2 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - A two-component [dvec2](../../../api/library/math/class.dvec2_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## dvec3 normalizeValid ( const dvec3 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - A three-component [dvec3](../../../api/library/math/class.dvec3_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## dvec4 normalizeValid ( const dvec4 & v )

Normalizes a vector, makes its magnitude equal to 1. When normalized, a vector keeps the same direction but its length is equal to 1. Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - A four-component [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## void normalize2 ( float * v )

Normalizes a 2-component vector, making it a unit vector (a vector with a length of 1) while preserving its direction.
### Arguments

- *float ** **v** - Pointer to the vector.

## void normalize3 ( float * v )

Normalizes a 3-component vector, making it a unit vector (a vector with a length of 1) while preserving its direction.
### Arguments

- *float ** **v** - Pointer to the vector.

## vec4 normalize3 ( const vec4 & v )

Normalizes a vector making its magnitude equal to 1. The vector is normalized as if it has only the first three components (the fourth one is ignored).
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - A four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## dvec4 normalize3 ( const dvec4 & v )

Normalizes a vector making its magnitude equal to 1. The vector is normalized as if it has only the first three components (the fourth one is ignored).
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - A four-component [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## vec4 normalizeValid3 ( const vec4 & v )

Normalizes a vector making its magnitude equal to 1. The vector is normalized as if it has only the first three components (the fourth one is ignored). Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - A four-component [vec4](../../../api/library/math/class.vec4_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## dvec4 normalizeValid3 ( const dvec4 & v )

Normalizes a vector making its magnitude equal to 1. The vector is normalized as if it has only the first three components (the fourth one is ignored). Check for the zero vector is performed: if the argument is a zero vector, then a zero vector is returned.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - A four-component [dvec4](../../../api/library/math/class.dvec4_cpp.md) vector to be normalized.

### Return value

Normalized vector.
## int npot ( int arg )

Rounds up to the nearest power of two value.
### Arguments

- *int* **arg** - Argument.

### Return value

The nearest upper power of 2 number.
## int ispot ( int v )

Checks if the argument value is a power of two by using bitwise operations. Doesn't check the zero value.
### Arguments

- *int* **v** - Argument value.

### Return value

1 if the value is a power of two; otherwise, 0.
## int isqrt ( int v )

Returns the integer square root of the argument value by using bitwise operations.
### Arguments

- *int* **v** - Argument value.

### Return value

Integer square root of the value.
## float overlay ( float a , float b , float x )

Performs overlay A over B with blending coefficient.
### Arguments

- *float* **a**
- *float* **b**
- *float* **x** - Blending coefficient.

### Return value

Resulting value.
## float rcp ( float v )

Returns the reciprocal of the specified argument.
### Arguments

- *float* **v** - Argument.

### Return value

Reciprocal of the argument.
## double rcp ( double v )

Returns the reciprocal of the specified argument.
### Arguments

- *double* **v** - Argument.

### Return value

Reciprocal of the argument.
## float rcpFast ( float v )

Returns the approximated (quicker calculated) reciprocal of the specified argument.
### Arguments

- *float* **v** - Argument.

### Return value

Reciprocal of the argument.
## float rerange ( float in , float in_range_min , float in_range_max , float out_range_min , float out_range_max )

Returns the value that corresponds to the input value remapped within the limits of the output range.
### Arguments

- *float* **in** - Input value.
- *float* **in_range_min** - Minimum value of the input range.
- *float* **in_range_max** - Maximum value of the input range.
- *float* **out_range_min** - Minimum value of the output range.
- *float* **out_range_max** - Maximum value of the output range.

### Return value

Output value that corresponds to the input value remapped in the output range.
## double rerange ( double in , double in_range_min , double in_range_max , double out_range_min , double out_range_max )

Returns the value that corresponds to the input value remapped within the limits of the output range.
### Arguments

- *double* **in** - Input value.
- *double* **in_range_min** - Minimum value of the input range.
- *double* **in_range_max** - Maximum value of the input range.
- *double* **out_range_min** - Minimum value of the output range.
- *double* **out_range_max** - Maximum value of the output range.

### Return value

Output value that corresponds to the input value remapped in the output range.
## unsigned int reverseBits ( unsigned int value )

Returns the value with the reversed order of the bits.
### Arguments

- *unsigned int* **value** - Value to be converted.

### Return value

Resulting value.
## mat4 rotate ( const quat & q )

Returns a resulting matrix for rotation by the specified angle around the axis specified as a quaternion/vector/vector components.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Resulting rotation matrix.
## mat3 rotate3 ( const quat & q )

Returns a resulting matrix for rotation by the specified angle around the axis specified as a quaternion/vector/vector components. The resulting matrix size for this method is **3 x 3**.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - Quaternion.

### Return value

Resulting rotation matrix.
## double round ( double v )


Rounds an argument to the nearest integer value.


> **Notice:** In halfway cases, when an argument has a fractional part of exactly 0.5, the function rounds away from zero to the integer with larger magnitude.
>
>
> - 3.5 -> 4
> - - 3.5 -> - 4


```text
double a = round(2.3) 					// a = 2.0
double b = round(5.5) 					// b = 6.0
double c = round(-5.5) 					// c = -6.0

```


### Arguments

- *double* **v** - Argument.

### Return value

Nearest integer value to the argument.
## float round ( float v )


Rounds an argument to the nearest integer value.


> **Notice:** In halfway cases, when an argument has a fractional part of exactly 0.5, the function rounds away from zero to the integer with larger magnitude.
>
>
> - 3.5 -> 4
> - - 3.5 -> - 4


```text
float a = round(2.3) 					// a = 2.0
float b = round(5.5) 					// b = 6.0
float c = round(-5.5) 					// c = -6.0

```


### Arguments

- *float* **v** - Argument.

### Return value

Nearest integer value to the argument.
## int roundFast ( float v )


Rounds an argument to the nearest integer value by adding 0.5 to the argument and discarding the decimal part.


> **Notice:** This method works for positive numbers but has limitations for negative numbers because it doesn't handle rounding in the traditional way for negative values.


### Arguments

- *float* **v** - Argument.

### Return value

Nearest integer value to the argument.
## float saturate ( float v )

Clamps the value within the range of **0.0** to **1.0**.
### Arguments

- *float* **v** - Argument.

### Return value

Argument value clamped within the range of **0.0** to **1.0**.
## double saturate ( double v )

Clamps the value within the range of **0.0** to **1.0**.
### Arguments

- *double* **v** - Argument.

### Return value

Argument value clamped within the range of **0.0** to **1.0**.
## dvec2 saturate ( const dvec2 & v )

Clamps the values of vector components within the range of **0.0** to **1.0**.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v**

## vec2 saturate ( const vec2 & v )

Clamps the values of vector components within the range of **0.0** to **1.0**.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - Vector.

### Return value

Vector with components clamped within the range of **0.0** to **1.0**.
## dvec3 saturate ( const dvec3 & v )

Clamps the values of vector components within the range of **0.0** to **1.0**.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Vector.

### Return value

Vector with components clamped within the range of **0.0** to **1.0**.
## vec3 saturate ( const vec3 & v )

Clamps the values of vector components within the range of **0.0** to **1.0**.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Vector.

### Return value

Vector with components clamped within the range of **0.0** to **1.0**.
## dvec4 saturate ( const dvec4 & v )

Clamps the values of vector components within the range of **0.0** to **1.0**.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - Vector.

### Return value

Vector with components clamped within the range of **0.0** to **1.0**.
## vec4 saturate ( const vec4 & v )

Clamps the values of vector components within the range of **0.0** to **1.0**.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - Vector.

### Return value

Vector with components clamped within the range of **0.0** to **1.0**.
## float sigmoid ( float x )

Returns the logistic sigmoid of the argument: **1 / (1 + e^-x)**.
### Arguments

- *float* **x** - Argument.

### Return value

Logistic sigmoid of the argument, in the range of **0.0** to **1.0**, exclusive.
## double sigmoid ( double x )

Returns the logistic sigmoid of the argument: **1 / (1 + e^-x)**.
### Arguments

- *double* **x** - Argument.

### Return value

Logistic sigmoid of the argument, in the range of **0.0** to **1.0**, exclusive.
## float sign ( float v )

Returns the sign of the argument.
### Arguments

- *float* **v** - Argument.

### Return value

Sign of the argument. 1.0 if *v* >= 0.0 ; -1.0 if *v* < 0.0.
## double sign ( double v )

Returns the sign of the argument.
### Arguments

- *double* **v** - Argument.

### Return value

Sign of the argument. 1.0 if *v* >= 0.0 ; -1.0 if *v* < 0.0.
## int signMask ( int v )

Returns the sign of the argument value.
### Arguments

- *int* **v** - Value.

### Return value

0 if the value is positive or zero, -1, if the value is negative.
## quat slerp ( const quat & q0 , const quat & q1 , float k )

Spherical interpolation between two given quaternions.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q0** - The value of the first quaternion.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q1** - The value of the second quaternion.
- *float* **k** - The current position (from 0 to 1).

### Return value

Resulting quaternion.
## float smoothstep ( float x )


Returns a smooth Hermite interpolation between 0 and 1, if **x** is in the range [**0**, **1**].


![](smoothstep.png)


It is convenient for creating a sequence of transitions using smoothstep to interpolate each segment as an alternative to using more sophisticated or expensive interpolation techniques.


### Arguments

- *float* **x** - Value to be interpolated.

### Return value


One of the following values:


- 0 if **x** is less than 0;
- 1 if **x** is greater than 1;
- interpolated value between 0 and 1 if **x** is in the range [**0**, **1**].


## double smoothstep ( double x )


Returns a smooth Hermite interpolation between 0 and 1, if **x** is in the range [**0**, **1**].


![](smoothstep.png)


It is convenient for creating a sequence of transitions using smoothstep to interpolate each segment as an alternative to using more sophisticated or expensive interpolation techniques.


### Arguments

- *double* **x** - Value to be interpolated.

### Return value


One of the following values:


- 0 if **x** is less than 0;
- 1 if **x** is greater than 1;
- interpolated value between 0 and 1 if **x** is in the range [**0**, **1**].


## float smoothstep ( float edge0 , float edge1 , float x )


Returns a smooth Hermite interpolation between 0 and 1, if **x** is in the range [**edge0**, **edge1**].


![](smoothstep.png)


It is convenient for creating a sequence of transitions using smoothstep to interpolate each segment as an alternative to using more sophisticated or expensive interpolation techniques.


### Arguments

- *float* **edge0** - Left edge value.
- *float* **edge1** - Right edge value.
- *float* **x** - Value to be interpolated.

### Return value


One of the following values:


- 0 if **x** is less than **edge0**;
- 1 if **x** is greater than **edge1**;
- interpolated value between 0 and 1 if **x** is in the range [**edge0**, **edge1**].


## double smoothstep ( double edge0 , double edge1 , double x )


Returns a smooth Hermite interpolation between 0 and 1, if **x** is in the range [**edge0**, **edge1**].


![](smoothstep.png)


It is convenient for creating a sequence of transitions using smoothstep to interpolate each segment as an alternative to using more sophisticated or expensive interpolation techniques.


### Arguments

- *double* **edge0** - Left edge value.
- *double* **edge1** - Right edge value.
- *double* **x** - Value to be interpolated.

### Return value


One of the following values:


- 0 if **x** is less than **edge0**;
- 1 if **x** is greater than **edge1**;
- interpolated value between 0 and 1 if **x** is in the range [**edge0**, **edge1**].


## float smootherstep ( float x )


Returns a smooth interpolation between 0 and 1 using a fifth-order polynomial function, if **x** is in the range [**0**, **1**].


![](smootherstep.png)


It is convenient for creating a sequence of transitions using smoothstep to interpolate each segment as an alternative to using more sophisticated or expensive interpolation techniques.


### Arguments

- *float* **x** - Value to be interpolated.

### Return value


One of the following values:


- 0 if **x** is less than 0;
- 1 if **x** is greater than 1;
- interpolated value between 0 and 1 if **x** is in the range [**0**, **1**].


## double smootherstep ( double x )


Returns a smooth interpolation between 0 and 1 using a fifth-order polynomial function, if **x** is in the range [**0**, **1**].


![](smootherstep.png)


It is convenient for creating a sequence of transitions using smoothstep to interpolate each segment as an alternative to using more sophisticated or expensive interpolation techniques.


### Arguments

- *double* **x** - Value to be interpolated.

### Return value


One of the following values:


- 0 if **x** is less than 0;
- 1 if **x** is greater than 1;
- interpolated value between 0 and 1 if **x** is in the range [**0**, **1**].


## float smootherstep ( float edge0 , float edge1 , float x )


Returns a smooth interpolation between 0 and 1 using a fifth-order polynomial function, if **x** is in the range [**edge0**, **edge1**].


![](smootherstep.png)


It is convenient for creating a sequence of transitions using smoothstep to interpolate each segment as an alternative to using more sophisticated or expensive interpolation techniques.


### Arguments

- *float* **edge0** - Left edge value.
- *float* **edge1** - Right edge value.
- *float* **x** - Value to be interpolated.

### Return value


One of the following values:


- 0 if **x** is less than **edge0**;
- 1 if **x** is greater than **edge1**;
- interpolated value between 0 and 1 if **x** is in the range [**edge0**, **edge1**].


## double smootherstep ( double edge0 , double edge1 , double x )


Returns a smooth interpolation between 0 and 1 using a fifth-order polynomial function, if **x** is in the range [**edge0**, **edge1**].


![](smootherstep.png)


It is convenient for creating a sequence of transitions using smoothstep to interpolate each segment as an alternative to using more sophisticated or expensive interpolation techniques.


### Arguments

- *double* **edge0** - Left edge value.
- *double* **edge1** - Right edge value.
- *double* **x** - Value to be interpolated.

### Return value


One of the following values:


- 0 if **x** is less than **edge0**;
- 1 if **x** is greater than **edge1**;
- interpolated value between 0 and 1 if **x** is in the range [**edge0**, **edge1**].


## float srgb ( float x )

Converts RGB color value to sRGB format.
### Arguments

- *float* **x** - Value to convert.

### Return value

sRGB color value.
## vec2 srgb ( const vec2 & color )

Converts RGB color value to sRGB format.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **color** - Value to convert.

### Return value

sRGB color value.
## vec3 srgb ( const vec3 & color )

Converts RGB color value to sRGB format.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **color** - Value to convert.

### Return value

sRGB color value.
## vec4 srgb ( const vec4 & color )

Converts RGB color value and alpha to sRGB format.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Value to convert.

### Return value

sRGB color value.
## vec4 srgbColor ( const vec4 & color )

Converts RGB color value to sRGB format without converting alpha.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Value to convert.

### Return value

sRGB color value.
## bool step ( float a , float b )

Checks whether the value a is greater than or equal to b.
### Arguments

- *float* **a** - Value.
- *float* **b** - Value.

### Return value

true if a is greater than or equal to b, otherwise false.
## int stoi ( Scalar v )

Converts a scalar value (float or double, depending on the precision) to an integer value.
### Arguments

- *Scalar* **v** - Scalar value (float or double, depending on the precision).

### Return value

Integer value.
## float * sub3 ( float *UNIGINE_RESTRICT ret , const float *UNIGINE_RESTRICT v0 , const float *UNIGINE_RESTRICT v1 )

Returns the result of a componentwise subtraction of three components of vectors by storing it in the array.
### Arguments

- *float *UNIGINE_RESTRICT* **ret** - Array to store the return value.
- *const float *UNIGINE_RESTRICT* **v0** - Pointer to vector.
- *const float *UNIGINE_RESTRICT* **v1** - Pointer to vector.

### Return value

Pointer to the array that stores the return value.
## void swap ( Type & v0 , Type & v1 )

Swaps two values.
### Arguments

- *Type &* **v0** - First value.
- *Type &* **v1** - Second value.

## void swap ( Type * v0 , Type * v1 , int size )

Swaps two arrays.
### Arguments

- *Type ** **v0** - The first array.
- *Type ** **v1** - The second array.
- *int* **size** - The array size.

## int floatToIntBits ( float value )

Returns an integer corresponding to the bits of the given value.
### Arguments

- *float* **value** - Value to be converted.

### Return value

Resulting value.
## unsigned int floatToUIntBits ( float value )

Returns an unsigned integer corresponding to the bits of the given value.
### Arguments

- *float* **value** - Value to be converted.

### Return value

Resulting value.
## float intBitsToFloat ( int value )

Returns the float corresponding to the given bits.
### Arguments

- *int* **value** - Value to be converted.

### Return value

Resulting value.
## float intBitsToFloat ( unsigned int value )

Returns the float corresponding to the given bits.
### Arguments

- *unsigned int* **value** - Value to be converted.

### Return value

Resulting value.
## long long floatToLongBits ( double value )

Returns a long long value corresponding to the given value.
### Arguments

- *double* **value** - Value to be converted.

### Return value

Resulting value.
## unsigned long long floatToULongBits ( double value )

Returns a long long value corresponding to the given value.
### Arguments

- *double* **value** - Value to be converted.

### Return value

Resulting value.
## double longBitsToFloat ( long long value )

Returns the double corresponding to the given bits.
### Arguments

- *long long* **value** - Value to be converted.

### Return value

Resulting value.
## double longBitsToFloat ( unsigned long long value )

Returns the double corresponding to the given bits.
### Arguments

- *unsigned long long* **value** - Value to be converted.

### Return value

Resulting value.
## unsigned long long doubleIntToLong ( unsigned int a1 , unsigned int a2 )

Returns a conversion of two unsigned integer values to a unsigned long long value.
### Arguments

- *unsigned int* **a1** - Source value.
- *unsigned int* **a2** - Source value.

### Return value

Resulting value.
## float toFloat ( double v )

Converts a double value to a float value.
### Arguments

- *double* **v** - Double value.

### Return value

Float value.
## float toFloat ( long double v )

Converts a long double value to a float value.
### Arguments

- *long double* **v** - Long double value.

### Return value

Float value.
## float toFloat ( char v )

Converts a character value to a float value.
### Arguments

- *char* **v** - Char value.

### Return value

Float value.
## float toFloat ( int v )

Converts an integer value to a float value.
### Arguments

- *int* **v** - Integer value.

### Return value

Float value.
## float toFloat ( long long v )

Converts a long value to a float value.
### Arguments

- *long long* **v** - Long value.

### Return value

Float value.
## float toFloat ( unsigned int v )

Converts an unsigned int value to a float value.
### Arguments

- *unsigned int* **v** - Unsigned int value.

### Return value

Float value.
## float toFloat ( unsigned char v )

Converts an unsigned char value to a float value.
### Arguments

- *unsigned char* **v** - Unsigned char value.

### Return value

Float value.
## float toFloat ( bool v )

Converts a boolean value to a float value.
### Arguments

- *bool* **v** - Boolean value.

### Return value

Float value.
## float toFloat ( half v )

Converts a half value to a float value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Half value.

### Return value

Float value.
## float toFloat ( const String & v )

Converts a const String value to a float value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **v** - const String value.

### Return value

Float value.
## float toFloat ( const char * v )

Converts a const char pointer value to a float value.
### Arguments

- *const char ** **v** - const char ptr value.

### Return value

Float value.
## half toHalf ( float v )

Converts a float value to a half value.
### Arguments

- *float* **v** - Float value.

### Return value

Half value.
## half toHalf ( double v )

Converts a double value to a half value.
### Arguments

- *double* **v** - Double value.

### Return value

Half value.
## half toHalf ( long double v )

Converts a long double value to a half value.
### Arguments

- *long double* **v** - Long double value.

### Return value

Half value.
## half toHalf ( char v )

Converts a char value to a half value.
### Arguments

- *char* **v** - Char value.

### Return value

Half value.
## half toHalf ( int v )

Converts an int value to a half value.
### Arguments

- *int* **v** - Int value.

### Return value

Half value.
## half toHalf ( long long v )

Converts a long long value to a half value.
### Arguments

- *long long* **v** - Long long value.

### Return value

Half value.
## half toHalf ( unsigned int v )

Converts an unsigned int value to a half value.
### Arguments

- *unsigned int* **v** - Unsigned int value.

### Return value

Half value.
## half toHalf ( unsigned char v )

Converts an unsigned char value to a half value.
### Arguments

- *unsigned char* **v** - Unsigned char value.

### Return value

Half value.
## half toHalf ( bool v )

Converts a bool value to a half value.
### Arguments

- *bool* **v** - Bool value.

### Return value

Half value.
## half toHalf ( const String & v )

Converts a const String value to a half value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **v** - Const String value.

### Return value

Half value.
## half toHalf ( const char * v )

Converts a const char pointer value to a half value.
### Arguments

- *const char ** **v** - Const char ptr value.

### Return value

Half value.
## double toDouble ( float value )

Converts a float value to a double value.
### Arguments

- *float* **value** - Float value.

### Return value

Double value.
## double toDouble ( char value )

Converts a character value to a double value.
### Arguments

- *char* **value** - Char value.

### Return value

Double value.
## double toDouble ( int value )

Converts an integer value to a double value.
### Arguments

- *int* **value** - Integer value.

### Return value

Double value.
## double toDouble ( long long value )

Converts a long value to a double value.
### Arguments

- *long long* **value** - Long value.

### Return value

Double value.
## double toDouble ( bool value )

Converts a boolean value to a double value.
### Arguments

- *bool* **value** - Boolean value.

### Return value

Double value.
## double toDouble ( unsigned int v )

Converts an unsigned int value to a double value.
### Arguments

- *unsigned int* **v** - Unsigned int value.

### Return value

Double value.
## double toDouble ( unsigned char v )

Converts an unsigned char value to a double value.
### Arguments

- *unsigned char* **v** - Unsigned char value.

### Return value

Double value.
## double toDouble ( half v )

Converts a half value to a double value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Half value.

### Return value

Double value.
## double toDouble ( const String & v )

Converts a const String value to a double value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **v** - const String value.

### Return value

Double value.
## double toDouble ( const char * v )

Converts a const char pointer value to double value.
### Arguments

- *const char ** **v** - const char ptr value.

### Return value

Double value.
## Scalar toScalar ( double value )

Converts a double value to a Scalar value.
### Arguments

- *double* **value** - Double value.

### Return value

Scalar value.
## Scalar toScalar ( long double value )

Converts a long double value to a Scalar value.
### Arguments

- *long double* **value** - Long double value.

### Return value

Scalar value.
## Scalar toScalar ( float value )

Converts a float value to a Scalar value.
### Arguments

- *float* **value** - Float value.

### Return value

Scalar value.
## Scalar toScalar ( char value )

Converts a char value to a Scalar value.
### Arguments

- *char* **value** - Char value.

### Return value

Scalar value.
## Scalar toScalar ( int value )

Converts an int value to a Scalar value.
### Arguments

- *int* **value** - Int value.

### Return value

Scalar value.
## Scalar toScalar ( long long value )

Converts a long long value to a Scalar value.
### Arguments

- *long long* **value** - Long long value.

### Return value

Scalar value.
## Scalar toScalar ( unsigned int value )

Converts an unsigned int value to a Scalar value.
### Arguments

- *unsigned int* **value** - Unsigned int value.

### Return value

Scalar value.
## Scalar toScalar ( unsigned char value )

Converts an unsigned char value to a Scalar value.
### Arguments

- *unsigned char* **value** - Unsigned char value.

### Return value

Scalar value.
## Scalar toScalar ( bool value )

Converts a bool value to a Scalar value.
### Arguments

- *bool* **value** - Bool value.

### Return value

Scalar value.
## Scalar toScalar ( half value )

Converts a half value to a Scalar value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **value** - Half value.

### Return value

Scalar value.
## Scalar toScalar ( const String & value )

Converts a const String value to a Scalar value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **value** - Const String value.

### Return value

Scalar value.
## Scalar toScalar ( const char value )

Converts a const char value to a Scalar value.
### Arguments

- *const char* **value** - Const char value.

### Return value

Scalar value.
## int toInt ( float value )

Converts a float value to an integer value.
### Arguments

- *float* **value** - Float value.

### Return value

Integer value.
## int toInt ( double value )

Converts a double value to an integer value.
### Arguments

- *double* **value** - Double value.

### Return value

Integer value.
## int toInt ( char value )

Converts a character value to an integer value.
### Arguments

- *char* **value** - Char value.

### Return value

Integer value.
## int toInt ( long long value )

Converts a long value to an integer value.
### Arguments

- *long long* **value** - Long value.

### Return value

Integer value.
## int toInt ( bool value )

Converts a boolean value to an integer value.
### Arguments

- *bool* **value** - Boolean value.

### Return value

Integer value.
## int toInt ( unsigned int v )

Converts an unsigned int value to an int value.
### Arguments

- *unsigned int* **v** - Unsigned int value.

### Return value

Int value.
## int toInt ( unsigned char v )

Converts an unsigned char value to an int value.
### Arguments

- *unsigned char* **v** - Unsigned char value.

### Return value

Int value.
## int toInt ( half v )

Converts a half value to an int value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Half value.

### Return value

Int value.
## int toInt ( const String & v )

Converts a const String value to an int value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **v** - const String value.

### Return value

Int value.
## int toInt ( const char * v )

Converts a const char pointer value to an int value.
### Arguments

- *const char ** **v** - const char ptr value.

### Return value

Int value.
## unsigned int toUInt ( float value )

Converts a float value to an unsigned int value.
### Arguments

- *float* **value** - Float value.

### Return value

Unsigned int value.
## unsigned int toUInt ( double value )

Converts a double value to an unsigned int value.
### Arguments

- *double* **value** - Double value.

### Return value

Unsigned int value.
## unsigned int toUInt ( char value )

Converts a char value to an unsigned int value.
### Arguments

- *char* **value** - Char value.

### Return value

Unsigned int value.
## unsigned int toUInt ( int value )

Converts an int value to an unsigned int value.
### Arguments

- *int* **value** - Int value.

### Return value

Unsigned int value.
## unsigned int toUInt ( long long value )

Converts a long long value to an unsigned int value.
### Arguments

- *long long* **value** - Long long value.

### Return value

Unsigned int value.
## unsigned int toUInt ( unsigned char value )

Converts an unsigned char value to an unsigned int value.
### Arguments

- *unsigned char* **value** - Unsigned char value.

### Return value

Unsigned int value.
## unsigned int toUInt ( bool value )

Converts a bool value to an unsigned int value.
### Arguments

- *bool* **value** - Bool value.

### Return value

Unsigned int value.
## unsigned int toUInt ( half value )

Converts a half value to an unsigned int value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **value** - Half value.

### Return value

Unsigned int value.
## unsigned int toUInt ( const String & value )

Converts a const String value to an unsigned int value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **value** - Const String value.

### Return value

Unsigned int value.
## unsigned int toUInt ( const char * value )

Converts a const char pointer value to an unsigned int value.
### Arguments

- *const char ** **value** - Const char ptr value.

### Return value

Unsigned int value.
## long long toLong ( int value )

Converts an integer value to a long value.
### Arguments

- *int* **value** - Integer value.

### Return value

Long value.
## long long toLong ( float value )

Converts a float value to a long value.
### Arguments

- *float* **value** - Float value.

### Return value

Long value.
## long long toLong ( double value )

Converts a double value to a long value.
### Arguments

- *double* **value** - Double value.

### Return value

Long value.
## long long toLong ( char value )

Converts a character value to a long value.
### Arguments

- *char* **value** - Char value.

### Return value

Long value.
## long long toLong ( bool value )

Converts a boolean value to a long value.
### Arguments

- *bool* **value** - Boolean value.

### Return value

Long value.
## long long toLong ( unsigned int v )

Converts an unsigned int value to a long value.
### Arguments

- *unsigned int* **v** - Unsigned int value.

### Return value

Int value.
## long long toLong ( unsigned char v )

Converts an unsigned char value to a long value.
### Arguments

- *unsigned char* **v** - Unsigned char value.

### Return value

Int value.
## long long toLong ( half v )

Converts a half value to a long value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Half value.

### Return value

Int value.
## long long toLong ( const String & v )

Converts a const String value to a long value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **v** - const String value.

### Return value

Int value.
## long long toLong ( const char * v )

Converts a const char pointer value to a long value.
### Arguments

- *const char ** **v** - const char ptr value.

### Return value

Int value.
## unsigned long long toULong ( int value )

Converts an integer value to an unsigned long value.
### Arguments

- *int* **value** - Integer value.

### Return value

Long value.
## unsigned long long toULong ( float value )

Converts a float value to an unsigned long value.
### Arguments

- *float* **value** - Float value.

### Return value

Long value.
## unsigned long long toULong ( double value )

Converts a double value to an unsigned long value.
### Arguments

- *double* **value** - Double value.

### Return value

Long value.
## unsigned long long toULong ( char value )

Converts a character value to an unsigned long value.
### Arguments

- *char* **value** - Char value.

### Return value

Long value.
## unsigned long long toULong ( bool value )

Converts a boolean value to an unsigned long value.
### Arguments

- *bool* **value** - Boolean value.

### Return value

Long value.
## unsigned long long toULong ( unsigned int v )

Converts an unsigned int value to an unsigned long value.
### Arguments

- *unsigned int* **v** - Unsigned int value.

### Return value

Int value.
## unsigned long long toULong ( unsigned char v )

Converts an unsigned char value to an unsigned long value.
### Arguments

- *unsigned char* **v** - Unsigned char value.

### Return value

Int value.
## unsigned long long toULong ( half v )

Converts a half value to an unsigned long value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Half value.

### Return value

Int value.
## unsigned long long toULong ( const String & v )

Converts a const String value to an unsigned long value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **v** - const String value.

### Return value

Int value.
## unsigned long long toULong ( const char * v )

Converts a const char pointer value to an unsigned long value.
### Arguments

- *const char ** **v** - const char ptr value.

### Return value

Int value.
## char toChar ( float value )

Converts a float value to a character value.
### Arguments

- *float* **value** - Float value.

### Return value

Char value.
## char toChar ( double value )

Converts a double value to a character value.
### Arguments

- *double* **value** - Double value.

### Return value

Char value.
## char toChar ( int value )

Converts an integer value to a character value.
### Arguments

- *int* **value** - Integer value.

### Return value

Char value.
## char toChar ( long long value )

Converts a long value to a character value.
### Arguments

- *long long* **value** - Long value.

### Return value

Char value.
## char toChar ( bool value )

Converts a boolean value to a character value.
### Arguments

- *bool* **value** - Boolean value.

### Return value

Char value.
## char toChar ( unsigned int v )

Converts an unsigned int value to a char value.
### Arguments

- *unsigned int* **v** - Unsigned int value.

### Return value

Char value.
## char toChar ( unsigned char v )

Converts an unsigned char value to a char value.
### Arguments

- *unsigned char* **v** - Unsigned char value.

### Return value

Char value.
## char toChar ( half v )

Converts a half value to a char value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Half value.

### Return value

Char value.
## char toChar ( const String & v )

Converts a const String value to a char value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **v** - const String value.

### Return value

Char value.
## char toChar ( const char * v )

Converts a const char pointer value to char value.
### Arguments

- *const char ** **v** - const char ptr value.

### Return value

Char value.
## short toShort ( float value )

Converts a float value to a short value.
### Arguments

- *float* **value** - Float value.

### Return value

Short value.
## short toShort ( double value )

Converts a double value to a short value.
### Arguments

- *double* **value** - Double value.

### Return value

Short value.
## short toShort ( char value )

Converts a char value to a short value.
### Arguments

- *char* **value** - Char value.

### Return value

Short value.
## short toShort ( int value )

Converts an int value to a short value.
### Arguments

- *int* **value** - Int value.

### Return value

Short value.
## short toShort ( long long value )

Converts a long long value to a short value.
### Arguments

- *long long* **value** - Long long value.

### Return value

Short value.
## short toShort ( unsigned char value )

Converts an unsigned char value to a short value.
### Arguments

- *unsigned char* **value** - Unsigned char value.

### Return value

Short value.
## short toShort ( bool value )

Converts a bool value to a short value.
### Arguments

- *bool* **value** - Bool value.

### Return value

Short value.
## short toShort ( half value )

Converts a half value to a short value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **value** - Half value.

### Return value

Short value.
## short toShort ( const String & value )

Converts a const String value to a short value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **value** - Const String value.

### Return value

Short value.
## short toShort ( const char * value )

Converts a const char pointer value to a short value.
### Arguments

- *const char ** **value** - Const char ptr value.

### Return value

Short value.
## uchar toUChar ( float value )

Converts a float value to an unsigned character value.
### Arguments

- *float* **value** - Float value.

### Return value

Unsigned char value.
## uchar toUChar ( double value )

Converts a double value to an unsigned character value.
### Arguments

- *double* **value** - Double value.

### Return value

Unsigned char value.
## uchar toUChar ( int value )

Converts an integer value to an unsigned character value.
### Arguments

- *int* **value** - Integer value.

### Return value

Unsigned char value.
## uchar toUChar ( long long value )

Converts a long value to an unsigned character value.
### Arguments

- *long long* **value** - Long value.

### Return value

Unsigned char value.
## uchar toUChar ( bool value )

Converts a boolean value to an unsigned character value.
### Arguments

- *bool* **value** - Boolean value.

### Return value

Unsigned char value.
## unsigned char toUChar ( unsigned int v )

Converts an unsigned int value to an unsigned char value.
### Arguments

- *unsigned int* **v** - Unsigned int value.

### Return value

Unsigned char value.
## unsigned char toUChar ( half v )

Converts a half value to an unsigned char value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Half value.

### Return value

Unsigned char value.
## unsigned char toUChar ( const String & v )

Converts a const String value to an unsigned char value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **v** - const String value.

### Return value

Unsigned char value.
## unsigned char toUChar ( const char * v )

Converts a const char pointer value to an unsigned char value.
### Arguments

- *const char ** **v** - const char ptr value.

### Return value

Unsigned char value.
## unsigned short toUShort ( float value )

Converts a float value to an unsigned short value.
### Arguments

- *float* **value** - Float value.

### Return value

Unsigned short value.
## unsigned short toUShort ( double value )

Converts a double value to an unsigned short value.
### Arguments

- *double* **value** - Double value.

### Return value

Unsigned short value.
## unsigned short toUShort ( char value )

Converts a char value to an unsigned short value.
### Arguments

- *char* **value** - Char value.

### Return value

Unsigned short value.
## unsigned short toUShort ( int value )

Converts an int value to an unsigned short value.
### Arguments

- *int* **value** - Int value.

### Return value

Unsigned short value.
## unsigned short toUShort ( long long value )

Converts a long long value to an unsigned short value.
### Arguments

- *long long* **value** - Long long value.

### Return value

Unsigned short value.
## unsigned short toUShort ( bool value )

Converts a bool value to an unsigned short value.
### Arguments

- *bool* **value** - Bool value.

### Return value

Unsigned short value.
## unsigned short toUShort ( half value )

Converts a half value to an unsigned short value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **value** - Half value.

### Return value

Unsigned short value.
## unsigned short toUShort ( const String & value )

Converts a const String value to an unsigned short value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **value** - Const String value.

### Return value

Unsigned short value.
## unsigned short toUShort ( const char * value )

Converts a const char pointer value to an unsigned short value.
### Arguments

- *const char ** **value** - Const char ptr value.

### Return value

Unsigned short value.
## bool toBool ( float value )

Converts a float value to a boolean value.
### Arguments

- *float* **value** - Float value.

### Return value

Boolean value.
## bool toBool ( double value )

Converts a double value to a boolean value.
### Arguments

- *double* **value** - Double value.

### Return value

Boolean value.
## bool toBool ( int value )

Converts an integer value to a boolean value.
### Arguments

- *int* **value** - Integer value.

### Return value

Boolean value.
## bool toBool ( char value )

Converts a character value to a boolean value.
### Arguments

- *char* **value** - Char value.

### Return value

Boolean value.
## bool toBool ( long long value )

Converts a long value to a boolean value.
### Arguments

- *long long* **value** - Long value.

### Return value

Boolean value.
## bool toBool ( unsigned int v )

Converts an unsigned int value to a bool value.
### Arguments

- *unsigned int* **v** - Unsigned int value.

### Return value

Boolean value.
## bool toBool ( unsigned char v )

Converts an unsigned char value to a bool value.
### Arguments

- *unsigned char* **v** - Unsigned char value.

### Return value

Boolean value.
## bool toBool ( half v )

Converts a half value to a bool value.
### Arguments

- *[half](../../../api/library/math/class.half_cpp.md)* **v** - Half value.

### Return value

Boolean value.
## bool toBool ( const String & v )

Converts a const String value to a bool value.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **v** - const String value.

### Return value

Boolean value.
## bool toBool ( const char * v )

Converts a const char pointer value to a bool value.
### Arguments

- *const char ** **v** - const char ptr value.

### Return value

Boolean value.
## mat2x2_values unsafeToMat2x2 ( float * data )

Performs an unsafe conversion of the specified pointer to a source array containing matrix data to the dedicated type used to store elements of a 2x2 matrix. Make sure that the number of elements and their positions in the pointed source array matches the target type, otherwise you may get wrong data or end up with a crash.
### Arguments

- *float ** **data** - Pointer to the matrix data.

### Return value

The value storing matrix float values.
## mat3x3_values unsafeToMat3x3 ( float * data )

Performs an unsafe conversion of the specified pointer to a source array containing matrix data to the dedicated type used to store elements of a 3x3 matrix. Make sure that the number of elements and their positions in the pointed source array matches the target type, otherwise you may get wrong data or end up with a crash.
### Arguments

- *float ** **data** - Pointer to the matrix data.

### Return value

The value storing matrix float values.
## mat4x3_values unsafeToMat4x3 ( float * data )

Performs an unsafe conversion of the specified pointer to a source array containing matrix data to the dedicated type used to store elements of a 4x3 matrix. Make sure that the number of elements and their positions in the pointed source array matches the target type, otherwise you may get wrong data or end up with a crash.
### Arguments

- *float ** **data** - Pointer to the matrix data.

### Return value

The value storing matrix float values.
## mat4x4_values unsafeToMat4x4 ( float * data )

Performs an unsafe conversion of the specified pointer to a source array containing matrix data to the dedicated type used to store elements of a 4x4 matrix. Make sure that the number of elements and their positions in the pointed source array matches the target type, otherwise you may get wrong data or end up with a crash.
### Arguments

- *float ** **data** - Pointer to the matrix data.

### Return value

The value storing matrix float values.
## dmat4x3_values unsafeToDMat4x3 ( double * data )

Performs an unsafe conversion of the specified pointer to a source array containing matrix data to the dedicated type used to store elements of a 4x3 matrix. Make sure that the number of elements and their positions in the pointed source array matches the target type, otherwise you may get wrong data or end up with a crash.
### Arguments

- *double ** **data** - Pointer to the matrix data.

### Return value

The value storing matrix double values.
## dmat4x4_values unsafeToDMat4x4 ( double * data )

Performs an unsafe conversion of the specified pointer to a source array containing matrix data to the dedicated type used to store elements of a 4x4 matrix. Make sure that the number of elements and their positions in the pointed source array matches the target type, otherwise you may get wrong data or end up with a crash.
### Arguments

- *double ** **data** - Pointer to the matrix data.

### Return value

The value storing matrix double values.
## int udiv ( int x , int y )

Performs integer division with rounding up: it adds 1 to the result if there is a remainder from the division.
### Arguments

- *int* **x** - First argument.
- *int* **y** - Second argument.

### Return value

The rounded up quotient of two arguments that satisfies the following condition: *y* * *z* >= *x*.
## vec2 vogelDisk ( uint i , uint count , float noise )

Returns a generated set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside. This method is suitable for getting uniform distribution of coordinates for a circle. For example you can use it is a loop to generate UV coordinates offset for making the uniform circular blur effect. You can use the current loop iteration index as the i argument and the maximum number of iterations ï¿½ as count.
### Arguments

- *uint* **i** - Index of the current point for the disk.
- *uint* **count** - Number of points.
- *float* **noise** - Normalized noise.

### Return value

Set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside.
## vec2 vogelDisk ( uint i , uint count )

Returns a generated set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside. This method is suitable for getting uniform distribution of coordinates for a circle. For example you can use it is a loop to generate UV coordinates offset for making the uniform circular blur effect. You can use the current loop iteration index as the i argument and the maximum number of iterations ï¿½ as count.
### Arguments

- *uint* **i** - Index of the current point for the disk.
- *uint* **count** - Number of points.

### Return value

Set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside.
## int operator== ( const Controls Ptr & c0 , const Controls Ptr & c1 , g0 , g1 , i0 , i1 , m0 , m1 , m0 , m1 , p0 , p1 , m0 , m1 , s0 , s1 , s0 , s1 , t0 , t1 , t0 , t1 , ui0 , ui1 , w0 , w1 , x0 , x1 )

Checks if two controls are actually the same controls.
### Arguments

- *const [Controls](../../../api/library/controls/class.controls_cpp.md)Ptr &* **c0** - The first control.
- *const [Controls](../../../api/library/controls/class.controls_cpp.md)Ptr &* **c1** - The second control.

### Return value

Returns **1** if two values are the same; otherwise, **0**.
## int operator== ( const vec2 & v0 , const vec2 & v1 )

Vector equal comparison.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - The first vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - The second vector.

## int operator== ( const vec3 & v0 , const vec3 & v1 )

Vector equal comparison.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second vector.

## int operator== ( const vec4 & v0 , const vec4 & v1 )

Vector equal comparison.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - The first vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - The second vector.

## int operator== ( const dvec2 & v0 , const dvec2 & v1 )

Vector equal comparison.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - The first vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - The second vector.

## int operator== ( const dvec3 & v0 , const dvec3 & v1 )

Vector equal comparison.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second vector.

## int operator== ( const dvec4 & v0 , const dvec4 & v1 )

Vector equal comparison.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - The first vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - The second vector.

## int operator== ( const ivec2 & v0 , const ivec2 & v1 )

Vector equal comparison.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - The first vector.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - The second vector.

## int operator== ( const ivec3 & v0 , const ivec3 & v1 )

Vector equal comparison.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - The first vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - The second vector.

## int operator== ( const ivec4 & v0 , const ivec4 & v1 )

Vector equal comparison.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - The first vector.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - The second vector.

## int operator== ( const bvec4 & v0 , const bvec4 & v1 )

Vector equal comparison.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - The first vector.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - The second vector.

## int operator== ( const svec4 & v0 , const svec4 & v1 )

Vector equal comparison.
### Arguments

- *const [svec4](../../../api/library/math/class.svec4_cpp.md) &* **v0** - The first vector.
- *const [svec4](../../../api/library/math/class.svec4_cpp.md) &* **v1** - The second vector.

## int operator== ( const mat4 & m0 , const mat4 & m1 )

Matrix equal comparison.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m0** - The first matrix.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m1** - The second matrix.

## int operator== ( const dmat4 & m0 , const dmat4 & m1 )

Matrix equal comparison.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The second matrix.

## int operator== ( const quat & q0 , const quat & q1 )

Quaternion equal comparison.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q0** - The first quaternion.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q1** - The second quaternion.

## int operator== ( const String & s0 , const String & s1 )

String equal comparison.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s0** - The first string.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **s1** - The second string.

## int operator== ( )

## int operator== ( )

## int operator== ( const TypeInfo & t0 , const TypeInfo & t1 )

Check if two TypeInfo classes are referenced the same types.
### Arguments

- *const [TypeInfo](../../../api/library/common/class.typeinfo_cpp.md) &* **t0** - The first TypeIndo class.
- *const [TypeInfo](../../../api/library/common/class.typeinfo_cpp.md) &* **t1** - The second TypeIndo class.

### Return value

Returns **1** if types are the same; otherwise, **0** is returned.
## int operator!= ( const Controls Ptr & c0 , const Controls Ptr & c1 , g0 , g1 , i0 , i1 , m0 , m1 , m0 , m1 , p0 , p1 , m0 , m1 , s0 , s1 , s0 , s1 , t0 , t1 , t0 , t1 , ui0 , ui1 , w0 , w1 , x0 , x1 )

Checks if two controls are not the same controls.
### Arguments

- *const [Controls](../../../api/library/controls/class.controls_cpp.md)Ptr &* **c0** - The first control.
- *const [Controls](../../../api/library/controls/class.controls_cpp.md)Ptr &* **c1** - The second control.

### Return value

Returns **1** if two values are not the same; otherwise, **0**.
## int operator!= ( const vec2 & v0 , const vec2 & v1 )

Vector not equal comparison.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - The first vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - The second vector.

## int operator!= ( const vec3 & v0 , const vec3 & v1 )

Vector not equal comparison.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The first vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - The second vector.

## int operator!= ( const vec4 & v0 , const vec4 & v1 )

Vector not equal comparison.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - The first vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - The second vector.

## int operator!= ( const dvec2 & v0 , const dvec2 & v1 )

Vector not equal comparison.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - The first vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - The second vector.

## int operator!= ( const dvec3 & v0 , const dvec3 & v1 )

Vector not equal comparison.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The first vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - The second vector.

## int operator!= ( const dvec4 & v0 , const dvec4 & v1 )

Vector not equal comparison.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - The first vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - The second vector.

## int operator!= ( const ivec2 & v0 , const ivec2 & v1 )

Vector not equal comparison.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - The first vector.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - The second vector.

## int operator!= ( const ivec3 & v0 , const ivec3 & v1 )

Vector not equal comparison.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - The first vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - The second vector.

## int operator!= ( const ivec4 & v0 , const ivec4 & v1 )

Vector not equal comparison.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - The first vector.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - The second vector.

## int operator!= ( const bvec4 & v0 , const bvec4 & v1 )

Vector not equal comparison.
### Arguments

- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v0** - The first vector.
- *const [bvec4](../../../api/library/math/class.bvec4_cpp.md) &* **v1** - The second vector.

## int operator!= ( const svec4 & v0 , const svec4 & v1 )

Vector not equal comparison.
### Arguments

- *const [svec4](../../../api/library/math/class.svec4_cpp.md) &* **v0** - The first vector.
- *const [svec4](../../../api/library/math/class.svec4_cpp.md) &* **v1** - The second vector.

## int operator!= ( const mat4 & m0 , const mat4 & m1 )

Matrix not equal comparison.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m0** - The first matrix.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m1** - The second matrix.

## int operator!= ( const dmat4 & m0 , const dmat4 & m1 )

Matrix not equal comparison.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The second matrix.

## int operator!= ( const quat & q0 , const quat & q1 )

Quaternion not equal comparison.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q0** - The first quaternion.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q1** - The second quaternion.

## int operator!= ( const String & s0 , const String & s1 )

String not equal comparison.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s0** - The first string.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **s1** - The second string.

## int operator!= ( )

## int operator!= ( )

## int operator!= ( const TypeInfo & t0 , const TypeInfo & t1 )

Check if two TypeInfo classes are not referenced the same types.
### Arguments

- *const [TypeInfo](../../../api/library/common/class.typeinfo_cpp.md) &* **t0** - The first TypeIndo class.
- *const [TypeInfo](../../../api/library/common/class.typeinfo_cpp.md) &* **t1** - The second TypeIndo class.

### Return value

Returns **1** if types are not the same; otherwise, **0** is returned.
## vec2 operator* ( const vec2 & v0 , float v1 )

Scalar multiplication.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - The value of the vector.
- *float* **v1** - The value of the scalar.

### Return value

Resulting vector.
## vec2 operator* ( const vec2 & v0 , const vec2 & v1 )

Vector multiplication.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec3 operator* ( const vec3 & v0 , float v1 )

Scalar multiplication.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - The value of the vector.
- *float* **v1** - The value of the scalar.

### Return value

Resulting vector.
## vec3 operator* ( const vec3 & v0 , const vec3 & v1 )

Vector multiplication.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec4 operator* ( const vec4 & v0 , float v1 )

Scalar multiplication.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - The value of the vector.
- *float* **v1** - The value of the scalar.

### Return value

Resulting vector.
## vec4 operator* ( const vec4 & v0 , const vec4 & v1 )

Vector multiplication.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec2 operator* ( const dvec2 & v0 , double v1 )

Scalar multiplication.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - The value of the vector.
- *double* **v1** - The value of the scalar.

### Return value

Resulting vector.
## dvec2 operator* ( const dvec2 & v0 , const dvec2 & v1 )

Vector multiplication.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec3 operator* ( const dvec3 & v0 , double v1 )

Scalar multiplication.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - The value of the vector.
- *double* **v1** - The value of the scalar.

### Return value

Resulting vector.
## dvec3 operator* ( const dvec3 & v0 , const dvec3 & v1 )

Vector multiplication.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec4 operator* ( const dvec4 & v0 , double v1 )

Scalar multiplication.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - The value of the vector.
- *double* **v1** - The value of the scalar.

### Return value

Resulting vector.
## dvec4 operator* ( const dvec4 & v0 , const dvec4 & v1 )

Vector multiplication.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec2 operator* ( const ivec2 & v0 , int v1 )

Scalar multiplication.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The value of the scalar.

### Return value

Resulting vector.
## ivec2 operator* ( const ivec2 & v0 , const ivec2 & v1 )

Vector multiplication.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - First vector.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec3 operator* ( const ivec3 & v0 , int v1 )

Scalar multiplication.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The value of the scalar.

### Return value

Resulting vector.
## ivec3 operator* ( const ivec3 & v0 , const ivec3 & v1 )

Vector multiplication.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec4 operator* ( const ivec4 & v0 , int v1 )

Scalar multiplication.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The value of the scalar.

### Return value

Resulting vector.
## ivec4 operator* ( const ivec4 & v0 , const ivec4 & v1 )

Vector multiplication.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - First vector.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## mat4 operator* ( const mat4 & m , const float v )

Matrix multiplication.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the matrix.
- *const float* **v** - The value of the scalar.

### Return value

The resulting matrix.
## vec3 operator* ( const mat4 & m , const vec3 & v )

Vector multiplication.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## vec3 operator* ( const vec3 & v , const mat4 & m )

Vector multiplication.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## vec4 operator* ( const mat4 & m , const vec4 & v )

Vector multiplication.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## vec4 operator* ( const vec4 & v , const mat4 & m )

Vector multiplication.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The value of the vector.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## dvec3 operator* ( const mat4 & m , const dvec3 & v )

Vector multiplication.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## dvec3 operator* ( const dvec3 & v , const mat4 & m )

Vector multiplication.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## dvec4 operator* ( const mat4 & m , const dvec4 & v )

Vector multiplication.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## dvec4 operator* ( const dvec4 & v , const mat4 & m )

Vector multiplication.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## mat4 operator* ( const mat4 & m0 , const mat4 & m1 )

Matrix multiplication.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## dmat4 operator* ( const dmat4 & m , double v )

Matrix multiplication.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *double* **v** - The value of the scalar.

### Return value

The resulting matrix.
## vec2 operator* ( const dmat4 & m , const vec2 & v )

Vector multiplication.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## vec2 operator* ( const vec2 & v , const dmat4 & m )

Vector multiplication.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## vec3 operator* ( const dmat4 & m , const vec3 & v )

Vector multiplication.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## vec3 operator* ( const vec3 & v , const dmat4 & m )

Vector multiplication.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## vec4 operator* ( const dmat4 & m , const vec4 & v )

Vector multiplication.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## vec4 operator* ( const vec4 & v , const dmat4 & m )

Vector multiplication.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## dvec2 operator* ( const dmat4 & m , const dvec2 & v )

Vector multiplication.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## dvec2 operator* ( const dvec2 & v , const dmat4 & m )

Vector multiplication.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## dvec3 operator* ( const dmat4 & m , const dvec3 & v )

Vector multiplication.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## dvec3 operator* ( const dvec3 & v , const dmat4 & m )

Vector multiplication.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## dvec4 operator* ( const dmat4 & m , const dvec4 & v )

Vector multiplication.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## dvec4 operator* ( const dvec4 & v , const dmat4 & m )

Vector multiplication.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v** - The value of the vector.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m** - The value of the matrix.

### Return value

Resulting vector.
## dmat4 operator* ( const dmat4 & m0 , const dmat4 & m1 )

Matrix multiplication.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## quat operator* ( const quat & q , float v )

Quaternion multiplication.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - The value of the quaternion.
- *float* **v** - The value of the scalar.

### Return value

The resulting quaternion.
## vec3 operator* ( const quat & q , const vec3 & v )

Quaternion multiplication.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - The value of the quaternion.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## vec3 operator* ( const vec3 & v , const quat & q )

Quaternion multiplication.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - The value of the vector.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - The value of the quaternion.

### Return value

Resulting vector.
## dvec3 operator* ( const quat & q , const dvec3 & v )

Quaternion multiplication.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - The value of the quaternion.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.

### Return value

Resulting vector.
## dvec3 operator* ( const dvec3 & v , const quat & q )

Quaternion multiplication.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - The value of the vector.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q** - The value of the quaternion.

### Return value

Resulting vector.
## quat operator* ( const quat & q0 , const quat & q1 )

Quaternion multiplication.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q0** - The value of the first quaternion.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q1** - The value of the second quaternion.

### Return value

The resulting quaternion.
## vec2 operator+ ( const vec2 & v0 , const vec2 & v1 )

Vector addition.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec3 operator+ ( const vec3 & v0 , const vec3 & v1 )

Vector addition.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec3 operator+ ( const vec3 & v0 , const float & v1 )

Adds the float value to all vector components.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Vector.
- *const float &* **v1** - Float value.

### Return value

Resulting vector.
## vec4 operator+ ( const vec4 & v0 , const vec4 & v1 )

Vector addition.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec2 operator+ ( const dvec2 & v0 , const dvec2 & v1 )

Vector addition.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec3 operator+ ( const dvec3 & v0 , const dvec3 & v1 )

Vector addition.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec4 operator+ ( const dvec4 & v0 , const dvec4 & v1 )

Vector addition.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec2 operator+ ( const ivec2 & v0 , const ivec2 & v1 )

Vector addition.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - First vector.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec3 operator+ ( const ivec3 & v0 , const ivec3 & v1 )

Vector addition.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec4 operator+ ( const ivec4 & v0 , const ivec4 & v1 )

Vector addition.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - First vector.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## mat4 operator+ ( const mat4 & m0 , const mat4 & m1 )

Matrix addition.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## dmat4 operator+ ( const dmat4 & m0 , const dmat4 & m1 )

Matrix addition.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## quat operator+ ( const quat & q0 , const quat & q1 )

Quaternion addition.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q0** - The value of the first quaternion.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q1** - The value of the second quaternion.

### Return value

The resulting quaternion.
## String operator+ ( const String & s0 , const String & s1 )

String addition.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s0** - The first string.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **s1** - The second string.

## String operator+ ( )

## String operator+ ( )

## vec2 operator- ( const vec2 & v0 , const vec2 & v1 )

Vector subtraction.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec3 operator- ( const vec3 & v0 , const vec3 & v1 )

Vector subtraction.
### Arguments

- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - First vector.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec4 operator- ( const vec4 & v0 , const vec4 & v1 )

Vector subtraction.
### Arguments

- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v0** - First vector.
- *const [vec4](../../../api/library/math/class.vec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec2 operator- ( const dvec2 & v0 , const dvec2 & v1 )

Vector subtraction.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - First vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec3 operator- ( const dvec3 & v0 , const dvec3 & v1 )

Vector subtraction.
### Arguments

- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v0** - First vector.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## dvec4 operator- ( const dvec4 & v0 , const dvec4 & v1 )

Vector subtraction.
### Arguments

- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v0** - First vector.
- *const [dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec2 operator- ( const ivec2 & v0 , const ivec2 & v1 )

Vector subtraction.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - First vector.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec3 operator- ( const ivec3 & v0 , const ivec3 & v1 )

Vector subtraction.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec4 operator- ( const ivec4 & v0 , const ivec4 & v1 )

Vector subtraction.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - First vector.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## mat4 operator- ( const mat4 & m0 , const mat4 & m1 )

Matrix subtraction.
### Arguments

- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [mat4](../../../api/library/math/class.mat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## dmat4 operator- ( const dmat4 & m0 , const dmat4 & m1 )

Matrix subtraction.
### Arguments

- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m0** - The value of the first matrix.
- *const [dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **m1** - The value of the second matrix.

### Return value

The resulting matrix.
## quat operator- ( const quat & q0 , const quat & q1 )

Quaternion subtraction.
### Arguments

- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q0** - The value of the first quaternion.
- *const [quat](../../../api/library/math/class.quat_cpp.md) &* **q1** - The value of the second quaternion.

### Return value

The resulting quaternion.
## ivec2 operator% ( const ivec2 & v0 , int v1 )

Modulus operation.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The value of the scalar.

### Return value

Resulting vector.
## ivec2 operator% ( const ivec4 & v0 , int v1 )

Modulus operation.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The value of the scalar.

### Return value

Resulting vector.
## ivec2 operator/ ( const ivec2 & v0 , int v1 )

Scalar division.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The value of the scalar.

### Return value

Resulting vector.
## ivec2 operator/ ( const ivec2 & v0 , const ivec2 & v1 )

Vector division.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - First vector.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec3 operator/ ( const ivec3 & v0 , int v1 )

Scalar division.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The value of the scalar.

### Return value

Resulting vector.
## ivec3 operator/ ( const ivec3 & v0 , const ivec3 & v1 )

Vector division.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - First vector.
- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## vec2 operator/ ( const vec2 & v0 , const ivec2 & v1 )

Vector division.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - First vector.
- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec4 operator/ ( const ivec4 & v0 , int v1 )

Scalar division.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The value of the scalar.

### Return value

Resulting vector.
## ivec4 operator/ ( const ivec4 & v0 , const ivec4 & v1 )

Vector division.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - First vector.
- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v1** - Second vector.

### Return value

Resulting vector.
## ivec2 operator<< ( const ivec2 & v0 , int v1 )

Left bit shift.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The shift amount.

### Return value

Resulting vector.
## ivec3 operator<< ( const ivec3 & v0 , int v1 )

Left bit shift.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The shift amount.

### Return value

Resulting vector.
## ivec4 operator<< ( const ivec4 & v0 , int v1 )

Left bit shift.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The shift amount.

### Return value

Resulting vector.
## ivec2 operator>> ( const ivec2 & v0 , int v1 )

Right bit shift.
### Arguments

- *const [ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The shift amount.

### Return value

Resulting vector.
## ivec3 operator>> ( const ivec3 & v0 , int v1 )

Right bit shift.
### Arguments

- *const [ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The shift amount.

### Return value

Resulting vector.
## ivec4 operator>> ( const ivec4 & v0 , int v1 )

Right bit shift.
### Arguments

- *const [ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **v0** - The value of the vector.
- *int* **v1** - The shift amount.

### Return value

Resulting vector.
## float mod ( float x , float y )

Returns the floating-point remainder of the division operation: *first argument / second argument*.
### Arguments

- *float* **x** - Value.
- *float* **y** - Value.

### Return value

Resulting *float* value.
## double mod ( double x , double y )

Returns the floating-point remainder of the division operation: *first argument / second argument*.
### Arguments

- *double* **x** - Value.
- *double* **y** - Value.

### Return value

Resulting *double* value.
## float mad ( float a , float b , float c )

Returns the result of multiplication of the first value by the second value and addition of the third value (a * b + c).
### Arguments

- *float* **a** - Value.
- *float* **b** - Value.
- *float* **c** - Value.

### Return value

Return value.
## double mad ( double a , double b , double c )

Returns the result of multiplication of the first value by the second value and addition of the third value (a * b + c).
### Arguments

- *double* **a** - Value.
- *double* **b** - Value.
- *double* **c** - Value.

### Return value

Return value.
## int select ( int c , int v0 , int v1 )

Returns one of the two argument values (v0 and v1) based on the specified condition (c). This method is efficient for selecting between two values without branching, which can be beneficial in performance-critical code where branching might introduce overhead.
### Arguments

- *int* **c** - Condition to be checked.
- *int* **v0** - Value to be returned in case the condition is true (non-zero).
- *int* **v1** - Value to be returned in case the condition is false (zero).

### Return value

One of the two argument values (v0 and v1) based on the specified condition.
## float select ( int c , float v0 , float v1 )

Returns one of the two argument values (v0 and v1) based on the specified condition (c). This method is efficient for selecting between two values without branching, which can be beneficial in performance-critical code where branching might introduce overhead.
### Arguments

- *int* **c** - Condition to be checked.
- *float* **v0** - Value to be returned in case the condition is true (non-zero).
- *float* **v1** - Value to be returned in case the condition is false (zero).

### Return value

One of the two argument values (v0 and v1) based on the specified condition.
## float select ( float c , float v0 , float v1 )

Returns one of the two argument values (v0 and v1) based on the specified condition (c). This method is efficient for selecting between two values without branching, which can be beneficial in performance-critical code where branching might introduce overhead.
### Arguments

- *float* **c** - Condition to be checked.
- *float* **v0** - Value to be returned in case the condition is true (non-zero).
- *float* **v1** - Value to be returned in case the condition is false (zero).

### Return value

One of the two argument values (v0 and v1) based on the specified condition.
## int operator< ( const dvec2 & v0 , const dvec2 & v1 )

Vector less than comparison.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - The first vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - The second vector.

## int operator< ( const String & s0 , const String & s1 )

String less than comparison.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s0** - The first string.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **s1** - The second string.

## int operator< ( )

## int operator< ( )

## int operator> ( const dvec2 & v0 , const dvec2 & v1 )

Vector greater than comparison.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - The first vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - The second vector.

## int operator> ( const String & s0 , const String & s1 )

String greater than comparison.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s0** - The first string.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **s1** - The second string.

## int operator> ( )

## int operator> ( )

## int operator<= ( const dvec2 & v0 , const dvec2 & v1 )

Vector less than or equal comparison.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - The first vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - The second vector.

## int operator<= ( const String & s0 , const String & s1 )

String less or equal to comparison.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s0** - The first string.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **s1** - The second string.

## int operator<= ( )

## int operator<= ( )

## int operator>= ( const dvec2 & v0 , const dvec2 & v1 )

Vector greater than or equal comparison.
### Arguments

- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v0** - The first vector.
- *const [dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **v1** - The second vector.

## int operator>= ( const String & s0 , const String & s1 )

String greater or equal to comparison.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s0** - The first string.
- *const [String](../../../api/library/common/class.string_cpp.md) &* **s1** - The second string.

## int operator>= ( )

## int operator>= ( )

## FloatTransform inverse ( const FloatTransform & t )

Returns the inverse of the given [FloatTransform](../../../api/library/math/class.floattransform_cpp.md). The result is computed component-wise: inverted scale, inverted rotation, and offset position.
### Arguments

- *const FloatTransform &* **t** - Source transform.

### Return value

Inverse of the transform.
## FloatTransform & inverse ( FloatTransform & ret , const FloatTransform & t )

Computes the inverse of the given [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) and stores it in the provided output.
### Arguments

- *FloatTransform &* **ret** - Output to store the result.
- *const FloatTransform &* **t** - Source transform.

### Return value

Reference to the output.
## FloatTransform mul ( const FloatTransform & t0 , const FloatTransform & t1 )

Combines two [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) values by composing their components independently: scales are multiplied component-wise, rotations are composed as quaternions, and positions are accumulated taking parent scale and rotation into account.
### Arguments

- *const FloatTransform &* **t0** - Parent transform.
- *const FloatTransform &* **t1** - Child transform.

### Return value

Combined transform.
## FloatTransform & mul ( FloatTransform & ret , const FloatTransform & t0 , const FloatTransform & t1 )

Combines two [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) values and stores the result in the provided output.
### Arguments

- *FloatTransform &* **ret** - Output to store the result.
- *const FloatTransform &* **t0** - Parent transform.
- *const FloatTransform &* **t1** - Child transform.

### Return value

Reference to the output.
## vec3 mul ( const FloatTransform & t , const vec3 & v )

Applies a [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) to a [vec3](../../../api/library/math/class.vec3_cpp.md) point: scales and rotates the point, then adds the transform position.
### Arguments

- *const FloatTransform &* **t** - Transform to apply.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Point to transform.

### Return value

Transformed point.
## dvec3 mul ( const FloatTransform & t , const dvec3 & v )

Applies a [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) to a [dvec3](../../../api/library/math/class.dvec3_cpp.md) point: scales and rotates the point, then adds the transform position.
### Arguments

- *const FloatTransform &* **t** - Transform to apply.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Point to transform.

### Return value

Transformed point.
## FloatTransform blendTransform ( const FloatTransform & t0 , const FloatTransform & t1 , float k )

Interpolates between two [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) values. Position and scale are linearly interpolated; rotation is interpolated using spherical linear interpolation (slerp).
### Arguments

- *const FloatTransform &* **t0** - Start transform.
- *const FloatTransform &* **t1** - End transform.
- *float* **k** - Interpolation factor in the [0, 1] range.

### Return value

Interpolated transform.
## FloatTransform operator* ( const FloatTransform & a , const FloatTransform & b )

Combines two [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) values. Equivalent to *mul(a, b)*.
### Arguments

- *const FloatTransform &* **a** - Parent transform.
- *const FloatTransform &* **b** - Child transform.

### Return value

Combined transform.
## vec3 operator* ( const FloatTransform & t , const vec3 & v )

Applies a [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) to a [vec3](../../../api/library/math/class.vec3_cpp.md) point. Equivalent to *mul(t, v)*.
### Arguments

- *const FloatTransform &* **t** - Transform to apply.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Point to transform.

### Return value

Transformed point.
## dvec3 operator* ( const FloatTransform & t , const dvec3 & v )

Applies a [FloatTransform](../../../api/library/math/class.floattransform_cpp.md) to a [dvec3](../../../api/library/math/class.dvec3_cpp.md) point. Equivalent to *mul(t, v)*.
### Arguments

- *const FloatTransform &* **t** - Transform to apply.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Point to transform.

### Return value

Transformed point.
## DoubleTransform inverse ( const DoubleTransform & t )

Returns the inverse of the given [DoubleTransform](../../../api/library/math/class.doubletransform_cpp.md).
### Arguments

- *const DoubleTransform &* **t** - Source transform.

### Return value

Inverse of the transform.
## DoubleTransform & inverse ( DoubleTransform & ret , const DoubleTransform & t )

Computes the inverse of the given [DoubleTransform](../../../api/library/math/class.doubletransform_cpp.md) and stores it in the provided output.
### Arguments

- *DoubleTransform &* **ret** - Output to store the result.
- *const DoubleTransform &* **t** - Source transform.

### Return value

Reference to the output.
## DoubleTransform mul ( const DoubleTransform & t0 , const DoubleTransform & t1 )

Combines two [DoubleTransform](../../../api/library/math/class.doubletransform_cpp.md) values by composing their components independently. Position arithmetic is performed in double precision.
### Arguments

- *const DoubleTransform &* **t0** - Parent transform.
- *const DoubleTransform &* **t1** - Child transform.

### Return value

Combined transform.
## vec3 mul ( const DoubleTransform & t , const vec3 & v )

Applies a [DoubleTransform](../../../api/library/math/class.doubletransform_cpp.md) to a [vec3](../../../api/library/math/class.vec3_cpp.md) point. The result is returned as float precision.
### Arguments

- *const DoubleTransform &* **t** - Transform to apply.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Point to transform.

### Return value

Transformed point.
## dvec3 mul ( const DoubleTransform & t , const dvec3 & v )

Applies a [DoubleTransform](../../../api/library/math/class.doubletransform_cpp.md) to a [dvec3](../../../api/library/math/class.dvec3_cpp.md) point in full double precision.
### Arguments

- *const DoubleTransform &* **t** - Transform to apply.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Point to transform.

### Return value

Transformed point.
## DoubleTransform blendTransform ( const DoubleTransform & t0 , const DoubleTransform & t1 , float k )

Interpolates between two [DoubleTransform](../../../api/library/math/class.doubletransform_cpp.md) values. Position and scale are linearly interpolated; rotation is interpolated using spherical linear interpolation (slerp).
### Arguments

- *const DoubleTransform &* **t0** - Start transform.
- *const DoubleTransform &* **t1** - End transform.
- *float* **k** - Interpolation factor in the [0, 1] range.

### Return value

Interpolated transform.
## vec3 operator* ( const DoubleTransform & t , const vec3 & v )

Applies a [DoubleTransform](../../../api/library/math/class.doubletransform_cpp.md) to a [vec3](../../../api/library/math/class.vec3_cpp.md) point. Equivalent to *mul(t, v)*.
### Arguments

- *const DoubleTransform &* **t** - Transform to apply.
- *const [vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Point to transform.

### Return value

Transformed point.
## dvec3 operator* ( const DoubleTransform & t , const dvec3 & v )

Applies a [DoubleTransform](../../../api/library/math/class.doubletransform_cpp.md) to a [dvec3](../../../api/library/math/class.dvec3_cpp.md) point. Equivalent to *mul(t, v)*.
### Arguments

- *const DoubleTransform &* **t** - Transform to apply.
- *const [dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **v** - Point to transform.

### Return value

Transformed point.
## vec3 getWeightedAverage ( const Vector < vec3 > & points , const Vector <float> & normalized_weights )

Returns the weighted average of an array of [vec3](../../../api/library/math/class.vec3_cpp.md) points using the given normalized weights. The weights must be normalized (sum to 1), such as those produced by *blend1DWeights()* or *blend2DCartesianWeights()*.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec3](../../../api/library/math/class.vec3_cpp.md)> &* **points** - Array of points.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **normalized_weights** - Array of normalized weights. Must sum to 1.

### Return value

Weighted average position.
## quat getWeightedAverage ( const Vector < quat > & rotations , const Vector <float> & normalized_weights )

Returns the weighted average of an array of [quat](../../../api/library/math/class.quat_cpp.md) rotations using the given normalized weights. Rotations are accumulated using sequential slerp, weighted by each element's contribution relative to the running total.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[quat](../../../api/library/math/class.quat_cpp.md)> &* **rotations** - Array of rotations.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **normalized_weights** - Array of normalized weights. Must sum to 1.

### Return value

Weighted average rotation.
## void blend1DWeights ( float blend_point , Vector <WeightPoint1D> & sorted_points )

Computes normalized blend weights for a set of 1D points using Gradient Band Interpolation and writes the results back into each element's *normalized_weight* field. Points must be sorted by *position* in ascending order. If the query point lies outside the range of the provided points, full weight is assigned to the nearest endpoint.
### Arguments

- *float* **blend_point** - The query position on the 1D axis.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<WeightPoint1D> &* **sorted_points** - Array of blend points sorted by position. On return, the *normalized_weight* field of each element is updated.

## void blend1DWeights ( float blend_point , const Vector <float> & sorted_points , Vector <float> & out_normalized_weights )

Computes normalized blend weights for a set of 1D points and writes them to the output array. Points must be sorted in ascending order. If the query point lies outside the range, full weight is assigned to the nearest endpoint.
### Arguments

- *float* **blend_point** - The query position on the 1D axis.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **sorted_points** - Array of positions sorted in ascending order.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **out_normalized_weights** - Output array that receives the normalized weight for each point.

## void blend2DCartesianWeights ( const vec2 & blend_point , Vector <WeightPoint2D> & points )

Computes normalized blend weights for a set of 2D points in Cartesian coordinates using Gradient Band Interpolation and writes the results into each element's *normalized_weight* field. Suitable for blend spaces where directions are spread across a flat 2D plane.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **blend_point** - The 2D query position.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<WeightPoint2D> &* **points** - Array of blend points. On return, the *normalized_weight* field of each element is updated.

## void blend2DCartesianWeights ( const vec2 & blend_point , const Vector < vec2 > & points , Vector <float> & out_normalized_weights )

Computes normalized blend weights for a set of 2D points in Cartesian coordinates and writes them to the output array.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **blend_point** - The 2D query position.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **points** - Array of 2D positions.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **out_normalized_weights** - Output array that receives the normalized weight for each point.

## void blend2DPolarWeights ( const vec2 & blend_point , Vector <WeightPoint2D> & points )

Computes normalized blend weights for a set of 2D points in polar coordinates using Gradient Band Interpolation and writes the results into each element's *normalized_weight* field. Suitable for directional blend spaces such as locomotion (speed and direction).
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **blend_point** - The 2D query position.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<WeightPoint2D> &* **points** - Array of blend points. On return, the *normalized_weight* field of each element is updated.

## void blend2DPolarWeights ( const vec2 & blend_point , Vector < vec2 > & points , Vector <float> & out_normalized_weights )

Computes normalized blend weights for a set of 2D points in polar coordinates and writes them to the output array.
### Arguments

- *const [vec2](../../../api/library/math/class.vec2_cpp.md) &* **blend_point** - The 2D query position.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[vec2](../../../api/library/math/class.vec2_cpp.md)> &* **points** - Array of 2D positions.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **out_normalized_weights** - Output array that receives the normalized weight for each point.
