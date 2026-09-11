# Unigine::AnimationCurveUGUID Class (CS)

**Inherits from:** AnimationCurve


This class represents an interface enabling you to create and manage animation curves containing UGUID values.


## AnimationCurveUGUID Class

### Properties

## 🔒︎ UGUID DefaultKeyValue

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

## AnimationCurveUGUID ( )

Constructor. Creates a new animation curve instance containing UGUID values.
## void AssignFrom ( AnimationCurveUGUID curve )

Copies all data (key points and tangents) from the specified source curve.
### Arguments

- *[AnimationCurveUGUID](../../../../api/library/animations/timeline/class.animationcurveuguid_cs.md)* **curve** - Source curve.

## int AddKey ( float time , UGUID value )

Adds a new key point with the specified value at the specified point of the timeline to the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **value** - The UGUID value of the key.

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
## float GetKeyTime ( int index )

Returns the current time of the key point with the specified index.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The time of the specified key point on the timeline, in seconds.
## void SetKeyValue ( int index , UGUID value )

Sets the value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **value** - The UGUID value of the key.

## UGUID GetKeyValue ( int index )

Returns the current value for the specified key on the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

The UGUID value of the key.
## void Clear ( )

Clears the curve removing all key points and tangents.
## UGUID GetValueByTime ( float time )

Returns the key value at the specified key point of the curve.
### Arguments

- *float* **time** - Time of the key on the timeline, in seconds.

### Return value

The UGUID value of the key.
## UGUID GetValueByNormalizedTime ( float time )

Returns the key value using the normalized time value of the key.
### Arguments

- *float* **time** - The normalized time value of the key.

### Return value

The UGUID value of the key.
## void Save ( Blob blob )

Saves the curve data to a blob.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob to which the curve data will be saved.

## void Load ( Blob blob )

Loads the curve data from the blob.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob storing the curve data.
