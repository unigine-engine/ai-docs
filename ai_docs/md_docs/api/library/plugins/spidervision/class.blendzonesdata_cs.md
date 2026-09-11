# Unigine::Plugins::SpiderVision::BlendZonesData Class (CS)


This class stores data on all [blend zones](../../../../principles/render/output/multi_monitor/spidervision_plugin/projection_setup.md#blend) created for the viewport and provides the interface for configuring each blend zone.


The blend zone is an arbitrary shape formed by three vertical lines so that it has two parts � one part is a mask (from blue to green line), and the other one (from green to red line) is a gradient zone.


![](../../../../principles/render/output/multi_monitor/spidervision_plugin/blend_zone.jpg)


The blend zone data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


To configure parameters of a specific blend zone of a viewport, the methods of this class are to be used. However, the instance of the *BlendZonesData* class doesn't store any information on which viewport it is assigned to � the information is stored in the *[ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#getBlendZones_BlendZonesData)* class instance.


## BlendZonesData Class

### Enums

## BLEND_POINT_ROLE

| Name | Description |
|---|---|
| **TRANSPARENT** = 0 | Point on the side of blend zone that fades out to transparent. |
| **CENTER** = 1 | Point in the center of blend zone. |
| **MASK** = 2 | Point on the side of blend zone that is masked out. |
| **NUM** = 3 | Total number of blend point types. |

### Properties

## bool Enabled

The value indicating if blend zones rendering is enabled.
## 🔒︎ int NumZones

The total number of blend zones.
## 🔒︎ Event EventChanged

The event triggered on changing blend zones data. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

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
BlendZonesData.EventChanged.Connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
BlendZonesData.EventChanged.Connect(changed_event_connections, () => {
		Log.Message("Handling Changed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Changed event with a handler function
BlendZonesData.EventChanged.Connect(changed_event_handler);

// remove subscription to the Changed event later by the handler function
BlendZonesData.EventChanged.Disconnect(changed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection changed_event_connection;

// subscribe to the Changed event with a lambda handler function and keeping the connection
changed_event_connection = BlendZonesData.EventChanged.Connect(() => {
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
BlendZonesData.EventChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
BlendZonesData.EventChanged.Enabled = true;

```

</details>

### Members

---

## int AddZone ( )

Adds a new blend zone for the viewport.
### Return value

Index of the added blend zone.
## void RemoveZone ( int index )

Removes the specified blend zone.
### Arguments

- *int* **index** - Index of the blend zone.

## void Clear ( )

Clears all blend zones.
## void ChangeZoneResolution ( int zone , int count )

Defines the number of lines between the start and the end point that help configuring the contour. This method corresponds to the *Resolution* parameter in blend zone settings in UI.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **count** - Number of lines in the area from the start to the end point of the blend zone.

## void SetZoneEnabled ( int zone , bool in_enabled )

Enables or disables the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *bool* **in_enabled** - true to enable the specified blend zone, false to disable it.

## bool IsZoneEnabled ( int zone )

Returns the value indicating if the specified blend zone is enabled.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

true if the specified blend zone is enabled, otherwise false.
## void SetZoneAlpha ( int zone , float in_alpha )

Sets the alpha value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *float* **in_alpha** - Alpha value.

## float GetZoneAlpha ( int zone )

Returns the alpha value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Alpha value.
## void SetZoneContrast ( int zone , float in_contrast )

Sets the contrast value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *float* **in_contrast** - Contrast value.

## float GetZoneContrast ( int zone )

Returns the contrast value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Contrast value.
## void SetZoneGamma ( int zone , float in_gamma )

Sets the gamma value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *float* **in_gamma** - Gamma value.

## float GetZoneGamma ( int zone )

Returns the gamma value for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Gamma value.
## void SetZoneLinked ( int zone , bool linked )

Sets the value specifying if linking of the zone is enabled. If enabled, allows adjusting Alpha, Contrast, and Gamma for two blends simultaneously for better neighboring of two viewports.
### Arguments

- *int* **zone** - Index of the blend zone.
- *bool* **linked** - true to enable linking of the zone, false to disable it.

## bool IsZoneLinked ( int zone )

Returns the value specifying if linking of the zone is enabled. If enabled, allows adjusting Alpha, Contrast, and Gamma for two blends simultaneously for better neighboring of two viewports.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

true if linking of the zone is enabled, otherwise false.
## void SetZoneLink ( int zone , ivec2 link )

Links two blendzones to configure their parameters sinchronously.
### Arguments

- *int* **zone** - Index of the blend zone.
- *ivec2* **link** - Vector containing two values:

  1. Index of the vieport the blend zone of which is to be linked
  2. Index of the blend zone in the list of blend zones of that viewport

## ivec2 GetZoneLink ( int zone )

Returns the information on the blend zone linked to this blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Vector containing two values:
1. Index of the vieport the blend zone of which is to be linked
2. Index of the blend zone in the list of blend zones of that viewport


## int AddLine ( int zone )

Adds the line to the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Index of the line.
## void RemoveLine ( int zone , int index )

Removes the specified line from the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **index** - Index of the line.

## int GetNumLines ( int zone )

Returns the total number of lines for the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Total number of lines.
## void SetLinePoint ( int zone , int line , BlendZonesData.BLEND_POINT_ROLE type , vec2 point )

Sets the point with the specified coordinates and type on the specified line of the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData.BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cs.md#BLEND_POINT_ROLE)* **type** - Type of the point.
- *vec2* **point** - Coordinates of the point.

## vec2 GetLinePoint ( int zone , int line , BlendZonesData.BLEND_POINT_ROLE type )

Returns the coordinates of the point with the specified type on the specified line of the specified blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData.BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cs.md#BLEND_POINT_ROLE)* **type** - Type of the point.

### Return value

Coordinates of the point.
## void SetLinePointHandleLeft ( int zone , int line , BlendZonesData.BLEND_POINT_ROLE type , vec2 handle_left )

Sets the coordinates of the left handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData.BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cs.md#BLEND_POINT_ROLE)* **type** - Type of the point.
- *vec2* **handle_left** - Coordinates of the handle.

## vec2 GetLinePointHandleLeft ( int zone , int line , BlendZonesData.BLEND_POINT_ROLE type )

Returns the coordinates of the left handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData.BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cs.md#BLEND_POINT_ROLE)* **type** - Type of the point.

### Return value

Coordinates of the handle.
## void SetLinePointHandleRight ( int zone , int line , BlendZonesData.BLEND_POINT_ROLE type , vec2 handle_right )

Sets the coordinates of the right handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData.BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cs.md#BLEND_POINT_ROLE)* **type** - Type of the point.
- *vec2* **handle_right** - Coordinates of the handle.

## vec2 GetLinePointHandleRight ( int zone , int line , BlendZonesData.BLEND_POINT_ROLE type )

Returns the coordinates of the right handle for the specified point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData.BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cs.md#BLEND_POINT_ROLE)* **type** - Type of the point.

### Return value

Coordinates of the handle.
## void SetLinePointSmoothType ( int zone , int line , BlendZonesData.BLEND_POINT_ROLE type , ViewportData.POINT_SMOOTH_TYPE smooth_type )

Sets the line curving behavior for the point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData.BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cs.md#BLEND_POINT_ROLE)* **type** - Type of the point.
- *[ViewportData.POINT_SMOOTH_TYPE](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md#POINT_SMOOTH_TYPE)* **smooth_type** - Type of the line curving behavior in the point.

## ViewportData.POINT_SMOOTH_TYPE GetLinePointSmoothType ( int zone , int line , BlendZonesData.BLEND_POINT_ROLE type )

Returns the line curving behavior for the point.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **line** - Index of the line.
- *[BlendZonesData.BLEND_POINT_ROLE](../../../../api/library/plugins/spidervision/class.blendzonesdata_cs.md#BLEND_POINT_ROLE)* **type** - Type of the point.

### Return value

Type of the line curving behavior in the point.
## void SetZoneName ( int zone , string name )

Sets the name for the blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.
- *string* **name** - Name of the blend zone.

## string GetZoneName ( int zone )

Returns the name of the blend zone.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Name of the blend zone.
## void SetZoneSmooth ( int zone , int value )

Sets the smooth value that defines the roundness of the blend zone edges.
### Arguments

- *int* **zone** - Index of the blend zone.
- *int* **value** - Smooth value, the number of additional points creating the Bezier spline between two blend zone points.

## int GetZoneSmooth ( int zone )

Returns the smooth value that defines the roundness of the blend zone edges.
### Arguments

- *int* **zone** - Index of the blend zone.

### Return value

Smooth value.
## void SaveXml ( Xml xml )

Saves the blend zones data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance into which the data will be saved.

## bool RestoreXml ( Xml xml )

Loads the blend zones data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void Save ( Stream stream )

Saves the blend zones data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the blend zones data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.
