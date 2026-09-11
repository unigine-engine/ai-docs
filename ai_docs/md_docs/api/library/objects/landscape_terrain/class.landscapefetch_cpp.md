# Unigine.LandscapeFetch Class (CPP)

**Header:** #include <UnigineObjects.h>


This class is used to [fetch](#fetchForce_int) data of the [Landscape Terrain Object](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md) at a certain point (e.g. a height request) or check for an [intersection](#intersectionForce_int) with a traced line. The following performance optimizations are available:


- For each request you can engage or disengage certain data types (albedo, heights, masks, etc.). When the data type is engaged, you can obtain information via the corresponding *get()* *method*. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
- Both fetch and intersection requests can be performed [asynchronously](#example_async) when an instant result is not required.


The workflow is as follows:


1. Create a new *LandscapeFetch* object instance.
2. Set necessary parameters (e.g. which data layers are to be used, whether to enable holes or not, etc.).
3. To get terrain data for a certain point call the **[fetchForce()](../../../...md#fetchForce_int)** method providing coordinates for the desired point. > **Notice:** You can also fetch terrain data asynchronously via the **[fetchAsync()](../../../...md#fetchAsync_int_void)** method.
4. To find an intersection of a traced line with the terrain call either the **[intersectionForce()](../../../...md#intersectionForce_int)** method or the **[intersectionAsync()](../../../...md#intersectionAsync_int_void)** method, if you want to perform an asynchronous request.


### Usage Example


```cpp
// creating a fetch object and setting necessary parameters
LandscapeFetchPtr landscape_fetch = LandscapeFetch::create();

// disengage all terrain data types to enable only the necessary ones
landscape_fetch->setUses(0);

// enable checking for height data in fetch/intersection requests, if necessary
landscape_fetch->setUsesHeight(true);
// enable checking for normals data in fetch/intersection requests, if necessary
landscape_fetch->setUsesNormal(true);

// enable checking for terrain holes in fetch/intersection requests, if necessary
landscape_fetch->setHolesEnabled(true);

// enable checking for necessary masks (e.g. first and second) in fetch/intersection requests, if necessary
landscape_fetch->setUsesMask(0, true);
landscape_fetch->setUsesMask(1, true);

// ...

// getting terrain data for a point at (100, 100) and printing the height value
landscape_fetch->setFetchPosition(Vec2(100, 100));
if (landscape_fetch->fetchForce())
	Log::message("Terrain height at the specified point is: %f", Scalar(landscape_fetch->getHeight()));

```


### Asynchronous Operations Example


```cpp
// creating a fetch object and setting necessary parameters
LandscapeFetchPtr landscape_fetch = LandscapeFetch::create();
// disengage all terrain data types to enable only the necessary ones
landscape_fetch->setUses(0);
// enable checking for height data in fetch/intersection requests, if necessary
landscape_fetch->setUsesHeight(true);
// enable checking for terrain holes in fetch requests, if necessary
landscape_fetch->setHolesEnabled(true);

// ...

// making an asynchronous fetch request for a point at (2.05, 2.05)
landscape_fetch->setFetchPosition(Vec2(2.05f, 2.05f));
landscape_fetch->fetchAsync();

// ...

// checking if our asynchronous fetch request is completed and printing the height value
if (landscape_fetch->isAsyncCompleted())
		Log::message("Terrain height at the specified point is: %f", Scalar(landscape_fetch->getHeight()));

```


### Sample Component


<details>
<summary>TerrainFetchSample.h | Close</summary>

```cpp
#pragma once
#include <UnigineVector.h>
#include <UniginePlayers.h>
#include <UnigineComponentSystem.h>

class TerrainFetchSample : public Unigine::ComponentBase
{
public:
	COMPONENT(TerrainFetchSample, ComponentBase)
	COMPONENT_INIT(init)
	COMPONENT_UPDATE(update)
	COMPONENT_SHUTDOWN(shutdown)

	PROP_NAME("TerrainFetchSample")

private:
	void init();
	void update();
	void shutdown();

	// declare the main player and LandscapeFetch class instance to be used to retrieve terrain data
	Unigine::PlayerPtr main_player;
	Unigine::LandscapeFetchPtr fetch;
};

```

</details>


<details>
<summary>TerrainFetchSample.cpp | Close</summary>

```cpp
#include "TerrainFetchSample.h"
#include <UnigineVisualizer.h>

using namespace Unigine;
using namespace Math;

REGISTER_COMPONENT(TerrainFetchSample)

void TerrainFetchSample::init()
{
	// check if a node to which the component is assigned is s player
	main_player = checked_ptr_cast<Player>(node);
	if (!main_player)
		Log::error("TerrainFetchSample::init(): TerrainFetchSample must be assigned to a player node!\n");

	// turn the Visualizer on
	Visualizer::setEnabled(1);
}

void TerrainFetchSample::update()
{
	if (!main_player)
		return;

	Vec3 p0, p1;
	// get the main application window and mouse position
	const auto main_window = WindowManager::getMainWindow();
	const auto mouse_coord = Input::getMousePosition();

	// get a direction vector to which the mouse cursor points
	main_player->getDirectionFromMainWindow(p0, p1, mouse_coord.x, mouse_coord.y);

	if (!fetch)
	{
		// create fetch
		fetch = LandscapeFetch::create();

		// indicate that we're going to use height, albedo, and normals data
		fetch->setUsesHeight(true);
		fetch->setUsesNormal(true);
		fetch->setUsesAlbedo(true);

		// indicate that we're going to use mask layers from 0 to 3
		fetch->setUsesMask(0, true);
		fetch->setUsesMask(1, true);
		fetch->setUsesMask(2, true);
		fetch->setUsesMask(3, true);

		// get an intersection point between the direction vector and the terrain surface (point under the mouse cursor) asynchronously
		fetch->intersectionAsync(p0, p0 + ((p1 - p0) * 1000.0));
	}
	else
	{
		// checking if the async task is completed
		if (fetch->isAsyncCompleted())
		{
			// if there is an intersection found
			if (fetch->isIntersection())
			{
				// get fetched data and a landscape terrain that is currently active
				Vec3 point = fetch->getPosition();
				auto terrain = Landscape::getActiveTerrain();

				// render a normal and 'Up' vector at the intersection point
				Visualizer::renderVector(point, point + Vec3_up * 10, vec4_blue);
				Visualizer::renderVector(point, point + Vec3(fetch->getNormal() * 10), vec4_red);
				Visualizer::renderSolidSphere(1, translate(point), vec4_black);

				// print terrain height value at the point
				String string;
				string += String::format("Height : %f\n", fetch->getHeight());

				// add names and indices of masks under the cursor
				string += "Masks: \n";
				for (int i = 0; i < 4; i++)
				{
					string += String::format(" - \"%s\": %.2f\n", terrain->getDetailMask(i)->getName(), fetch->getMask(i));
				}
				// print the text at the intersectin point
				Visualizer::renderMessage3D(point, vec3(1, 1, 0), string.get(), vec4_green, 1);
			}
			else
			{
				// print a message indicating that we're pointing somwhere out of terrain
				Visualizer::renderMessage3D(p1, vec3(1, 1, 0), "Out of terrain", vec4_red, 1);
			}
			// get an intersection point between the direction vector and the terrain surface (point under the mouse cursor) asynchronously
			fetch->intersectionAsync(p0, p0 + ((p1 - p0) * 1000.0));
		}
	}
}

void TerrainFetchSample::shutdown()
{
	// do some cleanup
	fetch = nullptr;
}


```

</details>


### See also


- C++ sample
- C++ sample


## LandscapeFetch Class

### Members

## Math:: Vec3 getPosition () const

Returns the current coordinates of the fetch/intersection point.
### Return value

Current fetch/intersection point coordinates as a three-component vector.
## float getHeight () const

Returns the current height value at the point.
### Return value

Current height value at the point.
## Math:: vec3 getNormal () const

Returns the current normal vector coordinates at the point.
> **Notice:** To get valid normal information via this method, [engage normal data](#setUsesNormal_int_void) for the fetch/intersection request.


### Return value

Current normal vector coordinates at the point.
## Math:: vec4 getAlbedo () const

Returns the current albedo color information at the point.
> **Notice:** To get valid albedo color information via this method, [engage albedo data](#setUsesAlbedo_int_void) for the fetch/intersection request.


### Return value

Current albedo color at the point as a 4 component vector (R, G, B, A).
## bool isIntersection () const

Returns the current value indicating if an intersection was detected.
### Return value

**true** if an intersection was detected; otherwise **false**.
## void setUses ( int uses )

Sets a new flags engaging/disengaging certain data types for the fetch/intersection request.
### Arguments

- *int* **uses** - The combination of data engagement flags.

## int getUses () const

Returns the current flags engaging/disengaging certain data types for the fetch/intersection request.
### Return value

Current combination of data engagement flags.
## void setUsesHeight ( bool height )

Sets a new value indicating if heights data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point). This option is enabled by default.
### Arguments

- *bool* **height** - Set **true** to enable engagement of height data in the fetch/intersection request; **false** - to disable it.

## bool isUsesHeight () const

Returns the current value indicating if heights data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point). This option is enabled by default.
### Return value

**true** if engagement of height data in the fetch/intersection request is enabled ; otherwise **false**.
## void setUsesNormal ( bool normal )

Sets a new value indicating if normals data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [normal](#getNormal_vec3) information for the point.


### Arguments

- *bool* **normal** - Set **true** to enable engagement of normals data in the fetch/intersection request; **false** - to disable it.

## bool isUsesNormal () const

Returns the current value indicating if normals data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [normal](#getNormal_vec3) information for the point.


### Return value

**true** if engagement of normals data in the fetch/intersection request is enabled ; otherwise **false**.
## void setUsesAlbedo ( bool albedo )

Sets a new value indicating if albedo data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [albedo](#getAlbedo_vec4) information for the point.


### Arguments

- *bool* **albedo** - Set **true** to enable engagement of albedo data in the fetch/intersection request; **false** - to disable it.

## bool isUsesAlbedo () const

Returns the current value indicating if albedo data is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [albedo](#getAlbedo_vec4) information for the point.


### Return value

**true** if engagement of albedo data in the fetch/intersection request is enabled ; otherwise **false**.
## void setIntersectionPrecision ( float precision )

Sets a new precision value used for intersection detection requested by [*intersectionForce()*](#intersectionForce_int) and [*intersectionAsync()*](#intersectionAsync_int_void) methods.
### Arguments

- *float* **precision** - The precision for intersection detection as a fraction of maximum precision in the [0; 1] range. The default value is 0.5f. Maximum precision is determined by the Engine on the basis of the data of your Landscape Terrain.

## float getIntersectionPrecision () const

Returns the current precision value used for intersection detection requested by [*intersectionForce()*](#intersectionForce_int) and [*intersectionAsync()*](#intersectionAsync_int_void) methods.
### Return value

Current precision for intersection detection as a fraction of maximum precision in the [0; 1] range. The default value is 0.5f. Maximum precision is determined by the Engine on the basis of the data of your Landscape Terrain.
## void setIntersectionPositionBegin ( const Math:: Vec3 & begin )

Sets a new coordinates of the starting point for intersection detection.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md)&* **begin** - The three-component vector specifying starting point coordinates along X, Y, and Z axes.

## Math:: Vec3 getIntersectionPositionBegin () const

Returns the current coordinates of the starting point for intersection detection.
### Return value

Current three-component vector specifying starting point coordinates along X, Y, and Z axes.
## void setIntersectionPositionEnd ( const Math:: Vec3 & end )

Sets a new coordinates of the end point for intersection detection.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md)&* **end** - The three-component vector specifying end point coordinates along X, Y, and Z axes.

## Math:: Vec3 getIntersectionPositionEnd () const

Returns the current coordinates of the end point for intersection detection.
### Return value

Current three-component vector specifying end point coordinates along X, Y, and Z axes.
## void setFetchPosition ( const Math:: Vec2 & position )

Sets a new point for which terrain data is to be fetched.
### Arguments

- *const  Math::[Vec2](../../../../api/library/math/class.vec2_cpp.md)&* **position** - The two-component vector specifying point coordinates along X and Y axes.

## Math:: Vec2 getFetchPosition () const

Returns the current point for which terrain data is to be fetched.
### Return value

Current two-component vector specifying point coordinates along X and Y axes.
## bool isAsyncCompleted () const

Returns the current value indicating if async operation is completed. As the operation is completed you can obtain necessary data via *get*()* methods.
### Return value

**true** if async operation is completed; otherwise **false**.
## void setHolesEnabled ( bool enabled )

Sets a new value indicating if checking for terrain holes in the fetch/intersection request is enabled. This option is enabled by default. When disabled terrain holes created using decals are ignored.
### Arguments

- *bool* **enabled** - Set **true** to enable checking for terrain holes in the fetch/intersection request; **false** - to disable it.

## bool isHolesEnabled () const

Returns the current value indicating if checking for terrain holes in the fetch/intersection request is enabled. This option is enabled by default. When disabled terrain holes created using decals are ignored.
### Return value

**true** if checking for terrain holes in the fetch/intersection request is enabled ; otherwise **false**.
## Event<> getEventEnd () const

Event triggered on fetch completion. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

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
## Event<> getEventStart () const

Event triggered at the beginning of the fetch process. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Start event handler
void start_event_handler()
{
	Log::message("\Handling Start event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections start_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventStart().connect(start_event_connections, start_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventStart().connect(start_event_connections, []() {
		Log::message("\Handling Start event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
start_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection start_event_connection;

// subscribe to the Start event with a handler function keeping the connection
publisher->getEventStart().connect(start_event_connection, start_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
start_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
start_event_connection.setEnabled(true);

// ...

// remove subscription to the Start event via the connection
start_event_connection.disconnect();

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

	// A Start event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Start event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventStart().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId start_handler_id;

// subscribe to the Start event with a lambda handler function and keeping connection ID
start_handler_id = publisher->getEventStart().connect(e_connections, []() {
		Log::message("\Handling Start event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventStart().disconnect(start_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Start events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventStart().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventStart().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static LandscapeFetchPtr create ( )

The LandscapeFetch constructor.
## float getMask ( int num ) const

Returns information stored for the point in the detail mask with the specified number.
> **Notice:** To get valid detail mask information via this method, [engage mask data](#setUsesMask_int_int_void) for the fetch/intersection request.


### Arguments

- *int* **num** - Number of the detail mask in the **[0; 19]** range.

### Return value

Value for the point stored in the detail mask with the specified number.
## void setUsesMask ( int num , bool value )

Sets a value indicating if data of the specified detail mask is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [detail mask](#getMask_int_float) data for the point.


### Arguments

- *int* **num** - Detail mask number in the **[0; 19]** range.
- *bool* **value** - true to engage data of the specified detail mask in the fetch/intersection request, false - to disengage.

## bool isUsesMask ( int num ) const

Returns a value indicating if data of the specified detail mask is engaged in the fetch/intersection request. When the data type is engaged, you can obtain it via the corresponding *get()* method. Disengaging unnecessary data when performing requests saves some performance (e.g., you can engage albedo data only if you need only color information at a certain point).
> **Notice:** Enable this option to get [detail mask](#getMask_int_float) data for the point.


### Arguments

- *int* **num** - Detail mask number in the **[0; 19]** range.

### Return value

true if data of the specified detail mask is engaged in the fetch/intersection request; otherwise, false.
## bool fetchForce ( )

Fetches terrain data in forced mode for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void). You can use the [*fetchAsync()*](#fetchAsync_int_void) method to reduce load, when an instant result is not required.
### Return value

true if terrain data was successfully obtained for the specified point; otherwise, false.
## bool fetchForce ( const Math:: Vec2 & position )

Fetches terrain data in forced mode for the specified point. You can use the [*fetchAsync()*](#fetchAsync_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *const  Math::[Vec2](../../../../api/library/math/class.vec2_cpp.md) &* **position** - Coordinates of the point.

### Return value

true if terrain data was successfully obtained for the specified point; otherwise, false.
## bool intersectionForce ( )

Performs tracing along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in forced mode. You can use the [*intersectionAsync()*](#intersectionAsync_int_void) method to reduce load, when an instant result is not required.
### Return value

true if an intersection with the terrain was found; otherwise, false.
## bool intersectionForce ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 )

Performs tracing along the line from the **p0** point to the **p1** point to find an intersection with the terrain in forced mode. You can use the [*intersectionAsync()*](#intersectionAsync_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - Coordinates of the **p0** point.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - Coordinates of the **p1** point.

### Return value

true if an intersection with the terrain was found; otherwise, false.
## void fetchAsync ( bool critical = false )

Fetches terrain data for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void) in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*fetchForce()*](#fetchForce_int) method.
### Arguments

- *bool* **critical** - true to set high priority for the fetch task, false - to set normal priority.

## void fetchAsync ( const Math:: Vec2 & position , bool critical = false )

Fetches terrain data for the specified point in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*fetchForce()*](#fetchForce_int) method.
### Arguments

- *const  Math::[Vec2](../../../../api/library/math/class.vec2_cpp.md) &* **position** - Coordinates of the point.
- *bool* **critical** - true to set high priority for the fetch task, false - to set normal priority.

## void intersectionAsync ( bool critical = false )

Performs tracing along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*intersectionForce()*](#intersectionForce_int) method.
### Arguments

- *bool* **critical** - true to set high priority for the intersection task, false - to set normal priority.

## void intersectionAsync ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , bool critical = false )

Performs tracing along the line from the **p0** point to the **p1** point to find an intersection with the terrain in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_void) method). For an instant result use the [*intersectionForce()*](#intersectionForce_int) method.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p0** - Coordinates of the **p0** point.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **p1** - Coordinates of the **p1** point.
- *bool* **critical** - true to set high priority for the intersection task, false - to set normal priority.

## void fetchForce ( const Vector < Ptr < LandscapeFetch >> & fetches )

Fetches (batch) terrain data in forced mode for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void). You can use the [*fetchAsync()*](#fetchAsync_VECLandscapeFetch_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cpp.md)>> &* **fetches** - List of fetch requests to be completed.

## void intersectionForce ( const Vector < Ptr < LandscapeFetch >> & fetches )

Performs tracing (batch) along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in forced mode. You can use the [*intersectionAsync()*](#intersectionAsync_VECLandscapeFetch_int_void) method to reduce load, when an instant result is not required.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cpp.md)>> &* **fetches** - List of fetch requests to be completed.

## void fetchAsync ( const Vector < Ptr < LandscapeFetch >> & fetches , bool critical = false )

Fetches (batch) terrain data for the point specified by the [*setFetchPosition()*](#setFetchPosition_Vec2_void) in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_VECLandscapeFetch_void) method). For an instant result use the [*fetchForce()*](#fetchForce_VECLandscapeFetch_void) method.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cpp.md)>> &* **fetches** - List of fetch requests to be completed.
- *bool* **critical** - true to set high priority for the fetch task, false - to set normal priority.

## void intersectionAsync ( const Vector < Ptr < LandscapeFetch >> & fetches , bool critical = false )

Performs tracing (batch) along the line from the **p0** point specified by the [*setIntersectionPositionBegin()*](#setIntersectionPositionBegin_Vec3_void) to the **p1** point specified by the [*setIntersectionPositionEnd()*](#setIntersectionPositionEnd_Vec3_void) to find an intersection with the terrain in [asynchronous mode](#example_async) (the corresponding task shall be put to the queue, to wait until the result is obtained use the [*wait()*](#wait_VECLandscapeFetch_void) method). For an instant result use the [*intersectionForce()*](#intersectionForce_VECLandscapeFetch_void) method.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cpp.md)>> &* **fetches** - List of fetch requests to be completed.
- *bool* **critical** - true to set high priority for the intersection task, false - to set normal priority.

## void wait ( )

Waits for completion of the fetch operation. As the operation is completed you can obtain necessary data via *get*()* methods.
## void wait ( const Vector < Ptr < LandscapeFetch >> & fetches )

Waits for completion of the specified fetch operations. As the operations are completed you can obtain necessary data via *get*()* methods.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeFetch](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cpp.md)>> &* **fetches** - List of fetch requests to be completed.
