# Unigine.quat Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


## quat Class

### Properties

## 🔒︎ float x

The X component of the vector.
## 🔒︎ float y

The Y component of the vector.
## 🔒︎ float z

The Z component of the vector.
## 🔒︎ float w

The W component of the vector.
## 🔒︎ float Length

The Length of the vector.
## 🔒︎ float Minimum

The Minimum value among all components.
## 🔒︎ float Maximum

The Maximum value among all components.
## 🔒︎ float Length2

The Squared length of the vector. This method is much faster than *length()* � the calculation is basically the same only without the slow *Sqrt* call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
## 🔒︎ float ILength

The Inverted length of the vector.
## 🔒︎ float Sum

The Sum of vector components.
## 🔒︎ quat Normalized

The Returns a vector with the same direction as the specified vector, but with a length of one.
## 🔒︎ mat3 Mat3

The [Mat3](../../../../api/library/math/class.mat3_cs.md) that this quaternion represents.
## 🔒︎ mat4 Mat4

The [Mat4](../../../../api/library/math/class.mat4_cs.md) that this quaternion represents.
## 🔒︎ dmat4 DMat4

The [DMat4](../../../../api/library/math/class.dmat4_cs.md) that this quaternion represents.
## 🔒︎ vec3 Euler

The Euler angles as a [vec3](../../../../api/library/math/class.vec3_cs.md) that this quaternion represents.
## 🔒︎ float EulerX

The **X** Euler angle (yaw) of this quaternion.
## 🔒︎ float EulerY

The **Y** Euler angle (roll) of this quaternion.
## 🔒︎ float EulerZ

The **Z** Euler angle (pitch) of this quaternion.
## 🔒︎ vec3 Normal

The Quaternion normal vector.
## 🔒︎ vec3 Tangent

The Quaternion tangent vector as a [vec3](../../../../api/library/math/class.vec3_cs.md).
## 🔒︎ vec4 Tangent4

The Quaternion tangent vector as a [vec4](../../../../api/library/math/class.vec4_cs.md).
## 🔒︎ vec3 Binormal

The Quaternion binormal vector with respect to orientation as a [vec3](../../../../api/library/math/class.vec3_cs.md).
## 🔒︎ quat ZERO

The Quaternion, filled with zeros (0).
## 🔒︎ quat IDENTITY

The Identity matrix.
## 🔒︎ byte NUM_ELEMENTS

The Number of elements in the vector.
### Members

---

## quat operator* ( quat q , float v )

Multiplication.
### Arguments

- *quat* **q** - Quaternion.
- *float* **v** - Value.

## vec3 operator* ( quat q , vec3 v )

Multiplication.
### Arguments

- *quat* **q** - Quaternion.
- *vec3* **v** - Value.

## vec3 operator* ( vec3 v , quat q )

Multiplication.
### Arguments

- *vec3* **v** - Value.
- *quat* **q** - Quaternion.

## dvec3 operator* ( quat q , dvec3 v )

Multiplication.
### Arguments

- *quat* **q** - Quaternion.
- *dvec3* **v** - Value.

## dvec3 operator* ( dvec3 v , quat q )

Multiplication.
### Arguments

- *dvec3* **v** - Value.
- *quat* **q** - Quaternion.

## quat operator* ( quat q0 , quat q1 )

Multiplication.
### Arguments

- *quat* **q0** - First value.
- *quat* **q1** - Second value.

## quat operator/ ( quat q , float v )

Division.
### Arguments

- *quat* **q** - Quaternion.
- *float* **v** - Value.

## quat operator/ ( quat q0 , quat q1 )

Division.
### Arguments

- *quat* **q0** - First value.
- *quat* **q1** - Second value.

## quat operator+ ( quat q0 , quat q1 )

Addition.
### Arguments

- *quat* **q0** - First value.
- *quat* **q1** - Second value.

## quat operator- ( quat q0 , quat q1 )

Subtraction.
### Arguments

- *quat* **q0** - First value.
- *quat* **q1** - Second value.

## bool operator== ( quat v0 , quat v1 )

Performs equal comparison.
### Arguments

- *quat* **v0** - First value.
- *quat* **v1** - Second value.

## bool operator!= ( quat v0 , quat v1 )

Not equal comparison.
### Arguments

- *quat* **v0** - First value.
- *quat* **v1** - Second value.

## bool operator> ( quat v0 , quat v1 )

Greater comparison.
### Arguments

- *quat* **v0** - First value.
- *quat* **v1** - Second value.

## bool operator< ( quat v0 , quat v1 )

Greater comparison.
### Arguments

- *quat* **v0** - First value.
- *quat* **v1** - Second value.

## bool operator>= ( quat v0 , quat v1 )

Greater than or equal to comparison.
### Arguments

- *quat* **v0** - First value.
- *quat* **v1** - Second value.

## bool operator<= ( quat v0 , quat v1 )

Less than or equal to comparison.
### Arguments

- *quat* **v0** - First value.
- *quat* **v1** - Second value.

## bool operatortrue ( quat v )

Returns **true** if the operand is both, not **null** and not **NaN**.
### Arguments

- *quat* **v** - Value.

## bool operatorfalse ( quat v )

Returns **true** if the operand is both, **null** and **NaN**.
### Arguments

- *quat* **v** - Value.

## quat operator- ( quat v )

Subtraction.
### Arguments

- *quat* **v** - Value.

## void Set ( quat v )

Sets the value using the specified argument(s).
### Arguments

- *quat* **v** - Source vector.

## void Set ( vec4 v )

Sets the value using the specified argument(s).
### Arguments

- *vec4* **v** - Source vector.

## void Set ( vec3 axis , float angle )

Sets the value using the specified argument(s).
### Arguments

- *vec3* **axis** - Axis of rotation.
- *float* **angle** - Angle, in degrees.

## void Set ( float[] q )

Sets the value using the specified argument(s).
### Arguments

- *float[]* **q** - Source quaternion.

## void Set ( vec3 t , vec3 b , vec3 n )

Sets the quaternion using the specified argument(s).
### Arguments

- *vec3* **t** - Tangent vector.
- *vec3* **b** - Binormal vector.
- *vec3* **n** - Normal vector.

## void Get ( vec3 axis , float angle )

Gets the axis of rotation and the angle from the quaternion and stores it to the provided arguments.
### Arguments

- *vec3* **axis** - Returned axis of rotation.
- *float* **angle** - Returned angle, in degrees.

## void Clear ( )

Clears the value by setting all components/elements to 0.
## void Add ( vec4 v )

Performs addition of the specified argument.
### Arguments

- *vec4* **v** - Value.

## void Add ( float v )

Performs addition of the specified argument.
### Arguments

- *float* **v** - Value.

## void Sub ( vec4 v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *vec4* **v** - Value.

## void Sub ( float v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *float* **v** - Value.

## void Mul ( vec4 v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *vec4* **v** - Vector multiplier.

## void Mul ( float v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *float* **v** - A *float* multiplier.

## void Div ( vec4 v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *vec4* **v** - A *vec4* divisor value.

## void Div ( float v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *float* **v** - A *float* divisor value.

## void Normalize ( )

Returns a vector with the same direction, but with a length of 1.
## float GetAngle ( vec3 axis )

Returns the angle of rotation using the provided axis.
### Arguments

- *vec3* **axis** - Axis of rotation.

### Return value

Resulting *float* value.
## bool Equals ( quat other )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *quat* **other** - Value to be checked for equality.

### Return value

Return value.
## bool EqualsNearly ( quat other , float epsilon )

Checks if the argument represents the same value with regard to the specified accuracy (epsilon).
### Arguments

- *quat* **other** - Value to be checked for equality.
- *float* **epsilon** - Epsilon value, that determines accuracy of comparison.

### Return value

Return value.
## bool Equals ( object obj )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *[object](../../../../api/library/objects/class.object_cs.md)* **obj**

### Return value

Return value.
## int GetHashCode ( )

Returns a hash code for the current object. Serves as the default hash function.
### Return value

Resulting *int* value.
## string ToString ( )

Converts the current value to a *string* value.
### Return value

Resulting *string* value.
## string ToString ( string format )

Converts the current value to a *string* value.
### Arguments

- *string* **format** - String formatting to be used. A format string is composed of zero or more ordinary characters (excluding %) that are copied directly to the result string and control sequences, each of which results in fetching its own parameter. Each control sequence consists of a percent sign (%) followed by one or more of these elements, in order:

  - An optional number, a width specifier, that says how many characters (minimum) this conversion should result in.
  - An optional precision specifier that says how many decimal digits should be displayed for floating-point numbers.
  - A type specifier that says what type the argument data should be treated as. Possible types:

    - **c**: the argument is treated as an integer and presented as a character with that ASCII value.
    - **d** or **i**: the argument is treated as an integer and presented as a (signed) decimal number.
    - **o**: the argument is treated as an integer and presented as an octal number.
    - **u**: the argument is treated as an integer and presented as an unsigned decimal number.
    - **x**: the argument is treated as an integer and presented as a hexadecimal number (with lower-case letters).
    - **X**: the argument is treated as an integer and presented as a hexadecimal number (with upper-case letters).
    - **f**: the argument is treated as a float and presented as a floating-point number.
    - **g**: the same as e or f, the shortest one is selected.
    - **G**: the same as E or F, the shortest one is selected.
    - **e**: the argument is treated as using the scientific notation with lower-case 'e' (e.g. 1.2e+2).
    - **E**: the argument is treated as using the scientific notation with upper-case 'E' (e.g. 1.2E+2).
    - **s**: the argument is treated as and presented as a string.
    - **p**: the argument is treated as and presented as a pointer address.
    - **%**: a literal percent character. No argument is required.

### Return value

Resulting *string* value.
## string ToString ( string format , IFormatProvider formatProvider )

Converts the current value to a *string* value.
### Arguments

- *string* **format** - String formatting to be used. A format string is composed of zero or more ordinary characters (excluding %) that are copied directly to the result string and control sequences, each of which results in fetching its own parameter. Each control sequence consists of a percent sign (%) followed by one or more of these elements, in order:

  - An optional number, a width specifier, that says how many characters (minimum) this conversion should result in.
  - An optional precision specifier that says how many decimal digits should be displayed for floating-point numbers.
  - A type specifier that says what type the argument data should be treated as. Possible types:

    - **c**: the argument is treated as an integer and presented as a character with that ASCII value.
    - **d** or **i**: the argument is treated as an integer and presented as a (signed) decimal number.
    - **o**: the argument is treated as an integer and presented as an octal number.
    - **u**: the argument is treated as an integer and presented as an unsigned decimal number.
    - **x**: the argument is treated as an integer and presented as a hexadecimal number (with lower-case letters).
    - **X**: the argument is treated as an integer and presented as a hexadecimal number (with upper-case letters).
    - **f**: the argument is treated as a float and presented as a floating-point number.
    - **g**: the same as e or f, the shortest one is selected.
    - **G**: the same as E or F, the shortest one is selected.
    - **e**: the argument is treated as using the scientific notation with lower-case 'e' (e.g. 1.2e+2).
    - **E**: the argument is treated as using the scientific notation with upper-case 'E' (e.g. 1.2E+2).
    - **s**: the argument is treated as and presented as a string.
    - **p**: the argument is treated as and presented as a pointer address.
    - **%**: a literal percent character. No argument is required.
- *IFormatProvider* **formatProvider** - Provider to be used to format the value. Pass a **null** reference to obtain the numeric format information from the current locale setting of the operating system.

### Return value

Resulting *string* value.
## IEnumerator<float> GetEnumerator ( )

Returns an [**IEnumerator**](https://docs.microsoft.com/dotnet/api/system.collections.ienumerator?view=net-5.0) for the object.
### Return value

Return value.
## IEnumerator GetEnumerator ( )

Returns an [**IEnumerator**](https://docs.microsoft.com/dotnet/api/system.collections.ienumerator?view=net-5.0) for the object.
### Return value

Return value.
