# Math Trigonometric Functions (CPP)

**Header:** #include <UnigineMathLib.h>


This class contains basic and inverse trigonometric functions.


> **Notice:** Math trigonometrical functions are the members of the **Unigine::Math** namespace.


## Math Class

### Members

---

## float acos ( float v )

Returns the arccosine of the given argument - the angle in radians, whose cosine is equal to the argument. a == cos(acos(a)) for every value of a that is within acos()'s range.
### Arguments

- *float* **v** - Argument.

### Return value

Arccosine of the argument, in radians.
## double acos ( double v )

Returns the arccosine of the given argument - the angle in radians, whose cosine is equal to the argument. a == cos(acos(a)) for every value of a that is within acos()'s range.
### Arguments

- *double* **v** - Argument.

### Return value

Arccosine of the argument, in radians.
## float acosFast ( float a )

Returns the approximated, but calculated more quickly, arccosine of the given argument.
### Arguments

- *float* **a** - Argument, in radians.

### Return value

Approximated arccosine of the argument.
## float asin ( float v )

Returns the arcsine of the given argument - the angle in radians, whose sine is equal to the argument. a == sin(asin(a)) for every value of a that is within asin()'s range.
### Arguments

- *float* **v** - Argument.

### Return value

Arcsine of the argument, in radians.
## double asin ( double v )

Returns the arcsine of the given argument - the angle in radians, whose sine is equal to the argument. a == sin(asin(a)) for every value of a that is within asin()'s range.
### Arguments

- *double* **v** - Argument.

### Return value

Arcsine of the argument, in radians.
## float asinFast ( float a )

Returns the approximated, but calculated more quickly, arcsine of the given argument.
### Arguments

- *float* **a** - Argument, in radians.

### Return value

Approximated arcsine of the argument.
## float atan ( float v )

Returns the arctangent of the given argument - the angle in radians, whose tangent is equal to the argument. a == tan(atan(a)) for every value of a that is within atan()'s range.
### Arguments

- *float* **v** - Argument.

### Return value

Arctangent of the argument, in radians.
## double atan ( double v )

Returns the arctangent of the given argument - the angle in radians, whose tangent is equal to the argument. a == tan(atan(a)) for every value of a that is within atan()'s range.
### Arguments

- *double* **v** - Argument.

### Return value

Arctangent of the argument, in radians.
## float atan2 ( float y , float x )

Returns the arctangent of two arguments (**x** and **y**). It is similar to calculating the arctangent of **y / x**, except that the signs of both arguments are used to determine the quadrant of the result.
### Arguments

- *float* **y** - First argument.
- *float* **x** - Second argument.

### Return value

Result in radians, which is between **-PI** and **PI** (inclusive).
## double atan2 ( double y , double x )

Returns the arctangent of two arguments (**x** and **y**). It is similar to calculating the arctangent of **y / x**, except that the signs of both arguments are used to determine the quadrant of the result.
### Arguments

- *double* **y** - First argument.
- *double* **x** - Second argument.

### Return value

Result in radians, which is between **-PI** and **PI** (inclusive).
## float cos ( float a )

Returns the cosine of the given argument.
### Arguments

- *float* **a** - Argument, in radians.

### Return value

Cosine of the argument.
## double cos ( double a )

Returns the cosine of the given argument.
### Arguments

- *double* **a** - Argument, in radians.

### Return value

Cosine of the argument.
## float cosFast ( float a )

Returns the approximated, but calculated more quickly, cosine of the given argument.
### Arguments

- *float* **a** - Argument, in radians.

### Return value

Approximated cosine of the argument.
## float cosFastFixed ( float a )

Returns the approximated, but calculated more quickly, cosine of the given argument in range [-pi*0.5, pi*0.5].
### Arguments

- *float* **a** - Argument, in radians, in range [-pi*0.5, pi*0.5].

### Return value

Approximated cosine of the argument.
## float sin ( float a )

Returns the sine of the given argument.
### Arguments

- *float* **a** - Argument, in radians.

### Return value

Sine of the argument.
## double sin ( double a )

Returns the sine of the given argument.
### Arguments

- *double* **a** - Argument, in radians.

### Return value

Sine of the argument.
## float sinFast ( float a )

Returns the approximated, but calculated more quickly, sine of the given argument.
### Arguments

- *float* **a** - Argument, in radians.

### Return value

Approximated sine of the argument.
## float sinFastFixed ( float a )

Returns the approximated, but calculated more quickly, sine of the given argument in range [-pi*0.5, pi*0.5].
### Arguments

- *float* **a** - Argument, in radians, in range [-pi*0.5, pi*0.5].

### Return value

Approximated sine of the argument.
## void sincos ( float angle , float & s , float & c )

Calculates sine and cosine values for the specified angle value given in radians and puts them to **out_sin** and **out_cos**.
### Arguments

- *float* **angle** - Angle, in radians.
- *float &* **s** - Variable, to which the calculated sine value is to be put.
- *float &* **c** - Variable, to which the calculated cosine value is to be put.

## void sincos ( double angle , double & s , double & c )

Calculates sine and cosine values for the specified angle value given in radians and puts them to **out_sin** and **out_cos**.
### Arguments

- *double* **angle** - Angle, in radians.
- *double &* **s** - Variable, to which the calculated sine value is to be put.
- *double &* **c** - Variable, to which the calculated cosine value is to be put.

## void sincosFast ( float angle , float & s , float & c )

Calculates approximated sine and cosine values for the specified angle value given in radians and puts them to **out_sin** and **out_cos**.
### Arguments

- *float* **angle** - Angle, in radians.
- *float &* **s** - Variable, to which the calculated sine value is to be put.
- *float &* **c** - Variable, to which the calculated cosine value is to be put.

## float tan ( float a )

Returns the tangent of the given argument.
### Arguments

- *float* **a** - Argument, in radians.

### Return value

Tangent of the argument.
## double tan ( double a )

Returns the tangent of the given argument.
### Arguments

- *double* **a** - Argument, in radians.

### Return value

Tangent of the argument.
