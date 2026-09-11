# Unigine::AnimationCurveUGUID Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationCurve


This class represents an interface enabling you to create and manage animation curves containing UGUID values.


## AnimationCurveUGUID Class

### Members

## UGUID getDefaultKeyValue () const

Returns the current default value of all keys in the curve.
### Return value

Current default value of all keys in the curve.
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

## AnimationCurveUGUID ( )

Constructor. Creates a new animation curve instance containing UGUID values.
## void assignFrom ( const Ptr < AnimationCurveUGUID > & curve )

Copies all data (key points and tangents) from the specified source curve.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationCurveUGUID](../../../../api/library/animations/timeline/class.animationcurveuguid_cpp.md)> &* **curve** - Source curve.

## int addKey ( float time , const UGUID & value )

Adds a new key point with the specified value at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **value** - The UGUID value of the key.

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
## float getKeyTime ( int index ) const

Returns the current time of the key point with the specified index.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The time of the specified key point on the timeline, in seconds.
## void setKeyValue ( int index , const UGUID & value )

Sets the value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **value** - The UGUID value of the key.

## UGUID getKeyValue ( int index ) const

Returns the current value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The UGUID value of the key.
## void clear ( )

Clears the curve removing all key points and tangents.
## UGUID getValueByTime ( float time )

Returns the key value at the specified key point of the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The UGUID value of the key.
## UGUID getValueByNormalizedTime ( float time )

Returns the key value using the normalized time value of the key.
### Arguments

- *float* **time** - The normalized time value of the key.

### Return value

The UGUID value of the key.
## void save ( const Ptr < Blob > & blob ) const

Saves the curve data to a blob.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **blob** - Blob to which the curve data will be saved.

## void load ( const Ptr < Blob > & blob )

Loads the curve data from the blob.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **blob** - Blob storing the curve data.
