# Unigine::Plugins::SpiderVision::CalibrationGridData Class (CS)


[Calibration Grid](../../../../principles/render/output/multi_monitor/spidervision_plugin/calibration.md) stores the data on the calibration grid adjustments of the current configuration.


Calibration grid is in fact a grid of a certain shape (sphere or box) with a specified distance between the lines of this grid. The grid helps aligning the images rendered by projectors to obtain a seamless image.


> **Notice:** The calibration grid data are **not** stored in the configuration file.


This object is accessible via the corresponding method of the [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cs.md#getCalibrationGrid_CalibrationGridData) class.


## CalibrationGridData Class

### Enums

## CALIBRATION_GRID_TYPE

| Name | Description |
|---|---|
| **SPHERE** = 0 | Sperical calibration grid. |
| **BOX** = 1 | Box-type calibration grid. |
| **COLOR** = 2 | Color-filled calibration grid. |

### Properties

## bool Visible

The value indicating if the calibration grid is rendered.
## float Distance

The distance from the viewpoint to the grid. The difference is noticeable with the Box type of calibration pattern.
## CalibrationGridData.CALIBRATION_GRID_TYPE Type

The type of the calibration pattern.
## bool SphereCut

The value indicating if the Sphere Cut option is enabled for the sperical calibration grid. This option allows hiding the top and bottom poles.
## float LinesVerticalStep

The distance between major vertical lines.
## float LinesHorizontalStep

The distance between major horizontal lines.
## int LinesVerticalMinorCount

The number of secondary lines between the two neighboring major vertical lines.
## int LinesHorizontalMinorCount

The number of secondary lines between the two neighboring major horizontal lines.
## bool TextEnabled

The value indicating if text on the calibration grid is rendered.
## int TextFontSize

The size of the text displayed on the calibration grid.
## bool LineHighlightEnabled

The highlighting of one horizontal and one vertical line.
## int LineHighlightHorizontalIndex

The index of the horizontal highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
## int LineHighlightVerticalIndex

The index of the vertical highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
## float TransformYaw

The grid transform along the vertical axis. Only the grid is transformed, the projected image is not transformed.
## float TransformPitch

The grid transform along the transverse axis. Only the grid is transformed, the projected image is not transformed.
## float TransformRoll

The grid transform along the longitudinal axis. Only the grid is transformed, the projected image is not transformed.
## 🔒︎ Event EventChanged

The event triggered on changing calibration grid data. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

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
CalibrationGridData.EventChanged.Connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
CalibrationGridData.EventChanged.Connect(changed_event_connections, () => {
		Log.Message("Handling Changed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
changed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Changed event with a handler function
CalibrationGridData.EventChanged.Connect(changed_event_handler);

// remove subscription to the Changed event later by the handler function
CalibrationGridData.EventChanged.Disconnect(changed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection changed_event_connection;

// subscribe to the Changed event with a lambda handler function and keeping the connection
changed_event_connection = CalibrationGridData.EventChanged.Connect(() => {
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
CalibrationGridData.EventChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
CalibrationGridData.EventChanged.Enabled = true;

```

</details>

## vec4 BackgroundColor

The background color of the calibration grid.
## vec4 HighlightedColor

The color of the highlighted line.
## vec4 HorizontalMinorLinesColor

The color of the minor horizontal lines in the calibration grid.
## vec4 HorizontalMajorLinesColor

The color of the major horizontal lines in the calibration grid.
## vec4 VerticalMinorLinesColor

The color of the minor vertical lines in the calibration grid.
## vec4 VerticalMajorLinesColor

The color of the major vertical lines in the calibration grid.
## vec4 AxesColor

The color of the central axes in the calibration grid.
## vec4 TextColor

The color of the text in the calibration grid.
### Members

---

## void Save ( Stream stream )

Saves the calibration grid data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the calibration grid data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.
