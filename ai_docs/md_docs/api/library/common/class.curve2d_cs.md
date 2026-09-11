# Curve2d Class (CS)


This class represents an interface enabling you to [create and manage 2D curves](../../../editor2/curve_editor/index.md). These curves are used, for example, to control behavior of various parameters of particle systems (how they change over time).


## Curve2d Class

### Enums

## REPEAT_MODE

Mode to be used for repeating the sequence defined by the key points of the curve (tiling curves).
| Name | Description |
|---|---|
| **CLAMP** = 0 | The value of the start or the end key is retained. Use this option if you don't want any changes before or after the effect created by the curve. |
| **LOOP** = 1 | The curve is tiled. The created effect is repeated cyclically. If the values of the first and the last key are different, the transition between the curves will be abrupt. |
| **PING_PONG** = 2 | Every next curve section is a reflection of the previous curve section. The created effect is repeated in the forward-and-backward manner. |
| **NUM_REPEAT_MODES** = 3 | Number of repeat modes. |

### Properties

## 🔒︎ int Hash

The hash value calculated for the curve. Hash value is used for performance optimization and helps define if the curve really needs to be updated, or nothing has changed in its parameters (repeat mode, key points, and tangents are all the same).
## 🔒︎ int NumKeys

The total number of key points in the curve.
## Curve2d.REPEAT_MODE RepeatModeStart

The repeat mode for the beginning of the curve (defines behavior before the first key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values. This mode shall be used for repeating the sequence defined by the key points of the curve (tiling curves).
## Curve2d.REPEAT_MODE RepeatModeEnd

The repeat mode for the end of the curve (defines behavior after the last key point), one of the [*REPEAT_MODE_**](#REPEAT_MODE) values. This mode shall be used for repeating the sequence defined by the key points of the curve (tiling curves).
## 🔒︎ Event EventChanged

The event triggered when the curve is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Changed event handler
void changed_event_handler()
{
	Log.Message("\Handling Changed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections changed_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventChanged.Connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventChanged.Connect(changed_event_connections, () => {
		Log.Message("Handling Changed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Changed event with a handler function
publisher.EventChanged.Connect(changed_event_handler);

// remove subscription to the Changed event later by the handler function
publisher.EventChanged.Disconnect(changed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection changed_event_connection;

// subscribe to the Changed event with a lambda handler function and keeping the connection
changed_event_connection = publisher.EventChanged.Connect(() => {
		Log.Message("Handling Changed event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
changed_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
changed_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
changed_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventChanged.Enabled = true;

```

</details>

### Members

---

## Curve2d ( )

Constructor. Creates a new 2d curve instance.
## Curve2d ( Curve2d curve )

Constructor. Initializes the curve by copying the specified source curve.
### Arguments

- *[Curve2d](../../../api/library/common/class.curve2d_cs.md)* **curve** - Source curve.

## void Clear ( )

Clears the curve removing all key points and tangents.
## void Copy ( Curve2d curve )

Copies all the data (all key points and tangents) from the specified source curve.
### Arguments

- *[Curve2d](../../../api/library/common/class.curve2d_cs.md)* **curve** - Source curve.

## int AddKey ( vec2 point )

Adds a new key point with the specified coordinates to the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *vec2* **point** - Coordinates of the new key point to be added.

### Return value

Number of the added key point.
## int AddKey ( vec2 point , vec2 left_tangent , vec2 right_tangent )

Adds a new key point with the specified coordinates and tangents to the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *vec2* **point** - Coordinates of the new key point to be added.
- *vec2* **left_tangent** - Coordinates of the left tangent at the key point.
- *vec2* **right_tangent** - Coordinates of the right tangent at the key point.

### Return value

Number of the added key point.
## void RemoveKey ( int index )

Removes the key point with the specified number from the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

## int MoveKey ( int index , vec2 point )

Moves the key point with the specified number to a new position (preserving the tangents). Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered. The index of key point will be updated automatically. This method can be used to implement dragging of keys on the curve. In case of moving multiple keys it is recommended to use the [*setKeyPoint()*](#setKeyPoint_int_vec2_void) method to set new values for keys and then sort them all at once via the [*sortKeys()*](#sortKeys_void) method to save performance.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *vec2* **point** - New coordinates of the key point.

### Return value

New index of the key.
## void SortKeys ( )

Sorts all key points ov the curve by time (X axis) in the ascending order. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
## void SetKeyPoint ( int index , vec2 point )

Sets new coordinates for the specified key point (tangents are unaffected). Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered. This method unlike the [*moveKey()*](#moveKey_int_vec2_int) does not update the index of the key point automatically. It can be used to implement dragging of multiple keys to set new values for them along with subsequent sorting all keys at once via the [*sortKeys()*](#sortKeys_void) method to save performance.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *vec2* **point** - New coordinates to be set for the specified point.

## void SetKeyLeftTangent ( int index , vec2 point )

Sets new coordinates for the left tangent at the specified key point of the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *vec2* **point** - New coordinates of the left tangent at the specified key point to be set.

## void SetKeyRightTangent ( int index , vec2 point )

Sets new coordinates for the right tangent at the specified key point of the curve. Upon completion on this operation the [*CHANGED*](#getEventChanged_Event) event is triggered.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.
- *vec2* **point** - New coordinates of the right tangent at the specified key point to be set.

## vec2 GetKeyPoint ( int index )

Returns the coordinates of the key point with the specified number.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Current coordinates of the specified key point.
## vec2 GetKeyLeftTangent ( int index )

Returns the current coordinates for the left tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Current coordinates of the left tangent at the specified key point.
## vec2 GetKeyRightTangent ( int index )

Returns the current coordinates for the right tangent at the specified key point of the curve.
### Arguments

- *int* **index** - Key point number, in the range from 0 to the [total number of key points](#getNumKeys_int) in the curve.

### Return value

Current coordinates of the right tangent at the specified key point.
## bool SaveState ( Stream stream )


Saves data of the curve to a binary stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_int)* methods:


```csharp
// initialize a node and set its state
Curve2d curve = new Curve2d();
curve.AddKey(new vec2(1, 0));
curve.AddKey(new vec2(2, 1));
curve.AddKey(new vec2(4, 3));

// save state
Blob blob_state = new Blob();
curve.SaveState(blob_state);

// change the node state
curve.RemoveKey(1);

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
curve.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the curve data will be saved.

### Return value

true if the curve data is saved successfully; otherwise, false.
## bool RestoreState ( Stream stream )


Restores curve data from a binary stream.


**Example** using *[saveState()](#saveState_Stream_int)* and *restoreState()* methods:


```csharp
// initialize a node and set its state
Curve2d curve = new Curve2d();
curve.AddKey(new vec2(1, 0));
curve.AddKey(new vec2(2, 1));
curve.AddKey(new vec2(4, 3));

// save state
Blob blob_state = new Blob();
curve.SaveState(blob_state);

// change the node state
curve.RemoveKey(1);

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
curve.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream in which the saved curve parameter data is stored.

### Return value

true if the curve data is restored successfully; otherwise, false.
## bool Save ( Json json )

Saves data of the curve to the specified instance of the Json class.
### Arguments

- *[Json](../../../api/library/common/class.json_cs.md)* **json** - [Json class](../../../api/library/common/class.json_cs.md) instance to which the curve data will be saved.

### Return value

true if the curve data is successfully saved to the specified Json class instance; otherwise, false.
## bool Load ( Json json )

Loads curve data from the specified instance of the Json class.
### Arguments

- *[Json](../../../api/library/common/class.json_cs.md)* **json** - [Json class](../../../api/library/common/class.xml_cs.md) instance in which the curve data is stored.

### Return value

true if the curve data is successfully loaded from the specified Json class instance; otherwise, false.
## bool Save ( Xml xml )

Saves data of the curve to the specified instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../api/library/common/class.xml_cs.md) instance to which the curve data will be saved.

### Return value

true if the curve data is successfully saved to the specified Xml class instance; otherwise, false.
## bool Load ( Xml xml )

Loads curve data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../api/library/common/class.xml_cs.md) instance in which the curve data is stored.

### Return value

true if the curve data is successfully loaded from the specified Xml class instance; otherwise, false.
## float Evaluate ( float time )

Returns the evaluated value of the curve at the specified point in time.
### Arguments

- *float* **time** - The time within the curve you want to evaluate (horizontal axis in the curve graph).

### Return value

The value of the curve, at the specified point in time.
