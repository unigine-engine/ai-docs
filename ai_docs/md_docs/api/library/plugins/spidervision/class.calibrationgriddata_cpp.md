# Unigine::Plugins::SpiderVision::CalibrationGridData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


[Calibration Grid](../../../../principles/render/output/multi_monitor/spidervision_plugin/calibration.md) stores the data on the calibration grid adjustments of the current configuration.


Calibration grid is in fact a grid of a certain shape (sphere or box) with a specified distance between the lines of this grid. The grid helps aligning the images rendered by projectors to obtain a seamless image.


> **Notice:** The calibration grid data are **not** stored in the configuration file.


This object is accessible via the corresponding method of the [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cpp.md#getCalibrationGrid_CalibrationGridData) class.


## CalibrationGridData Class

### Enums

## CALIBRATION_GRID_TYPE

| Name | Description |
|---|---|
| **CALIBRATION_GRID_TYPE_SPHERE** = 0 | Sperical calibration grid. |
| **CALIBRATION_GRID_TYPE_BOX** = 1 | Box-type calibration grid. |
| **CALIBRATION_GRID_TYPE_COLOR** = 2 | Color-filled calibration grid. |

### Members

## void setVisible ( bool visible )

Sets a new value indicating if the calibration grid is rendered.
### Arguments

- *bool* **visible** - Set **true** to enable rendering of the calibration grid; **false** - to disable it.

## bool isVisible () const

Returns the current value indicating if the calibration grid is rendered.
### Return value

**true** if rendering of the calibration grid is enabled ; otherwise **false**.
## void setDistance ( float distance )

Sets a new distance from the viewpoint to the grid. The difference is noticeable with the Box type of calibration pattern.
### Arguments

- *float* **distance** - The distance from the viewpoint to the grid.

## float getDistance () const

Returns the current distance from the viewpoint to the grid. The difference is noticeable with the Box type of calibration pattern.
### Return value

Current distance from the viewpoint to the grid.
## void setType ( CalibrationGridData::CALIBRATION_GRID_TYPE type )

Sets a new type of the calibration pattern.
### Arguments

- *[CalibrationGridData::CALIBRATION_GRID_TYPE](../../../../api/library/plugins/spidervision/class.calibrationgriddata_cpp.md#CALIBRATION_GRID_TYPE)* **type** - The type of the calibration pattern.

## CalibrationGridData::CALIBRATION_GRID_TYPE getType () const

Returns the current type of the calibration pattern.
### Return value

Current type of the calibration pattern.
## void setSphereCut ( bool cut )

Sets a new value indicating if the Sphere Cut option is enabled for the sperical calibration grid. This option allows hiding the top and bottom poles.
### Arguments

- *bool* **cut** - Set **true** to enable Sphere Cut option; **false** - to disable it.

## bool isSphereCut () const

Returns the current value indicating if the Sphere Cut option is enabled for the sperical calibration grid. This option allows hiding the top and bottom poles.
### Return value

**true** if Sphere Cut option is enabled ; otherwise **false**.
## void setLinesVerticalStep ( float step )

Sets a new distance between major vertical lines.
### Arguments

- *float* **step** - The distance between major vertical lines.

## float getLinesVerticalStep () const

Returns the current distance between major vertical lines.
### Return value

Current distance between major vertical lines.
## void setLinesHorizontalStep ( float step )

Sets a new distance between major horizontal lines.
### Arguments

- *float* **step** - The distance between major horizontal lines.

## float getLinesHorizontalStep () const

Returns the current distance between major horizontal lines.
### Return value

Current distance between major horizontal lines.
## void setLinesVerticalMinorCount ( int count )

Sets a new number of secondary lines between the two neighboring major vertical lines.
### Arguments

- *int* **count** - The number of secondary lines between the two neighboring major vertical lines.

## int getLinesVerticalMinorCount () const

Returns the current number of secondary lines between the two neighboring major vertical lines.
### Return value

Current number of secondary lines between the two neighboring major vertical lines.
## void setLinesHorizontalMinorCount ( int count )

Sets a new number of secondary lines between the two neighboring major horizontal lines.
### Arguments

- *int* **count** - The number of secondary lines between the two neighboring major horizontal lines.

## int getLinesHorizontalMinorCount () const

Returns the current number of secondary lines between the two neighboring major horizontal lines.
### Return value

Current number of secondary lines between the two neighboring major horizontal lines.
## void setTextEnabled ( bool enabled )

Sets a new value indicating if text on the calibration grid is rendered.
### Arguments

- *bool* **enabled** - Set **true** to enable text rendering on the calibration grid; **false** - to disable it.

## bool isTextEnabled () const

Returns the current value indicating if text on the calibration grid is rendered.
### Return value

**true** if text rendering on the calibration grid is enabled ; otherwise **false**.
## void setTextFontSize ( int size )

Sets a new size of the text displayed on the calibration grid.
### Arguments

- *int* **size** - The size of the text displayed on the calibration grid.

## int getTextFontSize () const

Returns the current size of the text displayed on the calibration grid.
### Return value

Current size of the text displayed on the calibration grid.
## void setLineHighlightEnabled ( bool enabled )

Sets a new highlighting of one horizontal and one vertical line.
### Arguments

- *bool* **enabled** - Set **true** to enable highlighting of one horizontal and one vertical line; **false** - to disable it.

## bool isLineHighlightEnabled () const

Returns the current highlighting of one horizontal and one vertical line.
### Return value

**true** if highlighting of one horizontal and one vertical line is enabled ; otherwise **false**.
## void setLineHighlightHorizontalIndex ( int index )

Sets a new index of the horizontal highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
### Arguments

- *int* **index** - The index of the horizontal highlight.

## int getLineHighlightHorizontalIndex () const

Returns the current index of the horizontal highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
### Return value

Current index of the horizontal highlight.
## void setLineHighlightVerticalIndex ( int index )

Sets a new index of the vertical highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
### Arguments

- *int* **index** - The index of the vertical highlight.

## int getLineHighlightVerticalIndex () const

Returns the current index of the vertical highlight. Only one line can be highlighted. The line is invisible if its index is set to zero.
### Return value

Current index of the vertical highlight.
## void setTransformYaw ( float yaw )

Sets a new grid transform along the vertical axis. Only the grid is transformed, the projected image is not transformed.
### Arguments

- *float* **yaw** - The yaw angle, in degrees.

## float getTransformYaw () const

Returns the current grid transform along the vertical axis. Only the grid is transformed, the projected image is not transformed.
### Return value

Current yaw angle, in degrees.
## void setTransformPitch ( float pitch )

Sets a new grid transform along the transverse axis. Only the grid is transformed, the projected image is not transformed.
### Arguments

- *float* **pitch** - The pitch angle, in degrees.

## float getTransformPitch () const

Returns the current grid transform along the transverse axis. Only the grid is transformed, the projected image is not transformed.
### Return value

Current pitch angle, in degrees.
## void setTransformRoll ( float roll )

Sets a new grid transform along the longitudinal axis. Only the grid is transformed, the projected image is not transformed.
### Arguments

- *float* **roll** - The roll angle, in degrees.

## float getTransformRoll () const

Returns the current grid transform along the longitudinal axis. Only the grid is transformed, the projected image is not transformed.
### Return value

Current roll angle, in degrees.
## static Event<> getEventChanged () const

event triggered on changing calibration grid data. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

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
CalibrationGridData::getEventChanged().connect(changed_event_connections, changed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
CalibrationGridData::getEventChanged().connect(changed_event_connections, []() {
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
CalibrationGridData::getEventChanged().connect(changed_event_connection, changed_event_handler);

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
CalibrationGridData::getEventChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
changed_handler_id = CalibrationGridData::getEventChanged().connect(e_connections, []() {
		Log::message("\Handling Changed event (lambda).\n");
	}
);

// remove the subscription later using the ID
CalibrationGridData::getEventChanged().disconnect(changed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Changed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
CalibrationGridData::getEventChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
CalibrationGridData::getEventChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## void setBackgroundColor ( const Math:: vec4 & color )

Sets a new background color of the calibration grid.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **color** - The background color of the calibration grid.

## Math:: vec4 getBackgroundColor () const

Returns the current background color of the calibration grid.
### Return value

Current background color of the calibration grid.
## void setHighlightedColor ( const Math:: vec4 & color )

Sets a new color of the highlighted line.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **color** - The color of the highlighted line.

## Math:: vec4 getHighlightedColor () const

Returns the current color of the highlighted line.
### Return value

Current color of the highlighted line.
## void setHorizontalMinorLinesColor ( const Math:: vec4 & color )

Sets a new color of the minor horizontal lines in the calibration grid.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **color** - The color of the minor horizontal lines in the calibration grid.

## Math:: vec4 getHorizontalMinorLinesColor () const

Returns the current color of the minor horizontal lines in the calibration grid.
### Return value

Current color of the minor horizontal lines in the calibration grid.
## void setHorizontalMajorLinesColor ( const Math:: vec4 & color )

Sets a new color of the major horizontal lines in the calibration grid.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **color** - The color of the major horizontal lines in the calibration grid.

## Math:: vec4 getHorizontalMajorLinesColor () const

Returns the current color of the major horizontal lines in the calibration grid.
### Return value

Current color of the major horizontal lines in the calibration grid.
## void setVerticalMinorLinesColor ( const Math:: vec4 & color )

Sets a new color of the minor vertical lines in the calibration grid.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **color** - The color of the minor vertical lines in the calibration grid.

## Math:: vec4 getVerticalMinorLinesColor () const

Returns the current color of the minor vertical lines in the calibration grid.
### Return value

Current color of the minor vertical lines in the calibration grid.
## void setVerticalMajorLinesColor ( const Math:: vec4 & color )

Sets a new color of the major vertical lines in the calibration grid.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **color** - The color of the major vertical lines in the calibration grid.

## Math:: vec4 getVerticalMajorLinesColor () const

Returns the current color of the major vertical lines in the calibration grid.
### Return value

Current color of the major vertical lines in the calibration grid.
## void setAxesColor ( const Math:: vec4 & color )

Sets a new color of the central axes in the calibration grid.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **color** - The color of the central axes in the calibration grid.

## Math:: vec4 getAxesColor () const

Returns the current color of the central axes in the calibration grid.
### Return value

Current color of the central axes in the calibration grid.
## void setTextColor ( const Math:: vec4 & color )

Sets a new color of the text in the calibration grid.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **color** - The color of the text in the calibration grid.

## Math:: vec4 getTextColor () const

Returns the current color of the text in the calibration grid.
### Return value

Current color of the text in the calibration grid.
---

## void save ( const Ptr < Stream > & stream )

Saves the calibration grid data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the calibration grid data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.
