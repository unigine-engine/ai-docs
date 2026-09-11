# Unigine::Plugins::SpiderVision::ViewportData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


The object of this class stores all data on the viewport: transformations, viewport type settings, physical size of the display, VFOV, aspect, vertical and horizontal offsets, warping effect details, etc.


This object is accessible via the corresponding methods of the [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cpp.md#getViewportByIndex_int_ViewportData) class.


The mask data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## ViewportData Class

### Enums

## WINDOW_MODE

| Name | Description |
|---|---|
| **WINDOW_MODE_WINDOWED** = 0 | Window mode. |
| **WINDOW_MODE_BORDERLESS_WINDOWED** = 1 | Borderless OS window with the configurable size. |
| **WINDOW_MODE_EXCLUSIVE_FULLSCREEN** = 2 | Fullscreen window that occupies the entire display, while all other engine windows are minimized. Interaction with other engine windows is not possible. If focus is switched to another application window, the Fullscreen window is minimized automatically by the OS. |

## POINT_SMOOTH_TYPE

| Name | Description |
|---|---|
| **POINT_SMOOTH_TYPE_LINEAR** = 0 | Linear interpolation is applied for curving of the line on both sides of the point. |
| **POINT_SMOOTH_TYPE_SMOOTH** = 1 | Symmetric control handles for smooth curves on both sides of the point. |
| **POINT_SMOOTH_TYPE_BREAK** = 2 | Asymmetric control handles for an independent control of each handle. |
| **POINT_SMOOTH_TYPE_AUTO** = 3 | Automatic smooth line curving, no control handles available. |
| **POINT_SMOOTH_TYPE_NUM** = 4 | Total number of line curving modes. |

## DISPLAY_TRANSFORM_TYPE

| Name | Description |
|---|---|
| **DISPLAY_TRANSFORM_TYPE_DISPLAY** = 0 | Display viewport. |
| **DISPLAY_TRANSFORM_TYPE_PROJECTOR** = 1 | Projector (beamer) viewport. |

## RENDER_MODE

Rendering mode of the viewport: a single image or a side-by-side stereo pair.
| Name | Description |
|---|---|
| **RENDER_MODE_MONO** = 0 | The viewport renders a single image (default). |
| **RENDER_MODE_STEREO** = 1 | The viewport renders a side-by-side stereo image, with the left-eye view on the left and the right-eye view on the right. |

### Members

## int getID () const

Returns the current viewport ID.
### Return value

Current viewport ID.
## void setName ( const char * name )

Sets a new [viewport name](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#viewport_name).
### Arguments

- *const char ** **name** - The viewport name.

## String getName () const

Returns the current [viewport name](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#viewport_name).
### Return value

Current viewport name.
## void setComputerName ( const char * name )

Sets a new [name of the computer](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#computer_name), on which this viewport is to be rendered.
### Arguments

- *const char ** **name** - The name of the computer, on which this viewport is to be rendered. If not set, the viewport is rendered on any PC.

## String getComputerName () const

Returns the current [name of the computer](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#computer_name), on which this viewport is to be rendered.
### Return value

Current name of the computer, on which this viewport is to be rendered. If not set, the viewport is rendered on any PC.
## void setDisplayIndex ( int index )

Sets a new [display index](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#display_index).
### Arguments

- *int* **index** - The display index.

## int getDisplayIndex () const

Returns the current [display index](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#display_index).
### Return value

Current display index.
## void setWindowSize ( const Math:: ivec2 & size )

Sets a new [size of the window](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_size), if it is in the [Window mode](#WINDOW_MODE_WINDOWED).
### Arguments

- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md)&* **size** - The window size.

## Math:: ivec2 getWindowSize () const

Returns the current [size of the window](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_size), if it is in the [Window mode](#WINDOW_MODE_WINDOWED).
### Return value

Current window size.
## void setWindowPosition ( const Math:: ivec2 & position )

Sets a new [window position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_position) on the screen.
### Arguments

- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md)&* **position** - The coordinates of the top left corner of the window on the screen.

## Math:: ivec2 getWindowPosition () const

Returns the current [window position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_position) on the screen.
### Return value

Current coordinates of the top left corner of the window on the screen.
## void setWindowMode ( ViewportData::WINDOW_MODE mode )

Sets a new [window mode](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_mode) for the rendered viewport: fullscreen imitation (frameless window adapted to the full window area) or window.
### Arguments

- *[ViewportData::WINDOW_MODE](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#WINDOW_MODE)* **mode** - The window mode for the rendered viewport.

## ViewportData::WINDOW_MODE getWindowMode () const

Returns the current [window mode](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_mode) for the rendered viewport: fullscreen imitation (frameless window adapted to the full window area) or window.
### Return value

Current window mode for the rendered viewport.
## void setProjectionEnabled ( bool enabled )

Sets a new value indicating if the [projection rendering](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#projection_enabled) in viewport is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable projection rendering; **false** - to disable it.

## bool isProjectionEnabled () const

Returns the current value indicating if the [projection rendering](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#projection_enabled) in viewport is enabled.
### Return value

**true** if projection rendering is enabled ; otherwise **false**.
## void setPosition ( const Math:: vec3 & position )

Sets a new [viewport position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_position) relative to the viewpoint in the setup.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **position** - The viewport position relative to the viewpoint in the setup.

## Math:: vec3 getPosition () const

Returns the current [viewport position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_position) relative to the viewpoint in the setup.
### Return value

Current viewport position relative to the viewpoint in the setup.
## void setRotation ( const Math:: vec3 & rotation )

Sets a new [viewport rotation](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_rotation) relative to its own center in the setup.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md)&* **rotation** - The viewport rotation relative to its own center in the setup.

## Math:: vec3 getRotation () const

Returns the current [viewport rotation](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_rotation) relative to its own center in the setup.
### Return value

Current viewport rotation relative to its own center in the setup.
## void setOffset ( const Math:: vec2 & offset )

Sets a new offset of the FOV.
### Arguments

- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md)&* **offset** - The FOV offset.

## Math:: vec2 getOffset () const

Returns the current offset of the FOV.
### Return value

Current FOV offset.
## void setType ( ViewportData::DISPLAY_TRANSFORM_TYPE type )

Sets a new type of the projection matrix distortion applied to the viewport: display or projector.
### Arguments

- *[ViewportData::DISPLAY_TRANSFORM_TYPE](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#DISPLAY_TRANSFORM_TYPE)* **type** - The projection matrix distortion type applied to the viewport.

## ViewportData::DISPLAY_TRANSFORM_TYPE getType () const

Returns the current type of the projection matrix distortion applied to the viewport: display or projector.
### Return value

Current projection matrix distortion type applied to the viewport.
## void setSize ( const Math:: vec2 & size )

Sets a new physical size of the display.
### Arguments

- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md)&* **size** - The physical size of the display.

## Math:: vec2 getSize () const

Returns the current physical size of the display.
### Return value

Current physical size of the display.
## void setAspect ( float aspect )

Sets a new aspect ratio for the projector.
### Arguments

- *float* **aspect** - The aspect ratio for the projector.

## float getAspect () const

Returns the current aspect ratio for the projector.
### Return value

Current aspect ratio for the projector.
## void setVFov ( float vfov )

Sets a new vertical field of view for the projector.
### Arguments

- *float* **vfov** - The vertical field of view for the projector, in degrees.

## float getVFov () const

Returns the current vertical field of view for the projector.
### Return value

Current vertical field of view for the projector, in degrees.
## void setGroupID ( int id )

Sets a new ID of the group of viewports.
### Arguments

- *int* **id** - The ID of the group of viewports.

## int getGroupID () const

Returns the current ID of the group of viewports.
### Return value

Current ID of the group of viewports.
## static Event<ViewportData*> getEventBaseChanged () const

event triggered on changing basic viewport parameters (width, height, position, rotation, etc.). You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BaseChanged event handler
void basechanged_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling BaseChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections basechanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData::getEventBaseChanged().connect(basechanged_event_connections, basechanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData::getEventBaseChanged().connect(basechanged_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling BaseChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
basechanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection basechanged_event_connection;

// subscribe to the BaseChanged event with a handler function keeping the connection
ViewportData::getEventBaseChanged().connect(basechanged_event_connection, basechanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
basechanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
basechanged_event_connection.setEnabled(true);

// ...

// remove subscription to the BaseChanged event via the connection
basechanged_event_connection.disconnect();

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

	// A BaseChanged event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling BaseChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
ViewportData::getEventBaseChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId basechanged_handler_id;

// subscribe to the BaseChanged event with a lambda handler function and keeping connection ID
basechanged_handler_id = ViewportData::getEventBaseChanged().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling BaseChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
ViewportData::getEventBaseChanged().disconnect(basechanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BaseChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData::getEventBaseChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ViewportData::getEventBaseChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<ViewportData*> getEventWarpChanged () const

event triggered on changing warping (geometry correction). You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the WarpChanged event handler
void warpchanged_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling WarpChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections warpchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData::getEventWarpChanged().connect(warpchanged_event_connections, warpchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData::getEventWarpChanged().connect(warpchanged_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling WarpChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
warpchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection warpchanged_event_connection;

// subscribe to the WarpChanged event with a handler function keeping the connection
ViewportData::getEventWarpChanged().connect(warpchanged_event_connection, warpchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
warpchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
warpchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the WarpChanged event via the connection
warpchanged_event_connection.disconnect();

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

	// A WarpChanged event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling WarpChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
ViewportData::getEventWarpChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId warpchanged_handler_id;

// subscribe to the WarpChanged event with a lambda handler function and keeping connection ID
warpchanged_handler_id = ViewportData::getEventWarpChanged().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling WarpChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
ViewportData::getEventWarpChanged().disconnect(warpchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all WarpChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData::getEventWarpChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ViewportData::getEventWarpChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<ViewportData*> getEventEasyblendChanged () const

event triggered on loading or unloading a multi-projector setup configuration `.ol`-file (created via *Scalable Display Manager*). You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EasyblendChanged event handler
void easyblendchanged_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling EasyblendChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections easyblendchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData::getEventEasyblendChanged().connect(easyblendchanged_event_connections, easyblendchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData::getEventEasyblendChanged().connect(easyblendchanged_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling EasyblendChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
easyblendchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection easyblendchanged_event_connection;

// subscribe to the EasyblendChanged event with a handler function keeping the connection
ViewportData::getEventEasyblendChanged().connect(easyblendchanged_event_connection, easyblendchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
easyblendchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
easyblendchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the EasyblendChanged event via the connection
easyblendchanged_event_connection.disconnect();

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

	// A EasyblendChanged event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling EasyblendChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
ViewportData::getEventEasyblendChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId easyblendchanged_handler_id;

// subscribe to the EasyblendChanged event with a lambda handler function and keeping connection ID
easyblendchanged_handler_id = ViewportData::getEventEasyblendChanged().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling EasyblendChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
ViewportData::getEventEasyblendChanged().disconnect(easyblendchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EasyblendChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData::getEventEasyblendChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ViewportData::getEventEasyblendChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<ViewportData*> getEventBlendChanged () const

event triggered on changing screen-space or edge blending settings (alpha, contrast, gamma, etc.). You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BlendChanged event handler
void blendchanged_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling BlendChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections blendchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData::getEventBlendChanged().connect(blendchanged_event_connections, blendchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData::getEventBlendChanged().connect(blendchanged_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling BlendChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
blendchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection blendchanged_event_connection;

// subscribe to the BlendChanged event with a handler function keeping the connection
ViewportData::getEventBlendChanged().connect(blendchanged_event_connection, blendchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
blendchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
blendchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the BlendChanged event via the connection
blendchanged_event_connection.disconnect();

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

	// A BlendChanged event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling BlendChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
ViewportData::getEventBlendChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId blendchanged_handler_id;

// subscribe to the BlendChanged event with a lambda handler function and keeping connection ID
blendchanged_handler_id = ViewportData::getEventBlendChanged().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling BlendChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
ViewportData::getEventBlendChanged().disconnect(blendchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BlendChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData::getEventBlendChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ViewportData::getEventBlendChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<ViewportData*> getEventMaskChanged () const

event triggered on changing (adding, removing, or modifying) masks. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the MaskChanged event handler
void maskchanged_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling MaskChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections maskchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData::getEventMaskChanged().connect(maskchanged_event_connections, maskchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData::getEventMaskChanged().connect(maskchanged_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling MaskChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
maskchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection maskchanged_event_connection;

// subscribe to the MaskChanged event with a handler function keeping the connection
ViewportData::getEventMaskChanged().connect(maskchanged_event_connection, maskchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
maskchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
maskchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the MaskChanged event via the connection
maskchanged_event_connection.disconnect();

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

	// A MaskChanged event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling MaskChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
ViewportData::getEventMaskChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId maskchanged_handler_id;

// subscribe to the MaskChanged event with a lambda handler function and keeping connection ID
maskchanged_handler_id = ViewportData::getEventMaskChanged().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling MaskChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
ViewportData::getEventMaskChanged().disconnect(maskchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all MaskChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData::getEventMaskChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ViewportData::getEventMaskChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<ViewportData*> getEventColorChanged () const

event triggered on changing brightness and color correction settings. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ColorChanged event handler
void colorchanged_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling ColorChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections colorchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData::getEventColorChanged().connect(colorchanged_event_connections, colorchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData::getEventColorChanged().connect(colorchanged_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling ColorChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
colorchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection colorchanged_event_connection;

// subscribe to the ColorChanged event with a handler function keeping the connection
ViewportData::getEventColorChanged().connect(colorchanged_event_connection, colorchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
colorchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
colorchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the ColorChanged event via the connection
colorchanged_event_connection.disconnect();

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

	// A ColorChanged event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling ColorChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
ViewportData::getEventColorChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId colorchanged_handler_id;

// subscribe to the ColorChanged event with a lambda handler function and keeping connection ID
colorchanged_handler_id = ViewportData::getEventColorChanged().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling ColorChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
ViewportData::getEventColorChanged().disconnect(colorchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ColorChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData::getEventColorChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ViewportData::getEventColorChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<ViewportData*> getEventDebugChanged () const

event triggered on changing auxiliary debug settings. You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the DebugChanged event handler
void debugchanged_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling DebugChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections debugchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData::getEventDebugChanged().connect(debugchanged_event_connections, debugchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData::getEventDebugChanged().connect(debugchanged_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling DebugChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
debugchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection debugchanged_event_connection;

// subscribe to the DebugChanged event with a handler function keeping the connection
ViewportData::getEventDebugChanged().connect(debugchanged_event_connection, debugchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
debugchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
debugchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the DebugChanged event via the connection
debugchanged_event_connection.disconnect();

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

	// A DebugChanged event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling DebugChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
ViewportData::getEventDebugChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId debugchanged_handler_id;

// subscribe to the DebugChanged event with a lambda handler function and keeping connection ID
debugchanged_handler_id = ViewportData::getEventDebugChanged().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling DebugChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
ViewportData::getEventDebugChanged().disconnect(debugchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all DebugChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData::getEventDebugChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ViewportData::getEventDebugChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<ViewportData*> getEventSomethingChanged () const

event triggered on ANY changes in viewport configuration data (warping, blending, color correction, debug, etc.).
> **Notice:** This event is triggered along with all other events of this class.

  You can subscribe to events via *connect()* � and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(ViewportData ***viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the SomethingChanged event handler
void somethingchanged_event_handler(ViewportData *viewport_data)
{
	Log::message("\Handling SomethingChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections somethingchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData::getEventSomethingChanged().connect(somethingchanged_event_connections, somethingchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData::getEventSomethingChanged().connect(somethingchanged_event_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling SomethingChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
somethingchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection somethingchanged_event_connection;

// subscribe to the SomethingChanged event with a handler function keeping the connection
ViewportData::getEventSomethingChanged().connect(somethingchanged_event_connection, somethingchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
somethingchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
somethingchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the SomethingChanged event via the connection
somethingchanged_event_connection.disconnect();

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

	// A SomethingChanged event handler implemented as a class member
	void event_handler(ViewportData *viewport_data)
	{
		Log::message("\Handling SomethingChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
ViewportData::getEventSomethingChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId somethingchanged_handler_id;

// subscribe to the SomethingChanged event with a lambda handler function and keeping connection ID
somethingchanged_handler_id = ViewportData::getEventSomethingChanged().connect(e_connections, [](ViewportData *viewport_data) {
		Log::message("\Handling SomethingChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
ViewportData::getEventSomethingChanged().disconnect(somethingchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all SomethingChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData::getEventSomethingChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ViewportData::getEventSomethingChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## void setViewportRendering ( bool rendering )

Sets a new value indicating whether the viewport rendering is enabled.
### Arguments

- *bool* **rendering** - Set **true** to enable viewport rendering; **false** - to disable it.

## bool isViewportRendering () const

Returns the current value indicating whether the viewport rendering is enabled.
### Return value

**true** if viewport rendering is enabled ; otherwise **false**.
## void setPixelDensity ( float density )

Sets a new rendering resolution of the viewport in pixels per meter, used for display-type viewports: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
### Arguments

- *float* **density** - The rendering resolution of the viewport, in pixels per meter

## float getPixelDensity () const

Returns the current rendering resolution of the viewport in pixels per meter, used for display-type viewports: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
### Return value

Current rendering resolution of the viewport, in pixels per meter
## void setRenderMode ( ViewportData::RENDER_MODE mode )

Sets a new rendering mode of the viewport, one of the *RENDER_MODE_** values: a single (mono) image or a side-by-side stereo pair. The default is the mono mode.
### Arguments

- *[ViewportData::RENDER_MODE](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md#RENDER_MODE)* **mode** - The rendering mode of the viewport

## ViewportData::RENDER_MODE getRenderMode () const

Returns the current rendering mode of the viewport, one of the *RENDER_MODE_** values: a single (mono) image or a side-by-side stereo pair. The default is the mono mode.
### Return value

Current rendering mode of the viewport
## void setSwapEyesInStereoMode ( bool mode )

Sets a new value indicating if the left and right eye images are exchanged in stereo mode. Use this option if the stereo signal is reversed due to the display or projection hardware configuration. Has no effect in the mono mode.
### Arguments

- *bool* **mode** - Set **true** to enable swapping of the eye images in stereo mode; **false** - to disable it.

## bool isSwapEyesInStereoMode () const

Returns the current value indicating if the left and right eye images are exchanged in stereo mode. Use this option if the stereo signal is reversed due to the display or projection hardware configuration. Has no effect in the mono mode.
### Return value

**true** if swapping of the eye images in stereo mode is enabled ; otherwise **false**.
---

## void update ( )

Updates the data displayed in the viewport.
## void grabWindowParameters ( )

Updates the viewport data according to the [current window parameters](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#grab): display index, window size and position.
## bool isGrouped ( ) const

Returns the value specifying if the viewport is in the group.
### Return value

true if the viewport is a part of a group, otherwise false.
## void loadEasyBlendSettings ( const char * filepath )

Loads the settings from the EasyBlend setup file.
### Arguments

- *const char ** **filepath** - Path to the EasyBlend setup file.

## void removeEasyblendSetup ( )

Removes the EasyBlend setup.
## WarpGridData * getWarpGrid ( )

Returns the warp grid data.
### Return value

[WarpGridData class](../../../../api/library/plugins/spidervision/class.warpgriddata_cpp.md) instance that stores the warp grid data.
## BlendZonesData * getBlendZones ( )

Returns the blend zones data.
### Return value

[BlendZonesData class](../../../../api/library/plugins/spidervision/class.blendzonesdata_cpp.md) instance that stores the blend zones data.
## MasksData * getMasks ( )

Returns the masks data.
### Return value

[MasksData class](../../../../api/library/plugins/spidervision/class.masksdata_cpp.md) instance that stores the masks data.
## ColorCorrectionData * getColorCorrection ( )

Returns the color correction data.
### Return value

[ColorCorrectionData class](../../../../api/library/plugins/spidervision/class.colorcorrectiondata_cpp.md) instance that stores the color correction data.
## DebugData * getDebug ( )

Returns the debug data.
### Return value

[DebugData class](../../../../api/library/plugins/spidervision/class.debugdata_cpp.md) instance that stores the debug data.
## EasyBlendData * getEasyblendData ( )

Returns the EasyBlend data.
### Return value

[EasyBlendData class](../../../../api/library/plugins/spidervision/class.easyblenddata_cpp.md) instance that stores the EasyBlend data.
## void saveXml ( const Ptr < Xml > & xml )

Saves the viewport data to the given instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance into which the data will be saved.

## bool restoreXml ( const Ptr < Xml > & xml )

Loads the viewport data from the specified instance of the Xml class.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Xml](../../../../api/library/common/class.xml_cpp.md)> &* **xml** - [Xml class](../../../../api/library/common/class.xml_cpp.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void save ( const Ptr < Stream > & stream )

Saves the viewport data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restore ( const Ptr < Stream > & stream )

Loads the viewport data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.

## void saveBase ( const Ptr < Stream > & stream )

Saves the viewport data to the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to which the data is to be written.

## void restoreBase ( const Ptr < Stream > & stream )

Loads the viewport data from the specified stream.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream the data from which is to be loaded.

## void copy ( const ViewportData & data )

Copies the current viewport data to the specified instance of the ViewportData class.
### Arguments

- *const [ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cpp.md) &* **data** - Viewport data.
