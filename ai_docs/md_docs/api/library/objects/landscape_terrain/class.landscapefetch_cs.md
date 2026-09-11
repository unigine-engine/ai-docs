# Unigine.LandscapeFetch Class (CS)


This class is used to [fetch](#fetchForce_int) data of the [Landscape Terrain Object](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md) at a certain point (e.g. a height request) or check for an [intersection](#intersectionForce_int) with a traced line. The following performance optimizations are available:


- For each request you can engage or disengage certain data types (albedo, heights, masks, etc.). When the data type is engaged, you can obtain information via the corresponding  *property*. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
- Both fetch and intersection requests can be performed [asynchronously](#example_async) when an instant result is not required.


The workflow is as follows:


1. Create a new *LandscapeFetch* object instance.
2. Set necessary parameters (e.g. which data layers are to be used, whether to enable holes or not, etc.).
3. To get terrain data for a certain point call the **[FetchForce()](../../../...md#fetchForce_int)** method providing coordinates for the desired point. > **Notice:** You can also fetch terrain data asynchronously via the **[FetchAsync()](../../../...md#fetchAsync_int_void)** method.
4. To find an intersection of a traced line with the terrain call either the **[IntersectionForce()](../../../...md#intersectionForce_int)** method or the **[IntersectionAsync()](../../../...md#intersectionAsync_int_void)** method, if you want to perform an asynchronous request.


### Usage Example


```csharp
#if UNIGINE_DOUBLE
using Vec2 = Unigine.dvec2;
using Scalar = System.Double;
#else
	using Vec2 = Unigine.vec2;
	using Scalar = System.Single;
#endif

// ...

// creating a fetch object and setting necessary parameters
landscape_fetch = new LandscapeFetch();

// disengage all terrain data types to enable only the necessary ones
landscape_fetch.Uses = 0;

// enable checking for height data in fetch/intersection requests, if necessary
landscape_fetch.UsesHeight = true;
// enable checking for normals data in fetch/intersection requests, if necessary
landscape_fetch.UsesNormal = true;

// enable checking for terrain holes in fetch requests, if necessary
landscape_fetch.HolesEnabled = true;

// enable checking for necessary masks (e.g. first and second) in fetch/intersection requests, if necessary
landscape_fetch.SetUsesMask(0, true);
landscape_fetch.SetUsesMask(1, true);

// ...

// getting terrain data for a point at (100, 100) and printing the height value
landscape_fetch.FetchPosition = new Vec2(100, 100);
if (landscape_fetch.FetchForce())
	Log.Message("Terrain height at the specified point is: {0}", landscape_fetch.Height);

```


### Asynchronous Operations Example


```csharp
#if UNIGINE_DOUBLE
using Vec2 = Unigine.dvec2;
using Scalar = System.Double;
#else
	using Vec2 = Unigine.vec2;
	using Scalar = System.Single;
#endif

// ...

// creating a fetch object and setting necessary parameters
landscape_fetch = new LandscapeFetch();

// disengage all terrain data types to enable only the necessary ones
landscape_fetch.Uses = 0;
// enable checking for height data in fetch/intersection requests, if necessary
landscape_fetch.UsesHeight = true;
// enable checking for terrain holes in fetch requests, if necessary
landscape_fetch.HolesEnabled = true;

// ...

// making an asynchronous fetch request for a point at (2.05, 2.05)
landscape_fetch.FetchPosition =new Vec2(2.05f, 2.05f);
landscape_fetch.FetchAsync();

// ...

// checking if our asynchronous fetch request is completed and printing the height value
if (landscape_fetch.IsAsyncCompleted) {
		Log.Message("Terrain height at the specified point is: {0}", landscape_fetch.Height);
}

```


### Sample Component


<details>
<summary>TerrainFetchSample.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class TerrainFetchSample : Component
{
	void Init()
	{
		// check if a node to which the component is assigned is s player
		player = node as Player;
		if (!player)
			Log.Error("TerrainFetchSample::Init(): TerrainFetchSample must be assigned to a player node!\n");

		// turn the Visualizer on
		Visualizer.Enabled = true;

		// create a LandscapeFetch class instance
		fetch = new LandscapeFetch();

		// indicate that we're going to use height and normals data
		fetch.UsesHeight = true;
		fetch.UsesNormal = true;

		// indicate that we're going to use mask layers from 0 to 3
		fetch.SetUsesMask(0, true);
		fetch.SetUsesMask(1, true);
		fetch.SetUsesMask(2, true);
		fetch.SetUsesMask(3, true);
	}

	void Update()
	{
		dvec3 p0, p1;

		var main_window = WindowManager.MainWindow;
		var mouse = Input.MousePosition;
		// get a direction vector to which the mouse cursor points
		player.GetDirectionFromMainWindow(out p0, out p1, mouse.x, mouse.y);
		// get an intersection point between the direction vector and the terrain surface (point under the mouse cursor)
		fetch.IntersectionForce(p0, p0 + ((p1 - p0) * 1000.0f));

		// if there is an intersection found
		if (fetch.IsIntersection)
		{
			// get fetched data and a landscape terrain that is currently active
			var position = fetch.Position;
			var height = fetch.Height;
			var normal = fetch.Normal;
			var terrain = Landscape.GetActiveTerrain();

			// render a normal and 'Up' vector at the intersection point
			Visualizer.RenderVector(position, position + vec3.UP * 10, vec4.BLUE);
			Visualizer.RenderVector(position, position + normal * 10, vec4.RED);
			Visualizer.RenderSolidSphere(1, MathLib.Translate(position), vec4.BLACK);

			// print terrain height value at the point
			var text = new string("");
			text += string.Format($"height: {height}\n");

			// get names and indices of masks under the cursor
			for (var i = 0; i < 4; i += 1)
			{
				text += string.Format($"\"{terrain.GetDetailMask(i).Name}\": {fetch.GetMask(i)}\n");
			}

			// print the text at the intersectin point
			Visualizer.RenderMessage3D(position, new vec3(1, 1, 0), text, vec4.GREEN, 1);
		}
	}

	void Shutdown()
	{
		Visualizer.Enabled = false;
	}

	private Player player;
	private LandscapeFetch fetch;
}

```

</details>


### See also


- C++ sample
- C++ sample


## LandscapeFetch Class

### Properties

## 🔒︎ vec3 Position

The coordinates of the fetch/intersection point.
## 🔒︎ float Height

The height value at the point.
## 🔒︎ vec3 Normal

The normal vector coordinates at the point.
> **Notice:** To get valid normal information via this method, [engage normal data](#setUsesNormal_int_void) for the fetch/intersection request.


## 🔒︎ vec4 Albedo

The albedo color information at the point.
> **Notice:** To get valid albedo color information via this method, [engage albedo data](#setUsesAlbedo_int_void) for the fetch/intersection request.


## 🔒︎ bool IsIntersection

The value indicating if an intersection was detected.
## int Uses

The flags engaging/disengaging certain data types for the fetch/intersection request.
## bool UsesHeight

The value indicating if heights data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point). This option is enabled by default.
## bool UsesNormal

The value indicating if normals data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [normal](#getNormal_vec3) information for the point.


## bool UsesAlbedo

The value indicating if albedo data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [albedo](#getAlbedo_vec4) information for the point.


## float IntersectionPrecision

The precision value used for intersection detection requested by [*intersectionForce()*](#intersectionForce_int) and [*intersectionAsync()*](#intersectionAsync_int_void) methods.
## vec3 IntersectionPositionBegin

The coordinates of the starting point for intersection detection.
## vec3 IntersectionPositionEnd

The coordinates of the end point for intersection detection.
## vec2 FetchPosition

The point for which terrain data is to be fetched.
## 🔒︎ bool IsAsyncCompleted

The value indicating if async operation is completed. As the operation is completed you can obtain necessary data via *get*()* methods.
## bool HolesEnabled

The value indicating if checking for terrain holes in the fetch/intersection request is enabled. This option is enabled by default. When disabled terrain holes created using decals are ignored.
## 🔒︎ Event EventEnd

The Event triggered on fetch completion. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

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

## 🔒︎ Event EventStart

The Event triggered at the beginning of the fetch process. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Start event handler
void start_event_handler()
{
	Log.Message("\Handling Start event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections start_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventStart.Connect(start_event_connections, start_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventStart.Connect(start_event_connections, () => {
		Log.Message("Handling Start event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
start_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Start event with a handler function
publisher.EventStart.Connect(start_event_handler);

// remove subscription to the Start event later by the handler function
publisher.EventStart.Disconnect(start_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection start_event_connection;

// subscribe to the Start event with a lambda handler function and keeping the connection
start_event_connection = publisher.EventStart.Connect(() => {
		Log.Message("Handling Start event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
start_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
start_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
start_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Start events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventStart.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventStart.Enabled = true;

```

</details>

### Members

---

## LandscapeFetch ( )

The LandscapeFetch constructor.
## float GetMask ( int num )

Returns information stored for the point in the detail mask with the specified number.
> **Notice:** To get valid detail mask information via this method, [engage mask data](#setUsesMask_int_int_void) for the fetch/intersection request.


### Arguments

- *int* **num** - Number of the detail mask in the **[0; 19]** range.

### Return value

Value for the point stored in the detail mask with the specified number.
## void SetUsesMask ( int num , bool value )

Sets a value indicating if data of the specified detail mask is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [detail mask](#getMask_int_float) data for the point.


### Arguments

- *int* **num** - Detail mask number in the **[0; 19]** range.
- *bool* **value** - true to engage data of the specified detail mask in the fetch/intersection request, false - to disengage.

## bool IsUsesMask ( int num )

Returns a value indicating if data of the specified detail mask is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [detail mask](#getMask_int_float) data for the point.


### Arguments

- *int* **num** - Detail mask number in the **[0; 19]** range.

### Return value

true if data of the specified detail mask is engaged in the fetch/intersection request; otherwise, false.
## bool FetchForce ( )

Fetches terrain data in forced mode for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void). You can use the [*fetchAsync()*](#fetchAsync_int_void) method to reduce load, when an instant result is not required.
### Return value

true if terrain data was successfully obtained for the specified point; otherwise, false.
## bool FetchForce ( vec2 position )

Fetches terrain data in forced mode for the specified point. You can use the [*fetchAsync()*](#fetchAsync_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *vec2* **position** - Coordinates of the point.

### Return value

true if terrain data was successfully obtained for the specified point; otherwise, false.
## bool IntersectionForce ( )

Performs tracing along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in forced mode. You can use the [*intersectionAsync()*](#intersectionAsync_int_void) method to reduce load, when an instant result is not required.
### Return value

true if an intersection with the terrain was found; otherwise, false.
## bool IntersectionForce ( vec3 p0 , vec3 p1 )

Performs tracing along the line from the **p0** point to the **p1** point to find an intersection with the terrain in forced mode. You can use the [*intersectionAsync()*](#intersectionAsync_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *vec3* **p0** - Coordinates of the **p0** point.
- *vec3* **p1** - Coordinates of the **p1** point.

### Return value

true if an intersection with the terrain was found; otherwise, false.
## void FetchAsync ( bool critical = false )

Fetches terrain data for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void) in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*fetchForce()*](#fetchForce_int) method.
### Arguments

- *bool* **critical** - true to set high priority for the fetch task, false - to set normal priority.

## void FetchAsync ( vec2 position , bool critical = false )

Fetches terrain data for the specified point in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*fetchForce()*](#fetchForce_int) method.
### Arguments

- *vec2* **position** - Coordinates of the point.
- *bool* **critical** - true to set high priority for the fetch task, false - to set normal priority.

## void IntersectionAsync ( bool critical = false )

Performs tracing along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*intersectionForce()*](#intersectionForce_int) method.
### Arguments

- *bool* **critical** - true to set high priority for the intersection task, false - to set normal priority.

## void IntersectionAsync ( vec3 p0 , vec3 p1 , bool critical = false )

Performs tracing along the line from the **p0** point to the **p1** point to find an intersection with the terrain in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*intersectionForce()*](#intersectionForce_int) method.
### Arguments

- *vec3* **p0** - Coordinates of the **p0** point.
- *vec3* **p1** - Coordinates of the **p1** point.
- *bool* **critical** - true to set high priority for the intersection task, false - to set normal priority.

## void FetchForce ( LandscapeFetch [] fetches )

Fetches (batch) terrain data in forced mode for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void). You can use the [*fetchAsync()*](#fetchAsync_VECLandscapeFetch_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cs.md)[]* **fetches** - List of fetch requests to be completed.

## void IntersectionForce ( LandscapeFetch [] fetches )

Performs tracing (batch) along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in forced mode. You can use the [*intersectionAsync()*](#intersectionAsync_VECLandscapeFetch_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cs.md)[]* **fetches** - List of fetch requests to be completed.

## void FetchAsync ( LandscapeFetch [] fetches , bool critical = false )

Fetches (batch) terrain data for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void) in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_VECLandscapeFetch_void) method). For an instant result use the [*fetchForce()*](#fetchForce_VECLandscapeFetch_void) method.
### Arguments

- *[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cs.md)[]* **fetches** - List of fetch requests to be completed.
- *bool* **critical** - true to set high priority for the fetch task, false - to set normal priority.

## void IntersectionAsync ( LandscapeFetch [] fetches , bool critical = false )

Performs tracing (batch) along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_VECLandscapeFetch_void) method). For an instant result use the [*intersectionForce()*](#intersectionForce_VECLandscapeFetch_void) method.
### Arguments

- *[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cs.md)[]* **fetches** - List of fetch requests to be completed.
- *bool* **critical** - true to set high priority for the intersection task, false - to set normal priority.

## void Wait ( )

Waits for completion of the fetch operation. As the operation is completed you can obtain necessary data via *get*()* methods.
## void Wait ( LandscapeFetch [] fetches )

Waits for completion of the specified fetch operations. As the operations are completed you can obtain necessary data via *get*()* methods.
### Arguments

- *[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cs.md)[]* **fetches** - List of fetch requests to be completed.
