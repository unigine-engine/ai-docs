# Unigine::AnimationCurveFloat Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationCurve


This class represents an interface enabling you to create and manage animation curves containing floating point precision values.


## AnimationCurveFloat Class

### Members

## float getDefaultKeyValue () const

Returns the current default value of all keys in the curve.
### Return value

Current default value of all keys in the curve.
## getNumKeys () const

Returns the current total number of key points in the curve.
### Return value

Current total number of key points in the curve.
## getMinTime () const

Returns the current point of the whole animation timeline where this curve starts being applied, in units.
### Return value

Current point of the whole animation timeline where this curve starts being applied, in units.
## getMaxTime () const

Returns the current point of the whole animation timeline up to which this curve is applied, in units.
### Return value

Current point of the whole animation timeline up to which this curve is applied, in units.
---

## AnimationCurveFloat ( )

Constructor. Creates a new animation curve instance containing floating point precision values.
## void copy ( AnimationCurveFloat curve )

Copies all data (key points and tangents) from the specified source curve.
### Arguments

- *[AnimationCurveFloat](../../../../api/library/animations/timeline/class.animationcurvefloat_usc.md)* **curve** - Source curve.

## int addKey ( float time , float value )

Adds a new key point with the specified value at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *float* **value** - The float value of the key.

### Return value

Index of the added key point.
## int addKey ( float time , float value , int type )

Adds a new key point with the specified value and type at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *float* **value** - The float value of the key.
- *int* **type** - Interpolation type set for the key, one of the [ANIMATION_CURVE_KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_usc.md#KEY_TYPE_CONSTANT) values.

### Return value

Index of the added key point.
## int addKey ( float time , float value , int type , vec2 left_tangent , vec2 right_tangent )

Adds a new key point with the specified value, type and tangents at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *float* **value** - The float value of the key.
- *int* **type** - Interpolation type set for the key, one of the [ANIMATION_CURVE_KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_usc.md#KEY_TYPE_CONSTANT) values.
- *vec2* **left_tangent** - Coordinates of the left tangent at the key point.
- *vec2* **right_tangent** - Coordinates of the right tangent at the key point.

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
## void setKeyType ( int index , int type )

Sets the interpolation type for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *int* **type** - Interpolation type set for the key, one of the [ANIMATION_CURVE_KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_usc.md#KEY_TYPE_CONSTANT) values.

## int getKeyType ( int index )

Returns the interpolation type of the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Interpolation type set for the key, one of the [ANIMATION_CURVE_KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_usc.md#KEY_TYPE_CONSTANT) values.
## float getKeyTime ( int index )

Returns the current time of the key point with the specified index.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The time of the specified key point on the timeline, in seconds.
## void setKeyValue ( int index , float value )

Sets the value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *float* **value** - The float value of the key.

## float getKeyValue ( int index )

Returns the current value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The float value of the key.
## void setKeyLeftTangent ( int index , vec2 left_tangent )

Sets new coordinates for the left tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *vec2* **left_tangent** - Coordinates of the left tangent at the specified key point to be set.

## vec2 getKeyLeftTangent ( int index )

Returns the current coordinates for the left tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Coordinates of the left tangent at the specified key point to be set.
## void setKeyRightTangent ( int index , vec2 right_tangent )

Sets new coordinates for the right tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *vec2* **right_tangent** - Coordinates of the right tangent at the specified key point to be set.

## vec2 getKeyRightTangent ( int index )

Returns the current coordinates for the right tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Coordinates of the right tangent at the specified key point to be set.
## void setTypeOfAllKeys ( int type )

Sets the interpolation type for all keys of the curve.
### Arguments

- *int* **type** - Interpolation type set for the key, one of the [ANIMATION_CURVE_KEY_TYPE_*](../../../../api/library/animations/timeline/class.animationcurve_usc.md#KEY_TYPE_CONSTANT) values.

## void clear ( )

Clears the curve removing all key points and tangents.
## float getValueByTime ( float time )

Returns the key value at the specified key point of the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The float value of the key.
## float getValueByNormalizedTime ( float normalized_time )

Returns the key value using the normalized time value of the key.
### Arguments

- *float* **normalized_time** - The normalized time value of the key.

### Return value

The float value of the key.
## void save ( Blob blob )

Saves the curve data to a blob.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_usc.md)* **blob** - Blob to which the curve data will be saved.

## void load ( const Blob blob )

Loads the curve data from the blob.
### Arguments

- *const [Blob](../../../../api/library/common/class.blob_usc.md)* **blob** - Blob storing the curve data.
