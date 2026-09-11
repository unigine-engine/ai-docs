# Unigine.vec3 Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


## vec3 Class

### Properties

## 🔒︎ Vector3 vec

The
## 🔒︎ float x

The X component of the vector.Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ float y

The Y component of the vector.Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ float z

The Z component of the vector.Swizzle simplifying access to the corresponding vector components (in the specified order).
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
## 🔒︎ vec3 Absolute

The Returns the absolute value of an argument.
## 🔒︎ vec3 Clamped

The Returns the value clamped within the range of [0.0,1.0].
## 🔒︎ vec3 Normalized

The Returns a vector with the same direction as the specified vector, but with a length of one.
## 🔒︎ vec3 Frac

The Returns a vector containing fractional parts of the corresponding vector components.
## 🔒︎ vec3 Floor

The Returns a vector containing the largest integral values each being less than or equal to the corresponding vector component.
## 🔒︎ vec3 Ceil

The Returns a vector containing the smallest integral values each being greater than or equal to the corresponding vector component.
## 🔒︎ vec3 ZERO

The Vector, filled with zeros (0).
## 🔒︎ vec3 ONE

The Vector, filled with ones (1).
## 🔒︎ vec3 EPS

The Vector, filled with the *epsilon* constant (1e-6f).
## 🔒︎ vec3 INF

The Vector, filled with the *infinity* constant (1e+9f).
## 🔒︎ vec3 UP

The  UP direction vector: (0.0, 0.0, 1.0).
## 🔒︎ vec3 DOWN

The  DOWN direction vector: (0.0, 0.0, -1.0).
## 🔒︎ vec3 FORWARD

The  FORWARD direction vector: (0.0, 1.0, 0.0).
## 🔒︎ vec3 BACK

The  BACK direction vector: (0.0, -1.0, 0.0).
## 🔒︎ vec3 RIGHT

The  RIGHT direction vector: (1.0, 0.0, 0.0).
## 🔒︎ vec3 LEFT

The  LEFT direction vector: (-1.0, 0.0, 0.0).
## 🔒︎ vec3 WHITE

The  White color vector: RGBA is (1.0, 1.0, 1.0, 1.0).
## 🔒︎ vec3 BLACK

The  Black color vector: RGBA is (0.0, 0.0, 0.0, 1.0).
## 🔒︎ vec3 RED

The  Red color vector: RGBA is (1.0, 0.0, 0.0, 1.0).
## 🔒︎ vec3 GREEN

The  Green color vector: RGBA is (0.0, 1.0, 0.0, 1.0).
## 🔒︎ vec3 BLUE

The  Blue color vector: RGBA is (0.0, 0.0, 1.0, 1.0).
## 🔒︎ byte NUM_ELEMENTS

The Number of elements in the vector.
## 🔒︎ vec2 xx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 xy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 xz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 yx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 yy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 yz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 zx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 zy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 zz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 xxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 xxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 xxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 xyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 xyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 xyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 xzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 xzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 xzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 yxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 yxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 yxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 yyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 yyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 yyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 yzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 yzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 yzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 zxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 zxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 zxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 zyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 zyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 zyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 zzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 zzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 zzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xxxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xxxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xxxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xxyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xxyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xxyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xxzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xxzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xxzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xyxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xyxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xyxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xyyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xyyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xyyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xyzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xyzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xyzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xzxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xzxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xzxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xzyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xzyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xzyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xzzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xzzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 xzzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yxxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yxxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yxxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yxyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yxyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yxyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yxzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yxzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yxzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yyxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yyxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yyxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yyyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yyyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yyyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yyzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yyzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yyzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yzxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yzxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yzxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yzyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yzyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yzyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yzzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yzzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 yzzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zxxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zxxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zxxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zxyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zxyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zxyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zxzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zxzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zxzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zyxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zyxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zyxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zyyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zyyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zyyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zyzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zyzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zyzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zzxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zzxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zzxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zzyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zzyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zzyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zzzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zzzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 zzzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ float r

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ float g

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ float b

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 rr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 rg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 rb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 gr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 gg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 gb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 br

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 bg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec2 bb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 rrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 rrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 rrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 rgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 rgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 rgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 rbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 rbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 rbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 grr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 grg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 grb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 ggr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 ggg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 ggb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 gbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 gbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 gbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 brr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 brg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 brb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 bgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 bgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 bgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 bbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 bbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec3 bbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rrrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rrrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rrrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rrgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rrgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rrgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rrbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rrbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rrbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rgrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rgrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rgrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rggr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rggg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rggb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rgbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rgbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rgbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rbrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rbrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rbrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rbgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rbgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rbgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rbbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rbbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 rbbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 grrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 grrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 grrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 grgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 grgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 grgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 grbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 grbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 grbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 ggrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 ggrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 ggrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gggr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gggg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gggb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 ggbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 ggbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 ggbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gbrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gbrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gbrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gbgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gbgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gbgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gbbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gbbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 gbbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 brrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 brrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 brrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 brgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 brgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 brgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 brbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 brbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 brbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bgrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bgrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bgrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bggr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bggg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bggb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bgbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bgbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bgbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bbrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bbrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bbrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bbgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bbgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bbgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bbbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bbbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ vec4 bbbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
### Members

---

## vec3 operator* ( vec3 v0 , vec3 v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator* ( vec3 v0 , vec4 v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *vec4* **v1** - Second value.

## vec3 operator* ( vec3 v0 , vec2 v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *vec2* **v1** - Second value.

## vec3 operator* ( vec3 v0 , float v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *float* **v1** - Second value.

## vec3 operator* ( float v0 , vec3 v1 )

Multiplication.
### Arguments

- *float* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec3 operator* ( vec3 v0 , dvec3 v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec3 operator* ( vec3 v0 , dvec2 v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec3 operator* ( vec3 v0 , dvec4 v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec3 operator* ( vec3 v0 , double v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *double* **v1** - Second value.

## dvec3 operator* ( double v0 , vec3 v1 )

Multiplication.
### Arguments

- *double* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator* ( vec3 v0 , ivec3 v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *ivec3* **v1** - Second value.

## vec3 operator* ( vec3 v0 , ivec2 v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *ivec2* **v1** - Second value.

## vec3 operator* ( vec3 v0 , ivec4 v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *ivec4* **v1** - Second value.

## vec3 operator* ( vec3 v0 , int v1 )

Multiplication.
### Arguments

- *vec3* **v0** - First value.
- *int* **v1** - Second value.

## vec3 operator* ( int v0 , vec3 v1 )

Multiplication.
### Arguments

- *int* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator/ ( vec3 v0 , vec3 v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator/ ( vec3 v0 , vec4 v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *vec4* **v1** - Second value.

## vec3 operator/ ( vec3 v0 , vec2 v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *vec2* **v1** - Second value.

## vec3 operator/ ( vec3 v0 , float v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *float* **v1** - Second value.

## vec3 operator/ ( float v0 , vec3 v1 )

Division.
### Arguments

- *float* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec3 operator/ ( vec3 v0 , dvec3 v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec3 operator/ ( vec3 v0 , dvec2 v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec3 operator/ ( vec3 v0 , dvec4 v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec3 operator/ ( vec3 v0 , double v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *double* **v1** - Second value.

## dvec3 operator/ ( double v0 , vec3 v1 )

Division.
### Arguments

- *double* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator/ ( vec3 v0 , ivec3 v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *ivec3* **v1** - Second value.

## vec3 operator/ ( vec3 v0 , ivec2 v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *ivec2* **v1** - Second value.

## vec3 operator/ ( vec3 v0 , ivec4 v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *ivec4* **v1** - Second value.

## vec3 operator/ ( vec3 v0 , int v1 )

Division.
### Arguments

- *vec3* **v0** - First value.
- *int* **v1** - Second value.

## vec3 operator/ ( int v0 , vec3 v1 )

Division.
### Arguments

- *int* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator- ( vec3 v0 , vec3 v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator- ( vec3 v0 , vec4 v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *vec4* **v1** - Second value.

## vec3 operator- ( vec3 v0 , vec2 v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *vec2* **v1** - Second value.

## vec3 operator- ( vec3 v0 , float v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *float* **v1** - Second value.

## vec3 operator- ( float v0 , vec3 v1 )

Subtraction.
### Arguments

- *float* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec3 operator- ( vec3 v0 , dvec3 v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec3 operator- ( vec3 v0 , dvec2 v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec3 operator- ( vec3 v0 , dvec4 v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec3 operator- ( vec3 v0 , double v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *double* **v1** - Second value.

## dvec3 operator- ( double v0 , vec3 v1 )

Subtraction.
### Arguments

- *double* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator- ( vec3 v0 , ivec3 v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *ivec3* **v1** - Second value.

## vec3 operator- ( vec3 v0 , ivec2 v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *ivec2* **v1** - Second value.

## vec3 operator- ( vec3 v0 , ivec4 v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *ivec4* **v1** - Second value.

## vec3 operator- ( vec3 v0 , int v1 )

Subtraction.
### Arguments

- *vec3* **v0** - First value.
- *int* **v1** - Second value.

## vec3 operator- ( int v0 , vec3 v1 )

Subtraction.
### Arguments

- *int* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator+ ( vec3 v0 , vec3 v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator+ ( vec3 v0 , vec4 v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *vec4* **v1** - Second value.

## vec3 operator+ ( vec3 v0 , vec2 v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *vec2* **v1** - Second value.

## vec3 operator+ ( vec3 v0 , float v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *float* **v1** - Second value.

## vec3 operator+ ( float v0 , vec3 v1 )

Addition.
### Arguments

- *float* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec3 operator+ ( vec3 v0 , dvec3 v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec3 operator+ ( vec3 v0 , dvec2 v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec3 operator+ ( vec3 v0 , dvec4 v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec3 operator+ ( vec3 v0 , double v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *double* **v1** - Second value.

## dvec3 operator+ ( double v0 , vec3 v1 )

Addition.
### Arguments

- *double* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator+ ( vec3 v0 , ivec3 v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *ivec3* **v1** - Second value.

## vec3 operator+ ( vec3 v0 , ivec2 v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *ivec2* **v1** - Second value.

## vec3 operator+ ( vec3 v0 , ivec4 v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *ivec4* **v1** - Second value.

## vec3 operator+ ( vec3 v0 , int v1 )

Addition.
### Arguments

- *vec3* **v0** - First value.
- *int* **v1** - Second value.

## vec3 operator+ ( int v0 , vec3 v1 )

Addition.
### Arguments

- *int* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator% ( vec3 v0 , vec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator% ( vec3 v0 , vec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *vec4* **v1** - Second value.

## vec3 operator% ( vec3 v0 , vec2 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *vec2* **v1** - Second value.

## vec3 operator% ( vec3 v0 , float v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *float* **v1** - Second value.

## vec3 operator% ( float v0 , vec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *float* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec3 operator% ( vec3 v0 , dvec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec3 operator% ( vec3 v0 , dvec2 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec3 operator% ( vec3 v0 , dvec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec3 operator% ( vec3 v0 , double v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *double* **v1** - Second value.

## dvec3 operator% ( double v0 , vec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *double* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator% ( vec3 v0 , ivec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *ivec3* **v1** - Second value.

## vec3 operator% ( vec3 v0 , ivec2 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *ivec2* **v1** - Second value.

## vec3 operator% ( vec3 v0 , ivec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *ivec4* **v1** - Second value.

## vec3 operator% ( vec3 v0 , int v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *vec3* **v0** - First value.
- *int* **v1** - Second value.

## vec3 operator% ( int v0 , vec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *int* **v0** - First value.
- *vec3* **v1** - Second value.

## vec3 operator- ( vec3 v )

Subtraction.
### Arguments

- *vec3* **v** - Value.

## vec3 operator+ ( vec3 v )

Addition.
### Arguments

- *vec3* **v** - Value.

## vec3 operator++ ( vec3 v )

Increment.
### Arguments

- *vec3* **v** - Value.

## vec3 operator-- ( vec3 v )

Decrement.
### Arguments

- *vec3* **v** - Value.

## bool operator== ( vec3 v0 , vec3 v1 )

Performs equal comparison.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## bool operator!= ( vec3 v0 , vec3 v1 )

Not equal comparison.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## bool operator> ( vec3 v0 , vec3 v1 )

Greater comparison.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## bool operator< ( vec3 v0 , vec3 v1 )

Greater comparison.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## bool operator>= ( vec3 v0 , vec3 v1 )

Greater than or equal to comparison.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## bool operator<= ( vec3 v0 , vec3 v1 )

Less than or equal to comparison.
### Arguments

- *vec3* **v0** - First value.
- *vec3* **v1** - Second value.

## bool operatortrue ( vec3 v )

Returns **true** if the operand is both, not **null** and not **NaN**.
### Arguments

- *vec3* **v** - Value.

## bool operatorfalse ( vec3 v )

Returns **true** if the operand is both, **null** and **NaN**.
### Arguments

- *vec3* **v** - Value.

## void Set ( Vector3 v )

Sets the value using the specified argument(s).
### Arguments

- *Vector3* **v** - Source vector.

## void Set ( float vx , float vy , float vz )

Sets the value using the specified argument(s).
### Arguments

- *float* **vx** - New *float* value to be set for the first component.
- *float* **vy** - New *float* value to be set for the second component.
- *float* **vz** - New *float* value to be set for the third component.

## void Set ( float v )

Sets the value using the specified argument(s).
### Arguments

- *float* **v** - A *float* value to be used.

## void Set ( float[] v )

Sets the value using the specified argument(s).
### Arguments

- *float[]* **v** - Source vector.

## void Set ( vec2 v , float vz )

Sets the value using the specified argument(s).
### Arguments

- *vec2* **v** - Source vector.
- *float* **vz** - New *float* value to be set for the third component.

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

## void Set ( double vx , double vy , double vz )

Sets the value using the specified argument(s).
### Arguments

- *double* **vx** - New *double* value to be set for the first component.
- *double* **vy** - New *double* value to be set for the second component.
- *double* **vz** - New *double* value to be set for the third component.

## void Set ( double v )

Sets the value using the specified argument(s).
### Arguments

- *double* **v** - A *double* value to be used.

## void Set ( double[] v )

Sets the value using the specified argument(s).
### Arguments

- *double[]* **v** - Source vector.

## void Set ( dvec2 v , double vz )

Sets the value using the specified argument(s).
### Arguments

- *dvec2* **v** - Source vector.
- *double* **vz** - New *double* value to be set for the third component.

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

## void Set ( int vx , int vy , int vz )

Sets the value using the specified argument(s).
### Arguments

- *int* **vx** - New *int* value to be set for the first component.
- *int* **vy** - New *int* value to be set for the second component.
- *int* **vz** - New *int* value to be set for the third component.

## void Set ( int v )

Sets the value using the specified argument(s).
### Arguments

- *int* **v** - A *int* value to be used.

## void Set ( int[] v )

Sets the value using the specified argument(s).
### Arguments

- *int[]* **v** - Source vector.

## void Set ( ivec2 v , int vz )

Sets the value using the specified argument(s).
### Arguments

- *ivec2* **v** - Source vector.
- *int* **vz** - New *int* value to be set for the third component.

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

## void Set ( byte vx , byte vy , byte vz )

Sets the value using the specified argument(s).
### Arguments

- *byte* **vx** - New *byte* value to be set for the first component.
- *byte* **vy** - New *byte* value to be set for the second component.
- *byte* **vz** - New *byte* value to be set for the third component.

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
## void Add ( vec3 v )

Performs addition of the specified argument.
### Arguments

- *vec3* **v** - Value.

## void Add ( float v )

Performs addition of the specified argument.
### Arguments

- *float* **v** - Value.

## void Sub ( vec3 v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *vec3* **v** - Value.

## void Sub ( float v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *float* **v** - Value.

## void Mul ( vec3 v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *vec3* **v** - Vector multiplier.

## void Mul ( float v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *float* **v** - A *float* multiplier.

## void Div ( vec3 v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *vec3* **v** - A *vec3* divisor value.

## void Div ( float v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *float* **v** - A *float* divisor value.

## void Normalize ( )

Returns a vector with the same direction, but with a length of 1.
## bool Equals ( vec3 other )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *vec3* **other** - Value to be checked for equality.

### Return value

Return value.
## bool EqualsNearly ( vec3 other , float epsilon )

Checks if the argument represents the same value with regard to the specified accuracy (epsilon).
### Arguments

- *vec3* **other** - Value to be checked for equality.
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
