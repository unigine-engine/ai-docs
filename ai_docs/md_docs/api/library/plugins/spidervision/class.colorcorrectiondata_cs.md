# Unigine::Plugins::SpiderVision::ColorCorrectionData Class (CS)


The instance of this class stores the viewport color correction data. Color correction may be required to compensate for the difference in color rendition of different projectors.


You can also adjust the brightness of the image to make the parts of the image that are farther away from the viewer lighter and vice versa, so that the brightness of the resulting image is uniform.


The color correction data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#getColorCorrection_ColorCorrectionData) class.


## ColorCorrectionData Class

### Properties

## bool Enabled

The value indicating if the color correction is applied.
## vec4 ColorScale

The color multiplier for the rendered image.
## vec4 ColorBias

The color bias for the rendered image.
## vec4 CornerBrightness

The brightness correction values for the corners of the rendered image.
## 🔒︎ Event EventChanged

The event triggered on changing color correction data. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

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
ColorCorrectionData.EventChanged.Connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ColorCorrectionData.EventChanged.Connect(changed_event_connections, () => {
		Log.Message("Handling Changed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Changed event with a handler function
ColorCorrectionData.EventChanged.Connect(changed_event_handler);

// remove subscription to the Changed event later by the handler function
ColorCorrectionData.EventChanged.Disconnect(changed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection changed_event_connection;

// subscribe to the Changed event with a lambda handler function and keeping the connection
changed_event_connection = ColorCorrectionData.EventChanged.Connect(() => {
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
ColorCorrectionData.EventChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
ColorCorrectionData.EventChanged.Enabled = true;

```

</details>

### Members

---

## void SaveXml ( Xml xml )

Saves the color correction data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance into which the data will be saved.

## bool RestoreXml ( Xml xml )

Loads the color correction data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void Save ( Stream stream )

Saves the color correction data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the color correction data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.
