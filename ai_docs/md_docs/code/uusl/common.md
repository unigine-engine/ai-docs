# UUSL Common Intrinsic Functions


This documentation article contains information on the UUSL functions. This information can be used as the reference document for writing shaders.


To start using common UUSL functionality, include the `core/materials/shaders/api/common.h` file.


```glsl
#include <core/materials/shaders/api/common.h>
```


### Implementation of the API-dependent functions


The implementation of the API-dependent functions is available in the corresponding header file for your reference:


- `core/materials/shaders/api/wrapper/directx11.h`


## Float Functions


## bool equals ( float a , float b , float epsilon )

Compares two values.
### Arguments

- *float* **a** - Value to be compared.
- *float* **b** - Value to be compared.
- *float* **epsilon** - Epsilon value.

### Return value

true if A is equal to B, otherwise � false.
## bool equals ( float a , float b )

Compares two values.
### Arguments

- *float* **a** - Value to be compared.
- *float* **b** - Value to be compared.

### Return value

true if A is equal to B, otherwise � false.
## float max2 ( float2 value )

Returns the greater of the two vector components.


**Equivalent**


```glsl
max(value.r,value.g)
```


### Arguments

- *float2* **value** - Vector containing two values to be compared.

### Return value

The greater of the two vector components.
## float max2 ( float3 value )

Returns the greater of the first two vector components.


**Equivalent**


```glsl
max(value.r,value.g)
```


### Arguments

- *float3* **value** - Vector containing two values to be compared.

### Return value

The greater of the first two vector components.
## float max2 ( float4 value )

Returns the greater of the first two vector components.


**Equivalent**


```glsl
max(value.r,value.g)
```


### Arguments

- *float4* **value** - Vector containing two values to be compared.

### Return value

The greater of the first two vector components.
## float max3 ( float3 value )

Returns the greatest of the three vector components.


**Equivalent**


```glsl
max(max(value.r,value.g),value.b)
```


### Arguments

- *float3* **value** - Vector containing three values to be compared.

### Return value

The greater of the three vector components.
## float max3 ( float4 value )

Returns the greatest of the first three vector components.


**Equivalent**


```glsl
max(max(value.r,value.g),value.b)
```


### Arguments

- *float4* **value** - Vector containing three values to be compared.

### Return value

The greater of the first three vector components.
## float max3 ( float a , float b , float c )

Returns the greatest of the argument values.


**Equivalent**


```glsl
max(max(value.r,value.g),value.b)
```


### Arguments

- *float* **a** - Value to be compared.
- *float* **b** - Value to be compared.
- *float* **c** - Value to be compared.

### Return value

The greatest of the argument values.
## float max4 ( float4 value )

Returns the greatest of the four values.


**Equivalent**


```glsl
max(max(max(value.r,value.g),value.b),value.a)
```


### Arguments

- *float4* **value** - Vector containing four values to be compared.

### Return value

The maximum value.
## float max4 ( float a , float b , float c , float d )

Returns the greatest of the argument values.


**Equivalent**


```glsl
max(max(max(value.r,value.g),value.b),value.a)
```


### Arguments

- *float* **a** - Value to be compared.
- *float* **b** - Value to be compared.
- *float* **c** - Value to be compared.
- *float* **d** - Value to be compared.

### Return value

The greatest of the argument values.
## uint max4 ( uint4 value )

Returns the greatest of the four argument vector components.


**Equivalent**


```glsl
max(max(max(value.r,value.g),value.b),value.a)
```


### Arguments

- *uint4* **value** - Vector containing four values to be compared.

### Return value

The maximum value.
## float min2 ( float2 value )

Returns the lesser of the two vector components.


**Equivalent**


```glsl
min(value.r,value.g)
```


### Arguments

- *float2* **value** - Vector containing two values to be compared.

### Return value

The lower value.
## float min2 ( float3 value )

Returns the lesser of the first two vector components.


**Equivalent**


```glsl
min(value.r,value.g)
```


### Arguments

- *float3* **value** - Vector containing two values to be compared.

### Return value

The lower value.
## float min2 ( float4 value )

Returns the lesser of the first two vector components.


**Equivalent**


```glsl
min(value.r,value.g)
```


### Arguments

- *float4* **value** - Vector containing two values to be compared.

### Return value

The lower value.
## float min3 ( float3 value )

Returns the minimum of the three vector components.


**Equivalent**


```glsl
min(min(value.r,value.g),value.b)
```


### Arguments

- *float3* **value** - Vector containing three values to be compared.

### Return value

The lowest value.
## float min3 ( float a , float b , float c )

Returns the minimum of the argument values.


**Equivalent**


```glsl
min(min(value.r,value.g),value.b)
```


### Arguments

- *float* **a** - Value to be compared.
- *float* **b** - Value to be compared.
- *float* **c** - Value to be compared.

### Return value

The lowest value.
## float min3 ( float4 value )

Returns the minimum of the first three vector components.


**Equivalent**


```glsl
min(min(value.r,value.g),value.b)
```


### Arguments

- *float4* **value** - Vector containing three values to be compared.

### Return value

The lowest value.
## float min3 ( float a , float b , float c , float d )

Returns the minimum of the first three argument values.


**Equivalent**


```glsl
min(min(value.r,value.g),value.b)
```


### Arguments

- *float* **a** - Value to be compared.
- *float* **b** - Value to be compared.
- *float* **c** - Value to be compared.
- *float* **d** - Value.

### Return value

The lowest value.
## float min4 ( float4 value )

Returns the lowest of the four vector components.


**Equivalent**


```glsl
min(min(min(value.r,value.g),value.b),value.a)
```


### Arguments

- *float4* **value** - Vector containing four values to be compared.

### Return value

The lowest value.
## float min4 ( float a , float b , float c , float d )

Returns the lowest of the four argument values.


**Equivalent**


```glsl
min(min(min(value.r,value.g),value.b),value.a)
```


### Arguments

- *float* **a** - Value to be compared.
- *float* **b** - Value to be compared.
- *float* **c** - Value to be compared.
- *float* **d** - Value to be compared.

### Return value

The lowest value.
## float2 maxFloat2 ( float2 a , float2 b )

Returns a vector containing the greater values of the corresponding components of the two vectors.
### Arguments

- *float2* **a** - Vector to be compared.
- *float2* **b** - Vector to be compared.

### Return value

The vector containing the maximum values resulting from a per-component comparison of the argument vectors.
## float2 maxFloat2 ( float2 a , float2 b , float2 c )

Returns a vector containing the greatest values of the corresponding components of the three vectors.
### Arguments

- *float2* **a** - Vector to be compared.
- *float2* **b** - Vector to be compared.
- *float2* **c** - Vector to be compared.

### Return value

The vector containing the maximum values resulting from a per-component comparison of the argument vectors.
## float2 maxFloat2 ( float2 a , float2 b , float2 c , float2 d )

Returns a vector containing the greatest values of the corresponding components of the four vectors.
### Arguments

- *float2* **a** - Vector to be compared.
- *float2* **b** - Vector to be compared.
- *float2* **c** - Vector to be compared.
- *float2* **d** - Vector to be compared.

### Return value

The vector containing the maximum values resulting from a per-component comparison of the argument vectors.
## float3 maxFloat3 ( float3 a , float3 b )

Returns a vector containing the greater values of the corresponding components of the two vectors.
### Arguments

- *float3* **a** - Vector to be compared.
- *float3* **b** - Vector to be compared.

### Return value

The vector containing the maximum values resulting from a per-component comparison of the argument vectors.
## float3 maxFloat3 ( float3 a , float3 b , float3 c )

Returns a vector containing the greatst values of the corresponding components of the three vectors.
### Arguments

- *float3* **a** - Vector to be compared.
- *float3* **b** - Vector to be compared.
- *float3* **c** - Vector to be compared.

### Return value

The vector containing the maximum values resulting from a per-component comparison of the argument vectors.
## float3 maxFloat3 ( float3 a , float3 b , float3 c , float3 d )

Returns a vector containing the greatest values of the corresponding components of the four vectors.
### Arguments

- *float3* **a** - Vector to be compared.
- *float3* **b** - Vector to be compared.
- *float3* **c** - Vector to be compared.
- *float3* **d** - Vector to be compared.

### Return value

The vector containing the maximum values resulting from a per-component comparison of the argument vectors.
## float4 maxFloat4 ( float4 a , float4 b )

Returns a vector containing the greater values of the corresponding components of the two vectors.
### Arguments

- *float4* **a** - Vector to be compared.
- *float4* **b** - Vector to be compared.

### Return value

The vector containing the maximum values resulting from a per-component comparison of the argument vectors.
## float4 maxFloat4 ( float4 a , float4 b , float4 c )

Returns a vector containing the greatest values of the corresponding components of the three vectors.
### Arguments

- *float4* **a** - Vector to be compared.
- *float4* **b** - Vector to be compared.
- *float4* **c** - Vector to be compared.

### Return value

The vector containing the maximum values resulting from a per-component comparison of the argument vectors.
## float4 maxFloat4 ( float4 a , float4 b , float4 c , float4 d )

Returns a vector containing the greatest values of the corresponding components of the four vectors.
### Arguments

- *float4* **a** - Vector to be compared.
- *float4* **b** - Vector to be compared.
- *float4* **c** - Vector to be compared.
- *float4* **d** - Vector to be compared.

### Return value

The vector containing the maximum values resulting from a per-component comparison of the argument vectors.
## float2 minFloat2 ( float2 a , float2 b )

Returns a vector containing the lesser values of the corresponding components of the two vectors.
### Arguments

- *float2* **a** - Vector to be compared.
- *float2* **b** - Vector to be compared.

### Return value

The vector containing the minimum values resulting from a per-component comparison of the argument vectors.
## float2 minFloat2 ( float2 a , float2 b , float2 c )

Returns a vector containing the minimum values of the corresponding components of the three vectors.
### Arguments

- *float2* **a** - Vector to be compared.
- *float2* **b** - Vector to be compared.
- *float2* **c** - Vector to be compared.

### Return value

The vector containing the minimum values resulting from a per-component comparison of the argument vectors.
## float2 minFloat2 ( float2 a , float2 b , float2 c , float2 d )

Returns a vector containing the minimum values of the corresponding components of the four vectors.
### Arguments

- *float2* **a** - Vector to be compared.
- *float2* **b** - Vector to be compared.
- *float2* **c** - Vector to be compared.
- *float2* **d** - Vector to be compared.

### Return value

The vector containing the minimum values resulting from a per-component comparison of the argument vectors.
## float3 minFloat3 ( float3 a , float3 b )

Returns a vector containing the lesser values of the corresponding components of the two vectors.
### Arguments

- *float3* **a** - Vector to be compared.
- *float3* **b** - Vector to be compared.

### Return value

The vector containing the minimum values resulting from a per-component comparison of the argument vectors.
## float3 minFloat3 ( float3 a , float3 b , float3 c )

Returns a vector containing the minimum values of the corresponding components of the three vectors.
### Arguments

- *float3* **a** - Vector to be compared.
- *float3* **b** - Vector to be compared.
- *float3* **c** - Vector to be compared.

### Return value

The vector containing the minimum values resulting from a per-component comparison of the argument vectors.
## float3 minFloat3 ( float3 a , float3 b , float3 c , float3 d )

Returns a vector containing the minimum values of the corresponding components of the four vectors.
### Arguments

- *float3* **a** - Vector to be compared.
- *float3* **b** - Vector to be compared.
- *float3* **c** - Vector to be compared.
- *float3* **d** - Vector to be compared.

### Return value

The vector containing the minimum values resulting from a per-component comparison of the argument vectors.
## float4 minFloat4 ( float4 a , float4 b )

Returns a vector containing the lesser values of the corresponding components of the two vectors.
### Arguments

- *float4* **a** - Vector to be compared.
- *float4* **b** - Vector to be compared.

### Return value

The vector containing the minimum values resulting from a per-component comparison of the argument vectors.
## float4 minFloat4 ( float4 a , float4 b , float4 c )

Returns a vector containing the minimum values of the corresponding components of the three vectors.
### Arguments

- *float4* **a** - Vector to be compared.
- *float4* **b** - Vector to be compared.
- *float4* **c** - Vector to be compared.

### Return value

The vector containing the minimum values resulting from a per-component comparison of the argument vectors.
## float4 minFloat4 ( float4 a , float4 b , float4 c , float4 d )

Returns a vector containing the minimum values of the corresponding components of the four vectors.
### Arguments

- *float4* **a** - Vector to be compared.
- *float4* **b** - Vector to be compared.
- *float4* **c** - Vector to be compared.
- *float4* **d** - Vector to be compared.

### Return value

The vector containing the minimum values resulting from a per-component comparison of the argument vectors.
## float dotFixed ( float a , float b )

Returns the dot product of two values within the range of 0 to 1.


**Equivalent**


```glsl
saturate(dot(X,Y))
```


### Arguments

- *float* **a** - The first value.
- *float* **b** - The second value.

### Return value

Dot product within the range of 0 to 1.
## float dotFixed ( float2 a , float2 b )

Returns the dot product of two vectors within the range of 0 to 1.


**Equivalent**


```glsl
saturate(dot(X,Y))
```


### Arguments

- *float2* **a** - The first vector.
- *float2* **b** - The second vector.

### Return value

Dot product within the range of 0 to 1.
## float dotFixed ( float3 a , float3 b )

Returns the dot product of two vectors within the range of 0 to 1.


**Equivalent**


```glsl
saturate(dot(X,Y)))
```


### Arguments

- *float3* **a** - The first vector.
- *float3* **b** - The second vector.

### Return value

Dot product within the range of 0 to 1.
## float dotFixed ( float4 a , float4 b )

Returns the dot product of two vectors within the range of 0 to 1.


**Equivalent**


```glsl
saturate(dot(X,Y)))
```


### Arguments

- *float4* **a** - The first vector.
- *float4* **b** - The second vector.

### Return value

Dot product within the range of 0 to 1.
## float lerpFixed ( float a , float b , float coef )

Performs a linear interpolation of two values with the coefficient in the range of 0 to 1.


**Equivalent**


```glsl
lerp(X,Y,saturate(FACTOR))
```


### Arguments

- *float* **a** - The first value.
- *float* **b** - The second value.
- *float* **coef** - A value that linearly interpolates between the a value and the b value.

### Return value

Interpolated value.
## float2 lerpFixed ( float2 a , float2 b , float coef )

Performs a linear interpolation of two vectors with the coefficient in the range of 0 to 1.


**Equivalent**


```glsl
lerp(X,Y,saturate(FACTOR))
```


### Arguments

- *float2* **a** - The first vector.
- *float2* **b** - The second vector.
- *float* **coef** - A value that linearly interpolates between the corresponding components of the a vector and the b vector.

### Return value

Vector containing interpolated values.
## float3 lerpFixed ( float3 a , float3 b , float coef )

Performs a linear interpolation of two vectors with the coefficient in the range of 0 to 1.


**Equivalent**


```glsl
lerp(X,Y,saturate(FACTOR))
```


### Arguments

- *float3* **a** - The first vector.
- *float3* **b** - The second vector.
- *float* **coef** - A value that linearly interpolates between the corresponding components of the a vector and the b vector.

### Return value

Vector containing interpolated values.
## float4 lerpFixed ( float4 a , float4 b , float coef )

Performs a linear interpolation of two vectors with the coefficient in the range of 0 to 1.


**Equivalent**


```glsl
lerp(X,Y,saturate(FACTOR))
```


### Arguments

- *float4* **a** - The first vector.
- *float4* **b** - The second vector.
- *float* **coef** - A value that linearly interpolates between the corresponding components of the a vector and the b vector.

### Return value

Vector containing interpolated values.
## float2 lerpFixed ( float2 a , float2 b , float2 coef )

Performs a linear interpolation of two vectors with the coefficient in the range of 0 to 1 specified per component.


**Equivalent**


```glsl
lerp(X,Y,saturate(FACTOR))
```


### Arguments

- *float2* **a** - The first vector.
- *float2* **b** - The second vector.
- *float2* **coef** - Vector containing values that linearly interpolate between the corresponding components of the a vector and the b vector.

### Return value

Vector containing interpolated values.
## float3 lerpFixed ( float3 a , float3 b , float3 coef )

Performs a linear interpolation of two vectors with the coefficient in the range of 0 to 1 specified per component.


**Equivalent**


```glsl
lerp(X,Y,saturate(FACTOR))
```


### Arguments

- *float3* **a** - The first vector.
- *float3* **b**
- *float3* **coef** - Vector containing values that linearly interpolate between the corresponding components of the a vector and the b vector.

### Return value

Vector containing interpolated values.
## float4 lerpFixed ( float4 a , float4 b , float4 coef )

Performs a linear interpolation of two vectors with the coefficient in the range of 0 to 1 specified per component.


**Equivalent**


```glsl
lerp(X,Y,saturate(FACTOR))
```


### Arguments

- *float4* **a** - The first vector.
- *float4* **b**
- *float4* **coef** - Vector containing values that linearly interpolate between the corresponding components of the a vector and the b vector.

### Return value

Vector containing interpolated values.
## float lerpOne ( float value , float coef )

Performs the interpolation of the following type:


**Equivalent**


```glsl
value * (1.0f - factor) + factor;
```


### Arguments

- *float* **value** - Value for interpolation.
- *float* **coef** - Interpolation coefficient.

### Return value

Interpolated value.
## float2 lerpOne ( float2 value , float coef )

Performs the interpolation of the following type for each vector component:


**Equivalent**


```glsl
value * (1.0f - factor) + factor;
```


### Arguments

- *float2* **value** - Vector containing values for interpolation.
- *float* **coef** - Interpolation coefficient.

### Return value

Vector with interpolated values.
## float3 lerpOne ( float3 value , float coef )

Performs the interpolation of the following type for each vector component:


**Equivalent**


```glsl
value * (1.0f - factor) + factor;
```


### Arguments

- *float3* **value** - Vector containing values for interpolation.
- *float* **coef** - Interpolation coefficient.

### Return value

Vector with interpolated values.
## float4 lerpOne ( float4 value , float coef )

Performs the interpolation of the following type for each vector component:


**Equivalent**


```glsl
value * (1.0f - factor) + factor;
```


### Arguments

- *float4* **value** - Vector containing values for interpolation.
- *float* **coef** - Interpolation coefficient.

### Return value

Vector with interpolated values.
## float lerpZero ( float value , float coef )

Performs the interpolation of the following type: value * (1.0f - coef).
### Arguments

- *float* **value** - Value for interpolation.
- *float* **coef** - Interpolation coefficient.

### Return value

Interpolated value.
## float2 lerpZero ( float2 value , float coef )

Performs the interpolation of the following type for each vector component: value * (1.0f - coef).
### Arguments

- *float2* **value** - Vector containing values for interpolation.
- *float* **coef** - Interpolation coefficient.

### Return value

Vector with interpolated values.
## float3 lerpZero ( float3 value , float coef )

Performs the interpolation of the following type for each vector component: value * (1.0f - coef).
### Arguments

- *float3* **value** - Vector containing values for interpolation.
- *float* **coef** - Interpolation coefficient.

### Return value

Vector with interpolated values.
## float4 lerpZero ( float4 value , float coef )

Performs the interpolation of the following type for each vector component: value * (1.0f - coef).
### Arguments

- *float4* **value** - Vector containing values for interpolation.
- *float* **coef** - Interpolation coefficient.

### Return value

Vector with interpolated values.
## float2 rotateUV ( float2 uv , float angle )

Rotates the source UV coordinates to a specified angle, in degrees, and outputs the resulting UV coordinates.
### Arguments

- *float2* **uv** - Source UV coordinates.
- *float* **angle** - Rotation angle, in degrees.

### Return value

Resulting UV coordinates.
## float3 colorSaturation ( float3 color , float saturation )

Returns the color with the saturation value applied.
### Arguments

- *float3* **color** - Color.
- *float* **saturation** - Saturation value from 0 to 1, where the extreme value of 0 makes the color grey and 1 keeps the argument color unchanged.

### Return value

Resulting color.
## float rgbToLuma ( float3 color )

Returns the perceived brightness of the color.
### Arguments

- *float3* **color** - Color.

### Return value

Perceived brightness of the color.
## float rgbToLuma ( float4 color )

Returns the perceived brightness of the color.
### Arguments

- *float4* **color** - Color.

### Return value

Perceived brightness of the color.
## float length2 ( float2 vec )

Returns dot product of the vector: dot(vector, vector).
### Arguments

- *float2* **vec** - Vector.

### Return value

Calculated dot product.
## float length2 ( float3 vec )

Returns dot product of the vector: dot(vector, vector).
### Arguments

- *float3* **vec** - Vector.

### Return value

Calculated dot product.
## float4 lerp3 ( float4 a , float4 b , float4 c , float coef )


Performs linear interpolation between three vectors.


**Equivalent**


```glsl
if (a < 0.5)
{
	lerp(v0, v1, a * 2.0f);
}
else
{
	lerp(v1, v2, a * 2.0f - 1.0f);
	}

```


### Arguments

- *float4* **a** - First vector.
- *float4* **b** - Second vector.
- *float4* **c** - Third vector.
- *float* **coef** - Interpolation coefficient in the range [0.0f, 1.0f].

### Return value

Interpolated vector.
## float3 lerp3 ( float3 a , float3 b , float3 c , float coef )


Performs linear interpolation between three vectors.


**Equivalent**


```glsl
if (a < 0.5)
{
	lerp(v0, v1, a * 2.0f);
}
else
{
	lerp(v1, v2, a * 2.0f - 1.0f);
	}

```


### Arguments

- *float3* **a** - First vector.
- *float3* **b** - Second vector.
- *float3* **c** - Third vector.
- *float* **coef** - Interpolation coefficient in the range [0.0f, 1.0f].

### Return value

Interpolated vector.
## float2 lerp3 ( float2 a , float2 b , float2 c , float coef )


Performs linear interpolation between three vectors.


**Equivalent**


```glsl
if (a < 0.5)
{
	lerp(v0, v1, a * 2.0f);
}
else
{
	lerp(v1, v2, a * 2.0f - 1.0f);
	}

```


### Arguments

- *float2* **a** - First vector.
- *float2* **b** - Second vector.
- *float2* **c** - Third vector.
- *float* **coef** - Interpolation coefficient in the range [0.0f, 1.0f].

### Return value

Interpolated vector.
## float lerp3 ( float a , float b , float c , float coef )


Performs linear interpolation between three values.


**Equivalent**


```glsl
if (a < 0.5)
{
	lerp(v0, v1, a * 2.0f);
}
else
{
	lerp(v1, v2, a * 2.0f - 1.0f);
	}

```


### Arguments

- *float* **a** - First value.
- *float* **b** - Second value.
- *float* **c** - Third value.
- *float* **coef** - Interpolation coefficient in the range [0.0f, 1.0f].

### Return value

Interpolated value.
## float4 overlay ( float4 a , float4 b , float coef )


Performs overlay A over B with blending coefficient.


**Equivalent**


```glsl
saturate(A * lerp(float4_one * 0.5f,B,BLEND) * 2);
```


### Arguments

- *float4* **a** - First vector.
- *float4* **b** - Second vector.
- *float* **coef** - Blending coefficient.

### Return value

Resulting vector.
## float4 overlay ( float4 a , float4 b , float4 coef )


Performs overlay A over B with blending coefficient.


**Equivalent**


```glsl
saturate(A * lerp(float4_one * 0.5f,B,BLEND) * 2);
```


### Arguments

- *float4* **a** - First vector.
- *float4* **b** - Second vector.
- *float4* **coef** - Blending coefficient.

### Return value

Resulting vector.
## float3 overlay ( float3 a , float3 b , float coef )


Performs overlay A over B with blending coefficient.


**Equivalent**


```glsl
saturate(A * lerp(float4_one * 0.5f,B,BLEND) * 2);
```


### Arguments

- *float3* **a** - First vector.
- *float3* **b** - Second vector.
- *float* **coef** - Blending coefficient.

### Return value

Resulting vector.
## float3 overlay ( float3 a , float3 b , float3 coef )


Performs overlay A over B with blending coefficient.


**Equivalent**


```glsl
saturate(A * lerp(float4_one * 0.5f,B,BLEND) * 2);
```


### Arguments

- *float3* **a** - First vector.
- *float3* **b** - Second vector.
- *float3* **coef** - Blending coefficient.

### Return value

Resulting vector.
## float2 overlay ( float2 a , float2 b , float coef )


Performs overlay A over B with blending coefficient.


**Equivalent**


```glsl
saturate(A * lerp(float4_one * 0.5f,B,BLEND) * 2);
```


### Arguments

- *float2* **a** - First vector.
- *float2* **b** - Second vector.
- *float* **coef** - Blending coefficient.

### Return value

Resulting vector.
## float2 overlay ( float2 a , float2 b , float2 coef )


Performs overlay A over B with blending coefficient.


**Equivalent**


```glsl
saturate(A * lerp(float4_one * 0.5f,B,BLEND) * 2);
```


### Arguments

- *float2* **a** - First vector.
- *float2* **b** - Second vector.
- *float2* **coef** - Blending coefficient.

### Return value

Resulting vector.
## float overlay ( float a , float b , float coef )


Performs overlay A over B with blending coefficient.


**Equivalent**


```glsl
saturate(A * lerp(float4_one * 0.5f,B,BLEND) * 2);
```


### Arguments

- *float* **a**
- *float* **b**
- *float* **coef** - Blending coefficient.

### Return value

Resulting value.
## float invLerp ( float a , float b , float value )

Returns the value calculated according to the following formula: **(value - a) / (b - a)** clamped within the range of [0.0,1.0].
### Arguments

- *float* **a** - First value (lower limit of the interpolation range).
- *float* **b** - Second value (upper limit of the interpolation range).
- *float* **value** - Value.

### Return value

Resulting value.
## float2 invLerp ( float2 a , float2 b , float2 value )

Returns the vector with values calculated according to the following formula: **(value - a) / (b - a)** clamped within the range of [0.0,1.0].
### Arguments

- *float2* **a** - Vector containing the first value (lower limit of the interpolation range).
- *float2* **b** - Vector containing the second value (upper limit of the interpolation range).
- *float2* **value** - Vector containing values.

### Return value

Vector containing resulting values.
## float3 invLerp ( float3 a , float3 b , float3 value )

Returns the vector with values calculated according to the following formula: **(value - a) / (b - a)** clamped within the range of [0.0,1.0].
### Arguments

- *float3* **a** - Vector containing the first value (lower limit of the interpolation range).
- *float3* **b** - Vector containing the second value (upper limit of the interpolation range).
- *float3* **value** - Vector containing values.

### Return value

Vector containing resulting values.
## float4 invLerp ( float4 a , float4 b , float4 value )

Returns the vector with values calculated according to the following formula: **(value - a) / (b - a)** clamped within the range of [0.0,1.0].
### Arguments

- *float4* **a** - Vector containing the first value (lower limit of the interpolation range).
- *float4* **b** - Vector containing the second value (upper limit of the interpolation range).
- *float4* **value** - Vector containing values.

### Return value

Vector containing resulting values.
## float sum ( float4 value )

Returns the sum of vector components.
### Arguments

- *float4* **value** - Vector.

### Return value

Sum of the argument vector components.
## float sum ( float3 value )

Returns the sum of vector components.
### Arguments

- *float3* **value** - Vector.

### Return value

Sum of the argument vector components.
## float sum ( float2 value )

Returns the sum of vector components.
### Arguments

- *float2* **value** - Vector.

### Return value

Sum of the argument vector components.
## int sum ( int4 value )

Returns the sum of vector components.
### Arguments

- *int4* **value** - Vector.

### Return value

Sum of the argument vector components.
## int sum ( int3 value )

Returns the sum of vector components.
### Arguments

- *int3* **value** - Vector.

### Return value

Sum of the argument vector components.
## int sum ( int2 value )

Returns the sum of vector components.
### Arguments

- *int2* **value** - Vector.

### Return value

Sum of the argument vector components.
## uint sum ( uint4 value )

Returns the sum of vector components.
### Arguments

- *uint4* **value** - Vector.

### Return value

Sum of the argument vector components.
## uint sum ( uint3 value )

Returns the sum of vector components.
### Arguments

- *uint3* **value** - Vector.

### Return value

Sum of the argument vector components.
## uint sum ( uint2 value )

Returns the sum of vector components.
### Arguments

- *uint2* **value** - Vector.

### Return value

Sum of the argument vector components.
## float pow2 ( float value )

Returns the argument raised to the power of 2 (squared).
### Arguments

- *float* **value** - Value.

### Return value

Argument raised to the power of 2.
## float2 pow2 ( float2 value )

Returns the argument raised to the power of 2 (squared).
### Arguments

- *float2* **value** - Vector containing values.

### Return value

Argument values raised to the power of 2.
## float3 pow2 ( float3 value )

Returns the argument raised to the power of 2 (squared).
### Arguments

- *float3* **value** - Vector containing values.

### Return value

Argument values raised to the power of 2.
## float4 pow2 ( float4 value )

Returns the argument raised to the power of 2 (squared).
### Arguments

- *float4* **value** - Vector containing values.

### Return value

Argument values raised to the power of 2.
## float pow3 ( float value )

Returns the argument raised to the power of 3 (cube).
### Arguments

- *float* **value** - Value.

### Return value

Argument raised to the power of 3.
## float2 pow3 ( float2 value )

Returns the argument raised to the power of 3 (cube).
### Arguments

- *float2* **value** - Vector containing values.

### Return value

Argument values raised to the power of 3.
## float3 pow3 ( float3 value )

Returns the argument raised to the power of 3 (cube).
### Arguments

- *float3* **value** - Vector containing values.

### Return value

Argument values raised to the power of 3.
## float4 pow3 ( float4 value )

Returns the argument raised to the power of 3 (cube).
### Arguments

- *float4* **value** - Vector containing values.

### Return value

Argument values raised to the power of 3.
## float pow4 ( float value )

Returns the argument raised to the power of 4.
### Arguments

- *float* **value** - Value.

### Return value

Argument raised to the power of 4.
## float2 pow4 ( float2 value )

Returns the argument raised to the power of 4.
### Arguments

- *float2* **value** - Vector containing values.

### Return value

Argument values raised to the power of 4.
## float3 pow4 ( float3 value )

Returns the argument raised to the power of 4.
### Arguments

- *float3* **value** - Vector containing values.

### Return value

Argument values raised to the power of 4.
## float4 pow4 ( float4 value )

Returns the argument raised to the power of 4.
### Arguments

- *float4* **value** - Vector containing values.

### Return value

Argument values raised to the power of 4.
## float powMirror ( float value , float power )


Perform the following operation:


**Implementation**


```glsl
1.0f - pow(1.0f - value,power);
```


### Arguments

- *float* **value** - Argument value.
- *float* **power** - Power.

### Return value

Mirrored powered value.
## float2 powMirror ( float2 value , float2 power )


Perform the following operation:


**Implementation**


```glsl
1.0f - pow(1.0f - value,power);
```


### Arguments

- *float2* **value** - Vector containing argument values.
- *float2* **power** - Vector containing power values.

### Return value

Vector containing mirrored powered values.
## float3 powMirror ( float3 value , float3 power )


Perform the following operation:


**Implementation**


```glsl
1.0f - pow(1.0f - value,power);
```


### Arguments

- *float3* **value** - Vector containing argument values.
- *float3* **power** - Vector containing power values.

### Return value

Vector containing mirrored powered values.
## float4 powMirror ( float4 value , float4 power )


Perform the following operation:


**Implementation**


```glsl
1.0f - pow(1.0f - value,power);
```


### Arguments

- *float4* **value** - Vector containing argument values.
- *float4* **power** - Vector containing power values.

### Return value

Vector containing mirrored powered values.
## float powFast ( float a , float b )

 Returns the argument raised to the specified power (**ab**). Doesn't perform the check that the first argument is a negative value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **a** - Argument.
- *float* **b** - Power.

### Return value

Argument raised to the specified power (**ab**).
## float2 powFast ( float2 a , float2 b )

 Returns the argument raised to the specified power (**ab**). Doesn't perform the check that the first argument is a negative value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **a** - Argument.
- *float2* **b** - Power.

### Return value

Argument raised to the specified power (**ab**).
## float3 powFast ( float3 a , float3 b )

 Returns the argument raised to the specified power (**ab**). Doesn't perform the check that the first argument is a negative value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **a** - Argument.
- *float3* **b** - Power.

### Return value

Argument raised to the specified power (**ab**).
## float4 powFast ( float4 a , float4 b )

 Returns the argument raised to the specified power (**ab**). Doesn't perform the check that the first argument is a negative value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **a** - Argument.
- *float4* **b** - Power.

### Return value

Argument raised to the specified power (**ab**).
## int powFast ( int a , int b )

 Returns the argument raised to the specified power (**ab**). Doesn't perform the check that the first argument is a negative value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **a** - Argument.
- *int* **b** - Power.

### Return value

Argument raised to the specified power (**ab**).
## int2 powFast ( int2 a , int2 b )

 Returns the argument raised to the specified power (**ab**). Doesn't perform the check that the first argument is a negative value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **a** - Argument.
- *int2* **b** - Power.

### Return value

Argument raised to the specified power (**ab**).
## int3 powFast ( int3 a , int3 b )

 Returns the argument raised to the specified power (**ab**). Doesn't perform the check that the first argument is a negative value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **a** - Argument.
- *int3* **b** - Power.

### Return value

Argument raised to the specified power (**ab**).
## int4 powFast ( int4 a , int4 b )

 Returns the argument raised to the specified power (**ab**). Doesn't perform the check that the first argument is a negative value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **a** - Argument.
- *int4* **b** - Power.

### Return value

Argument raised to the specified power (**ab**).
## float srgb ( float color )

Converts RGB color from the linear space to gamma space.
### Arguments

- *float* **color** - Color value.

### Return value

Color converted from the linear space to gamma space.
## float2 srgb ( float2 color )

Converts RGB color from the linear space to gamma space.
### Arguments

- *float2* **color** - Color value.

### Return value

Color converted from the linear space to gamma space.
## float3 srgb ( float3 color )

Converts RGB color from the linear space to gamma space.
### Arguments

- *float3* **color** - Color value.

### Return value

Color converted from the linear space to gamma space.
## float4 srgb ( float4 color )

Converts RGB color from the linear space to gamma space.
### Arguments

- *float4* **color** - Color value.

### Return value

Color converted from the linear space to gamma space.
## float srgbInv ( float color )

Converts color from the gamma space to linear space.
### Arguments

- *float* **color** - Value to be converted.

### Return value

Value converted from the gamma space to linear space.
## float2 srgbInv ( float2 color )

Converts color from the gamma space to linear space.
### Arguments

- *float2* **color** - Vector containing values to be converted.

### Return value

Vector containing inverted sRGB values.
## float3 srgbInv ( float3 color )

Converts color from the gamma space to linear space.
### Arguments

- *float3* **color** - Vector containing values to be converted.

### Return value

Vector containing inverted sRGB values.
## float4 srgbInv ( float4 color )


Converts color from the gamma space to linear space.


**Implementation:**


```glsl
pow(value,float_isrgb);
```


### Arguments

- *float4* **color** - Vector containing values to be converted.

### Return value

Vector containing inverted sRGB values.
## float lerpSRGB ( float a , float b , float coef )

Returns a linearly interpolated value the following way: transforms the values A and B in gamma space to the linear space, obtains the linearly interpolated value using the coefficient, and transforms the interpolated value back to the gamma space.
### Arguments

- *float* **a** - Value in the gamma space.
- *float* **b** - Value in the gamma space.
- *float* **coef** - Interpolation coefficient

### Return value

Linearly interpolated value.
## float2 lerpSRGB ( float2 a , float2 b , float coef )

Returns a linearly interpolated value the following way: transforms the values A and B in gamma space to the linear space, obtains the linearly interpolated value using the coefficient, and transforms the interpolated value back to the gamma space.
### Arguments

- *float2* **a** - Value in the gamma space.
- *float2* **b** - Value in the gamma space.
- *float* **coef** - Interpolation coefficient

### Return value

Linearly interpolated value.
## float3 lerpSRGB ( float3 a , float3 b , float coef )

Returns a linearly interpolated value the following way: transforms the values A and B in gamma space to the linear space, obtains the linearly interpolated value using the coefficient, and transforms the interpolated value back to the gamma space.
### Arguments

- *float3* **a** - Value in the gamma space.
- *float3* **b** - Value in the gamma space.
- *float* **coef** - Interpolation coefficient

### Return value

Linearly interpolated value.
## float4 lerpSRGB ( float4 a , float4 b , float coef )

Returns a linearly interpolated value the following way: transforms the values A and B in gamma space to the linear space, obtains the linearly interpolated value using the coefficient, and transforms the interpolated value back to the gamma space.
### Arguments

- *float4* **a** - Value in the gamma space.
- *float4* **b** - Value in the gamma space.
- *float* **coef** - Interpolation coefficient

### Return value

Linearly interpolated value.
## float rerange ( float in_ , float in_range_min , float in_range_max , float out_range_min , float out_range_max )

Returns the value that corresponds to the input value remapped within the limits of the output range.
### Arguments

- *float* **in_** - Input value.
- *float* **in_range_min** - Minimum value of the input range.
- *float* **in_range_max** - Maximum value of the input range.
- *float* **out_range_min** - Minimum value of the output range.
- *float* **out_range_max** - Maximum value of the output range.

### Return value

Output value that corresponds to the input value remapped in the output range.
## float2 rerange ( float2 in_ , float in_range_min , float in_range_max , float out_range_min , float out_range_max )

Returns the vector containing the values that correspond to the input values remapped within the limits of the output range.
### Arguments

- *float2* **in_** - Vector containing input values.
- *float* **in_range_min** - Minimum value of the input range.
- *float* **in_range_max** - Maximum value of the input range.
- *float* **out_range_min** - Minimum value of the output range.
- *float* **out_range_max** - Maximum value of the output range.

### Return value

Vector containing the output values that correspond to the input values remapped in the output range.
## float3 rerange ( float3 in_ , float in_range_min , float in_range_max , float out_range_min , float out_range_max )

Returns the vector containing the values that correspond to the input values remapped within the limits of the output range.
### Arguments

- *float3* **in_** - Vector containing input values.
- *float* **in_range_min** - Minimum value of the input range.
- *float* **in_range_max** - Maximum value of the input range.
- *float* **out_range_min** - Minimum value of the output range.
- *float* **out_range_max** - Maximum value of the output range.

### Return value

Vector containing the output values that correspond to the input values remapped in the output range.
## float4 rerange ( float4 in_ , float in_range_min , float in_range_max , float out_range_min , float out_range_max )

Returns the vector containing the values that correspond to the input values remapped within the limits of the output range.
### Arguments

- *float4* **in_** - Vector containing input values.
- *float* **in_range_min** - Minimum value of the input range.
- *float* **in_range_max** - Maximum value of the input range.
- *float* **out_range_min** - Minimum value of the output range.
- *float* **out_range_max** - Maximum value of the output range.

### Return value

Vector containing the output values that correspond to the input values remapped in the output range.
## bool checkRange ( float value , float range_min , float range_max )

Checks if the input value is within the specified range.
### Arguments

- *float* **value** - Input value.
- *float* **range_min** - Minimum value of the range.
- *float* **range_max** - Maximum value of the range.

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
## float hasBit ( uint value , uint bit )

Returns the value of the specified bit.
### Arguments

- *uint* **value** - Source value.
- *uint* **bit** - The bit of source value to be checked.

### Return value

Value of the checked bit � either 1.0f, or 0.0f.
## float4 hasBit ( uint4 value , uint bit )

Returns the value of the specified bit.
### Arguments

- *uint4* **value** - Vector of source values.
- *uint* **bit** - The bit of source value to be checked.

### Return value

Values of the checked bits � either 1.0f, or 0.0f.
## float4 hasBit ( uint value , uint4 bit )

Returns the value of the specified bit.
### Arguments

- *uint* **value** - Source value.
- *uint4* **bit** - The vector of bits to be checked in the source value.

### Return value

Values of the checked bits � either 1.0f, or 0.0f.
## float ddxy ( float value )

Returns the sum of absolute values of the source value derivatives with respect to the screen-space X coordinate and screen-space Y coordinate respectively. This method can only be used in the pixel shader stage.
### Arguments

- *float* **value** - Source value.

### Return value

Output value.
## float2 ddxy ( float2 value )

Returns the sum of absolute values of the source value derivatives with respect to the screen-space X coordinate and screen-space Y coordinate respectively. This method can only be used in the pixel shader stage.
### Arguments

- *float2* **value** - Source value.

### Return value

Output value.
## float3 ddxy ( float3 value )

Returns the sum of absolute values of the source value derivatives with respect to the screen-space X coordinate and screen-space Y coordinate respectively. This method can only be used in the pixel shader stage.
### Arguments

- *float3* **value** - Source value.

### Return value

Output value.
## float4 ddxy ( float4 value )

Returns the sum of absolute values of the source value derivatives with respect to the screen-space X coordinate and screen-space Y coordinate respectively. This method can only be used in the pixel shader stage.
### Arguments

- *float4* **value** - Source value.

### Return value

Output value.
## void specularToMetalness ( float3 diffuse_color , float3 specular_color , float gloss , float3 albedo , float metalness , float roughness , float specular )

Performs conversion of material features from the legacy specular workflow to PBR.
### Arguments

- *float3* **diffuse_color** - Diffuse color of the specular workflow.
- *float3* **specular_color** - Specular color of the specular workflow.
- *float* **gloss** - Gloss value of the specular workflow.
- *float3* **albedo** - Albedo color of the PBR workflow.
- *float* **metalness** - Metalness value of the PBR workflow.
- *float* **roughness** - Roughness value of the PBR workflow.
- *float* **specular** - Specular value of the PBR workflow.


## float3 nativeDepthToPositionVS ( float native_depth , float2 screen_uv , float4x4 iprojection )

Returns the pixel position from the native depth texture in the view space.
### Arguments

- *float* **native_depth** - Sample of the depth texture.
- *float2* **screen_uv** - Pixel position on the screen.
- *float4x4* **iprojection** - Inverse projection matrix used to capture the depth texture.

### Return value

Pixel position from the depth texture in the view space.
## float3 nativeDepthToPositionVS ( float native_depth , float2 screen_uv )

Returns the pixel position from the native depth texture in the view space.
### Arguments

- *float* **native_depth** - Sample of the depth texture.
- *float2* **screen_uv** - Pixel position on the screen.

### Return value

Pixel position from the depth texture in the view space.
## float3 nativeDepthToPositionVS ( Texture2D TEX_NATIVE_DEPTH , float2 screen_uv , float4x4 iprojection )

Returns the pixel position from the native depth texture in the view space.
### Arguments

- *Texture2D* **TEX_NATIVE_DEPTH** - Depth texture.
- *float2* **screen_uv** - Pixel position on the screen.
- *float4x4* **iprojection** - Inverse projection matrix used to capture the depth texture.

### Return value

Pixel position from the depth texture in the view space.
## float3 nativeDepthToPositionVS ( Texture2D TEX_NATIVE_DEPTH , float2 screen_uv )

Returns the pixel position from the native depth texture in the view space.
### Arguments

- *Texture2D* **TEX_NATIVE_DEPTH** - Depth texture.
- *float2* **screen_uv** - Pixel position on the screen.

### Return value

Pixel position from the depth texture in the view space.
## float nativeDepthToLinearDepth ( float native_depth , float2 screen_uv )

Returns the linearized depth value in the view space.
### Arguments

- *float* **native_depth** - Sample of the depth texture.
- *float2* **screen_uv** - Pixel position on the screen.

### Return value

Linearized depth value in the view space.
## float nativeDepthToLinearDepth ( Texture2D TEX_NATIVE_DEPTH , float2 screen_uv )

Returns the linearized depth value in the view space.
### Arguments

- *Texture2D* **TEX_NATIVE_DEPTH** - Depth texture.
- *float2* **screen_uv** - Pixel position on the screen.

### Return value

Linearized depth value in the view space.
## float3 positionToViewDirection ( float3 position_vs )

Returns view direction from the position in the view space.
### Arguments

- *float3* **position_vs** - View space position.

### Return value

View direction from the position in the view space.
## float3 positionToViewDirection ( float3 position_vs , float depth )

Returns view direction from the position in the view space.
### Arguments

- *float3* **position_vs** - View space position.
- *float* **depth** - Depth value used for position normalization.

### Return value

View direction from the position in the view space.
## float3 screenUVToViewDirection ( float2 screen_uv )

Returns the view direction vector (unnormalized) in the view space based on the Screen UV.
### Arguments

- *float2* **screen_uv** - Screen UV coordinates.

### Return value

View direction vector in the view space (unnormalized).
## float3 screenUVToViewDirection ( float3 screen_uv )

Returns the view direction vector (unnormalized) in the view space based on the Screen UV.
### Arguments

- *float3* **screen_uv** - Screen UV coordinates.

### Return value

View direction vector in the view space (unnormalized).
## float3 screenUVToViewDirection ( float4 screen_uv )

Returns the view direction vector (unnormalized) in the view space based on the Screen UV.
### Arguments

- *float4* **screen_uv** - Screen UV coordinates.

### Return value

View direction vector in the view space (unnormalized).
## float2 positionToScreenUV ( float3 position_vs )

Returns Screen UV based on the coordinates of the position in the view space.
### Arguments

- *float3* **position_vs** - Position in the view space.

### Return value

Screen UV.
## float2 positionToScreenUV ( float4 position_vs )

Returns Screen UV based on the coordinates of the position in the view space.
### Arguments

- *float4* **position_vs** - Position in the view space.

### Return value

Screen UV.
## float degreesToRadians ( float degrees )

Returns the angle value provided in degrees as converted to radians.
### Arguments

- *float* **degrees** - Angle in degrees.

### Return value

Angle in radians.
## float2 degreesToRadians ( float2 degrees )

Returns the angle value provided in degrees as converted to radians.
### Arguments

- *float2* **degrees** - Angle in degrees.

### Return value

Angle in radians.
## float3 degreesToRadians ( float3 degrees )

Returns the angle value provided in degrees as converted to radians.
### Arguments

- *float3* **degrees** - Angle in degrees.

### Return value

Angle in radians.
## float4 degreesToRadians ( float4 degrees )

Returns the angle value provided in degrees as converted to radians.
### Arguments

- *float4* **degrees** - Angle in degrees.

### Return value

Angle in radians.
## float radiansToDegrees ( float radians )

Returns the angle value provided in radians as converted to degrees.
### Arguments

- *float* **radians** - Angle in radians.

### Return value

Angle in degrees.
## float2 radiansToDegrees ( float2 radians )

Returns the angle value provided in radians as converted to degrees.
### Arguments

- *float2* **radians** - Angle in radians.

### Return value

Angle in degrees.
## float3 radiansToDegrees ( float3 radians )

Returns the angle value provided in radians as converted to degrees.
### Arguments

- *float3* **radians** - Angle in radians.

### Return value

Angle in degrees.
## float4 radiansToDegrees ( float4 radians )

Returns the angle value provided in radians as converted to degrees.
### Arguments

- *float4* **radians** - Angle in radians.

### Return value

Angle in degrees.
## float3 reorientNormalBlend ( float3 base_normal , float3 detail_normal )

Performs blending of tangent-space normals and returns the reoriented normal vector.
### Arguments

- *float3* **base_normal** - Base normal.
- *float3* **detail_normal** - Detail normal.

### Return value

Reoriented normal vector.
## float3 reorientVectorBlend ( float3 main_vec , float3 vec , float3 rotation_vec )

Performs blending of vectors and outputs the reoriented vector.
### Arguments

- *float3* **main_vec** - Main vector.
- *float3* **vec** - Vector.
- *float3* **rotation_vec** - Rotation vector.

### Return value

Reoriented vector.
## float normalReconstructZ ( float2 normal )


Returns a reconstructed vector Z-coordinate using the input X and Y coordinates, which are within the [-1, 1] range, i.e., the resulting vector has a unit length.


This method can be used to calculate the direction vector along a hemisphere: you input X and Y and the output is Z.


For example, if you input Vertex Position as X and Y coordinates in the Absolute World space, and input the resulting Z as the vertex Z position into the Material node, you'll get a hemisphere form.


### Arguments

- *float2* **normal** - X and Y coordinates of the vector, which are within the [-1, 1] range.

### Return value

Reconstructed Z-coordinate of the vector.
## float normalReconstructZ ( float3 normal )


Returns a reconstructed vector Z-coordinate using the input X and Y coordinates, which are within the [-1, 1] range, i.e., the resulting vector has a unit length.


This method can be used to calculate the direction vector along a hemisphere: you input X and Y and the output is Z.


For example, if you input Vertex Position as X and Y coordinates in the Absolute World space, and input the resulting Z as the vertex Z position into the Material node, you'll get a hemisphere form.


### Arguments

- *float3* **normal** - Vector containing the X and Y coordinates of the vector, which are within the [-1, 1] range.

### Return value

Reconstructed Z-coordinate of the vector.
## float normalReconstructZ ( float4 normal )


Returns a reconstructed vector Z-coordinate using the input X and Y coordinates, which are within the [-1, 1] range, i.e., the resulting vector has a unit length.


This method can be used to calculate the direction vector along a hemisphere: you input X and Y and the output is Z.


For example, if you input Vertex Position as X and Y coordinates in the Absolute World space, and input the resulting Z as the vertex Z position into the Material node, you'll get a hemisphere form.


### Arguments

- *float4* **normal** - Vector containing the X and Y coordinates of the vector, which are within the [-1, 1] range.

### Return value

Reconstructed Z-coordinate of the vector.
## float3 positionToNormal ( float3 position )

Returns the normal by using the fragment position.
### Arguments

- *float3* **position** - Fragment position.

### Return value

Normal.
## float3 positionToNormal ( float4 position )

Returns the normal by using the fragment position.
### Arguments

- *float4* **position** - Fragment position.

### Return value

Normal.
## float calcMipLevel ( float2 coord )

Returns the mipmap level for the specified pixel position.
### Arguments

- *float2* **coord** - Pixel position.

### Return value

Mipmap level.
## void calculateTBN ( float3 T , float3 B , float3 N , float3 position , float2 uv )

Calculates the Tangent, Binormal, and Normal vectors based on the Normal vector, Position vector, and UV.
### Arguments

- *float3* **T** - Tangent.
- *float3* **B** - Binormal.
- *float3* **N** - Normal vector.
- *float3* **position** - Position vector.
- *float2* **uv** - Texture coordinates.


## bool toBool ( float v )

 Converts the argument's value to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( float2 v )

 Converts the argument's first component to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( float3 v )

 Converts the argument's first component to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( float4 v )

 Converts the argument's first component to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( bool v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v**


## bool toBool ( int v )

 Converts the argument's value to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( int2 v )

 Converts the argument's first component to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( int3 v )

 Converts the argument's first component to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( int4 v )

 Converts the argument's first component to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( uint v )

 Converts the argument's value to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( uint2 v )

 Converts the argument's first component to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( uint3 v )

 Converts the argument's first component to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## bool toBool ( uint4 v )

 Converts the argument's first component to a *boolean* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( float v )

 Converts the argument's value to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( float2 v )

 Converts the argument's first component to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( float3 v )

 Converts the argument's first component to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( float4 v )

 Converts the argument's first component to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( bool v )

 Converts the argument's value to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( int v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v**


## int toInt ( int2 v )

 Converts the argument's first component to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( int3 v )

 Converts the argument's first component to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( int4 v )

 Converts the argument's first component to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( uint v )

 Converts the argument's value to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( uint2 v )

 Converts the argument's first component to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( uint3 v )

 Converts the argument's first component to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## int toInt ( uint4 v )

 Converts the argument's first component to an *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( float v )

 Converts the argument to a two-component vector of *integer* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( float2 v )

 Converts the argument to the vector of *integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( float3 v )

 Converts the argument to a two-component vector of *integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( float4 v )

 Converts the argument to a two-component vector of *integer* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( bool v )

 Converts the argument to a two-component vector of *integer* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( int v )

 Converts the argument to a two-component vector of *integer* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( int2 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v**


## int2 toInt2 ( int3 v )

 Converts the argument to a two-component vector of *integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( int4 v )

 Converts the argument to a two-component vector of *integer* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( uint v )

 Converts the argument to a two-component vector of *integer* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( uint2 v )

 Converts the argument to the vector of *integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( uint3 v )

 Converts the argument to a two-component vector of *integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## int2 toInt2 ( uint4 v )

 Converts the argument to a two-component vector of *integer* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( float v )

 Converts the argument to a three-component vector of *integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( float2 v )

 Converts the argument to a three-component vector of *integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( float3 v )

 Converts the argument to a vector of *integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( float4 v )

 Converts the argument to a three-component vector of *integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( bool v )

 Converts the argument to a three-component vector of *integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( int v )

 Converts the argument to a three-component vector of *integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( int2 v )

 Converts the argument to a three-component vector of *integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( int3 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v**


## int3 toInt3 ( int4 v )

 Converts the argument to a three-component vector of *integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( uint v )

 Converts the argument to a three-component vector of *integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( uint2 v )

 Converts the argument to a three-component vector of *integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( uint3 v )

 Converts the argument to a vector of *integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## int3 toInt3 ( uint4 v )

 Converts the argument to a three-component vector of *integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( float v )

 Converts the argument to a four-component vector of *integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( float2 v )

 Converts the argument to a four-component vector of *integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( float3 v )

 Converts the argument to a four-component vector of *integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( float4 v )

 Converts the argument to a vector of *integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( bool v )

 Converts the argument to a four-component vector of *integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( int v )

 Converts the argument to a four-component vector of *integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( int2 v )

 Converts the argument to a four-component vector of *integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( int3 v )

 Converts the argument to a four-component vector of *integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( int4 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v**


## int4 toInt4 ( uint v )

 Converts the argument to a four-component vector of *integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( uint2 v )

 Converts the argument to a four-component vector of *integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( uint3 v )

 Converts the argument to a four-component vector of *integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## int4 toInt4 ( uint4 v )

 Converts the argument to a vector of *integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( float v )

 Converts the argument's value to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( float2 v )

 Converts the argument's first component to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( float3 v )

 Converts the argument's first component to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( float4 v )

 Converts the argument's first component to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( bool v )

 Converts the argument's value to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( int v )

 Converts the argument's value to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( int2 v )

 Converts the argument's first component to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( int3 v )

 Converts the argument's first component to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( int4 v )

 Converts the argument's first component to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( uint v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v**


## uint toUInt ( uint2 v )

 Converts the argument's first component to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( uint3 v )

 Converts the argument's first component to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## uint toUInt ( uint4 v )

 Converts the argument's first component to an *unsigned integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( float v )

 Converts the argument to a two-component vector of *unsigned integer* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( float2 v )

 Converts the argument to the vector of *unsigned integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( float3 v )

 Converts the argument to a two-component vector of *unsigned integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( float4 v )

 Converts the argument to a two-component vector of *unsigned integer* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( bool v )

 Converts the argument to a two-component vector of *unsigned integer* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( int v )

 Converts the argument to a two-component vector of *unsigned integer* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( int2 v )

 Converts the argument to the vector of *unsigned integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( int3 v )

 Converts the argument to a two-component vector of *unsigned integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( int4 v )

 Converts the argument to a two-component vector of *unsigned integer* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( uint v )

 Converts the argument to a two-component vector of *unsigned integer* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( uint2 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v**


## uint2 toUInt2 ( uint3 v )

 Converts the argument to a two-component vector of *unsigned integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## uint2 toUInt2 ( uint4 v )

 Converts the argument to a two-component vector of *unsigned integer* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( float v )

 Converts the argument to a three-component vector of *unsigned integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( float2 v )

 Converts the argument to a three-component vector of *unsigned integer* values, using the argument values as the corresponding components, and filling the extra one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( float3 v )

 Converts the argument to a vector of *unsigned integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( float4 v )

 Converts the argument to a three-component vector of *unsigned integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( bool v )

 Converts the argument to a three-component vector of *unsigned integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( int v )

 Converts the argument to a three-component vector of *unsigned integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( int2 v )

 Converts the argument to a three-component vector of *unsigned integer* values, using the argument values as the corresponding components, and filling the extra one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( int3 v )

 Converts the argument to a vector of *unsigned integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( int4 v )

 Converts the argument to a three-component vector of *unsigned integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( uint v )

 Converts the argument to a three-component vector of *unsigned integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( uint2 v )

 Converts the argument to a three-component vector of *unsigned integer* values, using the argument values as the corresponding components, and filling the extra one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## uint3 toUInt3 ( uint3 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v**


## uint3 toUInt3 ( uint4 v )

 Converts the argument to a three-component vector of *unsigned integer* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( float v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( float2 v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( float3 v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument values as the corresponding components, and filling the extra one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( float4 v )

 Converts the argument to a vector of *unsigned integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( bool v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( int v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( int2 v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( int3 v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument values as the corresponding components, and filling the extra one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( int4 v )

 Converts the argument to a vector of *unsigned integer* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( uint v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( uint2 v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( uint3 v )

 Converts the argument to a four-component vector of *unsigned integer* values, using the argument values as the corresponding components, and filling the extra one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## uint4 toUInt4 ( uint4 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v**


## float toFloat ( float v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v**


## float toFloat ( float2 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( float3 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( float4 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( bool v )

 Converts the argument's value to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( int v )

 Converts the argument's value to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( int2 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( int3 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( int4 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( uint v )

 Converts the argument's value to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( uint2 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( uint3 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( uint4 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( double v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double* **v** - Value to be converted.

### Return value

Resulting value.
## float toFloat ( double2 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double2* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( double3 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double3* **v** - Value to be converted.

### Return value

Converted value.
## float toFloat ( double4 v )

 Converts the argument's first component to a *floating-point* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double4* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( float v )

 Converts the argument to a two-component vector of *floating-point* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( float2 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v**


## float2 toFloat2 ( float3 v )

 Converts the argument to a two-component vector of *floating-point* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( float4 v )

 Converts the argument to a two-component vector of *floating-point* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( bool v )

 Converts the argument to a two-component vector of *floating-point* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( int v )

 Converts the argument to a two-component vector of *floating-point* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( int2 v )

 Converts the argument to the vector of *floating-point* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( int3 v )

 Converts the argument to a two-component vector of *floating-point* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( int4 v )

 Converts the argument to a two-component vector of *floating-point* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( uint v )

 Converts the argument to a two-component vector of *floating-point* values, using the argument value as the first component, and filling the other one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( uint2 v )

 Converts the argument to the vector of *floating-point* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( uint3 v )

 Converts the argument to a two-component vector of *floating-point* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( uint4 v )

 Converts the argument to a two-component vector of *floating-point* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( double v )

 Converts the argument to a two-component vector of *floating-point* values, using the argument value for both components.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( double2 v )

 Converts the argument to the vector of *floating-point* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double2* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( double3 v )

 Converts the argument to a two-component vector of *floating-point* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double3* **v** - Value to be converted.

### Return value

Converted value.
## float2 toFloat2 ( double4 v )

 Converts the argument to a two-component vector of *floating-point* values, discarding the extra components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double4* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( float v )

 Converts the argument to a three-component vector of *floating-point* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( float2 v )

 Converts the argument to a three-component vector of *floating-point* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( float3 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v**


## float3 toFloat3 ( float4 v )

 Converts the argument to a three-component vector of *floating-point* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( bool v )

 Converts the argument to a three-component vector of *floating-point* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( int v )

 Converts the argument to a three-component vector of *floating-point* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( int2 v )

 Converts the argument to a three-component vector of *floating-point* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( int3 v )

 Converts the argument to a vector of *floating-point* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( int4 v )

 Converts the argument to a three-component vector of *floating-point* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( uint v )

 Converts the argument to a three-component vector of *floating-point* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( uint2 v )

 Converts the argument to a three-component vector of *floating-point* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( uint3 v )

 Converts the argument to a vector of *floating-point* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( uint4 v )

 Converts the argument to a three-component vector of *floating-point* values, discarding the extra component of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( double v )

 Converts the argument to a three-component vector of *floating-point* values, using the argument value for all components.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( double2 v )

 Converts the argument to a three-component vector of *floating-point* values, using the argument value for the first two components and filling the third one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double2* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( double3 v )

 Converts the argument to the vector of *floating-point* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double3* **v** - Value to be converted.

### Return value

Converted value.
## float3 toFloat3 ( double4 v )

 Converts the argument to the vector of *floating-point* values using the first three components of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double4* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( float v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( float2 v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( float3 v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument values as the corresponding components, and filling the extra one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( float4 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v**


## float4 toFloat4 ( bool v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *bool* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( int v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( int2 v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( int3 v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument values as the corresponding components, and filling the extra one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( int4 v )

 Converts the argument to a vector of *floating-point* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( uint v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument value as the first component, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( uint2 v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument values as the corresponding components, and filling the extra ones with zeroes.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( uint3 v )

 Converts the argument to a four-component vector of *floating-point* values, using the argument values as the corresponding components, and filling the extra one with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Converted value.
## float4 toFloat4 ( uint4 v )

 Converts the argument to a vector of *floating-point* values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Converted value.
## float2x2 toFloat2x2 ( float3x3 v )

 Converts the 3x3 matrix to 2x2 matrix by removing the third column and row and returns the result.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **v** - 3x3 matrix.

### Return value

2x2 matrix.
## float2x2 toFloat2x2 ( float4x4 v )

 Converts the 4x4 matrix to 2x2 matrix by removing extra columns and rows and returns the result.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **v** - 4x4 matrix.

### Return value

2x2 matrix.
## float3x3 toFloat3x3 ( float2x2 v )


Converts the 2x2 matrix to 3x3 matrix by filling the additional row and column cells with 0 and the element on the main diagonal � with 1.


| v[0][0] | v[0][1] | 0.0f |
|---|---|---|
| v[1][0] | v[1][1] | 0.0f |
| 0.0f | 0.0f | 1.0f |


**This function is [API-dependent](#api_dependent).**


### Arguments

- *float2x2* **v** - 2x2 matrix.

### Return value

3x3 matrix.
## float3x3 toFloat3x3 ( float4x4 v )

 Converts the 4x4 matrix to 3x3 matrix by removing the fourth column and row and returns the result.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **v** - 4x4 matrix.

### Return value

3x3 matrix.
## float4x4 toFloat4x4 ( float2x2 v )


Converts the 2x2 matrix to 4x4 matrix by filling the additional row and column cells with 0 and the element on the main diagonal � with 1.


| v[0][0] | v[0][1] | 0.0f | 0.0f |
|---|---|---|---|
| v[1][0] | v[1][1] | 0.0f | 0.0f |
| 0.0f | 0.0f | 1.0f | 0.0f |
| 0.0f | 0.0f | 0.0f | 1.0f |


**This function is [API-dependent](#api_dependent).**


### Arguments

- *float2x2* **v** - 2x2 matrix.

### Return value

4x4 matrix.
## float4x4 toFloat4x4 ( float3x3 v )


Converts the 3x3 matrix to 4x4 matrix by filling the additional row and column cells with 0 and the element on the main diagonal � with 1.


| v[0][0] | v[0][1] | v[0][2] | 0.0f |
|---|---|---|---|
| v[1][0] | v[1][1] | v[1][2] | 0.0f |
| v[2][0] | v[2][1] | v[2][2] | 0.0f |
| 0.0f | 0.0f | 0.0f | 1.0f |


**This function is [API-dependent](#api_dependent).**


### Arguments

- *float3x3* **v** - 3x3 matrix.

### Return value

4x4 matrix.
## double3x3 toDouble3x3 ( double4x4 v )

 Converts the argument to the 3x3 matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double4x4* **v** - Value to be converted.

### Return value

Converted value.
## float4 toGVec4 ( float v )

 Converts the argument value to four-component vector of the same type filling all components with the argument values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **v** - Value to be converted.

### Return value

Four-component vector.
## float4 toGVec4 ( float2 v )

 Converts the argument value to four-component vector of the same type filling extra components with zeros.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float2* **v** - Value to be converted.

### Return value

Four-component vector.
## float4 toGVec4 ( float3 v )

 Converts the argument value to four-component vector of the same type filling the extra component with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3* **v** - Value to be converted.

### Return value

Four-component vector.
## float4 toGVec4 ( float4 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4* **v** - Value to be converted.

### Return value

Four-component vector.
## int4 toGVec4 ( int v )

 Converts the argument value to four-component vector of the same type filling all components with the argument values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int* **v** - Value to be converted.

### Return value

Four-component vector.
## int4 toGVec4 ( int2 v )

 Converts the argument value to four-component vector of the same type filling extra components with zeros.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int2* **v** - Value to be converted.

### Return value

Four-component vector.
## int4 toGVec4 ( int3 v )

 Converts the argument value to four-component vector of the same type filling the extra component with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int3* **v** - Value to be converted.

### Return value

Four-component vector.
## int4 toGVec4 ( int4 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *int4* **v** - Value to be converted.

### Return value

Four-component vector.
## uint4 toGVec4 ( uint v )

 Converts the argument value to four-component vector of the same type filling all components with the argument values.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - Value to be converted.

### Return value

Four-component vector.
## uint4 toGVec4 ( uint2 v )

 Converts the argument value to four-component vector of the same type filling extra components with zeros.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - Value to be converted.

### Return value

Four-component vector.
## uint4 toGVec4 ( uint3 v )

 Converts the argument value to four-component vector of the same type filling the extra component with zero.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - Value to be converted.

### Return value

Four-component vector.
## uint4 toGVec4 ( uint4 v )

 Returns the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - Value to be converted.

### Return value

Four-component vector.
## int uintToInt ( uint v )

 Converts the *unsigned integer* value to the *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint* **v** - The value to be converted.

### Return value

Converted value.
## int2 uintToInt ( uint2 v )

 Converts the *unsigned integer* value to the *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint2* **v** - The value to be converted.

### Return value

Converted value.
## int3 uintToInt ( uint3 v )

 Converts the *unsigned integer* value to the *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint3* **v** - The value to be converted.

### Return value

Converted value.
## int4 uintToInt ( uint4 v )

 Converts the *unsigned integer* value to the *integer* value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *uint4* **v** - The value to be converted.

### Return value

Converted value.
## float3x3 matrix3 ( float4x4 mat )

 Converts the 4x4 matrix to 3x3 matrix by removing extra column and row and returns the result.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

3x3 matrix.
## float4x4 matrix4 ( float3x3 mat )


Converts the 3x3 matrix to 4x4 matrix by filling the additional row and column cells with 0 and the element on the main diagonal � with 1.


| v[0][0] | v[0][1] | v[0][2] | 0.0f |
|---|---|---|---|
| v[1][0] | v[1][1] | v[1][2] | 0.0f |
| v[2][0] | v[2][1] | v[2][2] | 0.0f |
| 0.0f | 0.0f | 0.0f | 1.0f |


**This function is [API-dependent](#api_dependent).**


### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

4x4 matrix.
## Double Functions


These functions take one or more arguments that are double expressions and return a double value.


> **Notice:** It is not recommended to use these functions, unless there is no other option. Operations with doubles are significantly more time consuming (e.g. addition and multiplication operations are 8 times slower).


## double drsqrt ( double a )

 Returns the inverse square root of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double* **a** - Input value.

### Return value

Inverse square root of the argument.
## double ddot ( double2 a , double2 b )

 Returns the dot product of two vectors.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double2* **a** - First vector.
- *double2* **b** - Second vector.

### Return value

Resulting value.
## double ddot ( double3 a , double3 b )

 Returns the dot product of two vectors.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double3* **a** - First vector.
- *double3* **b** - Second vector.

### Return value

Resulting value.
## double ddot ( double4 a , double4 b )

 Returns the dot product of two vectors.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double4* **a** - First vector.
- *double4* **b** - Second vector.

### Return value

Resulting value.
## double dmad ( double a , double b , double c )

 Returns the result of a*b+c.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double* **a** - First value.
- *double* **b** - Second value.
- *double* **c** - Third value.

### Return value

Result of a*b+c.
## double dsign ( double a )

 Returns the value denoting the sign of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double* **a** - Argument value.

### Return value


Argument sign:


- 1 if the argument value is positive
- 0 if the argument value equals to zero
- -1 if the argument value is negative


## double dabs ( double a )

 Returns the absolute value of the specified argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double* **a** - Argument value.

### Return value

Return value.
## double dlerp ( double a , double b , double t )

 Returns the interpolated value according to the following formula: **a * (1.0 - t) + b * t**.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double* **a** - First value (lower limit of the interpolation range).
- *double* **b** - Second value (upper limit of the interpolation range).
- *double* **t** - Interpolation coefficient used to interpolate a value between a and b.

### Return value

Resulting value.
## double2 dlerp ( double2 a , double2 b , double2 t )

 Returns the interpolated value according to the following formula: **a * (1.0 - t) + b * t**.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double2* **a** - First value (lower limit of the interpolation range).
- *double2* **b** - Second value (upper limit of the interpolation range).
- *double2* **t** - Interpolation coefficient used to interpolate a value between a and b.

### Return value

Resulting value.
## double3 dlerp ( double3 a , double3 b , double3 t )

 Returns the interpolated value according to the following formula: **a * (1.0 - t) + b * t**.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double3* **a** - First value (lower limit of the interpolation range).
- *double3* **b** - Second value (upper limit of the interpolation range).
- *double3* **t** - Interpolation coefficient used to interpolate a value between a and b.

### Return value

Resulting value.
## double4 dlerp ( double4 a , double4 b , double4 t )

 Returns the interpolated value according to the following formula: **a * (1.0 - t) + b * t**.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double4* **a** - First value (lower limit of the interpolation range).
- *double4* **b** - Second value (upper limit of the interpolation range).
- *double4* **t** - Interpolation coefficient used to interpolate a value between a and b.

### Return value

Resulting value.
## double dfrac ( double value )

 Returns the fractional part of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double* **value** - Argument value.

### Return value

Resulting value.
## double2 dfrac ( double2 value )

 Returns the fractional part of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double2* **value** - Argument value.

### Return value

Resulting value.
## double3 dfrac ( double3 value )

 Returns the fractional part of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double3* **value** - Argument value.

### Return value

Resulting value.
## double4 dfrac ( double4 value )

 Returns the fractional part of the argument.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *double4* **value** - Argument value.

### Return value

Resulting value.
