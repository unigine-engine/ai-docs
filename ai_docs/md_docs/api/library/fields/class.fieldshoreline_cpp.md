# FieldShoreline Class (CPP)

**Header:** #include <UnigineFields.h>

**Inherits from:** Field


This class is used to create and modify a [field shoreline](../../../objects/effects/fields/field_shoreline/index.md). The field is applied to [global water](../../../api/library/objects/class.objectwaterglobal_cpp.md) and helps to create swashes near the shores and applies the wetness effect on objects near the shoreline.


> **Notice:** A field shoreline object will affect water only if the *FieldShoreline interaction* option is enabled on the *States* tab of the [water_global_base](../../../content/materials/library/water_global_base/index.md) material.


### Creating a Shoreline Field


> **Notice:** When creating a FieldShoreline object you should specify a shoreline texture for as this object doesn't have any default texture.


```cpp
// create a new instance of the FieldShoreline class and set its transformation
FieldShorelinePtr shoreline = FieldShoreline::create();
shoreline->setTransform(Mat4(1));
// set the size of the field
shoreline->setSize(vec3(4096.0f, 4096.0f, 512.0f));
// set the path to the shoreline texture
shoreline->setTexturePath("unigine_project/textures/shorelines/shoreline_0.texture");

```


## FieldShoreline Class

### Members

## void setTexture ( const Ptr < Texture >& texture )

Sets a new shoreline texture used by GPU for FieldShoreline.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)>&* **texture** - The shoreline texture instance.

## Ptr < Texture > getTexture () const

Returns the current shoreline texture used by GPU for FieldShoreline.
### Return value

Current shoreline texture instance.
## void setTexturePath ( const char * path )

Sets a new path to the FieldShoreline's texture.
### Arguments

- *const char ** **path** - The path to the FieldShoreline's texture.

## const char * getTexturePath () const

Returns the current path to the FieldShoreline's texture.
### Return value

Current path to the FieldShoreline's texture.
## void setSize ( const Math:: vec3 & size )

Sets a new vec3 size vector of FieldShoreline.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The vec3 size vector of FieldShoreline. The default value is (**512.0f**, **512.0f**, **512.0f**).

## Math:: vec3 getSize () const

Returns the current vec3 size vector of FieldShoreline.
### Return value

Current
vec3 size vector of FieldShoreline.


The default value is (**512.0f**, **512.0f**, **512.0f**).


## Event<> getEventProgress () const

event triggered when shoreline is baked ([bakeWaterLevel()](#bakeWaterLevel_Image_int) is called). This event is called for each baking iteration, and the value from 0 to 1 (where 1 equals to 100%) is passed to the event. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Progress event handler
void progress_event_handler()
{
	Log::message("\Handling Progress event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections progress_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventProgress().connect(progress_event_connections, progress_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventProgress().connect(progress_event_connections, []() {
		Log::message("\Handling Progress event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
progress_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection progress_event_connection;

// subscribe to the Progress event with a handler function keeping the connection
publisher->getEventProgress().connect(progress_event_connection, progress_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
progress_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
progress_event_connection.setEnabled(true);

// ...

// remove subscription to the Progress event via the connection
progress_event_connection.disconnect();

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

	// A Progress event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Progress event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventProgress().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId progress_handler_id;

// subscribe to the Progress event with a lambda handler function and keeping connection ID
progress_handler_id = publisher->getEventProgress().connect(e_connections, []() {
		Log::message("\Handling Progress event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventProgress().disconnect(progress_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Progress events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventProgress().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventProgress().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static FieldShorelinePtr create ( )

Default constructor. Creates a FieldShoreline instance with the default size vec3(**512.0f, 512.0f, 512.0f**).
> **Notice:** By default, a shoreline texture is empty. Specify it after creating the FieldShoreline by using an appropriate function.


## int bakeWaterLevel ( const Ptr < Image > & image )

Bakes shoreline for the current water level of the global water object and puts it to the specified image. This method generates a shoreline texture by finding intersections of the [Global Water](../../../objects/objects/water/water_object.md) object with terrains ([Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) and [Terrain Global](../../../objects/objects/terrain/terrain_global/index.md))
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image instance to which the shoreline for the current water level is to be baked.

### Return value

**1** if the shoreline is baked successfully; otherwise, **0**.
## int setTextureImage ( const Ptr < Image > & image )

Sets the given image as the shoreline texture of the FieldShoreline.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image instance with a shoreline texture for the FieldShoreline.

## int getTextureImage ( const Ptr < Image > & image ) const

Grabs the texture for the FieldShoreline (already loaded to GPU) and saves it into the given Image instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Image](../../../api/library/common/class.image_cpp.md)> &* **image** - Image instance into which the texture will be saved.

### Return value

**1** if the texture has been grabbed successfully; otherwise, **0**.
## int createShorelineDistanceField ( const Ptr < Texture > & texture , int shoreline_radius , int blur_radius , int downsample_resolution )

Creates a shoreline distance field with the specified parameters and puts it to the specified Image.
```text
float shoreline_radius = 64;
int blur_radius = 8;
int downsample_resolution = 128;
Texture distance_field = new Texture();
field.createShorelineDistanceField(distance_field,shoreline_radius,blur_radius,downsample_resolution);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Texture](../../../api/library/rendering/class.texture_cpp.md)> &* **texture** - Texture to which the shoreline distance field will be put.
- *int* **shoreline_radius** - Radius of the shoreline.
- *int* **blur_radius** - Radius of the blurred area.
- *int* **downsample_resolution** - Shoreline resolution.

### Return value

**1** if the field was created successfully; otherwise, **0**.
## static int type ( )

Returns the type of the object.
### Return value

[FieldShoreline](../../../api/library/nodes/class.node_cpp.md#FIELD_SHORELINE) type identifier.
