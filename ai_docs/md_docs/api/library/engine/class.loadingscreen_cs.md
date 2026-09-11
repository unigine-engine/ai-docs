# Unigine.LoadingScreen Class (CS)

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


```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Reflection;
using System.Runtime.InteropServices;
using System.Text;
using Unigine;

namespace UnigineApp
{
	internal class AppSystemLogic : SystemLogic
	{

		public override bool Init()
		{

			// get the size of the main window
			EngineWindow main_window = WindowManager.MainWindow;
			if (!main_window)
			{
				Engine.Quit();
				return false;
			}

			ivec2 main_size = main_window.Size;

			// define new transform for loading screen texture
			vec4 transform = new vec4(1.0f, 1.0f, 0.0f, 0.0f);

			// enable the loading screen
			LoadingScreen.Enabled = true;

			// set transform to the loading screen texture
			LoadingScreen.Transform = transform;

			// compute the aspect ratio to show corresponding texture
			float aspect_ratio = (float)main_size.x / (float)main_size.y;

			// if the aspect ratio is 4:3 show the following loading screen
			// during world loading
			if (aspect_ratio < 1.5f)
			{
				LoadingScreen.TexturePath = "textures/splash_4x3.png";
			}
			else
			{
				// if the aspect ratio is 16:9 show this loading screen
				// during world loading
				LoadingScreen.TexturePath = "textures/splash_16x9.png";
			}

			// set the text to be displayed on the loading screen
			// with a certain displacement along the X and Y axes
			LoadingScreen.Text = "<xy x=\"%50\" dx=\"0\" y=\"%50\" dy=\"0\"/>LOADING_PROGRESS";

			// set duration (in milliseconds) and display the loading screen on world loading
			int duration = 5;
			DateTime begin = DateTime.Now;

			while (DateTime.Now.Subtract(begin).TotalSeconds < duration)
				LoadingScreen.Render((int)(DateTime.Now.Subtract(begin).TotalSeconds / duration * 100.0f));

			// disable the loading screen
			LoadingScreen.Enabled = false;

			return true;
		}

	}
}


```


A loading screen defined in the *Init()* method of the [World Logic](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic) will be shown right after a world is loaded:


```csharp
private void Init()
{

	// enable the loading screen
	LoadingScreen.Enabled = true;

	// set the text to be displayed on the loading screen,
	// specifying a color, a font, and a certain displacement along the X and Y axes
	LoadingScreen.Text = "<p align=\"center\"><font size=\"20\" color=\"#FF0000FF\">CUSTOM LOADING TEXT</font></p>";

	// set duration (in seconds) and display the loading screen on world loading
	int duration = 5;
	DateTime begin = DateTime.Now;

	while (DateTime.Now.Subtract(begin).TotalSeconds < duration)
		LoadingScreen.Render((int)(DateTime.Now.Subtract(begin).TotalSeconds / duration * 100.0f));

	// disable the loading screen
	LoadingScreen.Enabled = false;
}


```


## LoadingScreen Class

### Properties

## 🔒︎ string Message

The text message representing the current loading stage.
## 🔒︎ int Progress

The progress state.
## string MessageShadersCompilation

The message displayed on shaders compilation. The text [aliases](#setText_cstr_void) are also supported.
## string MessageLoadingWorld

The message displayed on world loading. The text [aliases](#setText_cstr_void) are also supported.
## string FontPath

The path to the font used to render the text.
## string Text

The text of the loading screen.
## vec4 BackgroundColor

The background color of the loading screen.
## vec4 Transform

The transformation of the loading screen texture.
## string TexturePath

The path to the texture for the loading screen.
## int Threshold

The amount of blur in the alpha channel when interpolating between states of the loading screen.
> **Notice:** By default, the Threshold value is set to 16.


## bool Enabled

The value indicating if manual rendering of a loading screen is allowed.
> **Notice:** Enabling manual rendering is possible only together with the corresponding **render** functions (*[render()](#render_void)*). It cannot be used to enable or disable rendering of the loading screen during the initialization stage of the engine.


## 🔒︎ Event EventRenderEnd

The event triggered when rendering of the loading screen ends. The function is useful when you implement a custom loading screen rendering function, for example. The event handler must not take arguments. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the RenderEnd event handler
void renderend_event_handler()
{
	Log.Message("\Handling RenderEnd event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections renderend_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
LoadingScreen.EventRenderEnd.Connect(renderend_event_connections, renderend_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
LoadingScreen.EventRenderEnd.Connect(renderend_event_connections, () => {
		Log.Message("Handling RenderEnd event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
renderend_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the RenderEnd event with a handler function
LoadingScreen.EventRenderEnd.Connect(renderend_event_handler);

// remove subscription to the RenderEnd event later by the handler function
LoadingScreen.EventRenderEnd.Disconnect(renderend_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection renderend_event_connection;

// subscribe to the RenderEnd event with a lambda handler function and keeping the connection
renderend_event_connection = LoadingScreen.EventRenderEnd.Connect(() => {
		Log.Message("Handling RenderEnd event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
renderend_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
renderend_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
renderend_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring RenderEnd events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
LoadingScreen.EventRenderEnd.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
LoadingScreen.EventRenderEnd.Enabled = true;

```

</details>

## 🔒︎ Event EventRenderBegin

The event triggered when rendering of the loading screen begins. The function is useful when you implement a custom loading screen rendering function, for example. The event handler must not take arguments. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the RenderBegin event handler
void renderbegin_event_handler()
{
	Log.Message("\Handling RenderBegin event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections renderbegin_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
LoadingScreen.EventRenderBegin.Connect(renderbegin_event_connections, renderbegin_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
LoadingScreen.EventRenderBegin.Connect(renderbegin_event_connections, () => {
		Log.Message("Handling RenderBegin event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
renderbegin_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the RenderBegin event with a handler function
LoadingScreen.EventRenderBegin.Connect(renderbegin_event_handler);

// remove subscription to the RenderBegin event later by the handler function
LoadingScreen.EventRenderBegin.Disconnect(renderbegin_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection renderbegin_event_connection;

// subscribe to the RenderBegin event with a lambda handler function and keeping the connection
renderbegin_event_connection = LoadingScreen.EventRenderBegin.Connect(() => {
		Log.Message("Handling RenderBegin event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
renderbegin_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
renderbegin_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
renderbegin_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring RenderBegin events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
LoadingScreen.EventRenderBegin.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
LoadingScreen.EventRenderBegin.Enabled = true;

```

</details>

### Members

---

## void SetImage ( Image image )

Sets an [image](../../../code/gui/skin/index.md#splash) for a custom loading screen.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to be used as a custom loading screen.

## void GetImage ( Image image )

Returns the current [image](../../../code/gui/skin/index.md#splash) for a custom loading screen.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image**

## void RenderInterface ( )

Renders a static loading screen. Such a screen does not display any progress.
## void Render ( )

Renders the loading screen in the current progress state and with the current stage message.
## void Render ( int progress )

Renders a custom loading screen in a given progress state. Use this function in a loop to create a gradual change between the initial (upper opaque part) and the final states (bottom transparent part) of the loading screen texture.
### Arguments

- *int* **progress** - Progress of alpha blending between 2 screens stored in the texture. The value in range **[0;100]** sets an alpha channel threshold, according to which pixels from the *initial* (opaque) or *final* (transparent) screen in the texture are rendered. By the value of **0**, the initial screen is loaded. By the value of **100**, the final screen is loaded.

## void Render ( int progress , string message )

Renders a custom loading screen in a given progress state and prints a given message. Use this function in a loop to create a gradual change between the initial (upper opaque part) and the final states (bottom transparent part) of the loading screen texture, while printing a custom loading stage.
### Arguments

- *int* **progress** - Progress of alpha blending between 2 loading screens stored in the texture. The value in range **[0;100]** sets an alpha channel threshold, according to which pixels from the *initial* (opaque) or *final* (transparent) loading screen in the texture are rendered. By the value of **0**, the initial screen is loaded. By the value of **100**, the final screen is loaded.
- *string* **message** - message to print representing the loading stage.

## void RenderForce ( )

Renders the loading screen regardless of whether the manual rendering is allowed or not.
## void RenderForce ( string message )

Renders the loading screen regardless of whether the manual rendering is allowed or not and prints a given message.
### Arguments

- *string* **message** - message to print that represents the loading stage.
