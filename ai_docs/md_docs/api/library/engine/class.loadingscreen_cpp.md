# Unigine.LoadingScreen Class (CPP)

**Header:** #include <UnigineLoadingScreen.h>

> **Notice:** This class is a singleton.


A singleton that controls the settings of the [loading screen](../../../code/gui/screens/index.md#loading). Demonstration of it gives UNIGINE the time to load all world nodes and resources. You can also show your own loading screen when needed.


A loading screen displays a [texture](../../../code/gui/skin/index.md#splash) that is usually divided into two parts stacked vertically � the initial and final pictures � which are gradually blended from the beginning up to the end of loading to show the progress. Blending is performed based on the alpha channel of the outro (lower) part of the texture so pseudo-animation can be created using the alpha channel: regions of the lower half with small alpha values will be shown first, regions with larger alpha values will be shown last.


### See Also


- Quick Video Guide: [How To Customize Loading Screens](../../../videotutorials/how_to/how_to_cs/loading_screen.md)
- UnigineScript samples:

  -
  -
  -


### Example


Here's a code example on how to add your own loading screens for application and world loading.


To show your loading screen on system logic initialization before a world is loaded, define it inside the *init()* method of the [System Logic](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic):


```cpp
#include "AppSystemLogic.h"
#include "UnigineLoadingScreen.h"

using namespace Unigine;

int AppSystemLogic::init()
{


	// define new transform for loading screen texture
	Math::vec4 transform = Math::vec4(1.0f, 1.0f, 0.0f, 0.0f);

	// enable the loading screen
	LoadingScreen::setEnabled(true);

	// set transform to the loading screen texture
	LoadingScreen::setTransform(transform);

	Math::ivec2 winsize = WindowManager::getMainWindow()->getClientSize();
	// compute the aspect ratio to show the corresponding texture
	float aspect_ratio = (float)winsize.x / (float)winsize.y;

	// if the aspect ratio is 4:3 show the following loading screen
	// during world loading
	if (aspect_ratio < 1.5f) {
		LoadingScreen::setTexturePath("textures/splash_4x3.png");
	}
	else {
		// if the aspect ratio is 16:9 show this loading screen
		// during world loading
		LoadingScreen::setTexturePath("textures/splash_16x9.png");
	}
	// set the text to be displayed on the loading screen
	// with a certain displacement along the X and Y axes
	LoadingScreen::setText("<xy x=\"%50\" dx=\"0\" y=\"%50\" dy=\"0\"/>LOADING_PROGRESS");

	// set duration (in milliseconds) and display the loading screen on world loading
	float duration = 5000.0f;
	float begin = clock();

	while (clock() - begin < duration)
		LoadingScreen::render((clock() - begin) / duration * 100.0f);

	// disable the loading screen
	LoadingScreen::setEnabled(false);

	return 1;
}


```


A loading screen defined in the *init()* method of the [World Logic](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic) will be shown right after a world is loaded:


```cpp
#include "AppWorldLogic.h"
#include "UnigineLoadingScreen.h"

using namespace Unigine;

int AppWorldLogic::init()
{

	// enable the loading screen
	LoadingScreen::setEnabled(true);


	// set the text to be displayed on the loading screen,
	// specifying a color, a font, and a certain displacement along the X and Y axes
	LoadingScreen::setText("<p align=\"center\"><font size=\"20\" color=\"#FF0000FF\">CUSTOM LOADING TEXT</font></p>");

	// set duration (in milliseconds) and display the loading screen on world loading
	float duration = 5000.0f;
	float begin = clock();

	while (clock() - begin < duration)
		LoadingScreen::render((clock() - begin) / duration * 100.0f);

	// disable the loading screen
	LoadingScreen::setEnabled(false);

	return 1;
}


```


## LoadingScreen Class

### Members

## const char * getMessage () const

Returns the current text message representing the current loading stage.
### Return value

Current text message representing the current loading stage.
## int getProgress () const

Returns the current progress state.
### Return value

Current progress state in the **[0, 100]** range.
## void setMessageShadersCompilation ( const char * compilation )

Sets a new message displayed on shaders compilation. The text [aliases](#setText_cstr_void) are also supported.
### Arguments

- *const char ** **compilation** - The message displayed on shaders compilation.

## const char * getMessageShadersCompilation () const

Returns the current message displayed on shaders compilation. The text [aliases](#setText_cstr_void) are also supported.
### Return value

Current message displayed on shaders compilation.
## void setMessageLoadingWorld ( const char * world )

Sets a new message displayed on world loading. The text [aliases](#setText_cstr_void) are also supported.
### Arguments

- *const char ** **world** - The message displayed on world loading.

## const char * getMessageLoadingWorld () const

Returns the current message displayed on world loading. The text [aliases](#setText_cstr_void) are also supported.
### Return value

Current message displayed on world loading.
## void setFontPath ( const char * path )

Sets a new path to the font used to render the text.
### Arguments

- *const char ** **path** - The path to the font used to render the text (True Type Font).

## const char * getFontPath () const

Returns the current path to the font used to render the text.
### Return value

Current path to the font used to render the text (True Type Font).
## void setText ( const char * text )

Sets a new text of the loading screen.
### Arguments

- *const char ** **text** - The text of the loading screen. Can be either a plain or [rich text](../../../code/gui/ui/index.md#rich_text). A number of aliases is available:

  - UNIGINE_COPYRIGHT � the UNIGINE copyright text.
  - UNIGINE_VERSION � the current UNIGINE version.
  - LOADING_PROGRESS � the loading progress going from 0 to 100.
  - LOADING_WORLD � the world being loaded (if any).

## const char * getText () const

Returns the current text of the loading screen.
### Return value

Current
text of the loading screen. Can be either a plain or [rich text](../../../code/gui/ui/index.md#rich_text). A number of aliases is available:


- UNIGINE_COPYRIGHT � the UNIGINE copyright text.
- UNIGINE_VERSION � the current UNIGINE version.
- LOADING_PROGRESS � the loading progress going from 0 to 100.
- LOADING_WORLD � the world being loaded (if any).


## void setBackgroundColor ( const Math:: vec4 & color )

Sets a new background color of the loading screen.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **color** - The background color of the loading screen.

## Math:: vec4 getBackgroundColor () const

Returns the current background color of the loading screen.
### Return value

Current background color of the loading screen.
## void setTransform ( const Math:: vec4 & transform )

Sets a new transformation of the loading screen texture.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md)&* **transform** - The Transformation of the loading screen texture:

  1. Texture size multiplier.
  2. Window size multiplier.
  3. Horizontal position in the [0.0f, 1.0f] range.
  4. Vertical position in the [0.0f, 1.0f] range.

## Math:: vec4 getTransform () const

Returns the current transformation of the loading screen texture.
### Return value

Current Transformation of the loading screen texture:
1. Texture size multiplier.
2. Window size multiplier.
3. Horizontal position in the [0.0f, 1.0f] range.
4. Vertical position in the [0.0f, 1.0f] range.


## void setTexturePath ( const char * path )

Sets a new path to the texture for the loading screen.
### Arguments

- *const char ** **path** - The path to a file with the custom loading screen texture. If the value equals to NULL (0), no texture is used.

## const char * getTexturePath () const

Returns the current path to the texture for the loading screen.
### Return value

Current path to a file with the custom loading screen texture. If the value equals to NULL (0), no texture is used.
## void setThreshold ( int threshold )

Sets a new amount of blur in the alpha channel when interpolating between states of the loading screen.
> **Notice:** By default, the Threshold value is set to 16.


### Arguments

- *int* **threshold** - The amount of blur in the **[0, 255]** range.

## int getThreshold () const

Returns the current amount of blur in the alpha channel when interpolating between states of the loading screen.
> **Notice:** By default, the Threshold value is set to 16.


### Return value

Current amount of blur in the **[0, 255]** range.
## void setEnabled ( bool enabled )

Sets a new value indicating if manual rendering of a loading screen is allowed.
> **Notice:** Enabling manual rendering is possible only together with the corresponding **render** functions (*[render()](#render_void)*). It cannot be used to enable or disable rendering of the loading screen during the initialization stage of the engine.


### Arguments

- *bool* **enabled** - Set **true** to enable rendering of the loading screen; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if manual rendering of a loading screen is allowed.
> **Notice:** Enabling manual rendering is possible only together with the corresponding **render** functions (*[render()](#render_void)*). It cannot be used to enable or disable rendering of the loading screen during the initialization stage of the engine.


### Return value

**true** if rendering of the loading screen is enabled ; otherwise **false**.
## static Event<> getEventRenderEnd () const

event triggered when rendering of the loading screen ends. The function is useful when you implement a custom loading screen rendering function, for example. The event handler must not take arguments. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the RenderEnd event handler
void renderend_event_handler()
{
	Log::message("\Handling RenderEnd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections renderend_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
LoadingScreen::getEventRenderEnd().connect(renderend_event_connections, renderend_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
LoadingScreen::getEventRenderEnd().connect(renderend_event_connections, []() {
		Log::message("\Handling RenderEnd event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
renderend_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection renderend_event_connection;

// subscribe to the RenderEnd event with a handler function keeping the connection
LoadingScreen::getEventRenderEnd().connect(renderend_event_connection, renderend_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
renderend_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
renderend_event_connection.setEnabled(true);

// ...

// remove subscription to the RenderEnd event via the connection
renderend_event_connection.disconnect();

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

	// A RenderEnd event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling RenderEnd event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
LoadingScreen::getEventRenderEnd().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId renderend_handler_id;

// subscribe to the RenderEnd event with a lambda handler function and keeping connection ID
renderend_handler_id = LoadingScreen::getEventRenderEnd().connect(e_connections, []() {
		Log::message("\Handling RenderEnd event (lambda).\n");
	}
);

// remove the subscription later using the ID
LoadingScreen::getEventRenderEnd().disconnect(renderend_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all RenderEnd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
LoadingScreen::getEventRenderEnd().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
LoadingScreen::getEventRenderEnd().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventRenderBegin () const

event triggered when rendering of the loading screen begins. The function is useful when you implement a custom loading screen rendering function, for example. The event handler must not take arguments. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the RenderBegin event handler
void renderbegin_event_handler()
{
	Log::message("\Handling RenderBegin event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections renderbegin_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
LoadingScreen::getEventRenderBegin().connect(renderbegin_event_connections, renderbegin_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
LoadingScreen::getEventRenderBegin().connect(renderbegin_event_connections, []() {
		Log::message("\Handling RenderBegin event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
renderbegin_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection renderbegin_event_connection;

// subscribe to the RenderBegin event with a handler function keeping the connection
LoadingScreen::getEventRenderBegin().connect(renderbegin_event_connection, renderbegin_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
renderbegin_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
renderbegin_event_connection.setEnabled(true);

// ...

// remove subscription to the RenderBegin event via the connection
renderbegin_event_connection.disconnect();

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

	// A RenderBegin event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling RenderBegin event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
LoadingScreen::getEventRenderBegin().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId renderbegin_handler_id;

// subscribe to the RenderBegin event with a lambda handler function and keeping connection ID
renderbegin_handler_id = LoadingScreen::getEventRenderBegin().connect(e_connections, []() {
		Log::message("\Handling RenderBegin event (lambda).\n");
	}
);

// remove the subscription later using the ID
LoadingScreen::getEventRenderBegin().disconnect(renderbegin_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all RenderBegin events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
LoadingScreen::getEventRenderBegin().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
LoadingScreen::getEventRenderBegin().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## void setImage ( const Ptr < Image > & image )

Sets an [image](../../../code/gui/skin/index.md#splash) for a custom loading screen.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image smart pointer to an image to be used as a custom loading screen.

## void getImage ( const Ptr < Image > & image ) const

Returns the current [image](../../../code/gui/skin/index.md#splash) for a custom loading screen.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image used as a custom loading screen.

## void renderInterface ( )

Renders a static loading screen. Such a screen does not display any progress.
## void render ( )

Renders the loading screen in the current progress state and with the current stage message.
## void render ( int progress )

Renders a custom loading screen in a given progress state. Use this function in a loop to create a gradual change between the initial (upper opaque part) and the final states (bottom transparent part) of the loading screen texture.
### Arguments

- *int* **progress** - Progress of alpha blending between 2 screens stored in the texture. The value in range **[0;100]** sets an alpha channel threshold, according to which pixels from the *initial* (opaque) or *final* (transparent) screen in the texture are rendered. By the value of **0**, the initial screen is loaded. By the value of **100**, the final screen is loaded.

## void render ( int progress , const char * message )

Renders a custom loading screen in a given progress state and prints a given message. Use this function in a loop to create a gradual change between the initial (upper opaque part) and the final states (bottom transparent part) of the loading screen texture, while printing a custom loading stage.
### Arguments

- *int* **progress** - Progress of alpha blending between 2 loading screens stored in the texture. The value in range **[0;100]** sets an alpha channel threshold, according to which pixels from the *initial* (opaque) or *final* (transparent) loading screen in the texture are rendered. By the value of **0**, the initial screen is loaded. By the value of **100**, the final screen is loaded.
- *const char ** **message** - message to print representing the loading stage.

## void renderForce ( )

Renders the loading screen regardless of whether the manual rendering is allowed or not.
## void renderForce ( const char * message )

Renders the loading screen regardless of whether the manual rendering is allowed or not and prints a given message.
### Arguments

- *const char ** **message** - message to print that represents the loading stage.
