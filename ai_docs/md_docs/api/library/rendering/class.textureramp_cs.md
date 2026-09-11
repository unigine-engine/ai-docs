# Unigine.TextureRamp Class (CS)


Interface for handling ramp textures. This class lets the user store 2d curves in a form of a texture (convert vectors to raster data).


Ramp textures can be used for color variation in the [particles_base](../../../content/materials/library/particles_base/index.md) material of Particle Systems or in other custom materials.


![](texturecurve_editor.png)


You can set up to 4 channels for the ramp texture.


## TextureRamp Class

### Properties

## 🔒︎ Texture Texture

The new texture and updates hashes for curves, if required. Returns a pointer to the texture or null if the texture was not created.
## int NumChannels

The number of channels for the texture.
## int Resolution

The width resolution for the texture.
## int Flags

The texture flags.
## 🔒︎ bool IsDefaultAll

The value indicating if the values of all curve channels are the default ones which were previously set via *[DefaultCurve](../../...md#setDefaultCurve_int_Curve2d_void)*.
## 🔒︎ Event EventChanged

The event triggered on changing the ramp texture. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

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

## TextureRamp ( int num_channels , int resolution , int flags )

Sets resolution, number of channels and texture flags for this TextureRamp instance. The pointer to the ramp texture is set to null and curves are marked for an update.
### Arguments

- *int* **num_channels** - Number of texture channels.
- *int* **resolution** - Width resolution of the ramp texture.
- *int* **flags** - Texture flags.

## TextureRamp ( TextureRamp texture_ramp )

Ramp texture constructor. Creates a new ramp texture by copying a given source ramp texture.
### Arguments

- *[TextureRamp](../../../api/library/rendering/class.textureramp_cs.md)* **texture_ramp** - Pointer to a new ramp texture.

## TextureRamp ( )

## void ReleaseTexture ( )

Deletes the texture and its pointer.
## void Copy ( TextureRamp src_texture_ramp )

Copies the data of a source ramp texture to the texture.
### Arguments

- *[TextureRamp](../../../api/library/rendering/class.textureramp_cs.md)* **src_texture_ramp** - Source ramp texture.

## TextureRamp Clone ( )

Duplicates the ramp texture and returns a pointer to the copy.
## Curve2d GetCurve ( int channel )

Returns a pointer to the [Curve2d](../../../api/library/common/class.curve2d_cs.md) for the specified channel.
### Arguments

- *int* **channel** - Required channel.

### Return value

Pointer to a Curve2d object.
## void SetDefaultCurve ( Curve2d default_curve )

Resets a curve to a default one.
### Arguments

- *[Curve2d](../../../api/library/common/class.curve2d_cs.md)* **default_curve** - A curve to be used as the default one.

## void SetDefaultCurve ( int channel , Curve2d default_curve )

Resets a curve for the given channel to a default one.
### Arguments

- *int* **channel** - R, G, B, or A channel set by the corresponding value from 0 to 3.
- *[Curve2d](../../../api/library/common/class.curve2d_cs.md)* **default_curve** - A curve to be used as the default one.

## bool IsDefault ( int channel )

Returns a value indicating if the value of the given curve channel is the default one which was previously set via [setDefaultCurve](#setDefaultCurve_int_Curve2d_void).
### Arguments

- *int* **channel** - R, G, B, or A channel set by the corresponding value from 0 to 3.

### Return value

true if the curve value is the default one set via [setDefaultCurve](#setDefaultCurve_int_Curve2d_void), otherwise false.
## void Save ( Xml xml )

Saves the ramp texture data to the given [Xml](../../../api/library/common/class.xml_cs.md) node.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Target Xml node.

## void Save ( Json json )

Saves the ramp texture data to the given [Json](../../../api/library/common/class.json_cs.md) class instance.
### Arguments

- *[Json](../../../api/library/common/class.json_cs.md)* **json** - Target son class instance.

## void Load ( Xml xml )

Loads the ramp texture data from the given [Xml](../../../api/library/common/class.xml_cs.md) node.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Source Xml node containing ramp texture data.

## void Load ( Json json )

Loads the ramp texture data from the given [Json](../../../api/library/common/class.json_cs.md) class instance.
### Arguments

- *[Json](../../../api/library/common/class.json_cs.md)* **json** - Source Json class instance containing ramp texture data.

## void SaveState ( Stream stream )

Saves the state of the ramp texture into a binary stream.


**Example** using *SaveState()* and *[RestoreState()](#restoreState_Stream_void)* methods:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
ramp.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
ramp.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - The stream to save the ramp texture state data.

## void RestoreState ( Stream stream )


Restores the state of the ramp texture from the binary stream.


**Example** using *[SaveState()](#saveState_Stream_void)* and *RestoreState()* methods:


```csharp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
ramp.SaveState(blob_state);

// change the node state
//...//

// restore state
blob_state.SeekSet(0);	// returning the carriage to the start of the blob
ramp.RestoreState(blob_state);

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - The stream that stores the ramp texture state data.
