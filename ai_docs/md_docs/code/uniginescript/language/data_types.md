# Data Types

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


In UnigineScript, [Dynamical Typing](../../../code/uniginescript/language/features.md#dynamic_typing) is used. It means that type checking is performed during code execution.


Information about the **Container Types** (maps and vectors) can be found [here](../../../code/uniginescript/language/containers/index.md).


## Fundamental Data Types


A variable can hold the following Fundamental Data Types:


| Name | Description | Size | Range |
|---|---|---|---|
| [int](#int) | Integer | 4 bytes | signed: -2147483648 to 2147483647 |
| [long](#long) | Long Integer | 8 bytes | signed: �9223372036854775808 to 9223372036854775807 |
| [float](#float) | Floating Point Number | 4 bytes | +/- 3.4e +/- 38 (~7 digits) |
| [double](#double) | Double Precision Floating Point Number | 8 bytes | +/- 1.7e +/- 308 (~15 digits) |
| [string](#string) | A String of Characters |  |  |
| [enum](#enum) | A Set of Integer Constants with Names | 2 bytes | signed: -2147483648 to 2147483647 |


### int


Represents an integer number. The initial value is **0**.


You can use decimal (base-10), hexadecimal (base-16) or ASCII character notation, with an optional preceding sign (- or +).


```cpp
int a = -123;	// negative number, decimal
int b = 0x1E;	// hexadecimal number (equivalent to 30 in decimal notation)
int c = 'N';	// character from the ASCII table (equivalent to 78 in decimal notation)

```


### long


Represents a long integer. This data type is used when you need a range of values wider than those provided by [int](#int). The initial value is **0L**.


You can use decimal (base-10) or hexadecimal (base-16) notations with a mandatory **l** or **L** postfix and an optional preceding sign (- or +).


> **Notice:** If there is no **l** or **L** postfix, a value is considered as [int](#int).


```cpp
long a = -123456789123456L;	// negative number, decimal
long b = 0x1EL;	// hexadecimal number

```


### float


A single-precision (32-bit) floating point value. The initial value is **0.0f**.


You can use any of the following notations, with a mandatory **f** or **F** postfix and an optional preceding sign (- or +).


> **Notice:** If there is no **f** or **F** after the number, it is considered a [double](#double).


```cpp
float a = 3.14f;	// decimal notation
float b = 1.8e15F;	// exponential notation
float c = 9.5E-7F;	// exponential notation

```


### double


Represents a double DC2-precision (64-bit) floating point value. The initial value is **0.0**.

```cpp
double a = 3.14;	// decimal notation
double b = 1.8e15;	// exponential notation
double c = 9.5E-7;	// exponential notation

```


### string


A string of characters. The initial value is an empty string.

> **Notice:** Unlike C++, UnigineScript doesn't require null-termination of strings.


```cpp
string a = "sequence of characters";
string b = "long " + a;	// b = "long sequence of characters"

```

 Strings can be concatenated not only with strings but with variables of any base type due to type casting.
```cpp
int b = 4;
string c = "sequence of " + b + " characters";	// d = "sequence of 4 characters"
string d = string(b) + " characters";	// d = "4 characters"

```


### enum


A set of integer constants with names assigned to them.


By default, values start from **0** and then increase from element to element:

```cpp
enum {
	KEY_UP,		// 0
	KEY_DOWN,	// 1
	KEY_LEFT,	// 2
	KEY_RIGHT,	// 3
};

```

 But you can set a value explicitly:
```cpp
enum {
	KEY_F1 = 100,	// 100
	KEY_F2, 	// 101
	KEY_F3 = 0x1E, 	// 30
	KEY_F4,		// 31
};

```

 For example, you can use the constants as follows:
```cpp
int key = 3;
if (key == KEY_RIGHT) {
	log.message("go right\n");
};

// the output is: go right

```


You can also set the value of previously specified enums. For example:

```cpp
enum {
	KEY_NEW = KEY_UP,
};

```


## 3D Related Data Types


### vec3


A vector of three [*float*](#float) components. The initial value is**(0.0f,0.0f,0.0f)**.


You can set a vector the following ways:

- As an object. In this case, all three vector components are specified. ```cpp vec3 a; a = vec3(2.0f,-3.1f,0.5f); ``` > **Notice:** [Vector](../../../code/uniginescript/language/containers/index.md#vector) initialization is different from C++. Instead of providing a list of vector items inside two curly braces {}, enclose the items in simple *parentheses* ().
- As an object, whose components are equal to the argument. ```cpp a = vec3(2.0f); ```
- 1-, 2-, 3-element or arbitrary [swizzles](#swizzling). ```cpp vec3 b; vec3 c; b.x = a.z; b.y = a.x; b.z = a.y; c = b.xzy; log.message("b is %s\n",typeinfo(b)); log.message("c is %s\n",typeinfo(c)); // b is vec3: 0.5 2 -3.1 // c is vec3: 0.5 -3.1 2 ```


Note that if you use [*vec4*](#vec4) (or [*dvec4*](#dvec4)) for initialization of*vec3*, then *vec4.w* will be omitted:

```cpp
vec3 a = vec3(vec4(2.0f,-3.1f,0.5f,7.2f)); // last number (7.2f) is omitted
```


It is possible to add or subtract a scalar value (*int*, *long*, *float* or *double*) from a vector. A vector should go first, before a scalar.

```cpp
vec3 a = vec3(2.0f,-3.1f,0.5f);

a += 1;
vec3 b = a - 1.5f;

// a contents: 3, -2.1, 1.5
// b contents: 1.5, -3.6, -0

```


### dvec3


A vector of three [double](#double) components. The initial value is **(0.0,0.0,0.0)**.


You can set a vector the following ways:

- As an object. In this case, all three vector components are specified. ```cpp dvec3 a; a = dvec3(2.0,-3.1,0.5); ```
- As an object, whose components are equal to the argument. ```cpp a = dvec3(2.0); ```
- [Swizzling](#swizzling) is also available for *dvec3*. ```cpp dvec3 b; b.x = a.z; b.yz = a.xy; log.message("b is %s\n",typeinfo(b)); // b is dvec3: 0.5 2 -3.1 ```


Note that if you use [*dvec4*](#dvec4) (or [*vec4*](#vec4)) for initialization of*dvec3*, then *dvec4.w* will be omitted:

```cpp
dvec3 a = dvec3(dvec4(2.0,-3.1,0.5,7.2)); // last number (7.2) is omitted
```


It is possible to add or subtract a scalar value (*int*, *long*, *float* or *double*) from a vector. A vector should go first, before a scalar.

```cpp
dvec3 a = dvec3(2.0f,-3.1f,0.5f);

a += 1;
dvec3 b = a - 1.5f;
log.message("%s\n",typeinfo(a));
log.message("%s\n",typeinfo(b));

```

 The example produces the following:
```text
dvec3: 3 -2.1 1.5
dvec3: 1.5 -3.6 0

```


### ivec3


A vector of three [integer](#int) components. The initial value is **(0,0,0)**.


You can set a vector the following ways:

- As an object. ```cpp ivec3 a; a = ivec3(2,-3,5); ```
- As an object, whose components are equal to the argument. ```cpp a = ivec3(2); ```
- [Swizzling](#swizzling) is also available for *ivec3*. You can use it the same way as for *vec3*. ```cpp ivec3 b; b = a.zyy; log.message("b is %s\n",typeinfo(b)); // b is ivec3: 5 -3 -3 ```


It is possible to add or subtract a scalar value (*int*) from a vector. A vector should go first, before a scalar.

```cpp
ivec3 a = ivec3(2,-3,1);

a += 1;
ivec3 b = a - 1;
log.message("%s\n",typeinfo(a));
log.message("%s\n",typeinfo(b));

```

 The example produces the following:
```text
ivec3: 3 -2 2
ivec3: 2 -3 1

```


### vec4


A vector of four [*float*](#float) components. The initial value is**(0f,0f,0f,0f)**.


You can set a vector the following ways:

- As an object. In this case, all vector components are specified. Also you can use vec3 for initialization of vec4. ```cpp vec4 a; a = vec4(2.0f,-3.1f,0.5f,7.2f); a = vec4(vec3(2.0f,-3.1f,0.5f),7.2f); ```
- As an object, whose components are equal to the argument. ```cpp a = vec4(2.0f); ```
- [Swizzling](#swizzling) is also available for *vec4*.The difference between [*vec4*](#vec4) and [*vec3*](#vec3) is that you can swizzle four components (x,y,z,w) for*vec4*. ```cpp vec4 b; vec4 c; b.x = a.z; b.y = a.w; b.zw = a.yy; c = b.xyyz; log.message("b is %s\n",typeinfo(b)); log.message("c is %s\n",typeinfo(c)); // b is vec4: 0.5 7.2 -3.1 -3.1 // c is vec4: 0.5 7.2 7.2 -3.1 ```


Note that if you use [*vec3*](#vec3) (or [*dvec3*](#dvec3)) for initialization of*vec4* then *vec4.w* will be **1.0f** by default:

```cpp
vec4 a = vec4(vec3(2.0f,-3.1f,0.5f)); // the vector content is: 2.0f,-3.1f,0.5f,1.0f
```


It is possible to add or subtract a scalar value (*int*, *long*, *float* or *double*) from a vector. A vector should go first, before a scalar.

```cpp
vec4 a = vec4(2.0f,-3.1f,0.5f,6.0f);

a += 1.5f;
vec4 b = a - 1.5f;
log.message("%s\n",typeinfo(a));
log.message("%s\n",typeinfo(b));

```

 The example produces the following output:
```text
vec4: 3.5 -1.6 2 7.5
vec4: 2 -3.1 0.5 6

```


### dvec4


A vector of four [double](#double) components. The initial value is **(0.0,0.0,0.0,0.0)**.


You can set a vector the following ways:

- As an object. You can use vec3 for initialization of dvec4. ```cpp dvec4 a; a = dvec4(2.0,-3.1,0.5,7.2); a = dvec4(vec3(2.0,-3.1,0.5),7.2); ```
- As an object, all components are equal to the argument. ```cpp a = dvec4(2.0); ```
- [Swizzling](#swizzling) is performed for *dvec4* the same way as for [*vec4*](#vec4). ```cpp dvec4 b; b.x = a.z; b.yzw = a.xy0; log.message("b is %s\n",typeinfo(b)); // b is dvec4: 0.5 2 -3.1 0 ```


Note that if you use [*dvec3*](#dvec3) (or [*vec3*](#vec3)) for initialization of*dvec4* then *dvec4.w* will be **1.0** by default:

```cpp
dvec4 a = dvec4(dvec3(2.0,-3.1,0.5)); // a.w = 1.0
```


It is possible to add or subtract a scalar value (*int*, *long*, *float* or *double*) from a vector. A vector should go first, before a scalar.

```cpp
dvec4 a = dvec4(2.0f,-3.1f,0.5f,6.0f);

a += 1.5f;
dvec4 b = a - 1.5f;
log.message("%s\n",typeinfo(a));
log.message("%s\n",typeinfo(b));

```

 The example produces the following:
```text
dvec4: 3.5 -1.6 2 7.5
dvec4: 2 -3.1 0.5 6

```


### ivec4


A vector of four [integer](#double) components. The initial value is **(0,0,0,0)**.


You can set a vector the following ways:

- As an object. ```cpp ivec4 a; a = ivec4(2,-3,5,7); ```
- As an object, whose components are equal to the argument. ```cpp a = ivec4(2); ```
- [Swizzling](#swizzling) is performed for *ivec4* the same way as for [*vec4*](#vec4) and [*dvec4*](#vec4). ```cpp ivec4 b; b = a.wyy1; log.message("b is %s\n",typeinfo(b)); // b is ivec4: 7 -3 -3 1 ```


It is possible to add or subtract a scalar value (*int*) from a vector. A vector should go first, before a scalar.

```cpp
ivec4 a = ivec4(2,-3,1,6);

a += 1.5f;
vec4 b = a - 1.5f;
log.message("%s\n",typeinfo(a));
log.message("%s\n",typeinfo(b));

```

 The example produces the following:
```text
ivec4: 3 -2 2 7
ivec4: 2 -3 1 6

```


### mat4


A matrix of sixteen (4�4) [*float*](#float) components. The initial value is the identity matrix:


| 1 | 0 | 0 | 0 |
|---|---|---|---|
| 0 | 1 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 0 | 0 | 1 |


> **Notice:** Matrices are column-oriented (OpenGL style).


Addressing:

```text
m00 m01 m02 m03
m10 m11 m12 m13
m20 m21 m22 m23
m30 m31 m32 m33

```


You can set a matrix the following ways:

- As an object. You can directly declare each matrix element. ```cpp mat4 a; a = mat4("0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15"); ``` The matrix contains the following: ```text 0 4  8 12 1 5  9 13 2 6 10 14 3 7 11 15 ```
- As a translation matrix. In this case, *vec3* serves to initialize *mat4*. ```cpp a = mat4(vec3(1,2,3)); ``` The other way to set the elements of *mat4*: ```cpp a = mat4(1,2,3); ``` The result is the translation matrix: ```text 1 0 0 1 0 1 0 2 0 0 1 3 0 0 0 1 ```
- As a rotation matrix. It is possible to use [quaternion](#quat) to set matrix elements. ```cpp a = mat4(quat(1,0,0,45)); ``` You can initialize *mat4* by axis and angle values. ```cpp a = mat4(vec3(1,0,0),45); ``` Or by scalars. ```cpp a = mat4(1,0,0,45); ``` The result is the rotation matrix: ```text 1 0    0   1 0 0.7 -0.7 0 0 0.7  0.7 0 0 0    0   1 ```
- [Swizzling](#swizzling) is also available for matrices. For example: ```cpp mat4 b; b.m00m01m02m03 = vec4(1,2,3,4); b.m00m10m20m30 = vec4(5,6,7,8); b.m03m13m23 = vec3(1,2,3); b.m03m23 = vec3(1,2,0); b.m00m11m22m33 = a.m30m21m12m03; log.message("b is %s\n",typeinfo(b)); ``` The result is: ```text 3  2  3  1 6  6  0  2 7  0  9  2 8  0  0  12 ```
- You can [swizzle](#swizzling) rows and columns of the matrix. For example: ```cpp vec4 row = a.row0;	// returns the full 1st row: 0 4 8 12 vec4 col = a.col3;	// returns the full 4th column: 12 13 14 15 dvec3 row_3 = a.row03;	// returns the first 3 elements of the 1st row: 0 4 8 dvec3 col_3 = a.col23;	// returns the first 3 elements of the 3rd column: 8 9 10 ```
- You can also [swizzle](#swizzling) columns as follows: ```cpp vec4 col1 = a.binormal; // get the first 3 components of the col1 vec4 col2 = a.normal; // get the first 3 components of the col2 ```


### dmat4


A matrix of twelve [*double*](#double) components. This is a 4�4 affine transformation matrix with the last row not stored. Instead, the last row is always of the form "**0 0 0 1** " and its values cannot be written, only read. The initial value is the identity matrix:


| 1 | 0 | 0 | 0 |
|---|---|---|---|
| 0 | 1 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| **0** | **0** | **0** | **1** |


> **Notice:** Matrices are column-oriented (OpenGL style).


Addressing:

```text
m00 m01 m02 m03
m10 m11 m12 m13
m20 m21 m22 m23
m30 m31 m32 m33

```


You can set a matrix the following ways:

- As an object. You can directly declare each matrix element. ```cpp dmat4 a; a = dmat4("0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15"); ``` The result is: ```text 0 4  8 12 1 5  9 13 2 6 10 14 0 0  0  1 ```
- As a translation matrix. *vec3* serves to initialize *dmat4*. ```cpp a = dmat4(dvec3(1,2,3)); ``` The other way to set the elements of *dmat4*: ```cpp a = dmat4(1,2,3); ``` The result is the translation matrix: ```text 1 0 0 1 0 1 0 2 0 0 1 3 0 0 0 1 ```
- As a rotation matrix. In this case, [quaternion](#quat) is used to set matrix elements. ```cpp a = dmat4(quat(1,0,0,45)); ``` Also you can initialize *dmat4* by axis and angle values. ```cpp a = dmat4(vec3(1,0,0),45); ``` Or by scalars. ```cpp a = dmat4(1,0,0,45); ``` The result is the rotation matrix: ```text 1 0    0   1 0 0.7 -0.7 0 0 0.7  0.7 0 0 0    0   1 ```
- [Swizzling](#swizzling) is also available for *dmat4*. For example: ```cpp dmat4 b; b.m00m01m02m03 = dvec4(1,2,3,4); b.m00m10m20m30 = dvec4(5,6,7,8); // m30 will not be written b.m03m13m23 = vec3(1,2,3); b.m03m23 = vec3(1,2,0); b.m00m11m22m33 = a.m30m21m12m03; // m33 will not be written log.message("b is %s\n",typeinfo(b)); ``` The result is: ```text 0  2  3  1 6  6  0  2 7  0  9  2 8  0  0  1 ``` > **Notice:** *.m30* and *.m33* elements will not be written.
- You can [swizzle](#swizzling) rows and columns of *dmat4*. ```cpp vec4 row = a.row0;	// returns the full 1st row: 0 4 8 12 vec4 col = a.col3;	// returns the full 4th column: 12 13 14 15 dvec3 row_3 = a.row03;	// returns the first 3 elements of the 1st row: 0 4 8 dvec3 col_3 = a.col23;	// returns the first 3 elements of the 3rd column: 8 9 10 ```
- You can also [swizzle](#swizzling) columns as follows: ```cpp vec4 col1 = a.binormal; // get the first 3 elements of the col1 vec4 col2 = a.normal; // get the first 3 elements of the col2 ```


### quat


*quat* is a quaternion, which components are [*float*](#float) numbers. The quaternion is a mathematical construct that represents a rotation in three dimensions. The initial value is**(0,0,0,1)**, where *x*, *y* and *z* components represent the rotation axis, and a w component represents the rotation angle.


You can set a quaternion by using different ways:

- As an object. You can directly set quaternion values. ```cpp quat a; a = quat(1,2,3,4); ```
- Also you can use *mat4* for initialization of *quat*. ```cpp a = quat(mat4(1,2,3,4)); ```
- By using axis and angle values. ```cpp a = quat(vec3(1,2,3),0.2); ```
- By scalars. ```cpp a = quat(1,2,3,0.2); ```
- Quaternion also supports [swizzling](#swizzling). For example: ```cpp a.xyz = a.wzx; a.wzy = vec3(1,2,3); a.xyzw = a.wzyx; a.wyzw = vec4(1,2,3,4); a.xyz += a.wyz; ```
- If the *quat* is the mesh compressed tangent vector, you can use the *binormal* and *normal* components  to get the corresponding vectors with the normalized **w** component. For example: ```cpp vec3 t = vec3(1.0f,0.0f,0.0f); // the tangent basis: tangent vector vec3 b = vec3(0.0f,1.0f,0.0f); // binormal vector vec3 n = vec3(0.0f,0.0f,1.0f); // normal vector vec4 tangent = orthoTangent(t,b,n); // this is the mesh compressed tangent vector quat q = quat(tangent); // convert vec4 to quat q.binormal; // get the binormal vector with w normalization q.normal; // get the normal vector with w normalization ```


## Swizzling


Swizzling gives an ability to select components in an arbitrary order. It provides a convenient elements access. It is available for the following 3D related data types:

- vector (*vec3, dvec3, ivec3, vec4, dvec4, ivec4*). You can use *x, y, z, w* to refer respectively to the first, the second, the third and the fourth vector component. The *r, g, b, a* components are used instead of *x, y, z, w* to refer to a color. > **Notice:** You can combine different component names in a single operation. For example, *a.xrb* is valid. Also it is possible to use *0* or *1* instead of *x, y, z* or *w* (or *r, g, b, a* respectively): ```cpp vec4 v = vec4(10.0f,11.0f,12.0f,13.0f); // swizzles log.message("%s\n",typeinfo(v.xyzw)); log.message("%s\n",typeinfo(v.10zw)); log.message("%s\n",typeinfo(v.xy10)); ``` The output is: ```text vec4: 10 11 12 13 vec4: 1 0 12 13 vec4: 10 11 1 0 ``` > **Notice:** You can use only *0* or *1*.
- matrix (*mat4, dmat4*).

  - The *m01..m33* components are used to refer to [matrix elements](#mat_addressing).
  - The *col0..col3* components are used to refer to [matrix columns](#mat_row_col). > **Notice:** To refer to the first *n* elements of the column, use *col00..col33*. The second digit specifies the number of column elements to be referred.
  - The *row0..row3* components are used to refer to [matrix rows](#mat_row_col). > **Notice:** To refer to the first *n* elements of the row, use *row00..row33*. The second digit specifies the number of row elements to be referred.
  - The *tangent*, *binormal* and *normal* components return the first 3 components of *col0*, *col1* and *col2* respectively.
- quaternion (*quat*).

  - The *x, y, z, w* components are also used for referring to quaternion components.
  - If the *quat* is the mesh compressed tangent vector, you can use the *binormal* and *normal* components  to get the corresponding vectors with the normalized **w** component.


### Examples


The following types of the swizzling are available:

- One-element swizzle. You can access any vector (matrix, quaternion) element as a scalar value (*int, long, float, double*). ```cpp vec3 a = vec3(2.0f,-3.1f,0.5f); float b = a.z; log.message("%s\n",typeinfo(b)); // the output is: float: 0.5 ``` Moreover, swizzling allows any component to take the value of any of the components of the same vector, matrix or quaternion.  For example, *x* component takes the value of *z* component: ```cpp vec3 a = vec3(2.0f,-3.1f,0.5f); a.x = a.z; log.message("%s\n",typeinfo(a.x)); // float: 0.5 ``` This is also true for swizzling any number of elements.
- Two-element swizzles. The result is a 3-component vector, where the last element is 0. ```cpp log.message("%s\n",typeinfo(a.zx)); // the output is: vec3: 0.5 2 0 ``` > **Notice:** If the two-element swizzle is applied to a 4-component vector, a matrix or a quaternion, the result is still the 3-component vector.
- Three-element swizzles give an ability to access the elements in any order. ```cpp log.message("%s\n",typeinfo(a.zyx)); // the output is: vec3: 0.5 -3.1 2 ``` Swizzling can be used in a vector setting: ```cpp vec3 b = a.xzy; log.message("%s\n",typeinfo(b)); // vec3: 2 0.5 -3.1 ```
- Arbitrary swizzles mean that any combination of the components can be used. It means that you can use the same components more than ones. ```cpp log.message("%s\n",typeinfo(a.zyy)); // the output is: vec3: 0.5 -3.1 -3.1 ```
- *rgba* swizzling. You can set a color by using the *rgba* components in the same way as the *xyzw* components. For example: ```cpp vec3 a = vec3(2.0f,-3.1f,0.5f); vec3 b; b.r = 2.0f; b.g = a.g; b.b = 0.5f; log.message("%s\n",typeinfo(b)); log.message("%s\n",typeinfo(a.rbb)); // vec3: 2 -3.1 0.5 // vec3: 2 0.5 0.5 ```
- Swizzles per row and column (for matrices). It means that the rows and the columns can be accessed the same way as elements. ```cpp mat4 a; a = mat4("0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15"); vec4 row = a.row0; // returns the full 1st row: 0 4 8 12 vec4 col = a.col3; // returns the full 4th column: 12 13 14 15 ``` Furthermore, you can access the specified number of the elements of the certain row or the column. ```cpp dvec3 row_3 = a.row03; // returns the first 3 elements of the 1st row: 0 4 8 dvec3 col_3 = a.col23; // returns the first 3 elements of the 3rd column: 8 9 10 ``` It is also possible to add **0** or **1** to the end of the row or the column: ```cpp dvec4 row_4 = a.row13_1; // returns the 3 elements of the 2nd column + 1 in the end: 1 5 9 1 dvec4 col_4 = a.col33_1; // returns the 3 elements of the 4th column + 1 in the end: 12 13 14 1 ```


## Automatic Type Conversion


To perform an operation, most of [operators](../../../code/uniginescript/language/operators.md#numerical) must have ***both*** operands of the same type. This is why the automatic conversion occurs: from two operands types the biggest type is always chosen to hold the entire value and avoid truncation.


### Automatic Conversion of Scalar Types


The result of operations between [int](#int), [long](#long), [float](#int) and [double](#int) will be as follows:


|  | int | long | float | double |
|---|---|---|---|---|
| int | int | long | float | double |
| long | long | long | float | double |
| float | float | float | float | double |
| double | double | double | double | double |


For example:

```cpp
int a = 5;
float b = 2.3f;

log.message("%s\n",typeinfo(a+b));

// float: 7.3

```


You can force type conversion by using an explicit type casting:

```cpp
int a = 5;
float b = 2.3f;

log.message("%s\n",typeinfo(float(a) + b));

```


### Automatic Conversion of Vector Types


Vector types cannot be automatically converted into each other or into scalar types. Because of that, only several operations such as [multiplication](../../../code/uniginescript/language/operators.md#vector_mul) and [division](../../../code/uniginescript/language/operators.md#vector_div) can be performed with vectors of different types or scalars as arguments.


Automatic conversion is possible only for the following types while being safe:

| From | To |
|---|---|
| vec3 | dvec3 |
| vec4 | dvec4 |


For example:

```cpp
vec3 a = vec3( 1, 2, 3);
dvec3 b = dvec3(2.0,-3.1,0.5);
ivec3 c = ivec3(2,-3,5);

log.message("%s\n",typeinfo(a + b));	// dvec3: 3 -1.1 3.5
log.message("%s\n",typeinfo(a + c));	// in this case, an error occurs

```


You can force vector type conversion by using an explicit type casting:

```cpp
vec3 a = vec3( 1, 2, 3);
dvec3 b = dvec3(2.0,-3.1,0.5);

log.message("the result is: %s\n",typeinfo(dvec3(a) + b));

```
