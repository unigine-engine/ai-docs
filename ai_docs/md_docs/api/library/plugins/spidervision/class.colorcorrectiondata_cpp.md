# Unigine::Plugins::SpiderVision::ColorCorrectionData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


The instance of this class stores the viewport color correction data. Color correction may be required to compensate for the difference in color rendition of different projectors.


You can also adjust the brightness of the image to make the parts of the image that are farther away from the viewer lighter and vice versa, so that the brightness of the resulting image is uniform.


The color correction data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


This object is accessible via the corresponding method of the [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#getColorCorrection_ColorCorrectionData) class.


## ColorCorrectionData Class

### Members

## void setEnabled ( bool enabled )

Sets a new value indicating if the color correction is applied.
### Arguments

- *bool* **enabled** - Set **true** to enable color correction; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the color correction is applied.
### Return value

**true** if color correction is enabled ; otherwise **false**.
## void setColorScale ( const Math:: vec4 & scale )

Sets a new color multiplier for the rendered image.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **scale** - The color multiplier

## Math:: vec4 getColorScale () const

Returns the current color multiplier for the rendered image.
### Return value

Current color multiplier
## void setColorBias ( const Math:: vec4 & bias )

Sets a new color bias for the rendered image.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **bias** - The per-channel color bias.

## Math:: vec4 getColorBias () const

Returns the current color bias for the rendered image.
### Return value

Current per-channel color bias.
## void setCornerBrightness ( const Math:: vec4 & brightness )

Sets a new brightness correction values for the corners of the rendered image.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **brightness** - The four-component vector containing brightness values, in the **[0.0f, 1.0f]** range, for the corners of the rendered image (upper left, upper right, lower left, lower right).

## Math:: vec4 getCornerBrightness () const

Returns the current brightness correction values for the corners of the rendered image.
### Return value

Current four-component vector containing brightness values, in the **[0.0f, 1.0f]** range, for the corners of the rendered image (upper left, upper right, lower left, lower right).
## static Event<> getEventChanged () const

event triggered on changing color correction data. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

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
ColorCorrectionData::getEventChanged().connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ColorCorrectionData::getEventChanged().connect(changed_event_connections, []() {
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
ColorCorrectionData::getEventChanged().connect(changed_event_connection, changed_event_handler);

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
ColorCorrectionData::getEventChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
changed_handler_id = ColorCorrectionData::getEventChanged().connect(e_connections, []() {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// remove the subscription later using the ID
ColorCorrectionData::getEventChanged().disconnect(changed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ColorCorrectionData::getEventChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ColorCorrectionData::getEventChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## void saveXml ( const Ptr < Xml > & xml )

Saves the color correction data to the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance into which the data will be saved.

## bool restoreXml ( const Ptr < Xml > & xml )

Loads the color correction data from the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void save ( const Ptr < Stream > & stream )

Saves the color correction data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the color correction data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.
