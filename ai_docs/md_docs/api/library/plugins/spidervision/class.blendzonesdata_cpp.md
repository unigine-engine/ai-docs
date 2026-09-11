# Unigine::Plugins::SpiderVision::BlendZonesData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


This class stores data on all [blend zones](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#blend) created for the viewport and provides the interface for configuring each blend zone.


The blend zone is an arbitrary shape formed by three vertical lines so that it has two parts � one part is a mask (from blue to green line), and the other one (from green to red line) is a gradient zone.


![](../../../../principles/render/output/multi_monitor/spidervision_plugin/blend_zone.jpg)


The blend zone data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


To configure parameters of a specific blend zone of a viewport, the methods of this class are to be used. However, the instance of the *BlendZonesData* class doesn't store any information on which viewport it is assigned to � the information is stored in the *[ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#getBlendZones_BlendZonesData)* class instance.


## BlendZonesData Class

### Enums

## BLEND_POINT_ROLE

| Name | Description |
|---|---|
| **BLEND_POINT_ROLE_TRANSPARENT** = 0 | Point on the side of blend zone that fades out to transparent. |
| **BLEND_POINT_ROLE_CENTER** = 1 | Point in the center of blend zone. |
| **BLEND_POINT_ROLE_MASK** = 2 | Point on the side of blend zone that is masked out. |
| **BLEND_POINT_ROLE_NUM** = 3 | Total number of blend point types. |

### Members

## void setEnabled ( bool enabled )

Sets a new value indicating if blend zones rendering is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable rendering of blend zones; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if blend zones rendering is enabled.
### Return value

**true** if rendering of blend zones is enabled ; otherwise **false**.
## int getNumZones () const

Returns the current total number of blend zones.
### Return value

Current total number of blend zones.
## static Event<> getEventChanged () const

event triggered on changing blend zones data. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

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
BlendZonesData::getEventChanged().connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
BlendZonesData::getEventChanged().connect(changed_event_connections, []() {
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
BlendZonesData::getEventChanged().connect(changed_event_connection, changed_event_handler);

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
BlendZonesData::getEventChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
changed_handler_id = BlendZonesData::getEventChanged().connect(e_connections, []() {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// remove the subscription later using the ID
BlendZonesData::getEventChanged().disconnect(changed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
BlendZonesData::getEventChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
BlendZonesData::getEventChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## int addZone ( )

Adds a new blend zone for the viewport.
### Return value

Index of the added blend zone.
## void removeZone ( int index )

Removes the specified blend zone.
### Arguments

- *int* **index** - Index of the blend zone.

## void clear ( )

Clears all blend zones.
## void changeZoneResolution ( int zone , int count )

Defines the number of lines between the start and the end point that help configuring the contour. This method corresponds to the *Resolution* parameter in blend zone settings in UI.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **count** - Number of lines in the area from the start to the end point of the blend zone.

## void setZoneEnabled ( int zone , bool in_enabled )

Enables or disables the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *bool* **in_enabled** - true to enable the specified blend zone, false to disable it.

## bool isZoneEnabled ( int zone ) const

Returns the value indicating if the specified blend zone is enabled.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

true if the specified blend zone is enabled, otherwise false.
## void setZoneAlpha ( int zone , float in_alpha )

Sets the alpha value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *float* **in_alpha** - Alpha value.

## float getZoneAlpha ( int zone ) const

Returns the alpha value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Alpha value.
## void setZoneContrast ( int zone , float in_contrast )

Sets the contrast value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *float* **in_contrast** - Contrast value.

## float getZoneContrast ( int zone ) const

Returns the contrast value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Contrast value.
## void setZoneGamma ( int zone , float in_gamma )

Sets the gamma value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *float* **in_gamma** - Gamma value.

## float getZoneGamma ( int zone ) const

Returns the gamma value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Gamma value.
## void setZoneLinked ( int zone , bool linked )

Sets the value specifying if linking of the zone is enabled. If enabled, allows adjusting Alpha, Contrast, and Gamma for two blends simultaneously for better neighboring of two viewports.
### Arguments

- *int* **zone** - Index of the blend zone.
- *bool* **linked** - true to enable linking of the zone, false to disable it.

## bool isZoneLinked ( int zone ) const

Returns the value specifying if linking of the zone is enabled. If enabled, allows adjusting Alpha, Contrast, and Gamma for two blends simultaneously for better neighboring of two viewports.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

true if linking of the zone is enabled, otherwise false.
## void setZoneLink ( int zone , const Math:: ivec2 & link )

Links two blendzones to configure their parameters sinchronously.
### Arguments

- *int* **zone** - Index of the blend zone.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **link** - Vector containing two values:

  1. Index of the vieport the blend zone of which is to be linked
  2. Index of the blend zone in the list of blend zones of that viewport

## Math:: ivec2 getZoneLink ( int zone ) const

Returns the information on the blend zone linked to this blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Vector containing two values:
1. Index of the vieport the blend zone of which is to be linked
2. Index of the blend zone in the list of blend zones of that viewport


## int addLine ( int zone )

Adds the line to the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Index of the line.
## void removeLine ( int zone , int index )

Removes the specified line from the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **index** - Index of the line.

## int getNumLines ( int zone ) const

Returns the total number of lines for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Total number of lines.
## void setLinePoint ( int zone , int line , BlendZonesData::BLEND_POINT_ROLE type , const Math:: vec2 & point )

Sets the point with the specified coordinates and type on the specified line of the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData::BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cpp.md#BLEND_POINT_ROLE)* **type** - Type of the point.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **point** - Coordinates of the point.

## Math:: vec2 getLinePoint ( int zone , int line , BlendZonesData::BLEND_POINT_ROLE type ) const

Returns the coordinates of the point with the specified type on the specified line of the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData::BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cpp.md#BLEND_POINT_ROLE)* **type** - Type of the point.

### Return value

Coordinates of the point.
## void setLinePointHandleLeft ( int zone , int line , BlendZonesData::BLEND_POINT_ROLE type , const Math:: vec2 & handle_left )

Sets the coordinates of the left handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData::BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cpp.md#BLEND_POINT_ROLE)* **type** - Type of the point.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **handle_left** - Coordinates of the handle.

## Math:: vec2 getLinePointHandleLeft ( int zone , int line , BlendZonesData::BLEND_POINT_ROLE type ) const

Returns the coordinates of the left handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData::BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cpp.md#BLEND_POINT_ROLE)* **type** - Type of the point.

### Return value

Coordinates of the handle.
## void setLinePointHandleRight ( int zone , int line , BlendZonesData::BLEND_POINT_ROLE type , const Math:: vec2 & handle_right )

Sets the coordinates of the right handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData::BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cpp.md#BLEND_POINT_ROLE)* **type** - Type of the point.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **handle_right** - Coordinates of the handle.

## Math:: vec2 getLinePointHandleRight ( int zone , int line , BlendZonesData::BLEND_POINT_ROLE type ) const

Returns the coordinates of the right handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData::BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cpp.md#BLEND_POINT_ROLE)* **type** - Type of the point.

### Return value

Coordinates of the handle.
## void setLinePointSmoothType ( int zone , int line , BlendZonesData::BLEND_POINT_ROLE type , ViewportData::POINT_SMOOTH_TYPE smooth_type )

Sets the line curving behavior for the point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData::BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cpp.md#BLEND_POINT_ROLE)* **type** - Type of the point.
- *[ViewportData::POINT_SMOOTH_TYPE](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#POINT_SMOOTH_TYPE)* **smooth_type** - Type of the line curving behavior in the point.

## ViewportData::POINT_SMOOTH_TYPE getLinePointSmoothType ( int zone , int line , BlendZonesData::BLEND_POINT_ROLE type ) const

Returns the line curving behavior for the point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData::BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cpp.md#BLEND_POINT_ROLE)* **type** - Type of the point.

### Return value

Type of the line curving behavior in the point.
## void setZoneName ( int zone , const char * name )

Sets the name for the blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *const char ** **name** - Name of the blend zone.

## String getZoneName ( int zone ) const

Returns the name of the blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Name of the blend zone.
## void setZoneSmooth ( int zone , int value )

Sets the smooth value that defines the roundness of the blend zone edges.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **value** - Smooth value, the number of additional points creating the Bezier spline between two blend zone points.

## int getZoneSmooth ( int zone ) const

Returns the smooth value that defines the roundness of the blend zone edges.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Smooth value.
## void saveXml ( const Ptr < Xml > & xml )

Saves the blend zones data to the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance into which the data will be saved.

## bool restoreXml ( const Ptr < Xml > & xml )

Loads the blend zones data from the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void save ( const Ptr < Stream > & stream )

Saves the blend zones data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the blend zones data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.
