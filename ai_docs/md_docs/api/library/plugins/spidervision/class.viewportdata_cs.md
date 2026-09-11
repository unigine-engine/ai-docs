# Unigine::Plugins::SpiderVision::ViewportData Class (CS)


The object of this class stores all data on the viewport: transformations, viewport type settings, physical size of the display, VFOV, aspect, vertical and horizontal offsets, warping effect details, etc.


This object is accessible via the corresponding methods of the [DisplaysConfig](../../../../api/library/plugins/spidervision/class.displaysconfig_cs.md#getViewportByIndex_int_ViewportData) class.


The mask data are stored in the [configuration file](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file).


## ViewportData Class

### Enums

## WINDOW_MODE

| Name | Description |
|---|---|
| **WINDOW** = 0 | Window mode. |
| **WINDOW_BORDERLESS** = 1 | Borderless OS window with the configurable size. |
| **FULLSCREEN** = 2 | Fullscreen window that occupies the entire display, while all other engine windows are minimized. Interaction with other engine windows is not possible. If focus is switched to another application window, the Fullscreen window is minimized automatically by the OS. |

## POINT_SMOOTH_TYPE

| Name | Description |
|---|---|
| **LINEAR** = 0 | Linear interpolation is applied for curving of the line on both sides of the point. |
| **SMOOTH** = 1 | Symmetric control handles for smooth curves on both sides of the point. |
| **BREAK** = 2 | Asymmetric control handles for an independent control of each handle. |
| **AUTO** = 3 | Automatic smooth line curving, no control handles available. |
| **NUM** = 4 | Total number of line curving modes. |

## DISPLAY_TRANSFORM_TYPE

| Name | Description |
|---|---|
| **DISPLAY** = 0 | Display viewport. |
| **PROJECTOR** = 1 | Projector (beamer) viewport. |

## RENDER_MODE

Rendering mode of the viewport: a single image or a side-by-side stereo pair.
| Name | Description |
|---|---|
| **MONO** = 0 | The viewport renders a single image (default). |
| **STEREO** = 1 | The viewport renders a side-by-side stereo image, with the left-eye view on the left and the right-eye view on the right. |

### Properties

## 🔒︎ int ID

The viewport ID.
## string Name

The [viewport name](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#viewport_name).
## string ComputerName

The [name of the computer](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#computer_name), on which this viewport is to be rendered.
## int DisplayIndex

The [display index](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#display_index).
## ivec2 WindowSize

The [size of the window](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_size), if it is in the [Window mode](#WINDOW_MODE_WINDOWED).
## ivec2 WindowPosition

The [window position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_position) on the screen.
## ViewportData.WINDOW_MODE WindowMode

The [window mode](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#window_mode) for the rendered viewport: fullscreen imitation (frameless window adapted to the full window area) or window.
## bool ProjectionEnabled

The value indicating if the [projection rendering](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#projection_enabled) in viewport is enabled.
## vec3 Position

The [viewport position](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_position) relative to the viewpoint in the setup.
## vec3 Rotation

The [viewport rotation](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#transform_rotation) relative to its own center in the setup.
## vec2 Offset

The offset of the FOV.
## ViewportData.DISPLAY_TRANSFORM_TYPE Type

The type of the projection matrix distortion applied to the viewport: display or projector.
## vec2 Size

The physical size of the display.
## float Aspect

The aspect ratio for the projector.
## float VFov

The vertical field of view for the projector.
## int GroupID

The ID of the group of viewports.
## 🔒︎ Event< ViewportData > EventBaseChanged

The event triggered on changing basic viewport parameters (width, height, position, rotation, etc.). You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BaseChanged event handler
void basechanged_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling BaseChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections basechanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData.EventBaseChanged.Connect(basechanged_event_connections, basechanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData.EventBaseChanged.Connect(basechanged_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling BaseChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
basechanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BaseChanged event with a handler function
ViewportData.EventBaseChanged.Connect(basechanged_event_handler);

// remove subscription to the BaseChanged event later by the handler function
ViewportData.EventBaseChanged.Disconnect(basechanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection basechanged_event_connection;

// subscribe to the BaseChanged event with a lambda handler function and keeping the connection
basechanged_event_connection = ViewportData.EventBaseChanged.Connect((ViewportData viewport_data) => {
		Log.Message("Handling BaseChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
basechanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
basechanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
basechanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BaseChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData.EventBaseChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
ViewportData.EventBaseChanged.Enabled = true;

```

</details>

## 🔒︎ Event< ViewportData > EventWarpChanged

The event triggered on changing warping (geometry correction) settings. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the WarpChanged event handler
void warpchanged_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling WarpChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections warpchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData.EventWarpChanged.Connect(warpchanged_event_connections, warpchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData.EventWarpChanged.Connect(warpchanged_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling WarpChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
warpchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the WarpChanged event with a handler function
ViewportData.EventWarpChanged.Connect(warpchanged_event_handler);

// remove subscription to the WarpChanged event later by the handler function
ViewportData.EventWarpChanged.Disconnect(warpchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection warpchanged_event_connection;

// subscribe to the WarpChanged event with a lambda handler function and keeping the connection
warpchanged_event_connection = ViewportData.EventWarpChanged.Connect((ViewportData viewport_data) => {
		Log.Message("Handling WarpChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
warpchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
warpchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
warpchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring WarpChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData.EventWarpChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
ViewportData.EventWarpChanged.Enabled = true;

```

</details>

## 🔒︎ Event< ViewportData > EventEasyblendChanged

The event triggered on loading or unloading a multi-projector setup configuration `.ol`-file (created via *Scalable Display Manager*). You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EasyblendChanged event handler
void easyblendchanged_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling EasyblendChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections easyblendchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData.EventEasyblendChanged.Connect(easyblendchanged_event_connections, easyblendchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData.EventEasyblendChanged.Connect(easyblendchanged_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling EasyblendChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
easyblendchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EasyblendChanged event with a handler function
ViewportData.EventEasyblendChanged.Connect(easyblendchanged_event_handler);

// remove subscription to the EasyblendChanged event later by the handler function
ViewportData.EventEasyblendChanged.Disconnect(easyblendchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection easyblendchanged_event_connection;

// subscribe to the EasyblendChanged event with a lambda handler function and keeping the connection
easyblendchanged_event_connection = ViewportData.EventEasyblendChanged.Connect((ViewportData viewport_data) => {
		Log.Message("Handling EasyblendChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
easyblendchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
easyblendchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
easyblendchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EasyblendChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData.EventEasyblendChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
ViewportData.EventEasyblendChanged.Enabled = true;

```

</details>

## 🔒︎ Event< ViewportData > EventBlendChanged

The event triggered on changing screen-space or edge blending settings (alpha, contrast, gamma, etc.). You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BlendChanged event handler
void blendchanged_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling BlendChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections blendchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData.EventBlendChanged.Connect(blendchanged_event_connections, blendchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData.EventBlendChanged.Connect(blendchanged_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling BlendChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
blendchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BlendChanged event with a handler function
ViewportData.EventBlendChanged.Connect(blendchanged_event_handler);

// remove subscription to the BlendChanged event later by the handler function
ViewportData.EventBlendChanged.Disconnect(blendchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection blendchanged_event_connection;

// subscribe to the BlendChanged event with a lambda handler function and keeping the connection
blendchanged_event_connection = ViewportData.EventBlendChanged.Connect((ViewportData viewport_data) => {
		Log.Message("Handling BlendChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
blendchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
blendchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
blendchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BlendChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData.EventBlendChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
ViewportData.EventBlendChanged.Enabled = true;

```

</details>

## 🔒︎ Event< ViewportData > EventMaskChanged

The event triggered on changing (adding, removing, or modifying) masks. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the MaskChanged event handler
void maskchanged_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling MaskChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections maskchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData.EventMaskChanged.Connect(maskchanged_event_connections, maskchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData.EventMaskChanged.Connect(maskchanged_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling MaskChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
maskchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the MaskChanged event with a handler function
ViewportData.EventMaskChanged.Connect(maskchanged_event_handler);

// remove subscription to the MaskChanged event later by the handler function
ViewportData.EventMaskChanged.Disconnect(maskchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection maskchanged_event_connection;

// subscribe to the MaskChanged event with a lambda handler function and keeping the connection
maskchanged_event_connection = ViewportData.EventMaskChanged.Connect((ViewportData viewport_data) => {
		Log.Message("Handling MaskChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
maskchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
maskchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
maskchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring MaskChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData.EventMaskChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
ViewportData.EventMaskChanged.Enabled = true;

```

</details>

## 🔒︎ Event< ViewportData > EventColorChanged

The event triggered on changing brightness and color correction settings. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ColorChanged event handler
void colorchanged_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling ColorChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections colorchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData.EventColorChanged.Connect(colorchanged_event_connections, colorchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData.EventColorChanged.Connect(colorchanged_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling ColorChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
colorchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ColorChanged event with a handler function
ViewportData.EventColorChanged.Connect(colorchanged_event_handler);

// remove subscription to the ColorChanged event later by the handler function
ViewportData.EventColorChanged.Disconnect(colorchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection colorchanged_event_connection;

// subscribe to the ColorChanged event with a lambda handler function and keeping the connection
colorchanged_event_connection = ViewportData.EventColorChanged.Connect((ViewportData viewport_data) => {
		Log.Message("Handling ColorChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
colorchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
colorchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
colorchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ColorChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData.EventColorChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
ViewportData.EventColorChanged.Enabled = true;

```

</details>

## 🔒︎ Event< ViewportData > EventDebugChanged

The event triggered on changing auxiliary debug settings. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the DebugChanged event handler
void debugchanged_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling DebugChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections debugchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData.EventDebugChanged.Connect(debugchanged_event_connections, debugchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData.EventDebugChanged.Connect(debugchanged_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling DebugChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
debugchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the DebugChanged event with a handler function
ViewportData.EventDebugChanged.Connect(debugchanged_event_handler);

// remove subscription to the DebugChanged event later by the handler function
ViewportData.EventDebugChanged.Disconnect(debugchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection debugchanged_event_connection;

// subscribe to the DebugChanged event with a lambda handler function and keeping the connection
debugchanged_event_connection = ViewportData.EventDebugChanged.Connect((ViewportData viewport_data) => {
		Log.Message("Handling DebugChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
debugchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
debugchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
debugchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring DebugChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData.EventDebugChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
ViewportData.EventDebugChanged.Enabled = true;

```

</details>

## 🔒︎ Event< ViewportData > EventSomethingChanged

The event triggered on ANY changes in viewport configuration data (warping, blending, color correction, debug, etc.).
> **Notice:** This event is triggered along with all other events of this class.

  You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(ViewportData **viewport_data**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the SomethingChanged event handler
void somethingchanged_event_handler(ViewportData viewport_data)
{
	Log.Message("\Handling SomethingChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections somethingchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
ViewportData.EventSomethingChanged.Connect(somethingchanged_event_connections, somethingchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
ViewportData.EventSomethingChanged.Connect(somethingchanged_event_connections, (ViewportData viewport_data) => {
		Log.Message("Handling SomethingChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
somethingchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the SomethingChanged event with a handler function
ViewportData.EventSomethingChanged.Connect(somethingchanged_event_handler);

// remove subscription to the SomethingChanged event later by the handler function
ViewportData.EventSomethingChanged.Disconnect(somethingchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection somethingchanged_event_connection;

// subscribe to the SomethingChanged event with a lambda handler function and keeping the connection
somethingchanged_event_connection = ViewportData.EventSomethingChanged.Connect((ViewportData viewport_data) => {
		Log.Message("Handling SomethingChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
somethingchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
somethingchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
somethingchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring SomethingChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
ViewportData.EventSomethingChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
ViewportData.EventSomethingChanged.Enabled = true;

```

</details>

## bool ViewportRendering

The value indicating whether the viewport rendering is enabled.
## float PixelDensity

The rendering resolution of the viewport in pixels per meter, used for display-type viewports: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
## ViewportData.RENDER_MODE RenderMode

The rendering mode of the viewport, one of the *RENDER_MODE_** values: a single (mono) image or a side-by-side stereo pair. The default is the mono mode.
## bool SwapEyesInStereoMode

The value indicating if the left and right eye images are exchanged in stereo mode. Use this option if the stereo signal is reversed due to the display or projection hardware configuration. Has no effect in the mono mode.
### Members

---

## void Update ( )

Updates the data displayed in the viewport.
## void GrabWindowParameters ( )

Updates the viewport data according to the [current window parameters](../../../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#grab): display index, window size and position.
## bool IsGrouped ( )

Returns the value specifying if the viewport is in the group.
### Return value

true if the viewport is a part of a group, otherwise false.
## void LoadEasyBlendSettings ( string filepath )

Loads the settings from the EasyBlend setup file.
### Arguments

- *string* **filepath** - Path to the EasyBlend setup file.

## void RemoveEasyblendSetup ( )

Removes the EasyBlend setup.
## WarpGridData GetWarpGrid ( )

Returns the warp grid data.
### Return value

[WarpGridData class](../../../../api/library/plugins/spidervision/class.warpgriddata_cs.md) instance that stores the warp grid data.
## BlendZonesData GetBlendZones ( )

Returns the blend zones data.
### Return value

[BlendZonesData class](../../../../api/library/plugins/spidervision/class.blendzonesdata_cs.md) instance that stores the blend zones data.
## MasksData GetMasks ( )

Returns the masks data.
### Return value

[MasksData class](../../../../api/library/plugins/spidervision/class.masksdata_cs.md) instance that stores the masks data.
## ColorCorrectionData GetColorCorrection ( )

Returns the color correction data.
### Return value

[ColorCorrectionData class](../../../../api/library/plugins/spidervision/class.colorcorrectiondata_cs.md) instance that stores the color correction data.
## DebugData GetDebug ( )

Returns the debug data.
### Return value

[DebugData class](../../../../api/library/plugins/spidervision/class.debugdata_cs.md) instance that stores the debug data.
## EasyBlendData GetEasyblendData ( )

Returns the EasyBlend data.
### Return value

[EasyBlendData class](../../../../api/library/plugins/spidervision/class.easyblenddata_cs.md) instance that stores the EasyBlend data.
## void SaveXml ( Xml xml )

Saves the viewport data to the given instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance into which the data will be saved.

## bool RestoreXml ( Xml xml )

Loads the viewport data from the specified instance of the Xml class.
### Arguments

- *[Xml](../../../../api/library/common/class.xml_cs.md)* **xml** - [Xml class](../../../../api/library/common/class.xml_cs.md) instance the data from which is to be loaded.

### Return value

true if the data has been loaded successfully, otherwise false.
## void Save ( Stream stream )

Saves the viewport data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void Restore ( Stream stream )

Loads the viewport data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.

## void SaveBase ( Stream stream )

Saves the viewport data to the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which the data is to be written.

## void RestoreBase ( Stream stream )

Loads the viewport data from the specified stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **stream** - Stream the data from which is to be loaded.

## void Copy ( ViewportData data )

Copies the current viewport data to the specified instance of the ViewportData class.
### Arguments

- *[ViewportData](../../../../api/library/plugins/spidervision/class.viewportdata_cs.md)* **data** - Viewport data.
