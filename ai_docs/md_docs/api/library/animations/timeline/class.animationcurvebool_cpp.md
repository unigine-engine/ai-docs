# Unigine::AnimationCurveBool Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationCurve


This class represents an interface enabling you to create and manage animation curves containing boolean values.


## AnimationCurveBool Class

### Members

## int getNumKeys () const

Returns the current total number of key points in the curve.
### Return value

Current total number of key points in the curve.
## float getMinTime () const

Returns the current point of the whole animation timeline where this curve starts being applied, in units.
### Return value

Current point of the whole animation timeline where this curve starts being applied, in units.
## float getMaxTime () const

Returns the current point of the whole animation timeline up to which this curve is applied, in units.
### Return value

Current point of the whole animation timeline up to which this curve is applied, in units.
## void setPreInfinity ( AnimationCurve::EXTRAPOLATION infinity )

Sets a new way the curve behaves before its first key.
### Arguments

- *[AnimationCurve::EXTRAPOLATION](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#EXTRAPOLATION)* **infinity** - The way the curve behaves before its first key

## AnimationCurve::EXTRAPOLATION getPreInfinity () const

Returns the current way the curve behaves before its first key.
### Return value

Current way the curve behaves before its first key
## void setPostInfinity ( AnimationCurve::EXTRAPOLATION infinity )

Sets a new way the curve behaves after its last key.
### Arguments

- *[AnimationCurve::EXTRAPOLATION](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#EXTRAPOLATION)* **infinity** - The way the curve behaves after its last key

## AnimationCurve::EXTRAPOLATION getPostInfinity () const

Returns the current way the curve behaves after its last key.
### Return value

Current way the curve behaves after its last key
---

## AnimationCurveBool ( )

Constructor. Creates a new boolean animation curve instance.
## void assignFrom ( const Ptr < AnimationCurveBool > & curve )

Copies all data (key points and tangents) from the specified source curve.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveBool](../../../../api/library/animations/timeline/class.animationcurvebool_cpp.md)> &* **curve** - Source curve.

## int addKey ( float time , bool value )

Adds a new key point with the specified value at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *bool* **value** - The boolean value of the key.

### Return value

Index of the added key point.
## int addKey ( float time , bool value , AnimationCurve::KEY_TYPE type )

Adds a new key point with the specified value and type at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *bool* **value** - The boolean value of the key.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_CONSTANT) values.

### Return value

Index of the added key point.
## int addKey ( float time , bool value , AnimationCurve::KEY_TYPE type , const Math:: vec2 & left_tangent , const Math:: vec2 & right_tangent )

Adds a new key point with the specified value, type and tangents at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *bool* **value** - The boolean value of the key.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_CONSTANT) values.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **left_tangent** - Coordinates of the left tangent at the key point.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **right_tangent** - Coordinates of the right tangent at the key point.

### Return value

Index of the added key point.
## void removeKey ( int index )

Removes the key point with the specified index from the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

## int moveKey ( int index , float new_time )

Moves the key point with the specified number to a new time position (preserving the tangents). The index of key point will be updated automatically. This method can be used to implement dragging of keys on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *float* **new_time** - Time of the key on the timeline, in seconds.

### Return value

New index of the key.
## void setKeyType ( int index , AnimationCurve::KEY_TYPE type , float value_time_ratio = 1.0f )

Sets the interpolation type for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_CONSTANT) values.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the handles of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_ALIGNED) key are made collinear. The default value is 1.0f, which measures value and time on the same scale.

## AnimationCurve::KEY_TYPE getKeyType ( int index ) const

Returns the interpolation type of the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Interpolation type set for the key, one of the [KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_CONSTANT) values.
## float getKeyTime ( int index ) const

Returns the current time of the key point with the specified index.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The time of the specified key point on the timeline, in seconds.
## bool getDefaultKeyValue ( ) const

Returns the default value for all keys in the curve.
### Return value

Default value for all keys in the curve.
## void setKeyValue ( int index , bool value )

Sets the value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *bool* **value** - The boolean value of the key.

## bool getKeyValue ( int index ) const

Returns the current value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The boolean value of the key.
## void setKeyLeftTangent ( int index , const Math:: vec2 & left_tangent , float value_time_ratio = 1.0f )

Sets new coordinates for the left tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **left_tangent** - Coordinates of the left tangent at the specified key point to be set.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the opposite handle of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_ALIGNED) key is brought back in line with this one. The default value is 1.0f, which measures value and time on the same scale.

## Math:: vec2 getKeyLeftTangent ( int index ) const

Returns the current coordinates for the left tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Coordinates of the left tangent at the specified key point.
## void setKeyRightTangent ( int index , const Math:: vec2 & right_tangent , float value_time_ratio = 1.0f )

Sets new coordinates for the right tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **right_tangent** - Coordinates of the right tangent at the specified key point to be set.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the opposite handle of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_ALIGNED) key is brought back in line with this one. The default value is 1.0f, which measures value and time on the same scale.

## Math:: vec2 getKeyRightTangent ( int index ) const

Returns the current coordinates for the right tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Coordinates of the right tangent at the specified key point.
## void setTypeOfAllKeys ( AnimationCurve::KEY_TYPE type , float value_time_ratio = 1.0f )

Sets the interpolation type for all keys of the curve.
### Arguments

- *[AnimationCurve::KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_CONSTANT) values.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the handles of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_ALIGNED) key are made collinear. The default value is 1.0f, which measures value and time on the same scale.

## void clear ( )

Clears the curve removing all key points and tangents.
## bool getValueByTime ( float time )

Returns the key value at the specified key point of the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The curve value at the specified key point.
## bool getValueByNormalizedTime ( float normalized_time )

Returns the key value using the normalized time value of the key.
### Arguments

- *float* **normalized_time** - The normalized time value of the key.

### Return value

The curve value at the specified key point.
## void save ( const Ptr < Blob > & blob ) const

Saves the curve data to a blob.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **blob** - Blob to which the curve data will be saved.

## void load ( const Ptr < Blob > & blob )

Loads the curve data from the blob.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **blob** - Blob storing the curve data.
