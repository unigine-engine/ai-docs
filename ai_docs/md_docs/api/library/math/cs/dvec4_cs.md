# Unigine.dvec4 Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


## dvec4 Class

### Properties

## 🔒︎ double x

The X component of the vector.
## 🔒︎ double y

The Y component of the vector.
## 🔒︎ double z

The Z component of the vector.
## 🔒︎ double w

The W component of the vector.
## 🔒︎ double Length

The Length of the vector.
## 🔒︎ double Minimum

The Minimum value among all components.
## 🔒︎ double Maximum

The Maximum value among all components.
## 🔒︎ double Length2

The Squared length of the vector. This method is much faster than *length()* � the calculation is basically the same only without the slow *Sqrt* call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
## 🔒︎ double ILength

The Inverted length of the vector.
## 🔒︎ double Sum

The Sum of vector components.
## 🔒︎ dvec4 Absolute

The Returns the absolute value of an argument.
## 🔒︎ dvec4 Clamped

The Returns the value clamped within the range of [0.0,1.0].
## 🔒︎ dvec4 Normalized

The Returns a vector with the same direction as the specified vector, but with a length of one.
## 🔒︎ dvec4 Frac

The Returns a vector containing fractional parts of the corresponding vector components.
## 🔒︎ dvec4 Floor

The Returns a vector containing the largest integral values each being less than or equal to the corresponding vector component.
## 🔒︎ dvec4 Ceil

The Returns a vector containing the smallest integral values each being greater than or equal to the corresponding vector component.
## 🔒︎ dvec4 ZERO

The Vector, filled with zeros (0).
## 🔒︎ dvec4 ONE

The Vector, filled with ones (1).
## 🔒︎ dvec4 EPS

The Vector, filled with the *epsilon* constant (1e-6f).
## 🔒︎ dvec4 INF

The Vector, filled with the *infinity* constant (1e+9f).
## 🔒︎ dvec4 WHITE

The  White color vector: RGBA is (1.0, 1.0, 1.0, 1.0).
## 🔒︎ dvec4 BLACK

The  Black color vector: RGBA is (0.0, 0.0, 0.0, 1.0).
## 🔒︎ dvec4 GREY

The  Grey color vector: RGBA is (0.5, 0.5, 0.5, 1.0).
## 🔒︎ dvec4 RED

The  Red color vector: RGBA is (1.0, 0.0, 0.0, 1.0).
## 🔒︎ dvec4 GREEN

The  Green color vector: RGBA is (0.0, 1.0, 0.0, 1.0).
## 🔒︎ dvec4 BLUE

The  Blue color vector: RGBA is (0.0, 0.0, 1.0, 1.0).
## 🔒︎ dvec4 CYAN

The  Cyan color vector: RGBA is (0.0, 1.0, 1.0, 1.0).
## 🔒︎ dvec4 MAGENTA

The  Magenta color vector: RGBA is (1.0, 0.0, 1.0, 1.0).
## 🔒︎ dvec4 YELLOW

The  Yellow color vector: RGBA is (1.0, 1.0, 0.0, 1.0).
## 🔒︎ byte NUM_ELEMENTS

The Number of elements in the vector.
## 🔒︎ dvec2 xx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 xy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 xz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 yx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 yy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 yz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 zx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 zy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 zz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 xxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 xxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 xxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 xyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 xyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 xyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 xzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 xzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 xzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 yxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 yxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 yxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 yyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 yyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 yyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 yzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 yzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 yzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 zxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 zxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 zxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 zyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 zyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 zyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 zzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 zzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 zzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xxxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xxxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xxxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xxyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xxyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xxyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xxzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xxzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xxzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xyxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xyxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xyxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xyyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xyyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xyyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xyzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xyzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xyzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xzxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xzxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xzxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xzyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xzyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xzyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xzzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xzzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 xzzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yxxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yxxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yxxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yxyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yxyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yxyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yxzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yxzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yxzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yyxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yyxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yyxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yyyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yyyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yyyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yyzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yyzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yyzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yzxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yzxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yzxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yzyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yzyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yzyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yzzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yzzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 yzzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zxxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zxxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zxxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zxyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zxyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zxyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zxzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zxzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zxzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zyxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zyxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zyxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zyyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zyyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zyyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zyzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zyzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zyzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zzxx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zzxy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zzxz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zzyx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zzyy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zzyz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zzzx

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zzzy

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 zzzz

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ double r

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ double g

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ double b

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 rr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 rg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 rb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 gr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 gg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 gb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 br

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 bg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec2 bb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 rrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 rrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 rrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 rgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 rgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 rgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 rbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 rbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 rbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 grr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 grg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 grb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 ggr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 ggg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 ggb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 gbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 gbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 gbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 brr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 brg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 brb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 bgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 bgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 bgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 bbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 bbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec3 bbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rrrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rrrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rrrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rrgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rrgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rrgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rrbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rrbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rrbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rgrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rgrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rgrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rggr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rggg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rggb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rgbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rgbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rgbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rbrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rbrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rbrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rbgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rbgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rbgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rbbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rbbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 rbbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 grrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 grrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 grrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 grgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 grgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 grgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 grbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 grbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 grbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 ggrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 ggrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 ggrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gggr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gggg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gggb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 ggbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 ggbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 ggbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gbrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gbrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gbrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gbgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gbgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gbgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gbbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gbbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 gbbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 brrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 brrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 brrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 brgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 brgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 brgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 brbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 brbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 brbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bgrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bgrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bgrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bggr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bggg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bggb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bgbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bgbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bgbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bbrr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bbrg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bbrb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bbgr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bbgg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bbgb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bbbr

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bbbg

The Swizzle simplifying access to the corresponding vector components (in the specified order).
## 🔒︎ dvec4 bbbb

The Swizzle simplifying access to the corresponding vector components (in the specified order).
### Members

---

## dvec4 operator* ( dvec4 v0 , vec2 v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *vec2* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , vec3 v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , vec4 v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *vec4* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , float v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *float* **v1** - Second value.

## dvec4 operator* ( float v0 , dvec4 v1 )

Multiplication.
### Arguments

- *float* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , dvec2 v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , dvec3 v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , dvec4 v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , double v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *double* **v1** - Second value.

## dvec4 operator* ( double v0 , dvec4 v1 )

Multiplication.
### Arguments

- *double* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , ivec2 v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , ivec3 v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , ivec4 v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## dvec4 operator* ( dvec4 v0 , int v1 )

Multiplication.
### Arguments

- *dvec4* **v0** - First value.
- *int* **v1** - Second value.

## dvec4 operator* ( int v0 , dvec4 v1 )

Multiplication.
### Arguments

- *int* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , vec2 v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *vec2* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , vec3 v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , vec4 v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *vec4* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , float v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *float* **v1** - Second value.

## dvec4 operator/ ( float v0 , dvec4 v1 )

Division.
### Arguments

- *float* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , dvec2 v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , dvec3 v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , dvec4 v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , double v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *double* **v1** - Second value.

## dvec4 operator/ ( double v0 , dvec4 v1 )

Division.
### Arguments

- *double* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , ivec2 v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , ivec3 v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , ivec4 v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## dvec4 operator/ ( dvec4 v0 , int v1 )

Division.
### Arguments

- *dvec4* **v0** - First value.
- *int* **v1** - Second value.

## dvec4 operator/ ( int v0 , dvec4 v1 )

Division.
### Arguments

- *int* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , vec2 v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *vec2* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , vec3 v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , vec4 v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *vec4* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , float v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *float* **v1** - Second value.

## dvec4 operator- ( float v0 , dvec4 v1 )

Subtraction.
### Arguments

- *float* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , dvec2 v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , dvec3 v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , dvec4 v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , double v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *double* **v1** - Second value.

## dvec4 operator- ( double v0 , dvec4 v1 )

Subtraction.
### Arguments

- *double* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , ivec2 v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , ivec3 v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , ivec4 v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## dvec4 operator- ( dvec4 v0 , int v1 )

Subtraction.
### Arguments

- *dvec4* **v0** - First value.
- *int* **v1** - Second value.

## dvec4 operator- ( int v0 , dvec4 v1 )

Subtraction.
### Arguments

- *int* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , vec2 v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *vec2* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , vec3 v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , vec4 v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *vec4* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , float v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *float* **v1** - Second value.

## dvec4 operator+ ( float v0 , dvec4 v1 )

Addition.
### Arguments

- *float* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , dvec2 v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , dvec3 v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , dvec4 v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , double v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *double* **v1** - Second value.

## dvec4 operator+ ( double v0 , dvec4 v1 )

Addition.
### Arguments

- *double* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , ivec2 v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , ivec3 v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , ivec4 v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## dvec4 operator+ ( dvec4 v0 , int v1 )

Addition.
### Arguments

- *dvec4* **v0** - First value.
- *int* **v1** - Second value.

## dvec4 operator+ ( int v0 , dvec4 v1 )

Addition.
### Arguments

- *int* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , vec2 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *vec2* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , vec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *vec3* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , vec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *vec4* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , float v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *float* **v1** - Second value.

## dvec4 operator% ( float v0 , dvec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *float* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , dvec2 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *dvec2* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , dvec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *dvec3* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , dvec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , double v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *double* **v1** - Second value.

## dvec4 operator% ( double v0 , dvec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *double* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , ivec2 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *ivec2* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , ivec3 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *ivec3* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , ivec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *ivec4* **v1** - Second value.

## dvec4 operator% ( dvec4 v0 , int v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *dvec4* **v0** - First value.
- *int* **v1** - Second value.

## dvec4 operator% ( int v0 , dvec4 v1 )

Modulo, gives the remainder of a division of two specified values.
### Arguments

- *int* **v0** - First value.
- *dvec4* **v1** - Second value.

## dvec4 operator- ( dvec4 v )

Subtraction.
### Arguments

- *dvec4* **v** - Value.

## dvec4 operator+ ( dvec4 v )

Addition.
### Arguments

- *dvec4* **v** - Value.

## dvec4 operator++ ( dvec4 v )

Increment.
### Arguments

- *dvec4* **v** - Value.

## dvec4 operator-- ( dvec4 v )

Decrement.
### Arguments

- *dvec4* **v** - Value.

## bool operator== ( dvec4 v0 , dvec4 v1 )

Performs equal comparison.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## bool operator!= ( dvec4 v0 , dvec4 v1 )

Not equal comparison.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## bool operator> ( dvec4 v0 , dvec4 v1 )

Greater comparison.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## bool operator< ( dvec4 v0 , dvec4 v1 )

Greater comparison.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## bool operator>= ( dvec4 v0 , dvec4 v1 )

Greater than or equal to comparison.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## bool operator<= ( dvec4 v0 , dvec4 v1 )

Less than or equal to comparison.
### Arguments

- *dvec4* **v0** - First value.
- *dvec4* **v1** - Second value.

## bool operatortrue ( dvec4 v )

Returns **true** if the operand is both, not **null** and not **NaN**.
### Arguments

- *dvec4* **v** - Value.

## bool operatorfalse ( dvec4 v )

Returns **true** if the operand is both, **null** and **NaN**.
### Arguments

- *dvec4* **v** - Value.

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

## void Set ( vec2 v , float vz , float vw )

Sets the value using the specified argument(s).
### Arguments

- *vec2* **v** - Source vector.
- *float* **vz** - New *float* value to be set for the third component.
- *float* **vw** - New *float* value to be set for the fourth component.

## void Set ( vec3 v , float vw )

Sets the value using the specified argument(s).
### Arguments

- *vec3* **v** - Source vector.
- *float* **vw** - New *float* value to be set for the fourth component.

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

## void Set ( dvec2 v , double vz , double vw )

Sets the value using the specified argument(s).
### Arguments

- *dvec2* **v** - Source vector.
- *double* **vz** - New *double* value to be set for the third component.
- *double* **vw** - New *double* value to be set for the fourth component.

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

## void Set ( ivec2 v , int vz , int vw )

Sets the value using the specified argument(s).
### Arguments

- *ivec2* **v** - Source vector.
- *int* **vz** - New *int* value to be set for the third component.
- *int* **vw** - New *int* value to be set for the fourth component.

## void Set ( ivec3 v , int vw )

Sets the value using the specified argument(s).
### Arguments

- *ivec3* **v** - Source vector.
- *int* **vw** - New *int* value to be set for the fourth component.

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
## void Add ( dvec4 v )

Performs addition of the specified argument.
### Arguments

- *dvec4* **v** - Value.

## void Add ( double v )

Performs addition of the specified argument.
### Arguments

- *double* **v** - Value.

## void Sub ( dvec4 v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *dvec4* **v** - Value.

## void Sub ( double v )

Subtracts each element of the specified argument from ther corresponding element.
### Arguments

- *double* **v** - Value.

## void Mul ( dvec4 v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *dvec4* **v** - Vector multiplier.

## void Mul ( double v )

Multiplies the vector by the value of the specified argument.
### Arguments

- *double* **v** - A *double* multiplier.

## void Div ( dvec4 v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *dvec4* **v** - A *dvec4* divisor value.

## void Div ( double v )

Returns the result of division of the vector by the value of the specified arguments.
### Arguments

- *double* **v** - A *double* divisor value.

## void Normalize ( )

Returns a vector with the same direction, but with a length of 1.
## bool Equals ( dvec4 other )

Checks if the vector and the specified argument are equal (epsilon).
### Arguments

- *dvec4* **other** - Value to be checked for equality.

### Return value

Return value.
## bool EqualsNearly ( dvec4 other , float epsilon )

Checks if the argument represents the same value with regard to the specified accuracy (epsilon).
### Arguments

- *dvec4* **other** - Value to be checked for equality.
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
## IEnumerator<double> GetEnumerator ( )

Returns an [**IEnumerator**](https://docs.microsoft.com/dotnet/api/system.collections.ienumerator?view=net-5.0) for the object.
### Return value

Return value.
## IEnumerator GetEnumerator ( )

Returns an [**IEnumerator**](https://docs.microsoft.com/dotnet/api/system.collections.ienumerator?view=net-5.0) for the object.
### Return value

Return value.
