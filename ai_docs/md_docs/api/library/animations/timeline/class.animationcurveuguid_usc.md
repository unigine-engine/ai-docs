# Unigine::AnimationCurveUGUID Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** AnimationCurve


This class represents an interface enabling you to create and manage animation curves containing UGUID values.


## AnimationCurveUGUID Class

### Members

## UGUID getDefaultKeyValue () const

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

## AnimationCurveUGUID ( )

Constructor. Creates a new animation curve instance containing UGUID values.
## void copy ( AnimationCurveUGUID curve )

Copies all data (key points and tangents) from the specified source curve.
### Arguments

- *[AnimationCurveUGUID](../../../../api/library/animations/timeline/class.animationcurveuguid_usc.md)* **curve** - Source curve.

## int addKey ( float time , UGUID value )

Adds a new key point with the specified value at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **value** - The UGUID value of the key.

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
## float getKeyTime ( int index )

Returns the current time of the key point with the specified index.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The time of the specified key point on the timeline, in seconds.
## void setKeyValue ( int index , UGUID value )

Sets the value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **value** - The UGUID value of the key.

## UGUID getKeyValue ( int index )

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
## void save ( Blob blob )

Saves the curve data to a blob.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_usc.md)* **blob** - Blob to which the curve data will be saved.

## void load ( const Blob blob )

Loads the curve data from the blob.
### Arguments

- *const [Blob](../../../../api/library/common/class.blob_usc.md)* **blob** - Blob storing the curve data.
