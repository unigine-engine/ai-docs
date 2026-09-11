# Curve2d Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents an interface enabling you to [create and manage 2D curves](../../../editor2/curve_editor/index.md). These curves are used, for example, to control behavior of various parameters of particle systems (how they change over time).


## Curve2d Class

### Members

## getHash () const

Returns the current hash value calculated for the curve. Hash value is used for performance optimization and helps define if the curve really needs to be updated, or nothing has changed in its parameters (repeat mode, key points, and tangents are all the same).
### Return value

Current hash value calculated for the curve.
## getNumKeys () const

Returns the current total number of key points in the curve.
### Return value

Current total number of key points in the curve.
## void setRepeatModeStart ( )

Sets a new repeat mode for the beginning of the curve (defines behavior before the first key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values. This mode shall be used for repeating the sequence defined by the key points of the curve (tiling curves).
### Arguments

- **start** - The repeat mode for the beginning of the curve (defines behavior before the first key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values.

## getRepeatModeStart () const

Returns the current repeat mode for the beginning of the curve (defines behavior before the first key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values. This mode shall be used for repeating the sequence defined by the key points of the curve (tiling curves).
### Return value

Current repeat mode for the beginning of the curve (defines behavior before the first key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values.
## void setRepeatModeEnd ( )

Sets a new repeat mode for the end of the curve (defines behavior after the last key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values. This mode shall be used for repeating the sequence defined by the key points of the curve (tiling curves).
### Arguments

- **end** - The repeat mode for the end of the curve (defines behavior after the last key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values.

## getRepeatModeEnd () const

Returns the current repeat mode for the end of the curve (defines behavior after the last key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values. This mode shall be used for repeating the sequence defined by the key points of the curve (tiling curves).
### Return value

Current repeat mode for the end of the curve (defines behavior after the last key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values.
## getEventChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## Curve2d ( )

Constructor. Creates a new 2d curve instance.
## void clear ( )

Clears the curve removing all key points and tangents.
## void copy ( const Curve2d curve )

Copies all the data (all key points and tangents) from the specified source curve.
### Arguments

- *const [Curve2d](../../../api/library/common/class.curve2d_usc.md)* **curve** - Source curve.

## int addKey ( const vec2 & point )

Adds a new key point with the specified coordinates to the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *const vec2 &* **point** - Coordinates of the new key point to be added.

### Return value

Number of the added key point.
## int addKey ( const vec2 & point , const vec2 & left_tangent , const vec2 & right_tangent )

Adds a new key point with the specified coordinates and tangents to the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *const vec2 &* **point** - Coordinates of the new key point to be added.
- *const vec2 &* **left_tangent** - Coordinates of the left tangent at the key point.
- *const vec2 &* **right_tangent** - Coordinates of the right tangent at the key point.

### Return value

Number of the added key point.
## void removeKey ( int index )

Removes the key point with the specified number from the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

## int moveKey ( int index , const vec2 & point )

Moves the key point with the specified number to a new position (preserving the tangents). Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered. The index of key point will be updated automatically. This method can be used to implement dragging of keys on the curve. In case of moving multiple keys it is recommended to use the [*setKeyPoint()*](#setKeyPoint_int_vec2_void) method to set new values for keys and then sort them all at once via the [*sortKeys()*](#sortKeys_void) method to save performance.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const vec2 &* **point** - New coordinates of the key point.

### Return value

New index of the key.
## void sortKeys ( )

Sorts all key points ov the curve by time (X axis) in the ascending order. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
## void setKeyPoint ( int index , const vec2 & point )

Sets new coordinates for the specified key point (tangents are unaffected). Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered. This method unlike the [*moveKey()*](#moveKey_int_vec2_int) does not update the index of the key point automatically. It can be used to implement dragging of multiple keys to set new values for them along with subsequent sorting all keys at once via the [*sortKeys()*](#sortKeys_void) method to save performance.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const vec2 &* **point** - New coordinates to be set for the specified point.

## void setKeyLeftTangent ( int index , const vec2 & point )

Sets new coordinates for the left tangent at the specified key point of the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const vec2 &* **point** - New coordinates of the left tangent at the specified key point to be set.

## void setKeyRightTangent ( int index , const vec2 & point )

Sets new coordinates for the right tangent at the specified key point of the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const vec2 &* **point** - New coordinates of the right tangent at the specified key point to be set.

## vec2 getKeyPoint ( int index )

Returns the coordinates of the key point with the specified number.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Current coordinates of the specified key point.
## vec2 getKeyLeftTangent ( int index )

Returns the current coordinates for the left tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Current coordinates of the left tangent at the specified key point.
## vec2 getKeyRightTangent ( int index )

Returns the current coordinates for the right tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Current coordinates of the right tangent at the specified key point.
## int saveState ( Stream stream )


Saves data of the curve to a binary stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int)* methods:


```cpp
// initialize a node and set its state
Curve2d curve = new Curve2d();
curve.addKey(vec2(1, 0));
curve.addKey(vec2(2, 1));
curve.addKey(vec2(4, 3));

// save state
Blob blob_state = new Blob();
curve.saveState(blob_state);

// change state
curve.removeKey(1);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
curve.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which the curve data will be saved.

### Return value

**1** if the curve data is saved successfully; otherwise, **0**.
## int restoreState ( Stream stream )


Restores curve data from a binary stream.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```cpp
// initialize a node and set its state
Curve2d curve = new Curve2d();
curve.addKey(vec2(1, 0));
curve.addKey(vec2(2, 1));
curve.addKey(vec2(4, 3));

// save state
Blob blob_state = new Blob();
curve.saveState(blob_state);

// change state
curve.removeKey(1);

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
curve.restoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream in which the saved curve parameter data is stored.

### Return value

**1** if the curve data is restored successfully; otherwise, **0**.
## int save ( Xml xml )

Saves data of the curve to the specified instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../api/library/common/class.xml_usc.md) instance to which the curve data will be saved.

### Return value

**1** if the curve data is successfully saved to the specified Xml class instance; otherwise, **0**.
## int load ( Xml xml )

Loads curve data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - [Xml class](../../../api/library/common/class.xml_usc.md) instance in which the curve data is stored.

### Return value

**1** if the curve data is successfully loaded from the specified Xml class instance; otherwise, **0**.
## float evaluate ( float time )

Returns the evaluated value of the curve at the specified point in time.
### Arguments

- *float* **time** - The time within the curve you want to evaluate (horizontal axis in the curve graph).

### Return value

The value of the curve, at the specified point in time.
