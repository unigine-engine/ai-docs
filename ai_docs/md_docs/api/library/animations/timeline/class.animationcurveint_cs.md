# Unigine::AnimationCurveInt Class (CS)

**Inherits from:** AnimationCurve


This class represents an interface enabling you to create and manage animation curves containing integer values.


## AnimationCurveInt Class

### Properties

## 🔒︎ int DefaultKeyValue

The default value of all keys in the curve.
## 🔒︎ int NumKeys

The total number of key points in the curve.
## 🔒︎ float MinTime

The point of the whole animation timeline where this curve starts being applied, in units.
## 🔒︎ float MaxTime

The point of the whole animation timeline up to which this curve is applied, in units.
## AnimationCurve.EXTRAPOLATION PreInfinity

The way the curve behaves before its first key.
## AnimationCurve.EXTRAPOLATION PostInfinity

The way the curve behaves after its last key.
### Members

---

## AnimationCurveInt ( )

Constructor. Creates a new animation curve instance containing integer values.
## void AssignFrom ( AnimationCurveInt curve )

Copies all data (key points and tangents) from the specified source curve.
### Arguments

- *[AnimationCurveInt](../../../../api/library/animations/timeline/class.animationcurveint_cs.md)* **curve** - Source curve.

## int AddKey ( float time , int value )

Adds a new key point with the specified value at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *int* **value** - The integer value of the key.

### Return value

Index of the added key point.
## int AddKey ( float time , int value , AnimationCurve.KEY_TYPE type )

Adds a new key point with the specified value and type at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *int* **value** - The integer value of the key.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE) values.

### Return value

Index of the added key point.
## int AddKey ( float time , int value , AnimationCurve.KEY_TYPE type , vec2 left_tangent , vec2 right_tangent )

Adds a new key point with the specified value, type and tangents at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *int* **value** - The integer value of the key.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE) values.
- *vec2* **left_tangent** - Coordinates of the left tangent at the key point.
- *vec2* **right_tangent** - Coordinates of the right tangent at the key point.

### Return value

Index of the added key point.
## void RemoveKey ( int index )

Removes the key point with the specified index from the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

## int MoveKey ( int index , float new_time )

Moves the key point with the specified number to a new time position (preserving the tangents). The index of key point will be updated automatically. This method can be used to implement dragging of keys on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *float* **new_time** - Time of the key on the timeline, in seconds.

### Return value

New index of the key.
## void SetKeyType ( int index , AnimationCurve.KEY_TYPE type , float value_time_ratio = 1.0f )

Sets the interpolation type for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE) values.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the handles of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_ALIGNED) key are made collinear. The default value is 1.0f, which measures value and time on the same scale.

## AnimationCurve.KEY_TYPE GetKeyType ( int index )

Returns the interpolation type of the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Interpolation type set for the key, one of the [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE) values.
## float GetKeyTime ( int index )

Returns the current time of the key point with the specified index.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The time of the specified key point on the timeline, in seconds.
## void SetKeyValue ( int index , int value )

Sets the value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *int* **value** - The integer value of the key.

## int GetKeyValue ( int index )

Returns the current value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The integer value of the key.
## void SetKeyLeftTangent ( int index , vec2 left_tangent , float value_time_ratio = 1.0f )

Sets new coordinates for the left tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *vec2* **left_tangent** - Coordinates of the left tangent at the specified key point to be set.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the opposite handle of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_ALIGNED) key is brought back in line with this one. The default value is 1.0f, which measures value and time on the same scale.

## vec2 GetKeyLeftTangent ( int index )

Returns the current coordinates for the left tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Coordinates of the left tangent at the specified key point to be set.
## void SetKeyRightTangent ( int index , vec2 right_tangent , float value_time_ratio = 1.0f )

Sets new coordinates for the right tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *vec2* **right_tangent** - Coordinates of the right tangent at the specified key point to be set.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the opposite handle of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_ALIGNED) key is brought back in line with this one. The default value is 1.0f, which measures value and time on the same scale.

## vec2 GetKeyRightTangent ( int index )

Returns the current coordinates for the right tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Coordinates of the right tangent at the specified key point to be set.
## void SetTypeOfAllKeys ( AnimationCurve.KEY_TYPE type , float value_time_ratio = 1.0f )

Sets the interpolation type for all keys of the curve.
### Arguments

- *[AnimationCurve.KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE)* **type** - Interpolation type set for the key, one of the [KEY_TYPE](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE) values.
- *float* **value_time_ratio** - Number of units of value that make up one unit of time, taken into account when the handles of an [aligned](../../../../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_ALIGNED) key are made collinear. The default value is 1.0f, which measures value and time on the same scale.

## void Clear ( )

Clears the curve removing all key points and tangents.
## int GetValueByTime ( float time )

Returns the key value at the specified key point of the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The integer value of the key.
## int GetValueByNormalizedTime ( float normalized_time )

Returns the key value using the normalized time value of the key.
### Arguments

- *float* **normalized_time** - The normalized time value of the key.

### Return value

The integer value of the key.
## void Save ( Blob blob )

Saves the curve data to a blob.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob to which the curve data will be saved.

## void Load ( Blob blob )

Loads the curve data from the blob.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob storing the curve data.
