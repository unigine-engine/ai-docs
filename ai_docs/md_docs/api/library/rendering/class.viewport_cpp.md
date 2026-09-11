# Unigine.Viewport Class (CPP)

**Header:** #include <UnigineViewport.h>


The **Viewport** class is used to render a scene with the specified settings.


The main use cases of the Viewport class are as follows:


1. Integrate the engine to a 3rd party renderer (or vice versa) and render the image anywhere (via the [render()](#render_Camera_void)  method): to the external library, [CustomSystemProxy](../../../api/library/engine/class.customsystemproxy_cpp.md) interface, [RenderTarget](../../../api/library/rendering/class.rendertarget_cpp.md) interface (a frame buffers abstraction), etc.

  - To render the image to the [RenderTarget](../../../api/library/rendering/class.rendertarget_cpp.md) interface, do the following: ```cpp // mono rendering ViewportPtr viewport; TexturePtr texture; CameraPtr camera; int AppWorldLogic::init() { viewport = Viewport::create(); texture = Texture::create(); // create 512 x 512 render target texture->create2D(512, 512, Texture::FORMAT_RGBA8, Texture::FORMAT_USAGE_RENDER); camera = Camera::create(); return 1; } int AppWorldLogic::update() { // set modelview & projection matrices to camera instance // ... // rendering RenderTargetPtr render_target = Render::getTemporaryRenderTarget(); render_target->bindColorTexture(0, texture); render_target->enable(); { viewport->render(camera); } render_target->disable(); render_target->unbindAll(); Render::releaseTemporaryRenderTarget(render_target); return 1; } ``` To render the image to the [RenderTarget](../../../api/library/rendering/class.rendertarget_cpp.md) interface in the stereo mode, do the following: ```cpp // stereo rendering ViewportPtr viewport; TexturePtr left_texture; TexturePtr right_texture; CameraPtr left_eye; CameraPtr right_eye; int AppWorldLogic::init() { viewport = Viewport::create(); left_texture = Texture::create(); right_texture = Texture::create(); // create two 512 x 512 render target for each eye left_texture->create2D(512, 512, Texture::FORMAT_RGBA8, Texture::FORMAT_USAGE_RENDER); right_texture->create2D(512, 512, Texture::FORMAT_RGBA8, Texture::FORMAT_USAGE_RENDER); left_eye = Camera::create(); right_eye = Camera::create(); return 1; } int AppWorldLogic::update() { // set modelview & projection matrices to camera instance // ... // rendering RenderTargetPtr render_target = Render::getTemporaryRenderTarget(); render_target->bindColorTexture(0, left_texture); render_target->bindColorTexture(1, right_texture); render_target->enable(); { // use "post_stereo_separate" material in order to render to both textures viewport->renderStereo(left_eye, right_eye, "Unigine::post_stereo_separate"); } render_target->disable(); render_target->unbindAll(); Render::releaseTemporaryRenderTarget(render_target); return 1; } ```
  - To render the image to the [CustomSystemProxy](../../../api/library/engine/class.customsystemproxy_cpp.md) interface, check the [3rd Party](../../../sdk/api_samples/third_party/qt.md) samples: `source -> samples -> 3rdparty -> ViewportQt`. > **Notice:** **ViewportQt** sample is available only for the Engineering and Sim editions of UNIGINE SDKs.
2. Render a scene to a [texture](../../../api/library/rendering/class.texture_cpp.md) (data stays in the GPU memory).

  - To render the scene to a [Texture](../../../api/library/rendering/class.texture_cpp.md) interface, use the following methods: ```cpp ViewportPtr viewport; TexturePtr texture; CameraPtr camera; int AppWorldLogic::init() { // initialization viewport = Viewport::create(); texture = Texture::create(); // create 512 x 512 render target texture->create2D(512, 512, Texture::FORMAT_RGBA8, Texture::FORMAT_USAGE_RENDER); camera = Camera::create(); return 1; } int AppWorldLogic::update() { // set modelview & projection matrices to camera instance // ... // rendering // // saving current render state and clearing it RenderState::saveState(); RenderState::clearStates(); { viewport->renderTexture2D(camera, texture); } RenderState::restoreState(); return 1; } ```

    - *[renderTexture2D(camera,texture)](#renderTexture2D_Camera_Texture_void)*
    - *[renderTexture2D(camera,texture,width,height,hdr)](#renderTexture2D_Camera_Texture_int_int_int_void)*
    - *[renderTextureCube(camera,texture,local_space)](#renderTextureCube_Camera_Texture_int_void)*
    - *[renderTextureCube(camera,texture,size,hdr,local_space)](#renderTextureCube_Camera_Texture_int_int_int_void)*
3. Render a node to a [texture](../../../api/library/rendering/class.texture_cpp.md) (data stays in the GPU memory).

  - To render a node (or nodes) to a [Texture](../../../api/library/rendering/class.texture_cpp.md) interface, use the following methods:

    - *[renderNodeTexture2D(camera,node,texture)](#renderNodeTexture2D_Camera_Node_Texture_void)*
    - *[renderNodeTexture2D(camera,node,texture,width,height,hdr)](#renderNodeTexture2D_Camera_Node_Texture_int_int_int_void)*
    - *[renderNodesTexture2D(camera,nodes,texture)](#renderNodesTexture2D_Camera_VECNode_Texture_void)*
    - *[renderNodesTexture2D(camera,nodes,texture,width,height,hdr)](#renderNodesTexture2D_Camera_VECNode_Texture_int_int_int_void)*


You can subscribe to events before and after any rendering pass using the **[getEvent***()](../../...md#getEventBegin_Event)**: thus, getting access to the intermediate state of rendering buffers and matrices. Some of them are read-only, but most of them can be modified ad hoc. The event handler can get a [Renderer](../../../api/library/rendering/class.renderer_cpp.md) pointer.


![](render_callbacks.jpg)


Thanks to this feature you can get direct access to G-Buffer, SSAO, lights or any other effect. One more example: you can create a custom post-process and apply it before TAA, thus, getting correct antialiased image as a result. You can even create your own custom light sources, decals, etc. The feature can also be useful for custom sensors view.


Viewport class has different rendering modes: [RENDER_DEPTH](#RENDER_DEPTH) (depth only), [RENDER_DEPTH_GBUFFER](#RENDER_DEPTH_GBUFFER) (depth + G-buffer), [RENDER_DEPTH_GBUFFER_FINAL](#RENDER_DEPTH_GBUFFER_FINAL) (depth + G-buffer + final image). This can give you extra performance boost if you need only depth info, for example.


> **Notice:** To set any viewport as a main, use the [setViewport()](../../../api/library/rendering/class.render_cpp.md#setViewport_Viewport_void)  method of the *Render* class.
>
>
> **A single viewport should be used with a single camera**, otherwise it may cause visual artefacts. To avoid artefacts, when using several cameras with a single viewport, all post effects must be disabled using the *[setSkipFlags()](#setSkipFlags_int_void)* method with the *[SKIP_POSTEFFECTS](../../...md#SKIP_POSTEFFECTS)* flag. See the usage example below.


<details>
<summary>Example: Single Viewport & Several Cameras | Close</summary>

```cpp
void setupMultipleCamerasWithSingleViewport()
{
    // Create a shared viewport for multiple cameras
    ViewportPtr shared_viewport = Viewport::create();

    // CRITICAL: Disable post-effects to avoid visual artifacts
    // when using multiple cameras with a single viewport
    shared_viewport->setSkipFlags(Viewport::SKIP_POSTEFFECTS);

    shared_viewport->setNodeLightUsage(Viewport::USAGE_WORLD_LIGHT);

    // Create multiple cameras
    CameraPtr camera1 = Camera::create();
    CameraPtr camera2 = Camera::create();

    // Position cameras differently
    camera1->setPosition(Vec3(0.0f, 0.0f, 5.0f));
    camera2->setPosition(Vec3(10.0f, 0.0f, 5.0f));

    // Create textures for each camera's output
    TexturePtr texture1 = Texture::create();
    TexturePtr texture2 = Texture::create();

    texture1->create2D(1920, 1080, Texture::FORMAT_RGBA8,
        Texture::FORMAT_USAGE_RENDER);
    texture2->create2D(1920, 1080, Texture::FORMAT_RGBA8,
        Texture::FORMAT_USAGE_RENDER);

    // Render from different cameras using the same viewport
    // Post-effects are disabled, so no artifacts will occur
    shared_viewport->renderTexture2D(camera1, texture1);
    shared_viewport->renderTexture2D(camera2, texture2);
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
- C++/C# usage example: [Creating Mirrors Using Viewports (Rendering to Texture) or a Standard Material](../../../code/usage/mirrors_viewports_materials/index_cpp.md)


## Viewport Class

### Members

## void setNodeLightUsage ( int usage )

Sets a new type of lighting of the render node.
### Arguments

- *int* **usage** - The lighting type. Can be one of the following:

  - 0 - *[USAGE_WORLD_LIGHT](../../...md#USAGE_WORLD_LIGHT)* (use lighting from the [LightWorld](../../../api/library/lights/class.lightworld_cpp.md) set in the current loaded world).
  - 1 - *[USAGE_AUX_LIGHT](../../...md#USAGE_AUX_LIGHT)* (use lighting from the auxiliary virtual scene containing one LightWorld with 45 degrees slope angles along all axes, scattering is not used).
  - 2 - *[USAGE_NODE_LIGHT](../../...md#USAGE_NODE_LIGHT)* (use the node lighting).

## int getNodeLightUsage () const

Returns the current type of lighting of the render node.
### Return value

Current
lighting type. Can be one of the following:


- 0 - *[USAGE_WORLD_LIGHT](../../...md#USAGE_WORLD_LIGHT)* (use lighting from the [LightWorld](../../../api/library/lights/class.lightworld_cpp.md) set in the current loaded world).
- 1 - *[USAGE_AUX_LIGHT](../../...md#USAGE_AUX_LIGHT)* (use lighting from the auxiliary virtual scene containing one LightWorld with 45 degrees slope angles along all axes, scattering is not used).
- 2 - *[USAGE_NODE_LIGHT](../../...md#USAGE_NODE_LIGHT)* (use the node lighting).


## void setStereoOffset ( float offset )

Sets a new virtual camera offset (an offset after the perspective projection).
### Arguments

- *float* **offset** - The virtual camera offset in units.

## float getStereoOffset () const

Returns the current virtual camera offset (an offset after the perspective projection).
### Return value

Current virtual camera offset in units.
## void setStereoRadius ( float radius )

Sets a new radius for stereo � the half of the separation distance between the cameras (i.e. between eyes).
### Arguments

- *float* **radius** - The stereo radius in units. If a negative value is provided, 0 will be used instead.

## float getStereoRadius () const

Returns the current radius for stereo � the half of the separation distance between the cameras (i.e. between eyes).
### Return value

Current stereo radius in units. If a negative value is provided, 0 will be used instead.
## void setStereoDistance ( float distance )

Sets a new focal distance for stereo rendering (distance in the world space to the point where two views line up, i.e. to the zero parallax plane).
### Arguments

- *float* **distance** - The focal distance in units.

## float getStereoDistance () const

Returns the current focal distance for stereo rendering (distance in the world space to the point where two views line up, i.e. to the zero parallax plane).
### Return value

Current focal distance in units.
## bool isStereo () const

Returns the current value indicating if the stereo rendering is enabled for the current viewport (one of the [stereo modes](../../../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_STEREO_ANAGLYPH) is set).
### Return value

**true** if stereo rendering for the current viewport (one of the [stereo modes](../../../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_STEREO_ANAGLYPH)) is enabled ; otherwise **false**.
## bool isPanorama () const

Returns the current value indicating if the panoramic rendering is enabled.
### Return value

**true** if panoramic rendering is enabled ; otherwise **false**.
## void setRenderMode ( int mode )

Sets a new render mode. The mode determines the set of buffers to be rendered.
### Arguments

- *int* **mode** - The render mode, one of the following:

  - *[RENDER_DEPTH](../../...md#RENDER_DEPTH)*
  - *[RENDER_DEPTH_GBUFFER](../../...md#RENDER_DEPTH_GBUFFER)*
  - *[RENDER_DEPTH_GBUFFER_FINAL](../../...md#RENDER_DEPTH_GBUFFER_FINAL)*

## int getRenderMode () const

Returns the current render mode. The mode determines the set of buffers to be rendered.
### Return value

Current
render mode, one of the following:


- *[RENDER_DEPTH](../../...md#RENDER_DEPTH)*
- *[RENDER_DEPTH_GBUFFER](../../...md#RENDER_DEPTH_GBUFFER)*
- *[RENDER_DEPTH_GBUFFER_FINAL](../../...md#RENDER_DEPTH_GBUFFER_FINAL)*


## void setMode ( Render::VIEWPORT_MODE mode )

Sets a new rendering mode for the current viewport.
### Arguments

- *[Render::VIEWPORT_MODE](../../../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE)* **mode** - The rendering mode set for the current viewport. It can be one of the [stereo](../../../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_STEREO_ANAGLYPH) or [panoramic](../../../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_PANORAMA_CURVED_180) modes or the [default](../../../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_DEFAULT) mode.

## Render::VIEWPORT_MODE getMode () const

Returns the current rendering mode for the current viewport.
### Return value

Current rendering mode set for the current viewport. It can be one of the [stereo](../../../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_STEREO_ANAGLYPH) or [panoramic](../../../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_PANORAMA_CURVED_180) modes or the [default](../../../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_DEFAULT) mode.
## void setSkipFlags ( int flags )

Sets a new [skip flag](#SKIP_SHADOWS) set for the current viewport.
### Arguments

- *int* **flags** - The [skip flag](#SKIP_SHADOWS) set for the current viewport.

## int getSkipFlags () const

Returns the current [skip flag](#SKIP_SHADOWS) set for the current viewport.
### Return value

Current [skip flag](#SKIP_SHADOWS) set for the current viewport.
## void setFirstFrame ( int frame )

Sets a new value indicating if the first frame is enabled over the current frame.
### Arguments

- *int* **frame** - The value indicating if the first frame is enabled over the current frame: 1 for the first frame flag; otherwise, 0.

## int getFirstFrame () const

Returns the current value indicating if the first frame is enabled over the current frame.
### Return value

Current value indicating if the first frame is enabled over the current frame: 1 for the first frame flag; otherwise, 0.
## void setAspectCorrection ( bool correction )

Sets a new value indicating if the aspect correction enabled for current viewport.
### Arguments

- *bool* **correction** - Set **true** to enable the aspect correction; **false** - to disable it.

## bool isAspectCorrection () const

Returns the current value indicating if the aspect correction enabled for current viewport.
### Return value

**true** if the aspect correction is enabled ; otherwise **false**.
## int getID () const

Returns the current Viewport ID.
### Return value

Current Viewport ID.
## void setPanoramaFisheyeFov ( float fov )

Sets a new field of view angle used for the panorama rendering mode.
### Arguments

- *float* **fov** - The field of view angle used for the panorama rendering mode, in degrees.

## float getPanoramaFisheyeFov () const

Returns the current field of view angle used for the panorama rendering mode.
### Return value

Current field of view angle used for the panorama rendering mode, in degrees.
## void setEnvironmentTexture ( const Ptr < Texture >& texture )

Sets a new cubemap defining the environment color.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)>&* **texture** - The cubemap defining the environment color.

## Ptr < Texture > getEnvironmentTexture () const

Returns the current cubemap defining the environment color.
### Return value

Current cubemap defining the environment color.
## void setUseTAAOffset ( bool taaoffset )

Sets a new  value indicating if skipping render mode check is enabled for using TAA.
Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to *[RENDER_DEPTH](../../...md#RENDER_DEPTH)*.

### Arguments

- *bool* **taaoffset** - Set **true** to enable skipping render mode check when using TAA; **false** - to disable it.

## bool isUseTAAOffset () const

Returns the current  value indicating if skipping render mode check is enabled for using TAA.
Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to *[RENDER_DEPTH](../../...md#RENDER_DEPTH)*.

### Return value

**true** if skipping render mode check when using TAA is enabled ; otherwise **false**.
## void setLifetime ( int lifetime )

Sets a new value indicating how many frames temporary viewport resources are available after the viewport stops rendering.
### Arguments

- *int* **lifetime** - The number of frames during which temporary viewport resources are available after the viewport stops rendering

## int getLifetime () const

Returns the current value indicating how many frames temporary viewport resources are available after the viewport stops rendering.
### Return value

Current number of frames during which temporary viewport resources are available after the viewport stops rendering
## Event<> getEventBegin () const

event triggered when rendering of the frame begins. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Begin event handler
void begin_event_handler()
{
	Log::message("\Handling Begin event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begin_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBegin().connect(begin_event_connections, begin_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBegin().connect(begin_event_connections, []() {
		Log::message("\Handling Begin event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begin_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begin_event_connection;

// subscribe to the Begin event with a handler function keeping the connection
publisher->getEventBegin().connect(begin_event_connection, begin_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begin_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begin_event_connection.setEnabled(true);

// ...

// remove subscription to the Begin event via the connection
begin_event_connection.disconnect();

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

	// A Begin event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Begin event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBegin().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begin_handler_id;

// subscribe to the Begin event with a lambda handler function and keeping connection ID
begin_handler_id = publisher->getEventBegin().connect(e_connections, []() {
		Log::message("\Handling Begin event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBegin().disconnect(begin_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Begin events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBegin().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBegin().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginEnvironment () const

event triggered before the Environment rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginEnvironment event handler
void beginenvironment_event_handler()
{
	Log::message("\Handling BeginEnvironment event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginenvironment_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginEnvironment().connect(beginenvironment_event_connections, beginenvironment_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginEnvironment().connect(beginenvironment_event_connections, []() {
		Log::message("\Handling BeginEnvironment event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginenvironment_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginenvironment_event_connection;

// subscribe to the BeginEnvironment event with a handler function keeping the connection
publisher->getEventBeginEnvironment().connect(beginenvironment_event_connection, beginenvironment_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginenvironment_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginenvironment_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginEnvironment event via the connection
beginenvironment_event_connection.disconnect();

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

	// A BeginEnvironment event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginEnvironment event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginEnvironment().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginenvironment_handler_id;

// subscribe to the BeginEnvironment event with a lambda handler function and keeping connection ID
beginenvironment_handler_id = publisher->getEventBeginEnvironment().connect(e_connections, []() {
		Log::message("\Handling BeginEnvironment event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginEnvironment().disconnect(beginenvironment_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginEnvironment events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginEnvironment().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginEnvironment().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndEnvironment () const

event triggered after the Environment rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndEnvironment event handler
void endenvironment_event_handler()
{
	Log::message("\Handling EndEnvironment event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endenvironment_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndEnvironment().connect(endenvironment_event_connections, endenvironment_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndEnvironment().connect(endenvironment_event_connections, []() {
		Log::message("\Handling EndEnvironment event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endenvironment_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endenvironment_event_connection;

// subscribe to the EndEnvironment event with a handler function keeping the connection
publisher->getEventEndEnvironment().connect(endenvironment_event_connection, endenvironment_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endenvironment_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endenvironment_event_connection.setEnabled(true);

// ...

// remove subscription to the EndEnvironment event via the connection
endenvironment_event_connection.disconnect();

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

	// A EndEnvironment event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndEnvironment event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndEnvironment().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endenvironment_handler_id;

// subscribe to the EndEnvironment event with a lambda handler function and keeping connection ID
endenvironment_handler_id = publisher->getEventEndEnvironment().connect(e_connections, []() {
		Log::message("\Handling EndEnvironment event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndEnvironment().disconnect(endenvironment_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndEnvironment events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndEnvironment().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndEnvironment().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginShadows () const

event triggered before the shadows rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginShadows event handler
void beginshadows_event_handler()
{
	Log::message("\Handling BeginShadows event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginshadows_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginShadows().connect(beginshadows_event_connections, beginshadows_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginShadows().connect(beginshadows_event_connections, []() {
		Log::message("\Handling BeginShadows event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginshadows_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginshadows_event_connection;

// subscribe to the BeginShadows event with a handler function keeping the connection
publisher->getEventBeginShadows().connect(beginshadows_event_connection, beginshadows_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginshadows_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginshadows_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginShadows event via the connection
beginshadows_event_connection.disconnect();

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

	// A BeginShadows event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginShadows event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginShadows().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginshadows_handler_id;

// subscribe to the BeginShadows event with a lambda handler function and keeping connection ID
beginshadows_handler_id = publisher->getEventBeginShadows().connect(e_connections, []() {
		Log::message("\Handling BeginShadows event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginShadows().disconnect(beginshadows_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginShadows events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginShadows().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginShadows().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginWorldShadow () const

event triggered before the stage of rendering shadows from World light sources. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWorldShadow event handler
void beginworldshadow_event_handler()
{
	Log::message("\Handling BeginWorldShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldshadow_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginWorldShadow().connect(beginworldshadow_event_connections, beginworldshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginWorldShadow().connect(beginworldshadow_event_connections, []() {
		Log::message("\Handling BeginWorldShadow event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginworldshadow_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginworldshadow_event_connection;

// subscribe to the BeginWorldShadow event with a handler function keeping the connection
publisher->getEventBeginWorldShadow().connect(beginworldshadow_event_connection, beginworldshadow_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginworldshadow_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginworldshadow_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWorldShadow event via the connection
beginworldshadow_event_connection.disconnect();

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

	// A BeginWorldShadow event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWorldShadow event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginWorldShadow().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginworldshadow_handler_id;

// subscribe to the BeginWorldShadow event with a lambda handler function and keeping connection ID
beginworldshadow_handler_id = publisher->getEventBeginWorldShadow().connect(e_connections, []() {
		Log::message("\Handling BeginWorldShadow event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginWorldShadow().disconnect(beginworldshadow_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWorldShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginWorldShadow().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginWorldShadow().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndWorldShadow () const

event triggered after the stage of rendering shadows from World light sources. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWorldShadow event handler
void endworldshadow_event_handler()
{
	Log::message("\Handling EndWorldShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldshadow_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndWorldShadow().connect(endworldshadow_event_connections, endworldshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndWorldShadow().connect(endworldshadow_event_connections, []() {
		Log::message("\Handling EndWorldShadow event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endworldshadow_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endworldshadow_event_connection;

// subscribe to the EndWorldShadow event with a handler function keeping the connection
publisher->getEventEndWorldShadow().connect(endworldshadow_event_connection, endworldshadow_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endworldshadow_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endworldshadow_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWorldShadow event via the connection
endworldshadow_event_connection.disconnect();

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

	// A EndWorldShadow event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWorldShadow event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndWorldShadow().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endworldshadow_handler_id;

// subscribe to the EndWorldShadow event with a lambda handler function and keeping connection ID
endworldshadow_handler_id = publisher->getEventEndWorldShadow().connect(e_connections, []() {
		Log::message("\Handling EndWorldShadow event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndWorldShadow().disconnect(endworldshadow_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWorldShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndWorldShadow().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndWorldShadow().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginProjShadow () const

event triggered before the stage of rendering shadows from Projected light sources. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginProjShadow event handler
void beginprojshadow_event_handler()
{
	Log::message("\Handling BeginProjShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginprojshadow_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginProjShadow().connect(beginprojshadow_event_connections, beginprojshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginProjShadow().connect(beginprojshadow_event_connections, []() {
		Log::message("\Handling BeginProjShadow event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginprojshadow_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginprojshadow_event_connection;

// subscribe to the BeginProjShadow event with a handler function keeping the connection
publisher->getEventBeginProjShadow().connect(beginprojshadow_event_connection, beginprojshadow_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginprojshadow_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginprojshadow_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginProjShadow event via the connection
beginprojshadow_event_connection.disconnect();

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

	// A BeginProjShadow event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginProjShadow event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginProjShadow().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginprojshadow_handler_id;

// subscribe to the BeginProjShadow event with a lambda handler function and keeping connection ID
beginprojshadow_handler_id = publisher->getEventBeginProjShadow().connect(e_connections, []() {
		Log::message("\Handling BeginProjShadow event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginProjShadow().disconnect(beginprojshadow_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginProjShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginProjShadow().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginProjShadow().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndProjShadow () const

event triggered after the stage of rendering shadows from Projected light sources. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndProjShadow event handler
void endprojshadow_event_handler()
{
	Log::message("\Handling EndProjShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endprojshadow_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndProjShadow().connect(endprojshadow_event_connections, endprojshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndProjShadow().connect(endprojshadow_event_connections, []() {
		Log::message("\Handling EndProjShadow event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endprojshadow_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endprojshadow_event_connection;

// subscribe to the EndProjShadow event with a handler function keeping the connection
publisher->getEventEndProjShadow().connect(endprojshadow_event_connection, endprojshadow_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endprojshadow_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endprojshadow_event_connection.setEnabled(true);

// ...

// remove subscription to the EndProjShadow event via the connection
endprojshadow_event_connection.disconnect();

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

	// A EndProjShadow event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndProjShadow event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndProjShadow().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endprojshadow_handler_id;

// subscribe to the EndProjShadow event with a lambda handler function and keeping connection ID
endprojshadow_handler_id = publisher->getEventEndProjShadow().connect(e_connections, []() {
		Log::message("\Handling EndProjShadow event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndProjShadow().disconnect(endprojshadow_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndProjShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndProjShadow().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndProjShadow().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginOmniShadow () const

event triggered before the stage of rendering shadows from Omni light sources. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginOmniShadow event handler
void beginomnishadow_event_handler()
{
	Log::message("\Handling BeginOmniShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginomnishadow_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginOmniShadow().connect(beginomnishadow_event_connections, beginomnishadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginOmniShadow().connect(beginomnishadow_event_connections, []() {
		Log::message("\Handling BeginOmniShadow event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginomnishadow_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginomnishadow_event_connection;

// subscribe to the BeginOmniShadow event with a handler function keeping the connection
publisher->getEventBeginOmniShadow().connect(beginomnishadow_event_connection, beginomnishadow_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginomnishadow_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginomnishadow_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginOmniShadow event via the connection
beginomnishadow_event_connection.disconnect();

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

	// A BeginOmniShadow event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginOmniShadow event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginOmniShadow().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginomnishadow_handler_id;

// subscribe to the BeginOmniShadow event with a lambda handler function and keeping connection ID
beginomnishadow_handler_id = publisher->getEventBeginOmniShadow().connect(e_connections, []() {
		Log::message("\Handling BeginOmniShadow event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginOmniShadow().disconnect(beginomnishadow_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginOmniShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginOmniShadow().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginOmniShadow().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndOmniShadow () const

event triggered after the stage of rendering shadows from Omni light sources. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndOmniShadow event handler
void endomnishadow_event_handler()
{
	Log::message("\Handling EndOmniShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endomnishadow_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndOmniShadow().connect(endomnishadow_event_connections, endomnishadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndOmniShadow().connect(endomnishadow_event_connections, []() {
		Log::message("\Handling EndOmniShadow event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endomnishadow_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endomnishadow_event_connection;

// subscribe to the EndOmniShadow event with a handler function keeping the connection
publisher->getEventEndOmniShadow().connect(endomnishadow_event_connection, endomnishadow_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endomnishadow_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endomnishadow_event_connection.setEnabled(true);

// ...

// remove subscription to the EndOmniShadow event via the connection
endomnishadow_event_connection.disconnect();

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

	// A EndOmniShadow event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndOmniShadow event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndOmniShadow().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endomnishadow_handler_id;

// subscribe to the EndOmniShadow event with a lambda handler function and keeping connection ID
endomnishadow_handler_id = publisher->getEventEndOmniShadow().connect(e_connections, []() {
		Log::message("\Handling EndOmniShadow event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndOmniShadow().disconnect(endomnishadow_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndOmniShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndOmniShadow().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndOmniShadow().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndShadows () const

event triggered after the shadows rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndShadows event handler
void endshadows_event_handler()
{
	Log::message("\Handling EndShadows event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endshadows_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndShadows().connect(endshadows_event_connections, endshadows_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndShadows().connect(endshadows_event_connections, []() {
		Log::message("\Handling EndShadows event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endshadows_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endshadows_event_connection;

// subscribe to the EndShadows event with a handler function keeping the connection
publisher->getEventEndShadows().connect(endshadows_event_connection, endshadows_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endshadows_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endshadows_event_connection.setEnabled(true);

// ...

// remove subscription to the EndShadows event via the connection
endshadows_event_connection.disconnect();

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

	// A EndShadows event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndShadows event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndShadows().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endshadows_handler_id;

// subscribe to the EndShadows event with a lambda handler function and keeping connection ID
endshadows_handler_id = publisher->getEventEndShadows().connect(e_connections, []() {
		Log::message("\Handling EndShadows event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndShadows().disconnect(endshadows_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndShadows events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndShadows().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndShadows().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginScreen () const

event triggered before the stage of rendering each screen (a stereo image has 2 screens, while a cubemap will have 6). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginScreen event handler
void beginscreen_event_handler()
{
	Log::message("\Handling BeginScreen event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginscreen_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginScreen().connect(beginscreen_event_connections, beginscreen_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginScreen().connect(beginscreen_event_connections, []() {
		Log::message("\Handling BeginScreen event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginscreen_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginscreen_event_connection;

// subscribe to the BeginScreen event with a handler function keeping the connection
publisher->getEventBeginScreen().connect(beginscreen_event_connection, beginscreen_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginscreen_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginscreen_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginScreen event via the connection
beginscreen_event_connection.disconnect();

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

	// A BeginScreen event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginScreen event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginScreen().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginscreen_handler_id;

// subscribe to the BeginScreen event with a lambda handler function and keeping connection ID
beginscreen_handler_id = publisher->getEventBeginScreen().connect(e_connections, []() {
		Log::message("\Handling BeginScreen event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginScreen().disconnect(beginscreen_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginScreen events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginScreen().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginScreen().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginMixedRealityBlendMaskColor () const

event triggered before the mask for Mixed Reality is rendered (after Common Camera for clouds and before Opacity GBuffer). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginMixedRealityBlendMaskColor event handler
void beginmixedrealityblendmaskcolor_event_handler()
{
	Log::message("\Handling BeginMixedRealityBlendMaskColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginmixedrealityblendmaskcolor_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginMixedRealityBlendMaskColor().connect(beginmixedrealityblendmaskcolor_event_connections, beginmixedrealityblendmaskcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginMixedRealityBlendMaskColor().connect(beginmixedrealityblendmaskcolor_event_connections, []() {
		Log::message("\Handling BeginMixedRealityBlendMaskColor event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginmixedrealityblendmaskcolor_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginmixedrealityblendmaskcolor_event_connection;

// subscribe to the BeginMixedRealityBlendMaskColor event with a handler function keeping the connection
publisher->getEventBeginMixedRealityBlendMaskColor().connect(beginmixedrealityblendmaskcolor_event_connection, beginmixedrealityblendmaskcolor_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginmixedrealityblendmaskcolor_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginmixedrealityblendmaskcolor_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginMixedRealityBlendMaskColor event via the connection
beginmixedrealityblendmaskcolor_event_connection.disconnect();

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

	// A BeginMixedRealityBlendMaskColor event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginMixedRealityBlendMaskColor event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginMixedRealityBlendMaskColor().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginmixedrealityblendmaskcolor_handler_id;

// subscribe to the BeginMixedRealityBlendMaskColor event with a lambda handler function and keeping connection ID
beginmixedrealityblendmaskcolor_handler_id = publisher->getEventBeginMixedRealityBlendMaskColor().connect(e_connections, []() {
		Log::message("\Handling BeginMixedRealityBlendMaskColor event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginMixedRealityBlendMaskColor().disconnect(beginmixedrealityblendmaskcolor_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginMixedRealityBlendMaskColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginMixedRealityBlendMaskColor().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginMixedRealityBlendMaskColor().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndMixedRealityBlendMaskColor () const

event triggered after the mask for Mixed Reality is rendered (after Common Camera for clouds and before Opacity GBuffer). You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndMixedRealityBlendMaskColor event handler
void endmixedrealityblendmaskcolor_event_handler()
{
	Log::message("\Handling EndMixedRealityBlendMaskColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endmixedrealityblendmaskcolor_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndMixedRealityBlendMaskColor().connect(endmixedrealityblendmaskcolor_event_connections, endmixedrealityblendmaskcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndMixedRealityBlendMaskColor().connect(endmixedrealityblendmaskcolor_event_connections, []() {
		Log::message("\Handling EndMixedRealityBlendMaskColor event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endmixedrealityblendmaskcolor_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endmixedrealityblendmaskcolor_event_connection;

// subscribe to the EndMixedRealityBlendMaskColor event with a handler function keeping the connection
publisher->getEventEndMixedRealityBlendMaskColor().connect(endmixedrealityblendmaskcolor_event_connection, endmixedrealityblendmaskcolor_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endmixedrealityblendmaskcolor_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endmixedrealityblendmaskcolor_event_connection.setEnabled(true);

// ...

// remove subscription to the EndMixedRealityBlendMaskColor event via the connection
endmixedrealityblendmaskcolor_event_connection.disconnect();

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

	// A EndMixedRealityBlendMaskColor event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndMixedRealityBlendMaskColor event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndMixedRealityBlendMaskColor().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endmixedrealityblendmaskcolor_handler_id;

// subscribe to the EndMixedRealityBlendMaskColor event with a lambda handler function and keeping connection ID
endmixedrealityblendmaskcolor_handler_id = publisher->getEventEndMixedRealityBlendMaskColor().connect(e_connections, []() {
		Log::message("\Handling EndMixedRealityBlendMaskColor event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndMixedRealityBlendMaskColor().disconnect(endmixedrealityblendmaskcolor_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndMixedRealityBlendMaskColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndMixedRealityBlendMaskColor().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndMixedRealityBlendMaskColor().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginOpacityGBuffer () const

event triggered before filling the Gbuffer. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginOpacityGBuffer event handler
void beginopacitygbuffer_event_handler()
{
	Log::message("\Handling BeginOpacityGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacitygbuffer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginOpacityGBuffer().connect(beginopacitygbuffer_event_connections, beginopacitygbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginOpacityGBuffer().connect(beginopacitygbuffer_event_connections, []() {
		Log::message("\Handling BeginOpacityGBuffer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginopacitygbuffer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginopacitygbuffer_event_connection;

// subscribe to the BeginOpacityGBuffer event with a handler function keeping the connection
publisher->getEventBeginOpacityGBuffer().connect(beginopacitygbuffer_event_connection, beginopacitygbuffer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginopacitygbuffer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginopacitygbuffer_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginOpacityGBuffer event via the connection
beginopacitygbuffer_event_connection.disconnect();

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

	// A BeginOpacityGBuffer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginOpacityGBuffer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginOpacityGBuffer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginopacitygbuffer_handler_id;

// subscribe to the BeginOpacityGBuffer event with a lambda handler function and keeping connection ID
beginopacitygbuffer_handler_id = publisher->getEventBeginOpacityGBuffer().connect(e_connections, []() {
		Log::message("\Handling BeginOpacityGBuffer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginOpacityGBuffer().disconnect(beginopacitygbuffer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginOpacityGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginOpacityGBuffer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginOpacityGBuffer().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventBeginAuxiliarySurfaces () const

event triggered before auxiliary surfaces rendering. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginAuxiliarySurfaces event handler
void beginauxiliarysurfaces_event_handler()
{
	Log::message("\Handling BeginAuxiliarySurfaces event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginauxiliarysurfaces_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Viewport::getEventBeginAuxiliarySurfaces().connect(beginauxiliarysurfaces_event_connections, beginauxiliarysurfaces_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Viewport::getEventBeginAuxiliarySurfaces().connect(beginauxiliarysurfaces_event_connections, []() {
		Log::message("\Handling BeginAuxiliarySurfaces event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginauxiliarysurfaces_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginauxiliarysurfaces_event_connection;

// subscribe to the BeginAuxiliarySurfaces event with a handler function keeping the connection
Viewport::getEventBeginAuxiliarySurfaces().connect(beginauxiliarysurfaces_event_connection, beginauxiliarysurfaces_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginauxiliarysurfaces_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginauxiliarysurfaces_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginAuxiliarySurfaces event via the connection
beginauxiliarysurfaces_event_connection.disconnect();

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

	// A BeginAuxiliarySurfaces event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginAuxiliarySurfaces event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Viewport::getEventBeginAuxiliarySurfaces().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginauxiliarysurfaces_handler_id;

// subscribe to the BeginAuxiliarySurfaces event with a lambda handler function and keeping connection ID
beginauxiliarysurfaces_handler_id = Viewport::getEventBeginAuxiliarySurfaces().connect(e_connections, []() {
		Log::message("\Handling BeginAuxiliarySurfaces event (lambda).\n");
	}
);

// remove the subscription later using the ID
Viewport::getEventBeginAuxiliarySurfaces().disconnect(beginauxiliarysurfaces_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginAuxiliarySurfaces events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Viewport::getEventBeginAuxiliarySurfaces().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Viewport::getEventBeginAuxiliarySurfaces().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventEndAuxiliarySurfaces () const

event triggered after auxiliary surfaces rendering. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndAuxiliarySurfaces event handler
void endauxiliarysurfaces_event_handler()
{
	Log::message("\Handling EndAuxiliarySurfaces event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endauxiliarysurfaces_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Viewport::getEventEndAuxiliarySurfaces().connect(endauxiliarysurfaces_event_connections, endauxiliarysurfaces_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Viewport::getEventEndAuxiliarySurfaces().connect(endauxiliarysurfaces_event_connections, []() {
		Log::message("\Handling EndAuxiliarySurfaces event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endauxiliarysurfaces_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endauxiliarysurfaces_event_connection;

// subscribe to the EndAuxiliarySurfaces event with a handler function keeping the connection
Viewport::getEventEndAuxiliarySurfaces().connect(endauxiliarysurfaces_event_connection, endauxiliarysurfaces_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endauxiliarysurfaces_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endauxiliarysurfaces_event_connection.setEnabled(true);

// ...

// remove subscription to the EndAuxiliarySurfaces event via the connection
endauxiliarysurfaces_event_connection.disconnect();

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

	// A EndAuxiliarySurfaces event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndAuxiliarySurfaces event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Viewport::getEventEndAuxiliarySurfaces().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endauxiliarysurfaces_handler_id;

// subscribe to the EndAuxiliarySurfaces event with a lambda handler function and keeping connection ID
endauxiliarysurfaces_handler_id = Viewport::getEventEndAuxiliarySurfaces().connect(e_connections, []() {
		Log::message("\Handling EndAuxiliarySurfaces event (lambda).\n");
	}
);

// remove the subscription later using the ID
Viewport::getEventEndAuxiliarySurfaces().disconnect(endauxiliarysurfaces_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndAuxiliarySurfaces events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Viewport::getEventEndAuxiliarySurfaces().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Viewport::getEventEndAuxiliarySurfaces().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndOpacityGBuffer () const

event triggered after filling the Gbuffer. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndOpacityGBuffer event handler
void endopacitygbuffer_event_handler()
{
	Log::message("\Handling EndOpacityGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacitygbuffer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndOpacityGBuffer().connect(endopacitygbuffer_event_connections, endopacitygbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndOpacityGBuffer().connect(endopacitygbuffer_event_connections, []() {
		Log::message("\Handling EndOpacityGBuffer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endopacitygbuffer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endopacitygbuffer_event_connection;

// subscribe to the EndOpacityGBuffer event with a handler function keeping the connection
publisher->getEventEndOpacityGBuffer().connect(endopacitygbuffer_event_connection, endopacitygbuffer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endopacitygbuffer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endopacitygbuffer_event_connection.setEnabled(true);

// ...

// remove subscription to the EndOpacityGBuffer event via the connection
endopacitygbuffer_event_connection.disconnect();

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

	// A EndOpacityGBuffer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndOpacityGBuffer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndOpacityGBuffer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endopacitygbuffer_handler_id;

// subscribe to the EndOpacityGBuffer event with a lambda handler function and keeping connection ID
endopacitygbuffer_handler_id = publisher->getEventEndOpacityGBuffer().connect(e_connections, []() {
		Log::message("\Handling EndOpacityGBuffer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndOpacityGBuffer().disconnect(endopacitygbuffer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndOpacityGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndOpacityGBuffer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndOpacityGBuffer().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginOpacityDecals () const

event triggered before the opacity decals rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginOpacityDecals event handler
void beginopacitydecals_event_handler()
{
	Log::message("\Handling BeginOpacityDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacitydecals_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginOpacityDecals().connect(beginopacitydecals_event_connections, beginopacitydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginOpacityDecals().connect(beginopacitydecals_event_connections, []() {
		Log::message("\Handling BeginOpacityDecals event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginopacitydecals_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginopacitydecals_event_connection;

// subscribe to the BeginOpacityDecals event with a handler function keeping the connection
publisher->getEventBeginOpacityDecals().connect(beginopacitydecals_event_connection, beginopacitydecals_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginopacitydecals_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginopacitydecals_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginOpacityDecals event via the connection
beginopacitydecals_event_connection.disconnect();

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

	// A BeginOpacityDecals event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginOpacityDecals event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginOpacityDecals().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginopacitydecals_handler_id;

// subscribe to the BeginOpacityDecals event with a lambda handler function and keeping connection ID
beginopacitydecals_handler_id = publisher->getEventBeginOpacityDecals().connect(e_connections, []() {
		Log::message("\Handling BeginOpacityDecals event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginOpacityDecals().disconnect(beginopacitydecals_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginOpacityDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginOpacityDecals().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginOpacityDecals().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndOpacityDecals () const

event triggered after the opacity decals rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndOpacityDecals event handler
void endopacitydecals_event_handler()
{
	Log::message("\Handling EndOpacityDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacitydecals_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndOpacityDecals().connect(endopacitydecals_event_connections, endopacitydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndOpacityDecals().connect(endopacitydecals_event_connections, []() {
		Log::message("\Handling EndOpacityDecals event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endopacitydecals_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endopacitydecals_event_connection;

// subscribe to the EndOpacityDecals event with a handler function keeping the connection
publisher->getEventEndOpacityDecals().connect(endopacitydecals_event_connection, endopacitydecals_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endopacitydecals_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endopacitydecals_event_connection.setEnabled(true);

// ...

// remove subscription to the EndOpacityDecals event via the connection
endopacitydecals_event_connection.disconnect();

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

	// A EndOpacityDecals event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndOpacityDecals event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndOpacityDecals().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endopacitydecals_handler_id;

// subscribe to the EndOpacityDecals event with a lambda handler function and keeping connection ID
endopacitydecals_handler_id = publisher->getEventEndOpacityDecals().connect(e_connections, []() {
		Log::message("\Handling EndOpacityDecals event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndOpacityDecals().disconnect(endopacitydecals_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndOpacityDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndOpacityDecals().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndOpacityDecals().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventBeginAuxiliaryDecals () const

event triggered before the auxiliary decals rendering. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginAuxiliaryDecals event handler
void beginauxiliarydecals_event_handler()
{
	Log::message("\Handling BeginAuxiliaryDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginauxiliarydecals_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Viewport::getEventBeginAuxiliaryDecals().connect(beginauxiliarydecals_event_connections, beginauxiliarydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Viewport::getEventBeginAuxiliaryDecals().connect(beginauxiliarydecals_event_connections, []() {
		Log::message("\Handling BeginAuxiliaryDecals event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginauxiliarydecals_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginauxiliarydecals_event_connection;

// subscribe to the BeginAuxiliaryDecals event with a handler function keeping the connection
Viewport::getEventBeginAuxiliaryDecals().connect(beginauxiliarydecals_event_connection, beginauxiliarydecals_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginauxiliarydecals_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginauxiliarydecals_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginAuxiliaryDecals event via the connection
beginauxiliarydecals_event_connection.disconnect();

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

	// A BeginAuxiliaryDecals event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginAuxiliaryDecals event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Viewport::getEventBeginAuxiliaryDecals().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginauxiliarydecals_handler_id;

// subscribe to the BeginAuxiliaryDecals event with a lambda handler function and keeping connection ID
beginauxiliarydecals_handler_id = Viewport::getEventBeginAuxiliaryDecals().connect(e_connections, []() {
		Log::message("\Handling BeginAuxiliaryDecals event (lambda).\n");
	}
);

// remove the subscription later using the ID
Viewport::getEventBeginAuxiliaryDecals().disconnect(beginauxiliarydecals_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginAuxiliaryDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Viewport::getEventBeginAuxiliaryDecals().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Viewport::getEventBeginAuxiliaryDecals().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventEndAuxiliaryDecals () const

event triggered after the auxiliary decals rendering. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndAuxiliaryDecals event handler
void endauxiliarydecals_event_handler()
{
	Log::message("\Handling EndAuxiliaryDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endauxiliarydecals_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Viewport::getEventEndAuxiliaryDecals().connect(endauxiliarydecals_event_connections, endauxiliarydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Viewport::getEventEndAuxiliaryDecals().connect(endauxiliarydecals_event_connections, []() {
		Log::message("\Handling EndAuxiliaryDecals event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endauxiliarydecals_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endauxiliarydecals_event_connection;

// subscribe to the EndAuxiliaryDecals event with a handler function keeping the connection
Viewport::getEventEndAuxiliaryDecals().connect(endauxiliarydecals_event_connection, endauxiliarydecals_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endauxiliarydecals_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endauxiliarydecals_event_connection.setEnabled(true);

// ...

// remove subscription to the EndAuxiliaryDecals event via the connection
endauxiliarydecals_event_connection.disconnect();

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

	// A EndAuxiliaryDecals event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndAuxiliaryDecals event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Viewport::getEventEndAuxiliaryDecals().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endauxiliarydecals_handler_id;

// subscribe to the EndAuxiliaryDecals event with a lambda handler function and keeping connection ID
endauxiliarydecals_handler_id = Viewport::getEventEndAuxiliaryDecals().connect(e_connections, []() {
		Log::message("\Handling EndAuxiliaryDecals event (lambda).\n");
	}
);

// remove the subscription later using the ID
Viewport::getEventEndAuxiliaryDecals().disconnect(endauxiliarydecals_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndAuxiliaryDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Viewport::getEventEndAuxiliaryDecals().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Viewport::getEventEndAuxiliaryDecals().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginCurvature () const

event triggered before the [SSBevel](../../../editor2/settings/render_settings/ssbevel/index.md) effect rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginCurvature event handler
void begincurvature_event_handler()
{
	Log::message("\Handling BeginCurvature event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincurvature_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginCurvature().connect(begincurvature_event_connections, begincurvature_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginCurvature().connect(begincurvature_event_connections, []() {
		Log::message("\Handling BeginCurvature event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begincurvature_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begincurvature_event_connection;

// subscribe to the BeginCurvature event with a handler function keeping the connection
publisher->getEventBeginCurvature().connect(begincurvature_event_connection, begincurvature_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begincurvature_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begincurvature_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginCurvature event via the connection
begincurvature_event_connection.disconnect();

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

	// A BeginCurvature event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginCurvature event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginCurvature().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begincurvature_handler_id;

// subscribe to the BeginCurvature event with a lambda handler function and keeping connection ID
begincurvature_handler_id = publisher->getEventBeginCurvature().connect(e_connections, []() {
		Log::message("\Handling BeginCurvature event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginCurvature().disconnect(begincurvature_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginCurvature events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginCurvature().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginCurvature().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndCurvature () const

event triggered after the [SSBevel](../../../editor2/settings/render_settings/ssbevel/index.md) effect rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndCurvature event handler
void endcurvature_event_handler()
{
	Log::message("\Handling EndCurvature event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcurvature_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndCurvature().connect(endcurvature_event_connections, endcurvature_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndCurvature().connect(endcurvature_event_connections, []() {
		Log::message("\Handling EndCurvature event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endcurvature_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endcurvature_event_connection;

// subscribe to the EndCurvature event with a handler function keeping the connection
publisher->getEventEndCurvature().connect(endcurvature_event_connection, endcurvature_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endcurvature_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endcurvature_event_connection.setEnabled(true);

// ...

// remove subscription to the EndCurvature event via the connection
endcurvature_event_connection.disconnect();

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

	// A EndCurvature event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndCurvature event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndCurvature().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endcurvature_handler_id;

// subscribe to the EndCurvature event with a lambda handler function and keeping connection ID
endcurvature_handler_id = publisher->getEventEndCurvature().connect(e_connections, []() {
		Log::message("\Handling EndCurvature event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndCurvature().disconnect(endcurvature_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndCurvature events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndCurvature().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndCurvature().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginCurvatureComposite () const

event triggered before the curvature rendering stage for the [SSDirt](../../../editor2/settings/render_settings/ssdirt/index.md) effect. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginCurvatureComposite event handler
void begincurvaturecomposite_event_handler()
{
	Log::message("\Handling BeginCurvatureComposite event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincurvaturecomposite_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginCurvatureComposite().connect(begincurvaturecomposite_event_connections, begincurvaturecomposite_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginCurvatureComposite().connect(begincurvaturecomposite_event_connections, []() {
		Log::message("\Handling BeginCurvatureComposite event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begincurvaturecomposite_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begincurvaturecomposite_event_connection;

// subscribe to the BeginCurvatureComposite event with a handler function keeping the connection
publisher->getEventBeginCurvatureComposite().connect(begincurvaturecomposite_event_connection, begincurvaturecomposite_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begincurvaturecomposite_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begincurvaturecomposite_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginCurvatureComposite event via the connection
begincurvaturecomposite_event_connection.disconnect();

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

	// A BeginCurvatureComposite event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginCurvatureComposite event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginCurvatureComposite().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begincurvaturecomposite_handler_id;

// subscribe to the BeginCurvatureComposite event with a lambda handler function and keeping connection ID
begincurvaturecomposite_handler_id = publisher->getEventBeginCurvatureComposite().connect(e_connections, []() {
		Log::message("\Handling BeginCurvatureComposite event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginCurvatureComposite().disconnect(begincurvaturecomposite_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginCurvatureComposite events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginCurvatureComposite().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginCurvatureComposite().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndCurvatureComposite () const

event triggered after the curvature rendering stage for the [SSDirt](../../../editor2/settings/render_settings/ssdirt/index.md) effect. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndCurvatureComposite event handler
void endcurvaturecomposite_event_handler()
{
	Log::message("\Handling EndCurvatureComposite event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcurvaturecomposite_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndCurvatureComposite().connect(endcurvaturecomposite_event_connections, endcurvaturecomposite_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndCurvatureComposite().connect(endcurvaturecomposite_event_connections, []() {
		Log::message("\Handling EndCurvatureComposite event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endcurvaturecomposite_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endcurvaturecomposite_event_connection;

// subscribe to the EndCurvatureComposite event with a handler function keeping the connection
publisher->getEventEndCurvatureComposite().connect(endcurvaturecomposite_event_connection, endcurvaturecomposite_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endcurvaturecomposite_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endcurvaturecomposite_event_connection.setEnabled(true);

// ...

// remove subscription to the EndCurvatureComposite event via the connection
endcurvaturecomposite_event_connection.disconnect();

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

	// A EndCurvatureComposite event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndCurvatureComposite event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndCurvatureComposite().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endcurvaturecomposite_handler_id;

// subscribe to the EndCurvatureComposite event with a lambda handler function and keeping connection ID
endcurvaturecomposite_handler_id = publisher->getEventEndCurvatureComposite().connect(e_connections, []() {
		Log::message("\Handling EndCurvatureComposite event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndCurvatureComposite().disconnect(endcurvaturecomposite_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndCurvatureComposite events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndCurvatureComposite().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndCurvatureComposite().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginSSRTGI () const

event triggered before the SSRTGI rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSSRTGI event handler
void beginssrtgi_event_handler()
{
	Log::message("\Handling BeginSSRTGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssrtgi_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginSSRTGI().connect(beginssrtgi_event_connections, beginssrtgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginSSRTGI().connect(beginssrtgi_event_connections, []() {
		Log::message("\Handling BeginSSRTGI event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginssrtgi_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginssrtgi_event_connection;

// subscribe to the BeginSSRTGI event with a handler function keeping the connection
publisher->getEventBeginSSRTGI().connect(beginssrtgi_event_connection, beginssrtgi_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginssrtgi_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginssrtgi_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSSRTGI event via the connection
beginssrtgi_event_connection.disconnect();

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

	// A BeginSSRTGI event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSSRTGI event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginSSRTGI().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginssrtgi_handler_id;

// subscribe to the BeginSSRTGI event with a lambda handler function and keeping connection ID
beginssrtgi_handler_id = publisher->getEventBeginSSRTGI().connect(e_connections, []() {
		Log::message("\Handling BeginSSRTGI event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginSSRTGI().disconnect(beginssrtgi_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSSRTGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginSSRTGI().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginSSRTGI().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndSSRTGI () const

event triggered after the SSRTGI rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSSRTGI event handler
void endssrtgi_event_handler()
{
	Log::message("\Handling EndSSRTGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssrtgi_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndSSRTGI().connect(endssrtgi_event_connections, endssrtgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndSSRTGI().connect(endssrtgi_event_connections, []() {
		Log::message("\Handling EndSSRTGI event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endssrtgi_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endssrtgi_event_connection;

// subscribe to the EndSSRTGI event with a handler function keeping the connection
publisher->getEventEndSSRTGI().connect(endssrtgi_event_connection, endssrtgi_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endssrtgi_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endssrtgi_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSSRTGI event via the connection
endssrtgi_event_connection.disconnect();

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

	// A EndSSRTGI event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSSRTGI event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndSSRTGI().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endssrtgi_handler_id;

// subscribe to the EndSSRTGI event with a lambda handler function and keeping connection ID
endssrtgi_handler_id = publisher->getEventEndSSRTGI().connect(e_connections, []() {
		Log::message("\Handling EndSSRTGI event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndSSRTGI().disconnect(endssrtgi_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSSRTGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndSSRTGI().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndSSRTGI().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginOpacityLights () const

event triggered before the opacity lightgs rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginOpacityLights event handler
void beginopacitylights_event_handler()
{
	Log::message("\Handling BeginOpacityLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacitylights_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginOpacityLights().connect(beginopacitylights_event_connections, beginopacitylights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginOpacityLights().connect(beginopacitylights_event_connections, []() {
		Log::message("\Handling BeginOpacityLights event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginopacitylights_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginopacitylights_event_connection;

// subscribe to the BeginOpacityLights event with a handler function keeping the connection
publisher->getEventBeginOpacityLights().connect(beginopacitylights_event_connection, beginopacitylights_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginopacitylights_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginopacitylights_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginOpacityLights event via the connection
beginopacitylights_event_connection.disconnect();

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

	// A BeginOpacityLights event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginOpacityLights event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginOpacityLights().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginopacitylights_handler_id;

// subscribe to the BeginOpacityLights event with a lambda handler function and keeping connection ID
beginopacitylights_handler_id = publisher->getEventBeginOpacityLights().connect(e_connections, []() {
		Log::message("\Handling BeginOpacityLights event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginOpacityLights().disconnect(beginopacitylights_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginOpacityLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginOpacityLights().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginOpacityLights().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndOpacityLights () const

event triggered after the opacity lightgs rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndOpacityLights event handler
void endopacitylights_event_handler()
{
	Log::message("\Handling EndOpacityLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacitylights_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndOpacityLights().connect(endopacitylights_event_connections, endopacitylights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndOpacityLights().connect(endopacitylights_event_connections, []() {
		Log::message("\Handling EndOpacityLights event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endopacitylights_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endopacitylights_event_connection;

// subscribe to the EndOpacityLights event with a handler function keeping the connection
publisher->getEventEndOpacityLights().connect(endopacitylights_event_connection, endopacitylights_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endopacitylights_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endopacitylights_event_connection.setEnabled(true);

// ...

// remove subscription to the EndOpacityLights event via the connection
endopacitylights_event_connection.disconnect();

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

	// A EndOpacityLights event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndOpacityLights event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndOpacityLights().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endopacitylights_handler_id;

// subscribe to the EndOpacityLights event with a lambda handler function and keeping connection ID
endopacitylights_handler_id = publisher->getEventEndOpacityLights().connect(e_connections, []() {
		Log::message("\Handling EndOpacityLights event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndOpacityLights().disconnect(endopacitylights_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndOpacityLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndOpacityLights().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndOpacityLights().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginOpacityVoxelProbes () const

event triggered before the opacity voxel probes rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginOpacityVoxelProbes event handler
void beginopacityvoxelprobes_event_handler()
{
	Log::message("\Handling BeginOpacityVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacityvoxelprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginOpacityVoxelProbes().connect(beginopacityvoxelprobes_event_connections, beginopacityvoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginOpacityVoxelProbes().connect(beginopacityvoxelprobes_event_connections, []() {
		Log::message("\Handling BeginOpacityVoxelProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginopacityvoxelprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginopacityvoxelprobes_event_connection;

// subscribe to the BeginOpacityVoxelProbes event with a handler function keeping the connection
publisher->getEventBeginOpacityVoxelProbes().connect(beginopacityvoxelprobes_event_connection, beginopacityvoxelprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginopacityvoxelprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginopacityvoxelprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginOpacityVoxelProbes event via the connection
beginopacityvoxelprobes_event_connection.disconnect();

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

	// A BeginOpacityVoxelProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginOpacityVoxelProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginOpacityVoxelProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginopacityvoxelprobes_handler_id;

// subscribe to the BeginOpacityVoxelProbes event with a lambda handler function and keeping connection ID
beginopacityvoxelprobes_handler_id = publisher->getEventBeginOpacityVoxelProbes().connect(e_connections, []() {
		Log::message("\Handling BeginOpacityVoxelProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginOpacityVoxelProbes().disconnect(beginopacityvoxelprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginOpacityVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginOpacityVoxelProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginOpacityVoxelProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndOpacityVoxelProbes () const

event triggered after the opacity voxel probes rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndOpacityVoxelProbes event handler
void endopacityvoxelprobes_event_handler()
{
	Log::message("\Handling EndOpacityVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacityvoxelprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndOpacityVoxelProbes().connect(endopacityvoxelprobes_event_connections, endopacityvoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndOpacityVoxelProbes().connect(endopacityvoxelprobes_event_connections, []() {
		Log::message("\Handling EndOpacityVoxelProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endopacityvoxelprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endopacityvoxelprobes_event_connection;

// subscribe to the EndOpacityVoxelProbes event with a handler function keeping the connection
publisher->getEventEndOpacityVoxelProbes().connect(endopacityvoxelprobes_event_connection, endopacityvoxelprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endopacityvoxelprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endopacityvoxelprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the EndOpacityVoxelProbes event via the connection
endopacityvoxelprobes_event_connection.disconnect();

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

	// A EndOpacityVoxelProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndOpacityVoxelProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndOpacityVoxelProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endopacityvoxelprobes_handler_id;

// subscribe to the EndOpacityVoxelProbes event with a lambda handler function and keeping connection ID
endopacityvoxelprobes_handler_id = publisher->getEventEndOpacityVoxelProbes().connect(e_connections, []() {
		Log::message("\Handling EndOpacityVoxelProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndOpacityVoxelProbes().disconnect(endopacityvoxelprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndOpacityVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndOpacityVoxelProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndOpacityVoxelProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginOpacityEnvironmentProbes () const

event triggered before the opacity environment probes rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginOpacityEnvironmentProbes event handler
void beginopacityenvironmentprobes_event_handler()
{
	Log::message("\Handling BeginOpacityEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacityenvironmentprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginOpacityEnvironmentProbes().connect(beginopacityenvironmentprobes_event_connections, beginopacityenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginOpacityEnvironmentProbes().connect(beginopacityenvironmentprobes_event_connections, []() {
		Log::message("\Handling BeginOpacityEnvironmentProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginopacityenvironmentprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginopacityenvironmentprobes_event_connection;

// subscribe to the BeginOpacityEnvironmentProbes event with a handler function keeping the connection
publisher->getEventBeginOpacityEnvironmentProbes().connect(beginopacityenvironmentprobes_event_connection, beginopacityenvironmentprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginopacityenvironmentprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginopacityenvironmentprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginOpacityEnvironmentProbes event via the connection
beginopacityenvironmentprobes_event_connection.disconnect();

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

	// A BeginOpacityEnvironmentProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginOpacityEnvironmentProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginOpacityEnvironmentProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginopacityenvironmentprobes_handler_id;

// subscribe to the BeginOpacityEnvironmentProbes event with a lambda handler function and keeping connection ID
beginopacityenvironmentprobes_handler_id = publisher->getEventBeginOpacityEnvironmentProbes().connect(e_connections, []() {
		Log::message("\Handling BeginOpacityEnvironmentProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginOpacityEnvironmentProbes().disconnect(beginopacityenvironmentprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginOpacityEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginOpacityEnvironmentProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginOpacityEnvironmentProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndOpacityEnvironmentProbes () const

event triggered after the opacity environment probes rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndOpacityEnvironmentProbes event handler
void endopacityenvironmentprobes_event_handler()
{
	Log::message("\Handling EndOpacityEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacityenvironmentprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndOpacityEnvironmentProbes().connect(endopacityenvironmentprobes_event_connections, endopacityenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndOpacityEnvironmentProbes().connect(endopacityenvironmentprobes_event_connections, []() {
		Log::message("\Handling EndOpacityEnvironmentProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endopacityenvironmentprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endopacityenvironmentprobes_event_connection;

// subscribe to the EndOpacityEnvironmentProbes event with a handler function keeping the connection
publisher->getEventEndOpacityEnvironmentProbes().connect(endopacityenvironmentprobes_event_connection, endopacityenvironmentprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endopacityenvironmentprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endopacityenvironmentprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the EndOpacityEnvironmentProbes event via the connection
endopacityenvironmentprobes_event_connection.disconnect();

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

	// A EndOpacityEnvironmentProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndOpacityEnvironmentProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndOpacityEnvironmentProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endopacityenvironmentprobes_handler_id;

// subscribe to the EndOpacityEnvironmentProbes event with a lambda handler function and keeping connection ID
endopacityenvironmentprobes_handler_id = publisher->getEventEndOpacityEnvironmentProbes().connect(e_connections, []() {
		Log::message("\Handling EndOpacityEnvironmentProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndOpacityEnvironmentProbes().disconnect(endopacityenvironmentprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndOpacityEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndOpacityEnvironmentProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndOpacityEnvironmentProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginOpacityPlanarProbes () const

event triggered before the opacity planar probes rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginOpacityPlanarProbes event handler
void beginopacityplanarprobes_event_handler()
{
	Log::message("\Handling BeginOpacityPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacityplanarprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginOpacityPlanarProbes().connect(beginopacityplanarprobes_event_connections, beginopacityplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginOpacityPlanarProbes().connect(beginopacityplanarprobes_event_connections, []() {
		Log::message("\Handling BeginOpacityPlanarProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginopacityplanarprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginopacityplanarprobes_event_connection;

// subscribe to the BeginOpacityPlanarProbes event with a handler function keeping the connection
publisher->getEventBeginOpacityPlanarProbes().connect(beginopacityplanarprobes_event_connection, beginopacityplanarprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginopacityplanarprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginopacityplanarprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginOpacityPlanarProbes event via the connection
beginopacityplanarprobes_event_connection.disconnect();

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

	// A BeginOpacityPlanarProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginOpacityPlanarProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginOpacityPlanarProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginopacityplanarprobes_handler_id;

// subscribe to the BeginOpacityPlanarProbes event with a lambda handler function and keeping connection ID
beginopacityplanarprobes_handler_id = publisher->getEventBeginOpacityPlanarProbes().connect(e_connections, []() {
		Log::message("\Handling BeginOpacityPlanarProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginOpacityPlanarProbes().disconnect(beginopacityplanarprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginOpacityPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginOpacityPlanarProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginOpacityPlanarProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndOpacityPlanarProbes () const

event triggered after the opacity planar probes rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndOpacityPlanarProbes event handler
void endopacityplanarprobes_event_handler()
{
	Log::message("\Handling EndOpacityPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacityplanarprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndOpacityPlanarProbes().connect(endopacityplanarprobes_event_connections, endopacityplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndOpacityPlanarProbes().connect(endopacityplanarprobes_event_connections, []() {
		Log::message("\Handling EndOpacityPlanarProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endopacityplanarprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endopacityplanarprobes_event_connection;

// subscribe to the EndOpacityPlanarProbes event with a handler function keeping the connection
publisher->getEventEndOpacityPlanarProbes().connect(endopacityplanarprobes_event_connection, endopacityplanarprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endopacityplanarprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endopacityplanarprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the EndOpacityPlanarProbes event via the connection
endopacityplanarprobes_event_connection.disconnect();

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

	// A EndOpacityPlanarProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndOpacityPlanarProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndOpacityPlanarProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endopacityplanarprobes_handler_id;

// subscribe to the EndOpacityPlanarProbes event with a lambda handler function and keeping connection ID
endopacityplanarprobes_handler_id = publisher->getEventEndOpacityPlanarProbes().connect(e_connections, []() {
		Log::message("\Handling EndOpacityPlanarProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndOpacityPlanarProbes().disconnect(endopacityplanarprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndOpacityPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndOpacityPlanarProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndOpacityPlanarProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginRefractionBuffer () const

event triggered before filling the refraction buffer. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginRefractionBuffer event handler
void beginrefractionbuffer_event_handler()
{
	Log::message("\Handling BeginRefractionBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginrefractionbuffer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginRefractionBuffer().connect(beginrefractionbuffer_event_connections, beginrefractionbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginRefractionBuffer().connect(beginrefractionbuffer_event_connections, []() {
		Log::message("\Handling BeginRefractionBuffer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginrefractionbuffer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginrefractionbuffer_event_connection;

// subscribe to the BeginRefractionBuffer event with a handler function keeping the connection
publisher->getEventBeginRefractionBuffer().connect(beginrefractionbuffer_event_connection, beginrefractionbuffer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginrefractionbuffer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginrefractionbuffer_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginRefractionBuffer event via the connection
beginrefractionbuffer_event_connection.disconnect();

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

	// A BeginRefractionBuffer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginRefractionBuffer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginRefractionBuffer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginrefractionbuffer_handler_id;

// subscribe to the BeginRefractionBuffer event with a lambda handler function and keeping connection ID
beginrefractionbuffer_handler_id = publisher->getEventBeginRefractionBuffer().connect(e_connections, []() {
		Log::message("\Handling BeginRefractionBuffer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginRefractionBuffer().disconnect(beginrefractionbuffer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginRefractionBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginRefractionBuffer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginRefractionBuffer().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndRefractionBuffer () const

event triggered after filling the refraction buffer. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndRefractionBuffer event handler
void endrefractionbuffer_event_handler()
{
	Log::message("\Handling EndRefractionBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endrefractionbuffer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndRefractionBuffer().connect(endrefractionbuffer_event_connections, endrefractionbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndRefractionBuffer().connect(endrefractionbuffer_event_connections, []() {
		Log::message("\Handling EndRefractionBuffer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endrefractionbuffer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endrefractionbuffer_event_connection;

// subscribe to the EndRefractionBuffer event with a handler function keeping the connection
publisher->getEventEndRefractionBuffer().connect(endrefractionbuffer_event_connection, endrefractionbuffer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endrefractionbuffer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endrefractionbuffer_event_connection.setEnabled(true);

// ...

// remove subscription to the EndRefractionBuffer event via the connection
endrefractionbuffer_event_connection.disconnect();

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

	// A EndRefractionBuffer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndRefractionBuffer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndRefractionBuffer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endrefractionbuffer_handler_id;

// subscribe to the EndRefractionBuffer event with a lambda handler function and keeping connection ID
endrefractionbuffer_handler_id = publisher->getEventEndRefractionBuffer().connect(e_connections, []() {
		Log::message("\Handling EndRefractionBuffer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndRefractionBuffer().disconnect(endrefractionbuffer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndRefractionBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndRefractionBuffer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndRefractionBuffer().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginTransparentBlurBuffer () const

event triggered before filling the transparent blur buffer. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginTransparentBlurBuffer event handler
void begintransparentblurbuffer_event_handler()
{
	Log::message("\Handling BeginTransparentBlurBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begintransparentblurbuffer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginTransparentBlurBuffer().connect(begintransparentblurbuffer_event_connections, begintransparentblurbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginTransparentBlurBuffer().connect(begintransparentblurbuffer_event_connections, []() {
		Log::message("\Handling BeginTransparentBlurBuffer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begintransparentblurbuffer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begintransparentblurbuffer_event_connection;

// subscribe to the BeginTransparentBlurBuffer event with a handler function keeping the connection
publisher->getEventBeginTransparentBlurBuffer().connect(begintransparentblurbuffer_event_connection, begintransparentblurbuffer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begintransparentblurbuffer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begintransparentblurbuffer_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginTransparentBlurBuffer event via the connection
begintransparentblurbuffer_event_connection.disconnect();

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

	// A BeginTransparentBlurBuffer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginTransparentBlurBuffer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginTransparentBlurBuffer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begintransparentblurbuffer_handler_id;

// subscribe to the BeginTransparentBlurBuffer event with a lambda handler function and keeping connection ID
begintransparentblurbuffer_handler_id = publisher->getEventBeginTransparentBlurBuffer().connect(e_connections, []() {
		Log::message("\Handling BeginTransparentBlurBuffer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginTransparentBlurBuffer().disconnect(begintransparentblurbuffer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginTransparentBlurBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginTransparentBlurBuffer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginTransparentBlurBuffer().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndTransparentBlurBuffer () const

event triggered after filling the transparent blur buffer. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndTransparentBlurBuffer event handler
void endtransparentblurbuffer_event_handler()
{
	Log::message("\Handling EndTransparentBlurBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endtransparentblurbuffer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndTransparentBlurBuffer().connect(endtransparentblurbuffer_event_connections, endtransparentblurbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndTransparentBlurBuffer().connect(endtransparentblurbuffer_event_connections, []() {
		Log::message("\Handling EndTransparentBlurBuffer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endtransparentblurbuffer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endtransparentblurbuffer_event_connection;

// subscribe to the EndTransparentBlurBuffer event with a handler function keeping the connection
publisher->getEventEndTransparentBlurBuffer().connect(endtransparentblurbuffer_event_connection, endtransparentblurbuffer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endtransparentblurbuffer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endtransparentblurbuffer_event_connection.setEnabled(true);

// ...

// remove subscription to the EndTransparentBlurBuffer event via the connection
endtransparentblurbuffer_event_connection.disconnect();

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

	// A EndTransparentBlurBuffer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndTransparentBlurBuffer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndTransparentBlurBuffer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endtransparentblurbuffer_handler_id;

// subscribe to the EndTransparentBlurBuffer event with a lambda handler function and keeping connection ID
endtransparentblurbuffer_handler_id = publisher->getEventEndTransparentBlurBuffer().connect(e_connections, []() {
		Log::message("\Handling EndTransparentBlurBuffer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndTransparentBlurBuffer().disconnect(endtransparentblurbuffer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndTransparentBlurBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndTransparentBlurBuffer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndTransparentBlurBuffer().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginSSSS () const

event triggered before the Screen-Space Shadow Shafts rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSSSS event handler
void beginssss_event_handler()
{
	Log::message("\Handling BeginSSSS event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssss_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginSSSS().connect(beginssss_event_connections, beginssss_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginSSSS().connect(beginssss_event_connections, []() {
		Log::message("\Handling BeginSSSS event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginssss_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginssss_event_connection;

// subscribe to the BeginSSSS event with a handler function keeping the connection
publisher->getEventBeginSSSS().connect(beginssss_event_connection, beginssss_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginssss_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginssss_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSSSS event via the connection
beginssss_event_connection.disconnect();

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

	// A BeginSSSS event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSSSS event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginSSSS().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginssss_handler_id;

// subscribe to the BeginSSSS event with a lambda handler function and keeping connection ID
beginssss_handler_id = publisher->getEventBeginSSSS().connect(e_connections, []() {
		Log::message("\Handling BeginSSSS event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginSSSS().disconnect(beginssss_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSSSS events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginSSSS().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginSSSS().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndSSSS () const

event triggered after the Screen-Space Shadow Shafts rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSSSS event handler
void endssss_event_handler()
{
	Log::message("\Handling EndSSSS event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssss_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndSSSS().connect(endssss_event_connections, endssss_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndSSSS().connect(endssss_event_connections, []() {
		Log::message("\Handling EndSSSS event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endssss_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endssss_event_connection;

// subscribe to the EndSSSS event with a handler function keeping the connection
publisher->getEventEndSSSS().connect(endssss_event_connection, endssss_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endssss_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endssss_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSSSS event via the connection
endssss_event_connection.disconnect();

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

	// A EndSSSS event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSSSS event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndSSSS().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endssss_handler_id;

// subscribe to the EndSSSS event with a lambda handler function and keeping connection ID
endssss_handler_id = publisher->getEventEndSSSS().connect(e_connections, []() {
		Log::message("\Handling EndSSSS event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndSSSS().disconnect(endssss_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSSSS events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndSSSS().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndSSSS().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginSSR () const

event triggered before the SSR rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSSR event handler
void beginssr_event_handler()
{
	Log::message("\Handling BeginSSR event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssr_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginSSR().connect(beginssr_event_connections, beginssr_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginSSR().connect(beginssr_event_connections, []() {
		Log::message("\Handling BeginSSR event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginssr_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginssr_event_connection;

// subscribe to the BeginSSR event with a handler function keeping the connection
publisher->getEventBeginSSR().connect(beginssr_event_connection, beginssr_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginssr_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginssr_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSSR event via the connection
beginssr_event_connection.disconnect();

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

	// A BeginSSR event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSSR event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginSSR().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginssr_handler_id;

// subscribe to the BeginSSR event with a lambda handler function and keeping connection ID
beginssr_handler_id = publisher->getEventBeginSSR().connect(e_connections, []() {
		Log::message("\Handling BeginSSR event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginSSR().disconnect(beginssr_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSSR events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginSSR().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginSSR().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndSSR () const

event triggered after the SSR rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSSR event handler
void endssr_event_handler()
{
	Log::message("\Handling EndSSR event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssr_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndSSR().connect(endssr_event_connections, endssr_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndSSR().connect(endssr_event_connections, []() {
		Log::message("\Handling EndSSR event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endssr_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endssr_event_connection;

// subscribe to the EndSSR event with a handler function keeping the connection
publisher->getEventEndSSR().connect(endssr_event_connection, endssr_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endssr_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endssr_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSSR event via the connection
endssr_event_connection.disconnect();

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

	// A EndSSR event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSSR event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndSSR().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endssr_handler_id;

// subscribe to the EndSSR event with a lambda handler function and keeping connection ID
endssr_handler_id = publisher->getEventEndSSR().connect(e_connections, []() {
		Log::message("\Handling EndSSR event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndSSR().disconnect(endssr_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSSR events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndSSR().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndSSR().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginSSAO () const

event triggered before the SSAO rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSSAO event handler
void beginssao_event_handler()
{
	Log::message("\Handling BeginSSAO event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssao_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginSSAO().connect(beginssao_event_connections, beginssao_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginSSAO().connect(beginssao_event_connections, []() {
		Log::message("\Handling BeginSSAO event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginssao_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginssao_event_connection;

// subscribe to the BeginSSAO event with a handler function keeping the connection
publisher->getEventBeginSSAO().connect(beginssao_event_connection, beginssao_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginssao_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginssao_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSSAO event via the connection
beginssao_event_connection.disconnect();

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

	// A BeginSSAO event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSSAO event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginSSAO().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginssao_handler_id;

// subscribe to the BeginSSAO event with a lambda handler function and keeping connection ID
beginssao_handler_id = publisher->getEventBeginSSAO().connect(e_connections, []() {
		Log::message("\Handling BeginSSAO event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginSSAO().disconnect(beginssao_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSSAO events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginSSAO().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginSSAO().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndSSAO () const

event triggered after the SSAO rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSSAO event handler
void endssao_event_handler()
{
	Log::message("\Handling EndSSAO event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssao_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndSSAO().connect(endssao_event_connections, endssao_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndSSAO().connect(endssao_event_connections, []() {
		Log::message("\Handling EndSSAO event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endssao_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endssao_event_connection;

// subscribe to the EndSSAO event with a handler function keeping the connection
publisher->getEventEndSSAO().connect(endssao_event_connection, endssao_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endssao_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endssao_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSSAO event via the connection
endssao_event_connection.disconnect();

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

	// A EndSSAO event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSSAO event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndSSAO().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endssao_handler_id;

// subscribe to the EndSSAO event with a lambda handler function and keeping connection ID
endssao_handler_id = publisher->getEventEndSSAO().connect(e_connections, []() {
		Log::message("\Handling EndSSAO event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndSSAO().disconnect(endssao_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSSAO events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndSSAO().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndSSAO().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginSSGI () const

event triggered before the SSGI rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSSGI event handler
void beginssgi_event_handler()
{
	Log::message("\Handling BeginSSGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssgi_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginSSGI().connect(beginssgi_event_connections, beginssgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginSSGI().connect(beginssgi_event_connections, []() {
		Log::message("\Handling BeginSSGI event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginssgi_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginssgi_event_connection;

// subscribe to the BeginSSGI event with a handler function keeping the connection
publisher->getEventBeginSSGI().connect(beginssgi_event_connection, beginssgi_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginssgi_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginssgi_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSSGI event via the connection
beginssgi_event_connection.disconnect();

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

	// A BeginSSGI event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSSGI event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginSSGI().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginssgi_handler_id;

// subscribe to the BeginSSGI event with a lambda handler function and keeping connection ID
beginssgi_handler_id = publisher->getEventBeginSSGI().connect(e_connections, []() {
		Log::message("\Handling BeginSSGI event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginSSGI().disconnect(beginssgi_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSSGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginSSGI().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginSSGI().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndSSGI () const

event triggered after the SSGI rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSSGI event handler
void endssgi_event_handler()
{
	Log::message("\Handling EndSSGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssgi_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndSSGI().connect(endssgi_event_connections, endssgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndSSGI().connect(endssgi_event_connections, []() {
		Log::message("\Handling EndSSGI event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endssgi_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endssgi_event_connection;

// subscribe to the EndSSGI event with a handler function keeping the connection
publisher->getEventEndSSGI().connect(endssgi_event_connection, endssgi_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endssgi_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endssgi_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSSGI event via the connection
endssgi_event_connection.disconnect();

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

	// A EndSSGI event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSSGI event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndSSGI().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endssgi_handler_id;

// subscribe to the EndSSGI event with a lambda handler function and keeping connection ID
endssgi_handler_id = publisher->getEventEndSSGI().connect(e_connections, []() {
		Log::message("\Handling EndSSGI event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndSSGI().disconnect(endssgi_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSSGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndSSGI().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndSSGI().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginSky () const

event triggered before the sky rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSky event handler
void beginsky_event_handler()
{
	Log::message("\Handling BeginSky event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsky_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginSky().connect(beginsky_event_connections, beginsky_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginSky().connect(beginsky_event_connections, []() {
		Log::message("\Handling BeginSky event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginsky_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginsky_event_connection;

// subscribe to the BeginSky event with a handler function keeping the connection
publisher->getEventBeginSky().connect(beginsky_event_connection, beginsky_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginsky_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginsky_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSky event via the connection
beginsky_event_connection.disconnect();

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

	// A BeginSky event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSky event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginSky().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginsky_handler_id;

// subscribe to the BeginSky event with a lambda handler function and keeping connection ID
beginsky_handler_id = publisher->getEventBeginSky().connect(e_connections, []() {
		Log::message("\Handling BeginSky event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginSky().disconnect(beginsky_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSky events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginSky().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginSky().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndSky () const

event triggered after the sky rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSky event handler
void endsky_event_handler()
{
	Log::message("\Handling EndSky event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsky_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndSky().connect(endsky_event_connections, endsky_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndSky().connect(endsky_event_connections, []() {
		Log::message("\Handling EndSky event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endsky_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endsky_event_connection;

// subscribe to the EndSky event with a handler function keeping the connection
publisher->getEventEndSky().connect(endsky_event_connection, endsky_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endsky_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endsky_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSky event via the connection
endsky_event_connection.disconnect();

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

	// A EndSky event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSky event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndSky().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endsky_handler_id;

// subscribe to the EndSky event with a lambda handler function and keeping connection ID
endsky_handler_id = publisher->getEventEndSky().connect(e_connections, []() {
		Log::message("\Handling EndSky event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndSky().disconnect(endsky_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSky events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndSky().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndSky().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginCompositeDeferred () const

event triggered before the clouds deferred composite stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginCompositeDeferred event handler
void begincompositedeferred_event_handler()
{
	Log::message("\Handling BeginCompositeDeferred event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincompositedeferred_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginCompositeDeferred().connect(begincompositedeferred_event_connections, begincompositedeferred_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginCompositeDeferred().connect(begincompositedeferred_event_connections, []() {
		Log::message("\Handling BeginCompositeDeferred event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begincompositedeferred_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begincompositedeferred_event_connection;

// subscribe to the BeginCompositeDeferred event with a handler function keeping the connection
publisher->getEventBeginCompositeDeferred().connect(begincompositedeferred_event_connection, begincompositedeferred_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begincompositedeferred_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begincompositedeferred_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginCompositeDeferred event via the connection
begincompositedeferred_event_connection.disconnect();

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

	// A BeginCompositeDeferred event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginCompositeDeferred event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginCompositeDeferred().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begincompositedeferred_handler_id;

// subscribe to the BeginCompositeDeferred event with a lambda handler function and keeping connection ID
begincompositedeferred_handler_id = publisher->getEventBeginCompositeDeferred().connect(e_connections, []() {
		Log::message("\Handling BeginCompositeDeferred event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginCompositeDeferred().disconnect(begincompositedeferred_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginCompositeDeferred events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginCompositeDeferred().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginCompositeDeferred().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndCompositeDeferred () const

event triggered after the clouds deferred composite stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndCompositeDeferred event handler
void endcompositedeferred_event_handler()
{
	Log::message("\Handling EndCompositeDeferred event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcompositedeferred_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndCompositeDeferred().connect(endcompositedeferred_event_connections, endcompositedeferred_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndCompositeDeferred().connect(endcompositedeferred_event_connections, []() {
		Log::message("\Handling EndCompositeDeferred event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endcompositedeferred_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endcompositedeferred_event_connection;

// subscribe to the EndCompositeDeferred event with a handler function keeping the connection
publisher->getEventEndCompositeDeferred().connect(endcompositedeferred_event_connection, endcompositedeferred_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endcompositedeferred_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endcompositedeferred_event_connection.setEnabled(true);

// ...

// remove subscription to the EndCompositeDeferred event via the connection
endcompositedeferred_event_connection.disconnect();

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

	// A EndCompositeDeferred event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndCompositeDeferred event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndCompositeDeferred().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endcompositedeferred_handler_id;

// subscribe to the EndCompositeDeferred event with a lambda handler function and keeping connection ID
endcompositedeferred_handler_id = publisher->getEventEndCompositeDeferred().connect(e_connections, []() {
		Log::message("\Handling EndCompositeDeferred event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndCompositeDeferred().disconnect(endcompositedeferred_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndCompositeDeferred events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndCompositeDeferred().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndCompositeDeferred().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginTransparent () const

event triggered before the transparent objects rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginTransparent event handler
void begintransparent_event_handler()
{
	Log::message("\Handling BeginTransparent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begintransparent_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginTransparent().connect(begintransparent_event_connections, begintransparent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginTransparent().connect(begintransparent_event_connections, []() {
		Log::message("\Handling BeginTransparent event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begintransparent_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begintransparent_event_connection;

// subscribe to the BeginTransparent event with a handler function keeping the connection
publisher->getEventBeginTransparent().connect(begintransparent_event_connection, begintransparent_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begintransparent_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begintransparent_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginTransparent event via the connection
begintransparent_event_connection.disconnect();

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

	// A BeginTransparent event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginTransparent event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginTransparent().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begintransparent_handler_id;

// subscribe to the BeginTransparent event with a lambda handler function and keeping connection ID
begintransparent_handler_id = publisher->getEventBeginTransparent().connect(e_connections, []() {
		Log::message("\Handling BeginTransparent event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginTransparent().disconnect(begintransparent_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginTransparent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginTransparent().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginTransparent().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginClouds () const

event triggered before the clouds rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginClouds event handler
void beginclouds_event_handler()
{
	Log::message("\Handling BeginClouds event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginclouds_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginClouds().connect(beginclouds_event_connections, beginclouds_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginClouds().connect(beginclouds_event_connections, []() {
		Log::message("\Handling BeginClouds event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginclouds_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginclouds_event_connection;

// subscribe to the BeginClouds event with a handler function keeping the connection
publisher->getEventBeginClouds().connect(beginclouds_event_connection, beginclouds_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginclouds_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginclouds_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginClouds event via the connection
beginclouds_event_connection.disconnect();

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

	// A BeginClouds event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginClouds event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginClouds().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginclouds_handler_id;

// subscribe to the BeginClouds event with a lambda handler function and keeping connection ID
beginclouds_handler_id = publisher->getEventBeginClouds().connect(e_connections, []() {
		Log::message("\Handling BeginClouds event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginClouds().disconnect(beginclouds_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginClouds events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginClouds().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginClouds().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndClouds () const

event triggered after the clouds rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndClouds event handler
void endclouds_event_handler()
{
	Log::message("\Handling EndClouds event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endclouds_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndClouds().connect(endclouds_event_connections, endclouds_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndClouds().connect(endclouds_event_connections, []() {
		Log::message("\Handling EndClouds event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endclouds_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endclouds_event_connection;

// subscribe to the EndClouds event with a handler function keeping the connection
publisher->getEventEndClouds().connect(endclouds_event_connection, endclouds_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endclouds_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endclouds_event_connection.setEnabled(true);

// ...

// remove subscription to the EndClouds event via the connection
endclouds_event_connection.disconnect();

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

	// A EndClouds event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndClouds event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndClouds().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endclouds_handler_id;

// subscribe to the EndClouds event with a lambda handler function and keeping connection ID
endclouds_handler_id = publisher->getEventEndClouds().connect(e_connections, []() {
		Log::message("\Handling EndClouds event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndClouds().disconnect(endclouds_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndClouds events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndClouds().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndClouds().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginWater () const

event triggered before the water rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWater event handler
void beginwater_event_handler()
{
	Log::message("\Handling BeginWater event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwater_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginWater().connect(beginwater_event_connections, beginwater_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginWater().connect(beginwater_event_connections, []() {
		Log::message("\Handling BeginWater event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginwater_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginwater_event_connection;

// subscribe to the BeginWater event with a handler function keeping the connection
publisher->getEventBeginWater().connect(beginwater_event_connection, beginwater_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginwater_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginwater_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWater event via the connection
beginwater_event_connection.disconnect();

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

	// A BeginWater event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWater event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginWater().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginwater_handler_id;

// subscribe to the BeginWater event with a lambda handler function and keeping connection ID
beginwater_handler_id = publisher->getEventBeginWater().connect(e_connections, []() {
		Log::message("\Handling BeginWater event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginWater().disconnect(beginwater_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWater events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginWater().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginWater().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginWaterGBuffer () const

event triggered before the Water G-Buffer rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWaterGBuffer event handler
void beginwatergbuffer_event_handler()
{
	Log::message("\Handling BeginWaterGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwatergbuffer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginWaterGBuffer().connect(beginwatergbuffer_event_connections, beginwatergbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginWaterGBuffer().connect(beginwatergbuffer_event_connections, []() {
		Log::message("\Handling BeginWaterGBuffer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginwatergbuffer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginwatergbuffer_event_connection;

// subscribe to the BeginWaterGBuffer event with a handler function keeping the connection
publisher->getEventBeginWaterGBuffer().connect(beginwatergbuffer_event_connection, beginwatergbuffer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginwatergbuffer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginwatergbuffer_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWaterGBuffer event via the connection
beginwatergbuffer_event_connection.disconnect();

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

	// A BeginWaterGBuffer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWaterGBuffer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginWaterGBuffer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginwatergbuffer_handler_id;

// subscribe to the BeginWaterGBuffer event with a lambda handler function and keeping connection ID
beginwatergbuffer_handler_id = publisher->getEventBeginWaterGBuffer().connect(e_connections, []() {
		Log::message("\Handling BeginWaterGBuffer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginWaterGBuffer().disconnect(beginwatergbuffer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWaterGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginWaterGBuffer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginWaterGBuffer().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndWaterGBuffer () const

event triggered after the Water G-Buffer rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWaterGBuffer event handler
void endwatergbuffer_event_handler()
{
	Log::message("\Handling EndWaterGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwatergbuffer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndWaterGBuffer().connect(endwatergbuffer_event_connections, endwatergbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndWaterGBuffer().connect(endwatergbuffer_event_connections, []() {
		Log::message("\Handling EndWaterGBuffer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endwatergbuffer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endwatergbuffer_event_connection;

// subscribe to the EndWaterGBuffer event with a handler function keeping the connection
publisher->getEventEndWaterGBuffer().connect(endwatergbuffer_event_connection, endwatergbuffer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endwatergbuffer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endwatergbuffer_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWaterGBuffer event via the connection
endwatergbuffer_event_connection.disconnect();

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

	// A EndWaterGBuffer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWaterGBuffer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndWaterGBuffer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endwatergbuffer_handler_id;

// subscribe to the EndWaterGBuffer event with a lambda handler function and keeping connection ID
endwatergbuffer_handler_id = publisher->getEventEndWaterGBuffer().connect(e_connections, []() {
		Log::message("\Handling EndWaterGBuffer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndWaterGBuffer().disconnect(endwatergbuffer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWaterGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndWaterGBuffer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndWaterGBuffer().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginWaterDecals () const

event triggered before the water decals rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWaterDecals event handler
void beginwaterdecals_event_handler()
{
	Log::message("\Handling BeginWaterDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterdecals_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginWaterDecals().connect(beginwaterdecals_event_connections, beginwaterdecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginWaterDecals().connect(beginwaterdecals_event_connections, []() {
		Log::message("\Handling BeginWaterDecals event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginwaterdecals_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginwaterdecals_event_connection;

// subscribe to the BeginWaterDecals event with a handler function keeping the connection
publisher->getEventBeginWaterDecals().connect(beginwaterdecals_event_connection, beginwaterdecals_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginwaterdecals_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginwaterdecals_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWaterDecals event via the connection
beginwaterdecals_event_connection.disconnect();

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

	// A BeginWaterDecals event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWaterDecals event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginWaterDecals().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginwaterdecals_handler_id;

// subscribe to the BeginWaterDecals event with a lambda handler function and keeping connection ID
beginwaterdecals_handler_id = publisher->getEventBeginWaterDecals().connect(e_connections, []() {
		Log::message("\Handling BeginWaterDecals event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginWaterDecals().disconnect(beginwaterdecals_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWaterDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginWaterDecals().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginWaterDecals().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndWaterDecals () const

event triggered after the water decals rendering stage. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWaterDecals event handler
void endwaterdecals_event_handler()
{
	Log::message("\Handling EndWaterDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterdecals_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndWaterDecals().connect(endwaterdecals_event_connections, endwaterdecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndWaterDecals().connect(endwaterdecals_event_connections, []() {
		Log::message("\Handling EndWaterDecals event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endwaterdecals_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endwaterdecals_event_connection;

// subscribe to the EndWaterDecals event with a handler function keeping the connection
publisher->getEventEndWaterDecals().connect(endwaterdecals_event_connection, endwaterdecals_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endwaterdecals_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endwaterdecals_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWaterDecals event via the connection
endwaterdecals_event_connection.disconnect();

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

	// A EndWaterDecals event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWaterDecals event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndWaterDecals().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endwaterdecals_handler_id;

// subscribe to the EndWaterDecals event with a lambda handler function and keeping connection ID
endwaterdecals_handler_id = publisher->getEventEndWaterDecals().connect(e_connections, []() {
		Log::message("\Handling EndWaterDecals event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndWaterDecals().disconnect(endwaterdecals_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWaterDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndWaterDecals().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndWaterDecals().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginWaterLights () const

event triggered before the water lights rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWaterLights event handler
void beginwaterlights_event_handler()
{
	Log::message("\Handling BeginWaterLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterlights_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginWaterLights().connect(beginwaterlights_event_connections, beginwaterlights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginWaterLights().connect(beginwaterlights_event_connections, []() {
		Log::message("\Handling BeginWaterLights event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginwaterlights_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginwaterlights_event_connection;

// subscribe to the BeginWaterLights event with a handler function keeping the connection
publisher->getEventBeginWaterLights().connect(beginwaterlights_event_connection, beginwaterlights_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginwaterlights_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginwaterlights_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWaterLights event via the connection
beginwaterlights_event_connection.disconnect();

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

	// A BeginWaterLights event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWaterLights event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginWaterLights().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginwaterlights_handler_id;

// subscribe to the BeginWaterLights event with a lambda handler function and keeping connection ID
beginwaterlights_handler_id = publisher->getEventBeginWaterLights().connect(e_connections, []() {
		Log::message("\Handling BeginWaterLights event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginWaterLights().disconnect(beginwaterlights_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWaterLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginWaterLights().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginWaterLights().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndWaterLights () const

event triggered after the water lights rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWaterLights event handler
void endwaterlights_event_handler()
{
	Log::message("\Handling EndWaterLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterlights_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndWaterLights().connect(endwaterlights_event_connections, endwaterlights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndWaterLights().connect(endwaterlights_event_connections, []() {
		Log::message("\Handling EndWaterLights event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endwaterlights_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endwaterlights_event_connection;

// subscribe to the EndWaterLights event with a handler function keeping the connection
publisher->getEventEndWaterLights().connect(endwaterlights_event_connection, endwaterlights_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endwaterlights_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endwaterlights_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWaterLights event via the connection
endwaterlights_event_connection.disconnect();

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

	// A EndWaterLights event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWaterLights event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndWaterLights().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endwaterlights_handler_id;

// subscribe to the EndWaterLights event with a lambda handler function and keeping connection ID
endwaterlights_handler_id = publisher->getEventEndWaterLights().connect(e_connections, []() {
		Log::message("\Handling EndWaterLights event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndWaterLights().disconnect(endwaterlights_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWaterLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndWaterLights().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndWaterLights().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginWaterVoxelProbes () const

event triggered before the water voxel probes rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWaterVoxelProbes event handler
void beginwatervoxelprobes_event_handler()
{
	Log::message("\Handling BeginWaterVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwatervoxelprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginWaterVoxelProbes().connect(beginwatervoxelprobes_event_connections, beginwatervoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginWaterVoxelProbes().connect(beginwatervoxelprobes_event_connections, []() {
		Log::message("\Handling BeginWaterVoxelProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginwatervoxelprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginwatervoxelprobes_event_connection;

// subscribe to the BeginWaterVoxelProbes event with a handler function keeping the connection
publisher->getEventBeginWaterVoxelProbes().connect(beginwatervoxelprobes_event_connection, beginwatervoxelprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginwatervoxelprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginwatervoxelprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWaterVoxelProbes event via the connection
beginwatervoxelprobes_event_connection.disconnect();

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

	// A BeginWaterVoxelProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWaterVoxelProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginWaterVoxelProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginwatervoxelprobes_handler_id;

// subscribe to the BeginWaterVoxelProbes event with a lambda handler function and keeping connection ID
beginwatervoxelprobes_handler_id = publisher->getEventBeginWaterVoxelProbes().connect(e_connections, []() {
		Log::message("\Handling BeginWaterVoxelProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginWaterVoxelProbes().disconnect(beginwatervoxelprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWaterVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginWaterVoxelProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginWaterVoxelProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndWaterVoxelProbes () const

event triggered after the water voxel probes rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWaterVoxelProbes event handler
void endwatervoxelprobes_event_handler()
{
	Log::message("\Handling EndWaterVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwatervoxelprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndWaterVoxelProbes().connect(endwatervoxelprobes_event_connections, endwatervoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndWaterVoxelProbes().connect(endwatervoxelprobes_event_connections, []() {
		Log::message("\Handling EndWaterVoxelProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endwatervoxelprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endwatervoxelprobes_event_connection;

// subscribe to the EndWaterVoxelProbes event with a handler function keeping the connection
publisher->getEventEndWaterVoxelProbes().connect(endwatervoxelprobes_event_connection, endwatervoxelprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endwatervoxelprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endwatervoxelprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWaterVoxelProbes event via the connection
endwatervoxelprobes_event_connection.disconnect();

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

	// A EndWaterVoxelProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWaterVoxelProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndWaterVoxelProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endwatervoxelprobes_handler_id;

// subscribe to the EndWaterVoxelProbes event with a lambda handler function and keeping connection ID
endwatervoxelprobes_handler_id = publisher->getEventEndWaterVoxelProbes().connect(e_connections, []() {
		Log::message("\Handling EndWaterVoxelProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndWaterVoxelProbes().disconnect(endwatervoxelprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWaterVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndWaterVoxelProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndWaterVoxelProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginWaterEnvironmentProbes () const

event triggered before the water environment probes rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWaterEnvironmentProbes event handler
void beginwaterenvironmentprobes_event_handler()
{
	Log::message("\Handling BeginWaterEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterenvironmentprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginWaterEnvironmentProbes().connect(beginwaterenvironmentprobes_event_connections, beginwaterenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginWaterEnvironmentProbes().connect(beginwaterenvironmentprobes_event_connections, []() {
		Log::message("\Handling BeginWaterEnvironmentProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginwaterenvironmentprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginwaterenvironmentprobes_event_connection;

// subscribe to the BeginWaterEnvironmentProbes event with a handler function keeping the connection
publisher->getEventBeginWaterEnvironmentProbes().connect(beginwaterenvironmentprobes_event_connection, beginwaterenvironmentprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginwaterenvironmentprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginwaterenvironmentprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWaterEnvironmentProbes event via the connection
beginwaterenvironmentprobes_event_connection.disconnect();

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

	// A BeginWaterEnvironmentProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWaterEnvironmentProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginWaterEnvironmentProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginwaterenvironmentprobes_handler_id;

// subscribe to the BeginWaterEnvironmentProbes event with a lambda handler function and keeping connection ID
beginwaterenvironmentprobes_handler_id = publisher->getEventBeginWaterEnvironmentProbes().connect(e_connections, []() {
		Log::message("\Handling BeginWaterEnvironmentProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginWaterEnvironmentProbes().disconnect(beginwaterenvironmentprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWaterEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginWaterEnvironmentProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginWaterEnvironmentProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndWaterEnvironmentProbes () const

event triggered after the water environment probes rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWaterEnvironmentProbes event handler
void endwaterenvironmentprobes_event_handler()
{
	Log::message("\Handling EndWaterEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterenvironmentprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndWaterEnvironmentProbes().connect(endwaterenvironmentprobes_event_connections, endwaterenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndWaterEnvironmentProbes().connect(endwaterenvironmentprobes_event_connections, []() {
		Log::message("\Handling EndWaterEnvironmentProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endwaterenvironmentprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endwaterenvironmentprobes_event_connection;

// subscribe to the EndWaterEnvironmentProbes event with a handler function keeping the connection
publisher->getEventEndWaterEnvironmentProbes().connect(endwaterenvironmentprobes_event_connection, endwaterenvironmentprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endwaterenvironmentprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endwaterenvironmentprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWaterEnvironmentProbes event via the connection
endwaterenvironmentprobes_event_connection.disconnect();

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

	// A EndWaterEnvironmentProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWaterEnvironmentProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndWaterEnvironmentProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endwaterenvironmentprobes_handler_id;

// subscribe to the EndWaterEnvironmentProbes event with a lambda handler function and keeping connection ID
endwaterenvironmentprobes_handler_id = publisher->getEventEndWaterEnvironmentProbes().connect(e_connections, []() {
		Log::message("\Handling EndWaterEnvironmentProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndWaterEnvironmentProbes().disconnect(endwaterenvironmentprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWaterEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndWaterEnvironmentProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndWaterEnvironmentProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginWaterPlanarProbes () const

event triggered before the water planar probes rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginWaterPlanarProbes event handler
void beginwaterplanarprobes_event_handler()
{
	Log::message("\Handling BeginWaterPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterplanarprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginWaterPlanarProbes().connect(beginwaterplanarprobes_event_connections, beginwaterplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginWaterPlanarProbes().connect(beginwaterplanarprobes_event_connections, []() {
		Log::message("\Handling BeginWaterPlanarProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginwaterplanarprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginwaterplanarprobes_event_connection;

// subscribe to the BeginWaterPlanarProbes event with a handler function keeping the connection
publisher->getEventBeginWaterPlanarProbes().connect(beginwaterplanarprobes_event_connection, beginwaterplanarprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginwaterplanarprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginwaterplanarprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginWaterPlanarProbes event via the connection
beginwaterplanarprobes_event_connection.disconnect();

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

	// A BeginWaterPlanarProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginWaterPlanarProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginWaterPlanarProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginwaterplanarprobes_handler_id;

// subscribe to the BeginWaterPlanarProbes event with a lambda handler function and keeping connection ID
beginwaterplanarprobes_handler_id = publisher->getEventBeginWaterPlanarProbes().connect(e_connections, []() {
		Log::message("\Handling BeginWaterPlanarProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginWaterPlanarProbes().disconnect(beginwaterplanarprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginWaterPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginWaterPlanarProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginWaterPlanarProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndWaterPlanarProbes () const

event triggered after the water planar probes rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWaterPlanarProbes event handler
void endwaterplanarprobes_event_handler()
{
	Log::message("\Handling EndWaterPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterplanarprobes_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndWaterPlanarProbes().connect(endwaterplanarprobes_event_connections, endwaterplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndWaterPlanarProbes().connect(endwaterplanarprobes_event_connections, []() {
		Log::message("\Handling EndWaterPlanarProbes event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endwaterplanarprobes_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endwaterplanarprobes_event_connection;

// subscribe to the EndWaterPlanarProbes event with a handler function keeping the connection
publisher->getEventEndWaterPlanarProbes().connect(endwaterplanarprobes_event_connection, endwaterplanarprobes_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endwaterplanarprobes_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endwaterplanarprobes_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWaterPlanarProbes event via the connection
endwaterplanarprobes_event_connection.disconnect();

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

	// A EndWaterPlanarProbes event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWaterPlanarProbes event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndWaterPlanarProbes().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endwaterplanarprobes_handler_id;

// subscribe to the EndWaterPlanarProbes event with a lambda handler function and keeping connection ID
endwaterplanarprobes_handler_id = publisher->getEventEndWaterPlanarProbes().connect(e_connections, []() {
		Log::message("\Handling EndWaterPlanarProbes event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndWaterPlanarProbes().disconnect(endwaterplanarprobes_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWaterPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndWaterPlanarProbes().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndWaterPlanarProbes().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndWater () const

event triggered after the water rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndWater event handler
void endwater_event_handler()
{
	Log::message("\Handling EndWater event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwater_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndWater().connect(endwater_event_connections, endwater_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndWater().connect(endwater_event_connections, []() {
		Log::message("\Handling EndWater event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endwater_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endwater_event_connection;

// subscribe to the EndWater event with a handler function keeping the connection
publisher->getEventEndWater().connect(endwater_event_connection, endwater_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endwater_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endwater_event_connection.setEnabled(true);

// ...

// remove subscription to the EndWater event via the connection
endwater_event_connection.disconnect();

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

	// A EndWater event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndWater event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndWater().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endwater_handler_id;

// subscribe to the EndWater event with a lambda handler function and keeping connection ID
endwater_handler_id = publisher->getEventEndWater().connect(e_connections, []() {
		Log::message("\Handling EndWater event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndWater().disconnect(endwater_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndWater events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndWater().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndWater().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndTransparent () const

event triggered after the transparent objects rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndTransparent event handler
void endtransparent_event_handler()
{
	Log::message("\Handling EndTransparent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endtransparent_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndTransparent().connect(endtransparent_event_connections, endtransparent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndTransparent().connect(endtransparent_event_connections, []() {
		Log::message("\Handling EndTransparent event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endtransparent_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endtransparent_event_connection;

// subscribe to the EndTransparent event with a handler function keeping the connection
publisher->getEventEndTransparent().connect(endtransparent_event_connection, endtransparent_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endtransparent_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endtransparent_event_connection.setEnabled(true);

// ...

// remove subscription to the EndTransparent event via the connection
endtransparent_event_connection.disconnect();

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

	// A EndTransparent event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndTransparent event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndTransparent().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endtransparent_handler_id;

// subscribe to the EndTransparent event with a lambda handler function and keeping connection ID
endtransparent_handler_id = publisher->getEventEndTransparent().connect(e_connections, []() {
		Log::message("\Handling EndTransparent event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndTransparent().disconnect(endtransparent_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndTransparent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndTransparent().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndTransparent().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginSrgbCorrection () const

event triggered before the sRGB correction stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginSrgbCorrection event handler
void beginsrgbcorrection_event_handler()
{
	Log::message("\Handling BeginSrgbCorrection event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsrgbcorrection_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginSrgbCorrection().connect(beginsrgbcorrection_event_connections, beginsrgbcorrection_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginSrgbCorrection().connect(beginsrgbcorrection_event_connections, []() {
		Log::message("\Handling BeginSrgbCorrection event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginsrgbcorrection_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginsrgbcorrection_event_connection;

// subscribe to the BeginSrgbCorrection event with a handler function keeping the connection
publisher->getEventBeginSrgbCorrection().connect(beginsrgbcorrection_event_connection, beginsrgbcorrection_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginsrgbcorrection_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginsrgbcorrection_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginSrgbCorrection event via the connection
beginsrgbcorrection_event_connection.disconnect();

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

	// A BeginSrgbCorrection event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginSrgbCorrection event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginSrgbCorrection().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginsrgbcorrection_handler_id;

// subscribe to the BeginSrgbCorrection event with a lambda handler function and keeping connection ID
beginsrgbcorrection_handler_id = publisher->getEventBeginSrgbCorrection().connect(e_connections, []() {
		Log::message("\Handling BeginSrgbCorrection event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginSrgbCorrection().disconnect(beginsrgbcorrection_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginSrgbCorrection events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginSrgbCorrection().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginSrgbCorrection().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndSrgbCorrection () const

event triggered after the sRGB correction stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndSrgbCorrection event handler
void endsrgbcorrection_event_handler()
{
	Log::message("\Handling EndSrgbCorrection event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsrgbcorrection_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndSrgbCorrection().connect(endsrgbcorrection_event_connections, endsrgbcorrection_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndSrgbCorrection().connect(endsrgbcorrection_event_connections, []() {
		Log::message("\Handling EndSrgbCorrection event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endsrgbcorrection_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endsrgbcorrection_event_connection;

// subscribe to the EndSrgbCorrection event with a handler function keeping the connection
publisher->getEventEndSrgbCorrection().connect(endsrgbcorrection_event_connection, endsrgbcorrection_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endsrgbcorrection_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endsrgbcorrection_event_connection.setEnabled(true);

// ...

// remove subscription to the EndSrgbCorrection event via the connection
endsrgbcorrection_event_connection.disconnect();

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

	// A EndSrgbCorrection event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndSrgbCorrection event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndSrgbCorrection().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endsrgbcorrection_handler_id;

// subscribe to the EndSrgbCorrection event with a lambda handler function and keeping connection ID
endsrgbcorrection_handler_id = publisher->getEventEndSrgbCorrection().connect(e_connections, []() {
		Log::message("\Handling EndSrgbCorrection event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndSrgbCorrection().disconnect(endsrgbcorrection_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndSrgbCorrection events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndSrgbCorrection().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndSrgbCorrection().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginAdaptationColorAverage () const

event triggered before the calculation of automatic exposure and white balance correction. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginAdaptationColorAverage event handler
void beginadaptationcoloraverage_event_handler()
{
	Log::message("\Handling BeginAdaptationColorAverage event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginadaptationcoloraverage_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginAdaptationColorAverage().connect(beginadaptationcoloraverage_event_connections, beginadaptationcoloraverage_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginAdaptationColorAverage().connect(beginadaptationcoloraverage_event_connections, []() {
		Log::message("\Handling BeginAdaptationColorAverage event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginadaptationcoloraverage_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginadaptationcoloraverage_event_connection;

// subscribe to the BeginAdaptationColorAverage event with a handler function keeping the connection
publisher->getEventBeginAdaptationColorAverage().connect(beginadaptationcoloraverage_event_connection, beginadaptationcoloraverage_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginadaptationcoloraverage_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginadaptationcoloraverage_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginAdaptationColorAverage event via the connection
beginadaptationcoloraverage_event_connection.disconnect();

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

	// A BeginAdaptationColorAverage event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginAdaptationColorAverage event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginAdaptationColorAverage().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginadaptationcoloraverage_handler_id;

// subscribe to the BeginAdaptationColorAverage event with a lambda handler function and keeping connection ID
beginadaptationcoloraverage_handler_id = publisher->getEventBeginAdaptationColorAverage().connect(e_connections, []() {
		Log::message("\Handling BeginAdaptationColorAverage event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginAdaptationColorAverage().disconnect(beginadaptationcoloraverage_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginAdaptationColorAverage events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginAdaptationColorAverage().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginAdaptationColorAverage().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndAdaptationColorAverage () const

event triggered after the calculation of automatic exposure and white balance correction. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndAdaptationColorAverage event handler
void endadaptationcoloraverage_event_handler()
{
	Log::message("\Handling EndAdaptationColorAverage event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endadaptationcoloraverage_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndAdaptationColorAverage().connect(endadaptationcoloraverage_event_connections, endadaptationcoloraverage_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndAdaptationColorAverage().connect(endadaptationcoloraverage_event_connections, []() {
		Log::message("\Handling EndAdaptationColorAverage event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endadaptationcoloraverage_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endadaptationcoloraverage_event_connection;

// subscribe to the EndAdaptationColorAverage event with a handler function keeping the connection
publisher->getEventEndAdaptationColorAverage().connect(endadaptationcoloraverage_event_connection, endadaptationcoloraverage_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endadaptationcoloraverage_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endadaptationcoloraverage_event_connection.setEnabled(true);

// ...

// remove subscription to the EndAdaptationColorAverage event via the connection
endadaptationcoloraverage_event_connection.disconnect();

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

	// A EndAdaptationColorAverage event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndAdaptationColorAverage event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndAdaptationColorAverage().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endadaptationcoloraverage_handler_id;

// subscribe to the EndAdaptationColorAverage event with a lambda handler function and keeping connection ID
endadaptationcoloraverage_handler_id = publisher->getEventEndAdaptationColorAverage().connect(e_connections, []() {
		Log::message("\Handling EndAdaptationColorAverage event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndAdaptationColorAverage().disconnect(endadaptationcoloraverage_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndAdaptationColorAverage events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndAdaptationColorAverage().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndAdaptationColorAverage().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginAdaptationColor () const

event triggered before the color adaptation rendering stage (automatic exposure and white balance correction). You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginAdaptationColor event handler
void beginadaptationcolor_event_handler()
{
	Log::message("\Handling BeginAdaptationColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginadaptationcolor_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginAdaptationColor().connect(beginadaptationcolor_event_connections, beginadaptationcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginAdaptationColor().connect(beginadaptationcolor_event_connections, []() {
		Log::message("\Handling BeginAdaptationColor event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginadaptationcolor_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginadaptationcolor_event_connection;

// subscribe to the BeginAdaptationColor event with a handler function keeping the connection
publisher->getEventBeginAdaptationColor().connect(beginadaptationcolor_event_connection, beginadaptationcolor_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginadaptationcolor_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginadaptationcolor_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginAdaptationColor event via the connection
beginadaptationcolor_event_connection.disconnect();

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

	// A BeginAdaptationColor event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginAdaptationColor event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginAdaptationColor().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginadaptationcolor_handler_id;

// subscribe to the BeginAdaptationColor event with a lambda handler function and keeping connection ID
beginadaptationcolor_handler_id = publisher->getEventBeginAdaptationColor().connect(e_connections, []() {
		Log::message("\Handling BeginAdaptationColor event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginAdaptationColor().disconnect(beginadaptationcolor_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginAdaptationColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginAdaptationColor().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginAdaptationColor().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndAdaptationColor () const

event triggered after the color adaptation rendering stage (automatic exposure and white balance correction). You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndAdaptationColor event handler
void endadaptationcolor_event_handler()
{
	Log::message("\Handling EndAdaptationColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endadaptationcolor_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndAdaptationColor().connect(endadaptationcolor_event_connections, endadaptationcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndAdaptationColor().connect(endadaptationcolor_event_connections, []() {
		Log::message("\Handling EndAdaptationColor event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endadaptationcolor_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endadaptationcolor_event_connection;

// subscribe to the EndAdaptationColor event with a handler function keeping the connection
publisher->getEventEndAdaptationColor().connect(endadaptationcolor_event_connection, endadaptationcolor_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endadaptationcolor_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endadaptationcolor_event_connection.setEnabled(true);

// ...

// remove subscription to the EndAdaptationColor event via the connection
endadaptationcolor_event_connection.disconnect();

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

	// A EndAdaptationColor event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndAdaptationColor event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndAdaptationColor().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endadaptationcolor_handler_id;

// subscribe to the EndAdaptationColor event with a lambda handler function and keeping connection ID
endadaptationcolor_handler_id = publisher->getEventEndAdaptationColor().connect(e_connections, []() {
		Log::message("\Handling EndAdaptationColor event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndAdaptationColor().disconnect(endadaptationcolor_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndAdaptationColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndAdaptationColor().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndAdaptationColor().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginTAA () const

event triggered before the Temporal Anti-Aliasing (TAA) pass. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginTAA event handler
void begintaa_event_handler()
{
	Log::message("\Handling BeginTAA event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begintaa_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginTAA().connect(begintaa_event_connections, begintaa_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginTAA().connect(begintaa_event_connections, []() {
		Log::message("\Handling BeginTAA event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begintaa_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begintaa_event_connection;

// subscribe to the BeginTAA event with a handler function keeping the connection
publisher->getEventBeginTAA().connect(begintaa_event_connection, begintaa_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begintaa_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begintaa_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginTAA event via the connection
begintaa_event_connection.disconnect();

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

	// A BeginTAA event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginTAA event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginTAA().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begintaa_handler_id;

// subscribe to the BeginTAA event with a lambda handler function and keeping connection ID
begintaa_handler_id = publisher->getEventBeginTAA().connect(e_connections, []() {
		Log::message("\Handling BeginTAA event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginTAA().disconnect(begintaa_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginTAA events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginTAA().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginTAA().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndTAA () const

event triggered after the Temporal Anti-Aliasing (TAA) pass. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndTAA event handler
void endtaa_event_handler()
{
	Log::message("\Handling EndTAA event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endtaa_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndTAA().connect(endtaa_event_connections, endtaa_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndTAA().connect(endtaa_event_connections, []() {
		Log::message("\Handling EndTAA event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endtaa_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endtaa_event_connection;

// subscribe to the EndTAA event with a handler function keeping the connection
publisher->getEventEndTAA().connect(endtaa_event_connection, endtaa_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endtaa_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endtaa_event_connection.setEnabled(true);

// ...

// remove subscription to the EndTAA event via the connection
endtaa_event_connection.disconnect();

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

	// A EndTAA event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndTAA event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndTAA().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endtaa_handler_id;

// subscribe to the EndTAA event with a lambda handler function and keeping connection ID
endtaa_handler_id = publisher->getEventEndTAA().connect(e_connections, []() {
		Log::message("\Handling EndTAA event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndTAA().disconnect(endtaa_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndTAA events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndTAA().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndTAA().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginCameraEffects () const

event triggered before the camera effects stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginCameraEffects event handler
void begincameraeffects_event_handler()
{
	Log::message("\Handling BeginCameraEffects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincameraeffects_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginCameraEffects().connect(begincameraeffects_event_connections, begincameraeffects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginCameraEffects().connect(begincameraeffects_event_connections, []() {
		Log::message("\Handling BeginCameraEffects event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begincameraeffects_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begincameraeffects_event_connection;

// subscribe to the BeginCameraEffects event with a handler function keeping the connection
publisher->getEventBeginCameraEffects().connect(begincameraeffects_event_connection, begincameraeffects_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begincameraeffects_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begincameraeffects_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginCameraEffects event via the connection
begincameraeffects_event_connection.disconnect();

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

	// A BeginCameraEffects event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginCameraEffects event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginCameraEffects().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begincameraeffects_handler_id;

// subscribe to the BeginCameraEffects event with a lambda handler function and keeping connection ID
begincameraeffects_handler_id = publisher->getEventBeginCameraEffects().connect(e_connections, []() {
		Log::message("\Handling BeginCameraEffects event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginCameraEffects().disconnect(begincameraeffects_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginCameraEffects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginCameraEffects().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginCameraEffects().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndCameraEffects () const

event triggered after the camera effects stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndCameraEffects event handler
void endcameraeffects_event_handler()
{
	Log::message("\Handling EndCameraEffects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcameraeffects_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndCameraEffects().connect(endcameraeffects_event_connections, endcameraeffects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndCameraEffects().connect(endcameraeffects_event_connections, []() {
		Log::message("\Handling EndCameraEffects event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endcameraeffects_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endcameraeffects_event_connection;

// subscribe to the EndCameraEffects event with a handler function keeping the connection
publisher->getEventEndCameraEffects().connect(endcameraeffects_event_connection, endcameraeffects_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endcameraeffects_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endcameraeffects_event_connection.setEnabled(true);

// ...

// remove subscription to the EndCameraEffects event via the connection
endcameraeffects_event_connection.disconnect();

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

	// A EndCameraEffects event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndCameraEffects event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndCameraEffects().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endcameraeffects_handler_id;

// subscribe to the EndCameraEffects event with a lambda handler function and keeping connection ID
endcameraeffects_handler_id = publisher->getEventEndCameraEffects().connect(e_connections, []() {
		Log::message("\Handling EndCameraEffects event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndCameraEffects().disconnect(endcameraeffects_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndCameraEffects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndCameraEffects().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndCameraEffects().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginPostMaterials () const

event triggered before the post materials rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginPostMaterials event handler
void beginpostmaterials_event_handler()
{
	Log::message("\Handling BeginPostMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpostmaterials_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginPostMaterials().connect(beginpostmaterials_event_connections, beginpostmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginPostMaterials().connect(beginpostmaterials_event_connections, []() {
		Log::message("\Handling BeginPostMaterials event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginpostmaterials_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginpostmaterials_event_connection;

// subscribe to the BeginPostMaterials event with a handler function keeping the connection
publisher->getEventBeginPostMaterials().connect(beginpostmaterials_event_connection, beginpostmaterials_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginpostmaterials_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginpostmaterials_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginPostMaterials event via the connection
beginpostmaterials_event_connection.disconnect();

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

	// A BeginPostMaterials event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginPostMaterials event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginPostMaterials().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginpostmaterials_handler_id;

// subscribe to the BeginPostMaterials event with a lambda handler function and keeping connection ID
beginpostmaterials_handler_id = publisher->getEventBeginPostMaterials().connect(e_connections, []() {
		Log::message("\Handling BeginPostMaterials event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginPostMaterials().disconnect(beginpostmaterials_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginPostMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginPostMaterials().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginPostMaterials().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndPostMaterials () const

event triggered after the post materials rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndPostMaterials event handler
void endpostmaterials_event_handler()
{
	Log::message("\Handling EndPostMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpostmaterials_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndPostMaterials().connect(endpostmaterials_event_connections, endpostmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndPostMaterials().connect(endpostmaterials_event_connections, []() {
		Log::message("\Handling EndPostMaterials event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endpostmaterials_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endpostmaterials_event_connection;

// subscribe to the EndPostMaterials event with a handler function keeping the connection
publisher->getEventEndPostMaterials().connect(endpostmaterials_event_connection, endpostmaterials_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endpostmaterials_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endpostmaterials_event_connection.setEnabled(true);

// ...

// remove subscription to the EndPostMaterials event via the connection
endpostmaterials_event_connection.disconnect();

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

	// A EndPostMaterials event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndPostMaterials event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndPostMaterials().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endpostmaterials_handler_id;

// subscribe to the EndPostMaterials event with a lambda handler function and keeping connection ID
endpostmaterials_handler_id = publisher->getEventEndPostMaterials().connect(e_connections, []() {
		Log::message("\Handling EndPostMaterials event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndPostMaterials().disconnect(endpostmaterials_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndPostMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndPostMaterials().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndPostMaterials().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginDebugMaterials () const

event triggered before the debug materials stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginDebugMaterials event handler
void begindebugmaterials_event_handler()
{
	Log::message("\Handling BeginDebugMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begindebugmaterials_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginDebugMaterials().connect(begindebugmaterials_event_connections, begindebugmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginDebugMaterials().connect(begindebugmaterials_event_connections, []() {
		Log::message("\Handling BeginDebugMaterials event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begindebugmaterials_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begindebugmaterials_event_connection;

// subscribe to the BeginDebugMaterials event with a handler function keeping the connection
publisher->getEventBeginDebugMaterials().connect(begindebugmaterials_event_connection, begindebugmaterials_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begindebugmaterials_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begindebugmaterials_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginDebugMaterials event via the connection
begindebugmaterials_event_connection.disconnect();

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

	// A BeginDebugMaterials event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginDebugMaterials event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginDebugMaterials().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begindebugmaterials_handler_id;

// subscribe to the BeginDebugMaterials event with a lambda handler function and keeping connection ID
begindebugmaterials_handler_id = publisher->getEventBeginDebugMaterials().connect(e_connections, []() {
		Log::message("\Handling BeginDebugMaterials event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginDebugMaterials().disconnect(begindebugmaterials_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginDebugMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginDebugMaterials().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginDebugMaterials().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndDebugMaterials () const

event triggered after the debug materials stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndDebugMaterials event handler
void enddebugmaterials_event_handler()
{
	Log::message("\Handling EndDebugMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enddebugmaterials_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndDebugMaterials().connect(enddebugmaterials_event_connections, enddebugmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndDebugMaterials().connect(enddebugmaterials_event_connections, []() {
		Log::message("\Handling EndDebugMaterials event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
enddebugmaterials_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection enddebugmaterials_event_connection;

// subscribe to the EndDebugMaterials event with a handler function keeping the connection
publisher->getEventEndDebugMaterials().connect(enddebugmaterials_event_connection, enddebugmaterials_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
enddebugmaterials_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
enddebugmaterials_event_connection.setEnabled(true);

// ...

// remove subscription to the EndDebugMaterials event via the connection
enddebugmaterials_event_connection.disconnect();

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

	// A EndDebugMaterials event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndDebugMaterials event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndDebugMaterials().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId enddebugmaterials_handler_id;

// subscribe to the EndDebugMaterials event with a lambda handler function and keeping connection ID
enddebugmaterials_handler_id = publisher->getEventEndDebugMaterials().connect(e_connections, []() {
		Log::message("\Handling EndDebugMaterials event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndDebugMaterials().disconnect(enddebugmaterials_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndDebugMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndDebugMaterials().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndDebugMaterials().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventBeginVisualizer () const

event triggered before the visualizer rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the BeginVisualizer event handler
void beginvisualizer_event_handler()
{
	Log::message("\Handling BeginVisualizer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginvisualizer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBeginVisualizer().connect(beginvisualizer_event_connections, beginvisualizer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBeginVisualizer().connect(beginvisualizer_event_connections, []() {
		Log::message("\Handling BeginVisualizer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
beginvisualizer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection beginvisualizer_event_connection;

// subscribe to the BeginVisualizer event with a handler function keeping the connection
publisher->getEventBeginVisualizer().connect(beginvisualizer_event_connection, beginvisualizer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
beginvisualizer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
beginvisualizer_event_connection.setEnabled(true);

// ...

// remove subscription to the BeginVisualizer event via the connection
beginvisualizer_event_connection.disconnect();

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

	// A BeginVisualizer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling BeginVisualizer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBeginVisualizer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId beginvisualizer_handler_id;

// subscribe to the BeginVisualizer event with a lambda handler function and keeping connection ID
beginvisualizer_handler_id = publisher->getEventBeginVisualizer().connect(e_connections, []() {
		Log::message("\Handling BeginVisualizer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBeginVisualizer().disconnect(beginvisualizer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all BeginVisualizer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBeginVisualizer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBeginVisualizer().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndVisualizer () const

event triggered after the visualizer rendering stage. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndVisualizer event handler
void endvisualizer_event_handler()
{
	Log::message("\Handling EndVisualizer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvisualizer_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndVisualizer().connect(endvisualizer_event_connections, endvisualizer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndVisualizer().connect(endvisualizer_event_connections, []() {
		Log::message("\Handling EndVisualizer event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endvisualizer_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endvisualizer_event_connection;

// subscribe to the EndVisualizer event with a handler function keeping the connection
publisher->getEventEndVisualizer().connect(endvisualizer_event_connection, endvisualizer_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endvisualizer_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endvisualizer_event_connection.setEnabled(true);

// ...

// remove subscription to the EndVisualizer event via the connection
endvisualizer_event_connection.disconnect();

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

	// A EndVisualizer event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndVisualizer event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndVisualizer().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endvisualizer_handler_id;

// subscribe to the EndVisualizer event with a lambda handler function and keeping connection ID
endvisualizer_handler_id = publisher->getEventEndVisualizer().connect(e_connections, []() {
		Log::message("\Handling EndVisualizer event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndVisualizer().disconnect(endvisualizer_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndVisualizer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndVisualizer().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndVisualizer().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndScreen () const

event triggered after the stage of rendering each screen (a stereo image has 2 screens, while a cubemap will have 6). You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndScreen event handler
void endscreen_event_handler()
{
	Log::message("\Handling EndScreen event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endscreen_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndScreen().connect(endscreen_event_connections, endscreen_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndScreen().connect(endscreen_event_connections, []() {
		Log::message("\Handling EndScreen event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endscreen_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endscreen_event_connection;

// subscribe to the EndScreen event with a handler function keeping the connection
publisher->getEventEndScreen().connect(endscreen_event_connection, endscreen_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endscreen_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endscreen_event_connection.setEnabled(true);

// ...

// remove subscription to the EndScreen event via the connection
endscreen_event_connection.disconnect();

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

	// A EndScreen event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndScreen event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndScreen().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endscreen_handler_id;

// subscribe to the EndScreen event with a lambda handler function and keeping connection ID
endscreen_handler_id = publisher->getEventEndScreen().connect(e_connections, []() {
		Log::message("\Handling EndScreen event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndScreen().disconnect(endscreen_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndScreen events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndScreen().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndScreen().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEnd () const

event triggered when rendering of the frame ends. You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the End event handler
void end_event_handler()
{
	Log::message("\Handling End event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections end_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEnd().connect(end_event_connections, end_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEnd().connect(end_event_connections, []() {
		Log::message("\Handling End event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
end_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection end_event_connection;

// subscribe to the End event with a handler function keeping the connection
publisher->getEventEnd().connect(end_event_connection, end_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
end_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
end_event_connection.setEnabled(true);

// ...

// remove subscription to the End event via the connection
end_event_connection.disconnect();

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

	// A End event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling End event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEnd().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId end_handler_id;

// subscribe to the End event with a lambda handler function and keeping connection ID
end_handler_id = publisher->getEventEnd().connect(e_connections, []() {
		Log::message("\Handling End event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEnd().disconnect(end_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all End events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEnd().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEnd().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventEndVRQuadComposeEyeSwapchains () const

Event triggered after composing VR viewports, enabling you to subscribe and perform certain actions (e.g. implement a binoculars effect using post-materials). You can subscribe to events via *connect()* ï¿½and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* ï¿½and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* ï¿½classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the EndVRQuadComposeEyeSwapchains event handler
void endvrquadcomposeeyeswapchains_event_handler()
{
	Log::message("\Handling EndVRQuadComposeEyeSwapchains event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvrquadcomposeeyeswapchains_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEndVRQuadComposeEyeSwapchains().connect(endvrquadcomposeeyeswapchains_event_connections, endvrquadcomposeeyeswapchains_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEndVRQuadComposeEyeSwapchains().connect(endvrquadcomposeeyeswapchains_event_connections, []() {
		Log::message("\Handling EndVRQuadComposeEyeSwapchains event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
endvrquadcomposeeyeswapchains_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection endvrquadcomposeeyeswapchains_event_connection;

// subscribe to the EndVRQuadComposeEyeSwapchains event with a handler function keeping the connection
publisher->getEventEndVRQuadComposeEyeSwapchains().connect(endvrquadcomposeeyeswapchains_event_connection, endvrquadcomposeeyeswapchains_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
endvrquadcomposeeyeswapchains_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
endvrquadcomposeeyeswapchains_event_connection.setEnabled(true);

// ...

// remove subscription to the EndVRQuadComposeEyeSwapchains event via the connection
endvrquadcomposeeyeswapchains_event_connection.disconnect();

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

	// A EndVRQuadComposeEyeSwapchains event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling EndVRQuadComposeEyeSwapchains event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEndVRQuadComposeEyeSwapchains().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId endvrquadcomposeeyeswapchains_handler_id;

// subscribe to the EndVRQuadComposeEyeSwapchains event with a lambda handler function and keeping connection ID
endvrquadcomposeeyeswapchains_handler_id = publisher->getEventEndVRQuadComposeEyeSwapchains().connect(e_connections, []() {
		Log::message("\Handling EndVRQuadComposeEyeSwapchains event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEndVRQuadComposeEyeSwapchains().disconnect(endvrquadcomposeeyeswapchains_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all EndVRQuadComposeEyeSwapchains events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEndVRQuadComposeEyeSwapchains().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEndVRQuadComposeEyeSwapchains().setEnabled(true);

```

</details>

### Return value

Event instance.
## void setPanoramaFisheyeKannalaBrandtCoefficients ( const Math:: vec4 & coefficients )

Sets a new four radial distortion coefficients (k1, k2, k3, k4) of the Kannala-Brandt fisheye camera model used by the corresponding panorama mode. They define the polynomial mapping the angle between the incoming ray and the optical axis to the normalized image radius. The default value (1, 0, 0, 0) corresponds to the pure equidistant projection. This mode reproduces the image geometry of a real calibrated fisheye camera, with the coefficients taken from the camera calibration data.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **coefficients** - The radial distortion coefficients of the Kannala-Brandt model

## Math:: vec4 getPanoramaFisheyeKannalaBrandtCoefficients () const

Returns the current four radial distortion coefficients (k1, k2, k3, k4) of the Kannala-Brandt fisheye camera model used by the corresponding panorama mode. They define the polynomial mapping the angle between the incoming ray and the optical axis to the normalized image radius. The default value (1, 0, 0, 0) corresponds to the pure equidistant projection. This mode reproduces the image geometry of a real calibrated fisheye camera, with the coefficients taken from the camera calibration data.
### Return value

Current radial distortion coefficients of the Kannala-Brandt model
## void setPanoramaFisheyeKannalaBrandtFocalLength ( const Math:: vec2 & length )

Sets a new focal length intrinsics (fx, fy) of the calibrated fisheye camera, in pixels, used by the Kannala-Brandt panorama mode to convert pixel coordinates to normalized camera coordinates.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **length** - The focal length intrinsics of the calibrated fisheye camera

## Math:: vec2 getPanoramaFisheyeKannalaBrandtFocalLength () const

Returns the current focal length intrinsics (fx, fy) of the calibrated fisheye camera, in pixels, used by the Kannala-Brandt panorama mode to convert pixel coordinates to normalized camera coordinates.
### Return value

Current focal length intrinsics of the calibrated fisheye camera
## void setPanoramaFisheyeKannalaBrandtImageCircleRadius ( float radius )

Sets a new radius of the valid image circle of the fisheye lens in normalized radial coordinates, used by the Kannala-Brandt panorama mode: pixels outside this radius are masked out, reproducing the image circle of the real lens.
### Arguments

- *float* **radius** - The radius of the valid image circle of the fisheye lens

## float getPanoramaFisheyeKannalaBrandtImageCircleRadius () const

Returns the current radius of the valid image circle of the fisheye lens in normalized radial coordinates, used by the Kannala-Brandt panorama mode: pixels outside this radius are masked out, reproducing the image circle of the real lens.
### Return value

Current radius of the valid image circle of the fisheye lens
## void setPanoramaFisheyeKannalaBrandtImageDimensions ( const Math:: vec2 & dimensions )

Sets a new dimensions (width, height), in pixels, of the calibrated camera image the Kannala-Brandt intrinsics refer to. The viewport coordinates are mapped to this pixel space before the intrinsics are applied.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **dimensions** - The image dimensions the fisheye intrinsics refer to

## Math:: vec2 getPanoramaFisheyeKannalaBrandtImageDimensions () const

Returns the current dimensions (width, height), in pixels, of the calibrated camera image the Kannala-Brandt intrinsics refer to. The viewport coordinates are mapped to this pixel space before the intrinsics are applied.
### Return value

Current image dimensions the fisheye intrinsics refer to
## void setPanoramaFisheyeKannalaBrandtPrincipalPoint ( const Math:: vec2 & point )

Sets a new principal point intrinsics (cx, cy) of the calibrated fisheye camera, in pixels: the image position of the optical axis used by the Kannala-Brandt panorama mode.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **point** - The principal point intrinsics of the calibrated fisheye camera

## Math:: vec2 getPanoramaFisheyeKannalaBrandtPrincipalPoint () const

Returns the current principal point intrinsics (cx, cy) of the calibrated fisheye camera, in pixels: the image position of the optical axis used by the Kannala-Brandt panorama mode.
### Return value

Current principal point intrinsics of the calibrated fisheye camera
## void setPanoramaFisheyeKannalaBrandtSkew ( float skew )

Sets a new skew (axis non-orthogonality) coefficient of the calibration matrix used by the Kannala-Brandt panorama mode. The value of 0 (default) corresponds to orthogonal pixel axes.
### Arguments

- *float* **skew** - The skew intrinsic of the calibrated fisheye camera

## float getPanoramaFisheyeKannalaBrandtSkew () const

Returns the current skew (axis non-orthogonality) coefficient of the calibration matrix used by the Kannala-Brandt panorama mode. The value of 0 (default) corresponds to orthogonal pixel axes.
### Return value

Current skew intrinsic of the calibrated fisheye camera
## void setPanoramaFisheyeKannalaBrandtTangentialDistortion ( const Math:: vec2 & distortion )

Sets a new tangential (decentering) distortion coefficients (p1, p2) of the calibrated fisheye camera used by the Kannala-Brandt panorama mode. The value (0, 0) means no tangential distortion.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **distortion** - The tangential distortion coefficients of the calibrated fisheye camera

## Math:: vec2 getPanoramaFisheyeKannalaBrandtTangentialDistortion () const

Returns the current tangential (decentering) distortion coefficients (p1, p2) of the calibrated fisheye camera used by the Kannala-Brandt panorama mode. The value (0, 0) means no tangential distortion.
### Return value

Current tangential distortion coefficients of the calibrated fisheye camera
## void setPanoramaForceDisableScreenSpaceEffects ( bool effects )

Sets a new value indicating if screen-space and screen-dependent camera effects (such as SSR, SSAO, SSGI, motion blur, DOF, bloom, lens flares, local tonemapper) are forcibly disabled while the viewport renders a panorama. These effects are computed per panorama face and would produce visible seams between the faces. Enabled by default; when disabled, the effects stay as configured at the cost of per-face artifacts.
### Arguments

- *bool* **effects** - Set **true** to enable forced disabling of screen-space effects in panorama modes; **false** - to disable it.

## bool isPanoramaForceDisableScreenSpaceEffects () const

Returns the current value indicating if screen-space and screen-dependent camera effects (such as SSR, SSAO, SSGI, motion blur, DOF, bloom, lens flares, local tonemapper) are forcibly disabled while the viewport renders a panorama. These effects are computed per panorama face and would produce visible seams between the faces. Enabled by default; when disabled, the effects stay as configured at the cost of per-face artifacts.
### Return value

**true** if forced disabling of screen-space effects in panorama modes is enabled ; otherwise **false**.
## void setPanoramaFisheyeKannalaBrandtChromaticAberration ( float aberration )

Sets a new chromatic aberration intensity of the fisheye lens, used by the Kannala-Brandt panorama mode: the red channel is sampled at the radial distance scaled by (1 - value), the blue channel at (1 + value), reproducing lateral chromatic aberration of a real lens. 0 means no chromatic aberration.
### Arguments

- *float* **aberration** - The chromatic aberration intensity of the fisheye lens

## float getPanoramaFisheyeKannalaBrandtChromaticAberration () const

Returns the current chromatic aberration intensity of the fisheye lens, used by the Kannala-Brandt panorama mode: the red channel is sampled at the radial distance scaled by (1 - value), the blue channel at (1 + value), reproducing lateral chromatic aberration of a real lens. 0 means no chromatic aberration.
### Return value

Current chromatic aberration intensity of the fisheye lens
## void setPanoramaFisheyeKannalaBrandtVignettingCoefficient5 ( float coefficient5 )

Sets a new fifth coefficient of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the coefficient at the 10th power of the normalized radial distance, kept separate because the coefficients vector holds only four components.
### Arguments

- *float* **coefficient5** - The fifth coefficient of the fisheye vignetting polynomial

## float getPanoramaFisheyeKannalaBrandtVignettingCoefficient5 () const

Returns the current fifth coefficient of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the coefficient at the 10th power of the normalized radial distance, kept separate because the coefficients vector holds only four components.
### Return value

Current fifth coefficient of the fisheye vignetting polynomial
## void setPanoramaFisheyeKannalaBrandtVignettingCoefficients ( const Math:: vec4 & coefficients )

Sets a new first four coefficients of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the vignetting intensity is an even-order polynomial of the radial distance normalized by the image circle radius, with these values as the coefficients at the 2nd, 4th, 6th, and 8th powers.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **coefficients** - The first four coefficients of the fisheye vignetting polynomial

## Math:: vec4 getPanoramaFisheyeKannalaBrandtVignettingCoefficients () const

Returns the current first four coefficients of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the vignetting intensity is an even-order polynomial of the radial distance normalized by the image circle radius, with these values as the coefficients at the 2nd, 4th, 6th, and 8th powers.
### Return value

Current first four coefficients of the fisheye vignetting polynomial
---

## static ViewportPtr create ( )


Creates a new viewport with default settings.


> **Notice:** We don't recommend creating a viewport every frame, as such approach is unoptimal and exhaust GPU resources. Create viewports in **init()** instead, to have them cached for further use.


## void appendSkipFlags ( int flags )

Appends specified [skip flags](#SKIP_SHADOWS) to the list of currently used ones.
### Arguments

- *int* **flags** - [Skip flags](#SKIP_SHADOWS) to append.

## int checkSkipFlags ( int flags )

Returns a value indicating if the specified [skip flags](#SKIP_SHADOWS) are set for the current viewport.
### Arguments

- *int* **flags** - [Skip flags](#SKIP_SHADOWS) to check.

### Return value

1 if the skip flags are set; otherwise, 0.
## void removeSkipFlags ( int flags )

Removes specified [skip flags](#SKIP_SHADOWS) from the list of currently used ones.
### Arguments

- *int* **flags** - [Skip flags](#SKIP_SHADOWS) to remove.

## void render ( const Ptr < Camera > & camera )


Renders an image from the specified camera. This method is used to integrate the engine to a 3rd party renderer.


To render an image from the camera to the *[RenderTarget](../../../api/library/rendering/class.rendertarget_cpp.md)* interface, do the following:


```cpp
camera = Camera::create();

render_target->enable();
{
	viewport->render(camera);
}
render_target->disable();

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera an image from which should be rendered.

## void render ( const Ptr < Camera > & camera , int width , int height )

Renders an image of the specified size from the specified camera to the current rendering target.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.

## void renderEngine ( const Ptr < Camera > & camera )

Renders an Engine viewport for the specified camera to the current rendering target. This method renders a splash screen and provides an image in accordance with panoramic and stereo rendering settings.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.

## void renderTexture2D ( const Ptr < Camera > & camera , const Ptr < Texture > & texture )

Renders an image from the camera to the specified 2D texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cpp.md) to save the result to.

## void renderTexture2D ( const Ptr < Camera > & camera , const Ptr < Texture > & texture , int width , int height , bool hdr = 0 )

Renders an image of the specified size from the camera to a 2D texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cpp.md) to save the result to.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *bool* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D texture: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_cpp.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_cpp.md#FORMAT_RGBA8)

## void renderTextureCube ( const Ptr < Camera > & camera , const Ptr < Texture > & texture , bool local_space = false )

Renders the image from the camera to the cubemap texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target Cube [texture](../../../api/library/rendering/class.texture_cpp.md) to save the result to.
- *bool* **local_space** - A flag indicating if the camera angle should be used for the cube map rendering.

## void renderTextureCube ( const Ptr < Camera > & camera , const Ptr < Texture > & texture , int size , bool hdr = 0 , bool local_space = 0 )

Renders the image from the camera to the cube map of the specified size.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target cube map to save the result to.
- *int* **size** - Cube map edge size.
- *bool* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D texture: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_cpp.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_cpp.md#FORMAT_RGBA8)
- *bool* **local_space** - A flag indicating if the camera angle should be used for the cube map rendering.

## void renderNode ( const Ptr < Camera > & camera , const Ptr < Node > & node )

Renders the given node with all children to the current rendering target.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to be rendered.

## void renderNode ( const Ptr < Camera > & camera , const Ptr < Node > & node , int width , int height )

Renders the given node with all children to the current rendering target.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to be rendered.
- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.

## void renderNodeTexture2D ( const Ptr < Camera > & camera , const Ptr < Node > & node , const Ptr < Texture > & texture , int width , int height , bool hdr )

Renders the given node with all children to the 2D texture of the specified size.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Pointer to the node to be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cpp.md) to save the result to.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *bool* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D texture: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_cpp.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_cpp.md#FORMAT_RGBA8)

## void renderNodeTexture2D ( const Ptr < Camera > & camera , const Ptr < Node > & node , const Ptr < Texture > & texture )

Renders the given node with all children to the specified 2D texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Pointer to the node to be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cpp.md) to save the result to.

## void renderNodes ( const Ptr < Camera > & camera , const Vector < Ptr < Node >> & nodes )

Renders given nodes with all their children to the current rendering target.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - List of the nodes to be rendered.

## void renderNodes ( const Ptr < Camera > & camera , const Vector < Ptr < Node >> & nodes , int width , int height )

Renders given nodes with all their children to the current rendering target of the specified size.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - List of the nodes to be rendered.
- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.

## void renderNodesTexture2D ( const Ptr < Camera > & camera , const Vector < Ptr < Node >> & nodes , const Ptr < Texture > & texture , int width , int height , int hdr )

Renders given nodes with all their children to the 2D texture of the specified size.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - List of the nodes to be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cpp.md) to save the result to.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D image: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_cpp.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_cpp.md#FORMAT_RGBA8)

## void renderNodesTexture2D ( const Ptr < Camera > & camera , const Vector < Ptr < Node >> & nodes , const Ptr < Texture > & texture )

Renders given nodes with all their children to the specified 2D texture.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera, an image from which should be rendered.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - List of the nodes to be rendered.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_cpp.md) to save the result to.

## void renderStereo ( const Ptr < Camera > & camera_left , const Ptr < Camera > & camera_right , const char * stereo_material )

Renders a stereo image in the current viewport.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera_left** - Camera that renders an image for the left eye.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera_right** - Camera that renders an image for the right eye.
- *const char ** **stereo_material** - List of names of stereo materials to be used.

## void renderStereoPeripheral ( const Ptr < Camera > & camera_left , const Ptr < Camera > & camera_right , const Ptr < Camera > & camera_focus_left , const Ptr < Camera > & camera_focus_right , const Ptr < Texture > & texture_left , const Ptr < Texture > & texture_right , const Ptr < Texture > & texture_focus_left , const Ptr < Texture > & texture_focus_right , const char * stereo_material )

Renders a stereo image for HMDs having context (peripheral) and focus displays. This method saves performance on shadows and reflections along with other optimizations reducing rendering load, such as reduced resolutions for textures.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera_left** - Camera that renders an image for the left context (low-res) display.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera_right** - Camera that renders an image for the right context (low-res) display.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera_focus_left** - Camera that renders an image for the left focus (high-res) display.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera_focus_right** - Camera that renders an image for the right focus (high-res) display.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture_left** - Texture to save the image rendered for the left context (low-res) display.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture_right** - Texture to save the image rendered for the right context (low-res) display.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture_focus_left** - Texture to save the image rendered for the left focus (high-res) display.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture_focus_right** - Texture to save the image rendered for the right focus (high-res) display.
- *const char ** **stereo_material** - List of names of stereo materials to be used.

## void setStereoHiddenAreaMesh ( const Ptr < Mesh > & hidden_area_mesh_left , const Ptr < Mesh > & hidden_area_mesh_right )


Sets custom meshes to be used for culling pixels, that are not visible in VR.


> **Notice:** Requires [render_stereo_hidden_area](../../../code/console/index.md#render_stereo_hidden_area) = 2


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **hidden_area_mesh_left** - [Mesh](../../../api/library/rendering/class.mesh_cpp.md) representing hidden area for the left eye.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **hidden_area_mesh_right** - [Mesh](../../../api/library/rendering/class.mesh_cpp.md) representing hidden area for the right eye.

## void clearStereoHiddenAreaMesh ( )

Clears meshes that represent hidden areas for both, left and right eye. Hidden areas are used for culling pixels, that are not visible in VR
## void setEnvironmentTexturePath ( const char * name )

Sets the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) for the viewport. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Arguments

- *const char ** **name** - Path to the cubemap defining the environment color.

## const char * getEnvironmentTexturePath ( )

Returns the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) set for the viewport. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Return value

Path to the cubemap defining the environment color.
## void resetEnvironmentTexture ( )

Resets the current environment texture to the default one.
## void renderVREngine ( )

Renders the VR viewport if VR is enabled, taking into account the [vr mirror mode](../../../api/library/vr/class.vr_cpp.md#MirrorMode) set.
## void lockResources ( )

Locks resources (such as temporal old textures) in the current viewport so they won't be reused or released.
## void unlockResources ( )

Unlocks resources (such as temporal old textures) in the current viewport so they can be reused and released by the engine.
## bool isLockedResources ( ) const

Returns a value indicating if resources (such as temporal old textures) in the current viewport are locked and won't be reused or released.
### Return value

true if the resources are locked; otherwise, false.
