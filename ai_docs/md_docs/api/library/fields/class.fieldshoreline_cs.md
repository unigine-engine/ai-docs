# FieldShoreline Class (CS)

**Inherits from:** Field


This class is used to create and modify a [field shoreline](../../../objects/effects/fields/field_shoreline/index.md). The field is applied to [global water](../../../api/library/objects/class.objectwaterglobal_cs.md) and helps to create swashes near the shores and applies the wetness effect on objects near the shoreline.


> **Notice:** A field shoreline object will affect water only if the *FieldShoreline interaction* option is enabled on the *States* tab of the [water_global_base](../../../content/materials/library/water_global_base/index.md) material.


### Creating a Shoreline Field


> **Notice:** When creating a FieldShoreline object you should specify a shoreline texture for as this object doesn't have any default texture.


```csharp
// create a new instance of the FieldShoreline class and set its transformation
FieldShoreline shoreline = new FieldShoreline();
shoreline.setTransform(Mat4(1));
// set the size of the field
shoreline.setSize(vec3(4096.0f, 4096.0f, 512.0f));
// set the path to the shoreline texture
shoreline.setTexturePath("unigine_project/textures/shorelines/shoreline_0.texture");

```


## FieldShoreline Class

### Properties

## Texture Texture

The shoreline texture used by GPU for FieldShoreline.
## string TexturePath

The path to the FieldShoreline's texture.
## vec3 Size

The vec3 size vector of FieldShoreline.
## 🔒︎ Event EventProgress

The event triggered when shoreline is baked ([BakeWaterLevel](#bakeWaterLevel_Image_int) is called). This event is called for each baking iteration, and the value from 0 to 1 (where 1 equals to 100%) is passed to the event. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Progress event handler
void progress_event_handler()
{
	Log.Message("\Handling Progress event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections progress_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventProgress.Connect(progress_event_connections, progress_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventProgress.Connect(progress_event_connections, () => {
		Log.Message("Handling Progress event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
progress_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Progress event with a handler function
publisher.EventProgress.Connect(progress_event_handler);

// remove subscription to the Progress event later by the handler function
publisher.EventProgress.Disconnect(progress_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection progress_event_connection;

// subscribe to the Progress event with a lambda handler function and keeping the connection
progress_event_connection = publisher.EventProgress.Connect(() => {
		Log.Message("Handling Progress event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
progress_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
progress_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
progress_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Progress events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventProgress.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventProgress.Enabled = true;

```

</details>

### Members

---

## FieldShoreline ( )

Default constructor. Creates a FieldShoreline instance with the default size vec3(**512.0f, 512.0f, 512.0f**).
> **Notice:** By default, a shoreline texture is empty. Specify it after creating the FieldShoreline by using an appropriate function.


## int BakeWaterLevel ( Image image )

Bakes shoreline for the current water level of the global water object and puts it to the specified image. This method generates a shoreline texture by finding intersections of the [Global Water](../../../objects/objects/water/water_object.md) object with terrains ([Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) and [Terrain Global](../../../objects/objects/terrain/terrain_global/index.md))
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image instance to which the shoreline for the current water level is to be baked.

### Return value

**1** if the shoreline is baked successfully; otherwise, **0**.
## int SetTextureImage ( Image image )

Sets the given image as the shoreline texture of the FieldShoreline.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image instance with a shoreline texture for the FieldShoreline.

## int GetTextureImage ( Image image )

Grabs the texture for the FieldShoreline (already loaded to GPU) and saves it into the given Image instance.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image instance into which the texture will be saved.

### Return value

**1** if the texture has been grabbed successfully; otherwise, **0**.
## int CreateShorelineDistanceField ( Texture texture , int shoreline_radius , int blur_radius , int downsample_resolution )

Creates a shoreline distance field with the specified parameters and puts it to the specified Image.
```text
float shoreline_radius = 64;
int blur_radius = 8;
int downsample_resolution = 128;
Texture distance_field = new Texture();
field.createShorelineDistanceField(distance_field,shoreline_radius,blur_radius,downsample_resolution);

```


### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture to which the shoreline distance field will be put.
- *int* **shoreline_radius** - Radius of the shoreline.
- *int* **blur_radius** - Radius of the blurred area.
- *int* **downsample_resolution** - Shoreline resolution.

### Return value

**1** if the field was created successfully; otherwise, **0**.
## static int type ( )

Returns the type of the object.
### Return value

[FieldShoreline](../../../api/library/nodes/class.node_cs.md#FIELD_SHORELINE) type identifier.
