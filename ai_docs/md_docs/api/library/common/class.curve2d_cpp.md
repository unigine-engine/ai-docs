# Curve2d Class (CPP)

**Header:** #include <UnigineCurve2d.h>


This class represents an interface enabling you to [create and manage 2D curves](../../../editor2/curve_editor/index.md). These curves are used, for example, to control behavior of various parameters of particle systems (how they change over time).


## Curve2d Class

### Enums

## REPEAT_MODE

Mode to be used for repeating the sequence defined by the key points of the curve (tiling curves).
| Name | Description |
|---|---|
| **REPEAT_MODE_CLAMP** = 0 | The value of the start or the end key is retained. Use this option if you don't want any changes before or after the effect created by the curve. |
| **REPEAT_MODE_LOOP** = 1 | The curve is tiled. The created effect is repeated cyclically. If the values of the first and the last key are different, the transition between the curves will be abrupt. |
| **REPEAT_MODE_PING_PONG** = 2 | Every next curve section is a reflection of the previous curve section. The created effect is repeated in the forward-and-backward manner. |
| **NUM_REPEAT_MODES** = 3 | Number of repeat modes. |

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
## Event<> getEventChanged () const

event triggered when the curve is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Changed event handler
void changed_event_handler()
{
	Log::message("\Handling Changed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections changed_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventChanged().connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventChanged().connect(changed_event_connections, []() {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection changed_event_connection;

// subscribe to the Changed event with a handler function keeping the connection
publisher->getEventChanged().connect(changed_event_connection, changed_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
changed_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
changed_event_connection.setEnabled(true);

// ...

// remove subscription to the Changed event via the connection
changed_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A Changed event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Changed event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId changed_handler_id;

// subscribe to the Changed event with a lambda handler function and keeping connection ID
changed_handler_id = publisher->getEventChanged().connect(e_connections, []() {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventChanged().disconnect(changed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## Curve2d ( )

Constructor. Creates a new 2d curve instance.
## Curve2d ( const Ptr < Curve2d > & curve )

Constructor. Initializes the curve by copying the specified source curve.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Curve2d](../../../api/library/common/class.curve2d_cpp.md)> &* **curve** - Source curve.

## void clear ( )

Clears the curve removing all key points and tangents.
## void copy ( const Ptr < Curve2d > & curve )

Copies all the data (all key points and tangents) from the specified source curve.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Curve2d](../../../api/library/common/class.curve2d_cpp.md)> &* **curve** - Source curve.

## int addKey ( const Math:: vec2 & point )

Adds a new key point with the specified coordinates to the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **point** - Coordinates of the new key point to be added.

### Return value

Number of the added key point.
## int addKey ( const Math:: vec2 & point , const Math:: vec2 & left_tangent , const Math:: vec2 & right_tangent )

Adds a new key point with the specified coordinates and tangents to the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **point** - Coordinates of the new key point to be added.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **left_tangent** - Coordinates of the left tangent at the key point.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **right_tangent** - Coordinates of the right tangent at the key point.

### Return value

Number of the added key point.
## void removeKey ( int index )

Removes the key point with the specified number from the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

## int moveKey ( int index , const Math:: vec2 & point )

Moves the key point with the specified number to a new position (preserving the tangents). Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered. The index of key point will be updated automatically. This method can be used to implement dragging of keys on the curve. In case of moving multiple keys it is recommended to use the [*setKeyPoint()*](#setKeyPoint_int_vec2_void) method to set new values for keys and then sort them all at once via the [*sortKeys()*](#sortKeys_void) method to save performance.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **point** - New coordinates of the key point.

### Return value

New index of the key.
## void sortKeys ( )

Sorts all key points ov the curve by time (X axis) in the ascending order. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
## void setKeyPoint ( int index , const Math:: vec2 & point )

Sets new coordinates for the specified key point (tangents are unaffected). Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered. This method unlike the [*moveKey()*](#moveKey_int_vec2_int) does not update the index of the key point automatically. It can be used to implement dragging of multiple keys to set new values for them along with subsequent sorting all keys at once via the [*sortKeys()*](#sortKeys_void) method to save performance.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **point** - New coordinates to be set for the specified point.

## void setKeyLeftTangent ( int index , const Math:: vec2 & point )

Sets new coordinates for the left tangent at the specified key point of the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **point** - New coordinates of the left tangent at the specified key point to be set.

## void setKeyRightTangent ( int index , const Math:: vec2 & point )

Sets new coordinates for the right tangent at the specified key point of the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **point** - New coordinates of the right tangent at the specified key point to be set.

## Math:: vec2 getKeyPoint ( int index )

Returns the coordinates of the key point with the specified number.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Current coordinates of the specified key point.
## Math:: vec2 getKeyLeftTangent ( int index )

Returns the current coordinates for the left tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Current coordinates of the left tangent at the specified key point.
## Math:: vec2 getKeyRightTangent ( int index )

Returns the current coordinates for the right tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Current coordinates of the right tangent at the specified key point.
## int saveState ( const Ptr < Stream > & stream ) const


Saves data of the curve to a binary stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int)* methods:


```cpp
// initialize a node and set its state
Curve2dPtr curve = Curve2d::create();
curve->addKey(vec2(1, 0));
curve->addKey(vec2(2, 1));
curve->addKey(vec2(4, 3));

// save state
BlobPtr blob_state = Blob::create();
curve->saveState(blob_state);

// change state
curve->removeKey(1);

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
curve->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the curve data will be saved.

### Return value

true if the curve data is saved successfully; otherwise, false.
## bool restoreState ( const Ptr < Stream > & stream )


Restores curve data from a binary stream.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```cpp
// initialize a node and set its state
Curve2dPtr curve = Curve2d::create();
curve->addKey(vec2(1, 0));
curve->addKey(vec2(2, 1));
curve->addKey(vec2(4, 3));

// save state
BlobPtr blob_state = Blob::create();
curve->saveState(blob_state);

// change state
curve->removeKey(1);

// restore state
blob_state->seekSet(0);				// returning the carriage to the start of the blob
curve->restoreState(blob_state);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream in which the saved curve parameter data is stored.

### Return value

true if the curve data is restored successfully; otherwise, false.
## bool save ( const Ptr < Json > & json ) const

Saves data of the curve to the specified instance of the Json class.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Json](../../../api/library/common/class.json_cpp.md)> &* **json** - [Json class](../../../api/library/common/class.json_cpp.md) instance to which the curve data will be saved.

### Return value

true if the curve data is successfully saved to the specified Json class instance; otherwise, false.
## bool load ( const Ptr < Json > & json )

Loads curve data from the specified instance of the Json class.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Json](../../../api/library/common/class.json_cpp.md)> &* **json** - [Json class](../../../api/library/common/class.xml_cpp.md) instance in which the curve data is stored.

### Return value

true if the curve data is successfully loaded from the specified Json class instance; otherwise, false.
## bool save ( const Ptr < Xml > & xml ) const

Saves data of the curve to the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../api/library/common/class.xml_cpp.md) instance to which the curve data will be saved.

### Return value

true if the curve data is successfully saved to the specified Xml class instance; otherwise, false.
## bool load ( const Ptr < Xml > & xml )

Loads curve data from the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../api/library/common/class.xml_cpp.md) instance in which the curve data is stored.

### Return value

true if the curve data is successfully loaded from the specified Xml class instance; otherwise, false.
## float evaluate ( float time ) const

Returns the evaluated value of the curve at the specified point in time.
### Arguments

- *float* **time** - The time within the curve you want to evaluate (horizontal axis in the curve graph).

### Return value

The value of the curve, at the specified point in time.
