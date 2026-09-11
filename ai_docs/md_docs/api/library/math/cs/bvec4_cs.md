# Unigine.bvec4 Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


## bvec4 Class

### Properties

## 🔒︎ byte x

The X component of the vector.
## 🔒︎ byte y

The Y component of the vector.
## 🔒︎ byte z

The Z component of the vector.
## 🔒︎ byte w

The W component of the vector.
## 🔒︎ byte Minimum

The Minimum value among all components.
## 🔒︎ byte Maximum

The Maximum value among all components.
## 🔒︎ int Length2

The Squared length of the vector. This method is much faster than *length()* � the calculation is basically the same only without the slow *Sqrt* call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
## 🔒︎ int Sum

The Sum of vector components.
## 🔒︎ bvec4 ZERO

The Vector, filled with zeros (0).
## 🔒︎ bvec4 ONE

The Vector, filled with ones (1).
## 🔒︎ byte NUM_ELEMENTS

The Number of elements in the vector.
### Members

---

## ivec4 operator* ( bvec4 v0 , ivec2 v1 )

Multiplication.
### Arguments

- *bvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## ivec4 operator* ( bvec4 v0 , ivec3 v1 )

Multiplication.
### Arguments

- *bvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## ivec4 operator* ( bvec4 v0 , ivec4 v1 )

Multiplication.
### Arguments

- *bvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## ivec4 operator* ( bvec4 v0 , int v1 )

Multiplication.
### Arguments

- *bvec4* **v0** - First value.
- *int* **v1** - Second value.

## bvec4 operator* ( bvec4 v0 , bvec4 v1 )

Multiplication.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bvec4 operator* ( bvec4 v0 , byte v1 )

Multiplication.
### Arguments

- *bvec4* **v0** - First value.
- *byte* **v1** - Second value.

## ivec4 operator/ ( bvec4 v0 , ivec2 v1 )

Division.
### Arguments

- *bvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## ivec4 operator/ ( bvec4 v0 , ivec3 v1 )

Division.
### Arguments

- *bvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## ivec4 operator/ ( bvec4 v0 , ivec4 v1 )

Division.
### Arguments

- *bvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## ivec4 operator/ ( bvec4 v0 , int v1 )

Division.
### Arguments

- *bvec4* **v0** - First value.
- *int* **v1** - Second value.

## bvec4 operator/ ( bvec4 v0 , bvec4 v1 )

Division.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bvec4 operator/ ( bvec4 v0 , byte v1 )

Division.
### Arguments

- *bvec4* **v0** - First value.
- *byte* **v1** - Second value.

## ivec4 operator- ( bvec4 v0 , ivec2 v1 )

Subtraction.
### Arguments

- *bvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## ivec4 operator- ( bvec4 v0 , ivec3 v1 )

Subtraction.
### Arguments

- *bvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## ivec4 operator- ( bvec4 v0 , ivec4 v1 )

Subtraction.
### Arguments

- *bvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## ivec4 operator- ( bvec4 v0 , int v1 )

Subtraction.
### Arguments

- *bvec4* **v0** - First value.
- *int* **v1** - Second value.

## bvec4 operator- ( bvec4 v0 , bvec4 v1 )

Subtraction.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bvec4 operator- ( bvec4 v0 , byte v1 )

Subtraction.
### Arguments

- *bvec4* **v0** - First value.
- *byte* **v1** - Second value.

## ivec4 operator+ ( bvec4 v0 , ivec2 v1 )

Addition.
### Arguments

- *bvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## ivec4 operator+ ( bvec4 v0 , ivec3 v1 )

Addition.
### Arguments

- *bvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## ivec4 operator+ ( bvec4 v0 , ivec4 v1 )

Addition.
### Arguments

- *bvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## ivec4 operator+ ( bvec4 v0 , int v1 )

Addition.
### Arguments

- *bvec4* **v0** - First value.
- *int* **v1** - Second value.

## bvec4 operator+ ( bvec4 v0 , bvec4 v1 )

Addition.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bvec4 operator+ ( bvec4 v0 , byte v1 )

Addition.
### Arguments

- *bvec4* **v0** - First value.
- *byte* **v1** - Second value.

## ivec4 operator% ( bvec4 v0 , ivec2 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *bvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## ivec4 operator% ( bvec4 v0 , ivec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *bvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## ivec4 operator% ( bvec4 v0 , ivec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *bvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## ivec4 operator% ( bvec4 v0 , int v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *bvec4* **v0** - First value.
- *int* **v1** - Second value.

## bvec4 operator% ( bvec4 v0 , bvec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bvec4 operator% ( bvec4 v0 , byte v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *bvec4* **v0** - First value.
- *byte* **v1** - Second value.

## bvec4 operator>> ( bvec4 v0 , int v1 )

Bitwise right shift.
### Arguments

- *bvec4* **v0** - First value.
- *int* **v1** - Second value.

## bvec4 operator<< ( bvec4 v0 , int v1 )

Bitwise left shift.
### Arguments

- *bvec4* **v0** - First value.
- *int* **v1** - Second value.

## bvec4 operator++ ( bvec4 v )

Increment.
### Arguments

- *bvec4* **v** - Value.

## bvec4 operator-- ( bvec4 v )

Decrement.
### Arguments

- *bvec4* **v** - Value.

## bool operator== ( bvec4 v0 , bvec4 v1 )

Performs equal comparison.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bool operator!= ( bvec4 v0 , bvec4 v1 )

Not equal comparison.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bool operator> ( bvec4 v0 , bvec4 v1 )

Greater comparison.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bool operator< ( bvec4 v0 , bvec4 v1 )

Greater comparison.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bool operator>= ( bvec4 v0 , bvec4 v1 )

Greater than or equal to comparison.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bool operator<= ( bvec4 v0 , bvec4 v1 )

Less than or equal to comparison.
### Arguments

- *bvec4* **v0** - First value.
- *bvec4* **v1** - Second value.

## bool operatortrue ( bvec4 v )

Returns **true** if the operand is both, not **null** and not **NaN**.
### Arguments

- *bvec4* **v** - Value.

## bool operatorfalse ( bvec4 v )

Returns **true** if the operand is both, **null** and **NaN**.
### Arguments

- *bvec4* **v** - Value.

## void Set ( float vx , float vy , float vz , float vw )

Sets the value using the specified argument(s).
### Arguments

- *float* **vx** - New *float* value to be set for the first component.
- *float* **vy** - New *float* value to be set for the second component.
- *float* **vz** - New *float* value to be set for the third component.
- *float* **vw** - New *float* value to be set for the fourth component.

## void Set ( float v )

Sets the value using the specified argument(s).
### Arguments

- *float* **v** - A *float* value to be used.

## void Set ( float[] v )

Sets the value using the specified argument(s).
### Arguments

- *float[]* **v** - Source vector.

## void Set ( vec2 v , double vz , float vw )

Sets the value using the specified argument(s).
### Arguments

- *vec2* **v** - Source vector.
- *double* **vz** - New *double* value to be set for the third component.
- *float* **vw** - New *float* value to be set for the fourth component.

## void Set ( vec3 v , double vw )

Sets the value using the specified argument(s).
### Arguments

- *vec3* **v** - Source vector.
- *double* **vw** - New *double* value to be set for the fourth component.

## void Set ( vec2 v )

Sets the value using the specified argument(s).
### Arguments

- *vec2* **v** - Source vector.

## void Set ( vec3 v )

Sets the value using the specified argument(s).
### Arguments

- *vec3* **v** - Source vector.

## void Set ( vec4 v )

Sets the value using the specified argument(s).
### Arguments

- *vec4* **v** - Source vector.

## void Set ( vec4 v , float scale )

Sets the value using the specified argument(s).
### Arguments

- *vec4* **v** - Source vector.
- *float* **scale** - Scaling vector (**scale.x, scale.y, scale.z**).

## void Set ( double vx , double vy , double vz , double vw )

Sets the value using the specified argument(s).
### Arguments

- *double* **vx** - New *double* value to be set for the first component.
- *double* **vy** - New *double* value to be set for the second component.
- *double* **vz** - New *double* value to be set for the third component.
- *double* **vw** - New *double* value to be set for the fourth component.

## void Set ( double v )

Sets the value using the specified argument(s).
### Arguments

- *double* **v** - A *double* value to be used.

## void Set ( double[] v )

Sets the value using the specified argument(s).
### Arguments

- *double[]* **v** - Source vector.

## void Set ( dvec2 v , double vz , float vw )

Sets the value using the specified argument(s).
### Arguments

- *dvec2* **v** - Source vector.
- *double* **vz** - New *double* value to be set for the third component.
- *float* **vw** - New *float* value to be set for the fourth component.

## void Set ( dvec3 v , double vw )

Sets the value using the specified argument(s).
### Arguments

- *dvec3* **v** - Source vector.
- *double* **vw** - New *double* value to be set for the fourth component.

## void Set ( dvec2 v )

Sets the value using the specified argument(s).
### Arguments

- *dvec2* **v** - Source vector.

## void Set ( dvec3 v )

Sets the value using the specified argument(s).
### Arguments

- *dvec3* **v** - Source vector.

## void Set ( dvec4 v )

Sets the value using the specified argument(s).
### Arguments

- *dvec4* **v** - Source vector.

## void Set ( int vx , int vy , int vz , int vw )

Sets the value using the specified argument(s).
### Arguments

- *int* **vx** - New *int* value to be set for the first component.
- *int* **vy** - New *int* value to be set for the second component.
- *int* **vz** - New *int* value to be set for the third component.
- *int* **vw** - New *int* value to be set for the fourth component.

## void Set ( int v )

Sets the value using the specified argument(s).
### Arguments

- *int* **v** - A *int* value to be used.

## void Set ( int[] v )

Sets the value using the specified argument(s).
### Arguments

- *int[]* **v** - Source vector.

## void Set ( ivec2 v , double vz , float vw )

Sets the value using the specified argument(s).
### Arguments

- *ivec2* **v** - Source vector.
- *double* **vz** - New *double* value to be set for the third component.
- *float* **vw** - New *float* value to be set for the fourth component.

## void Set ( ivec3 v , double vw )

Sets the value using the specified argument(s).
### Arguments

- *ivec3* **v** - Source vector.
- *double* **vw** - New *double* value to be set for the fourth component.

## void Set ( ivec2 v )

Sets the value using the specified argument(s).
### Arguments

- *ivec2* **v** - Source vector.

## void Set ( ivec3 v )

Sets the value using the specified argument(s).
### Arguments

- *ivec3* **v** - Source vector.

## void Set ( ivec4 v )

Sets the value using the specified argument(s).
### Arguments

- *ivec4* **v** - Source vector.

## void Set ( byte vx , byte vy , byte vz , byte vw )

Sets the value using the specified argument(s).
### Arguments

- *byte* **vx** - New *byte* value to be set for the first component.
- *byte* **vy** - New *byte* value to be set for the second component.
- *byte* **vz** - New *byte* value to be set for the third component.
- *byte* **vw** - New *byte* value to be set for the fourth component.

## void Set ( byte v )

Sets the value using the specified argument(s).
### Arguments

- *byte* **v** - A *byte* value to be used.

## void Set ( byte[] v )

Sets the value using the specified argument(s).
### Arguments

- *byte[]* **v** - Source vector.

## void Set ( bvec4 v )

Sets the value using the specified argument(s).
### Arguments

- *bvec4* **v** - Source vector.

## void Clear ( )

Clears the value by setting all components/elements to 0.
## void Add ( bvec4 v )

Performs addition of the specified argument.
### Arguments

- *bvec4* **v** - Value.

## void Add ( byte v )

Performs addition of the specified argument.
### Arguments

- *byte* **v** - Value.

## void Sub ( bvec4 v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *bvec4* **v** - Value.

## void Sub ( byte v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *byte* **v** - Value.

## void Mul ( bvec4 v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *bvec4* **v** - Vector multiplier.

## void Mul ( byte v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *byte* **v** - A *byte* multiplier.

## void Div ( bvec4 v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *bvec4* **v** - A *bvec4* divisor value.

## void Div ( byte v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *byte* **v** - A *byte* divisor value.

## bool Equals ( bvec4 other )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *bvec4* **other** - Value to be checked for equality.

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
## IEnumerator<byte> GetEnumerator ( )

Returns an [**IEnumerator**](https://docs.microsoft.com/dotnet/api/system.collections.ienumerator?view=net-5.0) for the object.
### Return value

Return value.
## IEnumerator GetEnumerator ( )

Returns an [**IEnumerator**](https://docs.microsoft.com/dotnet/api/system.collections.ienumerator?view=net-5.0) for the object.
### Return value

Return value.
