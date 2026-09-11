# Unigine.Viewport Class (CS)


The **Viewport** class is used to render a scene with the specified settings.


There are two main use cases of the Viewport class:


1. Integrate the engine to a 3rd party renderer (or vice versa) and render the image anywhere (via the [Render()](#render_Camera_void)  method): to the external library, [CustomSystemProxy](../../../api/library/engine/class.customsystemproxy_cs.md) interface, [RenderTarget](../../../api/library/rendering/class.rendertarget_cs.md) interface (a frame buffers abstraction), etc.

  - To render the image to the [RenderTarget](../../../api/library/rendering/class.rendertarget_cs.md) interface, do the following: ```csharp // mono rendering Viewport viewport; Texture texture; Camera camera; private void Init() { viewport = new Viewport(); texture = new Texture(); // create 512 x 512 render target texture.Create2D(512, 512, Texture.FORMAT_RGBA8, Texture.FORMAT_USAGE_RENDER); camera = new Camera(); } private void Update() { // set modelview & projection matrices to camera instance // ... // rendering RenderTarget render_target = Render.GetTemporaryRenderTarget(); render_target.BindColorTexture(0, texture); render_target.Enable(); { viewport.Render(camera); } render_target.Disable(); render_target.UnbindAll(); Render.ReleaseTemporaryRenderTarget(render_target); } ``` To render the image to the [RenderTarget](../../../api/library/rendering/class.rendertarget_cs.md) interface in the stereo mode, do the following: ```csharp // stereo rendering Viewport viewport; Texture left_texture; Texture right_texture; Camera left_eye; Camera right_eye; private void Init() { viewport = new Viewport(); left_texture = new Texture(); right_texture = new Texture(); // create two 512 x 512 render target for each eye left_texture.Create2D(512, 512, Texture.FORMAT_RGBA8, Texture.FORMAT_USAGE_RENDER); right_texture.Create2D(512, 512, Texture.FORMAT_RGBA8, Texture.FORMAT_USAGE_RENDER); left_eye = new Camera(); right_eye = new Camera(); } private void Update() { // set modelview & projection matrices to camera instance // ... // rendering RenderTarget render_target = Render.GetTemporaryRenderTarget(); render_target.BindColorTexture(0, left_texture); render_target.BindColorTexture(1, right_texture); render_target.Enable(); { // use "post_stereo_separate" material in order to render to both textures viewport.RenderStereo(left_eye, right_eye, "Unigine::post_stereo_separate"); } render_target.Disable(); render_target.UnbindAll(); Render.ReleaseTemporaryRenderTarget(render_target); } ```
  - To render the image to the [CustomSystemProxy](../../../api/library/engine/class.customsystemproxy_cs.md) interface, check the following 3rd party samples (e.g. `Samples -> 3rd Party -> QT -> ViewportQt`) > **Notice:** **ViewportQt** sample is available only for the Engineering and Sim editions of UNIGINE SDKs.
2. Render a scene to a [texture](../../../api/library/rendering/class.texture_cs.md) (data stays in the GPU memory).

  - To render the scene to a [Texture](../../../api/library/rendering/class.texture_cs.md) interface, use the following methods: ```csharp Viewport viewport; Texture texture; Camera camera; private void Init() { viewport = new Viewport(); texture = new Texture(); // create 512 x 512 render target texture.Create2D(512, 512, Texture.FORMAT_RGBA8, Texture.FORMAT_USAGE_RENDER); camera = new Camera(); } private void Update() { // set modelview & projection matrices to camera instance // ... // rendering // // saving current render state and clearing it RenderState.SaveState(); RenderState.ClearStates(); { viewport.RenderTexture2D(camera, texture); } RenderState.RestoreState(); } ```

    - *[RenderTexture2D(camera,texture)](#renderTexture2D_Camera_Texture_void)*
    - *[RenderTexture2D(camera,texture,width,height,hdr)](#renderTexture2D_Camera_Texture_int_int_int_void)*
    - *[RenderTextureCube(camera,texture,local_space)](#renderTextureCube_Camera_Texture_int_void)*
    - *[RenderTextureCube(camera,texture,size,hdr,local_space)](#renderTextureCube_Camera_Texture_int_int_int_void)*
3. Render a node to a [texture](../../../api/library/rendering/class.texture_cs.md) (data stays in the GPU memory).

  - To render a node (or nodes) to a [Texture](../../../api/library/rendering/class.texture_cs.md) interface, use the following methods:

    - *[RenderNodeTexture2D(camera,node,texture)](#renderNodeTexture2D_Camera_Node_Texture_void)*
    - *[RenderNodeTexture2D(camera,node,texture,width,height,hdr)](#renderNodeTexture2D_Camera_Node_Texture_int_int_int_void)*
    - *[RenderNodesTexture2D(camera,nodes,texture)](#renderNodesTexture2D_Camera_VECNode_Texture_void)*
    - *[RenderNodesTexture2D(camera,nodes,texture,width,height,hdr)](#renderNodesTexture2D_Camera_VECNode_Texture_int_int_int_void)*


> **Notice:** To set any viewport as a main, use the *[Viewport](../../../api/library/rendering/class.render_cs.md#setViewport_Viewport_void)* property of the *Render* class.
>
>
> **A single viewport should be used with a single camera**, otherwise it may cause visual artefacts. To avoid artefacts, when using several cameras with a single viewport, all post effects must be disabled using the *[SkipFlags](#setSkipFlags_int_void)* property with the [SKIP_POSTEFFECTS](#SKIP_POSTEFFECTS) flag.


<details>
<summary>Example: Single Viewport & Several Cameras | Close</summary>

```csharp
public void SetupMultipleCamerasWithSingleViewport()
{
    // Create a shared viewport for multiple cameras
    Viewport sharedViewport = Viewport.Create();

    // CRITICAL: Disable post-effects to avoid visual artifacts
    // when using multiple cameras with a single viewport
    sharedViewport.SkipFlags = Viewport.SKIP_POSTEFFECTS;

    sharedViewport.NodeLightUsage = Viewport.USAGE_WORLD_LIGHT;

    // Create multiple cameras
    Camera camera1 = Camera.Create();
    Camera camera2 = Camera.Create();

    // Position cameras differently
    camera1.Position = new vec3(0.0f, 0.0f, 5.0f);
    camera2.Position = new vec3(10.0f, 0.0f, 5.0f);

    // Create textures for each camera's output
    Texture texture1 = Texture.Create();
    Texture texture2 = Texture.Create();

    texture1.Create2D(1920, 1080, Texture.FORMAT_RGBA8,
        Texture.FORMAT_USAGE_RENDER);
    texture2.Create2D(1920, 1080, Texture.FORMAT_RGBA8,
        Texture.FORMAT_USAGE_RENDER);

    // Render from different cameras using the same viewport
    // Post-effects are disabled, so no artifacts will occur
    sharedViewport.RenderTexture2D(camera1, texture1);
    sharedViewport.RenderTexture2D(camera2, texture2);
}

```

</details>


### See also


- C++ samples:

  -
  -
  -
  -
- C# Component sample
- C++/C# usage example: [Creating Mirrors Using Viewports (Rendering to Texture) or a Standard Material](../../../code/usage/mirrors_viewports_materials/index_cs.md)


## Viewport Class

### Properties

## int NodeLightUsage

The type of lighting of the render node.
## float StereoOffset

The virtual camera offset (an offset after the perspective projection).
## float StereoRadius

The radius for stereo � the half of the separation distance between the cameras (i.e. between eyes).
## float StereoDistance

The focal distance for stereo rendering (distance in the world space to the point where two views line up, i.e. to the zero parallax plane).
## 🔒︎ bool IsStereo

The value indicating if the stereo rendering is enabled for the current viewport (one of the [stereo modes](../../../api/library/rendering/class.render_cs.md#VIEWPORT_MODE_STEREO_ANAGLYPH) is set).
## 🔒︎ bool IsPanorama

The value indicating if the panoramic rendering is enabled.
## int RenderMode

The render mode. The mode determines the set of buffers to be rendered.
## Render.VIEWPORT_MODE Mode

The rendering mode for the current viewport.
## int SkipFlags

The [skip flag](#SKIP_SHADOWS) set for the current viewport.
## int FirstFrame

The value indicating if the first frame is enabled over the current frame.
## bool AspectCorrection

The value indicating if the aspect correction enabled for current viewport.
## 🔒︎ int ID

The Viewport ID.
## float PanoramaFisheyeFov

The field of view angle used for the panorama rendering mode.
## Texture EnvironmentTexture

The cubemap defining the environment color.
## bool UseTAAOffset

The  value indicating if skipping render mode check is enabled for using TAA.
Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to *[RENDER_DEPTH](../../...md#RENDER_DEPTH)*.

## int Lifetime

The value indicating how many frames temporary viewport resources are available after the viewport stops rendering.
## 🔒︎ Event EventBegin

The event triggered when rendering of the frame begins. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Begin event handler
void begin_event_handler()
{
	Log.Message("\Handling Begin event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begin_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBegin.Connect(begin_event_connections, begin_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBegin.Connect(begin_event_connections, () => {
		Log.Message("Handling Begin event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begin_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Begin event with a handler function
publisher.EventBegin.Connect(begin_event_handler);

// remove subscription to the Begin event later by the handler function
publisher.EventBegin.Disconnect(begin_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begin_event_connection;

// subscribe to the Begin event with a lambda handler function and keeping the connection
begin_event_connection = publisher.EventBegin.Connect(() => {
		Log.Message("Handling Begin event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begin_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begin_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begin_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Begin events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBegin.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBegin.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginEnvironment

The event triggered before the Environment rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginEnvironment event handler
void beginenvironment_event_handler()
{
	Log.Message("\Handling BeginEnvironment event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginenvironment_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginEnvironment.Connect(beginenvironment_event_connections, beginenvironment_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginEnvironment.Connect(beginenvironment_event_connections, () => {
		Log.Message("Handling BeginEnvironment event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginenvironment_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginEnvironment event with a handler function
publisher.EventBeginEnvironment.Connect(beginenvironment_event_handler);

// remove subscription to the BeginEnvironment event later by the handler function
publisher.EventBeginEnvironment.Disconnect(beginenvironment_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginenvironment_event_connection;

// subscribe to the BeginEnvironment event with a lambda handler function and keeping the connection
beginenvironment_event_connection = publisher.EventBeginEnvironment.Connect(() => {
		Log.Message("Handling BeginEnvironment event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginenvironment_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginenvironment_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginenvironment_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginEnvironment events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginEnvironment.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginEnvironment.Enabled = true;

```

</details>

## 🔒︎ Event EventEndEnvironment

The event triggered after the Environment rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndEnvironment event handler
void endenvironment_event_handler()
{
	Log.Message("\Handling EndEnvironment event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endenvironment_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndEnvironment.Connect(endenvironment_event_connections, endenvironment_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndEnvironment.Connect(endenvironment_event_connections, () => {
		Log.Message("Handling EndEnvironment event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endenvironment_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndEnvironment event with a handler function
publisher.EventEndEnvironment.Connect(endenvironment_event_handler);

// remove subscription to the EndEnvironment event later by the handler function
publisher.EventEndEnvironment.Disconnect(endenvironment_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endenvironment_event_connection;

// subscribe to the EndEnvironment event with a lambda handler function and keeping the connection
endenvironment_event_connection = publisher.EventEndEnvironment.Connect(() => {
		Log.Message("Handling EndEnvironment event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endenvironment_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endenvironment_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endenvironment_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndEnvironment events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndEnvironment.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndEnvironment.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginShadows

The event triggered before the shadows rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginShadows event handler
void beginshadows_event_handler()
{
	Log.Message("\Handling BeginShadows event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginshadows_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginShadows.Connect(beginshadows_event_connections, beginshadows_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginShadows.Connect(beginshadows_event_connections, () => {
		Log.Message("Handling BeginShadows event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginshadows_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginShadows event with a handler function
publisher.EventBeginShadows.Connect(beginshadows_event_handler);

// remove subscription to the BeginShadows event later by the handler function
publisher.EventBeginShadows.Disconnect(beginshadows_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginshadows_event_connection;

// subscribe to the BeginShadows event with a lambda handler function and keeping the connection
beginshadows_event_connection = publisher.EventBeginShadows.Connect(() => {
		Log.Message("Handling BeginShadows event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginshadows_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginshadows_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginshadows_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginShadows events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginShadows.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginShadows.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWorldShadow

The event triggered before the stage of rendering shadows from World light sources. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWorldShadow event handler
void beginworldshadow_event_handler()
{
	Log.Message("\Handling BeginWorldShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldshadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginWorldShadow.Connect(beginworldshadow_event_connections, beginworldshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginWorldShadow.Connect(beginworldshadow_event_connections, () => {
		Log.Message("Handling BeginWorldShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginworldshadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWorldShadow event with a handler function
publisher.EventBeginWorldShadow.Connect(beginworldshadow_event_handler);

// remove subscription to the BeginWorldShadow event later by the handler function
publisher.EventBeginWorldShadow.Disconnect(beginworldshadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginworldshadow_event_connection;

// subscribe to the BeginWorldShadow event with a lambda handler function and keeping the connection
beginworldshadow_event_connection = publisher.EventBeginWorldShadow.Connect(() => {
		Log.Message("Handling BeginWorldShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginworldshadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginworldshadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginworldshadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWorldShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginWorldShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginWorldShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWorldShadow

The event triggered after the stage of rendering shadows from World light sources. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWorldShadow event handler
void endworldshadow_event_handler()
{
	Log.Message("\Handling EndWorldShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldshadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndWorldShadow.Connect(endworldshadow_event_connections, endworldshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndWorldShadow.Connect(endworldshadow_event_connections, () => {
		Log.Message("Handling EndWorldShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endworldshadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWorldShadow event with a handler function
publisher.EventEndWorldShadow.Connect(endworldshadow_event_handler);

// remove subscription to the EndWorldShadow event later by the handler function
publisher.EventEndWorldShadow.Disconnect(endworldshadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endworldshadow_event_connection;

// subscribe to the EndWorldShadow event with a lambda handler function and keeping the connection
endworldshadow_event_connection = publisher.EventEndWorldShadow.Connect(() => {
		Log.Message("Handling EndWorldShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endworldshadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endworldshadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endworldshadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWorldShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndWorldShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndWorldShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginProjShadow

The event triggered before the stage of rendering shadows from Projected light sources. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginProjShadow event handler
void beginprojshadow_event_handler()
{
	Log.Message("\Handling BeginProjShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginprojshadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginProjShadow.Connect(beginprojshadow_event_connections, beginprojshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginProjShadow.Connect(beginprojshadow_event_connections, () => {
		Log.Message("Handling BeginProjShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginprojshadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginProjShadow event with a handler function
publisher.EventBeginProjShadow.Connect(beginprojshadow_event_handler);

// remove subscription to the BeginProjShadow event later by the handler function
publisher.EventBeginProjShadow.Disconnect(beginprojshadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginprojshadow_event_connection;

// subscribe to the BeginProjShadow event with a lambda handler function and keeping the connection
beginprojshadow_event_connection = publisher.EventBeginProjShadow.Connect(() => {
		Log.Message("Handling BeginProjShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginprojshadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginprojshadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginprojshadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginProjShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginProjShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginProjShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventEndProjShadow

The event triggered after the stage of rendering shadows from Projected light sources. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndProjShadow event handler
void endprojshadow_event_handler()
{
	Log.Message("\Handling EndProjShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endprojshadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndProjShadow.Connect(endprojshadow_event_connections, endprojshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndProjShadow.Connect(endprojshadow_event_connections, () => {
		Log.Message("Handling EndProjShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endprojshadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndProjShadow event with a handler function
publisher.EventEndProjShadow.Connect(endprojshadow_event_handler);

// remove subscription to the EndProjShadow event later by the handler function
publisher.EventEndProjShadow.Disconnect(endprojshadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endprojshadow_event_connection;

// subscribe to the EndProjShadow event with a lambda handler function and keeping the connection
endprojshadow_event_connection = publisher.EventEndProjShadow.Connect(() => {
		Log.Message("Handling EndProjShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endprojshadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endprojshadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endprojshadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndProjShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndProjShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndProjShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOmniShadow

The event triggered before the stage of rendering shadows from Omni light sources. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOmniShadow event handler
void beginomnishadow_event_handler()
{
	Log.Message("\Handling BeginOmniShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginomnishadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginOmniShadow.Connect(beginomnishadow_event_connections, beginomnishadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginOmniShadow.Connect(beginomnishadow_event_connections, () => {
		Log.Message("Handling BeginOmniShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginomnishadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOmniShadow event with a handler function
publisher.EventBeginOmniShadow.Connect(beginomnishadow_event_handler);

// remove subscription to the BeginOmniShadow event later by the handler function
publisher.EventBeginOmniShadow.Disconnect(beginomnishadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginomnishadow_event_connection;

// subscribe to the BeginOmniShadow event with a lambda handler function and keeping the connection
beginomnishadow_event_connection = publisher.EventBeginOmniShadow.Connect(() => {
		Log.Message("Handling BeginOmniShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginomnishadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginomnishadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginomnishadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOmniShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginOmniShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginOmniShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOmniShadow

The event triggered after the stage of rendering shadows from Omni light sources. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOmniShadow event handler
void endomnishadow_event_handler()
{
	Log.Message("\Handling EndOmniShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endomnishadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndOmniShadow.Connect(endomnishadow_event_connections, endomnishadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndOmniShadow.Connect(endomnishadow_event_connections, () => {
		Log.Message("Handling EndOmniShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endomnishadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOmniShadow event with a handler function
publisher.EventEndOmniShadow.Connect(endomnishadow_event_handler);

// remove subscription to the EndOmniShadow event later by the handler function
publisher.EventEndOmniShadow.Disconnect(endomnishadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endomnishadow_event_connection;

// subscribe to the EndOmniShadow event with a lambda handler function and keeping the connection
endomnishadow_event_connection = publisher.EventEndOmniShadow.Connect(() => {
		Log.Message("Handling EndOmniShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endomnishadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endomnishadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endomnishadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOmniShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndOmniShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndOmniShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventEndShadows

The event triggered after the shadows rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndShadows event handler
void endshadows_event_handler()
{
	Log.Message("\Handling EndShadows event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endshadows_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndShadows.Connect(endshadows_event_connections, endshadows_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndShadows.Connect(endshadows_event_connections, () => {
		Log.Message("Handling EndShadows event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endshadows_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndShadows event with a handler function
publisher.EventEndShadows.Connect(endshadows_event_handler);

// remove subscription to the EndShadows event later by the handler function
publisher.EventEndShadows.Disconnect(endshadows_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endshadows_event_connection;

// subscribe to the EndShadows event with a lambda handler function and keeping the connection
endshadows_event_connection = publisher.EventEndShadows.Connect(() => {
		Log.Message("Handling EndShadows event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endshadows_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endshadows_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endshadows_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndShadows events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndShadows.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndShadows.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginScreen

The event triggered before the stage of rendering each screen (a stereo image has 2 screens, while a cubemap will have 6). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginScreen event handler
void beginscreen_event_handler()
{
	Log.Message("\Handling BeginScreen event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginscreen_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginScreen.Connect(beginscreen_event_connections, beginscreen_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginScreen.Connect(beginscreen_event_connections, () => {
		Log.Message("Handling BeginScreen event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginscreen_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginScreen event with a handler function
publisher.EventBeginScreen.Connect(beginscreen_event_handler);

// remove subscription to the BeginScreen event later by the handler function
publisher.EventBeginScreen.Disconnect(beginscreen_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginscreen_event_connection;

// subscribe to the BeginScreen event with a lambda handler function and keeping the connection
beginscreen_event_connection = publisher.EventBeginScreen.Connect(() => {
		Log.Message("Handling BeginScreen event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginscreen_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginscreen_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginscreen_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginScreen events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginScreen.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginScreen.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginMixedRealityBlendMaskColor

The event triggered before the mask for Mixed Reality is rendered (after Common Camera for clouds and before Opacity GBuffer). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginMixedRealityBlendMaskColor event handler
void beginmixedrealityblendmaskcolor_event_handler()
{
	Log.Message("\Handling BeginMixedRealityBlendMaskColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginmixedrealityblendmaskcolor_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginMixedRealityBlendMaskColor.Connect(beginmixedrealityblendmaskcolor_event_connections, beginmixedrealityblendmaskcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginMixedRealityBlendMaskColor.Connect(beginmixedrealityblendmaskcolor_event_connections, () => {
		Log.Message("Handling BeginMixedRealityBlendMaskColor event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginmixedrealityblendmaskcolor_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginMixedRealityBlendMaskColor event with a handler function
publisher.EventBeginMixedRealityBlendMaskColor.Connect(beginmixedrealityblendmaskcolor_event_handler);

// remove subscription to the BeginMixedRealityBlendMaskColor event later by the handler function
publisher.EventBeginMixedRealityBlendMaskColor.Disconnect(beginmixedrealityblendmaskcolor_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginmixedrealityblendmaskcolor_event_connection;

// subscribe to the BeginMixedRealityBlendMaskColor event with a lambda handler function and keeping the connection
beginmixedrealityblendmaskcolor_event_connection = publisher.EventBeginMixedRealityBlendMaskColor.Connect(() => {
		Log.Message("Handling BeginMixedRealityBlendMaskColor event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginmixedrealityblendmaskcolor_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginmixedrealityblendmaskcolor_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginmixedrealityblendmaskcolor_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginMixedRealityBlendMaskColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginMixedRealityBlendMaskColor.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginMixedRealityBlendMaskColor.Enabled = true;

```

</details>

## 🔒︎ Event EventEndMixedRealityBlendMaskColor

The event triggered after the mask for Mixed Reality is rendered (after Common Camera for clouds and before Opacity GBuffer). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndMixedRealityBlendMaskColor event handler
void endmixedrealityblendmaskcolor_event_handler()
{
	Log.Message("\Handling EndMixedRealityBlendMaskColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endmixedrealityblendmaskcolor_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndMixedRealityBlendMaskColor.Connect(endmixedrealityblendmaskcolor_event_connections, endmixedrealityblendmaskcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndMixedRealityBlendMaskColor.Connect(endmixedrealityblendmaskcolor_event_connections, () => {
		Log.Message("Handling EndMixedRealityBlendMaskColor event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endmixedrealityblendmaskcolor_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndMixedRealityBlendMaskColor event with a handler function
publisher.EventEndMixedRealityBlendMaskColor.Connect(endmixedrealityblendmaskcolor_event_handler);

// remove subscription to the EndMixedRealityBlendMaskColor event later by the handler function
publisher.EventEndMixedRealityBlendMaskColor.Disconnect(endmixedrealityblendmaskcolor_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endmixedrealityblendmaskcolor_event_connection;

// subscribe to the EndMixedRealityBlendMaskColor event with a lambda handler function and keeping the connection
endmixedrealityblendmaskcolor_event_connection = publisher.EventEndMixedRealityBlendMaskColor.Connect(() => {
		Log.Message("Handling EndMixedRealityBlendMaskColor event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endmixedrealityblendmaskcolor_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endmixedrealityblendmaskcolor_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endmixedrealityblendmaskcolor_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndMixedRealityBlendMaskColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndMixedRealityBlendMaskColor.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndMixedRealityBlendMaskColor.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityGBuffer

The event triggered before filling the Gbuffer. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityGBuffer event handler
void beginopacitygbuffer_event_handler()
{
	Log.Message("\Handling BeginOpacityGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacitygbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginOpacityGBuffer.Connect(beginopacitygbuffer_event_connections, beginopacitygbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginOpacityGBuffer.Connect(beginopacitygbuffer_event_connections, () => {
		Log.Message("Handling BeginOpacityGBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacitygbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityGBuffer event with a handler function
publisher.EventBeginOpacityGBuffer.Connect(beginopacitygbuffer_event_handler);

// remove subscription to the BeginOpacityGBuffer event later by the handler function
publisher.EventBeginOpacityGBuffer.Disconnect(beginopacitygbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacitygbuffer_event_connection;

// subscribe to the BeginOpacityGBuffer event with a lambda handler function and keeping the connection
beginopacitygbuffer_event_connection = publisher.EventBeginOpacityGBuffer.Connect(() => {
		Log.Message("Handling BeginOpacityGBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacitygbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacitygbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacitygbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginOpacityGBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginOpacityGBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginAuxiliarySurfaces

The event triggered before auxiliary surfaces rendering. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginAuxiliarySurfaces event handler
void beginauxiliarysurfaces_event_handler()
{
	Log.Message("\Handling BeginAuxiliarySurfaces event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginauxiliarysurfaces_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Viewport.EventBeginAuxiliarySurfaces.Connect(beginauxiliarysurfaces_event_connections, beginauxiliarysurfaces_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Viewport.EventBeginAuxiliarySurfaces.Connect(beginauxiliarysurfaces_event_connections, () => {
		Log.Message("Handling BeginAuxiliarySurfaces event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginauxiliarysurfaces_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginAuxiliarySurfaces event with a handler function
Viewport.EventBeginAuxiliarySurfaces.Connect(beginauxiliarysurfaces_event_handler);

// remove subscription to the BeginAuxiliarySurfaces event later by the handler function
Viewport.EventBeginAuxiliarySurfaces.Disconnect(beginauxiliarysurfaces_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginauxiliarysurfaces_event_connection;

// subscribe to the BeginAuxiliarySurfaces event with a lambda handler function and keeping the connection
beginauxiliarysurfaces_event_connection = Viewport.EventBeginAuxiliarySurfaces.Connect(() => {
		Log.Message("Handling BeginAuxiliarySurfaces event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginauxiliarysurfaces_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginauxiliarysurfaces_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginauxiliarysurfaces_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginAuxiliarySurfaces events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Viewport.EventBeginAuxiliarySurfaces.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Viewport.EventBeginAuxiliarySurfaces.Enabled = true;

```

</details>

## 🔒︎ Event EventEndAuxiliarySurfaces

The event triggered after auxiliary surfaces rendering. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndAuxiliarySurfaces event handler
void endauxiliarysurfaces_event_handler()
{
	Log.Message("\Handling EndAuxiliarySurfaces event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endauxiliarysurfaces_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Viewport.EventEndAuxiliarySurfaces.Connect(endauxiliarysurfaces_event_connections, endauxiliarysurfaces_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Viewport.EventEndAuxiliarySurfaces.Connect(endauxiliarysurfaces_event_connections, () => {
		Log.Message("Handling EndAuxiliarySurfaces event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endauxiliarysurfaces_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndAuxiliarySurfaces event with a handler function
Viewport.EventEndAuxiliarySurfaces.Connect(endauxiliarysurfaces_event_handler);

// remove subscription to the EndAuxiliarySurfaces event later by the handler function
Viewport.EventEndAuxiliarySurfaces.Disconnect(endauxiliarysurfaces_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endauxiliarysurfaces_event_connection;

// subscribe to the EndAuxiliarySurfaces event with a lambda handler function and keeping the connection
endauxiliarysurfaces_event_connection = Viewport.EventEndAuxiliarySurfaces.Connect(() => {
		Log.Message("Handling EndAuxiliarySurfaces event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endauxiliarysurfaces_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endauxiliarysurfaces_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endauxiliarysurfaces_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndAuxiliarySurfaces events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Viewport.EventEndAuxiliarySurfaces.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Viewport.EventEndAuxiliarySurfaces.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityGBuffer

The event triggered after filling the Gbuffer. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityGBuffer event handler
void endopacitygbuffer_event_handler()
{
	Log.Message("\Handling EndOpacityGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacitygbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndOpacityGBuffer.Connect(endopacitygbuffer_event_connections, endopacitygbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndOpacityGBuffer.Connect(endopacitygbuffer_event_connections, () => {
		Log.Message("Handling EndOpacityGBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacitygbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityGBuffer event with a handler function
publisher.EventEndOpacityGBuffer.Connect(endopacitygbuffer_event_handler);

// remove subscription to the EndOpacityGBuffer event later by the handler function
publisher.EventEndOpacityGBuffer.Disconnect(endopacitygbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacitygbuffer_event_connection;

// subscribe to the EndOpacityGBuffer event with a lambda handler function and keeping the connection
endopacitygbuffer_event_connection = publisher.EventEndOpacityGBuffer.Connect(() => {
		Log.Message("Handling EndOpacityGBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacitygbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacitygbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacitygbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndOpacityGBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndOpacityGBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityDecals

The event triggered before the opacity decals rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityDecals event handler
void beginopacitydecals_event_handler()
{
	Log.Message("\Handling BeginOpacityDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacitydecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginOpacityDecals.Connect(beginopacitydecals_event_connections, beginopacitydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginOpacityDecals.Connect(beginopacitydecals_event_connections, () => {
		Log.Message("Handling BeginOpacityDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacitydecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityDecals event with a handler function
publisher.EventBeginOpacityDecals.Connect(beginopacitydecals_event_handler);

// remove subscription to the BeginOpacityDecals event later by the handler function
publisher.EventBeginOpacityDecals.Disconnect(beginopacitydecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacitydecals_event_connection;

// subscribe to the BeginOpacityDecals event with a lambda handler function and keeping the connection
beginopacitydecals_event_connection = publisher.EventBeginOpacityDecals.Connect(() => {
		Log.Message("Handling BeginOpacityDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacitydecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacitydecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacitydecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginOpacityDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginOpacityDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityDecals

The event triggered after the opacity decals rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityDecals event handler
void endopacitydecals_event_handler()
{
	Log.Message("\Handling EndOpacityDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacitydecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndOpacityDecals.Connect(endopacitydecals_event_connections, endopacitydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndOpacityDecals.Connect(endopacitydecals_event_connections, () => {
		Log.Message("Handling EndOpacityDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacitydecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityDecals event with a handler function
publisher.EventEndOpacityDecals.Connect(endopacitydecals_event_handler);

// remove subscription to the EndOpacityDecals event later by the handler function
publisher.EventEndOpacityDecals.Disconnect(endopacitydecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacitydecals_event_connection;

// subscribe to the EndOpacityDecals event with a lambda handler function and keeping the connection
endopacitydecals_event_connection = publisher.EventEndOpacityDecals.Connect(() => {
		Log.Message("Handling EndOpacityDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacitydecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacitydecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacitydecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndOpacityDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndOpacityDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginAuxiliaryDecals

The event triggered before the auxiliary decals rendering. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginAuxiliaryDecals event handler
void beginauxiliarydecals_event_handler()
{
	Log.Message("\Handling BeginAuxiliaryDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginauxiliarydecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Viewport.EventBeginAuxiliaryDecals.Connect(beginauxiliarydecals_event_connections, beginauxiliarydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Viewport.EventBeginAuxiliaryDecals.Connect(beginauxiliarydecals_event_connections, () => {
		Log.Message("Handling BeginAuxiliaryDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginauxiliarydecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginAuxiliaryDecals event with a handler function
Viewport.EventBeginAuxiliaryDecals.Connect(beginauxiliarydecals_event_handler);

// remove subscription to the BeginAuxiliaryDecals event later by the handler function
Viewport.EventBeginAuxiliaryDecals.Disconnect(beginauxiliarydecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginauxiliarydecals_event_connection;

// subscribe to the BeginAuxiliaryDecals event with a lambda handler function and keeping the connection
beginauxiliarydecals_event_connection = Viewport.EventBeginAuxiliaryDecals.Connect(() => {
		Log.Message("Handling BeginAuxiliaryDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginauxiliarydecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginauxiliarydecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginauxiliarydecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginAuxiliaryDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Viewport.EventBeginAuxiliaryDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Viewport.EventBeginAuxiliaryDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventEndAuxiliaryDecals

The event triggered after the auxiliary decals rendering. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndAuxiliaryDecals event handler
void endauxiliarydecals_event_handler()
{
	Log.Message("\Handling EndAuxiliaryDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endauxiliarydecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Viewport.EventEndAuxiliaryDecals.Connect(endauxiliarydecals_event_connections, endauxiliarydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Viewport.EventEndAuxiliaryDecals.Connect(endauxiliarydecals_event_connections, () => {
		Log.Message("Handling EndAuxiliaryDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endauxiliarydecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndAuxiliaryDecals event with a handler function
Viewport.EventEndAuxiliaryDecals.Connect(endauxiliarydecals_event_handler);

// remove subscription to the EndAuxiliaryDecals event later by the handler function
Viewport.EventEndAuxiliaryDecals.Disconnect(endauxiliarydecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endauxiliarydecals_event_connection;

// subscribe to the EndAuxiliaryDecals event with a lambda handler function and keeping the connection
endauxiliarydecals_event_connection = Viewport.EventEndAuxiliaryDecals.Connect(() => {
		Log.Message("Handling EndAuxiliaryDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endauxiliarydecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endauxiliarydecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endauxiliarydecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndAuxiliaryDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Viewport.EventEndAuxiliaryDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Viewport.EventEndAuxiliaryDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginCurvature

The event triggered before the [SSBevel](../../../editor2/settings/render_settings/ssbevel/index.md) effect rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginCurvature event handler
void begincurvature_event_handler()
{
	Log.Message("\Handling BeginCurvature event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincurvature_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginCurvature.Connect(begincurvature_event_connections, begincurvature_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginCurvature.Connect(begincurvature_event_connections, () => {
		Log.Message("Handling BeginCurvature event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begincurvature_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginCurvature event with a handler function
publisher.EventBeginCurvature.Connect(begincurvature_event_handler);

// remove subscription to the BeginCurvature event later by the handler function
publisher.EventBeginCurvature.Disconnect(begincurvature_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begincurvature_event_connection;

// subscribe to the BeginCurvature event with a lambda handler function and keeping the connection
begincurvature_event_connection = publisher.EventBeginCurvature.Connect(() => {
		Log.Message("Handling BeginCurvature event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begincurvature_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begincurvature_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begincurvature_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginCurvature events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginCurvature.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginCurvature.Enabled = true;

```

</details>

## 🔒︎ Event EventEndCurvature

The event triggered after the [SSBevel](../../../editor2/settings/render_settings/ssbevel/index.md) effect rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndCurvature event handler
void endcurvature_event_handler()
{
	Log.Message("\Handling EndCurvature event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcurvature_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndCurvature.Connect(endcurvature_event_connections, endcurvature_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndCurvature.Connect(endcurvature_event_connections, () => {
		Log.Message("Handling EndCurvature event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endcurvature_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndCurvature event with a handler function
publisher.EventEndCurvature.Connect(endcurvature_event_handler);

// remove subscription to the EndCurvature event later by the handler function
publisher.EventEndCurvature.Disconnect(endcurvature_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endcurvature_event_connection;

// subscribe to the EndCurvature event with a lambda handler function and keeping the connection
endcurvature_event_connection = publisher.EventEndCurvature.Connect(() => {
		Log.Message("Handling EndCurvature event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endcurvature_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endcurvature_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endcurvature_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndCurvature events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndCurvature.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndCurvature.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginCurvatureComposite

The event triggered before the curvature rendering stage for the [SSDirt](../../../editor2/settings/render_settings/ssdirt/index.md) effect. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginCurvatureComposite event handler
void begincurvaturecomposite_event_handler()
{
	Log.Message("\Handling BeginCurvatureComposite event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincurvaturecomposite_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginCurvatureComposite.Connect(begincurvaturecomposite_event_connections, begincurvaturecomposite_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginCurvatureComposite.Connect(begincurvaturecomposite_event_connections, () => {
		Log.Message("Handling BeginCurvatureComposite event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begincurvaturecomposite_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginCurvatureComposite event with a handler function
publisher.EventBeginCurvatureComposite.Connect(begincurvaturecomposite_event_handler);

// remove subscription to the BeginCurvatureComposite event later by the handler function
publisher.EventBeginCurvatureComposite.Disconnect(begincurvaturecomposite_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begincurvaturecomposite_event_connection;

// subscribe to the BeginCurvatureComposite event with a lambda handler function and keeping the connection
begincurvaturecomposite_event_connection = publisher.EventBeginCurvatureComposite.Connect(() => {
		Log.Message("Handling BeginCurvatureComposite event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begincurvaturecomposite_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begincurvaturecomposite_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begincurvaturecomposite_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginCurvatureComposite events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginCurvatureComposite.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginCurvatureComposite.Enabled = true;

```

</details>

## 🔒︎ Event EventEndCurvatureComposite

The event triggered after the curvature rendering stage for the [SSDirt](../../../editor2/settings/render_settings/ssdirt/index.md) effect. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndCurvatureComposite event handler
void endcurvaturecomposite_event_handler()
{
	Log.Message("\Handling EndCurvatureComposite event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcurvaturecomposite_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndCurvatureComposite.Connect(endcurvaturecomposite_event_connections, endcurvaturecomposite_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndCurvatureComposite.Connect(endcurvaturecomposite_event_connections, () => {
		Log.Message("Handling EndCurvatureComposite event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endcurvaturecomposite_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndCurvatureComposite event with a handler function
publisher.EventEndCurvatureComposite.Connect(endcurvaturecomposite_event_handler);

// remove subscription to the EndCurvatureComposite event later by the handler function
publisher.EventEndCurvatureComposite.Disconnect(endcurvaturecomposite_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endcurvaturecomposite_event_connection;

// subscribe to the EndCurvatureComposite event with a lambda handler function and keeping the connection
endcurvaturecomposite_event_connection = publisher.EventEndCurvatureComposite.Connect(() => {
		Log.Message("Handling EndCurvatureComposite event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endcurvaturecomposite_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endcurvaturecomposite_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endcurvaturecomposite_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndCurvatureComposite events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndCurvatureComposite.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndCurvatureComposite.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSRTGI

The event triggered before the SSRTGI rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSRTGI event handler
void beginssrtgi_event_handler()
{
	Log.Message("\Handling BeginSSRTGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssrtgi_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginSSRTGI.Connect(beginssrtgi_event_connections, beginssrtgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginSSRTGI.Connect(beginssrtgi_event_connections, () => {
		Log.Message("Handling BeginSSRTGI event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssrtgi_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSRTGI event with a handler function
publisher.EventBeginSSRTGI.Connect(beginssrtgi_event_handler);

// remove subscription to the BeginSSRTGI event later by the handler function
publisher.EventBeginSSRTGI.Disconnect(beginssrtgi_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssrtgi_event_connection;

// subscribe to the BeginSSRTGI event with a lambda handler function and keeping the connection
beginssrtgi_event_connection = publisher.EventBeginSSRTGI.Connect(() => {
		Log.Message("Handling BeginSSRTGI event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssrtgi_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssrtgi_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssrtgi_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSRTGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginSSRTGI.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginSSRTGI.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSRTGI

The event triggered after the SSRTGI rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSRTGI event handler
void endssrtgi_event_handler()
{
	Log.Message("\Handling EndSSRTGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssrtgi_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndSSRTGI.Connect(endssrtgi_event_connections, endssrtgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndSSRTGI.Connect(endssrtgi_event_connections, () => {
		Log.Message("Handling EndSSRTGI event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssrtgi_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSRTGI event with a handler function
publisher.EventEndSSRTGI.Connect(endssrtgi_event_handler);

// remove subscription to the EndSSRTGI event later by the handler function
publisher.EventEndSSRTGI.Disconnect(endssrtgi_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssrtgi_event_connection;

// subscribe to the EndSSRTGI event with a lambda handler function and keeping the connection
endssrtgi_event_connection = publisher.EventEndSSRTGI.Connect(() => {
		Log.Message("Handling EndSSRTGI event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssrtgi_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssrtgi_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssrtgi_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSRTGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndSSRTGI.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndSSRTGI.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityLights

The event triggered before the opacity lightgs rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityLights event handler
void beginopacitylights_event_handler()
{
	Log.Message("\Handling BeginOpacityLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacitylights_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginOpacityLights.Connect(beginopacitylights_event_connections, beginopacitylights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginOpacityLights.Connect(beginopacitylights_event_connections, () => {
		Log.Message("Handling BeginOpacityLights event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacitylights_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityLights event with a handler function
publisher.EventBeginOpacityLights.Connect(beginopacitylights_event_handler);

// remove subscription to the BeginOpacityLights event later by the handler function
publisher.EventBeginOpacityLights.Disconnect(beginopacitylights_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacitylights_event_connection;

// subscribe to the BeginOpacityLights event with a lambda handler function and keeping the connection
beginopacitylights_event_connection = publisher.EventBeginOpacityLights.Connect(() => {
		Log.Message("Handling BeginOpacityLights event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacitylights_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacitylights_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacitylights_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginOpacityLights.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginOpacityLights.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityLights

The event triggered after the opacity lightgs rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityLights event handler
void endopacitylights_event_handler()
{
	Log.Message("\Handling EndOpacityLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacitylights_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndOpacityLights.Connect(endopacitylights_event_connections, endopacitylights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndOpacityLights.Connect(endopacitylights_event_connections, () => {
		Log.Message("Handling EndOpacityLights event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacitylights_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityLights event with a handler function
publisher.EventEndOpacityLights.Connect(endopacitylights_event_handler);

// remove subscription to the EndOpacityLights event later by the handler function
publisher.EventEndOpacityLights.Disconnect(endopacitylights_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacitylights_event_connection;

// subscribe to the EndOpacityLights event with a lambda handler function and keeping the connection
endopacitylights_event_connection = publisher.EventEndOpacityLights.Connect(() => {
		Log.Message("Handling EndOpacityLights event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacitylights_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacitylights_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacitylights_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndOpacityLights.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndOpacityLights.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityVoxelProbes

The event triggered before the opacity voxel probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityVoxelProbes event handler
void beginopacityvoxelprobes_event_handler()
{
	Log.Message("\Handling BeginOpacityVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacityvoxelprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginOpacityVoxelProbes.Connect(beginopacityvoxelprobes_event_connections, beginopacityvoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginOpacityVoxelProbes.Connect(beginopacityvoxelprobes_event_connections, () => {
		Log.Message("Handling BeginOpacityVoxelProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacityvoxelprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityVoxelProbes event with a handler function
publisher.EventBeginOpacityVoxelProbes.Connect(beginopacityvoxelprobes_event_handler);

// remove subscription to the BeginOpacityVoxelProbes event later by the handler function
publisher.EventBeginOpacityVoxelProbes.Disconnect(beginopacityvoxelprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacityvoxelprobes_event_connection;

// subscribe to the BeginOpacityVoxelProbes event with a lambda handler function and keeping the connection
beginopacityvoxelprobes_event_connection = publisher.EventBeginOpacityVoxelProbes.Connect(() => {
		Log.Message("Handling BeginOpacityVoxelProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacityvoxelprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacityvoxelprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacityvoxelprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginOpacityVoxelProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginOpacityVoxelProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityVoxelProbes

The event triggered after the opacity voxel probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityVoxelProbes event handler
void endopacityvoxelprobes_event_handler()
{
	Log.Message("\Handling EndOpacityVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacityvoxelprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndOpacityVoxelProbes.Connect(endopacityvoxelprobes_event_connections, endopacityvoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndOpacityVoxelProbes.Connect(endopacityvoxelprobes_event_connections, () => {
		Log.Message("Handling EndOpacityVoxelProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacityvoxelprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityVoxelProbes event with a handler function
publisher.EventEndOpacityVoxelProbes.Connect(endopacityvoxelprobes_event_handler);

// remove subscription to the EndOpacityVoxelProbes event later by the handler function
publisher.EventEndOpacityVoxelProbes.Disconnect(endopacityvoxelprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacityvoxelprobes_event_connection;

// subscribe to the EndOpacityVoxelProbes event with a lambda handler function and keeping the connection
endopacityvoxelprobes_event_connection = publisher.EventEndOpacityVoxelProbes.Connect(() => {
		Log.Message("Handling EndOpacityVoxelProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacityvoxelprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacityvoxelprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacityvoxelprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndOpacityVoxelProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndOpacityVoxelProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityEnvironmentProbes

The event triggered before the opacity environment probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityEnvironmentProbes event handler
void beginopacityenvironmentprobes_event_handler()
{
	Log.Message("\Handling BeginOpacityEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacityenvironmentprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginOpacityEnvironmentProbes.Connect(beginopacityenvironmentprobes_event_connections, beginopacityenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginOpacityEnvironmentProbes.Connect(beginopacityenvironmentprobes_event_connections, () => {
		Log.Message("Handling BeginOpacityEnvironmentProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacityenvironmentprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityEnvironmentProbes event with a handler function
publisher.EventBeginOpacityEnvironmentProbes.Connect(beginopacityenvironmentprobes_event_handler);

// remove subscription to the BeginOpacityEnvironmentProbes event later by the handler function
publisher.EventBeginOpacityEnvironmentProbes.Disconnect(beginopacityenvironmentprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacityenvironmentprobes_event_connection;

// subscribe to the BeginOpacityEnvironmentProbes event with a lambda handler function and keeping the connection
beginopacityenvironmentprobes_event_connection = publisher.EventBeginOpacityEnvironmentProbes.Connect(() => {
		Log.Message("Handling BeginOpacityEnvironmentProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacityenvironmentprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacityenvironmentprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacityenvironmentprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginOpacityEnvironmentProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginOpacityEnvironmentProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityEnvironmentProbes

The event triggered after the opacity environment probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityEnvironmentProbes event handler
void endopacityenvironmentprobes_event_handler()
{
	Log.Message("\Handling EndOpacityEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacityenvironmentprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndOpacityEnvironmentProbes.Connect(endopacityenvironmentprobes_event_connections, endopacityenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndOpacityEnvironmentProbes.Connect(endopacityenvironmentprobes_event_connections, () => {
		Log.Message("Handling EndOpacityEnvironmentProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacityenvironmentprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityEnvironmentProbes event with a handler function
publisher.EventEndOpacityEnvironmentProbes.Connect(endopacityenvironmentprobes_event_handler);

// remove subscription to the EndOpacityEnvironmentProbes event later by the handler function
publisher.EventEndOpacityEnvironmentProbes.Disconnect(endopacityenvironmentprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacityenvironmentprobes_event_connection;

// subscribe to the EndOpacityEnvironmentProbes event with a lambda handler function and keeping the connection
endopacityenvironmentprobes_event_connection = publisher.EventEndOpacityEnvironmentProbes.Connect(() => {
		Log.Message("Handling EndOpacityEnvironmentProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacityenvironmentprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacityenvironmentprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacityenvironmentprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndOpacityEnvironmentProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndOpacityEnvironmentProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityPlanarProbes

The event triggered before the opacity planar probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityPlanarProbes event handler
void beginopacityplanarprobes_event_handler()
{
	Log.Message("\Handling BeginOpacityPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacityplanarprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginOpacityPlanarProbes.Connect(beginopacityplanarprobes_event_connections, beginopacityplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginOpacityPlanarProbes.Connect(beginopacityplanarprobes_event_connections, () => {
		Log.Message("Handling BeginOpacityPlanarProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacityplanarprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityPlanarProbes event with a handler function
publisher.EventBeginOpacityPlanarProbes.Connect(beginopacityplanarprobes_event_handler);

// remove subscription to the BeginOpacityPlanarProbes event later by the handler function
publisher.EventBeginOpacityPlanarProbes.Disconnect(beginopacityplanarprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacityplanarprobes_event_connection;

// subscribe to the BeginOpacityPlanarProbes event with a lambda handler function and keeping the connection
beginopacityplanarprobes_event_connection = publisher.EventBeginOpacityPlanarProbes.Connect(() => {
		Log.Message("Handling BeginOpacityPlanarProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacityplanarprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacityplanarprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacityplanarprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginOpacityPlanarProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginOpacityPlanarProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityPlanarProbes

The event triggered after the opacity planar probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityPlanarProbes event handler
void endopacityplanarprobes_event_handler()
{
	Log.Message("\Handling EndOpacityPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacityplanarprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndOpacityPlanarProbes.Connect(endopacityplanarprobes_event_connections, endopacityplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndOpacityPlanarProbes.Connect(endopacityplanarprobes_event_connections, () => {
		Log.Message("Handling EndOpacityPlanarProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacityplanarprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityPlanarProbes event with a handler function
publisher.EventEndOpacityPlanarProbes.Connect(endopacityplanarprobes_event_handler);

// remove subscription to the EndOpacityPlanarProbes event later by the handler function
publisher.EventEndOpacityPlanarProbes.Disconnect(endopacityplanarprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacityplanarprobes_event_connection;

// subscribe to the EndOpacityPlanarProbes event with a lambda handler function and keeping the connection
endopacityplanarprobes_event_connection = publisher.EventEndOpacityPlanarProbes.Connect(() => {
		Log.Message("Handling EndOpacityPlanarProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacityplanarprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacityplanarprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacityplanarprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndOpacityPlanarProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndOpacityPlanarProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginRefractionBuffer

The event triggered before filling the refraction buffer. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginRefractionBuffer event handler
void beginrefractionbuffer_event_handler()
{
	Log.Message("\Handling BeginRefractionBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginrefractionbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginRefractionBuffer.Connect(beginrefractionbuffer_event_connections, beginrefractionbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginRefractionBuffer.Connect(beginrefractionbuffer_event_connections, () => {
		Log.Message("Handling BeginRefractionBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginrefractionbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginRefractionBuffer event with a handler function
publisher.EventBeginRefractionBuffer.Connect(beginrefractionbuffer_event_handler);

// remove subscription to the BeginRefractionBuffer event later by the handler function
publisher.EventBeginRefractionBuffer.Disconnect(beginrefractionbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginrefractionbuffer_event_connection;

// subscribe to the BeginRefractionBuffer event with a lambda handler function and keeping the connection
beginrefractionbuffer_event_connection = publisher.EventBeginRefractionBuffer.Connect(() => {
		Log.Message("Handling BeginRefractionBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginrefractionbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginrefractionbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginrefractionbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginRefractionBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginRefractionBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginRefractionBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndRefractionBuffer

The event triggered after filling the refraction buffer. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndRefractionBuffer event handler
void endrefractionbuffer_event_handler()
{
	Log.Message("\Handling EndRefractionBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endrefractionbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndRefractionBuffer.Connect(endrefractionbuffer_event_connections, endrefractionbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndRefractionBuffer.Connect(endrefractionbuffer_event_connections, () => {
		Log.Message("Handling EndRefractionBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endrefractionbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndRefractionBuffer event with a handler function
publisher.EventEndRefractionBuffer.Connect(endrefractionbuffer_event_handler);

// remove subscription to the EndRefractionBuffer event later by the handler function
publisher.EventEndRefractionBuffer.Disconnect(endrefractionbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endrefractionbuffer_event_connection;

// subscribe to the EndRefractionBuffer event with a lambda handler function and keeping the connection
endrefractionbuffer_event_connection = publisher.EventEndRefractionBuffer.Connect(() => {
		Log.Message("Handling EndRefractionBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endrefractionbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endrefractionbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endrefractionbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndRefractionBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndRefractionBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndRefractionBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginTransparentBlurBuffer

The event triggered before filling the transparent blur buffer. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginTransparentBlurBuffer event handler
void begintransparentblurbuffer_event_handler()
{
	Log.Message("\Handling BeginTransparentBlurBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begintransparentblurbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginTransparentBlurBuffer.Connect(begintransparentblurbuffer_event_connections, begintransparentblurbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginTransparentBlurBuffer.Connect(begintransparentblurbuffer_event_connections, () => {
		Log.Message("Handling BeginTransparentBlurBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begintransparentblurbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginTransparentBlurBuffer event with a handler function
publisher.EventBeginTransparentBlurBuffer.Connect(begintransparentblurbuffer_event_handler);

// remove subscription to the BeginTransparentBlurBuffer event later by the handler function
publisher.EventBeginTransparentBlurBuffer.Disconnect(begintransparentblurbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begintransparentblurbuffer_event_connection;

// subscribe to the BeginTransparentBlurBuffer event with a lambda handler function and keeping the connection
begintransparentblurbuffer_event_connection = publisher.EventBeginTransparentBlurBuffer.Connect(() => {
		Log.Message("Handling BeginTransparentBlurBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begintransparentblurbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begintransparentblurbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begintransparentblurbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginTransparentBlurBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginTransparentBlurBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginTransparentBlurBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndTransparentBlurBuffer

The event triggered after filling the transparent blur buffer. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndTransparentBlurBuffer event handler
void endtransparentblurbuffer_event_handler()
{
	Log.Message("\Handling EndTransparentBlurBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endtransparentblurbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndTransparentBlurBuffer.Connect(endtransparentblurbuffer_event_connections, endtransparentblurbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndTransparentBlurBuffer.Connect(endtransparentblurbuffer_event_connections, () => {
		Log.Message("Handling EndTransparentBlurBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endtransparentblurbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndTransparentBlurBuffer event with a handler function
publisher.EventEndTransparentBlurBuffer.Connect(endtransparentblurbuffer_event_handler);

// remove subscription to the EndTransparentBlurBuffer event later by the handler function
publisher.EventEndTransparentBlurBuffer.Disconnect(endtransparentblurbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endtransparentblurbuffer_event_connection;

// subscribe to the EndTransparentBlurBuffer event with a lambda handler function and keeping the connection
endtransparentblurbuffer_event_connection = publisher.EventEndTransparentBlurBuffer.Connect(() => {
		Log.Message("Handling EndTransparentBlurBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endtransparentblurbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endtransparentblurbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endtransparentblurbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndTransparentBlurBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndTransparentBlurBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndTransparentBlurBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSSS

The event triggered before the Screen-Space Shadow Shafts rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSSS event handler
void beginssss_event_handler()
{
	Log.Message("\Handling BeginSSSS event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssss_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginSSSS.Connect(beginssss_event_connections, beginssss_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginSSSS.Connect(beginssss_event_connections, () => {
		Log.Message("Handling BeginSSSS event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssss_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSSS event with a handler function
publisher.EventBeginSSSS.Connect(beginssss_event_handler);

// remove subscription to the BeginSSSS event later by the handler function
publisher.EventBeginSSSS.Disconnect(beginssss_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssss_event_connection;

// subscribe to the BeginSSSS event with a lambda handler function and keeping the connection
beginssss_event_connection = publisher.EventBeginSSSS.Connect(() => {
		Log.Message("Handling BeginSSSS event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssss_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssss_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssss_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSSS events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginSSSS.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginSSSS.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSSS

The event triggered after the Screen-Space Shadow Shafts rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSSS event handler
void endssss_event_handler()
{
	Log.Message("\Handling EndSSSS event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssss_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndSSSS.Connect(endssss_event_connections, endssss_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndSSSS.Connect(endssss_event_connections, () => {
		Log.Message("Handling EndSSSS event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssss_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSSS event with a handler function
publisher.EventEndSSSS.Connect(endssss_event_handler);

// remove subscription to the EndSSSS event later by the handler function
publisher.EventEndSSSS.Disconnect(endssss_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssss_event_connection;

// subscribe to the EndSSSS event with a lambda handler function and keeping the connection
endssss_event_connection = publisher.EventEndSSSS.Connect(() => {
		Log.Message("Handling EndSSSS event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssss_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssss_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssss_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSSS events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndSSSS.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndSSSS.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSR

The event triggered before the SSR rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSR event handler
void beginssr_event_handler()
{
	Log.Message("\Handling BeginSSR event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssr_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginSSR.Connect(beginssr_event_connections, beginssr_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginSSR.Connect(beginssr_event_connections, () => {
		Log.Message("Handling BeginSSR event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssr_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSR event with a handler function
publisher.EventBeginSSR.Connect(beginssr_event_handler);

// remove subscription to the BeginSSR event later by the handler function
publisher.EventBeginSSR.Disconnect(beginssr_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssr_event_connection;

// subscribe to the BeginSSR event with a lambda handler function and keeping the connection
beginssr_event_connection = publisher.EventBeginSSR.Connect(() => {
		Log.Message("Handling BeginSSR event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssr_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssr_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssr_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSR events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginSSR.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginSSR.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSR

The event triggered after the SSR rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSR event handler
void endssr_event_handler()
{
	Log.Message("\Handling EndSSR event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssr_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndSSR.Connect(endssr_event_connections, endssr_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndSSR.Connect(endssr_event_connections, () => {
		Log.Message("Handling EndSSR event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssr_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSR event with a handler function
publisher.EventEndSSR.Connect(endssr_event_handler);

// remove subscription to the EndSSR event later by the handler function
publisher.EventEndSSR.Disconnect(endssr_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssr_event_connection;

// subscribe to the EndSSR event with a lambda handler function and keeping the connection
endssr_event_connection = publisher.EventEndSSR.Connect(() => {
		Log.Message("Handling EndSSR event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssr_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssr_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssr_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSR events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndSSR.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndSSR.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSAO

The event triggered before the SSAO rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSAO event handler
void beginssao_event_handler()
{
	Log.Message("\Handling BeginSSAO event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssao_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginSSAO.Connect(beginssao_event_connections, beginssao_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginSSAO.Connect(beginssao_event_connections, () => {
		Log.Message("Handling BeginSSAO event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssao_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSAO event with a handler function
publisher.EventBeginSSAO.Connect(beginssao_event_handler);

// remove subscription to the BeginSSAO event later by the handler function
publisher.EventBeginSSAO.Disconnect(beginssao_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssao_event_connection;

// subscribe to the BeginSSAO event with a lambda handler function and keeping the connection
beginssao_event_connection = publisher.EventBeginSSAO.Connect(() => {
		Log.Message("Handling BeginSSAO event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssao_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssao_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssao_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSAO events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginSSAO.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginSSAO.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSAO

The event triggered after the SSAO rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSAO event handler
void endssao_event_handler()
{
	Log.Message("\Handling EndSSAO event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssao_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndSSAO.Connect(endssao_event_connections, endssao_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndSSAO.Connect(endssao_event_connections, () => {
		Log.Message("Handling EndSSAO event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssao_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSAO event with a handler function
publisher.EventEndSSAO.Connect(endssao_event_handler);

// remove subscription to the EndSSAO event later by the handler function
publisher.EventEndSSAO.Disconnect(endssao_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssao_event_connection;

// subscribe to the EndSSAO event with a lambda handler function and keeping the connection
endssao_event_connection = publisher.EventEndSSAO.Connect(() => {
		Log.Message("Handling EndSSAO event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssao_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssao_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssao_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSAO events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndSSAO.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndSSAO.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSGI

The event triggered before the SSGI rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSGI event handler
void beginssgi_event_handler()
{
	Log.Message("\Handling BeginSSGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssgi_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginSSGI.Connect(beginssgi_event_connections, beginssgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginSSGI.Connect(beginssgi_event_connections, () => {
		Log.Message("Handling BeginSSGI event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssgi_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSGI event with a handler function
publisher.EventBeginSSGI.Connect(beginssgi_event_handler);

// remove subscription to the BeginSSGI event later by the handler function
publisher.EventBeginSSGI.Disconnect(beginssgi_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssgi_event_connection;

// subscribe to the BeginSSGI event with a lambda handler function and keeping the connection
beginssgi_event_connection = publisher.EventBeginSSGI.Connect(() => {
		Log.Message("Handling BeginSSGI event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssgi_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssgi_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssgi_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginSSGI.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginSSGI.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSGI

The event triggered after the SSGI rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSGI event handler
void endssgi_event_handler()
{
	Log.Message("\Handling EndSSGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssgi_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndSSGI.Connect(endssgi_event_connections, endssgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndSSGI.Connect(endssgi_event_connections, () => {
		Log.Message("Handling EndSSGI event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssgi_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSGI event with a handler function
publisher.EventEndSSGI.Connect(endssgi_event_handler);

// remove subscription to the EndSSGI event later by the handler function
publisher.EventEndSSGI.Disconnect(endssgi_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssgi_event_connection;

// subscribe to the EndSSGI event with a lambda handler function and keeping the connection
endssgi_event_connection = publisher.EventEndSSGI.Connect(() => {
		Log.Message("Handling EndSSGI event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssgi_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssgi_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssgi_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndSSGI.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndSSGI.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSky

The event triggered before the sky rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSky event handler
void beginsky_event_handler()
{
	Log.Message("\Handling BeginSky event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsky_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginSky.Connect(beginsky_event_connections, beginsky_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginSky.Connect(beginsky_event_connections, () => {
		Log.Message("Handling BeginSky event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsky_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSky event with a handler function
publisher.EventBeginSky.Connect(beginsky_event_handler);

// remove subscription to the BeginSky event later by the handler function
publisher.EventBeginSky.Disconnect(beginsky_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsky_event_connection;

// subscribe to the BeginSky event with a lambda handler function and keeping the connection
beginsky_event_connection = publisher.EventBeginSky.Connect(() => {
		Log.Message("Handling BeginSky event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsky_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsky_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsky_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSky events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginSky.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginSky.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSky

The event triggered after the sky rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSky event handler
void endsky_event_handler()
{
	Log.Message("\Handling EndSky event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsky_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndSky.Connect(endsky_event_connections, endsky_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndSky.Connect(endsky_event_connections, () => {
		Log.Message("Handling EndSky event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsky_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSky event with a handler function
publisher.EventEndSky.Connect(endsky_event_handler);

// remove subscription to the EndSky event later by the handler function
publisher.EventEndSky.Disconnect(endsky_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsky_event_connection;

// subscribe to the EndSky event with a lambda handler function and keeping the connection
endsky_event_connection = publisher.EventEndSky.Connect(() => {
		Log.Message("Handling EndSky event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsky_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsky_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsky_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSky events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndSky.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndSky.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginCompositeDeferred

The event triggered before the clouds deferred composite stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginCompositeDeferred event handler
void begincompositedeferred_event_handler()
{
	Log.Message("\Handling BeginCompositeDeferred event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincompositedeferred_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginCompositeDeferred.Connect(begincompositedeferred_event_connections, begincompositedeferred_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginCompositeDeferred.Connect(begincompositedeferred_event_connections, () => {
		Log.Message("Handling BeginCompositeDeferred event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begincompositedeferred_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginCompositeDeferred event with a handler function
publisher.EventBeginCompositeDeferred.Connect(begincompositedeferred_event_handler);

// remove subscription to the BeginCompositeDeferred event later by the handler function
publisher.EventBeginCompositeDeferred.Disconnect(begincompositedeferred_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begincompositedeferred_event_connection;

// subscribe to the BeginCompositeDeferred event with a lambda handler function and keeping the connection
begincompositedeferred_event_connection = publisher.EventBeginCompositeDeferred.Connect(() => {
		Log.Message("Handling BeginCompositeDeferred event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begincompositedeferred_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begincompositedeferred_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begincompositedeferred_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginCompositeDeferred events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginCompositeDeferred.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginCompositeDeferred.Enabled = true;

```

</details>

## 🔒︎ Event EventEndCompositeDeferred

The event triggered after the clouds deferred composite stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndCompositeDeferred event handler
void endcompositedeferred_event_handler()
{
	Log.Message("\Handling EndCompositeDeferred event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcompositedeferred_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndCompositeDeferred.Connect(endcompositedeferred_event_connections, endcompositedeferred_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndCompositeDeferred.Connect(endcompositedeferred_event_connections, () => {
		Log.Message("Handling EndCompositeDeferred event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endcompositedeferred_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndCompositeDeferred event with a handler function
publisher.EventEndCompositeDeferred.Connect(endcompositedeferred_event_handler);

// remove subscription to the EndCompositeDeferred event later by the handler function
publisher.EventEndCompositeDeferred.Disconnect(endcompositedeferred_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endcompositedeferred_event_connection;

// subscribe to the EndCompositeDeferred event with a lambda handler function and keeping the connection
endcompositedeferred_event_connection = publisher.EventEndCompositeDeferred.Connect(() => {
		Log.Message("Handling EndCompositeDeferred event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endcompositedeferred_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endcompositedeferred_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endcompositedeferred_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndCompositeDeferred events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndCompositeDeferred.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndCompositeDeferred.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginTransparent

The event triggered before the transparent objects rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginTransparent event handler
void begintransparent_event_handler()
{
	Log.Message("\Handling BeginTransparent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begintransparent_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginTransparent.Connect(begintransparent_event_connections, begintransparent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginTransparent.Connect(begintransparent_event_connections, () => {
		Log.Message("Handling BeginTransparent event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begintransparent_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginTransparent event with a handler function
publisher.EventBeginTransparent.Connect(begintransparent_event_handler);

// remove subscription to the BeginTransparent event later by the handler function
publisher.EventBeginTransparent.Disconnect(begintransparent_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begintransparent_event_connection;

// subscribe to the BeginTransparent event with a lambda handler function and keeping the connection
begintransparent_event_connection = publisher.EventBeginTransparent.Connect(() => {
		Log.Message("Handling BeginTransparent event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begintransparent_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begintransparent_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begintransparent_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginTransparent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginTransparent.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginTransparent.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginClouds

The event triggered before the clouds rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginClouds event handler
void beginclouds_event_handler()
{
	Log.Message("\Handling BeginClouds event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginclouds_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginClouds.Connect(beginclouds_event_connections, beginclouds_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginClouds.Connect(beginclouds_event_connections, () => {
		Log.Message("Handling BeginClouds event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginclouds_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginClouds event with a handler function
publisher.EventBeginClouds.Connect(beginclouds_event_handler);

// remove subscription to the BeginClouds event later by the handler function
publisher.EventBeginClouds.Disconnect(beginclouds_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginclouds_event_connection;

// subscribe to the BeginClouds event with a lambda handler function and keeping the connection
beginclouds_event_connection = publisher.EventBeginClouds.Connect(() => {
		Log.Message("Handling BeginClouds event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginclouds_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginclouds_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginclouds_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginClouds events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginClouds.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginClouds.Enabled = true;

```

</details>

## 🔒︎ Event EventEndClouds

The event triggered after the clouds rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndClouds event handler
void endclouds_event_handler()
{
	Log.Message("\Handling EndClouds event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endclouds_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndClouds.Connect(endclouds_event_connections, endclouds_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndClouds.Connect(endclouds_event_connections, () => {
		Log.Message("Handling EndClouds event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endclouds_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndClouds event with a handler function
publisher.EventEndClouds.Connect(endclouds_event_handler);

// remove subscription to the EndClouds event later by the handler function
publisher.EventEndClouds.Disconnect(endclouds_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endclouds_event_connection;

// subscribe to the EndClouds event with a lambda handler function and keeping the connection
endclouds_event_connection = publisher.EventEndClouds.Connect(() => {
		Log.Message("Handling EndClouds event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endclouds_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endclouds_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endclouds_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndClouds events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndClouds.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndClouds.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWater

The event triggered before the water rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWater event handler
void beginwater_event_handler()
{
	Log.Message("\Handling BeginWater event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwater_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginWater.Connect(beginwater_event_connections, beginwater_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginWater.Connect(beginwater_event_connections, () => {
		Log.Message("Handling BeginWater event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwater_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWater event with a handler function
publisher.EventBeginWater.Connect(beginwater_event_handler);

// remove subscription to the BeginWater event later by the handler function
publisher.EventBeginWater.Disconnect(beginwater_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwater_event_connection;

// subscribe to the BeginWater event with a lambda handler function and keeping the connection
beginwater_event_connection = publisher.EventBeginWater.Connect(() => {
		Log.Message("Handling BeginWater event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwater_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwater_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwater_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWater events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginWater.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginWater.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterGBuffer

The event triggered before the Water G-Buffer rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterGBuffer event handler
void beginwatergbuffer_event_handler()
{
	Log.Message("\Handling BeginWaterGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwatergbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginWaterGBuffer.Connect(beginwatergbuffer_event_connections, beginwatergbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginWaterGBuffer.Connect(beginwatergbuffer_event_connections, () => {
		Log.Message("Handling BeginWaterGBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwatergbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterGBuffer event with a handler function
publisher.EventBeginWaterGBuffer.Connect(beginwatergbuffer_event_handler);

// remove subscription to the BeginWaterGBuffer event later by the handler function
publisher.EventBeginWaterGBuffer.Disconnect(beginwatergbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwatergbuffer_event_connection;

// subscribe to the BeginWaterGBuffer event with a lambda handler function and keeping the connection
beginwatergbuffer_event_connection = publisher.EventBeginWaterGBuffer.Connect(() => {
		Log.Message("Handling BeginWaterGBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwatergbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwatergbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwatergbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginWaterGBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginWaterGBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterGBuffer

The event triggered after the Water G-Buffer rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterGBuffer event handler
void endwatergbuffer_event_handler()
{
	Log.Message("\Handling EndWaterGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwatergbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndWaterGBuffer.Connect(endwatergbuffer_event_connections, endwatergbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndWaterGBuffer.Connect(endwatergbuffer_event_connections, () => {
		Log.Message("Handling EndWaterGBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwatergbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterGBuffer event with a handler function
publisher.EventEndWaterGBuffer.Connect(endwatergbuffer_event_handler);

// remove subscription to the EndWaterGBuffer event later by the handler function
publisher.EventEndWaterGBuffer.Disconnect(endwatergbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwatergbuffer_event_connection;

// subscribe to the EndWaterGBuffer event with a lambda handler function and keeping the connection
endwatergbuffer_event_connection = publisher.EventEndWaterGBuffer.Connect(() => {
		Log.Message("Handling EndWaterGBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwatergbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwatergbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwatergbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndWaterGBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndWaterGBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterDecals

The event triggered before the water decals rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterDecals event handler
void beginwaterdecals_event_handler()
{
	Log.Message("\Handling BeginWaterDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterdecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginWaterDecals.Connect(beginwaterdecals_event_connections, beginwaterdecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginWaterDecals.Connect(beginwaterdecals_event_connections, () => {
		Log.Message("Handling BeginWaterDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwaterdecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterDecals event with a handler function
publisher.EventBeginWaterDecals.Connect(beginwaterdecals_event_handler);

// remove subscription to the BeginWaterDecals event later by the handler function
publisher.EventBeginWaterDecals.Disconnect(beginwaterdecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwaterdecals_event_connection;

// subscribe to the BeginWaterDecals event with a lambda handler function and keeping the connection
beginwaterdecals_event_connection = publisher.EventBeginWaterDecals.Connect(() => {
		Log.Message("Handling BeginWaterDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwaterdecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwaterdecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwaterdecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginWaterDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginWaterDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterDecals

The event triggered after the water decals rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterDecals event handler
void endwaterdecals_event_handler()
{
	Log.Message("\Handling EndWaterDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterdecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndWaterDecals.Connect(endwaterdecals_event_connections, endwaterdecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndWaterDecals.Connect(endwaterdecals_event_connections, () => {
		Log.Message("Handling EndWaterDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwaterdecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterDecals event with a handler function
publisher.EventEndWaterDecals.Connect(endwaterdecals_event_handler);

// remove subscription to the EndWaterDecals event later by the handler function
publisher.EventEndWaterDecals.Disconnect(endwaterdecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwaterdecals_event_connection;

// subscribe to the EndWaterDecals event with a lambda handler function and keeping the connection
endwaterdecals_event_connection = publisher.EventEndWaterDecals.Connect(() => {
		Log.Message("Handling EndWaterDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwaterdecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwaterdecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwaterdecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndWaterDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndWaterDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterLights

The event triggered before the water lights rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterLights event handler
void beginwaterlights_event_handler()
{
	Log.Message("\Handling BeginWaterLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterlights_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginWaterLights.Connect(beginwaterlights_event_connections, beginwaterlights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginWaterLights.Connect(beginwaterlights_event_connections, () => {
		Log.Message("Handling BeginWaterLights event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwaterlights_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterLights event with a handler function
publisher.EventBeginWaterLights.Connect(beginwaterlights_event_handler);

// remove subscription to the BeginWaterLights event later by the handler function
publisher.EventBeginWaterLights.Disconnect(beginwaterlights_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwaterlights_event_connection;

// subscribe to the BeginWaterLights event with a lambda handler function and keeping the connection
beginwaterlights_event_connection = publisher.EventBeginWaterLights.Connect(() => {
		Log.Message("Handling BeginWaterLights event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwaterlights_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwaterlights_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwaterlights_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginWaterLights.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginWaterLights.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterLights

The event triggered after the water lights rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterLights event handler
void endwaterlights_event_handler()
{
	Log.Message("\Handling EndWaterLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterlights_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndWaterLights.Connect(endwaterlights_event_connections, endwaterlights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndWaterLights.Connect(endwaterlights_event_connections, () => {
		Log.Message("Handling EndWaterLights event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwaterlights_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterLights event with a handler function
publisher.EventEndWaterLights.Connect(endwaterlights_event_handler);

// remove subscription to the EndWaterLights event later by the handler function
publisher.EventEndWaterLights.Disconnect(endwaterlights_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwaterlights_event_connection;

// subscribe to the EndWaterLights event with a lambda handler function and keeping the connection
endwaterlights_event_connection = publisher.EventEndWaterLights.Connect(() => {
		Log.Message("Handling EndWaterLights event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwaterlights_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwaterlights_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwaterlights_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndWaterLights.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndWaterLights.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterVoxelProbes

The event triggered before the water voxel probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterVoxelProbes event handler
void beginwatervoxelprobes_event_handler()
{
	Log.Message("\Handling BeginWaterVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwatervoxelprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginWaterVoxelProbes.Connect(beginwatervoxelprobes_event_connections, beginwatervoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginWaterVoxelProbes.Connect(beginwatervoxelprobes_event_connections, () => {
		Log.Message("Handling BeginWaterVoxelProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwatervoxelprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterVoxelProbes event with a handler function
publisher.EventBeginWaterVoxelProbes.Connect(beginwatervoxelprobes_event_handler);

// remove subscription to the BeginWaterVoxelProbes event later by the handler function
publisher.EventBeginWaterVoxelProbes.Disconnect(beginwatervoxelprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwatervoxelprobes_event_connection;

// subscribe to the BeginWaterVoxelProbes event with a lambda handler function and keeping the connection
beginwatervoxelprobes_event_connection = publisher.EventBeginWaterVoxelProbes.Connect(() => {
		Log.Message("Handling BeginWaterVoxelProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwatervoxelprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwatervoxelprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwatervoxelprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginWaterVoxelProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginWaterVoxelProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterVoxelProbes

The event triggered after the water voxel probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterVoxelProbes event handler
void endwatervoxelprobes_event_handler()
{
	Log.Message("\Handling EndWaterVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwatervoxelprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndWaterVoxelProbes.Connect(endwatervoxelprobes_event_connections, endwatervoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndWaterVoxelProbes.Connect(endwatervoxelprobes_event_connections, () => {
		Log.Message("Handling EndWaterVoxelProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwatervoxelprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterVoxelProbes event with a handler function
publisher.EventEndWaterVoxelProbes.Connect(endwatervoxelprobes_event_handler);

// remove subscription to the EndWaterVoxelProbes event later by the handler function
publisher.EventEndWaterVoxelProbes.Disconnect(endwatervoxelprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwatervoxelprobes_event_connection;

// subscribe to the EndWaterVoxelProbes event with a lambda handler function and keeping the connection
endwatervoxelprobes_event_connection = publisher.EventEndWaterVoxelProbes.Connect(() => {
		Log.Message("Handling EndWaterVoxelProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwatervoxelprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwatervoxelprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwatervoxelprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndWaterVoxelProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndWaterVoxelProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterEnvironmentProbes

The event triggered before the water environment probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterEnvironmentProbes event handler
void beginwaterenvironmentprobes_event_handler()
{
	Log.Message("\Handling BeginWaterEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterenvironmentprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginWaterEnvironmentProbes.Connect(beginwaterenvironmentprobes_event_connections, beginwaterenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginWaterEnvironmentProbes.Connect(beginwaterenvironmentprobes_event_connections, () => {
		Log.Message("Handling BeginWaterEnvironmentProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwaterenvironmentprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterEnvironmentProbes event with a handler function
publisher.EventBeginWaterEnvironmentProbes.Connect(beginwaterenvironmentprobes_event_handler);

// remove subscription to the BeginWaterEnvironmentProbes event later by the handler function
publisher.EventBeginWaterEnvironmentProbes.Disconnect(beginwaterenvironmentprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwaterenvironmentprobes_event_connection;

// subscribe to the BeginWaterEnvironmentProbes event with a lambda handler function and keeping the connection
beginwaterenvironmentprobes_event_connection = publisher.EventBeginWaterEnvironmentProbes.Connect(() => {
		Log.Message("Handling BeginWaterEnvironmentProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwaterenvironmentprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwaterenvironmentprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwaterenvironmentprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginWaterEnvironmentProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginWaterEnvironmentProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterEnvironmentProbes

The event triggered after the water environment probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterEnvironmentProbes event handler
void endwaterenvironmentprobes_event_handler()
{
	Log.Message("\Handling EndWaterEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterenvironmentprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndWaterEnvironmentProbes.Connect(endwaterenvironmentprobes_event_connections, endwaterenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndWaterEnvironmentProbes.Connect(endwaterenvironmentprobes_event_connections, () => {
		Log.Message("Handling EndWaterEnvironmentProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwaterenvironmentprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterEnvironmentProbes event with a handler function
publisher.EventEndWaterEnvironmentProbes.Connect(endwaterenvironmentprobes_event_handler);

// remove subscription to the EndWaterEnvironmentProbes event later by the handler function
publisher.EventEndWaterEnvironmentProbes.Disconnect(endwaterenvironmentprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwaterenvironmentprobes_event_connection;

// subscribe to the EndWaterEnvironmentProbes event with a lambda handler function and keeping the connection
endwaterenvironmentprobes_event_connection = publisher.EventEndWaterEnvironmentProbes.Connect(() => {
		Log.Message("Handling EndWaterEnvironmentProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwaterenvironmentprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwaterenvironmentprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwaterenvironmentprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndWaterEnvironmentProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndWaterEnvironmentProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterPlanarProbes

The event triggered before the water planar probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterPlanarProbes event handler
void beginwaterplanarprobes_event_handler()
{
	Log.Message("\Handling BeginWaterPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterplanarprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginWaterPlanarProbes.Connect(beginwaterplanarprobes_event_connections, beginwaterplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginWaterPlanarProbes.Connect(beginwaterplanarprobes_event_connections, () => {
		Log.Message("Handling BeginWaterPlanarProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwaterplanarprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterPlanarProbes event with a handler function
publisher.EventBeginWaterPlanarProbes.Connect(beginwaterplanarprobes_event_handler);

// remove subscription to the BeginWaterPlanarProbes event later by the handler function
publisher.EventBeginWaterPlanarProbes.Disconnect(beginwaterplanarprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwaterplanarprobes_event_connection;

// subscribe to the BeginWaterPlanarProbes event with a lambda handler function and keeping the connection
beginwaterplanarprobes_event_connection = publisher.EventBeginWaterPlanarProbes.Connect(() => {
		Log.Message("Handling BeginWaterPlanarProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwaterplanarprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwaterplanarprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwaterplanarprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginWaterPlanarProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginWaterPlanarProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterPlanarProbes

The event triggered after the water planar probes rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterPlanarProbes event handler
void endwaterplanarprobes_event_handler()
{
	Log.Message("\Handling EndWaterPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterplanarprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndWaterPlanarProbes.Connect(endwaterplanarprobes_event_connections, endwaterplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndWaterPlanarProbes.Connect(endwaterplanarprobes_event_connections, () => {
		Log.Message("Handling EndWaterPlanarProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwaterplanarprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterPlanarProbes event with a handler function
publisher.EventEndWaterPlanarProbes.Connect(endwaterplanarprobes_event_handler);

// remove subscription to the EndWaterPlanarProbes event later by the handler function
publisher.EventEndWaterPlanarProbes.Disconnect(endwaterplanarprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwaterplanarprobes_event_connection;

// subscribe to the EndWaterPlanarProbes event with a lambda handler function and keeping the connection
endwaterplanarprobes_event_connection = publisher.EventEndWaterPlanarProbes.Connect(() => {
		Log.Message("Handling EndWaterPlanarProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwaterplanarprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwaterplanarprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwaterplanarprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndWaterPlanarProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndWaterPlanarProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWater

The event triggered after the water rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWater event handler
void endwater_event_handler()
{
	Log.Message("\Handling EndWater event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwater_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndWater.Connect(endwater_event_connections, endwater_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndWater.Connect(endwater_event_connections, () => {
		Log.Message("Handling EndWater event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwater_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWater event with a handler function
publisher.EventEndWater.Connect(endwater_event_handler);

// remove subscription to the EndWater event later by the handler function
publisher.EventEndWater.Disconnect(endwater_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwater_event_connection;

// subscribe to the EndWater event with a lambda handler function and keeping the connection
endwater_event_connection = publisher.EventEndWater.Connect(() => {
		Log.Message("Handling EndWater event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwater_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwater_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwater_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWater events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndWater.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndWater.Enabled = true;

```

</details>

## 🔒︎ Event EventEndTransparent

The event triggered after the transparent objects rendering stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndTransparent event handler
void endtransparent_event_handler()
{
	Log.Message("\Handling EndTransparent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endtransparent_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndTransparent.Connect(endtransparent_event_connections, endtransparent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndTransparent.Connect(endtransparent_event_connections, () => {
		Log.Message("Handling EndTransparent event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endtransparent_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndTransparent event with a handler function
publisher.EventEndTransparent.Connect(endtransparent_event_handler);

// remove subscription to the EndTransparent event later by the handler function
publisher.EventEndTransparent.Disconnect(endtransparent_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endtransparent_event_connection;

// subscribe to the EndTransparent event with a lambda handler function and keeping the connection
endtransparent_event_connection = publisher.EventEndTransparent.Connect(() => {
		Log.Message("Handling EndTransparent event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endtransparent_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endtransparent_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endtransparent_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndTransparent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndTransparent.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndTransparent.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSrgbCorrection

The event triggered before the sRGB correction stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSrgbCorrection event handler
void beginsrgbcorrection_event_handler()
{
	Log.Message("\Handling BeginSrgbCorrection event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsrgbcorrection_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginSrgbCorrection.Connect(beginsrgbcorrection_event_connections, beginsrgbcorrection_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginSrgbCorrection.Connect(beginsrgbcorrection_event_connections, () => {
		Log.Message("Handling BeginSrgbCorrection event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsrgbcorrection_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSrgbCorrection event with a handler function
publisher.EventBeginSrgbCorrection.Connect(beginsrgbcorrection_event_handler);

// remove subscription to the BeginSrgbCorrection event later by the handler function
publisher.EventBeginSrgbCorrection.Disconnect(beginsrgbcorrection_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsrgbcorrection_event_connection;

// subscribe to the BeginSrgbCorrection event with a lambda handler function and keeping the connection
beginsrgbcorrection_event_connection = publisher.EventBeginSrgbCorrection.Connect(() => {
		Log.Message("Handling BeginSrgbCorrection event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsrgbcorrection_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsrgbcorrection_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsrgbcorrection_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSrgbCorrection events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginSrgbCorrection.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginSrgbCorrection.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSrgbCorrection

The event triggered after the sRGB correction stage. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSrgbCorrection event handler
void endsrgbcorrection_event_handler()
{
	Log.Message("\Handling EndSrgbCorrection event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsrgbcorrection_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndSrgbCorrection.Connect(endsrgbcorrection_event_connections, endsrgbcorrection_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndSrgbCorrection.Connect(endsrgbcorrection_event_connections, () => {
		Log.Message("Handling EndSrgbCorrection event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsrgbcorrection_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSrgbCorrection event with a handler function
publisher.EventEndSrgbCorrection.Connect(endsrgbcorrection_event_handler);

// remove subscription to the EndSrgbCorrection event later by the handler function
publisher.EventEndSrgbCorrection.Disconnect(endsrgbcorrection_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsrgbcorrection_event_connection;

// subscribe to the EndSrgbCorrection event with a lambda handler function and keeping the connection
endsrgbcorrection_event_connection = publisher.EventEndSrgbCorrection.Connect(() => {
		Log.Message("Handling EndSrgbCorrection event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsrgbcorrection_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsrgbcorrection_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsrgbcorrection_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSrgbCorrection events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndSrgbCorrection.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndSrgbCorrection.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginAdaptationColorAverage

The event triggered before the calculation of automatic exposure and white balance correction. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginAdaptationColorAverage event handler
void beginadaptationcoloraverage_event_handler()
{
	Log.Message("\Handling BeginAdaptationColorAverage event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginadaptationcoloraverage_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginAdaptationColorAverage.Connect(beginadaptationcoloraverage_event_connections, beginadaptationcoloraverage_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginAdaptationColorAverage.Connect(beginadaptationcoloraverage_event_connections, () => {
		Log.Message("Handling BeginAdaptationColorAverage event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginadaptationcoloraverage_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginAdaptationColorAverage event with a handler function
publisher.EventBeginAdaptationColorAverage.Connect(beginadaptationcoloraverage_event_handler);

// remove subscription to the BeginAdaptationColorAverage event later by the handler function
publisher.EventBeginAdaptationColorAverage.Disconnect(beginadaptationcoloraverage_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginadaptationcoloraverage_event_connection;

// subscribe to the BeginAdaptationColorAverage event with a lambda handler function and keeping the connection
beginadaptationcoloraverage_event_connection = publisher.EventBeginAdaptationColorAverage.Connect(() => {
		Log.Message("Handling BeginAdaptationColorAverage event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginadaptationcoloraverage_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginadaptationcoloraverage_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginadaptationcoloraverage_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginAdaptationColorAverage events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginAdaptationColorAverage.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginAdaptationColorAverage.Enabled = true;

```

</details>

## 🔒︎ Event EventEndAdaptationColorAverage

The event triggered after the calculation of automatic exposure and white balance correction. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndAdaptationColorAverage event handler
void endadaptationcoloraverage_event_handler()
{
	Log.Message("\Handling EndAdaptationColorAverage event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endadaptationcoloraverage_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndAdaptationColorAverage.Connect(endadaptationcoloraverage_event_connections, endadaptationcoloraverage_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndAdaptationColorAverage.Connect(endadaptationcoloraverage_event_connections, () => {
		Log.Message("Handling EndAdaptationColorAverage event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endadaptationcoloraverage_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndAdaptationColorAverage event with a handler function
publisher.EventEndAdaptationColorAverage.Connect(endadaptationcoloraverage_event_handler);

// remove subscription to the EndAdaptationColorAverage event later by the handler function
publisher.EventEndAdaptationColorAverage.Disconnect(endadaptationcoloraverage_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endadaptationcoloraverage_event_connection;

// subscribe to the EndAdaptationColorAverage event with a lambda handler function and keeping the connection
endadaptationcoloraverage_event_connection = publisher.EventEndAdaptationColorAverage.Connect(() => {
		Log.Message("Handling EndAdaptationColorAverage event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endadaptationcoloraverage_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endadaptationcoloraverage_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endadaptationcoloraverage_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndAdaptationColorAverage events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndAdaptationColorAverage.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndAdaptationColorAverage.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginAdaptationColor

The event triggered before the color adaptation rendering stage (automatic exposure and white balance correction). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginAdaptationColor event handler
void beginadaptationcolor_event_handler()
{
	Log.Message("\Handling BeginAdaptationColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginadaptationcolor_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginAdaptationColor.Connect(beginadaptationcolor_event_connections, beginadaptationcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginAdaptationColor.Connect(beginadaptationcolor_event_connections, () => {
		Log.Message("Handling BeginAdaptationColor event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginadaptationcolor_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginAdaptationColor event with a handler function
publisher.EventBeginAdaptationColor.Connect(beginadaptationcolor_event_handler);

// remove subscription to the BeginAdaptationColor event later by the handler function
publisher.EventBeginAdaptationColor.Disconnect(beginadaptationcolor_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginadaptationcolor_event_connection;

// subscribe to the BeginAdaptationColor event with a lambda handler function and keeping the connection
beginadaptationcolor_event_connection = publisher.EventBeginAdaptationColor.Connect(() => {
		Log.Message("Handling BeginAdaptationColor event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginadaptationcolor_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginadaptationcolor_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginadaptationcolor_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginAdaptationColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginAdaptationColor.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginAdaptationColor.Enabled = true;

```

</details>

## 🔒︎ Event EventEndAdaptationColor

The event triggered after the color adaptation rendering stage (automatic exposure and white balance correction). You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndAdaptationColor event handler
void endadaptationcolor_event_handler()
{
	Log.Message("\Handling EndAdaptationColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endadaptationcolor_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndAdaptationColor.Connect(endadaptationcolor_event_connections, endadaptationcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndAdaptationColor.Connect(endadaptationcolor_event_connections, () => {
		Log.Message("Handling EndAdaptationColor event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endadaptationcolor_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndAdaptationColor event with a handler function
publisher.EventEndAdaptationColor.Connect(endadaptationcolor_event_handler);

// remove subscription to the EndAdaptationColor event later by the handler function
publisher.EventEndAdaptationColor.Disconnect(endadaptationcolor_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endadaptationcolor_event_connection;

// subscribe to the EndAdaptationColor event with a lambda handler function and keeping the connection
endadaptationcolor_event_connection = publisher.EventEndAdaptationColor.Connect(() => {
		Log.Message("Handling EndAdaptationColor event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endadaptationcolor_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endadaptationcolor_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endadaptationcolor_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndAdaptationColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndAdaptationColor.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndAdaptationColor.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginTAA

The event triggered before the Temporal Anti-Aliasing (TAA) pass. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginTAA event handler
void begintaa_event_handler()
{
	Log.Message("\Handling BeginTAA event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begintaa_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginTAA.Connect(begintaa_event_connections, begintaa_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginTAA.Connect(begintaa_event_connections, () => {
		Log.Message("Handling BeginTAA event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begintaa_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginTAA event with a handler function
publisher.EventBeginTAA.Connect(begintaa_event_handler);

// remove subscription to the BeginTAA event later by the handler function
publisher.EventBeginTAA.Disconnect(begintaa_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begintaa_event_connection;

// subscribe to the BeginTAA event with a lambda handler function and keeping the connection
begintaa_event_connection = publisher.EventBeginTAA.Connect(() => {
		Log.Message("Handling BeginTAA event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begintaa_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begintaa_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begintaa_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginTAA events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginTAA.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginTAA.Enabled = true;

```

</details>

## 🔒︎ Event EventEndTAA

The event triggered after the Temporal Anti-Aliasing (TAA) pass. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndTAA event handler
void endtaa_event_handler()
{
	Log.Message("\Handling EndTAA event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endtaa_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndTAA.Connect(endtaa_event_connections, endtaa_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndTAA.Connect(endtaa_event_connections, () => {
		Log.Message("Handling EndTAA event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endtaa_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndTAA event with a handler function
publisher.EventEndTAA.Connect(endtaa_event_handler);

// remove subscription to the EndTAA event later by the handler function
publisher.EventEndTAA.Disconnect(endtaa_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endtaa_event_connection;

// subscribe to the EndTAA event with a lambda handler function and keeping the connection
endtaa_event_connection = publisher.EventEndTAA.Connect(() => {
		Log.Message("Handling EndTAA event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endtaa_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endtaa_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endtaa_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndTAA events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndTAA.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndTAA.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginCameraEffects

The event triggered before the camera effects stage. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginCameraEffects event handler
void begincameraeffects_event_handler()
{
	Log.Message("\Handling BeginCameraEffects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincameraeffects_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginCameraEffects.Connect(begincameraeffects_event_connections, begincameraeffects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginCameraEffects.Connect(begincameraeffects_event_connections, () => {
		Log.Message("Handling BeginCameraEffects event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begincameraeffects_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginCameraEffects event with a handler function
publisher.EventBeginCameraEffects.Connect(begincameraeffects_event_handler);

// remove subscription to the BeginCameraEffects event later by the handler function
publisher.EventBeginCameraEffects.Disconnect(begincameraeffects_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begincameraeffects_event_connection;

// subscribe to the BeginCameraEffects event with a lambda handler function and keeping the connection
begincameraeffects_event_connection = publisher.EventBeginCameraEffects.Connect(() => {
		Log.Message("Handling BeginCameraEffects event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begincameraeffects_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begincameraeffects_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begincameraeffects_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginCameraEffects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginCameraEffects.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginCameraEffects.Enabled = true;

```

</details>

## 🔒︎ Event EventEndCameraEffects

The event triggered after the camera effects stage. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndCameraEffects event handler
void endcameraeffects_event_handler()
{
	Log.Message("\Handling EndCameraEffects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcameraeffects_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndCameraEffects.Connect(endcameraeffects_event_connections, endcameraeffects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndCameraEffects.Connect(endcameraeffects_event_connections, () => {
		Log.Message("Handling EndCameraEffects event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endcameraeffects_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndCameraEffects event with a handler function
publisher.EventEndCameraEffects.Connect(endcameraeffects_event_handler);

// remove subscription to the EndCameraEffects event later by the handler function
publisher.EventEndCameraEffects.Disconnect(endcameraeffects_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endcameraeffects_event_connection;

// subscribe to the EndCameraEffects event with a lambda handler function and keeping the connection
endcameraeffects_event_connection = publisher.EventEndCameraEffects.Connect(() => {
		Log.Message("Handling EndCameraEffects event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endcameraeffects_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endcameraeffects_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endcameraeffects_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndCameraEffects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndCameraEffects.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndCameraEffects.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPostMaterials

The event triggered before the post materials rendering stage. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPostMaterials event handler
void beginpostmaterials_event_handler()
{
	Log.Message("\Handling BeginPostMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpostmaterials_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginPostMaterials.Connect(beginpostmaterials_event_connections, beginpostmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginPostMaterials.Connect(beginpostmaterials_event_connections, () => {
		Log.Message("Handling BeginPostMaterials event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpostmaterials_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPostMaterials event with a handler function
publisher.EventBeginPostMaterials.Connect(beginpostmaterials_event_handler);

// remove subscription to the BeginPostMaterials event later by the handler function
publisher.EventBeginPostMaterials.Disconnect(beginpostmaterials_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpostmaterials_event_connection;

// subscribe to the BeginPostMaterials event with a lambda handler function and keeping the connection
beginpostmaterials_event_connection = publisher.EventBeginPostMaterials.Connect(() => {
		Log.Message("Handling BeginPostMaterials event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpostmaterials_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpostmaterials_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpostmaterials_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPostMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginPostMaterials.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginPostMaterials.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPostMaterials

The event triggered after the post materials rendering stage. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPostMaterials event handler
void endpostmaterials_event_handler()
{
	Log.Message("\Handling EndPostMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpostmaterials_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndPostMaterials.Connect(endpostmaterials_event_connections, endpostmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndPostMaterials.Connect(endpostmaterials_event_connections, () => {
		Log.Message("Handling EndPostMaterials event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpostmaterials_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPostMaterials event with a handler function
publisher.EventEndPostMaterials.Connect(endpostmaterials_event_handler);

// remove subscription to the EndPostMaterials event later by the handler function
publisher.EventEndPostMaterials.Disconnect(endpostmaterials_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpostmaterials_event_connection;

// subscribe to the EndPostMaterials event with a lambda handler function and keeping the connection
endpostmaterials_event_connection = publisher.EventEndPostMaterials.Connect(() => {
		Log.Message("Handling EndPostMaterials event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpostmaterials_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpostmaterials_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpostmaterials_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPostMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndPostMaterials.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndPostMaterials.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginDebugMaterials

The event triggered before the debug materials stage. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginDebugMaterials event handler
void begindebugmaterials_event_handler()
{
	Log.Message("\Handling BeginDebugMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begindebugmaterials_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginDebugMaterials.Connect(begindebugmaterials_event_connections, begindebugmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginDebugMaterials.Connect(begindebugmaterials_event_connections, () => {
		Log.Message("Handling BeginDebugMaterials event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begindebugmaterials_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginDebugMaterials event with a handler function
publisher.EventBeginDebugMaterials.Connect(begindebugmaterials_event_handler);

// remove subscription to the BeginDebugMaterials event later by the handler function
publisher.EventBeginDebugMaterials.Disconnect(begindebugmaterials_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begindebugmaterials_event_connection;

// subscribe to the BeginDebugMaterials event with a lambda handler function and keeping the connection
begindebugmaterials_event_connection = publisher.EventBeginDebugMaterials.Connect(() => {
		Log.Message("Handling BeginDebugMaterials event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begindebugmaterials_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begindebugmaterials_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begindebugmaterials_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginDebugMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginDebugMaterials.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginDebugMaterials.Enabled = true;

```

</details>

## 🔒︎ Event EventEndDebugMaterials

The event triggered after the debug materials stage. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndDebugMaterials event handler
void enddebugmaterials_event_handler()
{
	Log.Message("\Handling EndDebugMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enddebugmaterials_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndDebugMaterials.Connect(enddebugmaterials_event_connections, enddebugmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndDebugMaterials.Connect(enddebugmaterials_event_connections, () => {
		Log.Message("Handling EndDebugMaterials event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
enddebugmaterials_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndDebugMaterials event with a handler function
publisher.EventEndDebugMaterials.Connect(enddebugmaterials_event_handler);

// remove subscription to the EndDebugMaterials event later by the handler function
publisher.EventEndDebugMaterials.Disconnect(enddebugmaterials_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection enddebugmaterials_event_connection;

// subscribe to the EndDebugMaterials event with a lambda handler function and keeping the connection
enddebugmaterials_event_connection = publisher.EventEndDebugMaterials.Connect(() => {
		Log.Message("Handling EndDebugMaterials event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
enddebugmaterials_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
enddebugmaterials_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
enddebugmaterials_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndDebugMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndDebugMaterials.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndDebugMaterials.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginVisualizer

The event triggered before the visualizer rendering stage. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginVisualizer event handler
void beginvisualizer_event_handler()
{
	Log.Message("\Handling BeginVisualizer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginvisualizer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginVisualizer.Connect(beginvisualizer_event_connections, beginvisualizer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginVisualizer.Connect(beginvisualizer_event_connections, () => {
		Log.Message("Handling BeginVisualizer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginvisualizer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginVisualizer event with a handler function
publisher.EventBeginVisualizer.Connect(beginvisualizer_event_handler);

// remove subscription to the BeginVisualizer event later by the handler function
publisher.EventBeginVisualizer.Disconnect(beginvisualizer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginvisualizer_event_connection;

// subscribe to the BeginVisualizer event with a lambda handler function and keeping the connection
beginvisualizer_event_connection = publisher.EventBeginVisualizer.Connect(() => {
		Log.Message("Handling BeginVisualizer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginvisualizer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginvisualizer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginvisualizer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginVisualizer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginVisualizer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginVisualizer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndVisualizer

The event triggered after the visualizer rendering stage. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndVisualizer event handler
void endvisualizer_event_handler()
{
	Log.Message("\Handling EndVisualizer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvisualizer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndVisualizer.Connect(endvisualizer_event_connections, endvisualizer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndVisualizer.Connect(endvisualizer_event_connections, () => {
		Log.Message("Handling EndVisualizer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endvisualizer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndVisualizer event with a handler function
publisher.EventEndVisualizer.Connect(endvisualizer_event_handler);

// remove subscription to the EndVisualizer event later by the handler function
publisher.EventEndVisualizer.Disconnect(endvisualizer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endvisualizer_event_connection;

// subscribe to the EndVisualizer event with a lambda handler function and keeping the connection
endvisualizer_event_connection = publisher.EventEndVisualizer.Connect(() => {
		Log.Message("Handling EndVisualizer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endvisualizer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endvisualizer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endvisualizer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndVisualizer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndVisualizer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndVisualizer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndScreen

The event triggered after the stage of rendering each screen (a stereo image has 2 screens, while a cubemap will have 6). You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndScreen event handler
void endscreen_event_handler()
{
	Log.Message("\Handling EndScreen event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endscreen_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndScreen.Connect(endscreen_event_connections, endscreen_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndScreen.Connect(endscreen_event_connections, () => {
		Log.Message("Handling EndScreen event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endscreen_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndScreen event with a handler function
publisher.EventEndScreen.Connect(endscreen_event_handler);

// remove subscription to the EndScreen event later by the handler function
publisher.EventEndScreen.Disconnect(endscreen_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endscreen_event_connection;

// subscribe to the EndScreen event with a lambda handler function and keeping the connection
endscreen_event_connection = publisher.EventEndScreen.Connect(() => {
		Log.Message("Handling EndScreen event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endscreen_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endscreen_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endscreen_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndScreen events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndScreen.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndScreen.Enabled = true;

```

</details>

## 🔒︎ Event EventEnd

The event triggered when rendering of the frame ends. You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the End event handler
void end_event_handler()
{
	Log.Message("\Handling End event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections end_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEnd.Connect(end_event_connections, end_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEnd.Connect(end_event_connections, () => {
		Log.Message("Handling End event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
end_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the End event with a handler function
publisher.EventEnd.Connect(end_event_handler);

// remove subscription to the End event later by the handler function
publisher.EventEnd.Disconnect(end_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection end_event_connection;

// subscribe to the End event with a lambda handler function and keeping the connection
end_event_connection = publisher.EventEnd.Connect(() => {
		Log.Message("Handling End event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
end_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
end_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
end_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring End events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEnd.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEnd.Enabled = true;

```

</details>

## 🔒︎ Event EventEndVRQuadComposeEyeSwapchains

The Event triggered after composing VR viewports, enabling you to subscribe and perform certain actions (e.g. implement a binoculars effect using post-materials). You can subscribe to events via *Connect()* ï¿½and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndVRQuadComposeEyeSwapchains event handler
void endvrquadcomposeeyeswapchains_event_handler()
{
	Log.Message("\Handling EndVRQuadComposeEyeSwapchains event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvrquadcomposeeyeswapchains_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndVRQuadComposeEyeSwapchains.Connect(endvrquadcomposeeyeswapchains_event_connections, endvrquadcomposeeyeswapchains_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndVRQuadComposeEyeSwapchains.Connect(endvrquadcomposeeyeswapchains_event_connections, () => {
		Log.Message("Handling EndVRQuadComposeEyeSwapchains event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endvrquadcomposeeyeswapchains_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndVRQuadComposeEyeSwapchains event with a handler function
publisher.EventEndVRQuadComposeEyeSwapchains.Connect(endvrquadcomposeeyeswapchains_event_handler);

// remove subscription to the EndVRQuadComposeEyeSwapchains event later by the handler function
publisher.EventEndVRQuadComposeEyeSwapchains.Disconnect(endvrquadcomposeeyeswapchains_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endvrquadcomposeeyeswapchains_event_connection;

// subscribe to the EndVRQuadComposeEyeSwapchains event with a lambda handler function and keeping the connection
endvrquadcomposeeyeswapchains_event_connection = publisher.EventEndVRQuadComposeEyeSwapchains.Connect(() => {
		Log.Message("Handling EndVRQuadComposeEyeSwapchains event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endvrquadcomposeeyeswapchains_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endvrquadcomposeeyeswapchains_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endvrquadcomposeeyeswapchains_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndVRQuadComposeEyeSwapchains events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndVRQuadComposeEyeSwapchains.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndVRQuadComposeEyeSwapchains.Enabled = true;

```

</details>

## vec4 PanoramaFisheyeKannalaBrandtCoefficients

The four radial distortion coefficients (k1, k2, k3, k4) of the Kannala-Brandt fisheye camera model used by the corresponding panorama mode. They define the polynomial mapping the angle between the incoming ray and the optical axis to the normalized image radius. The default value (1, 0, 0, 0) corresponds to the pure equidistant projection. This mode reproduces the image geometry of a real calibrated fisheye camera, with the coefficients taken from the camera calibration data.
## vec2 PanoramaFisheyeKannalaBrandtFocalLength

The focal length intrinsics (fx, fy) of the calibrated fisheye camera, in pixels, used by the Kannala-Brandt panorama mode to convert pixel coordinates to normalized camera coordinates.
## float PanoramaFisheyeKannalaBrandtImageCircleRadius

The radius of the valid image circle of the fisheye lens in normalized radial coordinates, used by the Kannala-Brandt panorama mode: pixels outside this radius are masked out, reproducing the image circle of the real lens.
## vec2 PanoramaFisheyeKannalaBrandtImageDimensions

The dimensions (width, height), in pixels, of the calibrated camera image the Kannala-Brandt intrinsics refer to. The viewport coordinates are mapped to this pixel space before the intrinsics are applied.
## vec2 PanoramaFisheyeKannalaBrandtPrincipalPoint

The principal point intrinsics (cx, cy) of the calibrated fisheye camera, in pixels: the image position of the optical axis used by the Kannala-Brandt panorama mode.
## float PanoramaFisheyeKannalaBrandtSkew

The skew (axis non-orthogonality) coefficient of the calibration matrix used by the Kannala-Brandt panorama mode. The value of 0 (default) corresponds to orthogonal pixel axes.
## vec2 PanoramaFisheyeKannalaBrandtTangentialDistortion

The tangential (decentering) distortion coefficients (p1, p2) of the calibrated fisheye camera used by the Kannala-Brandt panorama mode. The value (0, 0) means no tangential distortion.
## bool PanoramaForceDisableScreenSpaceEffects

The value indicating if screen-space and screen-dependent camera effects (such as SSR, SSAO, SSGI, motion blur, DOF, bloom, lens flares, local tonemapper) are forcibly disabled while the viewport renders a panorama. These effects are computed per panorama face and would produce visible seams between the faces. Enabled by default; when disabled, the effects stay as configured at the cost of per-face artifacts.
## float PanoramaFisheyeKannalaBrandtChromaticAberration

The chromatic aberration intensity of the fisheye lens, used by the Kannala-Brandt panorama mode: the red channel is sampled at the radial distance scaled by (1 - value), the blue channel at (1 + value), reproducing lateral chromatic aberration of a real lens. 0 means no chromatic aberration.
## float PanoramaFisheyeKannalaBrandtVignettingCoefficient5

The fifth coefficient of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the coefficient at the 10th power of the normalized radial distance, kept separate because the coefficients vector holds only four components.
## vec4 PanoramaFisheyeKannalaBrandtVignettingCoefficients

The first four coefficients of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the vignetting intensity is an even-order polynomial of the radial distance normalized by the image circle radius, with these values as the coefficients at the 2nd, 4th, 6th, and 8th powers.
### Members

---

## Viewport ( )


Creates a new viewport with default settings.


> **Notice:** We don't recommend creating a viewport every frame, as such approach is unoptimal and exhaust GPU resources. Create viewports in **Init()** instead, to have them cached for further use.


## void AppendSkipFlags ( int flags )

Appends specified [skip flags](#SKIP_SHADOWS) to the list of currently used ones.
### Arguments

- *int* **flags** - [Skip flags](#SKIP_SHADOWS) to append.

## int CheckSkipFlags ( int flags )

Returns a value indicating if the specified [skip flags](#SKIP_SHADOWS) are set for the current viewport.
### Arguments

- *int* **flags** - [Skip flags](#SKIP_SHADOWS) to check.

### Return value

1 if the skip flags are set; otherwise, 0.
## void RemoveSkipFlags ( int flags )

Removes specified [skip flags](#SKIP_SHADOWS) from the list of currently used ones.
### Arguments

- *int* **flags** - [Skip flags](#SKIP_SHADOWS) to remove.

## void Render ( Camera camera )


Renders an image from the specified camera.


To render an image from the camera to the [RenderTarget](../../../api/library/rendering/class.rendertarget_cs.md) interface, do the following:


```csharp
camera = new Camera();

render_target.Enable();
{
	viewport.Render(camera);
}
render_target.Disable();

```


### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera an image from which should be rendered.

## void Render ( Camera camera , int width , int height )

Renders an image of the specified size from the specified camera to the current rendering target.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.

## void RenderEngine ( Camera camera )

Renders an Engine viewport for the specified camera to the current rendering target. This method renders a splash screen and provides an image in accordance with panoramic and stereo rendering settings.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.

## void RenderTexture2D ( Camera camera , Texture texture )

Renders an image from the camera to the specified 2D texture.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.

## void RenderTexture2D ( Camera camera , Texture texture , int width , int height , bool hdr = 0 )

Renders an image of the specified size from the camera to a 2D texture.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *bool* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D texture: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_cs.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_cs.md#FORMAT_RGBA8)

## void RenderTextureCube ( Camera camera , Texture texture , bool local_space = false )

Renders the image from the camera to the cubemap texture.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target Cube [texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *bool* **local_space** - A flag indicating if the camera angle should be used for the cube map rendering.

## void RenderTextureCube ( Camera camera , Texture texture , int size , bool hdr = 0 , bool local_space = 0 )

Renders the image from the camera to the cube map of the specified size.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target cube map to save the result to.
- *int* **size** - Cube map edge size.
- *bool* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D texture: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_cs.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_cs.md#FORMAT_RGBA8)
- *bool* **local_space** - A flag indicating if the camera angle should be used for the cube map rendering.

## void RenderNode ( Camera camera , Node node )

Renders the given node with all children to the current rendering target.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node to be rendered.

## void RenderNode ( Camera camera , Node node , int width , int height )

Renders the given node with all children to the current rendering target.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node to be rendered.
- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.

## void RenderNodeTexture2D ( Camera camera , Node node , Texture texture , int width , int height , bool hdr )

Renders the given node with all children to the 2D texture of the specified size.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node to be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *bool* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D texture: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_cs.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_cs.md#FORMAT_RGBA8)

## void RenderNodeTexture2D ( Camera camera , Node node , Texture texture )

Renders the given node with all children to the specified 2D texture.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node to be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.

## void RenderNodes ( Camera camera , Node [] nodes )

Renders given nodes with all their children to the current rendering target.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **nodes** - List of the nodes to be rendered.

## void RenderNodes ( Camera camera , Node [] nodes , int width , int height )

Renders given nodes with all their children to the current rendering target of the specified size.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **nodes** - List of the nodes to be rendered.
- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.

## void RenderNodesTexture2D ( Camera camera , Node [] nodes , Texture texture , int width , int height , int hdr )

Renders given nodes with all their children to the 2D texture of the specified size.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **nodes** - List of the nodes to be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D image: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_cs.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_cs.md#FORMAT_RGBA8)

## void RenderNodesTexture2D ( Camera camera , Node [] nodes , Texture texture )

Renders given nodes with all their children to the specified 2D texture.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **nodes** - List of the nodes to be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.

## void RenderStereo ( Camera camera_left , Camera camera_right , string stereo_material )

Renders a stereo image in the current viewport.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera_left** - Camera that renders an image for the left eye.
- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera_right** - Camera that renders an image for the right eye.
- *string* **stereo_material** - List of names of stereo materials to be used.

## void RenderStereoPeripheral ( Camera camera_left , Camera camera_right , Camera camera_focus_left , Camera camera_focus_right , Texture texture_left , Texture texture_right , Texture texture_focus_left , Texture texture_focus_right , string stereo_material )

Renders a stereo image for HMDs having context (peripheral) and focus displays. This method saves performance on shadows and reflections along with other optimizations reducing rendering load, such as reduced resolutions for textures.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera_left** - Camera that renders an image for the left context (low-res) display.
- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera_right** - Camera that renders an image for the right context (low-res) display.
- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera_focus_left** - Camera that renders an image for the left focus (high-res) display.
- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera_focus_right** - Camera that renders an image for the right focus (high-res) display.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture_left** - Texture to save the image rendered for the left context (low-res) display.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture_right** - Texture to save the image rendered for the right context (low-res) display.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture_focus_left** - Texture to save the image rendered for the left focus (high-res) display.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture_focus_right** - Texture to save the image rendered for the right focus (high-res) display.
- *string* **stereo_material** - List of names of stereo materials to be used.

## void SetStereoHiddenAreaMesh ( Mesh hidden_area_mesh_left , Mesh hidden_area_mesh_right )


Sets custom meshes to be used for culling pixels, that are not visible in VR.


> **Notice:** Requires [render_stereo_hidden_area](../../../code/console/index.md#render_stereo_hidden_area) = 2


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **hidden_area_mesh_left** - [Mesh](../../../api/library/rendering/class.mesh_cs.md) representing hidden area for the left eye.
- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **hidden_area_mesh_right** - [Mesh](../../../api/library/rendering/class.mesh_cs.md) representing hidden area for the right eye.

## void ClearStereoHiddenAreaMesh ( )

Clears meshes that represent hidden areas for both, left and right eye. Hidden areas are used for culling pixels, that are not visible in VR
## void SetEnvironmentTexturePath ( string name )

Sets the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) for the viewport. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Arguments

- *string* **name** - Path to the cubemap defining the environment color.

## string GetEnvironmentTexturePath ( )

Returns the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) set for the viewport. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Return value

Path to the cubemap defining the environment color.
## void ResetEnvironmentTexture ( )

Resets the current environment texture to the default one.
## void RenderVREngine ( )

Renders the VR viewport if VR is enabled, taking into account the [vr mirror mode](../../../api/library/vr/class.vr_cs.md#MirrorMode) set.
## void LockResources ( )

Locks resources (such as temporal old textures) in the current viewport so they won't be reused or released.
## void UnlockResources ( )

Unlocks resources (such as temporal old textures) in the current viewport so they can be reused and released by the engine.
## bool IsLockedResources ( )

Returns a value indicating if resources (such as temporal old textures) in the current viewport are locked and won't be reused or released.
### Return value

true if the resources are locked; otherwise, false.
